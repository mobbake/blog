---
title: vscode 的使用
date: 2018-07-01 08:52:05
tags: 效率
categories: 工具
---

# vscode 的使用

## 用户代码段

设置用户代码段file> preferences> user snippets

选择对应语言如js

example:

```json
"Nodejs require": {
    "prefix": "conreq",
    "body": "const $1 = require('$1')",
    "description": "Node require module"
  }
```

## 注释的使用技巧

### 特殊注释

`TODO`正在做但有紧急任务而未完成的标记

`FIXME`发现的bug

`NOTE` 提醒注意

`XXX`如果代码中有该标识，说明标识处代码虽然实现了功能，但是实现的方法有待商榷，希望将来能改进

`BUG`有bug

`OPTIMIZE`需要优化

`HACK`。。。

### 函数注释

```js
/***********************************************************************************************
*函数名 ： 
*函数功能描述 ： 
*函数参数 ： 
*函数返回值 ： 
*/
```

快捷键，在一个函数上方输入`/**`按`tab`