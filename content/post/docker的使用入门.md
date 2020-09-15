---
title: docker入门
date: 2017-09-02 23:40:58
tags: docker
---

### 系统 linuix-ubuntu

1. 安装 docker
   apt install docker
2. 创建 ubuntu 镜像
   docker pull ubuntu
3. 运行容器
   docker run -p 80:80 -v /var/www:/var/www -d ubuntu
4. 进入容器
   docker exec -it ubuntu /bin/bash
5. 查看镜像
   docker images
6. 导出容器
   docker ps -a
   docker export d66 > ubuntu.tar
7. 导入容器
   cat ubuntu.tar | docker import - ubuntu:latest
   docker run -d -v /data/wwwroot:/home/wwwroot -p 10022:22 -p 13306:3306 -p 443:443 -p 80:80 --name ubuntu ubuntu /sbin/sshd -D
