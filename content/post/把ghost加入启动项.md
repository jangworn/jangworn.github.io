---
title: 把ghost加入启动项
date: 2014-11-07 11:48:44
tags:  
---
1.打开网站https://raw.github.com/TryGhost/Ghost-Config/master/init.d/ghost

2.复制内容

3.vi /etc/init.d/ghost 粘贴

4.修改GHOST_ROOT的值 /usr/local/nodejs/ghost

5.修改DAEMON的值 /usr/local/nodejs/bin/node

6.esc :q 保存

useradd -r ghost -U

chown -R ghost:ghost /usr/local/nodejs/ghost

chmod 755 /etc/init.d/ghost

$ sudo service ghost start

$ sudo service ghost stop

$ sudo service ghost restart

$ sudo service ghost status

为了让 Ghost 能在系统启动时同时启动，我们必须要将刚刚创建的初始化脚本注册为为启动项。 执行以下两个命令：

$ sudo update-rc.d ghost defaults

$ sudo update-rc.d ghost enable