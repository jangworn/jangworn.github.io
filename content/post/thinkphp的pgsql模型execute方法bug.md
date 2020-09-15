---
title: thinkphp的pgsql模型execute方法bug
date: 2014-06-23 14:56:44
tags: ["thinkphp","pgsql","execute",]
---

ThinkPHP/Library/Think/Db/Driver 目录下的Pgsql.class.php 的102行
代码如下：

```PHP
<?php
      public function execute($str) {
        $this->initConnect(true);
        if ( !$this->_linkID ) return false;
        $this->queryStr = $str;
        //释放前次的查询结果
        if ( $this->queryID ) $this->free();
        N('db_write',1);
        // 记录开始执行时间
        G('queryStartTime');
        $result =   pg_query($this->_linkID,$str);
        $this->debug();
        if ( false === $result ) {
          $this->error();
          return false;
          } else {
          $this->numRows = pg_affected_rows($result);
          if(stristr($str,'insert')){ //修改部分
             $this->lastInsID =   $this->last_insert_id();
          }

             return $this->numRows;
        }
    }
```    
注释部分 list($last_insert_id) = pg_fetch_array($result,null,PGSQL_ASSOC); 函数pg_fetch_array 返回的是关联数组  ，用list给变量赋值时返回null
