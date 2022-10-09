## 01 将代码改造成模块化的React
组件划分力度，多小的组件是一个合格的组件呢？

什么是component based：
- 一个函数返回的JSX代码片段，单一职责的
> 补充：一个React的项目，除了index.js作为入口为html，就不应该再出现其它的html了
- 重要的语法
  - 在JSX中，如果statement，以<开头，那么在相应的>之前的内容会被当做markup来处理，以{开头，那么在相应的}之前的内容会被当做js来处理
- 申明式写出来的的代码，大家写出来的代码应该是相同的。这是规范化的好处
> 补充：`((App /)`中，第二层括号能不能省略 ? 
> `()`在JS中是不做任何作用的，可以省略。但是加了更readable一些。

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
		        // 就近维护原则 这里的class名应该叫items 而不是nav_item
                <a class="item" href="HOME">Home</a>
                <a class="item" href="RESUME">Resume</a>
                <a class="tem" href="SERVICES">Services</a>
                <a class="item" href="BLOG">Blog</a>
                <a class="item" href="CONTACT">Contact</a>
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
            
    export default App;
  ```

