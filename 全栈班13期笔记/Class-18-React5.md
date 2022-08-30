# Class-18 React-5

## 主要知识点
  - [1.针对P1课前答疑](#1针对p1课前答疑)
    - [1.1 State Lifting](#11-state-lifting)
    - [1.2 State Lifting 总结](#12-state-lifting-总结)
      - [1.2.1 父传子](#121-父传子)
      - [1.2.2 平级间传](#122-平级间传)
      - [1.2.3 子传父](#123-子传父)
  - [2.面试经验share by Darcy](#2面试经验share-by-darcy)
    - [2.1 技术面](#21-技术面)
    - [2.2 Behavior面](#22-behavior面)
    - [2.3 Code Test](#23-code-test)
    - [2.4 总结与其它问题](#24-总结与其它问题)
  - [3.P1回顾](#3p1回顾)
  - [4.P2初讲](#4p2初讲)
    - [4.1 对P2的思考](#41-对p2的思考)
      - [4.1.1 回顾怎样使用state](#411-回顾怎样使用state)
      - [4.1.2 目前难点](#412-目前难点)
    - [4.2 React API Caller](#42-react-api-caller)
      - [4.2.1 JS中写入最原始的http call](#421-js中写入最原始的http-call)
      - [4.2.2 回顾JSON](#422-回顾json)
      - [4.2.3 实现在React中调用API](#423-实现在react中调用api)
        - [4.2.3.1 为什么调用了6000次api](#4231-为什么调用了6000次api)
        - [4.2.3.2 React Lifecycle](#4232-react-lifecycle)

# 课堂笔记

## 1.针对P1课前答疑

- Q: 龙哥 react切换页面  是用react router 还是用state 有没有什么区别
    用state 貌似就没法用url 传递参数了
    - A: 现在我们P1用state切页面，好处是不用引入第三方的库，毕竟react原生并不带router，坏处是我们切换页面，url并没有更新。对于P1来讲，不用router也能做，用了也会更好
    - 就切换页面的话，router会更好：https://reactrouter.com/web/guides/quick-start
- Q: 发邮件的功能？
  - A: 不用写的太复杂，推荐用mailto就可以了 
  - a tag 的 mailto
- Q: 对于复杂嵌套的组件，组件间的传值，子传父，或者不在一个分支的两个组件传值怎么做呢
  - A: 有一个比较高级的概念，叫state lifting
   
### 1.1 State Lifting
首先，我们将Header从function component，改为class component：
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

class Header extends React.Component{
    render() {

        const {
            onPageChange,
            page,
        } = this.props;

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
}


export default Header;
``` 
做进一步修改：
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

class Header extends React.Component{
    constructor(props) {
        super(props);

        this.state = {
            page: 'HOME',
        };
    }

    handleItemClick(target) {
        this.setState({
            page: newPage,
        });
    }

    render() {

        const navbarItems = [
            { key: 'HOME', value: 'Home' },
            { key: 'RESUME', value: 'Resume' },
            { key: 'SERVICES', value: 'Services' },
            { key: 'BLOG', value: 'Blog' },
            { key: 'CONTACT', value: 'Contact' }
        ]
    
        const { page } = this.state;
        
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
                  onClick = {() => this.handleItemClick(navbarItem.key)}
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
}


export default Header;
```
### 1.2 State Lifting 总结
最初的时候，是App进来，然后Header和Page是平级，不存在父子关系  
我们希望Header和Page能够传值，这样Header和Page的值能统一
#### 1.2.1 父传子
父传子，用props
#### 1.2.2 平级间传
平级间怎么传，用state lifting
- 我们状态提升到 同级或者不同级 的组件的最小共用组件内，然后作为props向下传递
- 比如上面我们的组件结构如下
```
- App
    - Header {page}
        - Navigation
    - Page
```
- Header中的page这个prop，如果我们想通过state lifting做到全局统一，我们可以把page提到App里，然后通过prop相应的传给Header和Page
- 不同级也是类似的写法， 假如page在Navigation里，我们想让Page里的page也能达到统一，则必须将state提升到共用的App里
  
#### 1.2.3 子传父
子传父，用回调函数

- Q:为什么不推荐用pubsub
  - A: pubsub没法trigger state，这时候就需要把state跟pubsub连起来，管理pubsub会很难，而且会偏命令式
  - 再复杂一层的组件可以用context，再再复杂一层的组件可以用Redux

Cors主要是解决前后端api跨域，一般由后端设置，比如限制哪些ip address来访问

- Q:file loader和url laoder怎么选择
  - A:看官方文档，他们俩是做一件事的，将文件打包到项目来，引用这个文件
  - 前端有个performance的概念，network请求的数量越少，性能越好；
  - 当你引用一个图片的时候可以用url loader，他不会把文件引入进来作为单独文件使用（当文件大小小于设定的值），而会打包进你的代码，以减少请求；当文件大小大于设定的值，则会像file loader一样做单独资源打包

- Q: 老师，如果app中有很多自定义的函数，那bind的那个语句就要写好多遍，如果不小心没写就会出错，有没有什么更好的写法
  - A: 箭头函数；但是根据单一职责，app里不应该有很多函数
> 任何一个component应该都不多于150行代码，除掉import，每个组件应该都不多于100行代码
- Q: globalstyle放在app里行不行
  - A: 做一个global比较深的问题的时候，styled component并不是你的一个好的选择；比如修改body，borderbox，设fontfamily这样的，推荐大家在index.js里面，跟React DOM同级里面，import一个css做全局的样式
- Q: 是不是class component 都可以用function component写
  - A:class component比function component功能多，function component是没有state这个概念的；所以，所有的function component都可以写成class component
  - Q:是不是能用class component尽量用class component
    - A:能用function component就用function component，因为一个function占用的内存比class少的多的多
- Q: 如果用hooks呢
  - A:如果入行很久，去用hooks一点问题没有；但是hooks带来的性能问题，是junior没法handle的；所以对所有学生推荐，能写class component就不要写hooks，当你class component写熟了，再转去写hooks水到渠成

## 2.面试经验share by Darcy
### 2.1 技术面
- 看简历，照着简历问；比如项目技术，会对其中的概念问，遇到最大的困难是什么，对于Java，封装性，多样性的问题；
### 2.2 Behavior面
- 问题比较多
- 你能给团队带来什么：学习能力强，聪明；能快速的hands on，带来performance提升；人很nice，能让整个团队过的更和谐
### 2.3 Code Test
- 数字推理
- 简单的编程题
- 岛上有12人，一艘船一次能做3个人包括船夫，怎么最快的运出岛上的人
- 一架波音747能坐下多少高尔夫球
### 2.4 总结与其它问题
- Q:投了大概多少份简历拿到面试的呀？
  - Q:投了多少份简历开始有面试回应
    - A:一月底开始投，没有任何回应，改了简历，包装了自己的项目，三月份开始收到回应；质的改变是简历有写好
    - 一定要记住：投简历没有回复，不要找任何人来抱怨；没有回应，说明简历写的不够好
  - Q:面了多少家公司拿到offer，中间发生了什么要你有了质的改变直接面上了
    - A:经历过几场，就有经验了；前面几场容易乱答，后面有经验了知道怎么答会更好了；
    - 究极阶段是你面一个，收到一个offer；这时候你知道面试的套路，对面可能问你什么问题了

> 投简历没回应，不是因为没有junior的岗位；不要再找任何理由，比如没有工作经验，没有PR
- Q: 达西你做了好多项目啊，你是在校时候做的么
  - A: 放的自己做的项目；基本都是在匠人过来写的
  - 写三四个，让github绿起来；上龙哥的开始起，github就要一直是绿的
  - 从今天开始，每天写8小时代码，或者IT related，把自己逼上绝路
  - Q: 想问Darcy学了多久前端？
    - A:来报匠人课学的
- Q: 达西,你找工作有特意挑城市么?是根据自己住哪儿就找哪儿的 公司,还是不看工作地点,面试上了再搬?
  - A:找工作，除了达尔文，工作机会要远大于需求，不应该因为工作换城市；澳洲的工作，是供远小于求的
- Q: 老师 什么程序都可以往上传吗 练习啥的
  - A: 可以，哪怕只有一行的项目，也可以传
- Q:我有一个毛病,我能反复看教学视频,当就是不想自己敲代码,我总觉得我敲完代码也是不完美的,总想学到最完美的技术再敲
  - A:不要给自己找退路
  - 没有完美的代码，只有不停的敲，不停地refactor，才能让自己的代码趋近完美
- Q:龙哥 包装项目还没说
  - A:做的项目不一定是企业要求的，但是可以按照JD改成企业需要的；硬性，软性都写
  - 面向求职写简历：你学的永远跟企业要求的不是match的，你一定学不过来
- Q:我看达西也没写之前的工作经验啊，这个不用管jd上的年限要求，用自己做过很多项目来弥补对吧
  - A:澳洲工作，没有严格的工作经验要求，进来的面试和你工作经验没有关系；面试的时候，也没有一个人会问你工作经验
  - Q:猎头会问
    - A:很差的猎头，很不专业的猎头会问
- Q:darcy你的算法也是自学的吗?
  - A:去ANZ一定会考算法；去startup，越精高端的越会考；除了这两个地方，考你算法的天花板就是冒泡排序


## 3.P1回顾
三大核心概念
- Declarative
- Component base
- Learn once，write anywhere

P1及格的话，应该出现40个components(styled components)，如果不用styled component，则应该有20-30个components

当我们用Vanilla JS来切换页面的时候：很复杂，有压力；当我们再用React，state + props，切换页面就是水到渠成 
，这些做一般商业化项目就绰绰有余啦

从Vanilla JS的P1，改到React的P1，大家应该可以切实感受到Readable，Maintainable，Reusable上的一个质的提升

## 4.P2初讲
龙哥P2链接：  
https://github.com/KieraDOG/weather-app  
https://kieradog.github.io/weather-app/

推荐插件：  
https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi

可以根据插件查看网站的组件划分：  

P2根据复用度划分出的组件：
- Temperature
- Text
- Meta
- Vertical Divider
  
按照责任的划分：
- Current
- City(Sydney)
- City(Brisbane)
- City(Perth)
- Weather(Mon)
- Weather(Tue)
- Weather(Wed)
- Weather(Thu)
- Weather(Fri)

### 4.1 对P2的思考
我们发现根据前面课的知识，我们不足以完成P2，因为P2有功能：调用API，获取天气数据
- 调取API，用来更新页面数据
- 我们学过 component + props + state
#### 4.1.1 回顾怎样使用state 
- 提到页面改动，我们就会想到state，怎样使用state：
  - 1.转换做class component
  - 2.初始化 state
  - 3.做state相应的handler，并bind this
  - 4.在相应的 render中使用state
  - 5.在相应的地方更改 state
#### 4.1.2 目前难点 
在这个weather app里，我们对第五步并不是很清楚：在什么时候更新weather？
- 在api请求成功后，使用api数据更新weather

### 4.2 React API Caller
如何在React中请求api
- 首先找到openweathermap的官方api，例如https://openweathermap.org/api/hourly-forecast
- 上面要求我们提供cityname/cityID/经纬度/zip
  - 面试问题：如果我们可以通过上面四种方式拿数据，我们应该选择哪一种呢
    - 假如zip：全世界的zip code有没有相同的
      - zip code 源码有57W行，应该不会有重复的
    - 假如city name:全世界叫墨尔本的城市有多少个
      - 可以city name+国家
        - 假如同一个国家内有相同的city name呢
    - 所以说这个面试问题是在考验你是否考虑到重名问题
> 当你无法理解面试官的问题时候，你会觉得面试官在找你茬；只有充分的面试经验，才能让你理解面试问题的意图

#### 4.2.1 JS中写入最原始的http call
写一个Vanilla JS中最原始的http call
- 可以直接在openweatherapp上查到cityid，
- 在https://kieradog.github.io/weather-app/
- 打开调试工具，选择Network，Filter下选择XHR(异步调用，拿数据的call)
- 搜索xhr w3c，将xhr写入函数中
- 然后将url分割，让代码变的更readable一些
- 最后更改xhttp.open完成api call
```js
const Sydney = '2147714';

const getCurrentCityWeather = () => {
   
    const xhttp = new XMLHttpRequest();
    const basePath = 'https://api.openweathermap.org/data/2.5/';
    const units = 'metric';
    const appid = '2466213f21b4b723d341e00a430a7673';
    const url = `${basePath}/weather?id=${Sydney}&units=${units}&appid=${appid}`;
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            console.log(xhttp.responseText);
        }
    };
    xhttp.open("GET", url, true);
    xhttp.send();
}
```

#### 4.2.2 回顾JSON
- Q: 有用到JSON，需要学JSON吗？
  - A: 不用，可以在写代码中学习
  - JSON是用字符串的形式表达 JS Object
  - 在JS里拥有两个方法，stringfy 和 parse
  - stringfy是把JS Object转化为JSON
  - parse是把JSON转化为JS Object
  
#### 4.2.3 实现在React中调用API
下一个问题是，在什么地方调用getCurrentCityWeather
- 1.在render里面调用，成功console.log，即成功的拿到了data  
  
下一个问题，怎么把console.log换成 handleWeatherChange，让页面更新
- 2.set state 

##### 4.2.3.1 为什么调用了6000次api
我们在render里调用了set state，为什么保存运行一次，调用了6000次api  
首先这里不是callback hell: 讲的是一个代码readable的问题  
实际原因为：
- 1.getCurrentCityWeather后，他会this.setState
- 2.setState后会re-render，然后再次getCurrentCityWeather
- 然后不停重复步骤1.2，形成死循环

> 因此，setState 一定一定一定，不能在render里面直接调用

##### 4.2.3.2 React Lifecycle
这里引入一个新的概念：Lifecycle
- 组件的生命周期
- 生命，从出生到死亡
- 组件的出生到死亡所经历的步骤
- 所以我们应该在componentDidMount调用

React生命周期分为
- componentWillMount()
- componentDidMount()
- componentWillUpdate(object nextProps, object nextState)
- componentDidUpdate(object prevProps, object prevState)
- componentWillUnmount()

React 生命周期的三个状态:
- Mounting：插⼊ DOM
- Updating：重新渲染（更新）DOM
- Unmounting：移出 DOM

React 为每个状态都提供了两种处理函数，will 函数在进⼊状态之前调⽤，did 函数在进⼊状态之后调⽤

3个状态（Mount,Update,Unmount） * 2个处理函数(Will,Did) = 5个处理函数 

这里面为什么是5个而不是6个，是因为缺失一个componentDidUnmount()   
举个例子：
小孩子要准备生了：componentWillMount() ->  
小孩子生下来了：componentDidMount() ->  
小孩一生中发生很多事情，要不断学习，从准备学习到学会：componentWillUpdate(object nextProps, object nextState) -> componentDidUpdate(object prevProps, object prevState)  
这个人准备挂了：componentWillUnmount()  
因为挂了之后这个不能再说话了，所以就没有componentWillUnmount()   
即：  
Component -> constructor -> componentWillMount -> render -> componentDidMount -> (任何Snapshot更新 -> componentWillUpdate ->render -> componentDidUpdate) * n -> componentWillUnmount

在React里不推荐使用任何will函数，因为任何will函数都是不可靠的，  
我们得到最重要的经验是，过时的组件⽣命周期往往会带来不安全的编码实践，具体函数如下：
- componentWillMount
- componentWillUpdate

因为在React中，我们希望will只执行一次，其实可能执行了n次  
所以现在React的生命状态，只剩下了  
- componentDidMount()
- componentDidUpdate(object prevProps, object prevState)
- componentWillUnmount()

最后，为了实现我们的调用api，部分代码如下：
```js
const Sydney = '2147714';

const getCurrentWeather = (handleWeatherChange) => {
   
    const xhttp = new XMLHttpRequest();
    const basePath = 'https://api.openweathermap.org/data/2.5/';
    const units = 'metric';
    const appid = '2466213f21b4b723d341e00a430a7673';
    const url = `${basePath}/weather?id=${Sydney}&units=${units}&appid=${appid}`;
    xhttp.onreadystatechange = function() {
        if (this.readyState == 4 && this.status == 200) {
            const data = JSON.parse(xhttp.responseText);
           // console.log(data);
           handleWeatherChange(data);
        }
    };
    xhttp.open("GET", url, true);
    xhttp.send();
}

class Page extends React.Component{
    
    constructor(props){
        super(props);

        this.state = {
          weather: null,  
        };

        this.handleWeatherChange = this.handleWeatherChange.bind(this);
    }

    handleWeatherChange(newWeather) {
        this.setState({
            weather: newWeather,
        });
    };

    // 当组件被加载时，我们调用api call
    componentDidMount(){
        getCurrentWeather(this.handleWeatherChange);
    }

    render(){

        const {weather} = this.state;
        console.log(weather);
        return(）；
    }
}


```