---
title: let和var的区别
categories:
  - 前端
tags: JavaScript
abbrlink: 788c0b90
date: 2020-06-09 18:24:43
index_img: https://gitee.com/Stubborner/images/raw/master/images/9bd9b167gy1g4lhdmhva8j21hc0xc476.jpg
---
### let不允许重复声明

<!-- more -->

```javascript
{
    let a=4;
    let a=2;
    console.log(a);//ReferenceError
}

{
        var b=2;
        var b=4;
        console.log(b);//4
}
```

### let声明的变量只在let代码块有效

```javascript
{
        let a=8;
        var b=10;
}
    console.log(a);//a is not defined
    console.log(b);//10
```

_var声明变量是全局范围内有效的，虽然每次循环i都在改变，但是循环内都赋值给了a的i，相当于每次循环出来的i都是指向同一个i，也就是最后一个i，所以为10；_

```javascript
var a=[];
for(var i=0;i<10;i++){
        a[i]=function(){
            console.log(i);
            
        }
  }
 a[6]();//10
```

_let声明的变量i只在本轮循环有效，每次循环的i都是一个全新的变量，所以值为6；_

```javascript
var a=[];
for(let i=0;i<10;i++){
        a[i]=function(){
            console.log(i);
            
        }
    }
 a[6]();//6
```

### var存在变量提升

```javascript
 console.log(a);//undifinded
 var a=2;
 //相当于
 var a;
 console.log(a);
 a=2;

 let不存在变量提升

 console.log(b);//ReferenceError
 let b=5;
```

### 暂时性死区

全局声明了变量tmp，但是在代码块中又用let声明了tmp，使得后者绑定了块级作用域，此时的tmp是在声明之前就赋值了，所以报错。在代码块内，使用let命令声明变量之前，该变量都是不可用的。这在语法上，称为“暂时性死区”。

```javascript
var tmp = 123;
    if (true) {
        tmp = 'abc';
        let tmp;
        console.log(tmp); // ReferenceError
    }

    var tmp = 123;
        if (true) {
        tmp = 'abc';
        var tmp;
        console.log(tmp); // abc
    }
```