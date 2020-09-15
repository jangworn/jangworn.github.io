---
title: memcached安装
date: 2015-06-02 11:48:44
tags:  
---

> 在内存使用效率上，如果使用简单的key-value存储，Memcached的内存利用率更高。而如果Redis采用hash结构来做key-value存储，由于其组合式的压缩，其内存利用率会高于Memcached。当然，这和你的应用场景和数据特性有关。
> 如果你对数据持久化和数据同步有所要求，那么推荐你选择Redis。因为这两个特性Memcached都不具备。即使你只是希望在升级或者重启系统后缓存数据不会丢失，选择Redis也是明智的。
> 当然，最后还得说到你的具体应用需求。Redis相比Memcached来说，拥有更多的数据结构，并支持更丰富的数据操作。通常在Memcached里，你需要将数据拿到客户端来进行类似的修改再set回去。这大大增加了网络IO的次数和数据体积。在Redis中，这些复杂的操作通常和一般的GET/SET一样高效。所以，如果你需要缓存能够支持更复杂的结构和操作，那么Redis会是不错的选择。

## 下载memcached

wget http://memcached.org/files/memcached-1.4.24.tar.gz

tar -zxvf memcached-1.4.24.tar.gz

mv memcached-1.4.24 /usr/local/memcached

cd /usr/local/memcached/

./configure && make && make test && sudo make install

./memcached -d -m 128 -p 11211 -u root

## 下载libmemcached

wget http://launchpad.net/libmemcached/1.0/1.0.18/+download/libmemcached-1.0.18.tar.gz

tar -zxvf libmemcached-1.0.18.tar.gz 

mv libmemcached-1.0.18 /usr/local/libmemcached

cd /usr/local/libmemcached/

./configure

make && make install

安装php memcache扩展

wget http://github.com/php-memcached-dev/php-memcached/archive/master.zip

unzip master.zip

cd php-memcached-master/

phpize

./configure

make && make install

修改php.ini

 vi /etc/php5/cli/php.ini

增加一行 extension=memcached.so


