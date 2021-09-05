---
title: Js数组去重
tags: []
id: '50'
categories:
  - - 原生JS
date: 2018-09-05 10:29:51
---

**Js中使用算法的时候并不多，数组去重属于非常基础的功能，下面三种属于我感觉比较有意思的。** 先定义要去重的数组

var arr = \[1,12,12,5,2,2,9,3,10,3,12,13,20,2,1,20,2,1\]

一、排序后相邻去除法

// 先排序
function sortByGradeDown(arrA, arrB) {
if (arrA == arrB) {
return 0
} else if (arrA > arrB) {
return 1
} else if (arrA < arrB) {
return -1
}
}
// 再去重
function duplicateRemoval(arr) {
var a = \[\]
a.push(arr\[0\])
for (let i = 0; i < arr.length; i++) {
if (i == arr.length - 1) {
} else {
if (arr\[i\] !== arr\[i + 1\]) {
a.push(arr\[i + 1\])
}
}
}
return a
}

  **二、下标法** 相对比较讨巧使用 indexOf() 方法

function duplicateRemoval (arr) {
   var a = \[\]
   for (let i=0; i<arr.length; i++) {
      if(a.indexOf(arr\[i\]) == -1) {
 a.push(arr\[i\])
      }
   }
   return a
}

  **三、借用数组特性**

var arr = \[0,2,3,4,4,0,2\];
var obj = {};
var tmp = \[\];
for(var i = 0 ;i< arr.length;i++){
   if( !obj\[arr\[i\]\] ){
      obj\[arr\[i\]\] = 1;
      tmp.push(arr\[i\]);
   }
}
console.log(tmp);

    **四、ES6 Set** ES6的新方法

function duplicateRemoval (arr) {
    var x = new Set(arr)
    return \[...x\]
}