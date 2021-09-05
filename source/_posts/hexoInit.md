---
title: hexo初始化
date: 2021-04-08 16:07:32
tags:
- 网络
---
#### 1.全局安装 hexo.js

注：node.js git github  等相关不做表述

`npm install -g hexo-cli`

```
npmiiii
1
1

```

```
npm aaa
```

---


```
if(userStatus) {
   that.switchRoleAnchor()
}
1
```

#### 2.检测hexo

`hexo -v`

#### 3.项目初始化

`hexo init [myblog]`

`cd [myblog]`

#### 4.安装依赖

`npm i`

#### 5.下载第三方主题

`hexo-theme-Claudia`

`https://github.com/Haojen/hexo-theme-Claudia`

#### **6.配置第三方**

把下载好的解压文件夹放置到 themes 目录下

同时修改 根目录 _config.yml 的配置文件
theme 修改为下载的第三方主题

#### 7.第三方主题配置不表

#### 8.常用命令

启动本地服务器
`hexo s`

清除缓存文件 db.json 和已生成的静态文件 publi
`hexo clean`

生成网站静态文件到默认设置的 public 文件夹
`hexo generate`

上传至github gitee等
`hexo deployd`

一般简写
`hexo clean && hexo g`

`hexo d`
