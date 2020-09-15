---
title: 修改linux默认语言
date: 2015-07-15 11:48:44
tags:  
---
用vi(或nano等文本编辑器)打开 /etc/default/locale 文件

将原来的配置内容修改为

LANG=”en_US.UTF-8″

LANGUAGE=”en_US:en”

再在终端下运行：

locale-gen -en_US:en

注销或重启后生效
