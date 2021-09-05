---
title: react初始化以及主要使用包说明
tags: []
id: '202'
categories:
  - - react
  - - 前端
date: 2019-09-27 21:42:43
---

一、 脚手架安装 npx 安装

npx create-react-app my-app
cd my-app
npm start

注：

npx create-react-app my-app

等同于

npm install -g create-react-app
create-react-app my-app

  二、styled-components安装

npm install --save styled-components

注： styled-components 是对css样式进行模块化封装的包，所以文件应该是一个 .js，方便示例使用单个文件使用如下

import React, { Component,Fragment} from 'react';
//引入styled-components
import styled from 'styled-components'

//修改了div的样式
const Title = styled.div\`
  font-size:1.5rem;
  color:red
\`
// 修改了button的样式
const Button = styled.button\`
    border:none;
    background-color:blue
\`

class App extends Component {
  render() {
    return (
      <Fragment>
      <Title>大红牛</Title>
      <Button>枸杞</Button>
    </Fragment>
    )
  }
}
export default App;

    三、react-transition-group实现动画效果

npm install react-transition-group --save

注： react-transition-group较为方便的实现动画效果，以styled-components包示例修改如下，本意是实现隐藏和展现，但是并未写相关逻辑

import React, { Component,Fragment} from 'react';
//引入styled-components
import styled from 'styled-components'
// 在 react-transition-group 引入 CSSTransition
import { CSSTransition } from 'react-transition-group';

//修改了div的样式
const Title = styled.div\`
  font-size:1.5rem;
  color:red
    // enter是入场前的刹那
    &.slide-enter{
        transition: all .2s ease-out;
    }
    // 出场前的一刹那
    &.slide-exit{
        width     : 160px
        transition: all .2s ease-out;
    }
    // enter-active指入场后到入场结束的过程
    &.slide-enter-active{
        transition: all .2s ease-out;
    }
    &.slide-exit-active{
        width: 160px
    }
\`
// 修改了button的样式
const Button = styled.button\`
    border:none;
    background-color:blue
\`

class App extends Component {
  render() {
    return (
        <Fragment>
            <CSSTransition
                in         = {focused}
                timeout    = {200}
                classNames = "slide"
            >
                <Title>大红牛</Title>
                <Button>枸杞</Button>
            </Fragment>
        </Fragment>
    )
  }
}
export default App;

    四、redux 安装 1.安装redux相关库

npm  install redux --save

2.安装react-redux库

npm install react-redux --save

  注： redux 是与react完全无关的数据管理库，react-redux是redux专门为react封装的库。 更多的解释说明看阮一峰老师的博客即可，[http://www.ruanyifeng.com/blog/2016/09/redux\_tutorial\_part\_three\_react-redux.html](http://www.ruanyifeng.com/blog/2016/09/redux_tutorial_part_three_react-redux.html)     五、chrome 浏览器Redux DevTools插件的设置 1.详细信息在[GitHub](https://github.com/zalmoxisus/redux-devtools-extension) 2.store 中的 index 文件配置如下

const composeEnhancers = window.\_\_REDUX\_DEVTOOLS\_EXTENSION\_COMPOSE\_\_  compose;

const store = createStore(reducer, composeEnhancers());

  六、immutable-js安装

npm install immutable

注： immutable 格式数据是一旦创建，就不能再被更改的数据，主要是为了解决js的引用赋值。优点降低数据复杂度、节省内存不表，主要是刚刚使用注意他与原生JS数据相似的地方，例如，map、list等等  

七、使用redux-immutable统一数据格式

npm install redux-immutable --save

注： 这个包主要是配合 redux中的state 转变为 immutable 使用  

八、redux-thunk安装

npm install --save redux-thunk

注： Redux store 仅支持同步数据流。使用 thunk 等中间件可以帮助在 Redux 应用中实现异步性。可以将 thunk 看做 store 的 dispatch() 方法的封装器。更直白的将就是对 store.dispatch()的增强。示例

直接将thunk中间件引入，放在applyMiddleware方法之中，传入createStore方法，就完成了store.dispatch()的功能增强
// thunk 的引用
import thunk from 'redux-thunk';
import reducer from './reducer';

// chrome 拓展所用
const composeEnhancers = window.\_\_REDUX\_DEVTOOLS\_EXTENSION\_COMPOSE\_\_  compose;

const store = createStore(reducer, composeEnhancers(
    applyMiddleware(thunk)
));

  九、axios安装

npm isntall axios --save

  十、react-router-dom 安装

npm install --save react-router-dom

注： 用React单页面应用，要想实现页面间的跳转，常用的有两个包可以实现这个需求，那就是react-router和react-router-dom。 react-router-dom: 基于react-router，加入了在浏览器运行环境下的一些功能。示例

import React from 'react';
import { Provider } from 'react-redux';
import { BrowserRouter, Route } from 'react-router-dom';
import { Globalstyle } from './style'
import Header from './common/header'
import Home from './page/home/index'
import Detail from './page/detail/loadable'
import Login from './page/login/index'
import Write from './page/write/index'
import store from './store';

function App() {
  return (
    <Provider store={store} className="App">
      <BrowserRouter>
        <Header/>
        <Route path='/' exact component={Home}></Route>
        <Route path='/login' exact component={Login}></Route>
        <Route path='/write' exact component={Write}></Route>
        <Route path='/detail/:id' exact component={Detail}></Route>
      </BrowserRouter>
      <Globalstyle/>
    </Provider>
  );
}

export default App;

      十一、react-loadable安装

npm install react-loadable --save-dev

注： react开发单页面应用时，打包后的js文件特别巨大，首屏加载会特别缓慢。react-loadable思路是将代码分割。示例 公共通用组件

import React from 'react';
import Loadable from 'react-loadable';

//通用的过场组件
const loadingComponent =()=>{
    return (
        <div>loading</div>
    ) 
}

//过场组件默认采用通用的，若传入了loading，则采用传入的过场组件
export default (loader,loading = loadingComponent)=>{
    return Loadable({
        loader,
        loading
    });
}

home组件使用

import React, { Fragment } from 'react'
import { BrowserRouter, Route } from 'react-router-dom'
import loadable from '../util/loadable'

const Home = loadable(()=>import('@pages/home'))

const Routes = () => (
    <BrowserRouter>
        <Route path="/home" component={Home}/>
    </BrowserRouter>
);

export default Routes