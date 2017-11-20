---
title: koa2入门系列教程（一）mongoDB的使用
date: 2017-10-07 13:07:51
tags: koa
---
koa作为下一代web应用框架，尤其是使用了ES7的async和await,更是把简洁渗入血脉。在开始说koa之前，我们先讲讲koa的好搭档[MongoDB](https://www.mongodb.com/download-center?jmp=nav#community)。

## mongoBD服务配置(window)

### 在bin同级下，新建目录
``` bash
mkdir data
mkdir log
cd log
touch mongo.log
```

### 以管理员身份运行CMD
``` bash
mongod --dbpath "C:\Program Files\MongoDB\Server\3.4\data" --logpath "C:\Program Files\MongoDB\Server\3.4\log\mongo.log" --logappend 
```

### 另启一个窗口
```bash
	mongo
```

### 作为服务启动
``` bash
mongod --dbpath "C:\Program Files\MongoDB\Server\3.4\data" --logpath "C:\Program Files\MongoDB\Server\3.4\log\mongo.log" --logappend --install --serviceName "MongoDB"
```
## 基础命令

### 查看所有库
``` bash
show dbs

admin  0.000GB
local  0.000GB
```
### 使用库（没有则新建库）
``` bash
use app

switched to db app
```
### 创建一条数据并查找出来
``` bash
db.user.save({name: "chaoshuai"})

WriteResult({ "nInserted" : 1 })


db.user.find()

{ "_id" : ObjectId("59d87fc36f962cd49948149c"), "name" : "chaoshuai" }
```
### 更新一条数据（没有$set:{},会覆盖所有属性）
``` bash
db.user.update({"_id" : ObjectId("59d87fc36f962cd49948149c"},{$set:{"name": "xiaoshuai"}})
```
### 删除记录(条件为空不会执行)
``` bash
db.user.remove({name: 'xiaoshuai'})
```

### 删除表

``` bash
db.mytable.drop();
```

## mongoose 建模和操作数据库

### 连接数据库
``` javascript
const db = 'mongodb://localhost/app'
mongoose.connect(db, {useMongoClient:true})
```

### 定义Schema(不具备操作数据库的能力)

``` javascript
const mongoose = require('mongoose')
const UserSchema = new mongoose.Schema({
	name: String,
	age: Number
})
```

Schema Types内置类型如下：

　　String

　　Number

　　Boolean | Bool

　　Array

　　Buffer

　　Date

　　ObjectId | Oid

　　Mixed

### 由Schema生成Model(可以对数据库的操作)

``` javascript
const userModel = mongoose.model('User',UserSchema)
```

### 生成新用户并保存

``` javascript
const mongoose = require('mongoose')
const User = mongoose.model('User')
const user1 = new User({
	name: 'chaoshuai',
	age: 20
})

try{
	user1.save()
} catch (e) {
	console.log('保存信息出错')
	return
}
console.log('保存成功')
```