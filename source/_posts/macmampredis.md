---
title: MAC版MAMP环境下为PHP7.x安装redis扩展
tags: []
id: '170'
categories:
  - - mac
date: 2018-11-17 13:38:36
---

## 1.依赖安装 Homebrew

（Mac 电脑中已安装了 Homebrew 包管理器的可忽略此步）如果你的 MAC 电脑未安装有 Homebrew——一个包管理器，需要先安装 Homebrew 包管理器，后面步骤中的 ./configure 命令和安装 redis 服务端的命令等需要 brew 为其安装组件。 打开 terminal，安装 Homebrew：

/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)

脚本在执行过程中会有多次暂停，并说明将它将做什么；同时也会边执行、边需要联网下载资源，下载速度不会很快（因为是国内网络访问国外站点资源），请耐心等待安装完成。  

## 2.依赖安装 configure

（Mac 电脑中已安装了 configure 配置组件的可忽略此步）使用 brew 命令安装 configure 配置组件。

brew install autoconf wget

 

## 3.下载 php-redis 扩展组件的安装包

在终端中使用 git clone 命令下载 php-redis 扩展组件的安装包

git clone https://github.com/nicolasff/phpredis.git

下载完成后系统会自动解压安装包文件。如果未自动解压，请手动解压或使用 unzip phpredis.zip 命令解压。 解压后使用 cd 命令进入 phpredis 目录：

cd phpredis/

 

## 4.使用 phpize 命令编译生成 configure 配置文件

phpize 命令： 此时终端显示的当前目录是 phpredis，在终端中执行以下命令：

/Applications/MAMP/bin/php/php7.2.1/bin/phpize --with-php-config=/Applications/MAMP/bin/php/php7.2.1/bin/php-config

如果出现此错误：

Cannot find autoconf. Please check your autoconf installation and the $PHP\_AUTOCONF environment variable. Then, rerun this script.

则是因为此命令依赖 autoconf 工具，需要安装 autoconf 工具（参考第一步中的第2点）。 如果执行成功，会提示如下信息： ![](https://ss1.baidu.com/6ONXsjip0QIZ8tyhnq/it/u=2260770349,1912336145&fm=173&app=25&f=JPEG?w=640&h=106)  

## 5.配置、编译并安装 phpredis

配置 phpredis 命令。 此时终端显示的当前目录是 phpredis，在终端中执行以下命令

./configure --with-php-config=/Applications/MAMP/bin/php/php7.2.1/bin/php-config

如果执行出错，提示“未找到指定目录”之类的信息，也是因为此命令依赖 autoconf 工具，需要安装 autoconf 工具（参考第二步）。 如果执行成功，像这样： ![](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=2330634188,2198640965&fm=173&app=25&f=JPEG?w=640&h=427&s=ABE273235BBCB6C84ED5F50B0000E0C2) 编译与安装 phpredis 命令（make 是编译，make install 是安装）

make && make install

安装成功后，这时会在 phpredis/modules 目录下生成了 redis.so 文件。同时 redis.so 会自动复制到/Applications/MAMP/bin/php/php7.0.8/lib/php/extensions/no-debug-non-zts-20171025/ 目录下（extensions 后面带日期部分的那一级目录可能会与我的不一样，请以自己电脑上的为准）。如果该目录下不存在 redis.so，可手动将 phpredis/modules 目录下的 redis.so 复制过去。至此，phpredis 扩展已安装成功  

## 6.修改 php.ini

建议在 MAMP Pro 软件中打开 php.ini 文件并修改，因为在终端中使用 vim 命令编辑 php.ini 文件或手动打开编辑 php.ini 文件保存后可能不会起作用，所以建议在 MAMP Pro 软件中打开 php.ini 文件并修改： ![](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=2448095372,2140049450&fm=173&app=25&f=JPEG?w=639&h=259&s=F5259A545A65310B861E8AC30300B0BF) 在 php.ini 中搜索 "extension="，在后面添加一行："extension=redis.so"，保存后重启 MAMP。 ![](https://ss2.baidu.com/6ONYsjip0QIZ8tyhnq/it/u=185617445,1884557620&fm=173&app=25&f=JPEG?w=598&h=503&s=4FC2ED1A110E454D4A69A5DB0000D0B3)  

## 7.redis 组件是否安装成功

检测方案可以使用 php-m  也可以使用 phpinfo() 查看   注意：操作此步骤之前 必须将系统默认的php环境切换到MAMP中 参考：https://baijiahao.baidu.com/s?id=1602787432736329481&wfr=spider&for=pc