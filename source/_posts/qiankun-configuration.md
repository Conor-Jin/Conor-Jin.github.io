---
title: qiankun_配置
tags: []
id: '377'
categories:
  - - 前端
date: 2020-12-15 12:27:31
---

一、基座配置 以react为基座，进行配置   1.搭建react搭建

npx create-react-app micro-app-main

  2.安装 qiankun

yarn add qiankun # 或者 npm i qiankun -S

  3.修改 src/index.js，引入qiankun，注册子应用（本示例搭建分别搭建react、vue两个子应用，提前注册）。

import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

import {registerMicroApps, start, initGlobalState} from 'qiankun'   //引入qiankun

// 初始化 state
const initialState = {
  user: {
    name: 'zzzz',
    age: 14
  } // 用户信息
};
const actions = initGlobalState(initialState);
actions.onGlobalStateChange((state, prev) => {
  // state: 变更后的状态; prev 变更前的状态
  // console.log(state, prev);
});
actions.setGlobalState(initialState);
actions.offGlobalStateChange();

registerMicroApps(
  \[
    {
        name:'micro-app-react', //微应用的名称，微应用之间必须确保唯一(微应用中package.json中的name)
        entry:'//localhost:10100', //微应用的entry地址
        container:'#frame',//微应用的容器节点的选择器
        activeRule:'/react'//微应用的激活规则
    },
    {
        name:'micro-app-vue', //微应用的名称，微应用之间必须确保唯一(微应用中package.json中的name)
        entry:'//localhost:10200', //微应用的entry地址
        container:'#frame2',//微应用的容器节点的选择器
        activeRule:'/vue'//微应用的激活规则
    }
  \]
)
start();

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();

  4.修改 src/App.js，根据 index.js中配置的子应用，设置子应用挂载Dom节点

import './App.css';
function App() {
  return (
    <div className="App">
      <p>subapp-container</p>
      <div id='frame' />
      <div id='frame2' />
    </div>
  ); 
}

export default App;

  二、子应用配置，react   1.搭建react子应用

npx create-react-app micro-app-react

  2.由于使用 creact-react-app 搭建项目，webpack配置无法暴露，配置 react-app-rewired

npm install react-app-rewired -D

在 react-app-rewired 安装完成后，我们还需要修改 package.json 的 scripts 选项，修改为由 react-app-rewired 启动应用，就像下面这样

// micro-app-react/package.json

//...
"scripts": {
  "start": "react-app-rewired start",
  "build": "react-app-rewired build",
  "test": "react-app-rewired test",
  "eject": "react-app-rewired eject"
}

  3.根目录下添加 .env 文件

\# micro-app-react/.env
PORT=10100
BROWSER=none

  4.修改 src/public-path.js。webpack 默认的 publicPath 为 "" 空字符串，会基于当前路径来加载资源。我们在主应用中加载微应用时需要重新设置 publicPath，这样才能正确加载微应用的相关资源

if (window.\_\_POWERED\_BY\_QIANKUN\_\_) {
    // eslint-disable-next-line
    \_\_webpack\_public\_path\_\_ = window.\_\_INJECTED\_PUBLIC\_PATH\_BY\_QIANKUN\_\_;
}

  5.修改 src/index.js。导出微应用生命周期钩子函数

mport React from 'react';
import ReactDOM from 'react-dom';
import "./public-path";
import App from "./App.js";


if (window.\_\_POWERED\_BY\_QIANKUN\_\_) {
  // 动态设置 webpack publicPath，防止资源加载出错
  // eslint-disable-next-line no-undef
  \_\_webpack\_public\_path\_\_ = window.\_\_INJECTED\_PUBLIC\_PATH\_BY\_QIANKUN\_\_;
}


/\*\*
 \* 渲染函数
 \* 两种情况：主应用生命周期钩子中运行 / 微应用单独启动时运行
 \*/
function render() {
  ReactDOM.render(<App />, document.getElementById("root"));
}

// 独立运行时，直接挂载应用
if (!window.\_\_POWERED\_BY\_QIANKUN\_\_) {
  render();
}

export async function bootstrap() {
  console.log('react app bootstraped');
}
/\*\*
 \* 应用每次进入都会调用 mount 方法，通常我们在这里触发应用的渲染方法
 \* 通常我们可以在这里做一些全局变量的初始化，比如不会在 unmount 阶段被销毁的应用级别的缓存等。
 \* 
 \*/
export async function mount(props) {
  console.log(props)
  props.onGlobalStateChange((state, prev) => {
    // state: 变更后的状态; prev 变更前的状态
    console.log(state, prev);
  });
  ReactDOM.render(<App />, props.container ? props.container.querySelector('#root') : document.getElementById('root'));
}

