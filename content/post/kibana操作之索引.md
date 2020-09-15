---
title: kibana对索引相关操作
date: 2018-01-02 23:40:58
tags: Elasticsearch
---

#### 查看所有索引

```json
GET _cat/indices
```

#### 创建索引 article

```json
POST article/article/_mapping
{
  "article": {
    "properties": {
      "content": {
        "type": "text",
        "analyzer": "ngram_analyzer"
      },
      "title": {
        "type": "text",
        "analyzer": "ngram_analyzer"
      },
      "time": {
        "type": "date"
      },
      "author": {
        "type": "text"
      },

    }
  }
}
```

#### 查看 article 的 mapping

```json
GET article/article/_mapping
```

#### 删除索引 article 数据

```json
POST article/article/_delete_by_query
{
  "query": {
    "match_all": {}
  }
}
```

#### 删除索引 article

```json
DELETE article
```

#### 复制索引 article 到 article_new

```json
POST _reindex
{
  "conflicts": "proceed",
  "source": {
    "index": "article",
    "sort": {
      "time": "desc"
    }
  },
  "dest": {
    "index": "article_new",
    "op_type": "create"
  }
}
```
