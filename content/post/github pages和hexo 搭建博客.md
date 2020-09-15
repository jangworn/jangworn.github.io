---
title: github pages和hexo 搭建博客
date: 2016-04-26 11:48:44
tags: ["github","pages","hexo","git","nodejs",]
---
## 新建github pages
1.注册github账号

2.verify邮箱，不然访问github page 404

3.新建项目 名称 用户名.github.io
4.在master新建index.html 输入内容 访问 用户名.github.io

<!-- more -->
## 安装hexo
1.安装nodejs  访问nodejs.org下载对应版本
2.安装git    访问git-scm.com/download下载（ 建议使用迅雷等下载工具）
3.进入nodejs安装目录新建一个文件夹，例如：hexo
4.win+r 输入cmd或者运行nodejs  command
5cd hexo 目录
npm install -g hexo
npm install hexo-server
hexo init
hexo generate/hexo g
hexo server/hexo s
浏览器访问localhost:4000

## git上传代码部署
运行git bash

cd hexo目录
git clone https://github.com/用户名/用户名.github.io.git

把hexo的public目录文件复制到用户名.github.io文件夹
git config --global user.name "github用户名"
git config --global user.email "github邮箱"
git add .
git commit -m "first"
git remote add origin https://github.com/用户名/用户名.github.io.git
git push origin master


## 绑定域名
百度云注册一个账号，登录后注册一个域名

控制台-》产品服务-》域名服务-》域名管理 -》点击注册的域名右边的解析-》添加解析->记录类型选择 CNAME ->记录值:用户名.github.io
