---
title: ionic创建app入门
date: 2015-07-29 11:48:44
tags:  
---

	  linux
	  wget nodejs.tgz
	  ls -ls /usr/nodejs/bin/node /usr/bin/node
	  ls -ls /usr/nodejs/bin/npm /usr/bin/npm

	  npm install -g ionic cordova ionic
	  ionic start myapp tabs //创建tab
	  cd myapp
	  ionic setup sass
	  ionic serve 在浏览器里运行

	  //android里运行
	  ionic platform add android
	  ionic build android
	  ionic run android