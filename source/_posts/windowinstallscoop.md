---
title: window下安装Scoop
tags: []
id: '309'
categories:
  - - 其他
date: 2020-03-07 22:45:00
---

## 一、系统要求

Windows 7 SP1+ / Windows Server 2008+\* PowerShell 3+\* .NET Framework 4.5+

并且需要翻墙

## 二、准备

先设置 PowerShell 允许执行未签名脚本

Set-ExecutionPolicy RemoteSigned -scope CurrentUser

 

## 三、安装

下载 Scoop 安装脚本进行

iex (new-object net.webclient).downloadstring('https://get.scoop.sh')

 

## 四、成功

Initializing...
Downloading scoop...
Extracting...
Creating shim...
Downloading main bucket...
Extracting...
Adding ~\\scoop\\shims to your path.
'lastupdate' has been set to '2019-08-11T09:35:38.2537719+08:00'
Scoop was installed successfully!
Type 'scoop help' for instructions.

 

## 五、常用命令

scoop search 搜索软件名
scoop install 安装软件
scoop update 更新软件
scoop status 查看软件状态
scoop uninstall 卸载软件
scoop info 查看软件详情
scoop home 打开软件主页
scoop list 查看已安装软件列表

// bucket源
scoop bucket list 查看bucket源
scoop bucket add \[bucket源\] 添加bucket源
scoop bucket rm \[bucket源\] 移除bucket源

// 切换软件不同版本
scoop reset python27 切换27版本
scoop reset python 切换3版本

 

## 六、添加常用bucket

scoop bucket add extras
scoop bucket add versions
scoop bucket add java

## 七、安装java

// 先安装java源
scoop bucket add java
// 再安装
scoop install oraclejdk13