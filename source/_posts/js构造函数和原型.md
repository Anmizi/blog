---
title: Js构造函数和原型
categories:
  - 前端
tags:
  - JavaScript
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20-9-19.jpg'
abbrlink: 3309ee0a
date: 2021-01-23 22:46:23
---

## 概述

ES6， 全称 ECMAScript 6.0 ，2015.06 发版。但是目前浏览器的 JavaScript 是 ES5 版本，大多数高版本的浏览器也支持 ES6，不过只实现了 ES6 的部分特性和功能。

在 ES6之前 ，对象不是基于类创建的，而是用一种称为**构建函数的特殊函数**来定义对象和它们的特征。

创建对象可以通过以下三种方式：

1. 对象字面量
2. new Object()
3. 自定义构造函数

## 构造函数

**构造函数**是一种特殊的函数，主要用来初始化对象，即为对象成员变量赋初始值，它总与 new 一起使用。我们可以把对象中一些公共的属性和方法抽取出来，然后封装到这个函数里面。

在 JS 中，使用构造函数时要注意以下两点：
1. 构造函数用于创建某一类对象，其**首字母要大写**
2. 构造函数要**和 new 一起使用**才有意义

new 在执行时会做四件事情：

1. 在内存中创建一个新的空对象。
2. 让 this 指向这个新的对象。
3. 执行构造函数里面的代码，给这个新对象添加属性和方法。
4. 返回这个新对象（所以构造函数里面不需要 return ）。

JavaScript 的构造函数中可以添加一些成员，可以在构造函数本身上添加，也可以在构造函数内部的 this 上添加。通过这两种方式添加的成员，就分别称为**静态成员**和**实例成员**。

静态成员：在构造函数本上添加的成员称为**静态成员**，只能**由构造函数本身来访问**
实例成员：在构造函数内部创建的对象成员称为**实例成员**，只能**由实例化的对象来访问**

## 构造函数的问题

构造函数方法很好用，但是**存在浪费内存的问题**。

```javascript
function Star(uname,age){
    this.name = uname;
    this.age = age;
    this.sing = function(){
        console.log('我会唱歌');
    }
}
var ldh = new Star('刘德华',18);
var zxy = new Star('张学友',19);
```

<img src="https://gitee.com/Stubborner/images/raw/master/images/20210123162304.png" style="zoom:80%;" />



## 构造函数原型prototype

构造函数通过原型分配的函数是所有对象**所共享的**。

JavaScript 规定，**每一个构造函数都有一个 prototype 属性，指向另一个对象。注意这个 prototype 就是一个对象**，这个对象的所有属性和方法，都会被构造函数所拥有。

<font color=red>我们可以把那些不变的方法，直接定义在 prototype 对象上，这样所有对象的实例就可以共享这些方法。</font>



## 对象原型\_\_proto\_\_

<font color=red>对象都会有一个属性 \_\_proto\_\_ 指向构造函数的 prototype 原型对象</font>，之所以我们对象可以使用构造函数prototype 原型对象的属性和方法，就是因为对象_\_proto\_\_ 原型的存在。

\_\_proto\_\_对象原型和原型对象 prototype 是等价的

\_\_proto\_\_对象原型的意义就在于为对象的查找机制提供一个方向，或者说一条路线，但是它是一个非标准属性，因此实际开发中，不可以使用这个属性，它只是内部指向原型对象 prototype

<img src="https://gitee.com/Stubborner/images/raw/master/images/20210123163401.png" style="zoom:80%;" />



## constructor 构造函数

对象原型（\_\_proto\_\_）和构造函数（prototype）原型对象里面都有一个属性 constructor 属性 ，**constructor 我们称为构造函数，因为它指回构造函数本身**。

constructor 主要**用于记录该对象引用于哪个构造函数**，它可以让原型对象重新指向原来的构造函数。

**一般情况下，对象的方法都在构造函数的原型对象中设置**。如果有多个对象的方法，我们可以给原型对象采取对象形式赋值，但是这样就会覆盖构造函数原型对象原来的内容，这样修改后的原型对象 constructor 就不再指向当前构造函数了。此时，我们可以在修改后的原型对象中，添加一个 constructor 指向原来的构造函数。

<font color=red>构造函数，实例，原型对象三者的关系</font>

