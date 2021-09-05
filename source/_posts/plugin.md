---
title: Js插件封装
tags: []
id: '117'
categories:
  - - 原生JS
date: 2018-09-11 15:53:02
---

近日总结的相对简单的JS插件封装的模板  

;(function(){
    var demo  = function (options) {
        if(!(this instanceof demo)){return new demo(options)};
        this.options = this.extend({
            'x': 1,
            'y': 2,
            'z': 3
        },options)
        //初始化
        this.init();
    }
    demo.prototype = {
        init: function () {
            console.log(this.options.x)
            this.show()
            this.hide()
        },
        // 参数合并方法体
        extend: function (obj,obj2) {
            for (var key in obj2) {
                obj\[key\] = obj2\[key\]
            }
            return obj
        },
        show: function () {
            console.log('展开')
        },
        hide: function () {
            console.log('关闭')
        }
    }
    //暴露对象
    window.demo = demo
}())
// 使用方法 demo("args") 和 new demo("args")
demo({
    "x": "newX",
    "y": "newY",
    "c":"newC",
    fn1:function () {
        console.log("start")
    },
    fn2:function () {
        console.log("end")
    }
});