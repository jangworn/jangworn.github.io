---
title: WIN7 64位系统安装JDK并配置环境变量
date: 2014-06-21 11:48:44
tags: win7 JDK
---
首先，下载JDK安装包，到官网http://www.oracle.com/technetwork/java/javase/downloads/index.html进行下载，点左边的Java Platform (JDK) 7u51进入下一个下载页面，

安装好后便是配置JDK的环境变量，在桌面上计算机点右键选属性，或是开始菜单计算机上点右键选属性， 左边点高级系统设置，点下边的环境变量，

在新弹出窗口上，点系统变量区域下面的新建按钮，弹出新建窗口，变量名为JAVA_HOME，变量值填JDK安装的最终路径，我这里装的地址是D:\Program Files\Java\jdk1.7.0_51，所以填D:\Program Files\Java\jdk1.7.0_51，点确定完成，

下面需要设置Path变量，由于系统本身已经存在这个变量，所以无需新建，在原本基本上添加JDK相关的，找到Path变量双击编辑，由于每个值之间用;符号间断，所以先在末尾加上;（注意是英文格式的，不要输其他符号空格等），加上;符号后在末尾加入%JAVA_HOME%\bin，点确定完成，

下面添加CLASSPATH变量，由于不存在，所以新建一个，变量名CLASSPATH，变量值%JAVA_HOME%lib\dt.jar;%JAVA_HOME%\lib\tools.jar，首尾不带空格的，点确定完成，至此环境变量配置完成，点确定关掉环境变量配置窗口。

上面步骤完成后，下面验证下是否配置成功，点开始运行输入cmd打开命令行窗口，输入java -version，显示版本1.7.0_51，输入javac -version，也显示1.7.0_51，说明JDK安装及环境变量配置成功。
