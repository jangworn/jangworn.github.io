---
title: Elasticsearch查询语句
date: 2018-01-02 23:40:58
tags: Elasticsearch
---

> 假设mysql有一个article表，字段:id,title,content,author,time(int类型),comment_count。同时Elasticsearch有个索引article和mysql的字段相同

#### 查看 article 内容

按照 time 降序排列，从 0 开始显示 20  
类似 mysql 的 sql 语句:  
```sql
select * from article order by time desc limit 0,20;
```
> kibana
```json
GET article/_search
{
  "query": {
    "match_all": {}
  },
  "sort": [
    {
      "time": {
        "order": "desc"
      }
    }
  ],
  "size": 20,
  "from": 0
}
```

#### 查找加入条件

类似 mysql 语句：  
```sql
select * from article where time > 1589252400 and author='john' order by time asc limit 20;
```
> kibana
```json
GET article/_search
{
  "size": 20,
  "sort": [
    {
      "time": {
        "order": "asc"
      }
    }
  ],
  "query": {
    "bool": {
      "filter": {
        "bool": {
          "must":[
             {
               "range":{
                 "time":{
                   "gt":1589252400
                 }
               }
             },
             {
               "term":{
                 "author":"john"
               }
             }

           ]

        }
      }
    }
  }
}
```

#### or 查询

类似 mysql 语句：  
```sql
select * from article where author='lucy' or author='john' ;
```
> kibana
```json
GET article/_search
{
  "query": {
    "bool": {
      "filter": {
        "bool": {
          "should":[
             {
               "term":{
                 "author":"john"
               }
             },
             {
               "term":{
                 "author":"lucy"
               }
             }
             ]

        }
      }
    }
  }
}
```

#### 聚合查询

1. 按照天聚合查询每天评论数最大的  
   类似 mysql 语句：  
```sql
SELECT FROM_UNIXTIME(time,'%Y-%m-%d') as date,MAX(comment_number) as max 
FROM `article`
GROUP BY FROM_UNIXTIME(time,'%Y-%m-%d') 
ORDER BY date;
```
> kibana
```json
GET article/_search
{
  "query": {

  },
  	"aggs":{
         "aggs":{
             "date_histogram":{
                 "field":"time",
                 "interval":"1d",
                 "format":"yyyy-MM-dd",
                 "time_zone":"Asia/Shanghai",
                 "script":{
                   "inline":"doc['time'].value * 1000",
                   "lang":"painless"
                 },
                 "min_doc_count":0
             },
             "aggs":{
                 "avg":{
                    "max" : {
                      "field" : "comment_number" }
                 }
             }
         }
     }
}
```

2. 按照 author 统计每个人写的文章平均评论数量  
   类似 mysql 语句：  
```sql
select author,AVG(comment_number) from article group by author
```
> kibana
```json
GET article/_search
{
  "query": {

  },
  "aggs": {
    "aggs": {
      "terms":{
        "field":"author",
        "size":999
      },
      "aggs":{
        "aggs":{
          "avg": {
            "field": "comment_number"
          }
        }
      }
    }
  }
}
```

3. 按照时间统计 author 的数量  
   类似 mysql 语句：
```sql  
SELECT FROM_UNIXTIME(time,'%Y-%m-%d') as date,count(DISTINCT author) as count 
FROM `article`
GROUP BY FROM_UNIXTIME(time,'%Y-%m-%d') ORDER BY date;
```
> kibana
```json
GET article/_search
{
  "query": {

  },
 "aggs":{
    "aggs":{
        "date_histogram":{
            "field":"time",
            "interval":"1d",
            "format":"yyyy-MM-dd",
            "time_zone":"Asia/Shanghai",
            "script":{"source":"doc['time'].value * 1000","lang":"painless"},
            "min_doc_count":0
        },
        "aggs":{
            "distinct":{
                "cardinality":{
                    "field":"author",
                    "precision_threshold":40000
                }
            }
        }
    }
  }
}
```
