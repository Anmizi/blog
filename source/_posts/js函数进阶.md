---
title: Javascript函数进阶
categories:
  - 前端
tags:
  - JavaScript
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20-9-19.jpg'
abbrlink: c584aaaa
date: 2021-01-29 22:24:23
---

## 函数的定义和调用

### 函数的定义方式

1.函数声明方式function关键字(命名函数)

2.函数表达式(匿名函数)

3.new Function()

```javascript
var fn = new Function('参数1','参数2',...'函数体');
```

- Function里面的参数都是字符串格式
- 第三种方式执行效率低,较少用
- 所有函数都是Function的实例(对象)
- 函数也属于对象

![](https://gitee.com/Stubborner/images/raw/master/images/20210129150739.png)



### 函数的调用方式

1.普通函数

```javascript
function fn(){
	console.log('Hello,world')
}
fn();
fn.call();
```

2.对象的方法

```javascript
var o = {
    sayHi: function(){
        console.log('Hello,world');
    }
}
o.sayHi();
```

3.构造函数

```javascript
function Star(){};
new Star();
```

4.绑定事件函数

```javascript
btn.onclick = function(){}
```

5.定时器函数

```javascript
setInterval(function(){},1000)
```

6.立即执行函数

```javascript
(function(){
	console.log('Hello,world');
})();
```

## this

### 函数内this的指向

this的指向，是当我们调用函数的时候决定的，调用方式的不同决定了this的指向不同，一般指向我们的调用者

| 调用方式     | this指向                                  |
| ------------ | ----------------------------------------- |
| 普通函数调用 | window                                    |
| 构造函数调用 | 实例对象,原型对象里面的方法也指向实例对象 |
| 对象方法调用 | 该方法的所属对象                          |
| 事件绑定方法 | 绑定事件对象                              |
| 定时器函数   | window                                    |
| 立即执行函数 | window                                    |

### 改变函数内部this的指向

javascript为我们提供了一些函数方法来帮我们更好的处理函数内部this的指向问题，常用的有bind(),call(),apply()三种方法

1.call方法

call()方法调用一个对象，简单理解为调用函数的方式，但是它可以改变函数的this指向

```javascript
fun.call(thisArg,arg1,arg2,...)
```

- thisArg : 在fun函数运行时this的指向
- arg1,arg2: 传递的参数
- 返回值就是函数的返回值，因为它就是调用函数
- 因此当我们想改变this的指向，同时想调用这个函数的时候，可以使用call，比如继承

2.apply方法

apple()方法调用一个函数，简单理解为调用函数的方式，它可以改变函数的this指向

```javascript
fun.apply(thisArg,[argsArray])
```

- thisArg: 在fun函数运行时指定的this值
- argsArray: 传递的值，必须包含在数组里面
- 返回值就是函数的返回值，因为它就是调用函数
- 因此apply主要跟数组有关系，比如使用Math.max()求数组的最大值

3.bind方法

bind()方法不会调用函数,但是能改变函数的this指向

```javascript
fun.bind(thisArg,arg1,arg2,...)
```

- thisArg: 在fun函数运行时指定this值
- arg1，arg2：传递的其他参数
- 返回由指定的this值和初始化参数改造的原函数拷贝
- 因此当我们只是2想改变this指向，不调用这个函数的时候，可以使用bind

**call apply bind总结**

相同点

都可以改变函数内部的this指向

区别点

1.call和apply会调用函数，并且会改变内部this的指向

2.call和apply传递的参数不一样，call传递参数arg1，arg2...形式，apply必须数组形式[arg]

3.bind不会调用函数，可以改变函数内部的this指向

主要应用场景

1.call经常做继承

2.apply经常跟数组有关系，比如借助于数学对象实现数组最大值最小值

3.bind不调用函数，但是还想改变this指向，比如改变定时器内部this指向

## 严格模式

### 什么是严格模式

javascript除了提供正常模式外，还提供了严格模式，ES5的严格模式是采用具有限制性javascript变体的一种方式，即在严格的条件下运行js代码

严格模式在IE10以上版本的浏览器中才会被支持，旧版本浏览器中会被忽略。

严格模式对正常的JavaScript语义做了一些更改：

1. 消除了Javascript语法的一些不合理、不严谨之处，减少了一些怪异行为。
2. 消除代码运行的一些不安全之处，保证代码运行的安全。
3. 提高编译器效率，增加运行速度。
4. 禁用了在ECMAScript的未来版本中可能会定义的一些语法，为未来新版本的Javascript做好铺垫。比如一些保留字如：class，，enum，export，extends，import，super 不能做变量名

### 开启严格模式

严格模式可以应用到**整个脚本**或**个别函数**中。因此在使用时，我们可以将严格模式分为为**脚本开启严格模式**和为**函数开启严格模式**两种情况。

1.为脚本开启严格模式

为整个脚本文件开启严格模式，需要在所有语句之前放一个特定语句“use strict"；（或‘use strict'；）。
```html
<script>
    "use strict"
    console.log('这是严格模式');
</script>
```

因为“use strict"加了引号，所以老版本的浏览器会把它当作一行普通字符串而忽略。

有的script基本是严格模式，有的script 脚本是正常模式，这样不利于文件合并，所以可以将整个脚本文件放在一个立即执行的匿名函数之中。这样独立创建一个作用域而不影响其他 script脚本文件。

```html
<script>
	(function(){
        "use strict";
        var num = 10;
        function fn(){}
    })();
</script>
```

2.为函数开启严格模式

要给某个函数开启严格模式，需要把"use strict"声明放在函数体所有语句之前

```javascript
function fn(){
    "use strict";
    return "这是严格模式";
}
```

### 严格模式中的变化

1.变量规定

1. 在正常模式中，如果一个变量没有声明就赋值，默认是全局变量。严格模式禁止这种用法，变量都必须用var命令声明，然后在使用
2. 严禁删除已经声明的变量，例如，delete x;语法是错误的

2.严格模式下this的指向问题

1. 以前在全局作用域函数中的this指向window对象，严格模式下this指向的是undefinded
2. 以前构造函数不加new也可以调用，当普通函数，this指向全局对象
3. 严格模式下，如果构造函数不加new调用，this指向的是undefined如果给它赋值，会报错
4. new实例化的构造函数指向创建的对象实例
5. 定时器this还是指向window
6. 事件，对象还是指向调用者

3.函数变化

1. 函数不能有重名的参数
2. 函数必须声明在顶层，新版本的js会引入"块级作用域"（ES6已引入）。为了与新版本接轨，不允许在非函数的代码块内声明函数

## 高阶函数

**高阶函数**是对其它函数进行操作的函数，它接**收函数作为参数或将函数作为返回值输出**

## 闭包

1.变量作用域

变量根据作用域不同分两种：全局变量和局部变量

1. 函数内部可以使用全局变量
2. 函数外部不可以使用局部变量
3. 当函数执行完毕，本作用域的局部变量被销毁

### 什么是闭包

闭包(closure)是指**有权**访问另一个函数作用域中**变量**的函数

简单理解就是，一个作用域可以访问另一个函数内部的局部变量

```html
<script>
	function fn1(){
        var num = 10;
        function fn2(){
            console.log(num);
        }
        fn2();
    }
    fn1();
</script>
```

### 闭包的作用

提问：我们如何在fn()函数外面访问fn()中的局部变量num呢？

```html
<script>
	function fn(){
        var num = 10;
        return function(){
            console.log(num);
        }
    }
    var f = fn();
    f();
</script>
```

闭包作用：延伸变量的作用范围

