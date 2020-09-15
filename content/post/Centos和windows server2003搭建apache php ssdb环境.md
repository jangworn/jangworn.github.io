---
title: Centos和windows server2003搭建apache php ssdb环境
date: 2017-03-02 23:40:58
tags: ["httpd","php","mysql","windows2003"]
---

### centos安装 apache php mysql
yum install httpd
yum install php php-mysql
yum install mysql mysql-server
vi /etc/httpd/conf/httpd.conf
/etc/init.d/httpd start
/etc/init.d/mysqld start

<!-- more -->
### centos安装ssdb
yum install wget
wget --no-check-certificate https://github.com/ideawu/ssdb/archive/master.zip
yum install unzip zip
umzip master.zip
cd ssdb-master
yum install autoconf
yum install g++ gcc+ gcc-c++
make
make install
/usr/local/ssdb/ssdb-server -d /usr/local/ssdb/ssdb.confps aux | grep ssdb

如果修改apache的端口需要改selinux配置
vi /etc/selinux/config
将SELINUX=enforcing改为SELINUX=disabled

chkconfig mysqld on
chkconfig httpd on


/var/www/html/ssdb-master/tools/ssdb.sh /etc/init.d/ssdb
/etc/init.d/ssdb
/etc/init.d

vi ssdb
修改ssdb.conf路径
chkconfig --add ssdb
chkconfig ssdb on

### windows
远程连接windwos 2003 服务器
下载php-5.4.22-nts-Win32-VC9-x86.zip
下载httpd-2.2.25-win32-x86-no_ssl.msi
打开控制面板->添加或删除windows组件->应用程序服务器->关闭asp.net和iis

打开“本地连接状态”对话框，点击“属性”按钮。
在弹出的“本地连接属性”对话框中点击“高级”选项卡。

在弹出的“高级设置”对话框中的列外选项卡中，

添加10880，单击“添加端口”按钮。
名称和端口都写10880
修改apache配置

