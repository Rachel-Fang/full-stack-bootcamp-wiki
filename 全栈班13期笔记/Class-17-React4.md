# Class-17 React-4
(本节代码较多，可跳过部分代码阅读)
## 主要知识点
  - [1.课前答疑](#1课前答疑)
  - [2.使用Webpack DevServer进行开发](#2使用webpack-devserver进行开发)
    - [2.1 安装配置Webpack DevServer](#21-安装配置webpack-devserver)
    - [2.2 安装配置htmlplugin](#22-安装配置htmlplugin)
      - [2.2.1 npm run build 不能用了](#221-npm-run-build-不能用了)
      - [2.2.2 将main.css交给webpack统一管理](#222-将maincss交给webpack统一管理)
      - [2.2.3 安装配置htmlplugin](#223-安装配置htmlplugin)
      - [2.2.4 添加index template](#224-添加index-template)
  - [3.虚拟DOM](#3虚拟dom)
    - [3.1 从一个warning谈起](#31-从一个warning谈起)
    - [3.2 React的核心理念：虚拟DOM](#32-react的核心理念虚拟dom)
    - [3.3 React中的key问题](#33-react中的key问题)
    - [3.4 课间讨论答疑](#34-课间讨论答疑)
  - [4.State](#4state)
    - [4.1 styled components中传props](#41-styled-components中传props)
    - [4.2 通过点击button，改变props的值](#42-通过点击button改变props的值)
    - [4.3 引入state，实现点击button来改变页面渲染](#43-引入state实现点击button来改变页面渲染)
      - [4.3.1 为实现页面动态渲染，两个重要的概念](#431-为实现页面动态渲染两个重要的概念)
      - [4.3.2 引入class component](#432-引入class-component)
      - [4.3.3 在其他组件中调用class component方法](#433-在其他组件中调用class-component方法)
      - [4.3.4 bind this](#434-bind-this)


# 课堂笔记

## 1.课前答疑
- Q: 龙哥你上次说真实工作中几乎不会用create-react-app，都是自己配？但也不会让我们这些junior配就是了对吧，反正进react组了一般是让你做xx组件？
  - A: 工作中几乎没有公司会用create-react-app，create-react-app也官方声明说仅是用来学习的工具；但是大家也不要对于webpack产生恐慌心理，只要死记硬背就行，因为公司也不会要junior去配置webpack
  - A: 作为一个lead，会希望由webpack的报错，junior知道怎么会去解决；因此junior对webpack不一定要精通，但是一定要会
  - 招人中，他可能不会关心你现在会不会用webpack，但是他希望你能在 公司需要用的时候，可以学会并用起来
- Q: 实际工作中一个人会做webpack就可以了吧
  - A: 实际工作中会做的当然越多越好，公司需要的是一个很强学习能力，解决问题能力的人
   
## 2.使用Webpack DevServer进行开发
### 2.1 安装配置Webpack DevServer
首先来解决一个痛点，create-react-app每次更新代码都会自己帮你刷新，我们每次都要build，使用Webpack DevServer来解决这个问题
- 1. ```npx webpack serve```
- 2. 修改 main.js路径
- 3. 更新 ```package.json```

下面来实现上面的步骤
  - ```npx webpack serve```
    - npx是npm的一种执行方式
  - dev server每次打包，都会把打包的结果扔向 http://localhost:8080/webpack-dev-server，
    - 因此我们也需要更新index.html中的dist/main.js，重新定位编译好的js code指向才行
  - 修改main.js路径：```<script src="main.js"></script>```
    - dist/main.js 是在 npm run build（webpack）的情况下产生的
    - 如果用webpack server，那就是取了 dev server，dev server会自动编译与build变更的文件，并把文件放在某个地方
  - 官方文档里一般会把用户遇到的最多的问题置顶，放到醒目的位置，因此通过官方文档我们可以看到  
   ```If you're having trouble, navigating to the /webpack-dev-server route will show where files are served. For example, http://localhost:9000/webpack-dev-server.```
  - 在思维定式的情况下，以为```src = webpack-dev-server/main.js```，结果报错```Unexpected token '<'```
  - 如何解决，通过以往的经验，我们能得出webpack-dev-server/main.js不是一个合法的js，但是回到http://localhost:9000/webpack-dev-server 下能看到main.js应该是一个合法编译的js文件，同时发现路径其实为http://localhost:9000/main.js ，然后说明src后面不需要跟webpack-dev-server
    - 前端技术上千种，与其说找一个什么都会的人，不如去找一个能像上面这样解决问题的
  > 不要老想着答案是什么，更应该想怎么去找到答案，找答案的过程是什么
  - 最后写入```package.json```
    ```
     "scripts": {
        "start": "webpack server",
        "build": "webpack"
    },
    ```
    这样我们就可以通过```npm run stat```来直接开启dev-server 
- 这里dev server，类似于live server，但是多出了编译和打包的功能

### 2.2 安装配置htmlplugin
#### 2.2.1 npm run build 不能用了
因为修改了main.js的路径，```npm run build```编译完成的```dist/main.js```无法被引用，而失去了作用
#### 2.2.2 将main.css交给webpack统一管理
修改```index.js```，```index.html```中关于main.css的部分，交给webpack统一管理，以实现更好的maintainable
```js
//index.js
import React from 'react';
import ReactDOM from 'react-dom';
import App from './App';
import './main.css';


ReactDOM.render(
    <App />,
    document.querySelector('#app')
);

```
```html
//index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Demo</title>
  </head>

  <body>
    <div id="app"></div>
  </body>

</html>

```
#### 2.2.3 安装配置htmlplugin
我们需要一个htmlplugin，帮你自动生成一个bundle html
- ```webpack.config.js```中引入
  ```js
  //webpack.config.js
  const HtmlWebpackPlugin = require('html-webpack-plugin');

  module.exports = {
        //需要打包什么样的东西
        mode: 'development',
        entry: './index.js',
        module: {
            rules: [
            {
                test: /\.js$/,
                use: {
                loader: 'babel-loader',
                options: {
                    presets: ['@babel/preset-react']
                }
                }
            },{
                test: /\.css$/i,
                use: ["style-loader", "css-loader"],
                },
            ]
        },
        plugins: [
            new HtmlWebpackPlugin(),
        ],
    
    }
  ```
- ```npm i -D html-webpack-plugin```
  
#### 2.2.4 添加index template
此时index.html仍然不工作，这是因为index.js里我们要求render App，可是我们index.html里没有id为App的element。因此我们需要使用`template`来解决这个问题，告诉webpack我们在generate html的时候template是什么
```js
//webpack.config.js
const HtmlWebpackPlugin = require('html-webpack-plugin');

module.exports = {
    //需要打包什么样的东西
    mode: 'development',
    entry: './index.js',
    module: {
        rules: [
          {
            test: /\.js$/,
            use: {
              loader: 'babel-loader',
              options: {
                presets: ['@babel/preset-react']
              }
            }
          },{
              test: /\.css$/i,
              use: ["style-loader", "css-loader"],
            },
        ]
       },
    plugins: [
      new HtmlWebpackPlugin({
        template: 'index.html',
      }),
    ],
  
}
```
```html
//index.html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta http-equiv="X-UA-Compatible" content="IE=edge" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Demo</title>
  </head>

  <body>
    <div id="app"></div>
  </body>

</html>
``` 
以上我们实现dev server，步骤为
- package配置中加入webpack server
- webpack.config中加入htmlplugin

## 3.虚拟DOM
### 3.1 从一个warning谈起
"Warning: Each child in a list should have a unique "key" prop."
- 在Header.js中，加入 key = {navbarItem.key}
```js
//Header.js
import React from 'react';
import styled from 'styled-components';
import Flex from '../../components/Flex';
import './components/NavbarItem/NavbarItem.css';


const Highlight = styled.span`
    color:#377e9a;
`;

const Logo = styled.div`
    font-size: 1.5rem;
    font-weight:500;
`;

const Nav = styled(Flex)`
    padding: 15px 0;
    align-items: center;
`;

const Left = styled.div`
    flex: 1;
`;

const Right = styled.div`
`;


const Header = () => {
    const page = 'HOME';

    const navbarItems = [
        { key: 'HOME', value: 'Home' },
        { key: 'RESUME', value: 'Resume' },
        { key: 'SERVICES', value: 'Services' },
        { key: 'BLOG', value: 'Blog' },
        { key: 'CONTACT', value: 'Contact' }
    ]


    return (
    <Nav>
        <Left>
            <Logo>
                <Highlight>Tifa</Highlight>
                Lockhart
            </Logo>
        </Left>
        <Right>
            <Flex>
                {navbarItems.map((navbarItem) => (
            <a
              key = {navbarItem.key}
              className = {`navbarItem ${page === navbarItem.key && 'navbarItem--active'}`} href = {navbarItem.value} >
            {navbarItem.value}
            </a>
            ))}
            </Flex>
        </Right>
</Nav>
);
}

export default Header;
``` 
### 3.2 React的核心理念：虚拟DOM
核心概念：Virtual DOM(虚拟DOM)  
我们写的Jsx会被渲染成html，然后挂载在浏览器DOM上    
但是当项目足够高级的时候，会遇到一个效能问题   
历史由来：
HTML最早被开发出来是为了什么目的：是为了美国军方更方便快捷的分享文档   
所以才叫Markup Language, 非常类似于文本文档   
这时候看，一个（静态的）文档，进化成（动态的）Application，是一个非常巨大的改变，例如从wikipedia进化成一个比特币在线交易网站   
这种冲突会造成性能问题：
- 最初的静态页面，并不需要关心页面的动态更新效率，
- 到了Application，这个页面每一帧都在改变，HTML能不能实现这个功能？
  
答案是不能的  
前端性能问题的历史由来：
- 无论HTML如何更新，但是DOM的机制，使它无法完成复杂的动态的渲染的工作
- 所以最初是没有前端程序员这个职位的，因为前端有性能问题  
- AngularJS的问世，实现了Declarative和Component两个概念，才衍生出前端程序员  
- 但是AngularJS在三年时间内，迅速衰败，原因是浏览器性能问题  
- 在这里，无论是Angular还是React，目的都是把写成的类HTML代码，渲染到浏览器上

虚拟DOM概念的提出：
- React的出现，提出了虚拟DOM的概念  
- 从JSX到浏览器DOM的过程中，AngularJS有任何页面改动，就会刷新整个页面，从而造成性能问题；  
- 而React在这个过程中，插入了虚拟DOM：有任何页面改动，React会给你compile一个虚拟的DOM，在跟上一次进行比较后，会拿到差异，只更新差异部分  
这个比较的过程叫reconciliation：https://zh-hans.reactjs.org/docs/reconciliation.html
- Q:在react 中有虚拟DOM    如果用 js 改变html DOM  会不会导致混乱
  - A: 只有直接在入口html里直接引入新的js来改变真实dom，不然通过id=app走的都属于通过react走的虚拟dom部分
### 3.3 React中的key问题
```html
<div>
    <p>Hello World</p>
    <div>
        <button>CLICK ME</button>
    </div>
</div>
```
假如最近一次更新，CLICK ME变成了LOADING
```html
<div>
    <p>Hello World</p>
    <div>
        <button>LOADING</button>
    </div>
</div>
```
那这变化非常微小，React会很容易发现  
如果是点击button，让p消失了，变成
```html
<div>
    <div>
        <button>CLICK ME</button>
    </div>
    <p>LOADING</p>
</div>
```
也不会导致混乱  
但是React里会有一个极端情况
```js
 <Flex>
        {navbarItems.map((navbarItem) => (
    <a
    key = {navbarItem.key}
    className = {`navbarItem ${page === navbarItem.key && 'navbarItem--active'}`} href = {navbarItem.value} >
    {navbarItem.value}
    </a>
    ))}
 </Flex>
```
我们在用一个array生成另外一个array的时候，react根本不知道这是怎么生成的，也无法完全分析与控制这个dom，这时候就会引起混乱  
怎么解决这个问题  
在rending一个list的时候，每一个child都必须有一个unique的prop，让react辨别出谁是谁
- Q:所有的html elements都要有key吗
  - A:只有这种list items，通过map这种动态的方式，需要有key
- Q:没有key值怎么办
  - A:自己制造key
  - 如果从后端取数据，那一定有key，数据库里面是有primary key的
  - 如果实在没办法，那就用index吧，但这是非常非常大的性能隐患
- Q:react 可不可以完全避免使用js 操作dom
  - A:必须完全避免使用js操作dom
  - 因为react中所有的html都是通过jsx写出来的，而通过其它方式写入的html则无法享受react 虚拟dom带来的性能提升
> 对我们学生的要求： 1.没有key值时，也不能使用index 2.react以外不能用js操作dom
- Q: vue和react工作原理一样吗？
  - A: 前端三架马车:Angular, React，Vue，工作原理都是非常相似的

在面试的过程中，谈到React的好处，Declarative和Component是两个必须要说的，但是当谈及跟AngularJS和Vue的对比，虚拟Dom就是一个绕不开的话题

### 3.4 课间讨论答疑
- Q:那上上次课说到的angular很全面的framework，而react小而精的，是指的angularJS？？
  - A:angular跟angularJS师出一门，只不过angular是angularJS的重写
  - Q:刚才说没有虚拟dom直接搞真实dom的是angularjs？
    - A:对
- Q:老师之前学习 看过哪些书和资料？
  - A: 不太看书，基本通过Google和stackoverflow学习
  - 然后就是各种getting start，比如react getting start，webpack getting start
  - 以及各大conference
  - 不要靠买书来学习
  - Q: 但是这些知识都很碎片化，不够系统，很难理解整理
    - A: 这就是我们在澳洲需要的能力，将碎片化的知识学习并整理成系统
  - Q: 老师是怎么整理碎片化知识的
    - A: 本节课2.1的流程就是整理碎片化的知识
    - 另外比较重要的是："复盘"，"Working Dairy"(推荐每一个junior能写就写)，"写代码"（当你碎片多的时候自然就整理出来了）
> 犀牛书是业界神器
- Q: 龙哥你觉得工作中技术牛真的就很吃香吗?
  - A: 工作中技术牛分为很多种，但澳洲不看重技术牛；技术不牛，吃不吃香?在澳洲，技术不牛是没有问题的，技术不牛就熬资历吧
  - 每天8小时，你写了多少小时代码？Junior中，写10小时代码是比较常见的，坐火车时候也写
- Q:写代码八小时google七个半小时
  - A: 可以的，只要让自己在写代码的状态中就行
- Q:龙哥code review一般你都会关注什么方面呀
  - A：RMR
  - RMR是比较high level思想层面的东西，是否RMR就靠SOLID来判定

## 4.State
上节课我们把navbar item从styled components换成了css module，实现动态判断渲染    
这节课我们用style component来实现
### 4.1 styled components中传props
- 将navbarItem写回Header，并更改item样式从a变为button
但凡是component他就有props这个概念，因此我们可以给navbar item传一个props  
styled component里我们通过在component里注入一段js（```${}```）代码实现
```js
opacity: ${(props) => props.active ? '1':'0.6'};

${(props) => {
        console.log(props);
    }}

```
```js
//Header.js
import React from 'react';
import styled from 'styled-components';
import Flex from '../../components/Flex';
import './components/NavbarItem/NavbarItem.css';


const Highlight = styled.span`
    color:#377e9a;
`;

const Logo = styled.div`
    font-size: 1.5rem;
    font-weight:500;
`;

const Nav = styled(Flex)`
    padding: 15px 0;
    align-items: center;
`;

const NavbarItem = styled.button`
    
    border: 0;
    background: transparent;
    cursor: pointer;
    padding: 16px;
    text-decoration: none;
    color: #49515d;
    font-size: 15px;
    opacity: ${({active}) => active ? '1':'0.6'};
    display: block;
    transition: opacity 0.3s ease-in-out;

    ${(props) => {
        console.log(props);
    }}

    /* SCSS 规范 */
    &::after {
        content: "";  
        width: ${({active}) => active ? '24px' : '0'};
        border-bottom: 3px solid #377e9a;
        margin: auto;
        margin-top: 4px;
        display: block;
        transition: width 0.3s ease-in-out;
    }

    &:hover{
        opacity: 1;
    }

    &:hover::after {
        width: 24px;
    }
      
    &:last-of-type {
        padding-right: 0;
    }
`;

const Left = styled.div`
    flex: 1;
`;

const Right = styled.div`
`;


const Header = ({
    page,
}) => {

    const navbarItems = [
        { key: 'HOME', value: 'Home' },
        { key: 'RESUME', value: 'Resume' },
        { key: 'SERVICES', value: 'Services' },
        { key: 'BLOG', value: 'Blog' },
        { key: 'CONTACT', value: 'Contact' }
    ]


    return (
    <Nav>
        <Left>
            <Logo>
                <Highlight>Tifa</Highlight>
                Lockhart
            </Logo>
        </Left>
        <Right>
            <Flex>
                {navbarItems.map((navbarItem) => (
            <NavbarItem 
              key = {navbarItem.key}
              active = {page === navbarItem.key}
              href = {navbarItem.value} >
            {navbarItem.value}
            </NavbarItem>
            ))}
            </Flex>
        </Right>
</Nav>
);
}

export default Header;
``` 

### 4.2 通过点击button，改变props的值
将App.js中的page改为variable, 通过相应的button，来改变page的值，即实现了页面和导航  
如何 onclick
- jsx也可以像html一样用，但是要注意：
  - 1. camelCase
  - 2. pass javascript function

因此，首先在`App.js`中：
```js
//App.js
import React from 'react';
import Header from './app/Header';
import Page from './app/Page';
import Footer from './app/Footer';

const App = () => {
    let page = 'HOME';

    return(
    <div className="main">
        <div className="container">
        <Header arg = {page} />
        <Page arg = {page} />
        <Footer />
        </div>
    </div>
    );
}

export default App;
```
然后我们要更改Header.js中的html部分：
```js
//Header.js
import React from 'react';
import styled from 'styled-components';
import Flex from '../../components/Flex';
import './components/NavbarItem/NavbarItem.css';


const Highlight = styled.span`
    color:#377e9a;
`;

const Logo = styled.div`
    font-size: 1.5rem;
    font-weight:500;
`;

const Nav = styled(Flex)`
    padding: 15px 0;
    align-items: center;
`;

const NavbarItem = styled.button`
    
    border: 0;
    background: transparent;
    cursor: pointer;
    padding: 16px;
    text-decoration: none;
    color: #49515d;
    font-size: 15px;
    opacity: ${(props) => props.active ? '1':'0.6'};
    display: block;
    transition: opacity 0.3s ease-in-out;

    ${(props) => {
        console.log(props);
    }}

    /* SCSS 规范 */
    &::after {
        content: "";  
        width: ${(props) => props.active ? '24px' : '0'};
        border-bottom: 3px solid #377e9a;
        margin: auto;
        margin-top: 4px;
        display: block;
        transition: width 0.3s ease-in-out;
    }

    &:hover{
        opacity: 1;
    }

    &:hover::after {
        width: 24px;
    }
      
    &:last-of-type {
        padding-right: 0;
    }
`;

const Left = styled.div`
    flex: 1;
`;

const Right = styled.div`
`;


const Header = ({
    page,
}) => {

    const navbarItems = [
        { key: 'HOME', value: 'Home' },
        { key: 'RESUME', value: 'Resume' },
        { key: 'SERVICES', value: 'Services' },
        { key: 'BLOG', value: 'Blog' },
        { key: 'CONTACT', value: 'Contact' }
    ]


    return (
    <Nav>
        <Left>
            <Logo>
                <Highlight>Tifa</Highlight>
                Lockhart
            </Logo>
        </Left>
        <Right>
            <Flex>
                {navbarItems.map((navbarItem) => (
            <NavbarItem 
              onClick = {() => {
                  console.log(navbarItem.key);
                  page = navbarItem.key;
                  console.log(page);
              }}
              key = {navbarItem.key}
              active = {page === navbarItem.key}
              href = {navbarItem.value} >
            {navbarItem.value}
            </NavbarItem>
            ))}
            </Flex>
        </Right>
</Nav>
);
}

export default Header;
```
这个时候我们发现，虽然console输出了正确的值，但是页面仍然没有改变。

### 4.3 引入state，实现点击button来改变页面渲染
#### 4.3.1 为实现页面动态渲染，两个重要的概念
这里需要引入两个关键概念：
- virtual DOM： 所有相应的UI 更改都需要通过React，这样React 才能去做vDom的reconciliation
- state
  - React需要知道当前的组件状态是什么，才能根据状态做相应的组件渲染
  - React需要知道状态发生了改变，才能去触发协调（reconciliation）
  - 
我们以上代码
```js
        <NavbarItem 
              onClick = {() => {
                  console.log(navbarItem.key);
                  page = navbarItem.key;
                  console.log(page);
              }}
              key = {navbarItem.key}
              active = {page === navbarItem.key}
              href = {navbarItem.value} >
            {navbarItem.value}
        </NavbarItem>
```
仅仅是做了一个javaScript assignment，没有React的参与

#### 4.3.2 引入class component
我们写的App.js仅仅是一个Function Component，即component本身是通过声明一个function来创建的，
但是function component无法持久化，这时候我们需要一个class component

当我在代码中需要一个地方去持久化保存可更改的值的时候？我需要的东西是什么
- OOP：class，object，instance

回顾一下function component, 每一个function component都是要返回一段jsx片段的；在class component中，我们需要在render中return一段jsx片段
```js
//App.js
import React from 'react';
import Header from './app/Header';
import Page from './app/Page';
import Footer from './app/Footer';

// Class Component
class App extends React.Component {
    render() {
        let page = 'BLOG';

        return(
            <div className="main">
                <div className="container">
                <Header arg = {page} />
                <Page arg = {page} />
                <Footer />
                </div>
            </div>
        );
    }
}
```
我们使用class component是为了持久化一个值，首先我们要先写一个contructor, 并传入props（固定写法），然后我们需要state    
contructor中我们通过this，实现持久化存储；我们初始化state这个object时，包含了某些变量;然后在render中，通过解构state来获得变量，并进行渲染  

当我们要更新state的时候，不能
```js
this.state.page = 'HOME';
```
因为这是一个标准的JS赋值，没有React的参与，React就不知道需要去协调，去更新渲染  
所以我们需要`set state`  
`set state`会把this.state更新到最新值，并执行协调，更新内容
```js
//App.js
import React from 'react';
import Header from './app/Header';
import Page from './app/Page';
import Footer from './app/Footer';

// Class Component
class App extends React.Component {

    constructor(props){
        super(props);

        this.state = {
            page: 'HOME',
        };
    }
    render() {
        const {page} = this.state;

        return(
            <div className="main">
                <div className="container">
                <button
                    onClick = {() => this.setState({page: 'SERVICES'})}
                >
                    SET PAGE STATE TO SERVICES
                </button>
                <Header arg = {page} />
                <Page arg = {page} />
                <Footer />
                </div>
            </div>
        );
    }
}

export default App;
```
优化以上代码：
```js
//App.js
import React from 'react';
import Header from './app/Header';
import Page from './app/Page';
import Footer from './app/Footer';

// Class Component
class App extends React.Component {

    constructor(props){
        super(props);

        this.state = {
            page: 'HOME',
        };
    }

    handlePageChange(newPage){
        this.setState({
            page:newPage,
        });
    }
    render() {
        const {page} = this.state;

        return(
            <div className="main">
                <div className="container">
                <button
                    onClick = {() => this.handlePageChange('SERVICES')}
                >
                    SET PAGE STATE TO SERVICES
                </button>
                <Header arg = {page} />
                <Page arg = {page} />
                <Footer />
                </div>
            </div>
        );
    }
}

export default App;
```
- Q: 老师这里class的render是渲染该组件，然后ReactDOM的render渲染的是整个页面是不。
  - A: 可以这么理解

#### 4.3.3 在其他组件中调用class component方法
然后我们在Header.js这个function component中是不能用setState来改变状态的，  
首先记得"函数是普通老百姓"，即我们可以定义一个函数，然后调用handlePageChange，将它传给Header
```js
//App.js
import React from 'react';
import Header from './app/Header';
import Page from './app/Page';
import Footer from './app/Footer';

// Class Component
class App extends React.Component {

    constructor(props){
        super(props);

        this.state = {
            page: 'HOME',
        };
    }

    handlePageChange(newPage){
        this.setState({
            page:newPage,
        });
    }
    render() {
        const {page} = this.state;

        return(
            <div className="main">
                <div className="container">
                <button
                    onClick = {() => this.handlePageChange('SERVICES')}
                >
                    SET PAGE STATE TO SERVICES
                </button>
                <Header 
                    onPageChange = {this.handlePageChange}
                    page = {page}
                />
                <Page arg = {page} />
                <Footer />
                </div>
            </div>
        );
    }
}

export default App;
```
```js
//Header.js
import React from 'react';
import styled from 'styled-components';
import Flex from '../../components/Flex';
import './components/NavbarItem/NavbarItem.css';


const Highlight = styled.span`
    color:#377e9a;
`;

const Logo = styled.div`
    font-size: 1.5rem;
    font-weight:500;
`;

const Nav = styled(Flex)`
    padding: 15px 0;
    align-items: center;
`;

const NavbarItem = styled.button`
    
    border: 0;
    background: transparent;
    cursor: pointer;
    padding: 16px;
    text-decoration: none;
    color: #49515d;
    font-size: 15px;
    opacity: ${(props) => props.active ? '1':'0.6'};
    display: block;
    transition: opacity 0.3s ease-in-out;

    ${(props) => {
        console.log(props);
    }}

    /* SCSS 规范 */
    &::after {
        content: "";  
        width: ${(props) => props.active ? '24px' : '0'};
        border-bottom: 3px solid #377e9a;
        margin: auto;
        margin-top: 4px;
        display: block;
        transition: width 0.3s ease-in-out;
    }

    &:hover{
        opacity: 1;
    }

    &:hover::after {
        width: 24px;
    }
      
    &:last-of-type {
        padding-right: 0;
    }
`;

const Left = styled.div`
    flex: 1;
`;

const Right = styled.div`
`;


const Header = ({
    onPageChange,
    page,
}) => {

    const navbarItems = [
        { key: 'HOME', value: 'Home' },
        { key: 'RESUME', value: 'Resume' },
        { key: 'SERVICES', value: 'Services' },
        { key: 'BLOG', value: 'Blog' },
        { key: 'CONTACT', value: 'Contact' }
    ]


    return (
    <Nav>
        <Left>
            <Logo>
                <Highlight>Tifa</Highlight>
                Lockhart
            </Logo>
        </Left>
        <Right>
            <Flex>
                {navbarItems.map((navbarItem) => (
            <NavbarItem 
              onClick = {() => {
                  onPageChange(navbarItem.key);
              }}
              key = {navbarItem.key}
              active = {page === navbarItem.key}
              href = {navbarItem.value} >
            {navbarItem.value}
            </NavbarItem>
            ))}
            </Flex>
        </Right>
</Nav>
);
}

export default Header;
```
#### 4.3.4 bind this
这时候我们遇到了一个典型的问题：  
```Uncaught TypeError: Cannot read property 'setState' of undefined```  
这里this为什么是undefined，因为我们在Header调用onPageChange的时候，Caller是不存在的，这时候this是没有指向的，所以我们需要在App.js中，在constructor里对this进行bind，这样无论caller是谁，都指向app
```js
this.handlePageChange = this.handlePageChange.bind(this);
```
由此App.js与Header.js实现了完整的state的功能
```js
//App.js
import React from 'react';
import Header from './app/Header';
import Page from './app/Page';
import Footer from './app/Footer';

// Class Component
class App extends React.Component {

    constructor(props){
        super(props);

        this.state = {
            page: 'HOME',
        };

        //无论caller是谁，都指向this
        this.handlePageChange = this.handlePageChange.bind(this);
    }

    

    handlePageChange(newPage){
        this.setState({
            page:newPage,
        });
    }
    render() {
        const {page} = this.state;

        return(
            <div className="main">
                <div className="container">
                <Header 
                    onPageChange = {this.handlePageChange}
                    page = {page}
                />
                <Page arg = {page} />
                <Footer />
                </div>
            </div>
        );
    }
}

export default App;
```
```js
//Header.js
import React from 'react';
import styled from 'styled-components';
import Flex from '../../components/Flex';
import './components/NavbarItem/NavbarItem.css';


const Highlight = styled.span`
    color:#377e9a;
`;

const Logo = styled.div`
    font-size: 1.5rem;
    font-weight:500;
`;

const Nav = styled(Flex)`
    padding: 15px 0;
    align-items: center;
`;

const NavbarItem = styled.button`
    
    border: 0;
    background: transparent;
    cursor: pointer;
    padding: 16px;
    text-decoration: none;
    color: #49515d;
    font-size: 15px;
    opacity: ${(props) => props.active ? '1':'0.6'};
    display: block;
    transition: opacity 0.3s ease-in-out;

    ${(props) => {
        console.log(props);
    }}

    /* SCSS 规范 */
    &::after {
        content: "";  
        width: ${(props) => props.active ? '24px' : '0'};
        border-bottom: 3px solid #377e9a;
        margin: auto;
        margin-top: 4px;
        display: block;
        transition: width 0.3s ease-in-out;
    }

    &:hover{
        opacity: 1;
    }

    &:hover::after {
        width: 24px;
    }
      
    &:last-of-type {
        padding-right: 0;
    }
`;

const Left = styled.div`
    flex: 1;
`;

const Right = styled.div`
`;


const Header = ({
    onPageChange,
    page,
}) => {

    const navbarItems = [
        { key: 'HOME', value: 'Home' },
        { key: 'RESUME', value: 'Resume' },
        { key: 'SERVICES', value: 'Services' },
        { key: 'BLOG', value: 'Blog' },
        { key: 'CONTACT', value: 'Contact' }
    ]


    return (
    <Nav>
        <Left>
            <Logo>
                <Highlight>Tifa</Highlight>
                Lockhart
            </Logo>
        </Left>
        <Right>
            <Flex>
                {navbarItems.map((navbarItem) => (
            <NavbarItem 
              onClick = {() => onPageChange(navbarItem.key)}
              key = {navbarItem.key}
              active = {page === navbarItem.key}
              href = {navbarItem.value} >
            {navbarItem.value}
            </NavbarItem>
            ))}
            </Flex>
        </Right>
</Nav>
);
}

export default Header;
```
综合以上，我们即通过state来实现点击button，更改页面渲染

```
const ITEMS = [{
href: 'HOME',
name: 'Home Page',
}, {
href: 'RESUME',
name: 'Resume',
}];


let activeItem;

const renderNavigation = () => {
const elements = ITEMS.map((item) => {
const text = document.createTextNode(item.name);
const a = document.createElement('a');

a.setAttribute('href', item.href);
a.appendChild(text);

a.classList.add('navbar__item');

if (item.href === activeItem) {
a.classList.add('navbar__item--active');
}

a.onclick = (event) => {
event.preventDefault();

activeItem = item.href;

renderNavigation();
}

return a;
});

document.querySelector('#root').innerHTML = '';
elements.forEach((element) => document.querySelector('#root').appendChild(element));
}
```
以上代码，要理解React背后的核心工作原理（申明式编程）