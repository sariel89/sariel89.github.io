---
layout: post
title: MJRefresh 源码阅读
---
## 简介
MJRefresh是iOS开发过程中最常用的几个三方库之一，以无侵入式的加载方式和超级简单的集成逻辑深受广大开发者的喜爱。我对于它实现原理虽然有所了解，但是一直没有仔细看过。所以今天就来看一下内部的实现逻辑。
## 基本信息
#### 类结构
![MJRefresh类结构](/assets/images/MJRefresh%E7%B1%BB%E7%BB%93%E6%9E%84.png)
#### 类说明
`MJRefresh` 组件的头文件，外部调用的时候直接`import`这个文件就可以了
`MJRefreshConst` 定义了组件会用到的常量信息和宏
`UIView+MJExtension` 关于`UIView`的扩展，扩展了基本`frame`信息
## 调用逻辑

## 原理解析

## 总结

## 附录
