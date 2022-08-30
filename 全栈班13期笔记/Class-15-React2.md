# Class-15 React-2
(本节代码较多，可跳过部分代码阅读)
## 主要知识点
  - [1.课前答疑，及上节课回顾](#1课前答疑及上节课回顾)
    - [1.1 React相关面试问题思路](#11-react相关面试问题思路)
    - [1.2 React上节课知识点回顾](#12-react上节课知识点回顾)
  - [2.将P1改造成模块化的React](#2将p1改造成模块化的react)
    - [2.1 将P1改造成React](#21-将p1改造成react)
    - [2.2 将以上的React模块化](#22-将以上的react模块化)
    - [2.3 模块化page，解决page过大问题](#23-模块化page解决page过大问题)
    - [2.4 React中，import与export的对应关系](#24-react中import与export的对应关系)
    - [2.5 CSS的模块化](#25-css的模块化)
  - [3.使用styled-components](#3使用styled-components)
  - [4.课间Q&A](#4课间qa)
  - [5.项目文件结构化](#5项目文件结构化)
    - [5.1 依据RMR原则，重构app下的文件结构](#51-依据rmr原则重构app下的文件结构)
    - [5.2 更新import, 引入index](#52-更新import-引入index)
    - [5.3 从maintainable角度看，为什么一定要引入index](#53-从maintainable角度看为什么一定要引入index)


# 课堂笔记

## 1.课前答疑，及上节课回顾
- Q: 曾经有面试官问我有没Github账号，想知道他想在我的账号里看到什么东西呢？
  - A: 看你做的项目，比如https://github.com/jasonzhang7100
### 1.1 React相关面试问题思路  
关于React面试问题的思路,比如
- 什么是好的代码，你为什么写React，通过React你学到了什么
 
以上都可以通过下面三点来答
- Declarative
- Component-based
- Learn Once, Write Anywhere
  
什么是好的代码
- RMR
  
如何写出一个好的代码
- SOLID原则
  
什么是好的React代码
- 足够的Declarative，Component-based
- 针对以上两点，可以准备一下答案，比如从一个餐厅开始聊起
  
技术型面试的话，大概率会问到React和Angular的区别  
问及什么是React的时候，答案出发点为 A JavaScript library for building user interfaces
- Javascript library
- user interfaces
  
为什么JS跟以前的Script Language不一样了？
- 因为我们逐步加入了各种东西，比如Jsx，使js从解释型代码向编译型代码转变
  
面试中，如果能说到 解释型代码 vs 编译型代码的优缺点，也是非常好的

Jsx是什么
- 从RMR角度出发，一个让我们更容易书写的代码，例如在JS中直接写html，更加RMR

在index.js中，我们知道为什么import ReactDOM，import App，因为我们在本文件下面都会调用ReactDOM和App，但是我们为什么在所有Jsx文件都需要import React呢？
- JSX需要编译，在编译的过程中JSX被编译成 React.createElement

### 1.2 React上节课知识点回顾
React的编译需要的两个重要工具：
- Babel -> compile jsx to js: <App /> -> React.createElement
- Webpack -> bundle
  - 我们写了`import App from './App'`,`import React from 'react'`,我们需要webpack找到相应的代码并打包

什么是component based：
- 一个函数返回的JSX代码片段，单一职责的

一个React的项目，除了index.js作为入口为html，就不应该再出现其它的html了

- 重要的语法
  - 在JSX中，如果statement，以<开头，那么在相应的>之前的内容会被当做markup来处理，以{开头，那么在相应的}之前的内容会被当做js来处理
  
- 申明式写出来的的代码，大家写出来的代码应该是相同的。这是规范化的好处

- Q:`((App /)`中，第二层括号能不能省略
  - A: `()`在JS中是不做任何作用的，可以省略。但是加了更readable一些。 


## 2.将P1改造成模块化的React
### 2.1 将P1改造成React
首先，在上节课代码的基础上。
- 1. 更新`App.js`
  ```js
  //App.js
    import React from 'react';

    const App = () => (
        <div class="main">
        <div class="container">
        <header class="nav">
            <div class="nav__left">
            <div class="logo">
                <span class="logo__highlight">Tifa</span>
                Lockhart
            </div>
            </div>
            <div class="nav__right">
            <div class="navbar">
                <a class="navbar__item" href="HOME">Home</a>
                <a class="navbar__item" href="RESUME">Resume</a>
                <a class="navbar__item" href="SERVICES">Services</a>
                <a class="navbar__item" href="BLOG">Blog</a>
                <a class="navbar__item" href="CONTACT">Contact</a>
            </div>
            </div>
        </header>
        <div class="pages">
            <div id="HOME" class="page">
            <div class="page__header homepage__header">
                <image class="homepage__avatar" src="./assets/avatar.png" alt="Avatar" />
                <div class="homepage__title">
                <h2 class="homepage__name">Tifa Lockhart</h2>
                <div class="homepage__position">Final Fantasy VII</div>
                <div class="homepage__socialMedias">
                    <i class="fab fa-twitter homepage__socialMediaItem"></i>
                    <i class="fab fa-facebook-f homepage__socialMediaItem"></i>
                    <i class="fab fa-instagram homepage__socialMediaItem"></i>
                </div>
                </div>
            </div>
            <div class="page__content homepage__content">
                <div>
                <h3 class="homepage__aboutMeHeader">
                    About
                    <span class="homepage__aboutMeHeaderHighlight">Me</span>
                </h3>
                <div class="homepage__aboutMeContent">
                    Bright and optimistic, Tifa always cheers up the others when they're down. But don't let her looks fool you, she can decimate almost any enemy with her fists...
                </div>
                </div>
                <table class="homepage__contact">
                <tr>
                    <td>Age</td>
                    <td>20</td>
                </tr>
                <tr>
                    <td>Residence</td>
                    <td>Gaia</td>
                </tr>
                <tr>
                    <td>Address</td>
                    <td>Level 3 / 57 Coronation Drive, Brisbane</td>
                </tr>
                <tr>
                    <td>Email</td>
                    <td>
                    <a href="mailto:info@jiangren.com.au">
                        info@jiangren.com.au
                    </a>
                    </td>
                </tr>
                <tr>
                    <td>Phone</td>
                    <td>+0123 123 456 789</td>
                </tr>
                </table>
            </div>
            </div>
            <div id="RESUME" class="page">
            <div class="page__header">
                <h2 class="page__title">RESUME</h2>
            </div>
            <div class="page__content">
                <div class="resumePage__sub">
                <div>
                    <h3 class="resumeSub__title">Education</h3>
                    <div class="timelines">
                    <div class="timeline">
                        <h4 class="experience__title">Specialization Course</h4>
                        <div class="experience__meta">
                        <span class="experience__year">2010</span>
                        &nbsp;
                        <i class="experience__divider"></i>
                        &nbsp;
                        <spans class="experience__company">Apple Inc.</spans>
                        </div>
                        <div class="experience__description">
                        Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                        </div>
                    </div>
                    <div class="timeline">
                        <h4 class="experience__title">Specialization Course</h4>
                        <div class="experience__meta">
                        <span class="experience__year">2010</span>
                        &nbsp;
                        <i class="experience__divider"></i>
                        &nbsp;
                        <spans class="experience__company">Apple Inc.</spans>
                        </div>
                        <div class="experience__description">
                        Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                        </div>
                    </div>
                    <div class="timeline">
                        <h4 class="experience__title">Specialization Course</h4>
                        <div class="experience__meta">
                        <span class="experience__year">2010</span>
                        &nbsp;
                        <i class="experience__divider"></i>
                        &nbsp;
                        <spans class="experience__company">Apple Inc.</spans>
                        </div>
                        <div class="experience__description">
                        Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                        </div>
                    </div>  
                    </div>
                </div>
                <div>
                    <h3 class="resumeSub__title">Experience</h3>
                    <div class="timelines">
                    <div class="timeline">
                        <h4 class="experience__title">Specialization Course</h4>
                        <div class="experience__meta">
                        <span class="experience__year">2010</span>
                        &nbsp;
                        <i class="experience__divider"></i>
                        &nbsp;
                        <spans class="experience__company">Apple Inc.</spans>
                        </div>
                        <div class="experience__description">
                        Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                        </div>
                    </div>
                    <div class="timeline">
                        <h4 class="experience__title">Specialization Course</h4>
                        <div class="experience__meta">
                        <span class="experience__year">2010</span>
                        &nbsp;
                        <i class="experience__divider"></i>
                        &nbsp;
                        <spans class="experience__company">Apple Inc.</spans>
                        </div>
                        <div class="experience__description">
                        Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                        </div>
                    </div>
                    <div class="timeline">
                        <h4 class="experience__title">Specialization Course</h4>
                        <div class="experience__meta">
                        <span class="experience__year">2010</span>
                        &nbsp;
                        <i class="experience__divider"></i>
                        &nbsp;
                        <spans class="experience__company">Apple Inc.</spans>
                        </div>
                        <div class="experience__description">
                        Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                        </div>
                    </div>  
                    </div>
                </div>
                </div>
                <div class="resumePage__sub">
                <div>
                    <h3 class="resumeSub__title">Design <span class="resumeSub__titleHighlight">Skills</span></h3>
                    <div class="skill">
                    <h4 class="skill__title">Web Design</h4>
                    <div class="skill__level skill__level--webDesign"></div>
                    </div>
                    <div class="skill">
                    <h4 class="skill__title">Graphic Design</h4>
                    <div class="skill__level skill__level--graphicDesign"></div>
                    </div>
                    <div class="skill">
                    <h4 class="skill__title">Print Design</h4>
                    <div class="skill__level skill__level--printDesign"></div>
                    </div>
                </div>
                <div>
                    <h3 class="resumeSub__title">Coding <span class="resumeSub__titleHighlight">Skills</span></h3>
                    <div class="skill">
                    <h4 class="skill__title">HTML Design</h4>
                    <div class="skill__level skill__level--htmlDesign"></div>
                    </div>
                    <div class="skill">
                    <h4 class="skill__title">CSS Design</h4>
                    <div class="skill__level skill__level--cssDesign"></div>
                    </div>
                    <div class="skill">
                    <h4 class="skill__title">JavaScript Design</h4>
                    <div class="skill__level skill__level--jsDesign"></div>
                    </div>
                </div>
                </div>
            </div>
            </div>
            <div id="SERVICES" class="page">
            <div class="page__header">
                <h2 class="page__title">Services</h2>
            </div>
            <div class="page__content">
                <div class="servicesPage__services">
                <h3 class="services__title">
                    My
                    <span class="services__titleHightLight">Services</span>
                </h3>
                <div class="services">
                    <div class="serviceItem">
                    <div class="serviceItem__imageContainer">
                        <img alt="HTML5" src="./assets/html5.png" class="serviceItem__image"></img>
                    </div>
                    <h4 class="serviceItem__name">HTML5</h4>
                    <div class="serviceItem__description">Hypertext Markup Language (HTML) is the standard markup language for documents designed to be displayed in a web browser.</div>
                    </div>
                    <div class="serviceItem">
                    <div class="serviceItem__imageContainer">
                        <img alt="CSS3" src="./assets/css3.png" class="serviceItem__image"></img>
                    </div>
                    <h4 class="serviceItem__name">CSS3</h4>
                    <div class="serviceItem__description">Cascading Style Sheets (CSS) is a style sheet language used for describing the presentation of a document written in a markup language like HTML.</div>
                    </div>
                    <div class="serviceItem">
                    <div class="serviceItem__imageContainer">
                        <img alt="JavaScript" src="./assets/js.png" class="serviceItem__image"></img>
                    </div>
                    <h4 class="serviceItem__name">JavaScript</h4>
                    <div class="serviceItem__description">JavaScript often abbreviated as JS, is a programming language that conforms to the ECMAScript specification.</div>
                    </div>
                </div>
                </div>
                <div class="servicesPage__clients">
                <h3 class="services__title">
                    Clients
                </h3>
                <div class="clients">
                    <img alt="REA Group" src="./assets/rea.png" class="clientItem"></img>
                    <img alt="carsales.com.au" src="./assets/carsales.svg" class="clientItem"></img>
                    <img alt="Seek" src="./assets/seek.png" class="clientItem"></img>
                </div>
                </div>
            </div>
            </div>
            <div id="BLOG" class="page"></div>
            <div id="CONTACT" class="page"></div>
        </div>
        <footer class="footer">
            © 2017 All rights reserved. Designed by Jiangren
        </footer>
        </div>
    </div>
        
    );

    export default App;
  ```
- 2. 新建`main.css`，并移入css
  ```css
  //main.css
  * {
    font-family: 'Roboto', sans-serif;
    box-sizing: border-box;
  }
  
  body {
    margin: 0;
  }
  
  a {
    text-decoration: none;
    color: #377e9a;
  }
  
  .container {
    max-width: 1000px;
    margin: auto;
    min-height: 100vh;
    display: flex;
    flex-direction: column;
  }
  
  .main {
    background-color: #f5f5f5;
    background-image: url(./assets/main_bg.png);
    background-size: cover;
    background-repeat: no-repeat;
  }
  
  .nav {
    padding: 15px 0;
    display: flex;
    align-items: center;
  }
  
  .nav__left {
    flex: 1;
  }
  
  .logo {
    font-size: 1.5rem;
    font-weight: 500;
  }
  
  .logo__highlight {
    color: #377e9a;
  }
  
  .navbar {
    display: flex;
  }
  
  .navbar__item {
    padding: 16px;
    text-decoration: none;
    color: #49515d;
    font-size: 15px;
    opacity: 0.6;
    display: block;
    transition: opacity 0.3s ease-in-out;
  }
  
  .navbar__item::after {
    content: "";  
    width: 0;
    border-bottom: 3px solid #377e9a;
    margin: auto;
    margin-top: 4px;
    display: block;
    transition: width 0.3s ease-in-out;
  }
  
  .navbar__item--active,
  .navbar__item:hover {
    opacity: 1;
  }
  
  .navbar__item--active::after,
  .navbar__item:hover::after {
    width: 24px;
  }
  
  .navbar__item:last-of-type {
    padding-right: 0;
  }
  
  .pages {
    padding: 15px 0;
    position: relative;
    flex: 1;
  }
  
  .page {
    display: none;
    position: absolute;
    top: 0;
    left: 0;
    right: 0;
    visibility: hidden;
    opacity: 0;
    border-radius: 16px;
    background: white;
    transition: visibility 0.3s, opacity 0.3s ease-in-out;
    box-shadow: 0px 15px 25px 0px rgba(0,0,0,0.1);
  }
  
  .page--active {
    display: block;
    position: relative;
    visibility: visible;
    opacity: 1;
  }
  
  .page__header {
    padding: 32px 64px;
    background-color: #377e9a;
    color: white;
    background-image: url(./assets/main_bg.png);
    background-size: cover;
    background-repeat: no-repeat;
    border-top-left-radius: 16px;
    border-top-right-radius: 16px;
  }
  
  .page__title {
    margin: 0;
    text-align: center;
    font-size: 44px;
  }
  
  .page__content {
    padding: 32px 64px;
    background-color: white;
    border-bottom-left-radius: 16px;
    border-bottom-right-radius: 16px;
  }
  
  .homepage__header {
    display: flex;
    padding-bottom: 0;
    align-items: center;
  }
  
  .homepage__title {
    flex: 1;
    display: flex;
    flex-direction: column;
    align-items: center;
  }
  
  .homepage__avatar {
    border-radius: 4px;
    width: 250px;
    height: 250px;
    margin: 24px 0 -24px;
    border: 3px solid white;
    box-shadow: 0px 3px 8px 0px rgba(0,0,0,0.1);
    transition-property: transform, box-shadow;
    transition-duration: 0.3s;
    transition-timing-function: ease-in-out;
  }
  
  .homepage__avatar:hover {
    transform: translateY(-8px);
    box-shadow: 0 18px 24px rgba(0, 0, 0, 0.15);
  }
  
  .homepage__name {
    margin: 0;  
    font-size: 3rem;
    font-weight: 500;
  }
  
  .homepage__position {
    font-size: 1.25rem;
    margin-top: 8px;
  }
  
  .homepage__socialMedias {
    margin-top: 16px;
    display: flex;
    justify-content: center;
  }
  
  .homepage__socialMediaItem {
    display: flex;
    align-items: center;
    justify-content: center;
    box-sizing: content-box;
    width: 16px;
    height: 16px;
    margin: 0 4px;
    color: rgba(0, 0, 0, 0.5);
    background-color: white;
    padding: 8px;
    border-radius: 100%;
  }
  
  .homepage__content {
    padding-top: 56px;
  }
  
  .homepage__content,
  .resumePage__sub {
    display: flex;
    justify-content: space-between;
  }
  
  .homepage__content > div,
  .resumePage__sub > div {
    flex-basis: calc(50% - 32px);
  }
  
  .homepage__aboutMeHeader {
    margin-top: 0;
    font-size: 1.5rem;
    font-weight: bold;
  }
  
  .homepage__aboutMeHeaderHighlight {
    color: #377e9a;
  }
  
  .homepage__aboutMeContent {
    line-height: 1.75;
  }
  
  .homepage__contact {
    border: 0;
  }
  
  .homepage__contact td {
    padding: 4px 0;
  }
  
  .homepage__contact td:first-of-type {
    padding-right: 42px;
  }
  
  .homepage__contact td:last-of-type {
    color: #9e9e9e;
  }
  
  .footer {
    color: rgba(0, 0, 0, 0.5);
    text-align: center;
    margin: 8px 0;
  }
  
  .resumeSub__title {
    margin-top: 0;
  }
  
  .timelines {
    border-left: 2px solid #dadada;
    padding: 8px 0 8px 48px;
  }
  
  .timelines > div {
    margin-top: 16px;
    margin-bottom: 16px;
  }
  
  .timeline {
    position: relative;
    padding: 16px 20px;
    border-radius: 4px;
    box-shadow: 0px 3px 8px 0px rgba(0,0,0,0.1);
    border-left: 2px solid #377e98;
    margin-left: -5px;
  }
  
  .timeline::before {
    content: "";
    width: 48px;
    border-bottom: 2px solid #377e98;
    position: absolute;
    left: -48px;
    top: 8px;
  }
  
  .timeline::after {
    content: "";
    position: absolute;
    left: -52px;
    width: 10px;
    height: 10px;
    border-radius: 100%;
    border: 2px solid #377e98;
    top: 2px;
    background: white;
  }
  
  .experience__title {
    margin: 0 0 8px;
  }
  
  .experience__meta {
    font-size: 0.8rem;
    margin-bottom: 8px;
  }
  
  .experience__year {
    color: #377e98;
  }
  
  .experience__divider {
    border-right: 1px solid #dadada;
  }
  
  .experience__company {
    color: #49515d;
  }
  
  .experience__description {
    line-height: 1.75;
  }
  
  .resumePage__sub + .resumePage__sub {
    margin-top: 32px;
  }
  
  .resumeSub__titleHighlight {
    color: #377e98;
  }
  
  .skill {
    margin: 16px 0;
  }
  
  .skill__title {
    margin: 0 0 8px;
    font-size: 0.8rem;
  }
  
  .skill__level {
    position: relative;
    height: 16px;
    background-color: rgba(0,0,0,0.1);
  }
  
  .skill__level:after {
    content: "";
    position: absolute;
    left: 0;
    top: 0;
    bottom: 0;
    background-color: #377e98;
  }
  
  .skill__level--webDesign:after {
    width: 80%;
  }
  
  .skill__level--graphicDesign:after {
    width: 70%;
  }
  
  .skill__level--printDesign:after {
    width: 75%;
  }
  
  .skill__level--htmlDesign:after {
    width: 90%;
  }
  
  .skill__level--cssDesign:after {
    width: 85%;
  }
  
  .skill__level--jsDesign:after {
    width: 70%;
  }
  
  .services__titleHightLight {
    color: #377e9a;
  }
  
  .services {
    display: flex;
    justify-content: space-around;
    margin: 48px 0;
  }
  
  .serviceItem {
    width: calc(100%/3);
    margin: 0 32px;
    display: flex;
    align-items: center;
    flex-direction: column;
  }
  
  .serviceItem__imageContainer {
    width: 125px;
    height: 125px;
    display: flex;
    align-items: center;
    justify-content: center;
    background-color: rgba(0, 0, 0, 0.03);
    border-radius: 100%;
  }
  
  .serviceItem__image {
    width:55px;
  }
  
  .serviceItem__name {
    font-size: 18px;
  }
  
  .serviceItem__description {
    text-align: center;
    line-height: 1.5;
    font-size: 14px;
    color: rgba(0, 0, 0, 0.5);
  }
  
  .clients {
    display: flex;
    justify-content: space-around;
    align-items: center;
  }
  
  .clientItem {
    width: 150px;
  }
  
  .blogs {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
  }
  
  .blog {
    width: calc(100%/2 - 16px);
    margin: 16px 0;
  }
  
  .blog__image {
    border-radius: 16px;
    width: 100%;
    height: 100%;
  }
  ```  
- 3. 更新`index.html`
  ```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8" />
        <meta http-equiv="X-UA-Compatible" content="IE=edge" />
        <meta name="viewport" content="width=device-width, initial-scale=1.0" />
        <title>Demo</title>
        <link rel = "stylesheet" href="main.css">
    </head>

    <body>
        <div id="app"></div>
        <script src="dist/main.js"></script>
    </body>

    </html>
  ``` 
- 4. 更新`App.js`中
  ```html
  <a class="navbar__item navbar__item--active" href="HOME">Home</a>
  <div id="HOME" class="page page--active">
  ``` 
以上为不在index.html中写html的情况下，怎么通过jsx来实现一个html页面(快速找到Home page active)

### 2.2 将以上的React模块化
- 1. 新建app文件夹
- 2. 在app中新建`Header.js`
  ```js
  //Header.js
    import React from `react`;

    const Header = () => (
        <header class="nav">
            <div class="nav__left">
            <div class="logo">
                <span class="logo__highlight">Tifa</span>
                Lockhart
            </div>
            </div>
            <div class="nav__right">
            <div class="navbar">
                <a class="navbar__item navbar__item--active" href="HOME">Home</a>
                <a class="navbar__item" href="RESUME">Resume</a>
                <a class="navbar__item" href="SERVICES">Services</a>
                <a class="navbar__item" href="BLOG">Blog</a>
                <a class="navbar__item" href="CONTACT">Contact</a>
            </div>
            </div>
    </header>
    );

    export default Header;
  ``` 
- 3. `App.js`中替换Header, 导入Header
  ```js
  import Header from './app/Header';
  ``` 
- 4. 在app中新建`Page.js`
  ```js
  //Page.js
    import React from 'react';

    const Page = () => (
        <div class="pages">
        <div id="HOME" class="page page--active">
        <div class="page__header homepage__header">
            <image class="homepage__avatar" src="./assets/avatar.png" alt="Avatar" />
            <div class="homepage__title">
            <h2 class="homepage__name">Tifa Lockhart</h2>
            <div class="homepage__position">Final Fantasy VII</div>
            <div class="homepage__socialMedias">
                <i class="fab fa-twitter homepage__socialMediaItem"></i>
                <i class="fab fa-facebook-f homepage__socialMediaItem"></i>
                <i class="fab fa-instagram homepage__socialMediaItem"></i>
            </div>
            </div>
        </div>
        <div class="page__content homepage__content">
            <div>
            <h3 class="homepage__aboutMeHeader">
                About
                <span class="homepage__aboutMeHeaderHighlight">Me</span>
            </h3>
            <div class="homepage__aboutMeContent">
                Bright and optimistic, Tifa always cheers up the others when they're down. But don't let her looks fool you, she can decimate almost any enemy with her fists...
            </div>
            </div>
            <table class="homepage__contact">
            <tr>
                <td>Age</td>
                <td>20</td>
            </tr>
            <tr>
                <td>Residence</td>
                <td>Gaia</td>
            </tr>
            <tr>
                <td>Address</td>
                <td>Level 3 / 57 Coronation Drive, Brisbane</td>
            </tr>
            <tr>
                <td>Email</td>
                <td>
                <a href="mailto:info@jiangren.com.au">
                    info@jiangren.com.au
                </a>
                </td>
            </tr>
            <tr>
                <td>Phone</td>
                <td>+0123 123 456 789</td>
            </tr>
            </table>
        </div>
        </div>
        <div id="RESUME" class="page">
        <div class="page__header">
            <h2 class="page__title">RESUME</h2>
        </div>
        <div class="page__content">
            <div class="resumePage__sub">
            <div>
                <h3 class="resumeSub__title">Education</h3>
                <div class="timelines">
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>  
                </div>
            </div>
            <div>
                <h3 class="resumeSub__title">Experience</h3>
                <div class="timelines">
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>  
                </div>
            </div>
            </div>
            <div class="resumePage__sub">
            <div>
                <h3 class="resumeSub__title">Design <span class="resumeSub__titleHighlight">Skills</span></h3>
                <div class="skill">
                <h4 class="skill__title">Web Design</h4>
                <div class="skill__level skill__level--webDesign"></div>
                </div>
                <div class="skill">
                <h4 class="skill__title">Graphic Design</h4>
                <div class="skill__level skill__level--graphicDesign"></div>
                </div>
                <div class="skill">
                <h4 class="skill__title">Print Design</h4>
                <div class="skill__level skill__level--printDesign"></div>
                </div>
            </div>
            <div>
                <h3 class="resumeSub__title">Coding <span class="resumeSub__titleHighlight">Skills</span></h3>
                <div class="skill">
                <h4 class="skill__title">HTML Design</h4>
                <div class="skill__level skill__level--htmlDesign"></div>
                </div>
                <div class="skill">
                <h4 class="skill__title">CSS Design</h4>
                <div class="skill__level skill__level--cssDesign"></div>
                </div>
                <div class="skill">
                <h4 class="skill__title">JavaScript Design</h4>
                <div class="skill__level skill__level--jsDesign"></div>
                </div>
            </div>
            </div>
        </div>
        </div>
        <div id="SERVICES" class="page">
        <div class="page__header">
            <h2 class="page__title">Services</h2>
        </div>
        <div class="page__content">
            <div class="servicesPage__services">
            <h3 class="services__title">
                My
                <span class="services__titleHightLight">Services</span>
            </h3>
            <div class="services">
                <div class="serviceItem">
                <div class="serviceItem__imageContainer">
                    <img alt="HTML5" src="./assets/html5.png" class="serviceItem__image"></img>
                </div>
                <h4 class="serviceItem__name">HTML5</h4>
                <div class="serviceItem__description">Hypertext Markup Language (HTML) is the standard markup language for documents designed to be displayed in a web browser.</div>
                </div>
                <div class="serviceItem">
                <div class="serviceItem__imageContainer">
                    <img alt="CSS3" src="./assets/css3.png" class="serviceItem__image"></img>
                </div>
                <h4 class="serviceItem__name">CSS3</h4>
                <div class="serviceItem__description">Cascading Style Sheets (CSS) is a style sheet language used for describing the presentation of a document written in a markup language like HTML.</div>
                </div>
                <div class="serviceItem">
                <div class="serviceItem__imageContainer">
                    <img alt="JavaScript" src="./assets/js.png" class="serviceItem__image"></img>
                </div>
                <h4 class="serviceItem__name">JavaScript</h4>
                <div class="serviceItem__description">JavaScript often abbreviated as JS, is a programming language that conforms to the ECMAScript specification.</div>
                </div>
            </div>
            </div>
            <div class="servicesPage__clients">
            <h3 class="services__title">
                Clients
            </h3>
            <div class="clients">
                <img alt="REA Group" src="./assets/rea.png" class="clientItem"></img>
                <img alt="carsales.com.au" src="./assets/carsales.svg" class="clientItem"></img>
                <img alt="Seek" src="./assets/seek.png" class="clientItem"></img>
            </div>
            </div>
        </div>
        </div>
        <div id="BLOG" class="page"></div>
        <div id="CONTACT" class="page"></div>
    </div>
    );

    export default Page;
  ``` 
- 5. `App.js`中替换Page, 导入Page
  ```js
  import Page from './app/Page';
  ``` 
- 6. 在app中新建`Footer.js`
  ```js
  //Footer.js
    import React from 'react';

    const Footer = () => (
    <footer class="footer">
        © 2017 All rights reserved. Designed by Jiangren
    </footer>
    );

    export default Footer;
  ``` 
- 7. `App.js`中替换Footer, 导入Footer
  ```js
  import Footer from './app/Footer';
  ```  
- 8. 此时，模块化后的`App.js`已经变为
  ```js
  //App.js
    import React from 'react';
    import Header from './app/Header';
    import Page from './app/Page';
    import Footer from './app/Footer';

    const App = () => (
    <div class="main">
      <div class="container">
        <Header />
        <Page />
        <Footer />
      </div>
    </div>
        
    );

    export default App;
  ``` 
- 以上我们将Header，Page，Footer模块化，最后在App.js中完成拼装
- Q:CSS 可以（模块化）放进component里吗
  - A: 可以用styled component。

### 2.3 模块化page，解决page过大问题
- 1. 新建`HomePage.js`,将Page中对应的HomePage部分模块化
  ```js
  //HomePage.js
    import React from 'react';

    const HomePage = () => (
        <div id="HOME" class="page page--active">
        <div class="page__header homepage__header">
        <image class="homepage__avatar" src="./assets/avatar.png" alt="Avatar" />
        <div class="homepage__title">
            <h2 class="homepage__name">Tifa Lockhart</h2>
            <div class="homepage__position">Final Fantasy VII</div>
            <div class="homepage__socialMedias">
            <i class="fab fa-twitter homepage__socialMediaItem"></i>
            <i class="fab fa-facebook-f homepage__socialMediaItem"></i>
            <i class="fab fa-instagram homepage__socialMediaItem"></i>
            </div>
        </div>
        </div>
        <div class="page__content homepage__content">
        <div>
            <h3 class="homepage__aboutMeHeader">
            About
            <span class="homepage__aboutMeHeaderHighlight">Me</span>
            </h3>
            <div class="homepage__aboutMeContent">
            Bright and optimistic, Tifa always cheers up the others when they're down. But don't let her looks fool you, she can decimate almost any enemy with her fists...
            </div>
        </div>
        <table class="homepage__contact">
            <tr>
            <td>Age</td>
            <td>20</td>
            </tr>
            <tr>
            <td>Residence</td>
            <td>Gaia</td>
            </tr>
            <tr>
            <td>Address</td>
            <td>Level 3 / 57 Coronation Drive, Brisbane</td>
            </tr>
            <tr>
            <td>Email</td>
            <td>
                <a href="mailto:info@jiangren.com.au">
                info@jiangren.com.au
                </a>
            </td>
            </tr>
            <tr>
            <td>Phone</td>
            <td>+0123 123 456 789</td>
            </tr>
        </table>
        </div>
    </div>
    );

    export default HomePage;
  ``` 
- 2. 新建`ResumePage.js`，将Page中对应的ResumePage部分模块化
  ```js
  //ResumePage.js
    import React from 'react';

    const ResumePage = () => (
        <div id="RESUME" class="page">
        <div class="page__header">
            <h2 class="page__title">RESUME</h2>
        </div>
        <div class="page__content">
            <div class="resumePage__sub">
            <div>
                <h3 class="resumeSub__title">Education</h3>
                <div class="timelines">
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>  
                </div>
            </div>
            <div>
                <h3 class="resumeSub__title">Experience</h3>
                <div class="timelines">
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>
                <div class="timeline">
                    <h4 class="experience__title">Specialization Course</h4>
                    <div class="experience__meta">
                    <span class="experience__year">2010</span>
                    &nbsp;
                    <i class="experience__divider"></i>
                    &nbsp;
                    <spans class="experience__company">Apple Inc.</spans>
                    </div>
                    <div class="experience__description">
                    Mauris magna sapien, pharetra consectetur fringilla vitae, interdum sed tortor.
                    </div>
                </div>  
                </div>
            </div>
            </div>
            <div class="resumePage__sub">
            <div>
                <h3 class="resumeSub__title">Design <span class="resumeSub__titleHighlight">Skills</span></h3>
                <div class="skill">
                <h4 class="skill__title">Web Design</h4>
                <div class="skill__level skill__level--webDesign"></div>
                </div>
                <div class="skill">
                <h4 class="skill__title">Graphic Design</h4>
                <div class="skill__level skill__level--graphicDesign"></div>
                </div>
                <div class="skill">
                <h4 class="skill__title">Print Design</h4>
                <div class="skill__level skill__level--printDesign"></div>
                </div>
            </div>
            <div>
                <h3 class="resumeSub__title">Coding <span class="resumeSub__titleHighlight">Skills</span></h3>
                <div class="skill">
                <h4 class="skill__title">HTML Design</h4>
                <div class="skill__level skill__level--htmlDesign"></div>
                </div>
                <div class="skill">
                <h4 class="skill__title">CSS Design</h4>
                <div class="skill__level skill__level--cssDesign"></div>
                </div>
                <div class="skill">
                <h4 class="skill__title">JavaScript Design</h4>
                <div class="skill__level skill__level--jsDesign"></div>
                </div>
            </div>
            </div>
        </div>
        </div>
    );

    export default ResumePage;
  ``` 
- 3. 新建`Services.js`，将Page中对应的Services部分模块化
  ```js
  //Service.js
    import React from 'react';

    const Services = () => (
        <div id="SERVICES" class="page">
        <div class="page__header">
        <h2 class="page__title">Services</h2>
        </div>
        <div class="page__content">
        <div class="servicesPage__services">
            <h3 class="services__title">
            My
            <span class="services__titleHightLight">Services</span>
            </h3>
            <div class="services">
            <div class="serviceItem">
                <div class="serviceItem__imageContainer">
                <img alt="HTML5" src="./assets/html5.png" class="serviceItem__image"></img>
                </div>
                <h4 class="serviceItem__name">HTML5</h4>
                <div class="serviceItem__description">Hypertext Markup Language (HTML) is the standard markup language for documents designed to be displayed in a web browser.</div>
            </div>
            <div class="serviceItem">
                <div class="serviceItem__imageContainer">
                <img alt="CSS3" src="./assets/css3.png" class="serviceItem__image"></img>
                </div>
                <h4 class="serviceItem__name">CSS3</h4>
                <div class="serviceItem__description">Cascading Style Sheets (CSS) is a style sheet language used for describing the presentation of a document written in a markup language like HTML.</div>
            </div>
            <div class="serviceItem">
                <div class="serviceItem__imageContainer">
                <img alt="JavaScript" src="./assets/js.png" class="serviceItem__image"></img>
                </div>
                <h4 class="serviceItem__name">JavaScript</h4>
                <div class="serviceItem__description">JavaScript often abbreviated as JS, is a programming language that conforms to the ECMAScript specification.</div>
            </div>
            </div>
        </div>
        <div class="servicesPage__clients">
            <h3 class="services__title">
            Clients
            </h3>
            <div class="clients">
            <img alt="REA Group" src="./assets/rea.png" class="clientItem"></img>
            <img alt="carsales.com.au" src="./assets/carsales.svg" class="clientItem"></img>
            <img alt="Seek" src="./assets/seek.png" class="clientItem"></img>
            </div>
        </div>
        </div>
    </div>
    );

    export default Services;
  ```  
- 4. 更新`Page.js`
  ```js
  //Page.js
    import React from 'react';
    import HomePage from './HomePage';
    import ResumePage from './ResumePage';
    import Services from './Services';

    const Page = () => (
        <div class="pages">
        <HomePage />
        <ResumePage />
        <Services />
        <div id="BLOG" class="page"></div>
        <div id="CONTACT" class="page"></div>
    </div>
    );

    export default Page;
  ``` 

### 2.4 react中，import与export的对应关系
- Q:为什么每次需要export default，这个default代表什么？假如一个页面 有多个 function component，是不是可以分开export
  - A: import 与 export default 一一对应，即`App.js`中的`import Header from './app/Header';`对应了`Header.js`中的`export default Header;`；如果`Header.js`中存在多个`const`，那只有`export default`后面跟的才是对应`import`导入到`App.js`中的。
- Q:import的名字 不需要一致吗
  - A:`import` 不管后面跟什么名字，导入的都是`export default`后面跟的，因此不需要一一对应
  - 如果一个export文件中存在多个希望导出的html，则可以在此const前加入export，如
  ```js
  export const Logo = ()...
  export const Header = ()...
  ``` 
  同样的，此时`App.js`中，import语句将变为
  ```js
  import all from './app/Header'
  ```
  同时还需要跟着
  ```js
  const {Logo, Header} = all;
  ```
  或者将以上两行代码整合为
  ```js 
  import {Logo, Header} from './app/Header'
  ```
- Q: 那能不能 用js自带的 module.export?
  - A: JS的模块化分为 ESModule 和 CommonJS
  - ESModule为ECMA提出的模块化标准
    ```js
    //App.js
    const  App = () => (<div />);
    export default App;
    //main.js
    import React from 'react';
    import App from './App';
    ``` 
  - CommonJS为JS自带的模块化标准
    ```js
    //App.js
    const App = () => (<div />);
    module.export = App;
    //main.js
    const React = require('react');
    cosnt App = require('./App');
    ```
    - 他们两个的区别除了使用方法不同外，还有加载方式不同：esModule是编译的时候运行，commonJS是被加载的时候运行；nodejs虽然原生支持commonJS，但绝大多数浏览器现在并不支持commonJS，所以在前端应用中，我们通常应用 ESModule
- arrow function中
  ```js
  export const Header = () => (

  );
  ```
  第一个`()`为传参,第二个`()`为单行return省略出的括号，等效于
  ```js
  export const Header = () => {
      return (
      );
  }
  ```


### 2.5 CSS的模块化
为实现JS中直接写css
- 1. 新建`Header.css`,并移入相关的CSS内容
  ```css
  //Header.css
  .nav {
    padding: 15px 0;
    display: flex;
    align-items: center;
  }
  
  .nav__left {
    flex: 1;
  }
  
  .logo {
    font-size: 1.5rem;
    font-weight: 500;
  }
  
  .logo__highlight {
    color: #377e9a;
  }
  
  .navbar {
    display: flex;
  }
  
  .navbar__item {
    padding: 16px;
    text-decoration: none;
    color: #49515d;
    font-size: 15px;
    opacity: 0.6;
    display: block;
    transition: opacity 0.3s ease-in-out;
  }
  
  .navbar__item::after {
    content: "";  
    width: 0;
    border-bottom: 3px solid #377e9a;
    margin: auto;
    margin-top: 4px;
    display: block;
    transition: width 0.3s ease-in-out;
  }
  
  .navbar__item--active,
  .navbar__item:hover {
    opacity: 1;
  }
  
  .navbar__item--active::after,
  .navbar__item:hover::after {
    width: 24px;
  }
  
  .navbar__item:last-of-type {
    padding-right: 0;
  }
  
  ``` 
- 2. 更新`index.html`中的引用
  ```html
  <link rel = "stylesheet" href="Header.css">
  ```
- 3. JS中存在就近管理与就近维护（maintenance nearby）原则
  - 在app文件夹下，移入`Header.css`
  - 更新`Header.js`
   ```js
   import './Header.css';
   ```
   但是，html无法直接执行css，因此以上在使用webpack打包时会报错。为解决这个问题，我们将引入css loader与style loader
   - `npm i -D style-loader`
   - `npm i -D css-loader`
      
  通过我们在chrome上inspect可以发现，webpack打包了我们写入jsx中的css，然后直接放到了header里 
- Q:sass不可以吗
  - A:加个 sass loader就可以
- Q:sass 可以直接用吗 还是要map成css才能用
  - A:可以，配个sass loader就可以

以上这样的标准CSS模块化引用方式产生了三个痛点：
- BEM
  - body-element-modifier：每个class都会很长
- 维护两份文件
  - css和html文件都要维护
- 维护class name 的一致性 
   
因此我们会学习styled-components解决这个问题
## 3.使用styled-components
- 1. 安装styled-components 
    `npm i styled-components`
- 2. js文件中导入styled-components，同时更改html中标签的写法  
更新`Header.js`
```js
//Header.js
import React from 'react';
import './Header.css';
import styled from 'styled-components';

const Highlight = styled.span`
    color:#377e9a;
`;

const Logo = styled.div`
    font-size: 1.5rem;
    font-weight:500;
`;

const Nav = styled.div`
    padding: 15px 0;
    display: flex;
    align-items: center;
`;

const Left = styled.div`
    flex: 1;
`;

const Right = styled.div`
`;

const Navbar = styled.div`
    display: flex;
`;

const NavbarItem = styled.a`
    padding: 16px;
    text-decoration: none;
    color: #49515d;
    font-size: 15px;
    opacity: 0.6;
    display: block;
    transition: opacity 0.3s ease-in-out;

    /* SCSS 规范 */
    &::after {
        content: "";  
        width: 0;
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

const Header = () => (
    <Nav>
        <Left>
            <Logo class="logo">
                <Highlight>Tifa</Highlight>
                Lockhart
            </Logo>
        </Left>
        <Right>
            <Navbar>
                <NavbarItem href="HOME">Home</NavbarItem>
                <NavbarItem href="RESUME">Resume</NavbarItem>
                <NavbarItem href="SERVICES">Services</NavbarItem>
                <NavbarItem href="BLOG">Blog</NavbarItem>
                <NavbarItem href="CONTACT">Contact</NavbarItem>
            </Navbar>
        </Right>
  </Nav>
);

export default Header;
    
```
- Q: 为什么有两个单引号?
  - A: 直接调用了styled.div这个方法，其中的argument我们通过es的写法省略了括号，然后我们就通过反引号来声明其中的template string
- Q: styled component的 命名 有什么规范吗？
  - A: 没有什么规范，但是依然要遵循RMR
- Q: 可以导入吗
  - A: style component
- Q: 我也觉得，相当于把css和js代码都写在一起了，乱
  - A: 单看html部分非常清晰，可以自己解释自己了；只是文件长了；所以 component 要切的夠小
  - Styled component要求你在符合rmr的同时写出更好的代码
  - 如果某块styled觉得过长，可以将这个单一职责抽出来
- Q: 那如果navbar 有多个class呢
  - A: 现在已经不叫class，而是我们将之转成了styled component
- Q: 所以一般來說是全都用 styled component 嗎 , 還是也會並用 css/scss
  - A: 三者选其一
- Q: 划分component有什么严格的标准吗
  - A: 并没有；但是可以按责任划分和按复用划分
- Q: 如果多个component都要引用一个相同的style, 是import/export 对应的styled component 还是 重写一遍styled？
  - A: 可以创建一个新的js文件，作为可以复用的component，导入到其它使用他的地方
- Q: 那除了flex还有其他style咋办
  - A: 可以将flex作为参数，传入一个styled里
- Q: bootstrap之类的架构怎么用styled components
  - A: 一个足够好的架构，天生支持styled components
- Q: 所有component都是js结尾的文件我不知道在哪找stylecomponent怎么办
  - A: vs code中使用 ctrl + p/cmd + p 来检索文件

### 4.课间Q&A
- Q: styled都抽出来，会不会导致component文件过多
  - A: facebook的react，有上万个component
- Q: 老师 qantas招mid level以下的职位吗
  - A: 新项目组里因为快速搭建，不会招；老的项目，处于维护阶段的项目会招
- Q: 因为我在网上搜了以下好多职位都是招senior
  - A: senior难招，junior好招
- Q: senior 主要是靠经验么
  - A: 中国的所有程序员都是技术型程序员，狼性社会；澳洲是分拼技术的，和熬资历的程序员，羊性社会
- Q: 想问龙哥 1年熬到senior都做了啥
  - A: 平均一个月带出来一个项目
- Q: 所以年資高 技術不到位, 薪水也會高？
  - A: 澳洲，技术占70%，经验/资历占30%
- Q: it入职之后  都是要来回跳槽吗
  - A: 看公司，如果上升通道，环境都好可以不跳，但是澳洲，想要涨工资，跳槽是最快的
- Q: 龙哥工作之外有什么爱好呀,同事会时不时组织聚餐出去浪啥的么
  - A: 带娃；最怕长假回来，同事一定会问how's your holidays；或者周五去bar聊天
- Q:老师你能讲讲你以前pwc的实习申请面试经验吗
  - A: 跟高考难度差不多，刷题库，考试，再面试；所以没有什么面试经验
- Q: 是聽說在澳洲工作 溝通技巧很重要
  - A: 澳洲办公室政治也蛮严重
- Q: Qantas 有PR的要求吗
  - A: 只要你有working rights，他就不会很在乎；当然，堪培拉除外
- Q: Qantas喜欢找什么样的junior？
  - A: 看Job Description
- Q:aws是从官方那个文档看么
  - A: 学一个东西，官方文档一定是最正确的途径

## 5.项目文件结构化
在我们把各种styled抽出去后，`Header.js`只有几十行了，非常易读。  
抽出的components都放在一个文件夹里，非常不易读。

这时候我们想到就近原则，把components划分为两类
- 复用
  - 比如Flex，Highlight
  - 我们可以把这类放到components文件夹下面
- 责任
  - 比如Header，Footer，Page这种组成页面必不可少的
  - 我们可以把这类直接放在app文件夹下面

### 5.1 依据RMR原则，重构app下的文件结构
- 如果我们要维护NavbarItem,我们可以按照以下结构来管理文件
  - Header
    - components
      - `Navbaritem.js`
    - `Header.js` 
  - Footer
  - Page
- 并没有什么万金油的框架可以让我们来自动命名文件结构，但是上面tree-view的文件结构就是业界共识
- 我们可以在vs code里用
  - cmd + P （mac）
  - ctrl + P （windows）
  - 敲入文件名，来检索想要的文件

### 5.2 更新import, 引入index
对于 NavbarItem文件下的NavbarItem.js, 如果我们不想看到像  
`import NavbarItem from './components/NavbarItem/NavbarItem';`  
这样的重复引用，想变成下面这样    
`import NavbarItem from './components/NavbarItem';`  
那其实上面的语句，我们导入的是NavbarItem下的index.js,  
因此我们可以通过在NavbarItem文件夹下创建`index.js`来转发NavbarItem
```js
//index.js
export {default} from './NavbarItem';
```
上面的一行代码，几乎可以理解为下面两行代码的简写：
```js
import NavbarItem from './NavbarItem';
export default NavbarItem;
```
> 在计算机语言里面，当你去索引/指向 文件夹的时候，默认 索引/指向 index文件
 
如果`NavbarItem.js`里又定义了其他export，例如
```js
export const A = 'A';
```
index中想导入所有的NavbarItem里的export，则变为
```js
//index.js
export {default, A} from './NavbarItem';
```
- Q: 那navbatitem文件里要有多个文件呢？所有非index的文件都可以写在{ }里？
  - A: 是的

假如我们的NavbarItem文件夹下有两个文件，文件结构如下
- Header
  - components
    - NavbarItem
      - `index.js`
      - `NavbarItem.js`
      - `Link.js`
  - `Header.js`  
  
我们想将Link的export也加入到index里，那么在NavbarItem里的index可以这么写
```js
//index.js
export { default } from './NavbarItem';
export { default as Link } from './Link';
```
而在`Header.js`中的导入则变为了
```js
import NavbarItem, { Link } from './components/NavbarItem';
```

### 5.3 从maintainable角度看，为什么一定要引入index
> 代码只写一次，但是会被调用n次，会被阅览n+1次
- 虽然我们写了`index.js`，  
 `import NavbarItem from './components/NavbarItem';`中，仅仅避免了少写一次NavbarItem，但是别人调用的时候也会少写一次NavbarItem。如果你的代码被调用10000次，就节省了别人少些10000个NavbarItem的时间
- 面试官问你，rmr中，你认为什么是一段好的maintainable代码呢，你可以按照思路`代码只写一次，但是会被调用n次，会被阅览n+1次`来答，为了让后续调用和阅览的人舒服，虽然会cost我一点时间，但是可以节省别人n+1次时间
- ES6中有更好的写法
```js
export { default } from './Logo';
```
代替了
```js
import Logo from './Logo';
export default Logo;
```

### 5.4 命名学！！！很重要

### 5.5 文件结构
- /src/components 里面放components
- /src/components/Header 下还可以放components和helpers文件夹。更加readable，维护原则