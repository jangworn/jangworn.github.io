---
title: linux学习命令1
date: 2015-05-29 11:48:44
tags:  
---

在某个文件中查找某一段内容
grep  -F php   01.php

在某个目录和子目录查找字符串出现的次数
grep -r  'print'  /var/www

查看进程
ps -ef
cd命令  切换用户目录 例如 /root

倒引号里的会当做shell命令执行
echo "this dir is  `pwd`"

逻辑与&&吧2个命令连在一起 从左到右 命令1&&命令2 如果命令1执行不成功则命令2不执行
逻辑或||吧2个命令连在一起 从左到右 命令1||命令2 如果命令1执行不成功则执行命令2 如果命令1执行成功则不执行命令2

ll -lh 
du -lh
