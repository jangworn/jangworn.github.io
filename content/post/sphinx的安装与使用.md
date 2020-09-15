---
title: sphinx的安装与使用
date: 2014-08-06 11:48:44
tags:  
---
安装：apt-get install sphinxsearch

启动： /etc/init.d/sphinxsearch start

创建索引：indexer –all   或   indexer -c/etc/sphinxsearch/sphinx.conf –all –rotate

开启sphinxsearch功能

编辑/etc/default/sphinxsearch文件 将START=no 修改为 START=yes 用vi打开编辑就可以了

搜索: search -i test1 -q 刘德华