---
title: iis8，7 兼容iis6
date: 2018-03-07 08:52:05
tags: [iis, ASP]
categories: 开发
---

# iis8，7 兼容iis6

## 启用asp动态页面

启用或关闭windows打开iis

在应用程序开发功能中勾选ASP及ISAPI扩展

## 打开asp报错调试

双击右边的ASP图标

展开右侧配置中的“调试属性”，把“将错误发送到浏览器”的值设为 "true"

## **ADODB.Connection 错误 '800a0e7a' 未找到提供程序**

因为系统是64位的win7或win8.1所以会出现这个问题，解决方法如下：

找到IIS应用程序池，“设置应用程序池默认属性”->“常规”->”启用 32 位应用程序”，设置为 True