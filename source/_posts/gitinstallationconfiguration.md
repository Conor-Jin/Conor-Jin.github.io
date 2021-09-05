---
title: git的安装配置
tags: []
id: '149'
categories:
  - - 其他
date: 2018-10-11 23:17:56
---

## **一、安装**

直接进入官网 https://git-scm.com/downloads/ 下载，被墙的烈害，没有梯子可以下载网友分享的。 安装的话，一路默认，除了  **设置环境变量：选择使用什么样的命令行工具，一般情况下选择默认，使用Git Bash** 这个要注意之外  

## **二、配置**

为了推送、拉取足够快，选择国内的代码托管平台码云，注册过程省略。直接进行配置，从码云的设置中找到SSH公钥，进行添加（码云有足够简单的教程）。 以window系统为例子，在要建立代码仓库的地方鼠标右键，选择  Git Bash Here，进入终端之后，输入

ssh-keygen -t rsa -C "xxxxx@xxxxx.com"

安照提示完成三次回车，即可生成 ssh key。通过查看 `~/.ssh/id_rsa.pub` 文件内容，获取到你的 public key   ![SSH生成](https://images.gitee.com/uploads/images/2018/0814/170141_5aa5bc98_551147.png "SSH生成")   复制生成后的 ssh key，通过项目主页 **「管理」->「部署公钥管理」->「添加部署公钥」** ，添加生成的 public key 添加到项目中。  

## **三、检测**

在终端（Terminal）中输入

ssh -T git@gitee.com

若返回 `Hi XXX! You've successfully authenticated, but Gitee.com does not provide shell access.` 内容，则证明添加成功。  

## 四、clone 项目

在已经创建好的项目中，选择 clone  复制 SSH链接。在要建立代码仓库的地方鼠标右键，选择  Git Bash Here，进入终端之后 输入

git clone git@gitee.com:dadsasdasdasdasd

git@gitee.com:dadsasdasdasdasd 即复制的SSH链接 这样即可