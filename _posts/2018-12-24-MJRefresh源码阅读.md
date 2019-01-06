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
`UIScrollView+MJExtension` 关于`UIScrollView`的扩展，扩展关于`frame`和`content`的信息
`UIScrollView+MJRefresh` 关于`UIScrollView`的扩展，扩展了头部和底部刷新相关的组件
`NSBundle+MJRefresh` 关于资源文件的扩展，用于获取库中包含的资源文件

`MJRefreshComponent` 组件的基类，定义了刷新相关的方法，以及对`ScrollView`的滑动，`contentsize` 变化等情况的监听。对于其中某些方法是要子类实现的。

`MJRefreshHeader` 顶部下拉刷新，定义了下拉刷新需要使用的基本信息和对基类方法的实现，基本完成下拉刷新需要的逻辑功能
`MJRefreshStateHeader` 初始化组件的位置
`MJRefreshNormalHeader` 默认下拉刷新样式，对于默认下拉样式的定义
`MJRefreshGifHeader` 为下拉刷新的几种状态定制动画

`MJRefreshFooter` 底部上拉刷新，定义了上拉刷新需要使用的基本信息和对基类方法的实现，基本完成上拉刷新需要的逻辑功能
`MJRefreshBackFooter` 手动触发刷新，确定触发的位置，刷新过程中各个状态的设置
`MJRefreshBackStateFooter` 设置各个状态的显示样式
`MJRefreshBackNormalFooter` 默认上拉刷新样式，不同刷新状态在默认情况下的位置等设置
`MJRefreshBackGifFooter` 为上拉刷新的几种状态定制动画
`MJRefreshAutoFooter` 自动触发刷新，确定触发位置，刷新过程中的各种状态设置
`MJRefreshAutoStateFooter` 初始化组件的位置
`MJRefreshAutoNormalFooter` 默认上拉刷新样式，不同刷新状态在默认情况下的位置等设置
`MJRefreshAutoGifFooter` 为上拉刷新的几种状态定制动画

## 调用逻辑
调用代码就可以设置默认样式的下拉刷新：
```
self.scrollView.mj_header = [MJRefreshNormalHeader headerWithRefreshingBlock:^{
        
    }];
```
或者 
```
self.scrollView.mj_header = [MJRefreshNormalHeader headerWithRefreshingTarget:self refreshingAction:@selector(mjrefreshHeader:)];
```
这样设置之后就可以下拉看效果啦。

在需要结束动画的时候，调用
```
[self.scrollView.mj_header endRefreshing];
```
就可以结束下拉刷新动画，这句代码的调用其实就是设置`mj_header`的状态。

`footer`的调用方式和`header`是一样的。
## 原理解析
调用上面的方法之后，就会开始监听`scrollView`的`contentOffset`、`contentSize`和`state`等方法。
监听`contentOffset`和`state`方法可以知道什么时候修改状态；
监听`contentSize`方法可以知道是否需要修改header的位置(通常来讲，header位置基本不用修改，footer位置需要修改)。

## 总结
在实现的过程中，修改状态的时候要对当前当前`scrollView`的状态，方式出现意外情况。
下拉刷新的逻辑是比较简单的，但是本库在实现过程中考虑了很多平时我不太会考虑到的地方。全面考虑各种情况是我需要学习的地方。
