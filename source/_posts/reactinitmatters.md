---
title: 初用react注意事项
tags: []
id: '250'
categories:
  - - react
  - - 前端
date: 2019-10-16 15:01:39
---

## **一、绝对路径问题**

1.使用官方脚手架安装不会暴露webpack的配置，需要运行

npm run eject

成功之后（之前会有提示，git上传接文件即可） npm run eject过后就会生成两个文件夹 ![](http://jindk.wang/blog/wp-content/uploads/2019/10/20190415101622250副本.png)   2.然后找到config文件里面的webpack.config.js ![](http://jindk.wang/blog/wp-content/uploads/2019/10/20190415101754810副本.png)   3.搜索alias 并改成一下代码 ![](http://jindk.wang/blog/wp-content/uploads/2019/10/屏幕快照-2019-10-16-14.59.19.png)   4.然后再在页面里面把相对路径改成以@开头的绝对路径 ![](http://jindk.wang/blog/wp-content/uploads/2019/10/屏幕快照-2019-10-16-15.00.22.png) 5.重启项目  

## **二、antd 按需要引用组件无效**

1.先按照antd

npm install --save antd

  2.按需引用组件 ![](http://jindk.wang/blog/wp-content/uploads/2019/10/屏幕快照-2019-10-16-16.41.25.png)   3.这是使用无效。因为antd默认引入样式是less，所以需要手动配置为CSS，配置babel 安装 babel-plugin-import

npm install babel-plugin-import --save

  4.在package.json中配置，这种方法成功的前提是webpack里query下配置babelrc：true， 这样就会使用babelrc文件中的配置

  "babel": {
    "presets": \[
     "react-app"
    \],
    "plugins": \[
     \[
      "import",
      {
       "libraryName": "antd",
       "style": "css"
      }
     \]
    \]
  }

 

## **三、利用 styled-components** **修改** **antd 样式**

方法1.如图所示，再 antd 组件中引入 style样式 （与styled-components 无关） ![](http://jindk.wang/blog/wp-content/uploads/2019/10/屏幕快照-2019-10-17-16.49.19.png) ![](http://jindk.wang/blog/wp-content/uploads/2019/10/屏幕快照-2019-10-17-16.49.47.png)   方法2. 在styled-components 中引入 antd 组件 修改 css 样式 ![](http://jindk.wang/blog/wp-content/uploads/2019/10/屏幕快照-2019-10-17-16.59.40.png) ![](http://jindk.wang/blog/wp-content/uploads/2019/10/屏幕快照-2019-10-17-17.00.01.png)