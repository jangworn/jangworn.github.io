---
title: 快速搭建nginx+php+mysql
date: 2015-07-15 11:48:44
tags:  
---
apt-get install nginx php5-fpm

vi /etc/nginx/sites-available/default


修改如下

listen 80;

root /var/www/html;

index index.html index.htm index.php;

location ~ \.php$ {

include fastcgi.conf;

fastcgi_pass unix:/run/php/php7.0-fpm.sock;
fastcgi_index index.php;
#        fastcgi_intercept_errors   on;
include fastcgi_params;

}
       




保存

ps aux | grep -c php-fpm

/etc/init.d/php-fpm restart

service nginx restart

vi /var/www/html/phpinfo.php

echo phpinfo();

apt-get install mysql-server php5-mysql

vi /etc/php5/fpm/php.ini

修改extension_dir = “/usr/lib/php5/20090626+lfs”

service nginx restart

service php-fpm restart

nginx启动失败： nginx -t查看配置文件是否出错
