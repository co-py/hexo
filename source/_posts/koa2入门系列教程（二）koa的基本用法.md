---
title: koa2入门系列教程（二）koa的基本用法
date: 2017-10-08 17:41:07
tags: koa
---
koa作为下一代web应用框架，尤其是使用了ES7的async和await,更是把简洁渗入血脉。今天我们来看看koa的基本用法，开始之前请安装koa2，Koa2须使用 7.6 以上版本的[Node](http://nodejs.cn/download/)

### 事前准备

``` bash
node -v

v8.6.0

mkdir koa2
cd koa2
npm install koa --save
```
### 官网最简实例
``` javascript
const Koa = require('koa')
const app = new Koa()

app.use(async ctx => {
  ctx.body = 'Hello World'
})

app.listen(3000)
```
访问 http://127.0.0.1:3000 
可以看到 hello world

### koa-route
koa 可以靠ctx.request.url原生实现路由，如果依靠去手动处理路由，将会变得异常繁琐，我们不需要重复造轮子，github上有好多高质量插件，路由我们使用koa-router 
``` javascript
const route = require('koa-route')

app.use(route.get('/', (ctx, next) =＞｛
	ctx.response.body = 'Hello World'
｝)

app.use(route.get('/ａ', (ctx, next) =＞｛
	ctx.response.body = 'Hello ａ'
｝)

```

### 静态资源

一个http请求访问web服务静态资源，如果还是用路由去处理，将会产生很多路由，可是，我们会发现访问静态资源套路都一样，得知资源名称，拿到资源。所以我们使用koa-static来处理静态资源。

``` javascript
const path = require('path')
const static = require('koa-static')
app.use(static(path.join(__dirname)))

```
### 中间件
koa的重要概念就是中间件，它是一个个函数，用来处在 HTTP Request 和 HTTP Response，app.use()用来加载它，每个中间件默认接受两个参数，第一个参数是 Context 对象，第二个参数是next函数。只要调用next函数，就可以把执行权转交给下一个中间件。
``` javascript
app.use((ctx, next) => {
  console.log(`${ctx.request.url}`)
  next()
})
```
### 中间件栈
关于中间件栈，阮一峰老师的教程非常经典，看下面
``` javascript
const one = (ctx, next) => {
  console.log('>> one')
  next()
  console.log('<< one')
}

const two = (ctx, next) => {
  console.log('>> two')
  next()
  console.log('<< two')
}

const three = (ctx, next) => {
  console.log('>> three')
  next()
  console.log('<< three')
}

app.use(one)
app.use(two)
app.use(three)

// >> one
// >> two
// >> three
// << three
// << two
// << one

```

``` javascript
const one = (ctx, next) => {
  console.log('>> one')
  next()
  console.log('<< one')
}

const two = (ctx, next) => {
  console.log('>> two')
  // next()
  console.log('<< two')
}

const three = (ctx, next) => {
  console.log('>> three')
  next()
  console.log('<< three')
}

app.use(one)
app.use(two)
app.use(three)

// >> one
// >> two
// << two
// << one
```

结论： 如果中间件内部没有调用next函数，那么执行权就不会传递下去


### 异步中间件

异步处理，是web开发中最重要的，同时koa2中的asnyc和await的用法，让异步处理和同步处理一样简单。
``` javascript
const fs = require('fs')
const Koa = require('koa')
const app = new Koa()

app.use( async (ctx, next) => {
  ctx.response.body = await fs.readFile()
})

app.listen(3000)
```