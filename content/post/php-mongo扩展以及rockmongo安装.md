---
title: php-mongo扩展以及rockmongo安装
date: 2014-10-09 10:56:44
tags:
---
启动mongo：bin/mongod -port 27017 –dbpath data/ –logpath log/mongodb.log

下载php-mongodb-driver: wget https://github.com/mongodb/mongo-php-driver/archive/master.zip

解压： unzip master.zip

进入目录：cd mongo-php-driver-master/

安装：

phpize

./configure

make install

添加extension=mongo.so到php.ini

重启apache ：/etc/init.d/apache2 restart

下载rockmongo

wget http://github.com/iwind/rockmongo/archive/master.zip

unzip master.zip
