---
title: 在mac上打包
date: 2019-02-03 23:40:58
tags: 
---

### 在 mac 打包，在 linux 运行

CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build main.go

#### Golang 支持在一个平台下生成另一个平台可执行程序的交叉编译功能。

- Mac 下编译 Linux 平台的 64 位可执行程序：  
  CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build test.go

- 打包并指定输出二进制文件名  
  CGO_ENABLED=0 GOOS=linux GOARCH=amd64 go build -o run_some_script main.go

* Mac 下编译 Windows 平台的 64 位可执行程序  
  CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build test.go

#### Linux 下编译 Mac, Windows 平台的 64 位可执行程序：

CGO_ENABLED=0 GOOS=darwin GOARCH=amd64 go build test.go

CGO_ENABLED=0 GOOS=windows GOARCH=amd64 go build test.go

#### Windows 下编译 Mac, Linux 平台的 64 位可执行程序：

SET CGO_ENABLED=0SET GOOS=darwin3 SET GOARCH=amd64 go build test.go

SET CGO_ENABLED=0 SET GOOS=linux SET GOARCH=amd64 go build test.go

> 注：如果编译 web 等工程项目，直接 cd 到工程目录下直接执行以上命令

> GOOS：目标可执行程序运行操作系统，支持 darwin，freebsd，linux，windows

> GOARCH：目标可执行程序操作系统构架，包括 386，amd64，arm

> Golang version 1.5 以前版本在首次交叉编译时还需要配置交叉编译环境：
> CGO_ENABLED=0 GOOS=linux GOARCH=amd64 ./make.bash
> CGO_ENABLED=0 GOOS=windows GOARCH=amd64 ./make.bash
