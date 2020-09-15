---
title: nginx和docker负载均衡
date: 2017-09-09 15:48:44
tags: docker nginx
---

1. docker安装nginx镜像
docker pull nginx
2. 主机新建2个目录并添加index.html
/home/wwwroot/test1/index.html  /home/wwwroot/test2/index.html
<!-- more -->
3. 新建2个容器
docker run --name nginx-test1 -d -p 8081:80 -v /home/wwwroot/test1:/usr/share/nginx/html nginx
docker run --name nginx-test2 -d -p 8082:80 -v /home/wwwroot/test2:/usr/share/nginx/html nginx
4. 修改配置
vim /usr/local/nginx/conf/nginx.conf
在http{}添加
```
upstream ngtest {
    server 127.0.0.1:8081 weight=1;
    server 127.0.0.1:8082 weight=2;
}
```
在server{}添加
```
location / {
    root /usr/share/nginx/html;
    index index.html;
    proxy_pass http://ngtest;
} 
```
主机重启nginx
