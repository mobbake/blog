---
title: 备份vscode的插件
date: 2018-06-07 08:52:05
tags: 效率
categories: 工具
---

## setting sync 是vscode中同步设置和安装插件的小工具

在扩展商店中搜索并安装它

## 利用github帐户进行备份

登陆github>用户头像 > settings > developers > Personal access tokens > Generate new token

输入描述比如vscode ,勾选gist,> generate token

保存生成的token。

## 在vscode 上配置

1.快捷键 shift+alt+u 或 ctrl+p 输入>sync点击update/updload settings

2.把之前复制的access token粘贴后回车

3.成功后跳出如下图，复制GITHUB GIST的内容，在需要同步的另一台电脑上使用

## 在需要同步的电脑打开VSCode,安装相同的插件

## 按快捷键 shift+alt+d 或 ctrl+p 输入>sync点击Download Settings

## 把GITHUB GIST的内容粘贴然后回车