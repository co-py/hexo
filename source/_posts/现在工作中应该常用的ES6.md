---
title: 现在工作中应该常用的ES6
date: 2017-10-05 09:07:50
tags: ES6
---
ES6标准到现在已有三年了，普及程度相当高了，现在不会ES6都不好意思说自己是搞前端的，它的普及，也离不开它能真真切切的提高我们的生产力，下面我写些在开发中我常用的ES6语法，详情请参考[阮一峰](es6.ruanyifeng.com)老师的教程，方面的话可以买他的书《ECMAScript 6 入门》,现在第三版了。

## 让我们开始吧

###  一、let/const
新的变量声明方式 ，let声明变量，const 声明常量
注意点： 
1 不再存在变量的提升，必须先定义，后使用
``` javascript
console.log(a) //ReferenceError
let a = 0
```
2 提供了块级作用域

``` javascript
{
    let a = 1
}
console.log(a) // undefined
```


### 二、 => (箭头函数)
箭头函数，以及其简单，优雅的用法，俘虏了大多前端的心

``` javascript
var fn = function(a, b) {
    return a + b;
}

const fn = (a, b) => a + b
```
注意点： this指向发生了变化，不再是指向调用时的对象，而是固定的，就是定义是的所在对象。


### 三、 结构赋值
开发中使用结构赋值是件幸福事，看看实例就明白我为什么这样说
``` javascript
let [a, [b, c], d] = [1, [2, 3], 4]
// a = 1
// b = 2
// c = 3
// d = 4
```
开发中，常常通过ajax从后端获取数据，他们的结构不一，当知道他们的结构时候，赋值就是这么简单


### 四、 模板字符串
首先，它不是单引号，是tab键上面英文模式下输入的,我第一用的时候半天没找到。
它的出现是为了解决使用 + 拼接的不便利（拼接的两边要用引号隔开）而出现的。

``` javascript
var string = a '+' b '-' c 

const string = `${a}+${b}-${c}`
```
###  五、 默认参数
开发中我们常遇到这样的情景，当 a 有值传过来的时候，我们用传过来的值，没有传的时候，用一个默认的值，防止出错等

``` javascript
// ES5
function add(a, b) {
    var a = a || 0
	var b = b || 1
    return a + b
}

// ES6
(a = 0, b = 1) => a + b
```
注意点： a, b 两个参数，若a有默认值，而b没有，则b要在a之前

``` javascript
(a = 0, b) => a + b // X
(b, a = 0) => a + b // V
```
### 六、 数组和对象的扩展
ES6 为对象和数组定义了几个很实用的方法
数组的find(),findIndex()等

``` javascript
[1,2,3,4,5].find(n => n > 3 ) // 4 

[6,7,8,9,10].findIndex(n => n > 8 ) // 3(数组第3个元素) 

```
注意点：方法找到第一元素就返回，找不到返回undefined,
想要返回所有符合条件的元素，可以用ES5的filter()

对象的assign()

``` javascript
let obj = Object.assign({}, {a: 1, b: 1}, {c: 2})
obj //{a: 1, b: 2, c: 3}

```
注意点： assign()只能进行浅拷贝

### 七、 promise
promise是为解决ES5回调函数在多重嵌套的时候出现的'回调地狱',金字塔形的代码不好阅读与维护。

``` javascript
new Promise(fn)
const fn = (resolve, reject) => {
	if(符合要求或者正确执行){
		resolve()
	} else {
		reject()
	}
}
```
Promise是个构造函数，我们在定义代码的时候，只有一个参数，是个函数。函数有两个参数resolve, reject，浏览器已经实现，我们无需关心，只要知道，resolve是我们的代码正确执行或者符合我们要求时候执行它,相反就执行reject。

``` javascript
const Pro = new Promise(fn)
Pro.then(fn2).catch(fn3)
const fn2 = (a) => {'正确的时候我想要执行的代码'}
const fn3 = (b) => {'不正确的时候我想要执行的代码'}
```
Pro是一个对象，由then()方法和catch()等多个方法。
then()可以有两个参数，都是函数。第一个是在resolve()时候调用，第二个在reject()时候调用，如上，也可以只有一个参数，只是在resolve()调用，而reject()时候在catch()里调用。
#### Promise中的数据传递
``` javascript
const Pro = new Promise((resolve, reject) => {
	let a = 1
	resolve(a)
	
})

Pro.then(a => {
	console.log(a)
	return a + 1
})
.then(a => {
	console.log(a)
	return a + 1
})
.then(a => {
	console.log(a)
	return a + 1
})

// 1
// 2
// 3
```
还有Promise.all()和Promise.race()

### 八、Modules
在这里我们结合Commonjs对比这讲，
1,基本使用方法
``` javascript
// commonjs

// 导出使用exports(或者module.exports)
const add = (a, b) => a + b
module.exports.add = add
  
// 导入使用 require 
let common = require('./common.js')
common.add(1, 2) //3
```

``` javascript
// ES6

// 导出使用export(或者exprot default)
const add = (a, b) => a + b
export.default.add = add

// 导入使用improt from

import es6 from 'es6.js'
es6.add(1, 2) // 

```
