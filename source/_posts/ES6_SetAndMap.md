---
title: ES6之Set与Map
categories:
  - 前端
tags:
  - JavaScript
  - ES6
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20210729160415.png'
abbrlink: 9c5f5996
date: 2021-07-29 16:07:23
---



## 基本用法

ES6 提供了新的数据结构 Set。它类似于数组，但是**成员的值都是唯一的，没有重复的值**。



`Set`本身是一个构造函数，用来生成数据结构

```javascript
const s = new Set();
[2,3,5,4,5,2,2].forEach(x => s.add(x));

for(let i of s){
    console.log(i)
}
//2 3 5 4 -
```



`Set`函数可以接受一个数组（或者具有 iterable 接口的其他数据结构）作为参数，用来初始化



```javascript
//例一
const set = new Set([1,2,3,4,4]);
[...set]
//[1,2,3,4]

//例二
const items = new Set([1,2,3,4,5,5,5,5]);
items.size // 5

//例三
const set = new Set(doucment.querySelectorAll('div'));
set.size 

//类似于
const set = new Set();
doucment.querySelectorAll('div')
	.forEach(div => set.add(div));
set.size
```



上面代码也展示了一种去除数组重复成员的方法。

```javascript
[...new Set(array)]
```

去除字符串里面重复字符

```javascript
[...new Set('ababbc')].join('')
```



Set 内部判断两个值是否不同，使用的算法叫做“Same-value-zero equality”，它类似于精确相等运算符（`===`），主要的区别是向 Set 加入值时认为`NaN`等于自身，而精确相等运算符认为`NaN`不等于自身。



```javascript
let set = new Set();
let a = NaN;
let b = NaN;
set.add(a);
set.add(b);
set // Set{NaN}
```



两个对象总是不相等的

```javascript
let set = new Set();
set.add({});
set.size //1
set.add({});
set.size //2
```



## Set实例的属性和方法



Set结构的实例有以下属性：

- `Set.prototype.constructor`: 构造函数，默认就是Set函数
- `Set.prototype.size`: 返回Set实例的成员数



Set实例的方法分为两大类：操作方法和遍历方法

操作方法

- `Set.prototype.add(value)`:添加某个值，返回Set结构本身
- `Set.prototype.delete(value)`:删除某个值，返回一个布尔值，表示删除是否成功
- `Set.prototype.has(value)`:返回一个布尔值，表示该值是否在Set结构中
- `Set.prototype.clear()`: 清除所有成员，没有返回值。



上面这些属性和方法实例如下：

```javascript
s.add(1).add(2).add(2)
//2被加入两次

s.size // 2
s.has(1)//true
s.has(2) //true
s.has(3) //false

s.delete(2);

s.has(2)//false
```



## 遍历操作

Set结构的实例有四个遍历方法，可以用于遍历成员

- `Set.prototype.keys()`: 返回键名的遍历器
- `Set.prototype.values()`: 返回键值的遍历器
- `Set.prototype.entries()`: 返回键值对应的遍历器
- `Set.prototype.forEach()`: 使用回调函数遍历每个成员

`Set`的遍历顺序就是插入顺序。这个特性有时非常有用，比如使用 Set 保存一个回调函数列表，调用时就能保证按照添加顺序调用



#### （1）keys()，values()，entries()

`keys方法`，`values方法`，`entries方法` 返回的都是遍历器对象。由于Set结构没有键名，只有键值(或者说键名和键值是同一个值)。因此，keys方法和values方法行为完全一致。



```javascript
let set = new Set(['red','green','blue']);

for(let item of set.keys()){
    console.log(item);
}
//red
//green
//blue


for(let item of set.values()){
    console.log(item);
}
//red
//green
//blue

for(let item of set.entries()){
    console.log(item);
}
//["red","red"]
//["green","green"]
//["blue","blue"]
```



Set 结构的实例默认可遍历，它的默认遍历器生成函数就是它的`values`方法。

```javascript
Set.prototype[Symbol.iterator] === Set.prototype.values
//true
```

这意味着，可以省略`values`方法，直接用`for...of`循环遍历 Set。

```javascript
let set = new Set(['red','green','blue']);

for(let x of set){
    console.log(x);
}
//red
//green
//blue
```



### (2) forEach()

Set 结构的实例与数组一样，也拥有`forEach`方法，用于对每个成员执行某种操作，没有返回值

```javascript
let set = new Set([1, 4, 9]);
set.forEach((value, key) => console.log(key + ' : ' + value))
// 1 : 1
// 4 : 4
// 9 : 9
```



## 基本用法

JavaScript 的对象（Object），本质上是键值对的集合（Hash 结构），但是传统上只能用字符串当作键。这给它的使用带来了很大的限制。