/\*\*
 \* 应用每次 切出/卸载 会调用的方法，通常在这里我们会卸载微应用的应用实例/渲染方法
 \*/
export async function unmount(props) {
  console.log('卸载')
  ReactDOM.unmountComponentAtNode(props.container ? props.container.querySelector('#root') : document.getElementById('root'));
}

/\*\*
 \* 可选生命周期钩子，仅使用 loadMicroApp 方式加载微应用时生效，通常在这里我们会卸载微应用的应用实例
 \*/
export async function update(props) {
  console.log('update props', props);
}

  6.根目录创建config-overrides.js 文件。配置 webpack

const path = require("path");

module.exports = {
  webpack: (config) => {
    // 微应用的包名，这里与主应用中注册的微应用名称一致
    config.output.library = \`micro-app-react\`;
    // 将你的 library 暴露为所有的模块定义下都可运行的方式
    config.output.libraryTarget = "umd";
    // 按需加载相关，设置为 webpackJsonp\_VueMicroApp 即可
    config.output.jsonpFunction = \`webpackJsonp\_micro-app-react\`;

    config.resolve.alias = {
      ...config.resolve.alias,
      "@": path.resolve(\_\_dirname, "src"),
    };
    return config;
  },

  devServer: function (configFunction) {
    return function (proxy, allowedHost) {
      const config = configFunction(proxy, allowedHost);
      // 关闭主机检查，使微应用可以被 fetch
      config.disableHostCheck = true;
      // 配置跨域请求头，解决开发环境的跨域问题
      config.headers = {
        "Access-Control-Allow-Origin": "\*",
      };
      // 配置 history 模式
      config.historyApiFallback = true;

      return config;
    };
  },
};

  三、子应用配置，vue   1.vue-cli 先创建一个 Vue 的项目

vue create micro-app-vue

  2.创建 src/public-path.js 文件。webpack 默认的 publicPath 为 "" 空字符串，会基于当前路径来加载资源。我们在主应用中加载微应用时需要重新设置 publicPath，这样才能正确加载微应用的相关资源

if (window.\_\_POWERED\_BY\_QIANKUN\_\_) {
    // 动态设置 webpack publicPath，防止资源加载出错
    // eslint-disable-next-line no-undef
    \_\_webpack\_public\_path\_\_ = window.\_\_INJECTED\_PUBLIC\_PATH\_BY\_QIANKUN\_\_;
 }

  3.修改 src/main.js 文件。 导出生命周期

import { createApp } from 'vue'
import App from './App.vue'

createApp(App).mount('#app')

/\*\*
 \* bootstrap 只会在微应用初始化的时候调用一次，下次微应用重新进入时会直接调用 mount 钩子，不会再重复触发 bootstrap。
 \* 通常我们可以在这里做一些全局变量的初始化，比如不会在 unmount 阶段被销毁的应用级别的缓存等。
 \*/
export async function bootstrap() {
  console.log("VueMicroApp bootstraped");
}

/\*\*
 \* 应用每次进入都会调用 mount 方法，通常我们在这里触发应用的渲染方法
 \*/
export async function mount(props) {
  console.log("VueMicroApp mount", props);
//   render(props);
}

/\*\*
 \* 应用每次 切出/卸载 会调用的方法，通常在这里我们会卸载微应用的应用实例
 \*/
export async function unmount() {
  console.log("VueMicroApp unmount");
//   instance.$destroy();
//   instance = null;
//   router = null;
}

  4. 根目录 创建 vue.config.js 文件。webpack，使 main.js 导出的生命周期钩子函数可以被 qiankun 识别

const path = require("path");

module.exports = {
  devServer: {
    // 监听端口
    port: 10200,
    // 关闭主机检查，使微应用可以被 fetch
    disableHostCheck: true,
    // 配置跨域请求头，解决开发环境的跨域问题
    headers: {
      "Access-Control-Allow-Origin": "\*",
    },
  },
  configureWebpack: {
    resolve: {
      alias: {
        "@": path.resolve(\_\_dirname, "src"),
      },
    },
    output: {
      // 微应用的包名，这里与主应用中注册的微应用名称一致
      library: "VueMicroApp",
      // 将你的 library 暴露为所有的模块定义下都可运行的方式
      libraryTarget: "umd",
      // 按需加载相关，设置为 webpackJsonp\_VueMicroApp 即可
      jsonpFunction: \`webpackJsonp\_VueMicroApp\`,
    },
  },
};

  四、分别启动主应用，以及两个子应用，通过主应用的路由切换 即可看到对应配置子应用