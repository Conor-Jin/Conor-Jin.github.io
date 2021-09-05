---
title: 简单说明MVC/MVP/MVVM
tags: []
id: '142'
categories:
  - - 设计模式
date: 2018-10-02 16:53:11
---

## **一．来源**

MVC，MVP，MVVM　是三种常见的前端架构模式，它通过分离关注点来改进代码组织方式。MVC称得上业内传统的设计模式，MVP，MVVM　皆是从MVC中演化而来。  

## **二．MVC**

MVC即 Model-View-Controller ，核心部分分为 Model（数据）、View（视图）、Controller（控制），这三部分的通讯关系如下图（盗用阮一峰老师的解释图）。   ![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015020105.png)

1.  View 传送指令到 Controller
2.  Controller 完成业务逻辑后，要求 Model 改变状态
3.  Model 将新的数据发送到 View，用户得到反馈

 

## **二．MVP**

MVP 模式将 Controller 改名为 Presenter，同时改变了通信方向。 ![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015020109.png) 1. 各部分之间的通信，都是双向的。 2. View 与 Model 不发生联系，都通过 Presenter 传递。 3. View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而 Presenter非常厚，所有逻辑都部署在那里。  

## **三．MVVM**

MVVM 模式将 Presenter 改名为 ViewModel，基本上与 MVP 模式完全一致。![](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015020110.png) 唯一的区别是，它采用双向绑定（data-binding）：View的变动，自动反映在 ViewModel   注： 以上大多数摘自阮一峰老师的博客：http://www.ruanyifeng.com/blog/2015/02/mvcmvp\_mvvm.html  

## **四．个人习惯**

就我使用习惯而言，使用更多的是MVP（原生JS）、MVVM（VUE）。并没有使用MVC的经验，在于更习惯视图（V）和数据（M）分开，减少耦合，将更核心的代码（逻辑）放到 P/VM 上面。当然也都不是万能的，一般在公司的项目偏web应用较多，使用MVP虽然代码分离的很舒服，但是项目越大，逻辑越复杂，这个P 就越发的臃肿，所以真的感觉MVVM中VM非常的舒服。