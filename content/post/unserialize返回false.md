---
title: unserialize返回false
date: 2015-04-22 11:48:44
tags:  
---
```
<?php
	function mb_unserialize($serial_str) {
	 $serial_str= preg_replace(‘!s:(\d+):”(.*?)”;!se’, “‘s:’.strlen(‘$2′).':\”$2\”;'”, $serial_str );
	 $serial_str= str_replace(“\r”, “”, $serial_str);
	 return unserialize($serial_str);
	}
```
