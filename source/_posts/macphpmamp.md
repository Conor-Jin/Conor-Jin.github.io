---
title: 切换Mac默认PHP版本为MAMP
tags: []
id: '167'
categories:
  - - mac
date: 2018-11-17 13:28:17
---

安装装了MAMP集成环境，打开终端输入：which php，会显示/usr/bin/php，这个就是是系统自带的PHP版本，要切换默认的PHP版本为MAMP下的PHP，需要修改系统bash\_profile并执行这个shell脚本。  

## 1.前期准备

先查看好 MAMP 相关对应PHP版本的路径，例如

/Applications/MAMP/bin/php/php5.5.38/

 

## 2.修改  .bash\_profile

sudo vim ~/.bash\_profile

然后把以下代码添加到bash\_profile脚本最后面：

export PATH="/Applications/MAMP/bin/php/php5.5.38/bin:$PATH"

注：路径就是MAMP 相关对应PHP版本的路径  

## 3.source  ~/.bash\_profile 使其生效

## 4. 再次执行 which php

检查路径是否已经切换成功   注意：如果你安装了zsh，会出现重新打开terminal窗口时会发现php又跳回自带的PHP 原因；这是terminal init的时候并不会执行~/.bash\_profile、~/.bashrc等脚本了，这是因为其默认启动执行脚本变为了～/.zshrc。 方案：vim ~/.zshrc，在后面追加：

source ~/.bash\_profile

![](https://upload-images.jianshu.io/upload_images/6188107-a418765145532b96.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/416/format/webp)   转自：https://www.jianshu.com/p/cb5b489c8d93?utm\_campaign=maleskine&utm\_content=note&utm\_medium=seo\_notes&utm\_source=recommendation