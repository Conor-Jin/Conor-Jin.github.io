---
title: linux yum
tags: []
id: '353'
categories:
  - - ubuntu
date: 2020-06-29 11:38:02
---

1.创建yum 文件夹

mkdir install yum

  2.进入yum文件夹

cd yum

  3.解压

tar -xvf yum-3.2.28.tar.gz

手动创建一个yum的conf文件，不然会报找不到文件的错yum.cli:Config Error: Error accessing file for config file:///etc/ touch /etc/yum.conf(存疑)   4.安装

cd yum-3.2.28
sudo apt install yum

  5.更新到新版本

yum check-update
yum update
yum clean all