---
title: nvm的使用及配置
date: 2018-06-06 15:53:52
tags: [npm, Node.js]
categories: Node.js
---

## 1. nvm 下载与安装

nvm的项目地址[nvm-windows](https://github.com/coreybutler/nvm-windows)

下载解压得到 nvm-setup.exe，安装

个人习惯安装在`c:dev/nvm`

## 2. nvm配置

### npm 与 node 的下载地址设置

官方下载地址可能缓慢，把下载地址配置为淘宝镜像地址
打开nvmp安装包，settings.txt文件

加上

```
node_mirror: http://npm.taobao.org/mirrors/node/
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

### 环境变量的检查

默认的安装后在环境变量里会自动配置了 NVM_HOME 和 NVM_SYMLINK

NVM_HOME 为nvm的对应安装位置，NVM_SYMLINK为nodejs的默认安装位置

例如：

```
NVM_HOME： C:\dev\nvm
NVM_SYMLINK ： C:\dev\nodejs
```

在PATH里加上;%NVM_HOME%;%NVM_SYMLINK%;

### 检测安装结果 

`nvm -v`显示当前安装的nvm版本

## 3.安装nodejs

输入：`nvm install [版本号]`，下载最新版的可以直接输`nvm install latest`

下载完成后，在控制台输入：`nvm use [版本号]`。即使用这个版本号的node了。在use后，上面所说的nodejs文件夹就自动生成了。（在use之前是没有的哦）

## 4.常用命令

```
nvm install <version> ## 安装指定版本，可模糊安装，如：安装v4.4.0，既可nvm install v4.4.0，又可nvm install 4.4

nvm uninstall <version> ## 删除已安装的指定版本，语法与install类似

nvm use <version> ## 切换使用指定的版本node

nvm ls ## 列出所有安装的版本

nvm ls-remote ## 列出所以远程服务器的版本（官方node version list）

nvm current ## 显示当前的版本

nvm alias <name> <version> ## 给不同的版本号添加别名

nvm unalias <name> ## 删除已定义的别名

nvm reinstall-packages <version> ## 在当前版本node环境下，重新全局安装指定版本号的npm包
```