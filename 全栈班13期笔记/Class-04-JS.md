# Class-04 JavaScript
## 主要知识点
  - [1.重温网页三剑客](#1-html--css--js)
  - [2.什么是JavaScript](#2什么是javascript)
  - [3.变量Variable](#3变量variable)
  - [4.数据类型](#4数据类型)
  - [5.条件语句 Condition](#5条件语句-condition)
  - [6.循环语句 Loop](#6循环语句-Loop)
  - [7.函数 Function](#7函数-Function)
  - [8.Object 对象: 最重要的数据类型](#8Object-对象最重要的数据类型)
  - [9.DOM: javaScript操作网页的接口](#9DOMjavaScript操作网页的接口)
  - [10.课上练习: 写一个clock的网页](#10课上练习写一个clock的网页)
  - [11.JS异步加载](#11JS异步加载)


## 课堂笔记


### 1.HTML + CSS + JS
- HTML: 做content structure
- CSS: 做layout design，styling
- JS: 与user交互的桥梁，捕捉用户的操作，用户data（给backend）的传递
  - 在澳洲找第一份工作不会考察太深的js内容
- 推荐书籍： Refactoring
### 2.什么是JavaScript
- 首先是编程性语言
    - CSS, HTML, 都不是编程性语言，无法做逻辑性运算不是图灵完备的。
    - 图灵完备：https://www.zhihu.com/question/20115374
    - 高级语言（例如C#,JAVA）都跑在一个自己的运行环境里面，运行环境负责好了跟操作系统的交互，因此写起来很方便。
- JavaScript也是一个高级语言
    - 曾经只作为跑在browser里的一门语言，现在多了一个运行环境（nodejs），只要能安装nodejs的地方，就能运行js；nodejs可以运行在多种设备上，从大设备到小芯片，都可以加载。
    - Javascript可以从前到后一条线贯穿，frontend可以用，也可以做back-end service, 一样能做middle layer（中间层）的back-end for frontend。
    - 本身不是一门严谨的语言
       - weekly type, runtime时不会检查变量类型；写的时候可以动态的改变变量type
    - JavaScript跟Java并没有联系，只是蹭热度而已。
- ECMAScript: 一个标准，规定了满足ECMAScript的语言具备哪些语法特性；相当于基本决定了JavaScript的方向
    - JavaScript fatigue: JavaScript突然有一天进行了大量更新，令很多developer焦虑于对新特性的学习。
    - 2009～2015（ES6）:没有更新过，因此积累了大量的更新(语言特性)
    - ES6(2015)年带来了很多语言的新特性，之后就是慢慢在更新了
- 怎么测试运行
   - Chrome里，右键select inspect element, 然后console里直接敲代码(日常coding必备)
- 怎么写入网页
   - 嵌入在browser，HTML中直接加入`<script>`，例如  
     ```
     <script>
        console.log("Hello World!")
     </script>
     ```   
    - 引入式，HTML中加入引用文件，例如  
     ```<script src="./index.js"></script>```
- nodejs里运行JavaScript:首先要安装node(https://nodejs.org/en/download/)
  - 在Terminal下，敲`node`进入nodejs环境，然后输入JavaScript，类似于上面Chrome Dev Tools的console
  - (主要方法)或者在Terminal下，直接node引用js文件，例如  
  ```node index.js```
- VS code里运行js文件
  - 也可以通过安装code runner的插件
  - 写完代码后，右上角会有run图标，但是该插件不太稳定

### 3.变量Variable
- 相当于一个盒子，你在里面存了一样东西，东西可大可小
- 声明：
  - `var + <变量名>`, 例如  
   `var name;`
  - ES6中使用`let\const`
- 赋值：
  - `<变量名> = '<变量值>'`,例如  
    `name = 'Gary';`
  - 如果变量没有赋值被直接引用，变量结果为`undefined`
- `undefined` VS `null`
  - `undefined`: 声明了，却没有赋值；或者(该变量)不存在
  - `null`:存在，但没有赋值（实际系统已分配内存给该变量）
  >`null`可以理解为，人为定义该变量没有（赋空值），`undefined`可以理解为，JavaScript认为该变量不存在 
- 变量提升(hoisting）：编译器会自动把声明提升到 赋值前面去
  - 变量声明如果在`function`里, 它会自动提升到`function`的头部
  - 变量声明如果不在`function`里, 它会自动提升到文件的头部
  - ES6之后，开始使用`let\const`, `let\const`变量将不再做变量提升
- 动态类型(dynamic)：
  - JavaScript并不会绑定一个变量的类型，例如  
    ```
    var name = 'Gary';
    console.log(typeof name);
    ```   
   - `output`结果应为`string`,但是如果`name`在中间赋值 `name = 32`,最终`output`结果应为`number`
   - 类型只会绑定在值上，而不会绑定在变量上
   - `use strict`:在js文件的首行加入，会令js文件的编译进入strict模式，如果变量没有声明，则后面调用会报错
- 命名规则：
  - UPPERCASE:全大写
  - camelCase(最常用):第一个单词小写，从第二个单词开始，首字母大写
  - PascalCase(不常用):所有单词首字母大写
  - under_score:单词间用单下划线
  - hyphen:单词中间加`-`
  - 命名不能以数字开头
  - 命名中避免出现number,最好解释一下，除非做演示代码
  - 命名中避免出现乱七八糟的符号，除了`_`和`$`
  - 不能使用系统保留字符：`if`,`else`...

### 4.数据类型
- 简单数据类型
  - 数值（number）:整数和小数，包括`infinity`(无限大)，`NaN`（not a number）
    - 因为JavaScript没有float类型，在小数计算的时候要特别注意，容易出问题，例如  
  `0.1 + 0.2`  
  结果为`0.30000000000000004`  
  因此JavaScript做数据计算的时候需要用到额外的库，比如`numbers - npm`   
  >JavaScript很少用来做数据计算，数据计算基本被python垄断了
  - 字符串（string）:字符串
  - 布尔值（boolean）:`true`和`false`
  - `undefined`:表示未定义或不存在, 在GraphQL已经被严格限定
  - `null`：表示空值（即赋值为空）
  >简单数据类型记录的是一个确切的值
- 复杂数据类型
注意下`map`和`set`，后面用的比较多
  - object：有很多简单类型构成，各种值组的的集合，例如
    ```
    var person = {
        name: null,
        age: '32';
    }
    ``` 
    `person`存的是值组合的引用地址（reference），假如有    
    `var person2 = person;`  
    那`person2`将同样指向`person`的值组合,即`person2`赋值了`person`的引用地址  
    如果只要copy object的值，需要使用  
    ```var person2 = Object.assign({},person1);```  
    或者
    ```const person2 = { ...person};```
  - Array(隶属于object)：存储多个值在一个引用里
    - 声明：`var ages`
    - 赋值：`ages = [];`
      - 可以赋值不同类型的数值，例如 `ages = [12,'12',{}];`
      - 二维数组：`ages = [[12,'12'],[],[]];`
    - 访问：`ages[0]`
      - 访问二维数组：`ages[0][0]` 
    - 得到数组的长度：`ages.length`
    - 尾部添加新元素：`ages.push(4);`
    - 尾部删除元素：`ages.pop();`
    - 选择部分值，创建一个新的数组：`ages.slice()`;
    - 头部添加新元素：`ages.unshift(4);`
    - 头部删除元素：`ages.unshift();`
    - `map()`:对原array中对每一个元算执行一个方法，然后返回一个新的array
   > 现在开始去阅读MDN了解更多array和object的常用方法：比如`forEach()`, `map()`,知道JavaScript能做什么
      https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array/forEach#
      
   > 文档中`Array.function()`为静态方法，例如`Array.from()`（将对象强制转化为Array）; `Array.prototype.function()`则使用时前面直接跟array名，例如`ages.pop()`  

  >复杂数据类型记录的是一个/组值的reference  
- 常见符号
  - 取余`%`:做一些algorithm的题经常会用到
  - 相等：
    - `==`： 不做类型判断，只比较值（内容），工作中要避免
    - `===`：会加入类型判断
    > 工作中常会判断是否object的值(内容)相等，会比较复杂，可以用到额外的库，比如`lodash`(https://lodash.com)
  - 逻辑非：`!`
    - `!==`: 判断不等，返回boolean
    - `!!`会将数据类型强制转化，比如`if(!!person.name)`这里`!!person.name`就被转化为boolean
  > JavaScript中哪些是false的(falsy value)  
    > `false`, 空string（""），0，负数，`null`，`undefined`
  - 特殊的数字练习： 
    - `4 + 3 + "3"`
      - 结果为73，因为4+3 = 7，然后强制转化为了字符串，执行字符串合并
    - `"4" + 3 + 3`
      - output: 433
    - `1 + null`
      - output: 1
    - `1 + undefined`
      - NaN(not a number)
> JavaScript里`'`和`"`没有区别，现在使用中(ES6)，如果要输出双引号，会用到  
> ``` const description = `"a" is a criminal` ```

> 关于JavaScript的三套书推荐：  
> JavaScript: The Definitive Guide, 7th Edition  
> Professional JavaScript for Web Developers:ES6之后的内容不是很好
> You Don't Know JS: Up & Going

> REACT的官方document写的不错，你们学习的时候，强烈推荐阅读  
> 同时推荐REACT作者Dan Abramov博客：https://overreacted.io   
> 以及：https://kentcdodds.com  
> 推荐的Podcast:搜索“web development treats"- Syntax Tasty Web Development Treats  
> 也可以Learning by teaching

### 5.条件语句 Condition
- `if` condition:
   ```js
    if(<condition>) {
       
    } else {
    }
    ``` 
  - 尽量不要加else，会增加nesting，推荐阅读（尽量不要写if...else...）
> Refactoring: Martin Fowler
- 三元运算符：`?`
    - `(condition) ? expr1:expr2`  
    等同于  
     ```js
    if(<condition>) {
       expr1
    } else {
        expr2
    }
    ```
     例如：  ```const name = isMale ? 'Gary' : 'Sylvia';```   
    - 什么是expression:
        - 只要是能返回一个值，这部分代码就可以是一个expression

### 6.循环语句 Loop
- `for`循环
    - 基本写法，例如
     ```js
     var ages = [12, 32, 33];
     for (let index = 0; index < ages.length; index ++) {
         console.log(ages[index]);
     }
    ```  
    以上代码等同于  
    ```js
     ages.forEach((age) => {
         console.log(age);
     })
    ```
    或
    ```js
     ages.map((age) => {
         console.log(age);
     })
    ```
    以上，`forEach`与`map`都对ages中的元素进行了遍历，但是`map`的本意是遍历ages中的每一项，修改每一项，让他们都满足一个东西。例如：
    ```js
     const newAges = ages.map((age) => {
         return age + 1;
     })
     console.log(newAges);
    ```
    即
     ```js
     const newAges = ages.map((age) => age + 1）;
     console.log(newAges);
    ```
    - `continue` VS `break`：
         - `continue`：跳过本次循环，进入下次循环
         - `break`:跳出循环
    - 嵌套循环（nested loop）：例如
     ```js
     var ages = [12, 32, 33];
     var index;
     for (index = 0; index < ages.length; index ++) {
         for(index +1; index < ages.length; index ++) {
            const element = array[index];
         }
     }
    ``` 
    - 课堂练习：写一个9*9乘法口诀
    ```js
     for (let row = 1; row < 10; row++) {
         var rowText = '';
         for(let col = row; col < 10; col++) {
            rowText = rowText + `${row} * ${col} = ${row * col}\t`;
         }
         console.log(rowText);
     }
    ``` 
    ES6中，`特别好用，比如以上
    ```js
    `${row} * ${col} = ${row * col}\t`
    ```
    两个`间即为输出字符串
- `while`循环
    - 比较少用的一个循坏，容易造成死循环
>`while` 在工作中不会用到，因为会容易出问题，不是个小事

### 7.函数 Function
- 一般写法：
    ```js
     function printPerson(name,age)) {
         console.log(name,age);    
     }

     printPerson('Gary','32');
    ``` 
    - function传的参数，跟名字无关，跟顺序有关
    - 注意参数为引用型变量时，有可能更改该变量的内容
    > 写`function`时，尽量不要试图修改传进来的arguments
- JavaScript中没有真正意义上的`class`
- `return` 表示返回，JavaScript会直接返回`return`后的值，之后的语句不会被执行
- 理解`function`的参数是怎么传的，`function`里面可以定义`function`,`function`也可以被传递出去，`function` 也可以指定给别的variable, 该variable还可以被运行
- `function`在JavaScript中是一等公民(平头老百姓)，可以传递，也可以嵌套
    - 例如：
    ```js
    function outsideFunc()) {
         var temp = 1;
         function insideFunc() {
            console.log(temp);  
         }   
    }

    var foo = outsideFunc();
    foo();
    ```  
    >以上代码中引入了闭包（closure）的概念，建议课后去查  
    >是context传递和保留的概念  
    比如以上代码，传统语言中，在运行outsideFunc后，一般其中的变量等都会被系统回收；但是在JavaScript中，当insideFunc再次被运行时，它还是可以拿到在context中的temp值；可以理解为一种内部访问外部data的机制。因为insideFunc对temp的调用，导致该变量其实并没有被内存回收
    - 常常用在callback上
    - 要了解，这种insideFunc可以访问outsideFunc里变量的机制
    - 闭包的扩展示例：
     ```js
    function delayPrint(data)) {
         setTimeout(() => {
            console.log(data);  
         }, 2000);   
    }

    delayPrint('time');
    ``` 
    因为JavaScript的闭包机制，在dalayPrint运行完两秒之后，setTimeout依然可以访问delayPring中的data变量
- 变量只能`function`内部引用外部，不能外部使用内部
- `function`内部也存在变量提升，不管变量声明在什么位置，都会被提升到函数体头部
    - 例如
     ```js
    function foo(x) {
        if(x > 100){
            var localVar = 1000;
        }
    }
    ``` 
    在编译器实际运行时，等同于
    ```js
    function foo(x) {
        var localVar；
        if(x > 100){
            localVar = 1000;
        }
    }
    ``` 
    - 还例如：
    ```js
    for (var index = 0; index < array.length; index++) {
        var b;
        const element = array[index];
    }
    ``` 
    等同于
    ```js
    var index;
    var b;
    for (index = 0; index < array.length; index++) {
        const element = array[index];
    }
    ``` 
    >只有`function`才能拦住 `var`的变量提升,其他都拦不住

### 8.Object 对象:最重要的数据类型
- `object`是一组无序数据组成的集合，表达一个复杂的数据类型   
   例如， 
    ```js
    var person = {
        firstName: 'Gary',
        lastName: 'Sun',
        age: 32,
        printFullName: function (){
            console.log(this.firstName + this.lastName);
        },
    }
    console.log(person.firstName);
    ```  
    其中 `console.log(person.firstName);` 也可以写作
    ```js
    var name = 'firstName';
    console.log(person[name]);
    ``` 
    这里```person.firstName```跟```person[firstName]```是等效的  
    `function`本身也是一个value,一个复杂数据类型,在作为参数传递的时候，传递是指向该`function`的地址  
- `this` 指向object本身   
    假如，添加以下代码：
    ```js
    var person = {
        firstName: 'Gary',
        lastName: 'Sun',
        age: 32,
        printFullName: function (){
            console.log(this.firstName + this.lastName);
        },
    }
    var person2 = {
        firstName: 'Sylvia',
        lastName: 'Sun',
    };
    person2.printFullName = person.printFullName;
    person2.printFullName();
    ```  
    那实际输出结果将为：
    ```
    SylviaSun
    ```
    `this`不会绑定在被定义的person里，哪个object用this，那`this`指向的就是这个object  
  - 如果`this`写在了最外层（js文件里）
    - 如果是写在网页里，浏览器运行，`this`指向window
    - 如果是在node上运行，`this`指向document
- `for...in`遍历对象
    - 例如
    ```js
    var person = {
        firstName: 'Gary',
        lastName: 'Sun',
        age: 32,
        printFullName: function (){
            console.log(this.firstName + this.lastName);
        },
    }

    for (var key in person) {
        console.log(key);
        console.log(person[key]);
    }
    ```
    其中，key即为object里的`key`,person[key]为该key对应的value
    上面如果写作person.key将没有输出，因为`.`后面直接跟的是变量名  
    > 需要课下阅读更多`object`的方法：https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Object/assign  
    常用的如`assign()`, `entries()`,` keys()`, `values()`, `hasOwnProperty()`

### 9.DOM:javaScript操作网页的接口
 DOM(Document Object Model):文档对象模型，可以将网页转换成一个javaScript对象，然后进行各种操作。浏览器首先会根据DOM模型，将HTML解析成一系列节点，再由这些节点组成一个树状结构(DOM Tree)。所有的节点和最终树状结构都有规范的对外接口。以下为常见的DOM方法：
- `querySeletor`:返回找到的第一个element
- `querySelectorAll`:返回找到的所有element
    - 例如,在dev tool中  
    `var nodeList = document.querySelectorAll('li')`
    该方法将返回一个`nodelist`,这时候可以用`Array.from`将之转化为`array`:  
    `var nodeArray = Array.from(nodeList)`  
    然后可以通过`forEach`修改其中的属性：
    `nodeArray.forEach(li => li.innerText = "jiangren")`
    其中,`innerHTML`是包含`innerText`的，`innerHTML`具体指的就是`<a>`标签，而`innerText`就是指的其中的text
- `addEventListener`:加一个事件，监听用户对它做了什么，比如用户鼠标点了它，或者鼠标移开它
    - `unclick`是REACT给加了addEventListener事件后的简写
- `createElement`:创建一个新的HTML标签
- `appendChild`: 添加一个新的element
- `insertBefor`: 在找到的元素前面加一个element
- `setAttribute`: 给HTML element添加一个新的属性
>以上方法，在REACT中，都被包裹起来，然后提供了对应更宜用的方法，而避免让你直接操作DOM   

### 10.课上练习:写一个clock的网页
>想获得更多时间显示效果，可以使用moment.js
https://momentjs.com
- 第一步，先把element找出来；然后再更改element
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta http-equiv="X-UA-Compatible" content="IE=edge">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Clock</title>
    <style>
        .clock {
            background-color: black;
            color:green;
            width: 180px;
            padding: 11px;
        }

        .clock-reverse {
            background-color: white;
            color:black;    
        }
        
    </style>
</head>
<body>
    <div class="clock"></div>
</body>
<script>
    var element = document.querySelector('clock');

    function eventHandler(){
      element.add('clock-reverse');
    }

    function handleClick() {
        window.alert(new Date().toLocaleString());
    }

    function setTimeToDiv() {
        var clockElement = document.querySelector('.clock');
        clockElement.addEventListener('click',handleClick);
        clockElement.innerHTML = new Date().toLocaleString();
    }

    document.addEventListener('click', eventHandler);
    setInterval(setTimeToDiv, 1000);
</script>

</html>
```
### 11.JS异步加载
- 上面的练习中，`<script>`放的位置是正确的；
如果是放在`<head>`里，在执行的时候，因为网页没有完全生成，可能会有效果上的延迟；  
放在`<body>`中，则可以充分保证网页在渲染完成后，执行js代码
如果是放在外部引入，如`<script src = "http://"></script>`，同样也可能遇到延迟问题；  
因为原理上如下图，Html parsing完会等待scripti下载与执行，再做渲染
![script defer async](https://i0.wp.com/www.sertmedia.com/wp-content/uploads/2018/08/95ba8eb4-aa59-4dab-992e-adcb38cf9d8c.jpg)
- 现在有`<script defer>`:则会在html parsing的同时，完成js下载，在html parsing结束后，再执行js，类似于把js放在`<body>`里，是比较安全的方式
- 还有`<script async>`:则会在html parsing未完成时，执行已经下载好的js，因为html parsing未完成，也会产生问题(可以参考tutorial的内容学习)
- `defer` VS `async`
```html
 <script src = "http://...file1,js"></script>
 <script src = "http://...file2.js"></script>
```
 以上代码如果前面是使用的`defer`，则文件会等待下载完成后，依次运行，先file1,再file2  
 以上代码如果前面是使用的`async`，则文件会不等待下载完成，而是根据谁先下载完，执行谁的顺序运行，因此有可能先运行file2，再运行file1  
> 考虑到js的加载问题，用`<script defer>`就可以了

### 面试及学习建议
- 与国内不同，澳洲开发更需要横向广度的经验
- 从旧版本ES6之前开始学，更基础易懂
- overeacted.io 是一个JavaScript核心开发者的博客
- 学习方式：
  - Podcast(syntax, software daily), Front-end Master.
  - Side project
  - 参加Meet Up
- 多练习，复习和充分理解闭包和this等相对hardcore的内容