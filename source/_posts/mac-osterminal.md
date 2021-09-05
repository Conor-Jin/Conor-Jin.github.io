---
title: mac os终端常用命令记录
tags: []
id: '165'
categories:
  - - mac
date: 2018-11-17 13:21:03
---

## 1.终端中删除非空文件夹

rm \-r \-f filename

或者使用管理员账号

sudo rm -r -f filename

 

## 2.终端进入 vim

vim xx.xx/vi xx.xx

亦或者使用管理员账号

sudo vim xx.xx/vi xx.xx

 

## 3.终端退出 vim

按下ESC后输出，才能进入命令模式 保存并退出

:qw!

不保存退出

:q

注： 命令后面 + ! 是强制的意思

## 4.终端中解压命令

### tar （注：tar是打包，不是压缩！）

解包：tar xvf FileName.tar
打包：tar cvf FileName.tar DirName

### .gz

解压1：gunzip FileName.gz
解压2：gzip -d FileName.gz
压缩：gzip FileName

### .tar.gz 和 .tgz

解压：tar zxvf FileName.tar.gz
压缩：tar zcvf FileName.tar.gz DirName

### .bz2

解压1：bzip2 -d FileName.bz2
解压2：bunzip2 FileName.bz2
压缩： bzip2 -z FileName

 

### .tar.bz2

解压：tar jxvf FileName.tar.bz2
压缩：tar jcvf FileName.tar.bz2 DirName

 

### .bz

解压1：bzip2 -d FileName.bz
解压2：bunzip2 FileName.bz

 

### .tar.bz

解压：tar jxvf FileName.tar.bz

 

### .Z

解压：uncompress FileName.Z
压缩：compress FileName

 

### .tar.Z

解压：tar Zxvf FileName.tar.Z
压缩：tar Zcvf FileName.tar.Z DirName

 

### .zip

解压：unzip FileName.zip
压缩：zip FileName.zip DirName

 

### .lha

解压：lha -e FileName.lha
压缩：lha -a FileName.lha FileName

 

### .rpm

解包：rpm2cpio FileName.rpm  cpio -div

 

### .deb

解包：ar p FileName.deb data.tar.gz  tar zxf -