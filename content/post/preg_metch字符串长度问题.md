---
title: preg_metch字符串长度问题
date: 2014-07-11 14:56:44
tags:
---

今天抓一个网页匹配内容出问题，仔细检查规则并无问题，删掉要匹配的内容一大半就可以，后来一搜索是
backtrack_limit的问题，在代码前面加如下代码就ok了

ini_set('pcre.backtrack_limit', 999999);
ini_set('pcre.recursion_limit', 99999);
ini_set('memory_limit', '64M');
