---
title: centOS安装docker以及进阶
date: 2017-12-02 23:40:58
tags: docker
---

### 安装 docker

yum install -y yum-utils  
yum-config-manager --add-repo https://download.docker.com/linux/centos/docker-ce.repo
yum install docker-ce

- 启动 docker

service docker start

- 设置 docker 开机启动

systemctl enable docker

#### docker 迁移目录

1. 停止 docker 服务  
   systemctl stop docker
2. 编辑 dameon.json  
   vi /etc/docker/daemon.json
3. 增加如下内容（/home 是空间足够）

```json
{
  "graph": "/home/docker"
}
```

4. 移动 docker 默认目录到目标目录  
   mv /var/lib/docker/\* /home/docker/
5. 重新加载  
   systemctl daemon-reload
6. 启动 docker 服务  
   systemctl start docker
7. 查看 docker info，看目录是否修改成功  
   docker info

#### docker 迁移目录

1. 停止 docker 服务  
   systemctl stop docker
2. 编辑 dameon.json  
   vi /etc/docker/daemon.json
3. 增加如下内容（/home 是空间足够）

```json
{
  "graph": "/home/docker"
}
```

4. 移动 docker 默认目录到目标目录  
   mv /var/lib/docker/\* /home/docker/
5. 重新加载  
   systemctl daemon-reload
6. 启动 docker 服务  
   systemctl start docker
7. 查看 docker info，看目录是否修改成功  
   docker info

#### 修改现有容器的目录映射或端口

1. 停止 docker 服务  
   systemctl stop docker
2. 查看 docker 目录  
   df -lh
3. 进入容器目录  
   cd /disk01/docker/containers/容器 id.....
4. 修改以下 2 个配置文件  
   vi hostconfig.json  
   vi config.v2.json
5. 启动 docker 服务  
   systemctl start docker
6. 启动容器，看端口映射和目录是否修改成功
   docker start 容器 id
