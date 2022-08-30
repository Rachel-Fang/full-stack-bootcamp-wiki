# Class-16 React-3
(本节代码较多，可跳过部分代码阅读)
## 主要知识点
  - [1.课前答疑，及上节课回顾](#1课前答疑及上节课回顾)
    - [1.1 什么是一个好的component](#11-什么是一个好的component)
    - [1.2 两种程序员](#12-两种程序员)
    - [1.3 styled-components](#13-styled-components)
    - [1.4 学习阶段不要经常call api](#14-学习阶段不要经常call-api)
    - [1.5 问题答疑](#15-问题答疑)
    - [1.6 解决jsx中的warning代码块](#16-解决jsx中的warning代码块)
    - [1.7 解决频繁 run build](#17-解决频繁-run-build)
  - [2.如何用JSX实现分页渲染：页面渲染的声明式写法](#2如何用jsx实现分页渲染页面渲染的声明式写法)
  - [3.改造以上写法中的if-else](#3-改造以上写法中的if-else)
    - [3.1 回顾js中的key-value map,改造if-else](#31-回顾js中的key-value-map改造if-else)
    - [3.2 改造if-else, jsx中我们更常见的写法](#32-改造if-else-jsx中我们更常见的写法)
    - [3.3 课间提问](#33-课间提问)
  - [4.引入变量page，使header active与当前页面渲染一致](#4-引入变量page使header-active与当前页面渲染一致)
    - [4.1 复习模板字符串](#41-复习模板字符串)
  - [5.props值传递](#5props值传递)
    - [5.1 map映射](#51-map映射)
    - [5.2 props值传递的实现原理](#52-props值传递的实现原理)
    - [5.3 props值传递的实现步骤](#53-props值传递的实现步骤)
    - [5.4 props值传递的总结](#54-props值传递的总结)


# 课堂笔记

## 1.课前答疑，及上节课回顾
### 1.1 什么是一个好的component
- Q:什么是一个好的component，什么是一个好的component划分界限
  
面试时，谈到react好处，可能会按照下面思路谈下去->declarative，component based->component based->什么是一个好的component  
谈到什么是一个好的component的时候，谈solid不一定是个好的答案，因为可能会把话题往solid转  
正确方向可以是
- readable：以前一个300多行的html，被划分成了几个文件，原来的html仅变成了10几行非常易读，易维护
- reusable
- maintainable

### 1.2 两种程序员
程序员分两种，码畜和码农。希望大家做码农，而不是码畜：  
码畜 VS 码农
- 码畜：机械重复的写代码，看到别人写就写
- 码农：像农民一样，努力的呵护自己的庄稼，写完代码后，去反思，是否足够好，有没有可改进的空间，有没有可学习的空间

### 1.3 styled-components
styled-components：
让样式也成为components，让样式也获得可复用性地提升

### 1.4 学习阶段不要经常call api
作为前端开发，我们应该目标远大，而不是只把自己变成一个API Caller。

### 1.5 问题答疑
- Q: 老师 styled-components能对bootstrap原生css进行更改吗
    - A:除非你在工作中遇到了这样的项目，身为一个好的程序员不要把自己往低的地方拉，而是往好的地方看，弄清原理，自己写
- Q:怎么在react中用font-awesome
  - A: google，会发现font-awesome早已将变成了react official component，所以可以像component一样用font-awesome
- Q:工作中styled components一般和jsx写在同一个文件里吗？
  - A: 是的
  - Q: 你写jsx的时候，希望跟styled component写在一个同文件里面
    - A:RMR
- Q:那假如说一个项目有主题颜色,可能包含两三种颜色,我如果想复用这些颜色的话是应该单独把颜色的css写成一个组建么?还是有办法弄个什么全局变量可以所有组件调用?
  - A: 后几节课会讲，这个东西叫 theming，可以google theming styled components自学一下
- Q:好的前端应该尽量避免使用架构吗？这个度该怎么把握，例如珊格系统是该自己重新实现还是用架构
  - A:好的前端是全程手写的，因为所有东西都在自己手写范围里，但是这样cost是很高的。对于度，自己去把握，调用api，成本低，可交付快。好的前端在不考虑其它因素的情况下，要尽量少用别人写好的东西，“授人鱼不如授人以渔”，调用api，永远是在吃别人嚼过的东西。好的程序员，尽量少调用库。
    - Q:但是我写的就是不如别人好怎么办
      - A:班上永远有比你学习好的同学，你会直接去抄他答案吗？

### 1.6 解决jsx中的warning代码块
React在编译的同时会检查你的html错误，同时会对html中的`class`这一写法疯狂warning, 这是因为jsx有些html attribute 与原生 html attribute不同，例如
- class -> className
- for -> htmlFor  
  
为什么这两个会被改名，而`href`,`id`等没有，是因为`class`,`for`都是js关键字, 因此我们也极力避免以上情况。

jsx里的html都是经过js编译的，html又是一个忍耐性非常强的语言，哪怕你在html里瞎写，他也会努力帮你实现；但是jsx是一个很picky的语言，遇到问题就会给你提出来

### 1.7 解决频繁 run build
每次修改完成，我们都要`npm run build`一下，才能跑
- 程序语言发展到现在，应该不会有地方让你感觉不舒服，但是这里为什么每一次要这么麻烦，所以你要学会google
- webpack-dev-server，或者装plugin

## 2.如何用JSX实现分页渲染：页面渲染的声明式写法
实现切换页面，我们最常用到的是className，但是这个方法的弊端是没有被展现的page其实已经被渲染出来了。
- 事出反常必有妖：但是这样会占用浏览器资源
>什么是一个好的网站，在不影响功能的情况下，渲染出来的elements越少越好  

现在我们已经可以在jsx直接写html了
- 1. 更新Page.js，加入if
  ```js
  //Page.js
    import React from 'react';
    import HomePage from './components/HomePage';
    import ResumePage from './components/ResumePage';
    import Services from './components/Services';

    const page = 'RESUME';

    const Page = () => {
    if (page === 'HOME'){
        return (
        <div className="pages">
            <HomePage />
        </div>
        );
    }
    if (page === 'RESUME'){
        return (
        <div className="pages">
            <ResumePage />
        </div>
        );
    }
    if (page === 'SERVICES'){
        return (
        <div className="pages">
            <Services />
        </div>
        );
    }
    if (page === 'BLOG'){
        return (
        <div className="pages">
            <div id="BLOG" className="page"></div>
        </div>
        );
    }
    if (page === 'CONTACT'){
        return (
        <div className="pages">
            <div id="CONTACT" className="page"></div>
        </div>
        );
    }

    }

    export default Page;
  ```
- 2. 更新HomePage.js, main.css
  ```js
  //HomePage.js
    import React from 'react';

    const HomePage = () => (
        <div id="HOME" className="page">
        <div className="page__header homepage__header">
        <img className="homepage__avatar" src="./assets/avatar.png" alt="Avatar" />
        <div className="homepage__title">
            <h2 className="homepage__name">Tifa Lockhart</h2>
            <div className="homepage__position">Final Fantasy VII</div>
            <div className="homepage__socialMedias">
            <i className="fab fa-twitter homepage__socialMediaItem"></i>
            <i className="fab fa-facebook-f homepage__socialMediaItem"></i>
            <i className="fab fa-instagram homepage__socialMediaItem"></i>
            </div>
        </div>
        </div>
        <div className="page__content homepage__content">
        <div>
            <h3 className="homepage__aboutMeHeader">
            About
            <span className="homepage__aboutMeHeaderHighlight">Me</span>
            </h3>
            <div className="homepage__aboutMeContent">
            Bright and optimistic, Tifa always cheers up the others when they're down. But don't let her looks fool you, she can decimate almost any enemy with her fists...
            </div>
        </div>
        <table className="homepage__contact">
            <tbody>
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
            </tbody>
        </table>
        </div>
    </div>
    );

    export default HomePage;
  ```
  ```js
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
        display: block;
        position: relative;
        visibility: visible;
        opacity: 1;

        border-radius: 16px;
        background: white;
        transition: visibility 0.3s, opacity 0.3s ease-in-out;
        box-shadow: 0px 15px 25px 0px rgba(0,0,0,0.1);
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
这时候我们发现，只要我们在`Page.js`中，更改page的值，就会分别渲染不同的页面
```js
    //渲染为home page
    const page = 'HOME';
```
```js
    //渲染为resume page
    const page = 'RESUME';
```
这种按需求渲染的写法，就叫声明式写法；告诉page，在什么情况下渲染成什么page

## 3. 改造以上写法中的if-else
但是看到if，就要扇自己两巴掌；扇完以后，我们就要改造上面的if

### 3.1 回顾js中的key-value map,改造if-else
```js
const student = {
    name: 'LONG',
    age: 29,
};

const myAge = student.age;//29
const myAge = student['age'];//29

const key = 'age';
const myAge = student[key];//29
```
JS中直接写HTML，就变成了JSX

Q：jsx中可以插入JS片段吗
- 可以，
> 在JSX里，所有`<>`包起来的都被认为是html

> 在JSX里，所有`{}`包起来的都被认为是js
  
因此改掉page里的if-else：
```js
//Page.js
import React from 'react';
import HomePage from './components/HomePage';
import ResumePage from './components/ResumePage';
import Services from './components/Services';

const page = 'HOME';

const Page = () => {
  //key,value map
  //javascript variable
  const currentPage = {
    HOME: (<HomePage />),
    RESUME: (<ResumePage />),
    SERVICES: (<Services />),
    BLOG: (<div id="BLOG" className="page"></div>),
    CONTACT: (<div id="CONTACT" className="page"></div>),
  }[page];

  return (
    <div className = "pages">
      { currentPage }
    </div>
  )
}

export default Page;

```
### 3.2 改造if-else, jsx中我们更常见的写法
虽然上面的代码量是最小的，但是在jsx中，我们并不想看到一个东西up and down，上面的写法在工作中，我们更常见的写法是：
```js
//Page.js
import React from 'react';
import HomePage from './components/HomePage';
import ResumePage from './components/ResumePage';
import Services from './components/Services';

const page = 'HOME';

const Page = () => {
  return (
    <div className = "pages">
      { page === 'HOME' && (<HomePage />) }
      { page === 'RESUME' && (<ResumePage />) }
      { page === 'SERVICES' && (<Services />) }
      { page === 'CONTACT' && (<div id="CONTACT" className="page">CONTACT</div>) }
      { page === 'BLOG' && (<div id="BLOG" className="page">BLOG</div>) }
    </div>
  )
}

export default Page;
```
### 3.3 课间提问
- Q:龙哥嫂子也是程序媛吗2333
  - A:不是。之前她想做P1的网站，用了wordpress
- Q:龙哥,只有react是组件式的前端开发么
  - A:不是，所有能火起来的前端开发，一定是组件式的。组件式一定是大潮流。一定是declarative和component-based
- Q:组件 怎么能够准确，我用HTML +CSS 都会这里多一块，格式控制不好；就是格式不准确，比如多一点。
  - A:CSS一定是基本功，如果是padding，margin少一点，这种问题可以不用关心；但是position absolute，relative，要不要用position，还是用flex，这种问题一定要清楚
- Q:龙哥现在大公司都上云是不是?
  - A:是，小公司也上云，你们P2都上云
- Q:需要考证吗?
  - A:前端不需要，DevOps可以需要
- Q:前端框架进化淘汰频繁吗
  - A:相对于后端，一定是频繁的；前端程序员一定是比后端程序员学的多一些，但是不等于说后端程序员不用学习。前端为什么更新快，是因为人的审美变化快，前端项目迭代快，前端永远可以不停尝试新技术。
- Q:转行的，在澳洲学这个能吃一辈子不。。。
  - A:这个不好答...但是今年来问，学it还是会计，还是it；学it还是金融，如果想赚的多，还是学金融；所以特定问题，特定分析
- Q:啊我一直以为前端经常被后端鄙视的
  - A:后端心理不服气
- Q:但是国内后端比前端赚得多
  - A:现在在it行业，工资最高的是data miner，数据分析类；然后是devops；再其次是前端；垫底的是后端。比如阿里的P7，纯前端可以拿到120~140W的package，纯后端的可能拿不到100W
  - 市场Average情况下，程序员工资：6w5 -> 22w5：Jnr -> Mid -> Snr -> Principle
  - 想看salary的推荐glassdoor去看看,linkedin也可以，但是澳洲Linkedin上写的工资是偏低的，
- Q: 从junior到mid需要多久
  - A: 龙哥的经历：
    - 2016 -> 2021:Jnr -> Principle: 4w -> 20w
    - 从Jnr到Mid用了半年，7个月的时间，前提是看你多努力
- Q:这个 junior  mid senior  title 是自然晋升的  还是跳槽 换title的？
  - A: 如果你认为自己达到了mid，可以跟你的领导谈，问他review下你的title；或者你可以跳槽到别的公司做mid
- Q: 报Salary expectation多少合适
  - A:对于我们现在的学生，报7W5是没错的
  - Q:对方会砍价吗
    - A:砍价的很少见
  - Q:这个salary offer前 一定会问吗
    - A：一般都会问

## 4. 引入变量page，使header active与当前页面渲染一致
jsx内的falsy值不会被渲染出来：
- false，null，undefined，[]（空array）
- {} （空object）不会被接受
- 0会被渲染出来
- {true}是不是也出不来：true也不会被渲染出来

为了达到Header中的标签与page渲染的页面一致：
- 1. 从新写回css
```css
//NavbarItem.css
.navbarItem {
    padding: 16px;
    text-decoration: none;
    color: #49515d;
    font-size: 15px;
    opacity: 0.6;
    display: block;
    transition: opacity 0.3s ease-in-out;
}
  
.navbarItem::after {
    content: "";  
    width: 0;
    border-bottom: 3px solid #377e9a;
    margin: auto;
    margin-top: 4px;
    display: block;
    transition: width 0.3s ease-in-out;
}
  
.navbarItem--active,
.navbarItem:hover {
    opacity: 1;
}
  
.navbarItem--active::after,
.navbarItem:hover::after {
    width: 24px;
}
  
.navbarItem:last-of-type {
    padding-right: 0;
}
``` 
- 2. 改写`Header.js`
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


const Header = () => (
    <Nav>
        <Left>
            <Logo>
                <Highlight>Tifa</Highlight>
                Lockhart
            </Logo>
        </Left>
        <Right>
            <Flex>
                <a className = "navbarItem navbarItem--active" href="HOME">Home</a>
                <a className = "navbarItem" href="RESUME">Resume</a>
                <a className = "navbarItem" href="SERVICES">Services</a>
                <a className = "navbarItem" href="BLOG">Blog</a>
                <a className = "navbarItem" href="CONTACT">Contact</a>
            </Flex>
        </Right>
  </Nav>
);

export default Header;

```
- 3.继续修改`Header.js`，引入page变量
  
反引号不能省略，是字符串，是在a中的jsx中的html字符中的js
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
                <a className = {`navbarItem ${page === 'HOME' && 'navbarItem--active'}`} href="HOME">Home</a>
                <a className = {`navbarItem ${page === 'RESUME' && 'navbarItem--active'}`} href="RESUME">Resume</a>
                <a className = {`navbarItem ${page === 'SERVICES' && 'navbarItem--active'}`} href="SERVICES">Services</a>
                <a className = {`navbarItem ${page === 'BLOG' && 'navbarItem--active'}`} href="BLOG">Blog</a>
                <a className = {`navbarItem ${page === 'CONTACT' && 'navbarItem--active'}`} href="CONTACT">Contact</a>
            </Flex>
        </Right>
  </Nav>
   );
}

export default Header;
```
- 4.进一步引入getNavBarItemClassName
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
        { key: 'HOME', value: 'Home' }，
        { key: 'RESUME', value: 'Resume' }，
        { key: 'SERVICES', value: 'Services' }，
        { key: 'BLOG', value: 'Blog' }，
        { key: 'CONTACT', value: 'Contact' }
    ]

    const getNavBarItemClassName = (key) =>  `navbarItem ${page === key && 'navbarItem--active'}`;
    

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
                <a className = {getNavBarItemClassName('HOME')} href="HOME">Home</a>
                <a className = {getNavBarItemClassName('RESUME')} href="RESUME">Resume</a>
                <a className = {getNavBarItemClassName('SERVICES')} href="SERVICES">Services</a>
                <a className = {getNavBarItemClassName('BLOG')} href="BLOG">Blog</a>
                <a className = {getNavBarItemClassName('CONTACT')} href="CONTACT">Contact</a>
            </Flex>
        </Right>
  </Nav>
   );
}

export default Header;
``` 

- Q: 插一句哈，我看prettier自动格式是全改成双引号，不过看龙哥这里是js单引号，html部分双引号？
  - A: 首先我们在jsx里写的是html片段，在html原生的attribute写的是双引号，这就是我们在jsx里html部分写的都是双引号的原因。在js中，遇到string，我们采用单或者双引号是取决于这个项目要求。现在jsx的书写规范，单引号要多于双引号。只要保证项目内部一致性就好，html里只要是值永远都是双引号。

### 4.1 复习模板字符串
```js
const name = 'Long Zhao';
const age = 29;

const s = 'my name is ' + name + ', ' + age + ' years old.';
```
以上最后一句，用模板字符串可以写成
```js
const s = `my name is ${name}, ${age} years old.`;
```
即变量可以用${}包裹起来，直接传入字符串中

- 5.从第4步继续，因此Header可进一步简化为：
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
        { key: 'CONTACT', value: 'Contact' },
    ]

    const getNavBarItemClassName = (key) =>  `navbarItem ${page === key && 'navbarItem--active'}`;
    

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
                <a className = {getNavBarItemClassName(navbarItem.key)} href = {navbarItem.value} >
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

- Q: 老师 ·navbarItem ${false}· 这样输出的class会不会变成  narbarItem false
  - A: 是的
- Q: 我觉得刚才用模版字符串一句话挺方便的，真实工作中有必要这么先搞两个函数么？
  - A: 工作中代码是不需要两个const的,刚刚的两个const是教学需要，因此Header的最后优化版为
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

## 5.props值传递
### 5.1 map映射
  map 使一个array经过一个处理，获得一个新的array，即  
  array -> map(映射) -> 新array  
  例如  
  ```js
  ['鸡肉','蘑菇'] -> map(切菜) -> ['切好的鸡肉','切好的蘑菇'] 
  const 切菜 = （菜） => '切好的${菜}'
  ```
  map, reduce, filter是映射的三个高级用法

### 5.2 props值传递的实现原理
  `Header.js`中 `page = 'HOME'`  
  `Page.js`中 `page = 'HOME'`  
  两个组件中，对应的page应该是同一个值，这种情况类似于
  ```js
  const a = () => {
      b();
      c();
  }

  const b = () => {
      const s = 'ABC';
  }

  const c = () => {
      const s = 'ABC';
  }
  ```
  其中，b(),c()中的s永远是相等的  
  如果我们想让b(),c()中的s永远保持一致，原理上应该这么做
  ```js
  const a = () = {
      const s = 'ABC';

      b(s);
      c(s);
  }

  const b = (s) => {

  }

  const c = (s) => {
      
  }
  ```
  遇到可复用的值，我们通常是先提出去，再传进来

### 5.3 props值传递的实现步骤
  - 1. 更改App.js，定义page,并传递arg
```js
//App.js
import React from 'react';
import Header from './app/Header';
import Page from './app/Page';
import Footer from './app/Footer';

const App = () => {
    const page = 'HOME';

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

html attribute是一个key，value的形式  
在这里, className = main，attrib中，key = arg， value = page，  
说到key，value，就容易让我们想到object{}，因此我们可以在Page.js中进行解构，这种在component中传参的方式叫做props

  - 2. 更改Page.js, 接收page
```js
//Page.js
import React from 'react';
import HomePage from './components/HomePage';
import ResumePage from './components/ResumePage';
import Services from './components/Services';

const page = 'HOME';

const Page = ({
  arg,
  }) => (
    <div className = "pages">
      { arg === 'HOME' && (<HomePage />) }
      { arg === 'RESUME' && (<ResumePage />) }
      { arg === 'SERVICES' && (<Services />) }
      { arg === 'CONTACT' && (<div id="CONTACT" className="page">CONTACT</div>) }
      { arg === 'BLOG' && (<div id="BLOG" className="page">BLOG</div>) }
    </div>
  );


export default Page;
```
进一步简化后，可写为
```js
//Page.js
import React from 'react';
import HomePage from './components/HomePage';
import ResumePage from './components/ResumePage';
import Services from './components/Services';

const page = 'HOME';

const Page = (props) => {
  const { arg } = props;
  
  return(
    <div className = "pages">
      { arg === 'HOME' && (<HomePage />) }
      { arg === 'RESUME' && (<ResumePage />) }
      { arg === 'SERVICES' && (<Services />) }
      { arg === 'CONTACT' && (<div id="CONTACT" className="page">CONTACT</div>) }
      { arg === 'BLOG' && (<div id="BLOG" className="page">BLOG</div>) }
    </div>
  );
}

export default Page;
```

### 5.4 props值传递的总结
props传参：传递一个object（把所有attributes作为一个object，叫做props），component拿到props后，通过解构，可以拿到里面相应的东西，例如
`App.js`中这样定义了props：
```js
<Page foo = "bar" name = "Long Zhao"/>
```
则在`Page.js`中，我们可以这样调用
```js
props.foo
props.name
```
最后可以对Page.js做进一步简化：
```js
//Page.js
import React from 'react';
import HomePage from './components/HomePage';
import ResumePage from './components/ResumePage';
import Services from './components/Services';

const page = 'HOME';

const Page = ({arg,}) => {
  return(
    <div className = "pages">
      { arg === 'HOME' && (<HomePage />) }
      { arg === 'RESUME' && (<ResumePage />) }
      { arg === 'SERVICES' && (<Services />) }
      { arg === 'CONTACT' && (<div id="CONTACT" className="page">CONTACT</div>) }
      { arg === 'BLOG' && (<div id="BLOG" className="page">BLOG</div>) }
    </div>
  );
}

export default Page;

```
需要注意的是，`App.js`中的`arg`，即传递的参数atrribute名，需要与`Page.js`中的解构变量名`arg`一致

- Q: 好奇问一下，这里props是从上层组件往下面传递，请问有没有可能，能从下面组件往上传递？
  - A: 可以，后面会将，但不是你想象中的那种可以
  - React的简单理解——某个组件就是个基于state和props的函数，state是自己的，props是外来的，他们俩不管谁变了就重新渲染一遍

- Q:前端是不是不需要学习很多aws
  - A:作为Junior不需要太多
- Q:怎么能变得跟老师一样厉害？
  - A: (龙哥自谦)技术上理解还是比较浅的，但是很理解澳洲的文化，会把他跟中国文化做一个结合，结合中国文化的长处，比如执行力；理解了澳洲的圈子后，发挥了中国文化的优点
  - 澳洲为什么招一个2~3年经验的，因为懒；澳洲人认为一个星期可以完成的，中国人一天就能完成；所以2~3年的经验，你可能几个月就弥补过来，每天哪怕五小时，真的敲代码，对澳洲人来讲 也是作弊的
  - 所以你做为一个Junior去面试，澳洲人会先入为主的代入你实际的代码工作总时长其实不长，从而非常反感你去聊技术；他更关心你，每天磨工8小时你得到了什么锻炼，学到了什么东西