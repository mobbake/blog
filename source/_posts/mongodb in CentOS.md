---
title: mongodb in CentOS
date: 2018-09-29 09:35:07
tags: [Mongodbs, Node.js]
categories: 开发手册
toc: true
---

# mongodb in CentOS

## install

可能 有更新，见官网<https://docs.mongodb.com/manual/tutorial/install-mongodb-on-red-hat/>

创建仓库文件: 

```bash
vi /etc/yum.repos.d/mongodb-org-4.0.repo
```

 然后复制下面配置,保存退出

```
[mongodb-org-4.0]
name=MongoDB Repository
baseurl=https://repo.mongodb.org/yum/redhat/$releasever/mongodb-org/4.0/x86_64/
gpgcheck=1
enabled=1
gpgkey=https://www.mongodb.org/static/pgp/server-4.0.asc
```

yum安装

```bash
yum install -y mongodb-org
```

## 启动、停止、重启

MongoDB默认将数据文件存储在`/var/lib/mongo`目录，默认日志文件在`/var/log/mongodb`中。如果要修改,可以在 `/etc/mongod.conf` 配置中指定备用日志和数据文件目录。

启动命令:

```
`service mongod start`
```

 停止命令:

```
`service mongod stop`
```

 重启命令:

```
`service mongod restart`
```

## 配置

### ip配置

安装完毕后修改配置文件:

```
vi /etc/mongod.conf
```

修改配置文件的 `bind_ip,` 默认是 `127.0.0.1 只限于本机连接`。所以安装完成后必须把这个修改为 0.0.0.0

### 用户授权

MongoDB 默认没有设置用户名密码，需要我们自己设置，先设置 admin 用户，然后针对某个数据库设置用户

#### 设置 admin

```bash
mongo //进入控制台
```

创建管理员

```bash
use admin
db.createUser(
  {
    user: "myUserAdmin",
    pwd: "abc123",
    roles: [ { role: "userAdminAnyDatabase", db: "admin" } ]
  }
)
```

修改配置文件`vi /etc/mongod.conf`

```
security:
   authorization: <string>// enabled && disabled
```

#### 添加数据库用户

```
use test
db.createUser(
  {
    user: "myTester",
    pwd: "xyz123",
    roles: [ { role: "readWrite", db: "test" },
             { role: "read", db: "reporting" } ]
  }
)
```

## mongo 控制 台常用命令

```bash
mongo
```

```
## 查看数据库
> show dbs;
```

```
## 查看数据库版本
> db.version();
```

```
## 常用命令帮助
> db.help();
```

