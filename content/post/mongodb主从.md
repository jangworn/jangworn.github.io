---
title: mongodb主从
date: 2017-06-12 11:48:44
tags:  mongodb
---

1. 创建mongodb数据存放的文件夹

mkdir -p /mongodata/test/db27010
mkdir -p /mongodata/test/db27011
mkdir -p /mongodata/test/db27012
<!--more-->
2. 启动27010主

在启动命令中加入 master,该mongo服务即可作为主。
mongod --dbpath /mongodata/test/db27010 --port 27010 --master --logpath /mongodata/test/db27010/log.txt --fork

3. 启动27011、27012从

添加参数 --slave 作为从,通过--source localhost:27010来指定主的位置。
mongod --dbpath /mongodata/test/db27011 --port 27011 --slave --source localhost:27010 --logpath /mongodata/test/db27011/log.txt --fork
mongod --dbpath /mongodata/test/db27012 --port 27012 --slave --source localhost:27010  --logpath /mongodata/test/db27012/log.txt --fork


./bin/mongo --port 27010
use admin
db.system.users.find();
db.user.insert({'name':'root','password':'root',roles:[{role:'root',db:'admin'}]});

./bin/mongo --port 27011
use user;
rs.slaveOk();
db.user.find();

apt install php-dev php-pecl
pecl install mongodb

```
    echo "extension=mongodb.so" >> `php --ini | grep "Loaded Configuration" | sed -e "s|.*:\s*||"`
```
