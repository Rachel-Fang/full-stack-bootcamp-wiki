# Class-07 JavaScript ES6 Part2

## 主要知识点
  - [1.课前课间小讨论](#1课前课间小讨论)
  - [2.复习RMR](#2复习rmr)
  - [3.ES的历史及浏览器兼容性问题](#3es的历史及浏览器兼容性问题)
    - [3.1 ES的发展及背景](#31-es的发展及背景)
    - [3.2 浏览器兼容性的相关讨论](#32-浏览器兼容性的相关讨论)
  - [4.Object Oriented Programing](#4object-oriented-programing)
    - [4.1 怎样在JavaScript(ES6之前)中实现Object Oriented Programing](#41-怎样在javascriptes6之前中实现object-oriented-programing)
    - [4.2 prototype 在JavaScript中的使用](#42-prototype-在javascript中的使用)
  - [5.ES6引入的新功能](#5es6引入的新功能)
    - [5.1 class 在ES6中的使用](#51-class-在es6中的使用)
    - [5.2 let/const 在ES6中的使用](#52-letconst-在es6中的使用)
    - [5.3 Template String 模板字符串（反引号）在ES6中的使用](#53-template-string-模板字符串反引号在es6中的使用)
    - [5.4 函数参数的默认值](#54-函数参数的默认值)
    - [5.5 Destructuring 解构赋值(重要!)](#55-destructuring-解构赋值重要)
    - [5.5.1 Array的解构赋值](#551-array的解构赋值)
    - [5.5.1 解构赋值标准用法中的简写](#551-解构赋值标准用法中的简写)
      - [5.5.2.1 多层取值的简写](#5521-多层取值的简写)
      - [5.5.2.2 简易化赋值](#5522-简易化赋值)
    - [5.5.3 解构赋值的进阶学习](#553-解构赋值的进阶学习)
      - [5.5.3.1 语法糖 spread](#5531-语法糖-spread)
  - [6.JavaScript中的 this (最重要最无聊又最没用)](#6javascript中的-this-最重要最无聊又最没用)
    - [6.0 函数是一等公民](#60-函数是一等公民)
    - [6.1 对this的理解](#61-对this的理解)
    - [6.2 this代码题目分析](#62-this代码题目分析)
    - [6.3 字节跳动面试原题](#63-字节跳动面试原题)
  

# 课堂笔记

## 1.课前课间小讨论
- Q:三元表达式那里，expression可不可以是一块代码吗
  - A: 三元表达式中可以放function，因此可以间接放入一块代码，这种用法不多，例如
    ```js
    var isMyPet = true;
    var petName = isMyPet ? (function(){
        var pet = 'Luna';
        return pet;
    })():'旺财';
    ```
- Q:工作需要工作经验吗😭?
  - A: 澳洲公司更看重的是项目经验
  
- Q:如果想去大点的公司的话有要求gpa?
  - A: 不需要，其实大公司要比小公司面试简单，因为小公司的用人成本更高，要求反而会更严格。大公司普遍不会考算法，除了ANZ/Google/Amazon`会用算法卡人`
  
- Q:老师面试中对英语的要求高吗哈哈哈?
  - A: 公司对英语的要求一般不高，但是也要能达到日常交流的水准，对日常用语的要求是高的
  
- Q:年龄大的怎么建议？
  - A: 澳洲没有年龄限制，年龄大的跟年龄不大的都一样

- Q:工作需要PR吗
  - A：不需要，在澳洲找工作，PR并不重要（除非堪培拉），只要你有working right就可以了
  
- Q：前端的面试会面试算法吗?
  - A：普遍不会，除了ANZ的online assessment，和某些小公司；
  
- Q: JS object 等于 JSON 吗?
  - A: JSON全称为JavaScript Object Notation，为JavaScript Object的一种表达方式

## 2.复习RMR
- 为什么不停出现新的语言，框架，技术，我们又要去学习这些，还是因为核心原则RMR（`Readable, Maintainable, Reusable`）
> 希望这节课结束后，大家把这三个单词打印出来贴显示器上，现在学的所有东西，以及未来人生工作中学的所有东西都服务于这三个单词:`Readable, Maintainable, Reusable`
- 这节课学习ES6，就是来看一下，这三个单词，到底有多么重要

## 3.ES的历史及浏览器兼容性问题
### 3.1 ES的发展及背景
- 大部分高级语言，都是有大公司在维护，不断更新的，比如JAVA已经到了8(稳定版)/14，Python到了3.7，php到了8，CSS3，HTML5...
- 对于大公司维护一门高级语言，是一件名利双收的事情
- 对于JavaScript，从来没有版本号这个讲法，属于社区维护
- 维护JavaScript的社区叫做ECMA(European Computer Manufacturers Association，欧洲计算机制造协会)；在欧洲，JavaScript更愿被称之为ECMAScript(ES)
- JavaScript ES6：在ES6标准下执行的JavaScript
- 解释性语言 VS 编译型语言 
  - 解释性语言：源码->解释 ->解释成C ->编译 -> 010101
  - 编译型语言：源码->编译->010101
- 关于解释环境（代码在哪里解释，谁来解释）
  - 浏览器来负责解释JavaScript
  > Q: JS是在哪里运行  
  A: 在（浏览器的）网页环境里  
  Q: Java是在哪里运行的  
  A：是在一个拥有Java环境的容器里
### 3.2 浏览器兼容性的相关讨论
- 谈及JavaScript的运行环境：浏览器，又是一个涉及更多的话题
  - 浏览器究竟做了什么事情：发起接受请求（万网互通），负责渲染HTML, CSS, 以及解释JavaScript；
  - 对JavaScript的解释差异，造成了浏览器间的主要分别
  - |浏览器名 |  优势 | 原因|
    |------------------|-----|----------------------|
    |Chrome|性能好|大神更多|
    |FireFox|性能好||
    |Edge|性能更好|基于windows，高效解释js|
    |IE11|老电脑多||
    |360|标榜安全|更安全的解释js|
    |Safari|省电|基于apple底层硬件，高效解释js|
- 引入一个概念Immutable(无懈可击的，永恒的)
  - 意味着 唯一的输出，产生唯一的结果
  - 比如你要编程输出`hello world`，那个不论你怎么编译，它只会输出一个结果
  - 比如你翻译一句英文，同样的输入，但是翻译的不同，结果不同，那就不是immutable
  - 对于JavaScript在浏览器中的解释，不同的浏览器有不同的解释倾向；例如JavaScript引入一个新功能，Safari可能处于功耗考虑，而不去使用（解释）；这就造成了，不同的JavaScript版本，浏览器的支持度是不一样的。
  > 我们写的JavaScript，不同的浏览器可能在认定合法性和解释上，表现不同；因次，JavaScript对不同浏览器的兼容，要永远刻在脑子里
  - 前端程序员最大的敌人：IE11，对ES5以上不支持
  - ES7只是基于ES5开发的，跨过了ES6

## 4.Object Oriented Programing
- JavaScript中的object，不等同于Java中的object
  - OOP中，objects是一个class的instance
  - 但是在JavaScript是没有object的，JS中 everything is object
    - 什么叫everything is object?
    - 在js中，object就是一个`key`与`value`的mapping，例如
      ```js
      {
          //key: name, value: 'Long Zhao'
          name: 'Long Zhao',
          //key: greeting, value: function()
          greeting: function(){},
      }
      ```
### 4.1 怎样在JavaScript(ES6之前)中实现Object Oriented Programing
- JavaScript也可以通过函数实现OOP，例如
  ```js
  function createNewPerson(name) {
    var obj = {};
    obj.name = name;
    obj.greeting = function () {
        console.log('Hi! I\'m' + this.name + '.');
    }

    return obj;
  }

  //Low版本的JS OOP
  var alice = createNewPerson('Alice');
  alice.greeting();
  // Hi! I'm Alice
  ```
  但是，如果我们知道如何创建一个对象，就没有必要创建一个新的空对象并且返回它。改用this，也能实现这个功能。
  ```js
  function Person(name) { 
    this.name = name;
    this.greeting = function() {
        alert('Hi! I\'m ' + this.name + '.');
    }; 
  }
  //不要使用 var alice = Person('Alice');
  //因为这样没法使用 this
  var alice = new Person('Alice'); 
  alice.greeting();
  ```
  又但是，这不是一个readable，maintainable，reuseable的代码，而且存在内存泄漏的风险
  每次`new`一个Person，JS在运行到`this.greeting = function()`时，都会帮你生成一个新的function，每生成一个新的function就会占用一块新的内存
### 4.2 prototype 在JavaScript中的使用
- 大神说，想解决上面这个问题，可以引入`prototype`(但是ES6中不推荐使用)，将上面代码改造为
   ```js
   function Person(name) { 
    this.name = name;
   }

   Person.prototype.greeting = function() {
       alert('Hi! I\'m ' + this.name + '.');
   }

   const alice = new Person('Alice'); 
   alice.greeting();
   ```
   这样每次new function的过程中，就不会再创建一个新的function，只会执行name的赋值，而相应的function会使用prototype挂载，内存应用会更好 

## 5.ES6引入的新功能
### 5.1 class 在ES6中的使用
- 在ES6中，更可以通过新引入的`class`来实现，通过class可以定义类，比如
   ```js
   class Person { 
    constructor(name) {
        this.name = name; 
    }

    sayHi() {
        console.log('My name is ' + this.name);
    }

    joinMeeting(meeting) { 
        meeting.talks.push(this.sayHi);
    } 
   }

   var alice = new Person('Alice');
   ```
   
### 5.2 let/const 在ES6中的使用
- ES6 新增了let/const命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let/const命令所在的代码块内有效。
  - 以后要严格的遵循，先声明，再调用的原则 
  - let->变量，const->常量
  - 基本上const用的多，let用的少
### 5.3 Template String 模板字符串（反引号）在ES6中的使用
- 字符串操作在JavaScript中是非常繁琐的，ES6中可以用反引号直接，${}, 花括号里的是JavaScript statement，例如
   ```js 
    const greeting = `Hello ${name}`;
    const multiLinesGreeting = ` 
    Hello,
    My Name is ${name}.
    Nice to meet you.
    `;
   ```
### 5.4 函数参数的默认值
- ES6之前，我们在JS中写默认值，会用到if...else，比如
 ```js
    const hello = (name) => {
        if (!name) {
            name = 'World';
        }
        console.log(`Hello ${name}`);
    }
 ```
 ES6中，我们可以使用以下写法，通过给参数`=`与赋值，直接提供默认值给函数
 ```js
    //如果参数name没有传入，就默认为World
    const hello = (name = 'World') => {
        console.log(`Hello ${name}`);
    }
 ```
 或者
 ```js
    //b现在变成optional，可传可不传
    fucntion sum(a,b = 0){
        return a + b;
    }

    sum(1, 3); // 4
    sum(1); //1
 ```
 如果想把一个参数变成optional,就给他加`=`就可以了

### 5.5 Destructuring 解构赋值(重要!)
传统JavaScript中，我们想处理一个object中的key是非常复杂的，比如
```js
    const student = { 
        name: 'Alice', 
        age: 26, 
        courses: [{
            name: 'Introduction to JavaScript', 
        }, {
            name: 'How to give up JavaScript', }],
    };
```
想要获取其中key的value，就要依次写代码
```js
    const name = student.name; 
    const age = student.age;
    const courses = student.courses;
```
但是上面三行的代码出现了太多`copy/paste`,
> 一个代码中，一旦出现了`copy/paste`，这个代码就一定是有问题的，就一定有bad smell  

> 程序员的黄金法则：我一定是很懒的，所以我不屑于写重复的代码
 
所以上面三行代码，通过ES6中的解构赋值，可以一行搞定
```js
    //从student中取name, age, courses,分别赋值给新的变量name, age, courses
    const { name, age, courses } = student;
```
以上，按照一定模式，从数组和对象中提取值，对变量进行赋值，这被称为解构(Destructuring)

### 5.5.1 Array的解构赋值
Array可以理解成JS帮我们处理过的特殊过的object，比如
```js
    const arr = ['a','b','c'];
```
实际等同于（要学会用同理可得去推理代码）
```js
    const arr = {
        0: 'a',
        1: 'b',
        2: 'c',
    }
```
因此，我们也可以像上面解构object一样解构array，写成
```js
    //取key为0的值，赋值给value0
    //取key为1的值，赋值给value1
    //取key为2的值，赋值给value2
    const{0:value0, 1:value1, 2:value2} = arr;
```
在ES6中，针对array，`{}`会替换成`[]`，上行代码可以直接写成，
```js
    const [value0, value1, value2] = arr;
```
### 5.5.1 解构赋值标准用法中的简写
#### 5.5.2.1 多层取值的简写
依然是对于student object
```js
    const student = { 
        name: 'Alice', 
        age: 26, 
        courses: [{
            name: 'Introduction to JavaScript', 
        }, {
            name: 'How to give up JavaScript', }],
    };
```
进行解构，我们想提取`courses`中的第一个课程，于是有了
```js
    const { courses, name, age } = student;
    const [ introduction ] = courses;
    const [name: myFavouriteCourseName] = introduction;

    console.log(myFavouriteCourseName); // 'Introduction to JavaScript'
```
对上面的三行代码，我们做进一步简化，可以写成
```js
    const { courses, name, age } = student;
    const [{name: myFavouriteCourseName}] = courses;
```
再做一步简化，可写成
```js
    const { 
    courses: [{name: myFavouriteCourseName}],
    name, 
    age, 
    } = student;
```
#### 5.5.2.2 简易化赋值
举一个现实中的例子，我们想获得用户输入的信息，再赋值给一个object，在ES6之前会这么写
```js
    const { value: name } = document.getElementById('name-input');
    const { value: age } = document.getElementById('age-input');
    const { value: street } = document.getElementById('street-input');
    const { value: postCode } = document.getElementById('postCode-input');
    const address = `${street}, ${postCode}`

    const student = {
      name: name,
      age: age,
      address: address,
    };
```
上面这段代码，从`Maintainable`角度来看，当我们把`name`写成了`nmae`时，可能需要修改三处来修正，痛点在这里
```
      name: name,
      age: age,
      address: address,
```
于是在ES6中，如果object里，key的name跟传进来的变量名相同，可以直接简写为
```js
      const student = {
      name,
      age,
      address,
      //不同名的还是要写出来
      phone: mobile,
    };
```
### 5.5.3 解构赋值的进阶学习
#### 5.5.3.1 语法糖 spread
可以把想要的拿出来，剩下的分发出去，用...，例如以下代码
```js
    Alice {
      护照,
      行李:[大箱子，小箱子，电脑包],
    };

    const { 护照, 行李: [托运行李, ...其他行李]} = Alice;

    console.log(其他行李); // 小箱子 电脑包
```
## 6.JavaScript中的 this (最重要最无聊又最没用)
最重要：JavaScript的核心理论；有时候有莫名其妙的错误，可能就是`this`的导向造成的  
最没用：太过于高级，以至于现在没人愿意去用它了
### 6.0 函数是一等公民
Pure function is the one and only first-class citizen 函数是一等公民，   
有翻译问题，中文听起来感觉好像函数很高大上，有特权的样子，实际上英文中的`first-class citizen`是最普通，最基本，最没有特权的老百姓，龙哥的翻译是
`函数也就是个平头老百姓`。  
为什么这么说呢，因为函数的本质是`object`，它
- 可以在程序执行时动态创建函数（就像在函数里创建一个变量一样） 
- 可以将函数赋值给变量（就像你可以把一个值赋值给函数里的变量一样）
- 可以将函数作为参数传给例外一个函数，例如下面代码 
  ```js
    //在多少‘延时’后，执行什么‘操作’
    setInterval(操作，延时)
    
    const sayHi = function() {
      console.log('Hello World');
    }

    setInterval(sayHi, 300);  
  ```
- 可以作为返回值返回，例如下面代码
  ```js
  const createSayHi = function(greeting) {
    function sayHi(name) {
      console.log(`${greeting} ${name}`);
    }
  }

  const greetingMyName = createSayHi('Greeting');
  greetingMyName('Long');// Greeting Long
  ```

### 6.1 对this的理解
借用龙哥笔记的话，`this`是这样的:   
this 的指向是在调用时确定的。 用大白话来讲，“谁调用，指向谁。”
this 的指向，是在调用函数时根据上下文所动态确定的

具体环节和规则，可以先“死记硬背”以下几条规律。
- 在函数体中，简单调用该函数时，严格模式下 this 绑定到 undefined，否则绑定到全局对象 window (browser)/global (node); 
- 一般构造函数 new 调用，绑定到新创建的对象上;
- 一般由上下文对象调用，绑定在该对象上;
- 一般由 call/apply/bind 方法显式调用，绑定到指定参数的对象上;
> 能不写`this`就不写`this`是现在主流核心思想  
> 
怎么具体理解`this`呢，让我们看下面这个题：
```js
  var alice = {
    name: 'Alice',
    getName: function() {
        return this.name;
    },
  }
```
- 请问 `alice.getName()`得到什么？  
答案是`Alice`

再让我们看下面这个题
```js
  var alice = {
    name: 'Alice',
    getName: function() {
        return this.name;
    },
  }

  var bob = {};

  bob.name = 'Bob';
  bob.getName = alice.getName;
```
- 请问 `bob.getName()`得到什么？  
答案是`Bob`

如果对上面的代码加入
```js
  const { getName } = bob;
```
- 请问 `getName()`得到什么？  
答案是`undefined` 

在JavaScript中有`caller`的概念，比如`bob.getName()`中，`getName()`的`caller`就是`bob`；`caller`是谁，`this`就指向谁。

### 6.2 this代码题目分析
```js
  const alice = {
    name: 'Alice',
    brother: {
      name: 'Bob',
      getName: function() {
        return this.name;
      }
    }
  }

  const sister = {
      name = 'Tifa',
      getName: function(){
          return this.name;
      },
      getMyBrotherName:function(){
          return alice.brother.getName();
      }
      getSomebodyName:function(){
          const getName = function(){
              return this.name;
          };
            
          return getName();
      },
  };

  console.log(sister.getName());
  console.log(sister.getMyBrotherName());
  console.log(sister.getSomebodyName());
```
答案为：
```js
  Tifa //caller为sister
  Bob //caller为brother; 如果没有'name: Bob'这句，结果为 undefined
  undefined //caller为undefined 
```
如果加入下面两行：
```js
  alice.getName = sister.getName;
  alice.getName();
```
答案为 `Alice`

如果加入下面两行：
```js
  alice.getName = sister.getMyBrotherName;
  alice.getName();
```
答案为 `Bob`

如果加入下面两行：
```js
  alice.getName = sister.getSomebodyName;
  alice.getName();
```
答案为 `undefined`

>对于this，你所需要关心的就是最终的caller是谁

### 6.3 字节跳动面试原题
```js
  var o1 = {
      text: 'o1',
      fn: function(){
          return this.text;
      },
  };

  var o2 = {
      text: 'o2',
      fn: function(){
          return o1.fn();
      },
  };

  var o3 = {
      text: 'o3',
      fn: function(){
          var fn = o1.fn;
          return fn();
      },
  };

  console.log(o1.fn());
  console.log(o2.fn());
  console.log(o3.fn());
```
答案为：
```js
  o1 
  o2 
  undefined 
```
逻辑原理同6.2部分(重点看是谁调用)

