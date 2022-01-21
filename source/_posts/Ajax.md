---
title: Ajax
categories:
  - 前端
tags:
  - Ajax
  - JavaScript
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/ajaxImg.jpg'
abbrlink: 65940d5a
date: 2021-02-25 15:02:23
---

## 概念

**AJAX**即“**Asynchronous JavaScript and XML**”（异步的[JavaScript](https://www.wiki-wiki.top/baike-JavaScript)与[XML](https://www.wiki-wiki.top/baike-XML)技术），指的是一套综合了多项技术的[浏览器](https://www.wiki-wiki.top/baike-瀏覽器)端[网页](https://www.wiki-wiki.top/baike-網頁)开发技术。



传统的Web应用允许用户端填写表单（form），当提交表单时就向[网页服务器](https://www.wiki-wiki.top/baike-網頁伺服器)发送一个请求。服务器接收并处理传来的表单，然后送回一个新的网页，但这个做法浪费了许多带宽，因为在前后两个页面中的大部分[HTML](https://www.wiki-wiki.top/baike-HTML)码往往是相同的。由于每次应用的沟通都需要向服务器发送请求，应用的回应时间依赖于服务器的回应时间。这导致了用户界面的回应比本机应用慢得多



AJAX应用可以仅向服务器发送并取回必须的数据，并在客户端采用JavaScript处理来自服务器的回应。因为在服务器和浏览器之间交换的数据大量减少，服务器回应更快了。同时，很多的处理工作可以在发出请求的[客户端](https://www.wiki-wiki.top/baike-客户端)机器上完成，因此Web服务器的负荷也减少了。



## 基本使用

用JavaScript写一个完整的AJAX代码并不复杂，但是需要注意：AJAX请求是异步执行的，也就是说，要通过回调函数获得响应。



在现代浏览器上写AJAX主要依靠`XMLHttpRequest`对象：

```javascript
var textarea = document.querySelector('#res-text');
function success(text){
    textarea.innerText = text;
}
function fail(text){
    textarea.innerText = "Error code: " + text;
}
// 新建xmlhttprequest对象
var xml = new XMLHttpRequest();
// 状态发生变化时，函数被回调
xml.onreadystatechange = function(){
    if(xml.readyState === 4){
        if(xml.status === 200){
            // 成功，通过responseText拿到响应的文本
            return success(xml.responseText);

        }
    }else{
        // 失败，返回失败状态码
        return fail(xml.status);
    }
}
//发送请求
// 请求方式为Get,请求url为(一言接口)https://v1.hitokoto.cn
// get请求参数encode=text
xml.open('get','https://v1.hitokoto.cn?encode=text',{

});
xml.send();
```

<hr>

XmlHttpRequest对象在不同浏览器中不同的创建方法，以下是跨浏览器的通用方法：

```javascript
// Provide the XMLHttpRequest class for IE 5.x-6.x:
// Other browsers (including IE 7.x-8.x) ignore this
//   when XMLHttpRequest is predefined
var xmlHttp;
if (typeof XMLHttpRequest != "undefined") {
    xmlHttp = new XMLHttpRequest();
} else if (window.ActiveXObject) {
    var aVersions = ["Msxml2.XMLHttp.5.0", "Msxml2.XMLHttp.4.0", "Msxml2.XMLHttp.3.0", "Msxml2.XMLHttp", "Microsoft.XMLHttp"];
    for (var i = 0; i < aVersions.length; i++) {
        try {
            xmlHttp = new ActiveXObject(aVersions[i]);
            break;
        } catch (e) {}
    }
}
```



当创建了`XMLHttpRequest`对象后，要先设置`onreadystatechange`的回调函数。在回调函数中，通常我们只需通过`readyState === 4`判断请求是否完成，如果已完成，再根据`status === 200`判断是否是一个成功的响应。

`XMLHttpRequest`对象的`open()`方法有3个参数，第一个参数指定是`GET`还是`POST`，第二个参数指定URL地址，第三个参数指定是否使用异步，默认是`true`，所以不用写。

*注意*，千万不要把第三个参数指定为`false`，否则浏览器将停止响应，直到AJAX请求完成。如果这个请求耗时10秒，那么10秒内你会发现浏览器处于“假死”状态。

最后调用`send()`方法才真正发送请求。`GET`请求不需要参数，`POST`请求需要把body部分以字符串或者`FormData`对象传进去。

<hr>



## 安全限制

<font color=red>因为浏览器的同源策略，默认情况下，JavaScript在发送AJAX请求时，URL的域名必须和当前页面完全一致。</font>（否则会出现错误）

完全一致的意思是，域名要相同（`www.example.com`和`example.com`不同），协议要相同（`http`和`https`不同），端口号要相同（默认是`:80`端口，它和`:8080`就不同）。有的浏览器口子松一点，允许端口不同，大多数浏览器都会严格遵守这个限制。

## 跨域访问



第一种：

JSONP，它有个限制，只能用GET请求，并且要求返回JavaScript。这种方式跨域实际上是利用了浏览器允许跨域引用JavaScript资源



第二种：CORS



如果浏览器支持HTML5，那么就可以一劳永逸地使用新的跨域策略：CORS了。

CORS全称Cross-Origin Resource Sharing，是HTML5规范定义的如何跨域访问资源。

了解CORS前，我们先搞明白概念：

**Origin**表示本域，也就是浏览器当前页面的域。当JavaScript向外域（如sina.com）发起请求后，浏览器收到响应后，首先检查`Access-Control-Allow-Origin`是否包含本域，如果是，则此次跨域请求成功，如果不是，则请求失败，JavaScript将无法获取到响应的任何数据。



![js-cors](https://gitee.com/Stubborner/images/raw/master/images/20210303204619.png)

假设本域是`my.com`，外域是`sina.com`，只要响应头`Access-Control-Allow-Origin`为`http://my.com`，或者是`*`，本次请求就可以成功。

可见，跨域能否成功，取决于对方服务器是否愿意给你设置一个正确的`Access-Control-Allow-Origin`，决定权始终在对方手中。

上面这种跨域请求，称之为“简单请求”。简单请求包括GET、HEAD和POST（POST的Content-Type类型 仅限`application/x-www-form-urlencoded`、`multipart/form-data`和`text/plain`），并且不能出现任何自定义头（例如，`X-Custom: 12345`），通常能满足90%的需求。



对于PUT、DELETE以及其他类型如`application/json`的POST请求，在发送AJAX请求之前，浏览器会先发送一个`OPTIONS`请求（称为preflighted请求）到这个URL上，询问目标服务器是否接受：



```http
OPTIONS /path/to/resource HTTP/1.1
Host: bar.com
Origin: http://my.com
Access-Control-Request-Method: POST
```

服务器必须响应并明确指出允许的Method：

```http
HTTP/1.1 200 OK
Access-Control-Allow-Origin: http://my.com
Access-Control-Allow-Methods: POST, GET, PUT, OPTIONS
Access-Control-Max-Age: 86400
```

浏览器确认服务器响应的`Access-Control-Allow-Methods`头确实包含将要发送的AJAX请求的Method，才会继续发送AJAX，否则，抛出一个错误。

由于以`POST`、`PUT`方式传送JSON格式的数据在REST中很常见，所以要跨域正确处理`POST`和`PUT`请求，服务器端必须正确响应`OPTIONS`请求。



## 参考文档来源

[廖雪峰Ajax教程](https://www.liaoxuefeng.com/wiki/1022910821149312/1023022332902400)

[维基百科Ajax](https://www.wiki-wiki.top/wiki/Ajax)