<img src="https://gitee.com/Stubborner/images/raw/master/images/20210123204210.png" style="zoom:80%;" />



## 原型链

![](https://gitee.com/Stubborner/images/raw/master/images/20210123204430.png)

## JavaScript的成员查找机制



1. 当访问一个对象的属性（包括方法）时，首先**查找这个对象自身有没有该属性**。
2. 如果**没有就查找它的原型**（也就是 \_\_proto\_\_指向的 prototype 原型对象）
3. 如果**还没有就查找原型对象的原型**（Object的原型对象）。
4. **依此类推**一直找到 Object 为止（null）。
5. \_\_proto\_\_对象原型的意义就在于为对象成员查找机制提供一个方向，或者说一条路线。



## 原型对象this的指向

构造函数中的this 指向我们实例对象.

原型对象里面放的是方法, <font color=red>这个方法里面的this 指向的是 这个方法的调用者, 也就是这个实例对象.</font>

## 扩展内置对象

可以通过原型对象，对原来的内置对象进行扩展自定义的方法。比如给数组增加自定义求偶数和的功能。

<font color=red>注意：</font>数组和字符串内置对象不能给原型对象覆盖操作 Array.prototype = {} ，只能是 Array.prototype.xxx = function(){} 的方式。



## 继承

ES6之前并没有给我们提供 extends 继承。我们可以通过**构造函数+原型对象**模拟实现继承，被称为**组合继承**。

### 借用构造函数继承父类属性

核心原理： 通过 call() 把父类型的 this 指向子类型的 this ，这样就可以实现子类型继承父类型的属性。

```javascript
//父类
function Person(name,age,sex){
    this.name = name;
    this.age = age;
    this.sex = sex;
}
//子类
function Student(name,age,sex){
    Person.call(this,name,age,sex);
    this.score = score;
}
var s1 = new Student('zs',18,'男',100);
console.dir(sl);
```

### 借用原型对象继承父类型方法

<font color=red>一般情况下，对象的方法都在构造函数的原型对象中设置，通过构造函数无法继承父类方法。</font>

核心原理：

1. 将子类所共享的方法提取出来，**让子类的 prototype 原型对象 = new 父类()**
2. 本质：子类原型对象等于是实例化父类，因为父类实例化之后另外开辟空间，就不会影响原来父类原型对象
3. 将**子类的 constructor 从新指向子类的构造函数**



## ES5新增方法概述

### 数组方法

迭代(遍历)方法：forEach()、map()、filter()、some()、every()；

```javascript
array.forEach(function(currentValue,index,arr));
//currentValue 数组当前项值
//index 数组当前项索引
//arr 数组对象本身
```



```javascript
array.filter(function(currentValue,index,arr));
//filter() 方法创建一个新的数组，新数组中的元素是通过检查指定数组中符合条件的所有元素，主要用于筛选数组
//注意它直接返回一个新数组
//currentValue 数组当前项的值
//index 数组当前索引
//arr 数组对象本身
```



```javascript
array.some(function(currentValue, index, arr));
//some() 方法用于检测数组中的元素是否满足指定条件. 通俗点 查找数组中是否有满足条件的元素
//注意它返回值是布尔值, 如果查找到这个元素, 就返回true , 如果查找不到就返回false.
//如果找到第一个满足条件的元素,则终止循环. 不在继续查找.
//currentValue: 数组当前项的值
//index：数组当前项的索引
//arr：数组对象本身
```





### 字符串方法



trim() 方法会从一个字符串的两端删除空白字符。

```javascript
str.trim()
//trim() 方法并不影响原字符串本身，它返回的是一个新的字符串。
```

### 对象方法

Object.keys() 方法返回一个所有元素为字符串的数组。

Object.keys(obj);

Object.defineProperty() 定义新属性或修改原有的属性。

```javascript
Object.defineProperty(obj,prop,descriptor);
//obj 必须 目标对象
//prop 必须 需定义或修改的属性的名字
//descriptor 必须 目标属性所拥有的特性
```

第三个参数descriptor说明

- value 设置属性的值
- writable 值是否可以重写 true|false
- enumerable 目标属性是否可被枚举 true|false
- configurable 目标属性是否可以被删除或是否可以再次修改特性 true|false

