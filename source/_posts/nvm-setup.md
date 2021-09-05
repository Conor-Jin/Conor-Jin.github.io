---
title: nvm 配置
tags: []
id: '334'
categories:
  - - mac
date: 2020-06-12 16:27:55
---

1.前言 为了解决node各种版本存在不兼容现象，nvm是让你在同一台机器上安装和切换不同版本的node的工具   2.安装

curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.29.0/install.sh  bash

配置变量，打开文件

vim ~/.bashrc

添加

export NVM\_DIR="$HOME/.nvm"
\[ -s "$NVM\_DIR/nvm.sh" \] && . "$NVM\_DIR/nvm.sh" # This loads nvm

生效

source ~/.bashrc

  3.常见命令

nvm ls-remote 列出所有可安装的版本

nvm install <version> 安装指定的版本，如 nvm install v8.14.0

nvm uninstall <version> 卸载指定的版本

nvm ls 列出所有已经安装的版本

nvm use <version> 切换使用指定的版本

nvm current 显示当前使用的版本

nvm alias default <version> 设置默认 node 版本

nvm deactivate 解除当前版本绑定