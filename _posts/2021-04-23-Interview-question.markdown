---
layout: post
title:  "Web面试题汇总"
date:   2021-04-23 11:12:50
categories: IT
tags: Web 面试
excerpt: 记录自己知道的常见的面试题
mathjax: true
---

* content
{:toc}


# 当你在浏览器中输入 Google.com 并且按下回车之后发生了什么？
1. url解析,分析 所需要使用的协议和请求的资源的路径,如果协议不合法或者主机名不合法或者出现非法字符,搜索引擎会将非法字符进行转义;
2. 浏览器判断请求的资源是否有缓存,有则使用缓存,否则会向服务器发送请求;
3. 判断本地是否有服务器ip的缓存,如果有则使用,否则会进行 DNS 解析获取服务器的ip地址
4. 浏览器建立一条与服务器的TCP连接（三次握手）
5. 如果使用https协议,在通信前还存在一个TLS的一个四次握手的过程 (Https是在Http协议只上 加上了SSL)
6. 服务器收到请求,返回 一个 html 文本作为相应,浏览器收到相应后,会对 html 文本进行解析,开始页面的渲染
7. 浏览器根据 html 文件进行 dom 树的构建,根据解析到的 css 进行 CSSOM 的构建,如果遇到script标签会判断是否含有 defer 或者 aysnc 属性,否者 script 的加载和执行会造成页面渲染的阻塞;当 DOM 和 CSSOM 树建立好后,会根据它们来构建渲染树.渲染树构建好后,会根据渲染树进行页面的布局后，最后使用浏览器的 UI 接口对页面进行绘制。这个时候整个页面就显示出来了。
8. 最后一步是 TCP 断开连接的四次挥手过程

# http 和 https 的区别
http的中文叫做超文本传输协议,它负责完成客户端到服务端的一系列操作,是专门用来传输注入HTML的超媒体文档等web内容的协议,它是基于传输层的TCP协议的应用层协议
https:https是基于安全套接字的http协议,也可以理解为是http+ssl/tls(数字证书)的组合

http和https的区别:
HTTP 的 URL 以 http:// 开头，而 HTTPS 的 URL 以 https:// 开头
HTTP 是不安全的，而 HTTPS 是安全的
HTTP 标准端口是 80 ，而 HTTPS 的标准端口是 443
在 OSI 网络模型中，HTTPS的加密是在传输层完成的,因为SSL是位于传输层的,TLS的前身是SSL,所以同理
HTTP无需认证证书,而https需要认证证书 


# 转发与重定向的区别




# 深拷贝的方式有哪些，如何实现？
1. JSON

```js
JSON.parse(JSON.strinify());
```

2. 递归实现

```js
function deepCopy(newObj,oldObj) {  //（新数据，被拷贝数据）
  for(key in oldObj){
      if(Array.isArray(oldObj[key])){
          // 如果数据类型是数组，必须写在最上面，
          // 因为 ( [1,2] instanceof Object === true)
          newObj[key] = []
          deepCopy(newObj[key],oldObj[key])
      }else if(oldObj[key] instanceof Object){
          //如果数据是对象类型
          newObj[key] = {}
          deepCopy(newObj[key],oldObj[key])
      } else{
          //数据是基本数据类型
          newObj[key] = oldObj[key]
      }
  }
  return newObj
}

deepCopy(o,a)
console.log(o)  //深拷贝完成，并且deepCopy(o,a)的值就是o的值
```

3. 使用jQuery中的extend

```js
$.extend(true,obj,obj1)
```


# 数组去重,字符去重
```js
function distinct (arg){
  if(Array.isArray(arg)) return Array.from(new Set(arg));
  else if(typeof arg === "string") return Array.from(new Set(arg.split(""))).join("");
  else if(typeof arg === "number") return Array.from(new Set(arg.toString().split(""))).join("");
}
```

# 谈谈对this对象的理解？

1. this总是指向函数的直接调用者（而非间接调用者）；
   
2. 如果有new关键字，this指向new出来的那个对象；
   
3. 在事件中，this指向触发这个事件的对象，特殊的是，IE中的attachEvent中的this总是指向全局对象
