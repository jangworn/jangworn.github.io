---
title: nmon监控linux
date: 2015-07-23 11:48:44
tags:  
---
1. 安装nmon：apt-get install nmon
2. 生成10分钟的记录：nmon -s10 -c60 -f -m /var/www
3. 把记录文件下载到windows上
4. 访问https://www.ibm.com/developerworks/community/wikis/home?lang=en#!/wiki/Power%20Systems/page/nmon_analyser 下载
5. 用excel打开下载的xlsm文件
6. 点击Analyze nmon data按钮，打开下载的记录文件，生成之后保存
7. 打开生成的excel
