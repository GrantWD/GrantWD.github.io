---
layout: post
title: 'post请求获取body问题'
subtitle: 'fetch中body数据类型问题，头部设置'
date: 2018-09-12
categories: nodejs
tags: javascript nodejs express 
---


#在express服务端配置
```javascript
	var bodyParse = require('body-parser');
	var multer = require('multer');
	
	app.use(bodyParse.urlencoded({extended:true}))
	app.use(bodyParser.json())
	app.use(multer())

	// 在方法中可以使用req.body获得数据
```
#客户端配置
```javascript
	fetch('http://localhost:3000/add',{
		method:'POST',
		// 必须设置正确的请求头部否则服务端拿不到数据，设置的格式必须和body中书写个格式相同
		headers:{
			"Content-Type": "application/x-www-form-urlencoded"
		},
		// body中的数据格式必须正确
		body:"key=1"

	})
```

#get请求
将查询字符串参数追加到URL的末尾，将信息发送到服务器。
## 常见的问题：
	- 查询字符中的每一个参数的名称和值都必须使用encodeURIComponent()进行编码，然后才可以放到URL的末尾，而且所有的名值对都必须有(&)分隔
```javascript
	function addURLParam(url,name,value){
		var url = url;
		// 没有找到就在后面添加一个问号，开始添加参数，如果有问号，那么表示有键值对，那么就在url后面添加一个&
		url += (url.indexOf("?") == -1 ? "?" : "&")
		url += encodeURIComponent(name) + "=" + encodeURIComponent(value);
		return url;
	}
```
#post请求
POST请求是将数据作为请求体来提交到服务器,POST请求体可以包含很多的数据，而且格式没有限制
POST请求在AJAX中需要放在send中来发送到服务器，传入的数据需要格式化，在传递到后端，
- 首先将Content-Type设置为application/x-www-form-urlencoded,表单提交内容的类型，POST请求的数据格式和GET请求的格式向

##问题，请求类型设置为JSON时候的问题
在正式跨域请求之前，浏览器会根据需要，发起一个PerFlight(也就是Option请求),用来让服务器端返回允许的方法(比如get/post),被跨域访问的Origin(来源，或者域)，还有是否需要Credentials（认证信息）
POST请求时Content-Type的取值只能是
- application/x-www-form-urlencoded 
- multipart/form-data 
- text/plain

#### 解决方案
在服务器端设置
```javascript
	 res.header("Access-Control-Allow-Headers", "X-Requested-With,Content-Type")
	 // 设置允许的头部信息
```
前端设置
```javascript
	headers:{
		"Content-Type":application/json;charset=utf-8
	}
	对象必须同JSON.stringify(obj)，解析才可以通过body发送，否则服务器端是不能解析的
```

