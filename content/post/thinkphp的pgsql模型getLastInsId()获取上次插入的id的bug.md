---
title: thinkphp的pgsql模型getLastInsId()获取上次插入的id的bug
date: 2014-06-23 14:48:44
tags: ["thinkphp","pgsql","getlastinsid"]
---

hinkPHP/Library/Think/Db/Driver 目录下的Pgsql.class.php 的123行

代码如下

```PHP
<?php
      /**
      * 用于获取最后插入的ID
      * @access public
      * @return integer
      */

      public function last_insert_id() {
        $query = "SELECT LASTVAL() AS insert_id";
        $result = pg_query($this-&gt;_linkID,$query);
        $arr = pg_fetch_array($result,null,PGSQL_ASSOC);
        //list($last_insert_id) = pg_fetch_array($result,null,PGSQL_ASSOC);
        pg_free_result($result);
        // return $last_insert_id;
        return $arr['insert_id'];
      }
```
注释部分 list($last_insert_id) = pg_fetch_array($result,null,PGSQL_ASSOC); 函数pg_fetch_array 返回的是关联数组  ，用list给变量赋值时返回null
