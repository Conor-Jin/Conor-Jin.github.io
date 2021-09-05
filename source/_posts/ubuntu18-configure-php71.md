---
title: ubuntu18 配置php7.1
tags: []
id: '188'
categories:
  - - 前端
date: 2019-07-02 21:51:01
---

## 1.安装

$ sudo apt-get install software-properties-common
$ sudo add-apt-repository ppa:ondrej/php
$ sudo apt-get update
$ sudo apt-get install -y php7.1
$ sudo apt-get -y install php7.1-mysql
$ sudo apt-get install php7.1-fpm
$ apt-get install php7.1-curl php7.1-xml php7.1-mcrypt php7.1-json php7.1-gd php7.1-mbstring

 

## 2.检测

$ php-v

![](http://jindk.wang/blog/wp-content/uploads/2019/07/php7.1.png) 如图则成功  

## 3.配置(PHP)

$ sudo vim /etc/php/7.1/fpm/php.ini

将cgi.fix\_pathinfo=1这一行去掉注释，将1改为0  

$ sudo vim /etc/php/7.1/fpm/pool.d/www.conf

配置这个 listen = /var/run/php7.1-fpm.sock  

$ sudo service php7.1-fpm restart

重启php-fpm 模块  

## 4.配置(Nginx)

PHP-FPM 与 Nginx 通信方式有两种，一种是基于TCP的 Internet domain socket 方式，一种是 UNIX domain socket 方式。 这里的 3/4步骤是基于  UNIX domain socket 方式  

$ sudo vim /etc/nginx/sites-available/default

修改Nginx配置文件  

location ~ \\.php$ {
        include snippets/fastcgi-php.conf;
        # With php7.0-cgi alone:
        # fastcgi\_pass 127.0.0.1:9000;
        # With php7.0-fpm:
        fastcgi\_pass unix:/run/php/php7.1-fpm.sock;
    }

  Nginx已经为与 PHP-FPM的整合准备好了，只要吧注释去掉即可，只需要将下面这部分改好就可以了。sock文件路径为 /run/php/php7.1-fpm.sock 。（视安装php版本而定）  

$ sudo systemctl restart nginx

重启nginx即可  

## 5.检测

  新建php文件，phpinfo()，页面成功运行即可