---
title: siege并发
date: 2016-07-10 23:40:58
tags:
---

	  apt-get install siege
	  siege http://www.baidu.com -d1 -r10 -c1
	  -d1 //延迟1秒
	  -r10 //10次
	  -c1 //并发数

	  Transactions: 10 hits //访问次数
	  Availability: 100.00 % //成功次数
	  Elapsed time: 6.92 secs //测试用时
	  Data transferred: 0.25 MB //传输数据量
	  Response time: 0.09 secs //平均响应时间
	  Transaction rate: 1.45 trans/sec //每秒事务处理量
	  Throughput: 0.04 MB/sec //吞吐量
	  Concurrency: 0.13 //并发用户数
	  Successful transactions: 10 //成功传输次数
	  Failed transactions: 0 //失败传输次数
	  Longest transaction: 0.10 //最长响应时间
	  Shortest transaction: 0.08 //最短响应时间