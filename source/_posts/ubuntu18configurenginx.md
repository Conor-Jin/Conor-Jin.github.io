---
title: ubuntu18 配置nginx服务器
tags: []
id: '182'
categories:
  - - ubuntu
date: 2019-07-02 21:21:57
---

## **注意：**

1.  nginx服务器可以直接从软件源中进行安装。
2.  注意防火墙以及云服务器的端口列表是否开放。

## 1\. 安装

更新软件源

$ sudo apt-get update

安装nginx

sudo apt-get install nginx

 

## 2\. 检测

$ sudo systemctl status nginx

![](http://jindk.wang/blog/wp-content/uploads/2019/07/15620725731.png) 出现如上图所示则成功 或者直接输入ip或者域名 ![](http://jindk.wang/blog/wp-content/uploads/2019/07/nginx成功.png) 以上两种情况均可验证  

## 3\. 管理进程

停止nginx服务器:

$ sudo systemctl stop nginx

  启动nginx服务器:

$ sudo systemctl start nginx

  重启nginx服务器:

$ sudo systemctl restart nginx

  只是简单地进行配置更改，Nginx通常可以重新加载而不会丢失连接：

$ sudo systemctl reload nginx

  默认情况下，Nginx配置为在服务器引导时自动启动 启动服务器自动启动Nginx：

$ sudo systemctl enable nginx

  关闭自动服务器自动启动Nginx

$ sudo systemctl disable nginx

 

## 4\. 配置Nginx

在ubuntu18 和 nginx 1.14.0的环境下  nginx 配置文件位置如下 /etc/nginx/sites-available/default 可以设置端口， 网站根目录 ， ssl ， 网站首页等等不一一展开