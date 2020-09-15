---
title: solr使用
date: 2015-05-13 11:48:44
tags:  
---

下载：wget http://apache.fayea.com/lucene/solr/5.1.0/solr-5.1.0.zip

unzip -q solr-5.1.0.zip

cd solr-5.0.0.zip

启动solr: bin/solr start -p 8983

新建core name为：new_core

复制/var/www/solr-5.1.0/server/solr/configsets/basic_configs/ 目录下的conf和lang 到/var/www/solr-5.1.0/server/solr/new_core

打开浏览器localhost:8983 新建core

demo

修改conf/schema.xml 在fields下添加

	  <field name="song_id" type="string" indexed="true" stored="true" required="true" />
   	<field name="song_name" type="text_general" indexed="true" stored="true" omitNorms="true" termVectors="true" />
   	<field name="space_song_name" type="text_general" indexed="true" stored="true" omitNorms="true" termVectors="true" />
  	 <field name="hot_num" type="long" indexed="true" stored="true" omitNorms="true" termVectors="true" />
	把<uniqueKey>id</uniqueKey>
	改成
	<uniqueKey>song_id</uniqueKey>
	<defaultSearchField>song_name</defaultSearchField>
