---
title: npm源的设置与还原,cnpm的安装
date: 2017-09-19 14:52:43
tags: [npm, Node.js]
categories: Node.js
---
使用npm默认源安装时，因为国内网络原因，经常安装失败或等待时间太长  
可以使用淘宝的npm镜像来解决此问题
<!--more-->

淘宝 NPM 镜像 网址：https://npm.taobao.org/

### npm源设置（3种方法）

#### 1.命令行指定

```shell 
$ npm  install [包名] --registry https://registry.npm.taobao.org
```

#### 2.通过config命令

```shell 
$ npm config set registry https://registry.npm.taobao.org 
```

#### 3.编辑 ~/.npmrc 

```shell 
$ npm config edit
```

加入下面内容

`registry = https://registry.npm.taobao.org`

**NOTE**:上面设置中方法1只是当次安装使用淘宝源，方法2和方法3会改变源的设置，如果需要还原，见下文

### npm源还原默认设置

```shell 
$ npm config edit
```

打开配置文件后删除`registry = https://registry.npm.taobao.org` 一行，便会还原为默认的npm源

使用`npm config get registry`查看当前源

-----------------

### cnpm的安装与使用

#### 安装cnpm 

```shell 
$ npm install -g cnpm --registry=https://registry.npm.taobao.org
```

#### 使用cnpm安装模块

```shell 
$ cnpm install [name]
```

#### 同步模块

直接通过 `sync` 命令马上同步一个模块, 只有 `cnpm` 命令行才有此功能:

```shell 
$ cnpm sync connect
```

#### 其它命令

支持 npm 除了 `publish` 之外的所有命令, 如:

```shell 
$ cnpm info connect
```