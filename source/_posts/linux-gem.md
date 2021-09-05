---
title: Linux gem
tags: []
id: '349'
categories:
  - - ubuntu
date: 2020-06-29 10:53:42
---

1.查看源地址

gem source -l

  2.删除默认的源地址

gem sources -r url地址

gem source -r https://rubygems.org/

注：默认的url地址后必须有”/”,否则删不掉   3.添加源地址

gem sources -a https://gems.ruby-china.com

  4.更新源的缓存

gem sources -u

  5.安装sass

sudo gem install sass

  6.查看sass 版本

sass -v