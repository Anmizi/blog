---
title: '不会变量,别说你会JS'
categories:
  - 前端
tags:
  - JavaScript
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20210913200618.png'
abbrlink: '89576728'
date: 2021-09-13 20:07:23
---

### 题目

- typeof 能判断哪些类型
- 何时使用`===`何时使用`==`
- 值类型和引用类型的区别
- 手写深拷贝



值类型

```javascript
//值类型
let a = 100
let b = a
a = 200
console.log(b) // 100
```

![image-20210913144917327](https://gitee.com/Stubborner/images/raw/master/images/image-20210913144917327.png)

引用类型

```javascript
//引用类型
let a = {age: 20}
let b = a
b.age = 21
console.log(a.age) //21
```

![image-20210913144937327](https://gitee.com/Stubborner/images/raw/master/images/image-20210913144937327.png)

### 常见值类型

```javascript
let a //undefined
let s = 'abc'
let n = 100
let b = true
let s = Symbol('s')
```



### 常见引用类型

```javascript
const obj = {x:100}
const arr = {'a','b','c'}
const n = null
//特殊引用类型，不存储数据，所以没有拷贝，复制函数这一说法
function fn(){}
```



### typeof 运算符

- 识别所有有值类型
- 识别函数
- 判断是否是引用类型（不可细分）

```javascript
//判断所有值类型
let a
typeof a //'undefined'
const str = 'abc'
typeof str //'string'
const n = 100
typeof n //'number'
const b = true
typeof b //'boolean'
const s = Symbol('s')
typeof s //'symbol'
```

```javascript
//判断函数
typeof console.log //'function'
typeof function(){} // 'function'
//能识别引用类型（不能再继续识别）
typeof null // 'object'
typeof ['a','b'] //'object'
typeof {x:100} //'object'
```



### 深拷贝代码

```javascript
function deepClone(obj = {}){
  if(typeof obj !== 'object' || typeof obj == null){
    return obj
  }
  let result
  if(obj instanceof Array){
    result = []
  }else{
    result = {}
  }
  for(let key in obj){
    if(obj.hasOwnProperty(key)){
      result[key] = deepClone(obj[key])
    }
  }
  return result
}
```



### 类型转换

- 字符串拼接

```javascript
const a = 100 + 10 // 110
const b = 100 + '10' //'10010'
const c = true + '10' //'true10'
```



- `==`

```javascript
100 == '100'
0 == ''
0 == false
false == ''
null == undefined
//上述都返回true
```

```javascript
//除了 == null之外，其他都一律使用 ===
const obj = {x:100}
if(obj.a == null){}
//相当于：
// if(obj.a === null || obj.a === undefined)
```



- if语句和逻辑运算
  - truly变量：!!a === true的变量
  - false变量：!!a === false的变量

```javascript
//以下是falsey变量，除此之外都是truely变量
!!0 === false
!!'' === false
!!NaN === false
!!null === false
!!undefined === false
!!false === false
```

<font color=red>if语句判断的就是truely变量和falsely变量</font>



### 小结

- 值类型 vs 引用类型，堆栈模型，深拷贝
- typeof运算符
- 类型转换，truly 和falsely变量

