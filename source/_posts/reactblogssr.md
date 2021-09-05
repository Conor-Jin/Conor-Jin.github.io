---
title: 从头搭建博客系统之react服务端渲染
tags: []
id: '262'
categories:
  - - react
date: 2019-10-17 08:09:14
---

## **一、`Next.js` 安装**

```
npx create-next-app
```

```
npm install --save next react react-dom
```

 

## **二、**Ant Design安装

npm i antd --save

npm i babel-plugin-import --save

npm i babel-preset-react-app --save

package.json 添加配置信息

  "babel": {
    "presets": \[
      "react-app"
    \],
    "plugins": \[
      \[
        "import",
        {
          "libraryName": "antd",
          "style": "css"
        }
      \]
    \]
  }

个人喜欢按照需要引用，具体配置参考 [http://jindk.wang/blog/index.php/2019/10/16/reactinitmatters/](http://jindk.wang/blog/index.php/2019/10/16/reactinitmatters/)  

## **三、**`Next`支持CSS文件

如果要全局引入Ant Design可以进行第三步的配置

npm i @zeit/next-css

`blog`根目录下，新建一个`next.config.js`文件。这个就是`Next.js`的总配置文件

const withCss = require('@zeit/next-css')

if(typeof require !== 'undefined'){
    require.extensions\['.css'\]=file=>{}
}

module.exports = withCss({})

 

## **四、axios**

 npm i axios --save

 

## **五、**安装marked和highlight

npm i marked --save

 npm i highlight --save

    基础架子搭建完毕