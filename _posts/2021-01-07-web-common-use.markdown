---
layout: post
title:  "Web开发常用代码整理"
date:   2021-01-05 08:40:54
categories: Web
tags: Web 前端 jquery IE CSS
excerpt: Web开发常用代码整理
mathjax: true
---

* content
{:toc}


# Web前端开发常用代码整理
## IE条件注释
条件注释简介

1. IE中的条件注释（Conditional comments）对IE的版本和IE非IE有优秀的区分能力，是WEB设计中常用的hack方法。
2. 条件注释只能用于IE5以上，IE10以上不支持。
3. 如果你安装了多个IE，条件注释将会以最高版本的IE为标准。
4. 条件注释的基本结构和HTML的注释(<!– –>)是一样的。因此IE以外的浏览器将会把它们看作是普通的注释而完全忽略它们。
5. IE将会根据if条件来判断是否如解析普通的页面内容一样解析条件注释里的内容。

**条件注释使用方法示例**
```js
<!–-[if IE 5]>仅IE5.5可见<![endif]–->
<!–-[if gt IE 5.5]>仅IE 5.5以上可见<![endif]–->
<!–-[if lt IE 5.5]>仅IE 5.5以下可见<![endif]–->
<!–-[if gte IE 5.5]>IE 5.5及以上可见<![endif]–->
<!–-[if lte IE 5.5]>IE 5.5及以下可见<![endif]–->
<!–-[if !IE 5.5]>非IE 5.5的IE可见<![endif]–->
```


## js判断用户访问的是PC还是mobile
```js
var browser={ 
    versions:function(){
        var u = navigator.userAgent, app = navigator.appVersion;
        var sUserAgent = navigator.userAgent;
        return {
        trident: u.indexOf('Trident') > -1,
        presto: u.indexOf('Presto') > -1, 
        isChrome: u.indexOf("chrome") > -1, 
        isSafari: !u.indexOf("chrome") > -1 && (/webkit|khtml/).test(u),
        isSafari3: !u.indexOf("chrome") > -1 && (/webkit|khtml/).test(u) && u.indexOf('webkit/5') != -1,
        webKit: u.indexOf('AppleWebKit') > -1, 
        gecko: u.indexOf('Gecko') > -1 && u.indexOf('KHTML') == -1,
        mobile: !!u.match(/AppleWebKit.*Mobile.*/), 
        ios: !!u.match(/\(i[^;]+;( U;)? CPU.+Mac OS X/), 
        android: u.indexOf('Android') > -1 || u.indexOf('Linux') > -1,
        iPhone: u.indexOf('iPhone') > -1, 
        iPad: u.indexOf('iPad') > -1,
        iWinPhone: u.indexOf('Windows Phone') > -1
        };
    }()
}
if(browser.versions.mobile || browser.versions.iWinPhone){
    window.location = "http:/www.baidu.com/m/";
} 
```


## js如何判断用户是否是用微信浏览器
根据关键字 MicroMessenger 来判断是否是微信内置的浏览器。判断函数如下：
```js
function isWeiXin(){ 
    var ua = window.navigator.userAgent.toLowerCase(); 
    if(ua.match(/MicroMessenger/i) == 'micromessenger'){ 
        return true; 
    }else{ 
        return false; 
    } 
} 
```

## JS,Jquery获取各种屏幕的宽度和高度
Javascript:
```js
文档可视区域宽： document.documentElement.clientWidth
文档可视区域高： document.documentElement.clientHeight

网页可见区域宽： document.body.clientWidth
网页可见区域高： document.body.clientHeight
网页可见区域宽： document.body.offsetWidth (包括边线的宽)
网页可见区域高： document.body.offsetHeight (包括边线的高)
网页正文全文宽： document.body.scrollWidth
网页正文全文高： document.body.scrollHeight
网页被卷去的高： document.body.scrollTop
网页被卷去的左： document.body.scrollLeft
网页正文部分上： window.screenTop
网页正文部分左： window.screenLeft
屏幕分辨率的高： window.screen.height
屏幕分辨率的宽： window.screen.width
屏幕可用工作区高度： window.screen.availHeight
屏幕可用工作区宽度： window.screen.availWidth
```
JQuery:
```js
$(document).ready(function(){
alert($(window).height()); //浏览器当前窗口可视区域高度
alert($(document).height()); //浏览器当前窗口文档的高度
alert($(document.body).height());//浏览器当前窗口文档body的高度
alert($(document.body).outerHeight(true));//浏览器当前窗口文档body的总高度 包括border padding margin

alert($(window).width()); //浏览器当前窗口可视区域宽度
alert($(document).width());//浏览器当前窗口文档对象宽度
alert($(document.body).width());//浏览器当前窗口文档body的宽度
alert($(document.body).outerWidth(true));//浏览器当前窗口文档body的总宽度 包括border padding margin
})
```

## jquery对文本框只读状态与可读状态的相互转化
```js
$('input').removeAttr('Readonly');
$('input').attr('Readonly','true');
```

## 判断浏览器的简单有效方法
```js
function getInternet(){    
    if(navigator.userAgent.indexOf("MSIE")>0) {    
      return "MSIE";       //IE浏览器  
    }  

    if(isFirefox=navigator.userAgent.indexOf("Firefox")>0){    
      return "Firefox";     //Firefox浏览器  
    }  

    if(isSafari=navigator.userAgent.indexOf("Safari")>0) {    
      return "Safari";      // Safari, chrome浏览器   Chromium基于webkit
    }  

    if(isCamino=navigator.userAgent.indexOf("Camino")>0){    
      return "Camino";   //Camino浏览器  
    }  
    if(isMozilla=navigator.userAgent.indexOf("Gecko/")>0){    
      return "Gecko";    //Gecko浏览器  
    }    
} 
```

## 文本溢出显示省略号
### 单行
```css
p{
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;  
}
```
### 多行
```css
p{
  overflow : hidden;
  text-overflow: ellipsis;
  display: -webkit-box;
  -webkit-line-clamp: 2;      /* 显示的行数 */
  -webkit-box-orient: vertical;
}
```