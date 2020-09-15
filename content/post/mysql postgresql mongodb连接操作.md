---
title: mysql postgresql mongodb连接操作
date: 2015-06-03 11:48:44
tags:  
---

```PHP
	<?php

	header('Content-type:text/html;charset=utf-8');
	$conn = mysql_connect('localhost','root','111111');
	if(!$conn){
		die('');
	}
	mysql_select_db('imsl_media',$conn);
	mysql_query('set names utf8');
	$res = mysql_query('select * from imsl_singer limit 10');
	while($row = mysql_fetch_assoc($res)){
		var_dump($row);
	}
	//mongo
	$mongo = new mongo("mongodb://root:111111@localhost:27017");
	$db = $mongo->user;
	$table = $db->user_list;
	$sort['time'] = 1;
	$a = $table->find($where)->sort($sort)->limit(10)->skip(10);
	//postgresql
	$pg = pg_connect('host=localhost port=5443 dbname=imsl_media user=root password=bar');
	$res = pg_query($pg,'select * from imsl_singer limit 10');
	if(!$res){
		die('');
	}
	if(pg_num_rows($res)){
		while($row = pg_fetch_assoc($res)){
			var_dump($row);
		}
	}else{

	}
```

