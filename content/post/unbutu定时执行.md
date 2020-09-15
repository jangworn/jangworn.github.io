---
title: unbutu定时执行
date: 2015-04-22 11:48:44
tags:  
---
例子： 每分钟执行10.php 并把输出结果输出到showtime.log
	  crontab -e
 	  */1 * * * * php /var/www/html/10.php >> /var/www/html/showtime.log 