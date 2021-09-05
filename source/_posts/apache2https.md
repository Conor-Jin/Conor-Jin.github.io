---
title: apache2开启https
tags: []
id: '325'
categories:
  - - 网络
date: 2020-06-06 18:25:04
---

## 一、背景

ubuntu14，apache2，证书过期重新更换

 

## 二、分别修改，配置文件

sudo vi /etc/apache2/sites-available/000-default.conf

<VirtualHost \*:80>
        // 邮箱
ServerAdmin aaaa@aaa.com
        // 域名
ServerName www.xxx.wang
        // 根目录
DocumentRoot /var/www/html
        // 开启http强制跳转https
RewriteEngine on
RewriteCond %{HTTPS} !=on
RewriteRule   ^(.\*)  https://%{SERVER\_NAME}$1 \[L,R\]
ErrorLog ${APACHE\_LOG\_DIR}/error.log
CustomLog ${APACHE\_LOG\_DIR}/access.log combined
</VirtualHost>

 

sudo vi /etc/apache2/sites-available/default-ssl.conf

<IfModule mod\_ssl.c>
<VirtualHost \*:443>
// 邮箱
ServerAdmin aaaa@aaa.com
// 域名
ServerName www.xxx.wang
// 根目录
DocumentRoot /var/www/html

ErrorLog ${APACHE\_LOG\_DIR}/error.log
CustomLog ${APACHE\_LOG\_DIR}/access.log combined

SSLEngine on
SSLProxyEngine On
SSLProxyVerify none
SSLCertificateFile /etc/ssl/2020/2\_www.jindk.wang.crt
SSLCertificateKeyFile  /etc/ssl/2020/3\_www.jindk.wang.key
SSLCertificateChainFile /etc/ssl/2020/1\_root\_bundle.crt


<FilesMatch "\\.(cgishtmlphtmlphp)$">
SSLOptions +StdEnvVars
</FilesMatch>
<Directory /usr/lib/cgi-bin>
SSLOptions +StdEnvVars
</Directory>

</VirtualHost>
</IfModule>

# vim: syntax=apache ts=4 sw=4 sts=4 sr noet

 

## 三、确保生效，进行其他配置

1.开启SSL模块

sudo a2enmod ssl

2.启用SSL站点

sudo a2ensite default-ssl

3.加入监听端口 443

sudo gedit /etc/apache2/ports.conf

4.启动重定向

sudo a2enmod rewrite

5.重新加载配置

sudo service apache2 reload

6.重启apache2

sudo service apache2 restart

7.查看端口开放情况

netstat -tnl

  注：

1.  5/6 执行一个即可，一个是重新加载apache配置文件，另一个是重启服务
2.  需要注意阿里云/腾讯云等运营商设置相关端口开放