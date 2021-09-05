---
title: Edge调试安卓手机H5页面
tags: []
id: '369'
categories:
  - - 前端
date: 2020-08-06 18:48:11
---

一、前提 1.安卓手机，微信APP内打开url 2.PC浏览器，内核要求Chromium 3.手机打开开发者设置，USB调试   二、打开微信 http://debugx5.qq.com/页面，可扫描下面二维码 ![](https://jindk.wang/blog/wp-content/uploads/2020/08/截屏2020-08-06-下午6.51.24.png)   三、http://debugx5.qq.com/  配置   信息tab下面，勾选"打开TBS内核Inspector调试功能"和"打开TBS内核X5jscore Inspector调试功能" 渲染Tab下，抓取配置页面，填写目标网址，例如 https://m.baidu.com/   点击 开始抓取 RenderLog 按钮，进行页面跳转   三、打开浏览器调试页面 以Edge浏览器为例，打开 [edge://inspect/#devices](edge://inspect/#devices) 安卓USB连接电脑，打开开发者配置，开启USB调试，这时页面会显示链接成功， ![](https://jindk.wang/blog/wp-content/uploads/2020/08/截屏2020-08-06-下午6.58.31.png) 如图则是链接成功，如果连接失败，注意驱动等   四、进行调试 点击 inspect 即可进行调试