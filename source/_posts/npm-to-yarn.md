---
title: npm to yarn
date: 2018-07-26 09:45:13
tags: yarn
categories: 工具
---
# yarn的基本使用和与npm的主要区别

## yarn初始化(创建一个新项目)

`yarn init`这将打开一个用于创建Yarn项目的交互式表单，其中包含以下问题：

```json
name (your-project):
version (1.0.0):
description:
entry point (index.js):
git repository:
author:
license (MIT):
```

你既可以回答这些问题，也可以直接敲回车键（enter/return）使用默认配置或者留空。

## 添加依赖包

在使用一个包之前，你需要执行以下命令将其加入依赖项列表：

`yarn add [package]` 添加到 Dependencies

`yarn add --dev`添加到 devDependencies

`yarn add --peer` 添加到 peerDependencies

`yarn add --optional` 添加到 optionalDependencies

### 更新依赖包

`yarn upgrade [package]`

`yarn upgrade [package]@[version]`

`yarn upgrade [package]@[tag]`

这会更新package.json和yarn.lock 文件。

### 删除依赖包

`yarn remove [package]`

这会更新package.json和yarn.lock 文件。

## 安装依赖项

### 安装依赖

`yarn install` 是用于安装一个项目的所有依赖。 Yarn会从`package.json`中读取依赖，并将依赖信息存储到`yarn.lock`中。

如果你正在开发一个包，通常你会在以下情况之后进行依赖安装：

1. 你刚检出需要这些依赖项的项目代码。
2. 项目的另一个开发者添加了新的依赖，你需要用到。

### 安装选项

有很多参数可以控制依赖安装的过程，包括：

1. 安装所有依赖：`yarn` 或 `yarn install`
2. 安装一个包的单一版本：`yarn install --flat`
3. 强制重新下载所有包：`yarn install --force`
4. 只安装生产环境依赖：`yarn install --production`

## 与npm命令区别

CLI 命令比较

|npm (v5) |Yarn|
|  ------ | ------ |
|npm install  |   yarn install|
|(不适用)      |  yarn install --flat|
|(不适用)        |  yarn install --har
|npm install --no-package-lock   |yarn install --no-lockfile
|(不适用)           |yarn install --pure-lockfile
|npm install [package]            |  yarn add [package]
|npm install [package] --save-dev  | yarn add [package] --dev
|(不适用)                          |   yarn add [package] --peer
|npm install [package] --save-optional |yarn add [package] --optional
|npm install [package] --save-exact|yarn add [package] --exact
|(不适用)| yarn add [package] --tilde
|npm install [package] --global| yarn global add [package]
|npm update --global            |      yarn global upgrade
|npm rebuild | yarn install --force
|npm uninstall [package] | yarn remove [package]
|npm cache clean | yarn cache clean [package]
|rm -rf node_modules && npm install | yarn upgrade

`notice` 如果全局安装一个模块后bash提示找不到，使用`yarn global bin`
查看全局目录，将些目录添加到环境变量即可