---
title: 常用命令
tags: []
id: '328'
categories:
  - - ubuntu
date: 2020-06-06 18:40:07
---

1.scp 以从win到远程服务器为例子

scp E:\\tst\\a.png root@127.0.9.090:/a/v/c

  2.修改文件夹权限 以 修改/a/c/z文件夹权限为777为例

sudo chmod 777 /a/c/z

  3.查看端口号占用 以3000端口为例

lsof -i :3000

![](https://jindk.wang/blog/wp-content/uploads/2020/06/截屏2020-06-12-下午9.43.18.png) 关闭占用 kill -9 PID

 kill -9 5166

  4.tail 命令 tail 命令可用于查看文件的内容，有一个常用的参数 \-f 常用于查阅正在改变的日志文件。 tail -f filename 会把 filename 文件里的最尾部的内容显示在屏幕上，并且不断刷新，只要 filename 更新就可以看到最新的文件内 容。 -n 表示行数 以 error-1.log 文件为例子，查看最近200行代码，

tail /a/b/c/d/logs/error-1.log -n 200 -f

  5.ssh 链接远程服务器 以 name 为用户名，地址为 127.0.0.1为例子

ssh name@127.0.0.1

输入密码即可远程链接服务器