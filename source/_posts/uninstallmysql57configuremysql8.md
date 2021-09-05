---
title: linux卸载mysql5.7并配置mysql8
tags: []
id: '191'
categories:
  - - 前端
date: 2019-07-02 22:11:36
---

## 1.卸载mysql5.7

卸载：

$ sudo apt-get autoremove --purge mysql-server

$ sudo apt-get remove mysql-common

  清楚数据：

dpkg -l grep ^rcawk '{print $2}' sudo xargs dpkg -P

 

## 2.检测残留

$ sudo dpkg --listgrep mysql

查看mysql有哪些依赖  

$ sudo apt-get remove XXXXX

$ sudo apt-get autoremove  XXXXX

 

## 3.安装mysql8

注意： ubuntu会默认安装mysql5.7版本!!!  所以要先切换软件库   更新软件库：

sudo apt-get update

  在mysql官网下载8.0版本的deb文件并安装： https://dev.mysql.com/downloads/file/?id=477124 以 mysql-apt-config\_0.8.10-1\_all.deb，为例(一定要去官网下载最新版！！！) 切换到下载目录后执行安装命令

$ sudo dpkg -i mysql-apt-config\_0.8.10-1\_all.deb

  然后会弹出以下窗口，确认一下第一项MySQL Server & Cluster后面的版本是不是8.0版本，如果不是，将光标移动到此处，enter键修改成8.0。没问题后选OK ![](http://jindk.wang/blog/wp-content/uploads/2019/07/20180914221258288.png)   再次更新软件库:

$ sudo apt-get update

  安装mysql服务器:

$ sudo apt-get install mysql-server

  安装过程中，会弹出设置root用户的密码 ![](http://jindk.wang/blog/wp-content/uploads/2019/07/20180914221906522.png)   之后弹出选择加密方式，建议选择5.X ![](http://jindk.wang/blog/wp-content/uploads/2019/07/20180914222229652.png)  

## 4.测试

mysql -u root -p

输入密码成功登陆即可  

## 5.使用phpmyadmin

成功后在shell下输入mysql -u root -p，再输入密码能正常进入，但在phpmyadmin连接，提示无法连接，具体报错信息为

mysqli\_real\_connect(): The server requested authentication method unknown to the client \[sha256\_password\]

  原因； 8.0.11版本起，不再像mysql5.7及以前版本那样，设置用户密码时默认的验证方式为caching\_sha2\_password，如果发现升级mysql8.0.11后原有的程序不能连接mysql，可迅速在mysql command line client客户端用下面的命令设置成mysql5.7及以前版本的密码验证方式，同时MYSQL8.0.11下修改密码的方式与原先也不大一样，原先的部分修改密码的命令在mysql8.0.11下不能使用。   解决办法：为原来的验证方式，然后从新创建用户并授权即可

mysql -uroot -p
use mysql;
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql\_native\_password BY '你的密码';