为了解决这个问题，ES6 提供了 Map 数据结构。它类似于对象，也是键值对的集合，但是“键”的范围不限于字符串，各种类型的值（包括对象）都可以当作键。也就是说，Object 结构提供了“字符串—值”的对应，Map 结构提供了“值—值”的对应，是一种更完善的 Hash 结构实现。如果你需要“键值对”的数据结构，Map 比 Object 更合适。



Map 也可以接受一个数组作为参数。该数组的成员是一个个表示键值对的数组。

```javascript
const map = new Map([
    ['name','张三'],
    ['title','Author']
])
map.size //2
map.has('name') //true
map.get('name') //'张三'
map.has('title')//true
map.get('title')//'Author'
```



事实上，不仅仅是数组，任何具有 Iterator 接口、且每个成员都是一个双元素的数组的数据结构都可以当作`Map`构造函数的参数。这就是说，`Set`和`Map`都可以用来生成新的 Map。



如果 Map 的键是一个简单类型的值（数字、字符串、布尔值），则只要两个值严格相等，Map 将其视为一个键，比如`0`和`-0`就是一个键，布尔值`true`和字符串`true`则是两个不同的键。另外，`undefined`和`null`也是两个不同的键。虽然`NaN`不严格相等于自身，但 Map 将其视为同一个键。



```javascript
let map = new Map();

map.set(-0, 123);
map.get(+0) // 123

map.set(true, 1);
map.set('true', 2);
map.get(true) // 1

map.set(undefined, 3);
map.set(null, 4);
map.get(undefined) // 3

map.set(NaN, 123);
map.get(NaN) // 123
```



## 实例的属性和操作方法



### size属性

`size`属性返回 Map 结构的成员总数。

```javascript
const map = new Map();
map.set('foo', true);
map.set('bar', false);

map.size // 2
```



### Map.prototype.set(key,value)

`set`方法设置键名`key`对应的键值为`value`，然后返回整个 Map 结构。如果`key`已经有值，则键值会被更新，否则就新生成该键。

```javascript
const m = new Map();

m.set('edition', 6)        // 键是字符串
m.set(262, 'standard')     // 键是数值
m.set(undefined, 'nah')    // 键是 undefined
```

`set`方法返回的是当前的`Map`对象，因此可以采用链式写法。

```javascript
let map = new Map()
  .set(1, 'a')
  .set(2, 'b')
  .set(3, 'c');
```



### Map.prototype.get(key)

`get`方法读取`key`对应的键值，如果找不到`key`，返回`undefined`。

```javascript
const m = new Map();

const hello = function() {console.log('hello');};
m.set(hello, 'Hello ES6!') // 键是函数

m.get(hello)  // Hello ES6!
```



### Map.prototype.has(key)

`has`方法返回一个布尔值，表示某个键是否在当前 Map 对象之中。

```javascript
const m = new Map();

m.set('edition', 6);
m.set(262, 'standard');
m.set(undefined, 'nah');

m.has('edition')     // true
m.has('years')       // false
m.has(262)           // true
m.has(undefined)     // true
```



### Map.prototype.delete(key)

`delete`方法删除某个键，返回`true`。如果删除失败，返回`false`。

```javascript
const m = new Map();
m.set(undefined, 'nah');
m.has(undefined)     // true

m.delete(undefined)
m.has(undefined)       // false
```



### Map.prototype.clear()

`clear`方法清除所有成员，没有返回值。

```javascript
let map = new Map();
map.set('foo', true);
map.set('bar', false);

map.size // 2
map.clear()
map.size // 0
```



## 遍历方法

Map 结构原生提供三个遍历器生成函数和一个遍历方法。

- `Map.prototype.keys()`：返回键名的遍历器。
- `Map.prototype.values()`：返回键值的遍历器。
- `Map.prototype.entries()`：返回所有成员的遍历器。
- `Map.prototype.forEach()`：遍历 Map 的所有成员。



```javascript
const map = new Map([
  ['F', 'no'],
  ['T',  'yes'],
]);

for (let key of map.keys()) {
  console.log(key);
}
// "F"
// "T"

for (let value of map.values()) {
  console.log(value);
}
// "no"
// "yes"

for (let item of map.entries()) {
  console.log(item[0], item[1]);
}
// "F" "no"
// "T" "yes"

// 或者
for (let [key, value] of map.entries()) {
  console.log(key, value);
}
// "F" "no"
// "T" "yes"

// 等同于使用map.entries()
for (let [key, value] of map) {
  console.log(key, value);
}
// "F" "no"
// "T" "yes"
```



上面代码最后的那个例子，表示 Map 结构的默认遍历器接口（`Symbol.iterator`属性），就是`entries`方法。



```javascript
map[Symbol.iterator] === map.entries
// true
```



