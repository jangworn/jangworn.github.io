---
title: 开启gomod,配置goproxy
date: 2020-01-03 23:40:58
tags: go proxy
---

1. 编辑 MAC 电脑环境  
   vi ~/.bash_profile
2. 增加 2 行  
   export GO111MODULE=on  
   export GOPROXY=https://goproxy.cn
3. 使配置生效  
   souce ~/.bash_profile
