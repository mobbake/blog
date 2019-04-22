---
title: mongoDB in windows 
date: 2018-07-26 09:45:13
tags: mongoDB
categories: 开发
---

## MongoDB 下载

MongoDB 提供了可用于 32 位和 64 位系统的预编译二进制包，你可以从MongoDB官网下载安装，MongoDB 预编译二进制包下载地址：<https://www.mongodb.com/download-center#community>

## 创建数据目录

MongoDB将数据目录存储在 db 目录下。但是这个数据目录不会主动创建，我们在安装完成后需要创建它。

创建 `C:\data\db`目录

## 安装 mongod管理服务

当mongod.exe被关闭时，mongo.exe 就无法连接到数据库了，因此每次想使用mongodb数据库都要开启mongod.exe程序，所以比较麻烦，此时我们可以将MongoDB安装为windows服务

还是运行cmd，进入bin文件夹，执行下列命令

`c:\mongodb\bin>mongod   --install `

* `--dbpath "d:\mongodb\data\db"`

* `--logpath "c:\mongodb\data\log\MongoDB.log"`

* `--config "C:\mongodb\mongod.cfg"`

* `--serviceName "MongoDB`

>  '这里MongoDB.log就是开始建立的日志文件，--serviceName "MongoDB" 服务名为MongoDB

>  要使用备用 dbpath，可以在配置文件（例如：C:\mongodb\mongod.cfg）或命令行中通过 --dbpath 选项指定。

> 如果需要，您可以安装 mongod.exe 或 mongos.exe 的多个实例的服务。只需要通过使用 --serviceName 和 --serviceDisplayName 指定不同的实例名。只有当存在足够的系统资源和系统的设计需要这么做。

启动MongoDB服务

```
net start MongoDB
```

关闭MongoDB服务

```
net stop MongoDB
```

移除 MongoDB 服务

```
C:\mongodb\bin\mongod.exe --remove
```

## 使用mongodb

1.常用的命令

- show dbs    显示数据库列表
- use dbname    进入dbname数据库，大小写敏感，没有这个数据库也不要紧
- show collections    显示数据库中的集合，相当于表格

2.创建&新增

- db.users.save({"name":"lecaf"})    *创建了名为users的集合，并新增了一条{"name":"lecaf"}的数据*

- db.users.insert({"name":"ghost", "age":10})    *在users集合中插入一条新数据，，如果没有users这个集合，mongodb会自动创建*

- save()和insert()也存在着些许区别：若新增的数据主键已经存在，insert()会不做操作并提示错误，而save() 则更改原来的内容为新内容。

- - 存在数据：{ _id : 1, " name " : " n1 "} ，_id是主键
  - insert({ _id : 1, " name " : " n2 " })    *会提示错误*
  - save({ _id : 1, " name " : " n2 " })     *会把 n1 改为  n2 ，有update的作用。*

3.删除

- db.users.remove()    *删除users集合下所有数据*
- db.users.remove({"name": "lecaf"})    *删除users集合下name=lecaf的数据*
- db.users.drop()或db.runCommand({"drop","users"})    *删除集合users*
- db.runCommand({"dropDatabase": 1})    *删除当前数据库*

4.查找

- db.users.find()    *查找users集合中所有数据*
- db.users.findOne()    *查找users集合中的第一条数据*

5.修改

- db.users.update({"name":"lecaf"}, {"age":10})    *修改name=lecaf的数据为age=10，第一个参数是查找条件，第二个参数是修改内容，除了主键，其他内容会被第二个参数的内容替换，主键不能修改，如图*