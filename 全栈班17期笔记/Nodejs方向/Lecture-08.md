## 目录

- [8.0 15分钟理解this用法(Raymond讲解)](#80-15分钟理解this用法raymond讲解)
    - [8.0.1 this是什么?](#801-this是什么)
    - [8.0.2 箭头函数](#802-箭头函数)
    - [8.0.3 function（构造函数）和class](#803-function和class)
- [8.1 this](#81-this)
    - [8.1.1 this keyword in normal functions](#811-this-keyword-in-normal-functions)
    - [8.1.2 this keyword in normal functions with bind, call, apply](#812-bind-call-apply)
    - [8.1.3 this keyword in an object and callback functions](#813-this-keyword-in-an-object-and-callback-functions)
    - [8.1.4 this keyword in arrow function](#814-this-keyword-in-arrow-function)
    - [8.1.5 quiz](#815-quiz)
- [8.2 Common array operations](#82-common-array-operations)
    - [8.2.1 Manipulation](#821-manipulation)
    - [8.2.2 Iteration（遍历）](#822-iteration遍历)
    - [8.2.3 Map](#823-map非常常见)
    - [8.2.4 Reduce](#824-reduce)
    - [8.2.5 Search](#825-search)
    - [8.2.6 Extra reading source](#826-extra-reading-source)
- [8.3 Set](#83-set)
- [8.4 Basic Classes](#84-basic-classes)
- [8.5 extends（继承）](#85-extends继承)
- [8.6 quiz](#86-quiz)
- [8.7 Asynchronous（异步）](#87-asynchronous异步-in-js)



### 8.0 讲解Javascript的this使用方法，15分钟理解this用法(Raymond讲解)

>视频链接：https://www.youtube.com/watch?v=UcTmMSyWoqE

#### 8.0.1 this是什么？

- 什么东西会有this？this到底是什么？
    - this其实就是“我是谁”这个概念。
    - “人”或者“物”才会有“我是谁”这个概念。
    - 动作不具有“我是谁”这个概念。比如：爬山、骑自行车。
    - 得是“爬山的人”或“骑自行车的人”才会有“我是谁”这个概念。
    - 在JS中，object本身才会有“我是谁”这个概念。object内部的方法，才会有“我是谁”这个概念；外部的方法，不具有“我是谁”这个概念。

- 编程代码，应该是这样：
```js
const ming = {
    name: "xiaoming",
    climbing: function(){
        console.log(this)
    }
}

ming.climbing();
```
>chrome和Nodejs结果：
```js
{ name: 'xiaoming', climbing: [Function: climbing] }
```
>说明：
- 这个this其实就是指向这个ming，this永远指向object。

- 我们把function拿出来：
```js
const ming = {
    name: "xiaoming",
    climbing: function(){
        console.log(this)
    }
}

function climbing(){
    console.log(this)
}

climbing();
```
>chrome结果：
Window
>Nodejs结果：
Object [global]

>说明：
- function输出this的时候，要寻求一个合理性，我到底指向哪个object？
- 在非严格模式下，chrome认为你指的是全局；Nodejs也认为指的是全局，这个全局就是global。所以this在非严格模式下，本质上指向的就是global，不管是在哪个环境下，只不过一个是window，一个是global。
- 在严格模式下，两个都是undefined，为什么呢？
    - function严格来说，this根本没有持有人的，所以是这里的this是undefined。
    - 之后都会用严格模式来说话，除非遇到一些特殊情况。
- this实际上就是指向一个object，object就是这个对象本身是什么。为什么会有这样一个设定呢？原因如下：
    - 我们现在有一个object，
    ```js
    const ming = {
        name: "xiaoming",
        climbing: function(){
            console.log(this)
        }
    }

    function climbing(){
        console.log(this)
    }

    climbing();
    ```
    - 如果在this的位置换成name，会变成横杠。
    - chrome的执行结果是什么也没有，Nodejs的执行结果是报错。
    - 因为object ming这个{}，并非作用域，{}仅仅是包括的意思。name和climbing是同级的关系。并不是先执行name，再执行climbing。而是object里有一个name的property，另外还有一个function。
    - 因为name和function是并列关系，this根本不知道前面的name是什么，所以它并不会用到name。
    - 如何才会调用到name？JS的做法是：
        - function先要知道这个object是谁，然后通过object调用这个name，才能获得是谁。
        - 我们用(this.name)操作，就可以了。
            ```js
            const ming = {
                name: "xiaoming",
                climbing: function(){
                    console.log(this.name)
                }
            }

            function climbing(){
                console.log(this)
            }

            climbing();
            ```
            >结果：xiaoming（这里就知道object到底是谁了）



#### 8.0.2 箭头函数

- 结构：
```js
const ming = {
    name: "xiaoming",
    climbing: function(){
        console.log(this.name)
    }
}

function climbing(){
    console.log(this)
}

const cycling = () => {
    console.log(this)
}

cycling();
```
>执行cycling的结果：
- chrome下：window
- Nodejs下：{}

>说明：
- 箭头函数暴露在外界情况下：this在chrome下是global；在nodejs下，它觉得使用空的object是比较安全的。（在严格和非严格模式下是一样的）
- 箭头函数的特点：
    - 本身不具备this，那它的this是怎么来的呢？this在寻求外层的作用域。
    - object ming的{}是囊括的意思，并不是作用域。所以this会寻求ming外面的作用域。寻求外面作用域和放在ming外面，本质上是一样的，所以运行结果也是一样的：window和{}。

#### 8.0.3 function（构造函数）和class

***第一种情况：在const、function和class里面***

```js
"use strict"
console.clear();

function climbing(){
    console.log(this)
}

const cycling = () => {
    console.log(this)
}

const ming = {
    name: "xiaoming",
    climbing: function(){
        console.log(this)
    }
    cycling:() => {
        console.log(this)
    }
}

function person() {
    this.name = "xiaoming2";
    this.climbing = function(){
        console.log(this)
    }
    this.cycling = () => {
        console.log(this)
    }
}

class Person (
    constructor(){
        this.name = "xiaoming3"
    }
    climbing(){
        console.log(this)
    }
    cycling = () => {
        console.log(this)
    }
)

const ming2 = new person();
const ming3 = new Person();

ming2.climbing();
ming3.climbing();

ming2.cycling();
ming3.cycling();
```

>结果：
- chrome：person（小）、Person（大）、person（小）、Person（大）
- Nodejs：person（小）、Person（大）、person（小）、Person（大）

>说明：
- this.climbing = function()是function person()里面的方法体，在调用的时候，是以ming2的身份来调用的。以身份来调用的时候，它知道自己是谁。
- 而箭头函数cycling = () => { console.log(this) }在寻求外围的作用域，这个作用域就是在function和class的里面，所以它也知道是在person和Person里面的。this在这时已经被确定。
- new是object，它通过function和class被创造出来。创造的时候，它去寻找它的作用域，原来在function和class里面，这个箭头函数的this就被确定了。


- 把以上的输出改成如下，其他不变：
```js
ming2.climbing();
ming3.climbing();
ming2.cycling();
ming3.cycling();

// 换成

const func1 = ming.climbing;
const func2 = ming.cycling;
func1();
func2();
```

>结果：
- chrome：undefined、window
- Nodejs：undefined、{}

>说明：
- ming把climbing传递出来的时候，func1就丢失了自己的操作者。
- 执行func1的时候，没有提及谁来执行，所以func1是没有操作者的，所以是undefined。
- cycling因为它本身就是箭头函数，在定义的时候，就是这么指向的，不会更改的，所以一个是window，一个是空的object。


- 把以上的输出改成如下，其他不变：
```js
const func1 = ming.climbing;
const func2 = ming.cycling;
func1();
func2();

// 把ming换成ming2

const func1 = ming2.climbing;
const func2 = ming2.cycling;
func1();
func2();
```
>结果：
- chrome：undefined、person
- Nodejs：undefined、person

>说明：
- ming2中，func2两个都指向了小person，因为在ming2中已经定义了。
- 定义好之后，即便把它拽出来，它看到自己的作用域是person，所以它依然是person。
- 所以ming3也是同样的道理，和ming2同样的结果.

***第二种情况：在const、function和class外面，把参数传进去***

```js
function climbing(){
    console.log(this)
}

const cycling = () => {
    console.log(this)
}

const ming = {
    name: "xiaoming",
}

function person(){
    this.name = "xiaoming2";
}

class Person {
    constructor(){
        this.name = "xiaoming3";
    }    
}

const ming2 = new person();
const ming3 = new Person();

ming.climbing = climbing;
ming2.climbing = climbing;
ming3.climbing = climbing;

ming.cycling = cycling;
ming2.cycling = cycling;
ming3.cycling = cycling;

ming.climbing();
ming.cycling();
```
>结果：
- chrome：{name:"xiaoming, climbing:fn, cycling:f} / window
- Nodejs：{name:"xiaoming, climbing:fn, cycling:f} / {}

>说明：
- climbing已经知道自己是谁了，所以前面输出object很好理解。
- cycling这个箭头函数，在这里定义的时候，只能寻找到window和{}。


```js
ming.climbing();
ming.cycling();

//换成ming2

ming2.climbing();
ming2.cycling();
```
>结果：和ming同样结果。
- chrome：{name:"xiaoming2, climbing:fn, cycling:f} / window
- Nodejs：{name:"xiaoming2, climbing:fn, cycling:f} / {}


```js
ming.climbing();
ming.cycling();

//换成ming3

ming3.climbing();
ming3.cycling();
```
>结果：和ming同样结果。
- chrome：{name:"xiaoming3, climbing:fn, cycling:f} / window
- Nodejs：{name:"xiaoming3, climbing:fn, cycling:f} / {}



>总结：
- 我们现在把函数在里面、在外面，以及送到里面去和把它拿出来，这几种情况全都看了一下。
- 三种不同object创造方式，以及两种不同的函数，我们都已经看到了。
- 下面看一个比较复杂的例子：在function和const里面再放置函数，看它会是什么样。


***第三种情况：把function和const里面再加上一层函数***

```js
function start(){
    console.log(this)
}

const stop = () => {
    console.log(this)
}

function climbing(){
    console.log(this) //因为它知道自己绑定的函数是ming3，出现的就是第一个person
    start(); //定义的时候不是很重要，运行的时候比较重要。这种情况下不具备持有者，climbing并不会把自己的this直接传到start里面。所以是undefined，它并不知道自己是谁。
    stop(); // window和{}。
}

const cycling = () => {
    console.log(this)
}

const ming = {
    name: "xiaoming",
}

function person(){
    this.name = "xiaoming2";
}

class Person {
    constructor(){
        this.name = "xiaoming3";
    }    
}

const ming2 = new person();
const ming3 = new Person();
```
>结果：见上面代码种的comment。

>说明：
- start不知道自己的this是谁。但是有一种方法可以绑定this，用bind绑定。
    ```js
    function climbing(){
        console.log(this) 
        start.bind(this); // 把this传进去。
        stop(); 
    }
    ```
- start.bind(this); 会产生一个新的函数，这个函数会绑定外层的this，把外层作用域下的this传到里面去，传完之后，我们再用()来执行函数。
- start.bind(this); 虽然是一个新的函数，但是它并不影响原来的函数start();
- 我们尝试在里面继续绑定this：
    ```js
    function climbing(){
        console.log(this) 
        start.bind({name: "Jessie"}).bind(this)(); //结果还是name。
        start.call(this, a, b);
        start.apply(this);
        stop(); 
    }
    ```
    - 它不能绑定第二次，虽然两个绑定写在这不会报错，但第二个绑定没有任何意义。
    - call和apply的区别在于：参数是什么.
    - call是线性的，a，b这么传。
    - apply只能传一个数组进去。

***以下是全栈班老师Mason讲课内容***

### 8.1 this

In most cases, the value of `this` is determined by how a function is called (runtime binding). It can't be set by assignment during execution, and it may be different each time the function is called. [[MDN](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)]\* \*[strict mode](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Strict_mode) is enabled by default in ES6 modules


#### 8.1.1 _this_ keyword in normal functions

```js
function foo() {
  console.log(this);
}
foo(); // window
```
>说明：
- 大多数情况下，this的指向取决于它所在的这个function是怎么被调用的。
- 如果function在调用的时候，前面什么都没有，我们通过function的名字来调用它，意味着这个function的this指向window。可以理解它是由window调用的。在打印的时候，this指向window。
- strict mode：严格模式。现在说的越来越少，几乎不说了。代码里几乎也看不到了。旧的可能还会有。了解即可。
- ES6默认开启strict mode。说白了就是让我们写代码的时候更规范一些。在没有初始化之前就使用。JS是有变量提升的。虽然有hoisting这个功能，但是我们不应该这么使用它，维护起来麻烦。可能看到一个变量，要拉到最下面才看到它的声明。严格模式就对这个进行了限制。
- 一般用this，都会写在一个function里面，所以在说this的时候，基本上都说function在被调用的时候指向哪里。
- 如果function在被调用的时候，直接通过名字被调用，说明它的指向是window。


#### 8.1.2 _this_ keyword in normal functions with bind, call, apply

```js
// a1,a2
foo.call({ number: 1 }); // {number: 1}
// [a1,a2]
foo.apply({ number: 2 }); // {number: 2}
// bind returns a new function
const bar = foo.bind({ number: 3 });
bar(); // {number:3}
```

>说明：
- 在非正常情况下，我们可以指定，我想让function的this指向某个具体对象，所以就会用到bind, call, apply。其中call和apply基本上一样。接收的参数，第一个参数为this所指向的对象。
- foo.call传入一个对象，里面有个属性叫number。
    - 用call的时候，同时可以传入其他参数。foo本身可能会接收一些arguments，比如foo接受a和b，在调用function的时候，需要导入相应参数，如果用call的方式指定this指向的话，我们可以在第二位和第三位传入foo所需要的参数。
    - 所以第一位是this指向。在调用foo的时候，指定this指向是哪里。
- apply的用法基本相同。
    - 唯一区别在于：上面是把foo所需要的参数一个一个传进入，apply是以一个array的形式传进去。
- bind会把this指向，重新定义的我们传入的这个对象，同时返回一个新的function。
    - 比如const bar = foo.bind({ number: 3 });这里，我给bar做一个赋值操作，前面两个call和apply是立马执行foo，而bind是返回一个新的function，只不过新的function的this指向了我传入bind的这个新的function里。
- 如果我们想手动的改变function this指向的话，可以用call、apply或者bind。
- 但是现在基本上不用手动的给它一个指向，稍后讲常用的用法。

>Q&A：
1. JS的this和Java的this很像，有什么区别？
- A：Java的this改变指向，应该是不行的：
    - Java里是用class的方式，object Oriental programming的方式做开发；
    - 而JS里没有class的概念，只有function概念，对于function来说，它的this，它每一次运行的时候、执行这个function的时候，这个this指向是动态的；
    - 对于Java来说，基本上当你创建完这个对象，这个this指向的就一定是一个固定对象了。


#### 8.1.3 _this_ keyword in an object and callback functions

```js
const calendar = {
  currentDay: 6,
  nextDay() {
    this.currentDay++;
    console.log(this.currentDay);
  },
};
calendar.nextDay();
```
>结果：7
>说明：
- 这里有一个calendar对象，它有两个属性：currentDay和nextDay，currentDay值是6，nextDay是一个function。
- function前面的对象是this的对象。
- 在这里，调用nextDay的时候，是通过calendar来进行调用的。nextDay的this会指向calendar。
- calendar有currentDay的属性的。所以结果是6+1，打印出来。


```js
const calendar = {
  currentDay: 6,
  nextDay() {
    setTimeout(function () {
      this.currentDay++;
      console.log(this.currentDay);
    }); // .bind(this)
  },
};
calendar.nextDay();
```
>结果：NaN
>说明：
- 什么情况下会得到NaN？NaN是Not a Number的缩写。
    - 当我们把一个数字和undefined，或无法转换成数字的这样一个value，进行相加的时候，我们会得到NaN。
- 这里为什么会输出一个NaN？
    - 所执行的这个函数setTimeout，我们传了一个callback function给它，这个callback function在调用的时候，就和calendar就没有什么关系了。
    - 这个function被谁调用的？是由window调用的。所以this会指向window。而在window里并没有currentDay这个属性，所以我们把undefined和1相加，最终得到NaN。
    - setTimeout这个function就和calendar没什么关系了。
- 解决这个问题最简单的方法，用bind。
    - 给这个function做一个bind，再传给setTimeout，这样这个function在执行的时候，这个function的this指向的是calendar。
- window是什么？
    - 在浏览器里，会有一个全局的对象，就是window，可以理解它为当前的浏览器页面。
- bind先要绑定到某一个具体的function上面。
    ```js
    setTimeout ((function () {
        this.currentDay++;
        console.log(this.currentDay);
    })).bind(this); 
    ```
    - function外面加上一层()，然后再加上.bind(this)，表示给这个function进行bind操作，bind会返回一个新的function。其实是创建好这个function，给它做一个bind，得到一个新的function，再把这个新的function传给setTimeout。
    - 我们bind的，既不是setTimeout，也不是nextDay，我们bind的是传给setTimeout的callback function。
    ```js
    const calendar = {
        currentDay: 6,
        nextDay() {
            const cb = function () {
                this.currentDay++;
                console.log(this.currentDay);
            };
            const bindedCb = cb.bind(this);

            setTimeout(bindedCb);
        }
    };
    calendar.nextDay();
    ```
    - 把这个代码做一个拆分：
        - 先设定一个cb（callback），让它等于function。先不做bind；
        - 再设定一个bindedCb，等于cb.bind(this)；
        - 再把bindedCb传给setTimeout；
        - bind是针对传入的function。

>Q&A：
1. 为什么function在setTimeout里就和calendar无关了？是因为异步吗？
- A：是因为异步。也可以如下这样理解：
    - 我们把bindedCb的reference传给了setTimeout，setTimeout会在一定时间之后执行；
    - setTimeout执行的时候，它只得到了function的reference。关于这个function之前什么样一无所知；
    - 如果没有做任何绑定，this指向的是window；
    - 现在做了一个手动绑定，绑定完之后再传给setTimeout，所以它在执行的时候就知道，指向的是当前nextDay的this，而nextDay的this指向了calendar。因为在调用nextDay的时候，是通过calendar调用的。
    - nextDay这个function是立即执行的。只不过bindedCb不是立即执行的。
2. 用bind是为了什么？
- A：bind的目的是确保，我们这个callback function，它的this指向不会丢。如果不用bind，这个this就会指向window。


#### 8.1.4 _this_ keyword in arrow function

In arrow function, `this` points to the enclosing lexical context's `this`.

```js
const calendar = {
  currentDay: 6,
  nextDay() {
    setTimeout(() => {
      this.currentDay++;
      console.log(this.currentDay);
    });
  },
};
calendar.nextDay();
```
>结果：7
>说明：
- 在arrow function里面，this永远指向自己上一级作用域下this的指向。
- arrow function的this取决于arrow function写在哪里，通过它的*词法作用域*往上查找。
- 这里，包裹arrow function的作用域是nextDay。
- 接下来看nextDay的作用域指向哪里？
- 普通function的this是由调用那一刻决定的，调用的时候，是通过calendar.nextDay的方式。也就是说nextDay这个function在执行的时候，它的this会指向calendar。也就是setTimeout里面的这个function也会指向calendar。


>Q&A：
1. arrow function里的this和普通function里的this有什么区别？  
- A：arrow function里的this永远取决于包裹它的作用域里面的this。如上面代码：
    - arrow function是由nextDay包裹的，所以arrow function的this取决于nextDay的this是什么；
    - 而nextDay的this指向哪里呢？调用nextDay这个function的时候，才知道的；
    - 我们执行它的时候，是通过calendar.nextDay方式调用的；
    - 所以，对于nextDay这个function，它在这一刻，this指向的是calendar。
    - 因为nextDay指向calendar，arrow function也会指向calendar。
2. 为什么不是setTimeout包裹arrow function？
- A：setTimeout有自己的function，我们现在是传入一个参数给setTimeout，setTimeout它自己的function是在它的function定义里面，而不是在我们调用它的时候。在调用的时候，它是没有自己的作用域的。
3. 用arrow除了节省代码量，还有什么好处？
- A：第一是节省代码量。
    - 第二解决了this的指向问题。不用管传参的时候这个this指向哪，只需要知道arrow function在哪，它就会指向包裹住这个arrow function的这个作用域的this。
    - 第三个好处：（老师个人偏好）更简洁，看起来更舒服。
4. 以后几乎都用arrow function。它减少了很多麻烦。


```js
const calendar = {
  currentDay: 6,
  normal: function () {
    console.log(1, this);
    setTimeout(function () {
      console.log(2, this);
    });
  },
  arrow: function () {
    console.log(3, this);
    setTimeout(() => {
      console.log(4, this);
    });
  },
};
calendar.normal();
calendar.arrow();
```


#### 8.1.5 quiz


***第一题***

```js
const object = {
  message: 'Hello, World!',

  getMessage() {
    const message = 'Hello, Earth!';
    return this.message;
  },
};

console.log(object.getMessage()); // ??
```


***第二题***

```js
const object = {
  who: 'World',

  greet() {
    return `Hello, ${this.who}!`;
  },

  farewell: () => {
    return `Goodbye, ${this.who}!`;
  },
};

console.log(object.greet()); // ??
console.log(object.farewell()); // ??
```
>结果：
Hello, World!
undefined
>说明：
- greet是个普通的function，在调用的时候，是谁调用它？它在调用的时候，是通过object，也就是object.greet，所以greet的this是指向object，object是有who这个属性的，所以是Hello, World!
- arrow function的作用域取决于包裹住它的上级作用域，这里包裹住它的作用域是哪儿呢？这里的{}不是指作用域，而是一个object，object的{}不构成一个scope，所以farewell的作用域实际上是外面的global，所以这里的this指向的是window。window里没有who这个属性。所以结果是undefined。
- object内部的赋值实际上是这样的：object literal（对象自变量）
    ```js
    const object = {};
    obj.farewell = () => {this};
    ```
    - 这个this指向哪里，应该很明显，包裹arrow function的scope是global scope。
    - 所以object的{}不构成作用域。
    - object literal里面定义的所有属性，都是以这样的方式赋值上去的。


***第三题***

```js
const object = {
  who: 'mason',
  cb() {
    console.log(`Hello, ${this.who}!`);
  }, // 在这里return this的话，this指向是window。
};
// 如果让this指向object，先要在这里些一个arrow function，在这个arrow function里面做一个return this。

function foo(cb) {
  cb();
}

foo(object.cb); // ??
object.cb(); // ??
```
>结果：
Hello, undefined
Hello, mason
>说明：
- 第一个为什么是undefined？
    - foo()拆分：
    ```js
    const cb = object.cb;
    foo(cb);
    ```
    - cb是一个function，赋值的时候，并不会把它的function拷贝之后赋值过去，而是把它的引用赋值过去。所以我们其实是得到了这个function的引用。就是cb = object.cb。
    - 在调用foo的时候，并没有调用cb，我们只是把cb以传参的方式再传给了foo，而foo什么时候执行它的呢？在661行，是当它进入到这个参数以后，再执行。
    - 当cb()执行的时候，这个function是没有任何前缀的，没有对象在执行它，它的执行对象其实是window。
    - 所以最终这个function里面的this指向的是window，而window里面没有foo这个属性。
- 当我们把一个function赋值给一个object的时候，我们赋值的是它的引用地址，就是它的reference，所以cb这个variable的值就是一个普通function，现在把cb这个普通function的引用（一个reference）传给foo这个function，foo接收到了一个普通function，调用一个普通function，在调用的时候，前面没有加入任何的对象，它的this指向的是window。
- object不构成block scope。


***第四题***

```js
const object = {
  who: 'mason',
  cb() {
    function foo() {
      console.log(`Hello, ${this.who}!`);
    }
    foo();
  },
};

object.cb(); // ??
```
>结果：
Hello, undefined
>说明：
- 通过object.cb()的形式执行cb()这个函数，这个时候，cb里面的this指向的是object。
- 但是在整个cb的逻辑里面，是没有直接出现this的。我们是在foo这个function里用到的this。
- foo这个function里面的this，是谁调用它，this指向谁。我们在调用foo的时候，没有指明谁调用它。这里我们直接调用foo，它的this就会指向window，所以最终得到undefined。
- 如果foo是个箭头函数，this指向就是cb。

>Q&A：
1. object.cb.foo是指向object吗？
- A：object.cb里面是没有foo这个属性的。这里既没有return，也没有说cb是一个object，cb在这里是一个function，现在这个逻辑是处在cb的function里面的。
2. 为什么object.cb会用到foo？
- A：因为这段逻辑是写在cb里面。我们在执行cb的时候，我们才会执行这段文件。我们执行代码的时候，碰到function先放到一边不管，只有实际执行这个function的时候，才会看这个function里写的逻辑是什么。
- 这里object有个cb的属性，cd的值是一个function，除此之外我们不用管。只有我们执行它的时候，才会看function里面的代码是这样的。执行时，先创建一个foo变量，它的值是function，然后执行这个function。
3. 什么情况下foo是由cb调用的？
- A：foo作为一个普通function，不会由cb来调用。foo不是cb function的某一个属性，它只是cb function里面的一个普通function而已，它的this和cb的this没有关系。如果一定要有关系，先要把foo变成一个arrow function或者加上bind。
4. 怎么样让foo变成cb的一个属性？function也可以有属性吗？
- A：可以的。
- function是一个特殊的object，可以给它加属性，只不过更绕。在开发中也不会这么使用它。因为它虽然支持加属性，但是理解起来会很confused，所以在使用的时候也不会这么使用。
- 如果是function，我们就把它当function使用；如果是object，我们就把它当object使用。
5. 带function关键字的普通function，是不是都指向window？
- A：绝大多数情况下，它都是指向window的，只有把它放在一个object里面，作为一个属性值的时候，在调用的时候，如果是通过object.XXX调用时，这个普通的function才会指向object。
- 还有一种情况，把这个function做一个bind，或者call、apply，这种情况下会指向指定的对象。
- 其他时候都是指向window。
6. 什么场景下，我们需要把function放入object？
- A：很多场景下。object下有一个属性是function很常见。
- 调用的时候，是通过object.XXX的方式，所以function里的this，99%都会指向object。


### 8.2 Common array operations


#### 8.2.1 Manipulation

```js
const fruits = ['apple'];

fruits.push('pear');
console.log(fruits); // ["apple", "pear"]
fruits.unshift('grape');
console.log(fruits); // ["grape", "apple", "pear"]
// splice(x,y,newAdded)
// remove y items from index x, and add newAdded
fruits.splice(1, 1, 'watermelon', 'peach');
console.log(fruits); // ["grape", "watermelon", "peach", "pear"]
let fruit = fruits.pop();
console.log(fruit); // pear
console.log(fruits); //  ["grape", "watermelon", "peach"]
fruit = fruits.shift();
console.log(fruit); // grape
console.log(fruits); // ["watermelon", "peach"]
```
>说明：
- array是一个数据结构，大多数语言中，都是非常常用的数据格式。
- 通常情况下，我们会把同样类型的数据，都是字符串，都是数字。或者同一类型object，里面都有name属性，age属性，放到一起，统一管理，这时会用到array。
- array无外乎就是增删改查。
- 查找和删除都会遇到遍历。我们需要检索每一个element，来查找想要寻找的对象，所以需要做遍历。
- 添加可以用push，push是在尾部添加；可以用unshift在头部添加。
- 做删除，可以用splice(x,y,new elements):（从中间的某一部分开始添加）
    - 从index x开始，删除y个items，然后再加上new elements。
    ```js
    const fruits = ["grape", "apple", "pear"];
    fruits.splice(1, 1, 'watermelon', 'peach');
    console.log(fruits); // ["grape", "watermelon", "peach", "pear"]
    ```
- 如果只想对尾部进行操作，把最后一位删掉，可以用pop；把第一位删掉，用shift。


#### 8.2.2 Iteration（遍历）

***for loop***

```js
const fruits = ['apple', 'pear'];
for (let index = 0; index < fruits.length; index++) {
  const fruit = fruits[index];
  console.log(fruit);
}
// apple
// pear
```

***for...of***

```js
const fruits = ['apple', 'pear'];
for (let fruit of fruits) {
  console.log(fruit);
}
// apple
// pear

// for...in -> 0, 1    usually used in object
```

***forEach（最常用）***

```js
const fruits = ['apple', 'pear'];
fruits.forEach((fruit) => console.log(fruit));
// apple
// pear
// cannot use break here
```
>说明：
- forEach就是我们把element里面的每一项取出来。
- 本代码中，forEach里面有一个callback，可以理解为循环每次取一个元素出来，执行这个callback。所以这里的fruit就等于当中的每个元素。
- forEach和for loop的区别：
    - forEach不能提前终止；for loop可以提前终止，加一个break。


#### 8.2.3 Map（非常常见）

```js
const fruits = ['apple', 'pear'];
const newFruits = fruits.map((fruit) => ({
  name: fruit,
  price: 10,
}));
console.log(newFruits);
// [{name: "apple", price: 10},{name: "pear", price: 10}]
```
>说明：
- 当我们想要对原始数组做一些修改，同时创建一个和原始数组同等长度的数组的时候，用map。
- 例如：现在数组长度是2，用map也是做一个遍历，只不过它取出来之后，我们会做一个return，简写了，我们加了一个{}，其实是return。
- 我们把fruit的name取出来，然后创建一个新的object，里面有name属性，然后加一个price。
- 因为我们做了return操作，可以理解为，我们的原始array是['apple', 'pear'],map会创建一个新的array，长度和原始array是一模一样的。
- 现在是在做遍历，把apple取出来，做完一些操作，在callback里会return，return的对象最终就会等于我们在新的array里面同样位置的元素，就是用callback function里面的return出来。

>Q&A：
1. map里的信息会不会修改？
- A：map的信息会不会修改，取决于信息的类型是什么。
    - 如果是object，在callback里面对object进行修改，它就会修改原始的数据。因为它是一个reference，reference的任何修改，会反应到所有引用这个reference的对象上面。
    - 所以取决于它的类型是什么，以及如何修改。
- 一般对一个object做进行map操作，
```js
fruits.map(fruit => ({
    ...fruit, 
    // 把fruit做一个spread，spread目的是做一个浅拷贝，让它里面的每个值都展开出来，跟原本的object就没有任何关系了，然后可以添加新的字段。
}))
```  
或者写成
```js
fruits.map(fruit => ({
    const newFruits = {...fruit}
    // 先拷贝出来一份，然后对newFruit进行相应的更改
}))
```  


#### 8.2.4 Reduce

```js
const numbers = [1, 2, 3];
const sum = numbers.reduce((accumulator, number) => accumulator + number, 0);
console.log(sum); // 6
```
>说明：
- 老师说他不太常用。



#### 8.2.5 Search

***indexOf 和 findIndex***

```js
const numbers = [1, 2, 3, 4, 5];
console.log(numbers.includes(2)); // true
// Array.some
console.log(numbers.indexOf(2)); // 1
// Array.findIndex
```
>说明：
- 在array里面搜索我们感兴趣的element，用includes来看它是否存在，是否在array里面。
- 也可以用array.some，是当array里面的element比较复杂的时候，不再是primitive type，是object的时候，可以用some。
- indexOf是找到当前这个element的index。
- primitive type用indexOf，object类型会用到array.findIndex.



***filter***

```js
const numbers = [1, 2, 3, 4, 5];
const odds = numbers.filter((i) => i % 2);
console.log(odds); // [1,3,5]

const fruits = [
  {
    name: 'apple',
    color: 'red',
  },
  {
    name: 'pear',
    color: 'green',
  },
  {
    name: 'grape',
    color: 'green',
  },
];
const filteredFruits = fruits.filter((i) => i.color === 'green');
console.log(filteredFruits);
// [{name: "pear", color: "green"}, {name: "grape", color: "green"}]
```
>说明：
- 和map类似，区别在于：
    - map会返回一个一模一样的array。
    - filter不是，在callback function里面如果返回一个true，意味着这个element通过了筛选，只有通过了的element，它才会被添加到返回的array里。
    - 上句话里的这个array，如果element类型是object，对这个array里面的数据进行更改，也是一样会反应到原本的数据上的。
- 所以在做filter的时候，如果对array进行操作，最好把它做一个spread或者clone，deep clone。


```js
const fruits = [
  {
    name: 'apple',
    color: 'red',
  },
  {
    name: 'pear',
    color: 'green',
  },
  {
    name: 'grape',
    color: 'green',
  },
];
const greenFruit = fruits.find((i) => i.color === 'green');
console.log(greenFruit);
// {name: "pear", color: "green"}
```

#### 8.2.6 Extra reading source

[link](https://dmitripavlutin.com/operations-on-arrays-javascript/)




### 8.3 Set

>说明：
- set也是一个数据结构，和array很类似。
- 区别：set储存独一无二的数据。

Set is a data structure, we use it to store _unique_ values.

```js
const set = new Set([1, 2, 3, 4, 4]);
console.log(set); // Set(4) {1, 2, 3, 4}
set.add(5);
console.log(set); // Set(5) {1, 2, 3, 4, 5}
set.add(1);
console.log(set); // Set(5) {1, 2, 3, 4, 5}
console.log(set.has(5)); // true
set.delete(1);
console.log(set.has(1)); // false
console.log(set.size); // 4
```
>说明：
- set的好处在于：可以快速查询某一个元素是否在set里: set.has()
- set.add(), set.has(), set.delete(), set.size
- set.size: 看当前有多少给unique元素。
- set最常用的用法：（set本身用的比较少）
    - 有一个array，我们想取它里面的unique values；
    - 我可以先把array传给set，让set把重复的元素排除掉；
    - 再把set做一个spread，把它展开；
    - 最终得到了一个array，array里面的元素都是unique的。


```js
const array = [1, 2, 2, 3, 4, 4];
const uniqueArray = [...new Set(array)];
console.log(uniqueArray); // [1, 2, 3, 4]
```

>Q&A：
1. object.function是object的function，其他的function都算是window调用的。
- A：基本上是这样的。
- 例外是bind。我们明确的指定了function指向了某一个object。但是一般不这么做。
2. {} => (x) 和 {} => x 什么区别？x = object
- A：{} => (x)：如果想return一个object，因为object它自己也有一个{}，这个{}会和外面的搞混，所以为了区分他们，我们会加一个().
3. 什么情况下不适用箭头函数？比如说事件监听的箭头函数就没有意义。
- A：事件监听。
- 计算器的addEventListener，它的this就必须指向调用的那个对象，必须指向实际触发事件的那个对象，所以不能用arrow function。
- 如果用arrow function，这个this就和这个事件没有关系了，因为arrow function的this永远指向包裹arrow function的上级作用域。
- 所以像addEventListener这种情况，我们必须用普通function，不能用arrow function。


### 8.4 Basic Classes

Classes are a template for creating objects. Classes are in fact functions, class is only a syntax sugar（语法糖）.
>说明：
- class讲的不会很深，只讲讲怎么用。
- class涉及到JS的一个核心：原型链（prototype chain）。这个在课上不会讲到，可以作为课外阅读。
- 我们想要创建对象的时候，我们用class帮助我们搭建一个模板，通过这个模板，更快地创建一个我们想要的对象。


```js
function Person(name) {
  this.name = name;
  this.toString = function () {
    console.log('name: ' + this.name);
  };
}
var mason = new Person('mason');
mason.toString(); // name: mason
```
- 在没有class关键字之前，我们是用function。
- function的名字是大写Person，大写代表这是一个class，用JS的话说，这是一个模板function，用这个function来初始化一些对象。
- 在这个function里面，我们用到的this，我们在使用它的时候，会用到new这个关键字。
- 不加new这个关键字，这个函数就是一个普通的function：
    - 如果有return，就是它return的值；
    - 如果没有return，它就会返回undefined。
- 加了new这个关键字，可以理解为，他会给我们返回一个对象，这个对象就等同于我们function里面的this。
    - 调用mason.toString();的时候，toString();声明在function()这里，并且绑定到了this上面，this是一个对象，我们在用new这个关键字的时候，最后new所干的其中一件事是在function的最后把this作为一个返回值返回出来。这也是为什么我们可以把new Person给它赋值到一个对象上，因为这个function在用了new关键字之后，它会把this这个对象返回出来。这也就是说为什么mason等同于this，然后我们为什么可以通过mason.toString()的方式调用使用这个函数。
- 这是用function的写法，这是为了创建一个类似class的概念写成这个奇怪的样子，它既不像JS里正常function的样子，和Java里class也不一样。所以在ES6里加入了class的关键字。
- class出来之后，再创建模板的时候，就可以使用class了，和Java种定义一个class的方式几乎是一样的。只不过在编译阶段，它会把class再转换成JS里的function。让我们在书写代码的时候更方便一些。本质上仍然是function。


```js
class Person {
  constructor(name) {
    this.name = name;
  }
  toString() {
    console.log(`name: ${this.name}`);
  }
}
const mason = new Person('mason');
mason.toString(); // name: mason
```
>说明：
- 在class里，首先会有一个constructor function，就是它的构造函数，在初始化和创建一个Person对象的时候，它需要接收哪些参数？
- 首先传入这个person的name，在构造函数里加入这个参数，这个person想要初始化成功，是需要给他传入这样一个name信息的。
- 然后这个person所具有的所有的能力，就是这个对象能干什么，直接写在这，跟我们定义一个普通的object非常类似。
- 这个class创建好以后，如果想通过这个class创建一个新的对象，加上new关键字。

>Q&A：
1. class种一定会有constructor吗？
- A：不是。
- 如果class不需要接收任何参数，比如不需要接收name等，就不需要constructor。
- 默认是不接收任何参数的。
- 如果想让他接收参数，才需要加这个constructor function。
2. 接收的所有参数都要放入constructor吗？
- A：对。
- 用到的所有参数，如果是从外部传进来的，都需要放在constructor的传参里面。



### 8.5 extends（继承）

```js
class Teacher extends Person {
  constructor(name) {
    super(name); // 指代person的构造函数
  }
  teach() {
    console.log(`${this.name} is teaching`);
  }
}

const mason = new Teacher('mason');
mason.teach(); // mason is teaching
mason.toString(); // name: mason -> BUT how?
```
>说明：
- 继承的目的：为了把Person所拥有的说有的属性和它的function，Java说是全部继承给它的子类。用JS的话说，把他们在原型上关联起来。
- 这里就是，我们想用extends这个关键字把Teacher这个class和Person这个class关联在一起。
- 他们关联之后有什么好处？
    - 我们可以给Teacher这个class添加一些只属于Teacher的属性。
    - 在创建Teacher的时候，因为Teacher继承于Person，而Person需要传入name来初始化的，所以我们在初始化的时候，也需要传入name。
    - Teacher创建好之后，我们通过new Teacher()的方式创建好这样一个Teacher的实例之后，Teacher既可以访问它自己的method，也可以访问它继承的Person的method，比如toString。
    - 这就是我们做继承的目的。它能够访问到toString，是因为Teacher和Person是继承关系。或者说在原型上，他们有关联。



```js
// is mason constructed by Teacher?
mason instanceof Teacher; // true
mason instanceof Person; // true
mason instanceof Object; // true
```
>说明：
- 我们的继承关系，常常被用来做instanceof的检测。
- 就是检测这个对象它是不是一个Teachcer的instance。
- instanceof叫做实例，所以我们检测一下mason是不是Teacher的实例，或者说mason是不是由Teacher这个class（function）初始化出来的。因为Teacher继承于Person，mason间接由Person创造了出来。
- 原型链最顶端是object，用JS的话说，最老的这个class是object。


### 8.6 quiz

```js
function Pet(name) {
  this.name = name;
  this.getName = () => this.name;
}

const cat = new Pet('Fluffy');

console.log(cat.getName()); // Fluffy

const { getName } = cat;
console.log(getName()); // Fluffy
```
>说明：
- 第二个输出：
    - { getName }是个解构赋值，我想要从cat当中，把getName这个值取出来。
    - GetName是个function，并且是一个arrow function，arrow function的作用域取决于它的上级作用域，包裹它的上级作用域是pet这个function，而pet这个function，因为我们用的new这个关键字，当我们创建pet这个对象的时候，这个this就已经绑定到cat身上。
    - 虽然我们是把cat摘了出来，这个this仍然指向cat。
    - 注意：cat是一个object，不是一个函数。我们解构的是object。
- 箭头函数后的this指向的是new前面的cat，原因在于：我们用new关键字的时候，等同于把this.getName种的this返回了回来。const cat中的cat等同于this.getName的this。
- arrow function的this指向的是包裹它作用域的this，即this.name中的this。
- 综上，所以说，arrow function最终指向的是const cat中的cat。cat有name属性。

>Q&A：
1. 假如getName是个普通function，我们会得到undefined。
2. 如果去掉const { getName } = cat;会报错，getName不存在。


### 8.7 Asynchronous（异步） in JS

>说明：
- 异步 | 同步：
    - 同步：从上到下，一行一行执行的代码，一次就执行一行。
    - 异步：像setTimeout这种情况，需要等待一个倒计时的完成，等它倒计时完成，我们再回来执行。
    - 举例：有一个页面，请求一个数据或图片，数据传输的时间单程需要半秒钟，来回需要1s，从需要的地方到下载到电脑上共1s的时间。
        - 如果是同步的方式获取这个图片，意味这1s的时间内，我们什么也干不了。同步的代码一次只能做一件事情。因为JS是一个单线程语言，作为单线程，一次只能做一件事情。这显然不是一个很有效的处理方式，我们取数据的时候，用户仍然能够和我们的页面进行交互，而不是页面一动不动。
        - 【题外话】：页面的渲染和代码的执行用同一线程。要么在渲染页面，要么在执行JS代码，不会同时进行。我们要保证页面显示的一致性。不能多个地方同时修改页面上的内容。
        - 【题外话】：线程 | 进程（课下了解）
            - chrome浏览器，同时可以开多个tap，可以理解为每个窗口都是独立的线程。每个tap都是独立渲染的。
            - 除了tap之外，chrome可能有更新机制，用户登录机制，这些内容又是独立的线程。
            - 进程：开启chrome应用程序本身。在这一个应用程序里，可以把它拆分成多个线程。
            - 一个进程里可以拆分成多个线程，每个线程每次只能做一件事情。
        - 如果它一次只能做一件事情，请求数据的工作就会阻塞页面渲染，阻塞其他代码的运行。
            - 阻塞 | 非阻塞：阻塞代表同步；异步代表非阻塞。
        - 如果从上到下一步步执行代码，当我们遇到一个非常耗费时间的操作的时候，代码实际被阻塞住了，它在等待命令执行完再继续。
        - 异步就像计时器一样，让计时器在另外一个线程上进行工作。
        - 之前说JS是单线程，另外的线程是哪里来的？稍后会说。
        - 异步会在另外的线程上工作，计时器是另外一个线程的倒计时。异步的用处就是让我们不再对请求阻塞住。我们的代码可以执行，页面可以进行正常的渲染。用户仍然可以在页面上进行交互。计算器会在另外一个进程上倒计时。

>Q&A:
1. 进程是Windows操作系统里面的东西吗？再讲一下进程和线程。
- A：对于JS来说，不用太关心进程怎么回事。
- 理解：每个程序在开始的时候，系统都会给它分配一个进程。在这个程序里，会有多个线程做不同的事情。
- JS代码的执行是单线程的。它有什么东西不是单线程的呢？由JS引擎提供的一些东西不是单线程的。其中包括倒计时，setTimeout不是一个单线程，如果它是一个单线程，它永远会卡在那里。
- 我们想正常执行其他的代码，异步代码在一旁先等待，让其他线程帮我们处理。
2. 异步其中一个作用就是解决单线程的问题。
- A：对，它最主要的目的就是为了解决这个单线程。不会被阻塞。
3. 面试会考这些吗？
- A：非常大的概率会考什么是异步。异步在JS里是怎么工作的。
- 他不一定考你原理是什么，或者为什么要有异步。（一般是common sense）
- 一般会有一些题，看你对于异步是否了解。
- 异步无处不在，不管是前端还是后端，都有异步。
- eg：sever要监听事件，主线程不可能一直盯着事件，其他线程在监听这个事件是否触发，就是是否有请求进来。（稍后会学习Nodejs工作原理）
- 我们在做一件事情的时候，不被其他事情所干扰。先把这个事情放到一边，自己的事情干完了，再说放到一边的事情。放到一边的事情，其实就是异步操作。
4. JS的引擎就是指chrome浏览器吗？
- A：不是。
- 引擎是JS能够运行的根本所在，chrome是基于V8引擎的。V8是google自己开发的一个nodejs的引擎。引擎每一家的实现不太一样，这也是导致有些代码在不同的浏览器上会有细微的差别。


JS is single threaded, which means it can only execute one command at a time.

```js
function foo() {
  console.log('foo');
}
setTimeout(foo, 1000);
console.log('hello');
```
>结果：
hello
foo（foo是在1s之后打印的）
>说明：
- 整个代码执行过程：
    - 首先创建一个变量foo，foo是一个函数，里面写什么我不关心。
    - 调用setTimeout这个function，传入foo，1000毫秒。
    - 打印。
- setTimeout到底干了什么？
    - setTimeout这个function不是JS提供给我们的。
    - 在当前环境下，是浏览器提供给我们的。浏览器给我们提供了一系列的function或功能，这个功能叫做timer（计时器）。setTimeout是其中一个。
    - timer的功能是浏览器提供给我们的。它提供给我们的方式就是一个函数，可以被我们调用，来触发这些功能。
    - setTimeout就是，当我们需要设置一个计时器的时候，我们传一个callback function，传的就是一个reference，把这个reference传给浏览器，同时把时间传给浏览器，到底是多少秒。
    - 浏览器这边可以理解为它有自己的线程。它给我们一个单独的线程用来倒计时。
    - 以上就是setTimeout所干的事情。
- 执行一个函数的三要素：
    - 函数名
    - ()
    - 函数的参数
- 执行一个函数才加()；如果想传递一个函数，传它的引用，我并不执行它，是不加()的。



```js
function foo() {
  console.log('foo');
}
function runFor1Sec() {
  // a for loop or while loop or a heavy computing logic which requires 1 sec to finish
}
setTimeout(foo, 1000);
runFor1Sec();
console.log('hello');
```
>结果：
hello
foo（foo是在1s之后打印的）
>说明：
- 这里加了一个新的function，叫做runFor1Sec();，没写具体逻辑，但是想告诉我们说，这个函数它会跑1s，并且它真的需要1s实行。
- 在实际代码当中怎样触发一个1s的同步代码呢？
    - 写一个for loop or while loop，循环500w次，大概会等待1s。
    - 或者可能是一个需要大量计算的一个操作，这个函数需要跑1s。
- 有了这个function之后，在setTimeout后面执行它，然后再运行，打印。
- 这里会不会出现一个比谁更快的问题？
    - 比如这里setTimeout 1s后执行；
    - 然后我有一个函数需要执行1s；
- 我的倒计时只有1s，它应该在runFor1Sec前面，倒计时就结束了，是不是意味着要来执行foo了？
    - A：不是。
    - 我们仍然要等runFor1Sec执行完，并且兼打印console.log，然后再执行foo。
    - 为什么是这样？
        - 如果我们允许它在1s后立即执行foo，就会出现一个非常不确定的情况：我的foo到底在什么时候执行？
        - 是1s之后吗？1s之后不管在干什么都执行；
        - 如果它立即执行，我不能确保说它到底是在哪个代码后执行。可以在后面代码任何时候执行。如果我允许它在1s后立马执行。
        - 另外一个机制是它要进行一个等待。
- event loop


Quiz questions references
[1](https://dmitripavlutin.com/javascript-this-interview-questions/#question-1-variable-vs-property)
