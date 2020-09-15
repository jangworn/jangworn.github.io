---
title: nginx的pathinfo
date: 2017-05-16 11:48:44
tags:  nginx pathinfo
---

nginx -t 查看nginx启动失败原因
unknown directive “if(!-e”   if和(直接有空格
> 匹配nginx需要交给php-fpm执行的URI，先要允许pathinfo格式的URL能够被匹配到
> 所以要去掉$
> nginx文档中的匹配规则为：^(.+\.php)(.*)$
> 还有~ \.php这种写法 和 ~ \.php($|/)这种写法
> 都是差不多意思没啥严格区别
> 唯一区别就是有多个匹配php的location的话需要留意权重差异
```
location ~ ^(.+\.php)(.*)$ {
    root              /var/www/www.jjonline.cn/wwwRoot;
    fastcgi_pass   127.0.0.1:9000;
    fastcgi_index  index.php;
    ##增加 fastcgi_split_path_info指令，将URI匹配成PHP脚本的URI和pathinfo两个变量
    ##即$fastcgi_script_name 和$fastcgi_path_info
    fastcgi_split_path_info  ^(.+\.php)(.*)$;
    ##PHP中要能读取到pathinfo这个变量
    ##就要通过fastcgi_param指令将fastcgi_split_path_info指令匹配到的pathinfo部分赋值给PATH_INFO
    ##这样PHP中$_SERVER['PATH_INFO']才会存在值
    fastcgi_param PATH_INFO $fastcgi_path_info;
    ##在将这个请求的URI匹配完毕后，检查这个绝对地址的PHP脚本文件是否存在
    ##如果这个PHP脚本文件不存在就不用交给php-fpm来执行了
    ##否者页面将出现由php-fpm返回的:`File not found.`的提示
    if (!-e $document_root$fastcgi_script_name) {
        ##此处直接返回404错误
        ##你也可以rewrite 到新地址去，然后break;
        return 404;
    }
    fastcgi_param  SCRIPT_FILENAME  $document_root$fastcgi_script_name;
    include        fastcgi_params;
}
```