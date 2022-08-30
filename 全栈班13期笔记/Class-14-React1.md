# Class-14 React-1
## 主要知识点
  - [1.解释型语言](#1解释型语言)
  - [2.为什么学React](#2为什么学react)
    - [2.1 以史为镜，可以知得失，React的发展史](#21-以史为镜可以知得失react的发展史)
    - [2.2 React的好处，与Angular的对比](#22-react的好处与angular的对比)
  - [3.React 三大特性](#3react-三大特性)
    - [3.1 Declarative](#31-declarative)
      - [3.1.1 Imperative 命令式](#311-imperative-命令式)
      - [3.1.2 Declarative 声明式](#312-declarative-声明式)
      - [3.1.3 命令式 VS 声明式](#313-命令式-vs-声明式)
      - [3.1.4 其他小问题](#314-其他小问题)
    - [3.2 Component-Based（模块化）](#32-component-based模块化)
      - [3.2.1 模块化举例与理解](#321-模块化举例与理解)
    - [3.3 Learn Once, Write Anywhere](#33-learn-once-write-anywhere)
    - [3.4 课间问题解答](#34-课间问题解答)
  - [4.React实践](#4react实践)
    - [4.1 安装React](#41-安装react)
    - [4.2 引入并配置webpack](#42-引入并配置webpack)
    - [4.3 使用jsx](#43-使用jsx)
    - [4.4 使用component](#44-使用component写法)
    - [4.5 使用create-react-app 快速搭建react app](#45-使用create-react-app-快速搭建react-app)
  
# 课堂笔记

## 1.解释型语言
解释型语言： 更human-being一些，分变量与常量。但是从实际角度出发，绝大多数存在的是常量。
- 龙哥提醒，写let的时候要自己想，我真的需要let吗

## 2.为什么学React  
React让你尽量用少量的JS做更复杂的工作
- 龙哥提醒，首先写代码的时候，要human-being的方式思考一下，出了什么问题，使用该技术解决了什么问题。
  
### 2.1 以史为镜，可以知得失，React的发展史
只有（写HTML）难受了，才能去想到学习React  
历史时间线： AngularJS -> React -> Angular -> VUE
jQuery -> AngularJS -> React/ Angular -> VUE
- React的出现，倒逼AngularJS重写回了Angular
### 2.2 React的好处，与Angular的对比
- React到底好在哪里
    - VS Angular：One framework Mobile & Desktop
        - Angular可以做前端的所有事情
        - framework是架构是平台，是everything，学了Angular，从开发到部署到上线，前端，都会了。大而全，涵盖了前端所有东西。但是违反了solid中的单一职责
    - React: A JavaScript Library for building user interface
        - 只能做一件事情：UI
        - JavaScript Library
        - Only User interface, 只替代了Style相关的html，动态的html

## 3.React 三大特性
- Declarative
- Component-Based
- Learn Once, Write Anywhere
### 3.1 Declarative 声明式
做UI时，React让我们只用声明式去设计UI，再去控制内部状态的改变，UI就会根据状态的改变而改变。
- painless
- design
- efficiently update and render when data change
- more predictable and easier to debug
#### 3.1.1 Imperative 命令式
- Imperative 命令式
    - 现实世界中，我们⼤部分编码都是命令式的，例如
    ```js
    document.querySelector('#resume-page').classList.add('page--active');
    ```
    命令DOM更新，命令document去找东西，命令更新classlist
#### 3.1.2 Declarative 声明式
- Declarative 声明式
    - 例如 SQL，我们声明数据库，告诉数据库要什么，然后数据库就会给你对应的数据，⽽不是通过数据库的 API去取
    ```sql
    SELECT * FROM Products WHERE name='Alipay'
    ```
#### 3.1.3 命令式 VS 声明式
- 命令式 VS 声明式
    - ⼀家命令式餐馆，从客⼈进⼊店开始
    ```
    1. ⽼板告诉（命令）客⼈坐在 N 号桌。
    2. 客⼈向⽼板点餐 「交互」。
    3. ⽼板告诉（命令）后厨做⼏道什么样的菜。
    4. ⽼板告诉（命令）厨师放什么原材料，多少调料，⼏成熟。
    5. ⽼板上菜。
    ```
    5步里3步是命令，例如传统fish&chips。
    老板作为发号施令的人，必不可少。必须有一个核心的(老板)存在   
    以下为命令式代码： 
    ```jsx
    //切换到resume页面
    document.querySelector('#resumePage').classList.add('page--active');
    document.querySelector('[href="resume"]').classList.add('navItem--active');
    ```

    - ⼀家声明式餐馆，从客⼈进⼊店开始
    ```
    1. 当 Waiting Zone 有客⼈时，服务员A带客⼈⼊座。
    2. 当客⼈⼊座服务员B管理区域时，服务员B点单。
    3. 当客⼈点好单，服务员B讲单据送到后厨。
    4. 当后厨看到新的单据时，根据单据做菜。
    5. 当服务员C看到 Pick Up 区有菜品时，根据单据上菜。
    ```
    没有一个人发号施令，却每个人都有条不紊的进行工作，例如麦当劳
    以下为声明式代码： 
    ```jsx
    <button
        href="home"
        class={`navItem ${activePage === 'homepage' ? 'navItem---active' : ''}`}
        onclick = {activePage = 'homepage'}
    >
        Home
    </button>
    <button
        href="resume"
        class={`navItem ${activePage === 'resumePage' ? 'navItem---active':''}`}
        onclick = {activePage = 'resumePage'}
    >
        Resume
    </button>

    // ...
    <div class={`page ${activePage === 'homepage' ? 'page---active':''}`}>
    // ...
    </div>
    <div class={`page ${activePage === 'resumePage' ? 'page---active':''}`}>
    // ...
    </div>
    ```   
    申明式，重结果，轻过程
    命令式，重过程，轻结果
#### 3.1.4 其他小问题
- 为什么去写JS
    - 为了交互，为了操作页面（DOM，HTML）
- Q:声明式代码必须写在html里么?
    - A：好的声明式代码应该是紧跟html一起的，因此只有跟html一起的才是声明式
- Q:有个原则就是 越少js 越好吗
    - A: 是的。js仅是来处理ui交互的

### 3.2 Component-Based（模块化）
⽹⻚程序在业务发展的过程中体积越来越庞⼤，其中堆叠了⼤量的业务逻辑代码，不同业务模块的代码相互调⽤，相互嵌套，代码之间的耦合性越来越⾼，调⽤逻辑会越来越混乱。当某个模块需要升级的时候，改动代码的时候往往会有牵⼀发⽽动全身的感觉。特别是多⼈合作的情况下，代码的维护会让⼈奔溃。
#### 3.2.1 模块化举例与理解
- 模块化举例
    - 宜家家具：家具被划分成⽆数个⼩零件（Component），不同家具的⼩零件（Component）因为规格相同可以互相使⽤，安装⽅便
    - 乐⾼：相同规格的积⽊（Component）通过不同的组合⽅式组成不同的产品。
    - ⼤型⼯程：京港澳跨海⼤桥。由⼤桥，引道组成。⼤桥由桥⾯，桥墩，...。整体桥⾯由多个⼩桥⾯组成。每个⼩桥⾯由...组成，每个...由...组成，这种每个⼩产品（Component）由分布在各地不同的⼯⼚⽣产，最⼤化效率。
模块化代码举例：
```jsx
<body>
  <Header />
  <Pages />
  <Footer />

<!-- Header -->
<Logo />
<Navigation />

<!-- Navigation -->

<!-- Pages -->
<HomePage />
<ResumePage />
```
- 模块化有什么好处
    - Single Responsibility
    - Open Close
    - 就近维护，⾯向功能（责任）

### 3.3 Learn Once, Write Anywhere
学会了React，你就什么都会了，比如  
Server Side Rendering (SSR)  
React Native (RN)  
React DOM  (HTML Web)  
React VR  (VR)  
React TV  (TV) 
React IOT  (IOT)

### 3.4 课间问题解答
- Q:如何发现问题
    - A:三省吾身，自我批判，自我否定。写完代码后，就是觉得它不好，基于不好的角度，想问题出在哪里。
- Q:react 服务端渲染 是和那种引擎模板的功能差不多吗
    - A:首先要去了解各种渲染模式的不同和优劣，以及工作原理，具体可以问小花去要龙哥的公开课视频
- Q:老师用过dreamwaver吗
    - A:基本不用。
- Q:简历要求里3-5年经验一下子就把我吓着了
    - A:（龙哥）仅用了4年爬到principal。作为JR毕业学生，很多都无视JD里的工作经验年限要求。从HR角度来看，加个工作年限就能降低风险。工作年限不重要，只是用来吓退混子的。保证自己水品到位就可以了。
- 融入公司文化比较难，culture有时候就是理解不了。很难到达管理层。

尝试用create-react-app写P1，参考网站 https://reactjs.org/docs/getting-started.html

## 4.React实践
### 4.1 安装React
- Node package manager  
我们通常用yarn或者npm来管理外部依赖模块  
在之前我们已经学习过js的模块化，分为 ESModule和CommonJS  
使用命令init项目：  
`npm init`
- 自动生成pacakage.json
    - 其中version, description不要管，main不需要管，script可以先留空，repo如果有可以留着，author可以留着，license，homepage，bug可以删掉，可以加`"private": true`
    - script: 告诉项目怎么样去执行命令的
    - dependencies:中的lib可以是production需要的，也可以是development需要的
    - devDependencies：中的lib是development需要的 
  
    使用命令:  
    `npm i react`
- 安装react， "dependencies"会自动加入react，同时生成版本锁    
使用命令:    
`npm i react-dom`
- 安装react-dom
- Q: reactDOM 具体是干嘛的
    - A: 负责把相应的代码渲染到DOM上
- Q: script标签为什么不是在head里
    - A: html标准执行顺序是逐行，在执行script的时候如果还没有渲染到body的话，会报错；除非加入`defer`
- Q: dependency 和 devdependency 要严格区分吗
    - A: 严格要求自己，要区分

### 4.2 引入并配置webpack
新建`index.js`,里面敲入代码:     
`import React from 'react';`  
新建`index.html`,敲入标准html：
```html
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
    <script src="dist/main.js"></script>
  </body>

</html>
```
调用react,我们的目标是把`<div> hello world </div>`渲染到html里去
- 这里，写import会把解释型代码变为编译型代码，浏览器将无法运行；需要通过webpack来解决，使用命令    
`npm i webpack`   
- 新建`webpack.config.js`，并更新`package.json`中的配置  
```
 "scripts": {
    "build": "webpack"
  },
```
`webpack.config.js`中也需要更新entry：
```js
module.exports = {
    //需要打包什么样的东西
    mode: 'development',
    entry: './index.js',
}

```
`index.js`中来实现我们的渲染目标
```js
    import React from 'react';
    import ReactDOM from 'react-dom';
    import App from './App';

    ReactDOM.render(

    //createElement: 第一个参数是tag name，第二个参数是attribute，第三个参数是children
    React.createElement('div',{},'Hello world'),
    document.querySelector('#app'),
    );
    
```
`index.html`中还需要更新
```
  <body>
    <div id="app"></div>
    <script src="dist/main.js"></script>
  </body>
```
- `npm run build`：打包

### 4.3 使用jsx
我们发现上面index.js中，createElement组成的代码块并不宜读，因此我们改上面为JSX的写法
```js
ReactDOM.render(
    (
        <div id = 'my-div'>
            <p>hello world</p>
        </div>
    ),
    document.querySelector('#app'),
);
```
- 为实现以上代码块，编译jsx to jx, 需要引入babel  
  
  - Function Component 返回⼀个 React Component，这是⼀种对渲染内容的轻量级描述。⼤多数的 React 开发者使⽤了⼀种名为 “JSX” 的特殊语法    
    - JSX 可以让你更轻松地书写这些结构。语法` <div />` 会被编译成 React.createElement('div')。  
    - JSX 给我们更⼤的便利维护代码，因为 HTML in JS。但是需要注意，⼀些 HTML 的 keywords 在 JSX 是不⼀样的，不如 class。   
    - 安装babel
        - `npm i -D babel`
        - D表示安装的是一个dev dependency
        - 安装babel loader,babel core, reset-react：
        - `npm i -D babel-loader`
        - `npm i -D @babel/core`
        - `npm i -D @babel/preset-react`
        - 在`webpack.config.js`中更新配置:rules注入一个规则，test表示当打包时遇到js，使用babel-loader运行打包(load)，运行时的option为preset-react
        ```js
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
          }
        ]
       }
        ```

- 通过上面，我们看到运行React，我们实际需要的安装顺序
    - React，ReactDOM, webpack, jsx, babel(core,preset-react)

### 4.4 使用component写法
如何将上面的代码功能，改为模块化，我们需要
- 更新`App.js`
    ```js
    import React from 'react';

    const App = () => {
        return (
            <div> My App </div>
        );
    };

    export default App;
    ``` 
- 更新`index.js`,加入App.js
    ```js
    import App from './App';

    ReactDOM.render((<App />),document.querySelector('#app'));
    ```
- 通过App.js中的一个箭头函数，返回一段jsx片段，这就是function component

- 使⽤ JSX 组合和渲染⾃定义的 React 组件
    - 定制的组件名首字母一定要大写
- 留给课下的两个问题
    - 为什么需要引入React？
    - html attrs的另命名

### 4.5 使用create-react-app 快速搭建react app
- create-react-app
    - https://reactjs.org/docs/create-a-new-react-app.html
    - a comfortable environment for learning React
    ```
    npx create-react-app my-app
    cd my-app
    npm start
    ```
- Q:这个自动出可能打啥的是啥插件？
    - A:zsh-autosuggestions
- Q:直接用脚手架 和 自己做配置相比有什么问题
    - A:直接用脚手架比自己做舒服的多；但是公司里绝大多数都会手写webpack，手写babel。所以我们课上学webpack，足够应对面试。可以写不出来，但是一定要明白他的原理。