---
title: vue项目初始化
tags: []
id: '96'
categories:
  - - vue
date: 2018-09-07 10:16:57
---

默认使用 webpack 和 npm

## **Vue-cli初始化**

1、利用npm包管理工具，进行安装

npm install vue-cli -g

\-g 代表全局 安装好vue的脚手架以后，我们就可以在命令行中使用一个命令：vue

## **Vue 初始化**

语法： vue init webpack  demoName demoName 代表创建项目名称，如果不写则直接在该目录下创建

vue init webpack

![](http://jindk.wang/blog/wp-content/uploads/2018/09/vue-init.png) 如上图所示，输入完成命令后会有一些配置选项，全部填完后即可等待安装

## **Vuex 初始化**

vuex是一个专门为vue.js设计的集中式状态管理架构。状态？我把它理解为在data中的属性需要共享给其他vue组件使用的部分，就叫做状态。简单的说就是data中需要共用的属性。 1、利用npm包管理工具，进行安装 vuex

npm install vuex --save

![](http://jindk.wang/blog/wp-content/uploads/2018/09/vuex-init.png) 注： - -save 为保存 2、新建一个store文件夹（这个不是必须的），并在文件夹下新建store.js文件，文件中引入我们的vue和vuex

import Vue from 'vue';
import Vuex from 'vuex';

  3、使用我们vuex，引入之后用Vue.use进行引用

Vue.use(Vuex);

4、在main.js 中引入新建的vuex文件

import store from './vuex/store'

5、再然后 , 在实例化 Vue对象时加入 store 对象

new Vue({
   el: '#app',
   router,
   store,//使用store
   template: '<App/>',
   components: { App }
})

 

## **安装配置sass**

1、利用npm包管理工具，进行安装 依赖

npm install --save-dev sass-loader
//sass-loader依赖于node-sass
npm install --save-dev node-sass

2、利用build文件夹下的webpack.base.conf.js的rules里面添加配置

{
  test: /\\.sass$/,
  loaders: \['style', 'css', 'sass'\]
}

3、 vue 文件修改 style 标签

<style lang="scss" scoped="" type="text/css">

</style>