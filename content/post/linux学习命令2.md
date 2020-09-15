---
title: linux学习命令2
date: 2017-05-29 11:48:44
tags:  
---

重设mysql密码
wget http://soft.vpser.net/lnmp/ext/reset_mysql_root_password.sh


sh reset_mysql_root_password.sh

sudo ln -s 源文件 目标文件  //软连接
<!--more-->
git fetch origin master  //远程master下载最新到本地master
git log -p master..origin/master //比较差别
git merge origin/master  //合并
git pull origin master //远程合并到本地
mongoclient(host,username,paddword,port,array(slave-ok:true))

### 安装composer
curl -sS https://getcomposer.org/installer | php
mv composer.phar /usr/local/bin/composer

### 安装lnmp
wget -c http://soft.vpser.net/lnmp/lnmp1.4.tar.gz && tar zxf lnmp1.4.tar.gz && cd lnmp1.4 && ./install.sh lnmp

### tika
wget http://apache.fayea.com/tika/tika-app-1.16.jar
java -jar tika-app-1.16.jar  --html 基本信息.docx

### 解压与压缩
xz -d *.tar.sz
tar -xvf *.tar

tar -zcvf *.tar.gz /var/aaa
tar -zxvf *.tar.gz

unzip *.zip
unzip -v *.zip //查看目录但不解压

zip *.zip /var/aaa

### 递归创建目录456
mkdir /var/www/123/456 -pv

### find
find . -name "*" -type f -size 0c //查找大小为0文件
find . -name "*" -type f -size 0c | xargs -n 1 rm -f //删除空文件
find . -name "*" -type f -size 1024c | xargs -n 1 rm -f //删除指定大小
find -type d -empty  //找出空文件夹
find . -name "shuaige.txt" -exec ls {} ; //列出搜索到的文件
find . -name "shuaige.txt" -exec rm -f {} ; //批量删除
find . -name "shuaige.txt" -ok rm -rf {} ;  //删除前有提示
find . -name "test" -type d -exec rm -rf {} ; //删除当前目录下面所有 test 文件夹下面的文件
find . -name '.svn' -exec rm -rf {} ; //删除文件夹下面的所有的.svn文件