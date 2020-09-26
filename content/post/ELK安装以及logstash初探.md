---
title: ELK安装以及logstash自动收集日志文件和同步mysql数据初探
date: 2020-09-16 11:48:44
tags: ["Elasticsearch","Logstash","Kibana"]
---

## 安装
1. 下载elasticsearch并解压  
`wget https://artifacts.elastic.co/downloads/elasticsearch/elasticsearch-7.8.1-linux-x86_64.tar.gz`  
`tar -zxvf elasticsearch-7.8.1 && cd elasticsearch-7.8.1`  
1. 启动elasticsearch并解压  
`./bin/elasticsearch -d`
1. 下载kibana  
`wget https://artifacts.elastic.co/downloads/kibana/kibana-7.8.1-linux-x86_64.tar.gz`  
`tar -zxvf kibana-7.8.1-linux-x86_64.tar.gz && cd kibana-7.8.1-linux-x86_64`
1. 启动kibana  
`./bin/kibana` 

1. 下载logstash并解压   
`wget https://artifacts.elastic.co/downloads/logstash/logstash-7.8.1.tar.gz`  
`tar -zxvf logstash-7.8.1.tar.gz && cd logstash-7.8.1`

1. 下载mysql-connector-java并解压    
`wget https://dev.mysql.com/get/Downloads/Connector-J/mysql-connector-java-8.0.21.tar.gz`  
`tar -zxvf mysql-connector-java-8.0.21.tar.gz`


1. 新建logstash/config/conf/mysql.conf文件，配置如下
```conf
# 数据库
input {
  stdin {
  }
  jdbc {
    jdbc_driver_library => "/home/ling/logstash-7.8.1/mysql-connector-java-8.0.21-bin.jar"
    jdbc_driver_class => "com.mysql.jdbc.Driver"
    jdbc_connection_string => "jdbc:mysql://localhost:3306/test"
    jdbc_user => "root"
    jdbc_password => "111111"
    schedule => "* * * * *"
    statement => "select id,name,age from user"
    columns_charset => {
       "content" => "UTF-8"
    }
    type => "user"
  }
}

filter {
   if [type] == "user" {
       urldecode{
         all_fields=>true
       }
   }
}
output {
  if [type] == "user"{
  elasticsearch {
    hosts => "localhost:9200"
    index => "user"
    document_id => "%{id}"
    }
  }
}
```
8. 新建logstash/config/conf/log.conf文件，配置如下
```
#日志文件
input {
    file {
        path => "/home/ling/project/log/*.log"
        type => "runtime"
        start_position => "beginning" #从文件开始处读写
    }
}

filter {
   if [type] == "runtime" {
       urldecode{
         all_fields=>true
       }
   }
}
output{
    if [type] == "runtime"{

        elasticsearch {
          hosts=>["127.0.0.1:9200"]
          index => "runtime_log" #对日志进行索引归档
        }
    }
    stdout{codec => rubydebug}
}
```
9. 启动logstash  
`./bin/logstash -f config/conf` 


 