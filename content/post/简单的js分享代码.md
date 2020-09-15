---
title: 简单的js分享代码
date: 2015-02-09 11:48:44
tags:  
---
```PHP
function ToTencent(title,picUrl){

		var _t = encodeURI("【@xx："+title+"】");

		var _url = encodeURIComponent(document.location);

		var _appkey = encodeURI("xx");//你从腾讯获得的appkey

		var _pic = encodeURI(picUrl);//（例如：var _pic='图片url1|图片url2|图片url3....）

		var _site = '';//你的网站地址

		var _u = 'http://v.t.qq.com/share/share.php?url='+_url+'&appkey='+_appkey+'&site='+_site+'&pic='+_pic+'&title='+_t;

		window.open( _u,'', 'width=700, height=680, top=0, left=0, toolbar=no, menubar=no, scrollbars=no, location=yes, resizable=no, status=no' );

}

function ToSina(title,picUrl){

		var _t = encodeURI("【@xx："+title+"】");

		var _url = encodeURIComponent(document.location);

		var _appkey = encodeURI("xx");//你从微薄获得的appkey

		var _pic = encodeURI(picUrl);

		var _site = '';//你的网站地址

		var _u = 'http://service.weibo.com/share/share.php?url='+_url+'&appkey='+_appkey+'&pic='+_pic+'&title='+_t;

		window.open( _u,'', 'width=700, height=680, top=0, left=0, toolbar=no, menubar=no, scrollbars=no, location=yes, resizable=no, status=no' );

}

function Torenren(title,picUrl,description){

		var _t = encodeURI("【xx："+title+"】");

		var _url = encodeURIComponent(document.location);

		var _appkey = encodeURI("xx");//你从微薄获得的appkey

		var _pic = encodeURI(picUrl);

		var _site = '';//你的网站地址

		var _d = !description? encodeURI(title) : encodeURI(description);

		//var _u = 'http://share.renren.com/share/buttonshare.do?title='+_t+'&link='+_url+'&pic='+_pic;

		var _u = 'http://widget.renren.com/dialog/share?resourceUrl='+_url+'&srcUrl='+_url+'&title='+_t+'&pic='+_pic+'&description='+_d;

		window.open( _u,'', 'width=700, height=680, top=0, left=0, toolbar=no, menubar=no, scrollbars=no, location=yes, resizable=no, status=no' );

}

function Tozone(title,picUrl,description){

		var _t = encodeURI("【xx："+title+"】");

		var _url = encodeURIComponent(document.location);

		var _pic = encodeURI(picUrl);

		var _site = '';//你的网站地址

		var _d = !description? encodeURI(title) : encodeURI(description);

		var _u = 'http://sns.qzone.qq.com/cgi-bin/qzshare/cgi_qzshare_onekey?url='+_url+'&title='+_t+'&pics='+_pic+'&desc='+_d;

		window.open( _u,'', 'width=700, height=680, top=0, left=0, toolbar=no, menubar=no, scrollbars=no, location=yes, resizable=no, status=no' );
		
}
```