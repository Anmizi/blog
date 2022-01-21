---
title: JS判断数据类型
categories:
  - 前端
tags:
  - JavaScript
  - JS面试题
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20210913200618.png'
abbrlink: a4f46ae4
date: 2021-07-26 18:01:23
---

## typeof


**`typeof`** 操作符返回一个字符串，表示未经计算的操作数的类型。

typeof 总是返回一个字符串



`typeof` 可能的返回值

| 类型      | 结果        |
| --------- | ----------- |
| undefined | "undefined" |
| Null      | "object"    |
| Boolean   | "boolean"   |
| Number    | "number"    |
| String    | "string"    |
| Function  | "function"  |



<font color=red>`typeof`常用于检测基本数据类型(Number,String,Boolean等) </font>



```javascript
typeof 123;// "number"
typeof "hello js" //"string"
typeof true; //"boolean"
typeof function(){}; //"function"
```



## instanceof



**`instanceof`** **运算符**用于检测构造函数的 `prototype` 属性是否出现在某个实例对象的原型链上。



`instanceof` <font color=red>常用于检测引用数据类型(Array,Object,RegExp等)</font>



## Object.prototype.toString



可以通过 `toString()` 来获取每个对象的类型。为了每个对象都能通过 `Object.prototype.toString()` 来检测，需要以 `Function.prototype.call()` 或者 `Function.prototype.apply()` 的形式来调用，传递要检查的对象作为第一个参数，称为 `thisArg`。



```javascript
var toString = Object.prototype.toString;

toString.call(new Date); // [object Date]
toString.call(new String); // [object String]
toString.call(Math); // [object Math]

//Since JavaScript 1.8.5
toString.call(undefined); // [object Undefined]
toString.call(null); // [object Null]

```



`Object.prototype.toString.call()` <font color=red>可以较为全面的检测基本数据类型和引用数据类型</font>



注意：此方法对低版本IE浏览器不能做到全面兼容



