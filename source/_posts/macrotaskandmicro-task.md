---
title: JS中macro-task(宏任务)与micro -task(微任务)
tags: []
id: '291'
categories:
  - - 前端
date: 2019-11-18 21:47:38
---

## 一、前提 同步异步

JS是一门单线程的语言，换言之就是无论如何都只有一个主线程来处理任务，所以为了加快处理速度，会将**异步任务挂载起来（pending）**，优先执行同步任务。  

## 二、异步划分

  ![](http://jindk.wang/blog/wp-content/uploads/2019/11/异步分类.png) 异步分为macro-task(宏观任务)与micro -task(围观任务)。存放顺序都为先后顺序，反之执行顺序也是如此，更深入则是涉及到事件机制，这里不表。 既然执行顺序为先后顺序，划分又为宏观与微观，这两种执行顺序又怎样呢？   **微观任务完成才会执行宏观任务**  

## 三、demo

async function async1() {
    console.log('async1 start');
    await async2();
    console.log('async1 end');
}
async function async2() {
    console.log('async2');
}

console.log('script start');

setTimeout(function() {
    console.log('setTimeout');
}, 0)

async1();

new Promise(function(resolve) {
    console.log('promise1');
    resolve();
}).then(function() {
    console.log('promise2');
});
console.log('script end');

  执行顺序

script start
async1 start
async2
promise1
script end
async1 end
promise2
setTimeout

 

## 四、解析

![](http://jindk.wang/blog/wp-content/uploads/2019/11/macrotaskandmicrotask.png)   注意： 1.async/await实际上是promise+generator的语法糖，也就是promise，也就是微观任务 2.promise函数是同步