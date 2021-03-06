---
title: JS闭包的理解
tags: []
id: '146'
categories:
  - - 原生JS
date: 2018-10-07 18:16:47
---

## 一、前提

JS作用域分为全局作用域以及局部作用域。**局部作用域内部可以访问全局作用域的变量，而局部作用域外面无法访问局部作用域的变量**。这个根本原因在于JS的作用域是以作用域链的形式存在，子作用域可以访问父作用域的数据，而父作用域不可以访问子作用域的数据，全局作用域是作为最上级的父作用域，所以采用以上的情况。

##  二、闭包

所以我理解的闭包就是——闭包是指一个可以访问另外一个函数作用域中的变量**的函数**（定义在函数内部的函数）。 或者说闭包打破了JS的作用域链的模式。  

## 三、 用处

用来保存一个需要持久保存的变量（封装JS插件）。   网络上关于闭包的解释和函数有很多，这里只是简单的说明我的理解情况。