---
title: 基于Hexo的个人博客静态网站迁移到Hugo并定制theme
date: 2020-09-15 16:16:05
tags: ["hexo","hugo","theme"]
---

> 迁移的原因：Hugo生成静态页面速度飞快，相比基于node.js的Hexo快太多了

## 首先安装Hugo
安装方式以及运行方式看官方网站：[gohugo.io](https://gohugo.io)，或者[gohugo.org](https://www.gohugo.org/)

## 博文md文件迁移
1. 把Hexo目录下的博文md文件拷贝到<font color="#1890ff">hugo运行目录/content/post</font>目录
2. 确保文件开头内容格式如下,否则title、date、tags可能会提取错误  
2.1  date的格式是YYYY-mm-dd, tags的格式是数组
```
---
title: 标题
date: 2020-09-15 16:16:05
tags: ["hexo","hugo","theme"]  
---
```

## theme定制
#### 以官网推荐主题[hyde](https://github.com/spf13/hyde)为例
```
cd themes
git clone https://github.com/spf13/hyde.git
#目录结构如下
├── CHANGELOG.md
├── LICENSE.md
├── README.md
├── archetypes
│   └── default.md
├── go.mod
├── images
│   ├── screenshot.png
│   └── tn.png
├── layouts
│   ├── 404.html
│   ├── _default
│   │   ├── baseof.html
│   │   ├── list.html
│   │   └── single.html
│   ├── index.html
│   └── partials
│       ├── head.html
│       ├── head_fonts.html
│       ├── hook_head_end.html
│       └── sidebar.html
├── static
│   ├── apple-touch-icon-144-precomposed.png
│   ├── css
│   │   ├── hyde.css
│   │   ├── poole.css
│   │   ├── print.css
│   │   └── syntax.css
│   └── favicon.png
└── theme.toml
```
#### 增加搜索功能
* 参考网上分享的方法，使用fuse.min.js
#### 修改css
#### 增加翻页功能
* layouts/index.html #增加内容
```
{{ $paginator := .Paginate (where .Data.Pages "Type" "post") }}
{{ range $paginator.Pages }}
    {{ .Render "index" }}
    {{ end }}
{{ partial "pagination.html" $paginator }}
```
* layouts/partials/pagination.html #增加模板文件
```
<nav class="pagination">
	{{if .HasPrev}}
	    <a class="newer-posts" href="{{ .Prev.URL }}">&larr; 上一页</a>
	{{end}}
	<span class="page-number">Page {{ .PageNumber }} of {{.TotalPages}}</span>
	{{if .HasNext}}
	    <a class="older-posts" href="{{ .Next.URL }}">下一页 &rarr;</a>
	{{end}}
</nav>
```

## 定制theme后的目录结构
* theme以开源[hugo-theme-ling](https://github.com/jangworn/hugo-theme-ling)
```
├── LICENSE
├── README.md
├── archetypes
│   └── default.md
├── images
│   └── theme.png
├── layouts
│   ├── 404.html
│   ├── _default
│   │   ├── baseof.html #base模板
│   │   ├── index.json  #搜索要用到
│   │   ├── list.html   #tag列表页
│   │   └── single.html #博文详情页
│   ├── index.html
│   └── partials
│       ├── footer.html #网站footer
│       ├── head.html   #网站header
│       ├── pagination.html #翻页
│       └── sidebar.html #sidebar
├── static
│   ├── css
│   │   └── style.css #style
│   ├── favicon.png
│   ├── img
│   └── js
│       ├── fuse.min.js #搜索要用到
│       └── search.js   #搜索要用到
└── theme.toml
```
