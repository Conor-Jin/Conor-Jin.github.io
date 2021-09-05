---
title: mac mysql设置
tags: []
id: '331'
categories:
  - - mac
date: 2020-06-12 15:51:57
---

1，安装不表   2.mysql设置软链接

cd /usr/local/bin/

ln -s /usr/local/mysql/bin/mysql /usr/local/bin/

  3.验证

mysql --version

mysql  Ver 8.0.20 for macos10.15 on x86\_64 (MySQL Community Server - GPL)

看到以上即安装成功   4.登录mysql

mysql -u root -p

  5.退出MySQL `exit` 或者 `quit`   6.其他常用命令

创建数据库：create database test;

查询数据库:  show databases;

选择数据库：use test;

删除数据库:  drop database test;

  7.Sequel pro 始终出于loading状态，无法切换到数据库 [https://sequelpro.com/test-builds](https://sequelpro.com/test-builds), 升级版本sequelpro，先使用测试版 [https://github.com/sequelpro/sequelpro/issues/2699](https://github.com/sequelpro/sequelpro/issues/2699) 报错原因。 mysql8.0升级后造成的