# Class-27 React-6

## 主要知识点
  - [1.强化state和lifecycle的概念](#1强化state和lifecycle的概念)
    - [1.1 React学习再总结](#11-react学习再总结)
  - [2.课间提问](#2课间提问)
    - [2.1 抓紧机会，好好准备，努力找工](#21-抓紧机会好好准备努力找工)
  - [3.P2收尾：RMR原则重构部分功能](#3p2收尾rmr原则重构部分功能)
    - [3.1 变量命名](#31-变量命名)
    - [3.2 反思代码](#32-反思代码)
      - [3.2.1 令componentDidMount变得更Readable](#321-令componentdidmount变得更readable)
      - [3.2.2 用promise解决异步问题](#322-用promise解决异步问题)
      - [3.2.3 componentDidMount仍不完美，是否有库可以取代promise](#323-componentdidmount仍不完美是否有库可以取代promise)
      - [3.2.4 用fetch取代promise](#324-用fetch取代promise)
      - [3.2.5 修改weather，让代码更readable](#325-修改weather让代码更readable)
    - [3.3 程序报错，怎么解决第一次渲染没有data的问题](#33-程序报错怎么解决第一次渲染没有data的问题)
    - [3.4 写OtherCities Component](#34-写othercities-component)
      - [3.4.1 让city id更readable](#341-让city-id更readable)
      - [3.4.2 array的join用法](#342-array的join用法)
    - [3.5 增强代码复用性，开始写工具component:fetchOpenWeatherMap](#35-增强代码复用性开始写工具componentfetchopenweathermap)
      - [3.5.1 使用axios](#351-使用axios)
       
# 课堂笔记

## 1.强化state和lifecycle的概念
- Q:ANZ面试题：当你看到你的浏览器内容发生了更新，那么其背后 React 发生了什么？
  - A:看到关键词"更新"，就是跟state相关的；更新一定是由state改变相关，并且一步步触发如下
  - state 改变 -> re-render -> render / function -> reconciliation (VDom) -> 更新实际Dom，浏览器内容
  - 得分点分别为：state，render，reconciliation，vDOM
  - Q: 从 Component 的角度考虑，React 更新一定是由 state 改变引起的吗？比如下面代码，```componentDidUpdate```一定会被调用吗？```componentDidUpdate```在什么情况下会被打印log
```js
class List extends React.Component {
  componentDidUpdate() {
    console.log('componentDidUpdate');
  }

  render() {
    const { items } = this.props;

    return (
      <ul>
        {items.map((item) => (
          <li key={item.key}>{item.text}</li>
        ))}
      </ul>
    );
  }
}
``` 
  - A:props 发生改变，也会触发```componentDidUpdate```
    - Q: props 改变也会触发 re-render 吗?
    - Q: React 会在以下那种情况进行协调 （reconciliation）?
     - 1. props 改变
     - 2. state 改变 
     - 3. both
       - A: 答案是2，所有的更新都是由 state 更新触发的 ！！！没有一个更新，是由props更新触发
> 所有的更新都是由 state 更新触发的 !!! 所有的更新都是由 state 更新触发的 !!! 所有的更新都是由 state 更新触发的 !!!

- 但是为什么上面props会触发```componentDidUpdate```，或者说什么时候list props 会更新
```js
class Parent extends React.component {
  constructor(props) {
    super(props);

    this.state = {
      students: [],
    };
  }

  setStudents(newStudents) {
    this.setState({
      students: newStudents,
    });
  }

  componentDidMount() {
    getStudents().then((data) => this.setStudents(data));
  }

  render() {
    const { students } = this.state;

    return (
      <>
        <Header />
        <List items={students} />
      </>
    )
  }
}
```
通过上面这段代码，我们可以理解，props触发了更新，一定是父组件那边state发生了改变，所以触发了reconcilliation

- Q:假如我们如果有下面这样component，parent component已经发生了更新，那么下面代码里面的1，2会不会log出来，或者都不log

```js
class Header extends React.component {
  componentDidUpdate() {
    console.log('componentDidUpdate'); // 1.
  }

  render() {
    console.log('render'); // 2.

    return (
      <h2>Students</h2>
    );
  }
}
```
  - A:答案是2，因为parent的state发生改变后，会触发re-render，react会跑一边render，即parent的render()下的所有代码，在render各个子组件的时候，会执行子组件的render()

面试跟考试不一样，面试不会上来就问你一个比较难的问题，会从一个比较简单的问题入手，一步步来引导你；他不关心你会不会这道题，而是关心在他的引导下你有没有学习能力，理解能力，思考能力，以及React的基本原理   
不要以中国人的思维在澳洲面试，每个面试题都追求一个完美答案

如何判断哪些是state，哪些是props
- React中，如果组件里有数据变化，就是state；例如页面加载，加载过来的数据就是state，这时候子组件需要渲染，子组件之间需要通信需要拿数据，这些就是props

state越小越好，state应该在最小应用单元里
- PWC面试题里的weather-app，可能有100个state，如果到放在了app里，那app的性能就决定了整个项目的性能；正确顺序应该是先写到应用单元里，然后根据调用情况，做state lifing
- 比如weather里的future weather这个state，可以先写在furture weather这个子组件里，当另一个子组件同样需要这个数据的时候，可以给这个state做lifting，提升到两个子组件的共用组件里
> state lifting才是正道，这个过程一定不能省略，千万不能一上来就写到app里

### 1.1 React学习再总结
到此，我们React全部学完，我们学过了
- JSX 
- Component： class / function
- state (state lifting)
- props
- lifecycle  

React就以上知识点，大家要多做复盘，多做反思
- Q: refs算什么
  - A:属于JSX知识点，目前Junior基本用不到；ref属于打通React同JS，Vanlila JS的一个界限；React是本身自成一体的体系，并不需要其它框架的支持，但是如果非要在React写Jquery，Vanlila JS，那就需要refs了

最新版本的React中，component class，state与lifecycle合并成了hooks，因此学习的知识点变为了：
1. JSX, 2. function component,  3. props,  4.hooks

## 2.课间提问
- Q:用库的话可以省很多代码，那付出的成本有什么呢，不是说能用轮子就用轮子么，成本是库可能太大了？
  - A:不用调库，自己去写付出的成本是什么，时间；调库，不自己写付出的成本是什么，学习的机会。
- Q:那么用什么替代if-else呢？比如， if (a=1) then {return }
  - A: 没有替代方案，只是谈根据业务逻辑，能不能用别的方法来写。if-else并不是我们最好的解决方案。全是if-else，何谈rmr。

### 2.1 抓紧机会，好好准备，努力找工
澳洲IT市场，原来30-40%都是由海外签证组成，由于疫情，现在这部分由本土人员取代，从业人员少了一大半，但是IT业务增长了一大些，所以招人进入了一个极度不平衡的供需状态：junior没人了。
但是正是在这种情况下，求职人员中充斥着大量的杂兵杂将的junior，你们就是要准备完善，从这些人中脱颖而出。
现在大好的机会在等着你们，抓住这些机会的是什么，已经教给你们了。

面向求职学习：上午投简历，下午学习；第二天如果简历没响，就学第二天简历里面的东西

## 3.P2收尾：RMR原则重构部分功能

### 3.1 变量命名
Variable Naming READABLE：  
MELBOURNE -> MELBOURNE_CITY_ID 

### 3.2 反思代码
我们获取数据，并且渲染的流程为：  
MELBOURNE_CITY_ID + Metric + unit ->   
获取current weather ->  
componetDidMount的时候来getCurrentWeather ->   
再通过传入的handleWeatherChange来set state  

我们现在来反思，这个代码写的好不好，好不好的标准是RMR
#### 3.2.1 令componentDidMount变得更Readable
```js
componentDidMount(){
    getCurrentWeather(this.handleWeatherChange);
}
```
上面代码中，我们把function传进去了，这样直接下降了我们代码的readable  
我们可以先将代码加入onSucess：
```js
componentDidMount(){
    getCurrentWeather({
        onSuccess: this.handleWeatherChange});
}
```
这时候同样需要变更getCurrentWeather
```js
const getCurrentWeather = ({
    onSuccess,
}) => {
```
但是这里的onSuccess是我们创建出来的  
举个极端例子，如果这里有人会说onSuccess为什么不用onResponse呢
> 所以这里有个黄金原则：尽量减少made-up

#### 3.2.2 用promise解决异步问题
这里我们为什么调用handleWeatherChange，这个callback function，是因为我们要解决异步问题  
但是这又给我们带来了rmr的问题  
面试问题：如果因为解决异步，我们这里引入了callback，但是又产生了rmr，那我们怎么解决
- async await
- promise:https://juejin.cn/post/6844903586074198029
- 将getCurrentWeather return promise，然后更改componentDidMount：
```js
componentDidMount(){
    getCurrentWeather()
        .then((data) => this.handleWeatherChange(data));
}
```
即
```js
componentDidMount(){
    getCurrentWeather()
        .then(this.handleWeatherChange);
}
```
上面这个写法我们改好了，但是getCurrentWeather中仍然问题很多

#### 3.2.3 componentDidMount仍不完美，是否有库可以取代promise
我们这时候想，有没有方法可以用promise直接取代xmlhttprequest  
我们google：promise vs xmlhttprequest  
这时候我们从结果中发现了fetch api  
https://developer.mozilla.org/en-US/docs/Web/API/Fetch_API  
Fetch API 提供了一个获取资源的接口（包括跨域请求）。任何使用过 XMLHttpRequest 的人都能轻松上手，而且新的 API 提供了更强大和灵活的功能集。

#### 3.2.4 用fetch取代promise
直接去找using fetch，我们看到它非常易用，并且是一个原生的promise api  
这里我们可以修改getCurrentWeather（）
```js
const Sydney = '2147714';

const getCurrentWeather = () => {
   
    const basePath = 'https://api.openweathermap.org/data/2.5/';
    const units = 'metric';
    const appid = '2466213f21b4b723d341e00a430a7673';
    const url = `${basePath}/weather?id=${Sydney}&units=${units}&appid=${appid}`;
    
    return fetch(url)
    .then((response) => {
        console.log(response);
    });
}

```
为输出Json对象，我们可以写成：
```js
const getCurrentWeather = () => {
   
    const basePath = 'https://api.openweathermap.org/data/2.5/';
    const units = 'metric';
    const appid = '2466213f21b4b723d341e00a430a7673';
    const url = `${basePath}/weather?id=${Sydney}&units=${units}&appid=${appid}`;
    
    return fetch(url)
    .then((response) => response.json())
    .then((data) => console.log(data));
}
```
最终简写为
```js
const getCurrentLikeNum = () => {
   
    const basePath = 'https://api.openweathermap.org/data/2.5/';
    const units = 'metric';
    const appid = '2466213f21b4b723d341e00a430a7673';
    const url = `${basePath}/weather?id=${Sydney}&units=${units}&appid=${appid}`;
    
    return fetch(url).then((response) => response.json());
}
```
这时候面试官问你为什么用fetch，你就可以跟他聊起来了

- Q: 老师那我们就是学习的时候尽量选择原生的写法?这些库知道他们怎么用能应付面试就行了是么?
  - A: 不对，用不用原生的写法都是无所谓的；但是，如果能用原生的写法，发现痛点，解决痛点，那用原生的写法是没有问题的；这里的关键点不是用不用库，也不是原生不原生，而是你有没有分析出问题，解决问题的能力
- Q:老师如果我想同时fetch两个api的地址该怎么办。。我之前p2用的promise.all
  - A:Yes，是promise all
- Q:老师有了fetch
    我是不是就可以不用学xmlhttprequest了
    - A: 可以，如果你完全理解了我们为什么用fetch，而不用xmlhttprequest
- Q: 我是在didMount之后给不同的url发了两次ajax请求，都取到以后再下一步,但是感觉有点慢
  - A: 必不可免的

#### 3.2.5 修改weather，让代码更readable
在顺利fetch到data后，我们就可以将data添加到页面上了
```js
<div className={styles.temperature}>
     <Temperature>{weather.main.temp}</Temperature>
</div>
<div className={styles.weather}>
     <Text>{weather.weather[0].main}</Text>
</div>
```
这里我们有遇到了一个readable的问题，应该将weather改为data
- Q:龙哥这里的state结构应该怎么设置更合理，跟请求回来的数据一样的结构设么，我看你这边是设置的一个weather对象
  - A:state一定是一个总的state，如果把每个数据都抽出来，会非常长且麻烦

### 3.3 程序报错，怎么解决第一次渲染没有data的问题
保存完后，我们还遇到了一个问题
```Cannot read property 'main' of undefined```
这里的错误是data是undefined，这是因为data在下列过程中
construct { data: undefined } -> render -> componentDidMount -> getCurrentWeather -> setState { data: 数据 } -> render
第一次render的时候，data并没有数据

这里有三个解决方案
- &&
  - 短路计算
  - ```<Temperature>{data && data.main.temp}</Temperature>```
  - 这里的问题是，每一个有data的地方都要用 &&
- 初始值
  - ```<Temperature>{data === undefined ? '0' : data.main.temp}</Temperature>```
  - 这里的问题是，不仅每一个data要分别给初始值，而且还要改每一个data
- loading
  - 进一个页面，数据还没有拿到的时候，页面会看到loading...完美
```js
render(){
    const {data} = this.state;
    if(!data){
        return 'Loading';
    }
}
```
如此我们完成了current.js

### 3.4 写OtherCities Component
这个时候，我们再来做OtherCities页面，首先我们想到的就是那些需要更新的数据：state，然后我们
- initialize state
- state handler
- stage usage/set state
#### 3.4.1 让city id更readable 
注意在这里，我们要留意readable：
```js
const OTHER_CITIES = [{
  name: 'Sydney', id: '2147714',
}, {
  name: 'Brisbane', id: '2174003',
}, {
  name: 'Perth', id: '2063523',
}];

const otherCitiesId = OTHER_CITIES.map((city) => city.id).join(',');
```
#### 3.4.2 array的join用法
这里，如果array是[1,2,3]，我们想把这个array变成字符串"1,2,3"，就可以用join(',')，最后通过解构data，传到render里
```js
return (
      <div className={styles.otherCities}>
        <h2 className={styles.header}>Other Cities</h2>
        <div className={styles.cities}>
          {data.list.map(({ id, name, main: { temp }, weather: [{ icon, main }] }) => (
            <City 
              key={id}
              name={name}
              temperature={temp}
              weather={{ icon, description: main }} 
            />
          ))}
        </div>
      </div>
);
```
- Q: 能不能在get current weather的api call获得同时这些数据，然后通过props传到othercities?
  - A: RMR, other city里的state就需要lift上去，这么做的目的是什么
    - Q: 对，我就是这么做的，为了不分别loading，不然分别loading不好看
      - A: 但是这样single responsibility就没有了
    - Q: 想少写点代码
      - A: 想少写点代码靠的是复用
      - rmr出发点，没有一个是想少写点代码

### 3.5 增强代码复用性，开始写工具component:fetchOpenWeatherMap
怎么能少写点代码呢? 把部分代码复用起来   
新建utils，在当中新建fetchOpenWeatherMap.js，将相同部分copy过来
```js
    const basePath = 'https://api.openweathermap.org/data/2.5/';
    const units = 'metric';
    const appid = '2466213f21b4b723d341e00a430a7673';
    const url = `${basePath}/weather?id=${Sydney}&units=${units}&appid=${appid}`;
    
    return fetch(url)
    .then((response) => response.json());
```
然后修改不同的部分，引入path
```js
const fetchOpenWeatherMap = ({
    path,
}) => {
    const basePath = 'https://api.openweathermap.org/data/2.5/';
    const units = 'metric';
    const appid = '2466213f21b4b723d341e00a430a7673';
    const url = `${basePath}/${path}&units=${units}&appid=${appid}`;
    
    return fetch(url)
    .then((response) => response.json());
}
```
然后我们的getCurrentCityWeather就可以简化为
```js
const getCurrentCityWeather = () => {
    return fetchOpenWeatherMap(SYDNEY_CITY_ID);
}
```

#### 3.5.1 使用axios
这时候我们觉得还是很复杂，我们google发现还有一个更好的东西：axios  
https://github.com/axios/axios  
Promise based HTTP client for the browser and node.js  
回到一个面试问题：你怎么连接API
- 用过了xmlhttprequest, 发现不够maintainable
- 用过了fetch，发现声明basePath这样，以及写一个custom function
- 最后选了用axios
```
npm i -D axios
```
首先我们可以新建OpenWeatherMap.js，然后再在current里，调用即可
```js
//OpenWeatherMap.js
import axios from 'axios';

const baseURL = 'https://api.openweathermap.org/data/2.5';
const units = 'metric';
const appid = '2466213f21b4b723d341e00a430a7673';

const OpenWeatherMap = axios.create({
  baseURL,
  params: {
    units,
    appid,
  }
});

export default OpenWeatherMap;
```
```js
// Variable Naming READABLE
const MELBOURNE_CITY_ID = '2158177'; // readable

// RMR
const getCurrentCityWeather = () => OpenWeatherMap.get('/weather', {
  params: {
    id: MELBOURNE_CITY_ID,
  },
}).then((response) => response.data);
```
到此，我们就将api调用写的非常RMR了

- Q: 龙哥你每个组件都加个index.js，感觉优势只是import的时候指到文件夹，为少写一个单词而多加个js文件，还是说有其他优点
  - A: 给每个文件加了一个入口文件，来进行分发

这节课里的知识点fetch，axios，都可以讲两节课，但是我们的重点是希望大家理解，什么样的代码是对的，怎么样学习才是对的，比如这是个什么库，我们在什么情况下选择用这个库