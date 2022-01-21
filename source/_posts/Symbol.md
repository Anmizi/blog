---
title: Javascript之Symbol类型
categories:
  - 前端
tags:
  - JavaScript
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20210729160415.png'
abbrlink: eabb124d
date: 2021-07-28 15:33:23
---

## 概述


ES5的对象属性名都是字符串，容易造成属性名冲突，比如，你使用了一个他人提供的对象，但又想为这个对象添加新的方法，新方法的名字就可能与现有的方法产生冲突。ES6引入了Symbol就从根本上防止属性名的冲突。

Symbol是一种新的原始数据类型，表示独一无二的值。它是JavaScript的第七种数据类型，前六种是：undifined,null,Boolean,String,Number,Object

Symbol值通过Symbol函数生成

```javascript
let s = Symbol();
typeof s
//"symbol"
```



<font color=red>注意</font>：`Symbol`函数前不能使用new命令，否则会报错。这是因为生成的Symbol是一个原始类型的值，而不是对象。也就是说，由于Symbol值不是对象，所以不能添加属性。



`Symbol`函数可以接受一个字符串作为参数，表示对Symbol实例的描述，便于在控制台显示，或者转为字符串时，比较容易区分。

```javascript
let s1  = Symbol('foo')
let s2 = Symbol('bar')

s1 //Symbol(foo)
s2 //Symbo(bar)

s1.toString() //"Symbol(foo)"
s2.toString() //"Symbol(bar)"
```



如果 Symbol 的参数是一个对象，就会调用该对象的`toString`方法，将其转为字符串，然后才生成一个 Symbol 值。

```javascript
const obj = {
	toString(){
		return	'abc';
	}
};
const sym = Symbol(obj);
sym //Symbol(abc);
```



<font color=red>注意</font>，`Symbol`函数的参数只是表示对当前 Symbol 值的描述，因此相同参数的`Symbol`函数的返回值是不相等的。

```javascript
let s1 = Symbol();
let s2 = Symbol();

s1 === s2 //false

let s1 = Symbol('foo');
let s2 = Symbol('bar');

s1 === s2 //false
```

Symbol值不能与其他类型的值进行运算，会报错。但是Symbol值可以显式转为字符串，也可以转为布尔值，但是不可转为数值。



## Symbol.prototype.description

在读取Symbol值的描述时，可以将其转为字符串，但是用法不方便。ES2019提供了一个实例属性description,直接返回Symbol的描述

```javascript
const sym = Symbol('foo')
sym.description // 'foo'
```



## 作为属性名的Symbol

由于每个Symbol值都是不相等的，这意味着Symbol值可以作为标识符，用于对象的属性名，保证不会出现同名的属性。

```javascript
let mySymbol = Symbol()

//第一种写法
let a = {};
a[mySymbol] = 'Hello!';

//第二种写法
let a = {
    [mySymbol]: 'Hello!'
}
//第三种写法
let a = {};
Object.defineProperty(a,mySymbol,{value: 'Hello!'});

//以上写法都得到同样的结果
a[mySymbol] //"Hello!"
```



## 属性名的遍历



`Symbol`作为属性名，遍历对象的时候，该属性不会出现在`for...in`,`for...of`，循环中，也不会被`Object.keys()`,`Object.getOwnPropertyNames()`,`JSON.stringify()`返回。



但是，它也不是私有属性，有一个`Object.getOwnPropertySymbols()`方法，可以获取指定对象所有Symbol属性名。该方法返回一个数组，成员是当前对象的所以Symbol属性名。



```javascript
cosnt obj = {}
let a = Symbol('a')
let b = Symbol('b')

obj[a] = 'Hello'
obj[b] = 'World'

const objectSymbols = Object.getOwnPropertySymbols(obj);

objectSymbols
// [Symbol(a),Symbol(b)]
```



另外一个新的API，`Reflect.ownKeys()`方法可以返回所以类型的键名，包括常规键名和Symbol键名。

```javascript
let obj = {
	[Symbol('my_key')]: 1,
    enum:2,
    nonEnum:3
}
Reflect.ownKeys(ojb)
// ['enum','nonEnum',Symbol(my_key)]
```



由于以 Symbol 值作为键名，不会被常规方法遍历得到。我们可以利用这个特性，为对象定义一些非私有的、但又希望只用于内部的方法。



## Symbol.for(),Symbol.keyFor()



有时，我们希望重新使用同一个 Symbol 值，`Symbol.for()`方法可以做到这一点。它接受一个字符串作为参数，然后搜索有没有以该参数作为名称的 Symbol 值。如果有，就返回这个 Symbol 值，否则就新建一个以该字符串为名称的 Symbol 值，并将其注册到全局。



```javascript
let s1 = Symbol.for('foo');
let s2 = Symbol.for('foo');

s1 === s2 //true
```



`Symbol.for()`与`Symbol()`这两种写法，都会生成新的 Symbol。它们的区别是，前者会被登记在全局环境中供搜索，后者不会。`Symbol.for()`不会每次调用就返回一个新的 Symbol 类型的值，而是会先检查给定的`key`是否已经存在，如果不存在才会新建一个值。

`Symbol.keyFor()`方法返回一个已登记的 Symbol 类型值的`key`。

```javascript
let s1 = Symbol.for('foo')
Symbol.keyFor(s1)// 'foo'

let s2 = Symbol('foo')
Symbol.keyFor(s2)// undefined
```



<font color=red>注意</font>，`Symbol.for()`为 Symbol 值登记的名字，是全局环境的，不管有没有在全局环境运行。

```javascript
function foo(){
	return Symbol.for('bar');
}
const x = foo();
const y = Symbol.for('bar');
console.log(x === y) //true
```

