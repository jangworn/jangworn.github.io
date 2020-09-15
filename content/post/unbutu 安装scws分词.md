---
title: unbutu 安装scws分词
date: 2014-08-07 11:48:44
tags:  
---
	wget http://www.ftphp.com/scws/down/scws-1.1.3.tar.bz2   //源码包

　　wget http://www.ftphp.com/scws/down/scws-dict-chs-utf8.tar.bz2  //utf8词典，

　　wget http://www.ftphp.com/scws/down/scws-dict-chs-gbk.tar.bz2

　　[root@localhost src]# tar xjvf scws-1.1.3.tar.bz2

　　[root@localhost src]# cd scws-1.1.3

　　编译scws：

　　[root@localhost scws-1.1.3]# ./configure –prefix=/usr/local/scws

　　[root@localhost scws-1.1.3]# make

　　[root@localhost scws-1.1.3]# make install

　　[root@localhost scws-1.1.3]# ls -al /usr/local/scws/lib/libscws.la  //看看有没有这个文件，如果有就说明安装成功了。

　　[root@localhost scws-1.1.3]# /usr/local/scws/bin/scws -h  //这个也是看看安装成功了没有，如果看到下面输出，也说明安装成功。

　　scws (scws-cli/1.1.3)

　　Simple Chinese Word Segmentation – Command line usage.

　　Copyright (C)2007 by hightman.

　　安装中文分词的php扩展：

　　安装此扩展要求您的 php 和系统环境安装了相应的 autoconf automake 工具及 phpize 。

　　[root@localhost src]# tar xjvf scws-dict-chs-utf8.tar.bz2 -C /usr/local/scws/etc //把utf8词典安装到scws指定的目录下。

　　1）.进入源码目录的 phpext/ 目录

　　[root@localhostcd ~]# cd /usr/local/src/scws-1.1.3/phpext/

　　2）.执行 phpize （在PHP安装目录的bin/目录下）

　　[root@localhost phpext]# /usr/local/php/bin/phpize

　　#Configuring for:

　　#PHP Api Version:         20090626

　　#Zend Module Api No:      20090626

　　#Zend Extension Api No:   220090626

　　3）.进行编译

　　[root@localhost phpext]#

     ./configure --with-scws=/usr/local/scws
　　[root@localhost phpext]# make

　　[root@localhost phpext]# make install

　　4）. 找到php.ini的位置，并修改和加入内容

　　[root@localhost phpext]# vi /etc/php5/apache2/php.ini

　　加上

　　[scws]

　　extension = scws.so

　　scws.default.charset = utf8

　　scws.default.fpath   = /usr/local/scws/etc

　　[root@localhost phpext]#php -m  //执行 php -m 就能看到 scws 了或者在 phpinfo() 中 scws 的相关部分

　　重启Apache