## 目录

- [5.1 基础知识](#51-基础知识)
- [5.1.1 JS主要作用](#511-js主要控制……)
- [5.1.2 JS定义](#512-javascript……)
- [5.1.3 强类和弱类语言](#513-强类和弱类语言)
- [5.1.4 脚本语言与非脚本语言的区别](#514-脚本语言与非脚本语言的区别)
- [5.1.5 JavaScript is……](#515-javascript三大之一)
- [5.1.6 JS简单历史](#516-js简单历史)
- [5.1.7 ES5和ES6](#517-es5和es6)
- [5.1.8 chrome上如何操作](#518-chrome如何操作)
- [5.2 变量 Variable](#52-变量-variable)
- [5.2.1 变量 Variable](#521-变量-variable)
- [5.2.2 安装nodejs](#522-安装nodejs)
- [5.2.3 重新赋值](#523-重新赋值)
- [5.2.4 多个赋值](#524-多个赋值)
- [5.2.5 数字、字符、布尔输出结果](#525-数字字符布尔输出结果)
- [5.2.6 工程化代码](#526-工程化代码)
- [5.3 命名规则Naming convention](#53-命名规则)
- [5.3.1 Cases](#531-cases)
- [5.3.2 Starting character](#532-starting-character)
- [5.3.3 Reserved words](#533-reserved-words)
- [5.4 数据类型 Data type](#54-数据类型-data-type)
- [5.4.1 数值（number）](#541-数值number)
- [5.4.2 字符串（string）](#542-字符串string)
- [5.4.3 布尔值（boolean）](#543-布尔值)
- [5.4.4 undefined](#544-undefined)
- [5.4.5 null](#545-null)
- [5.4.6 对象（object）](#546-对象object)
- [5.4.7 数组(Array)](#547-数组array)
- [5.5 运算符](#55-运算符)
- [5.5.1 "+"号](#551-"+"号)
- [5.5.2 减法、乘法、除法](#552-减法乘法除法)
- [5.5.3 严格和不严格相等](#553-严格和不严格相等)
- [5.5.4 练习](#554-练习)
- [5.6 数组](#56-数组)
- [5.6.1 增删](#561-增删)
- [5.6.2 数组长度](#562-数组长度)
- [5.6.3 如何定位一个数字在数组中的位置](#563-如何定位)
- [5.7 条件语句](#57-条件语句)
- [5.8 Falsey value](#58-falsey-value)
- [5.9 循环语句](#59-循环语句)
- [5.9.1 for循环语句](#591-for循环语句)
- [5.9.2 i++和++i](#592-i和i)
- [5.9.3 while循环语句](#593-while循环语句)
- [5.9.4 break和continue](#594-break和continue)
- [5.10 函数](#510-函数)
- [5.10.1 定义](#5101-定义)
- [5.10.2 参数化](#5102-参数化)
- [5.10.3 function declaration和function expression](#5103-function-declaration和function-expression)
- [5.10.4 作用域scope](#5104-作用域scope)


### 5.1 基础知识

#### 5.1.1 JS主要控制content behavior，把内容变得更dynamic。  
Interaction with user, User behaviour tracking, ***Post and get data***（与后端进行交互）

#### 5.1.2 JavaScript is a dynamic, weakly typed programming language. + script（脚本类语言） 

#### 5.1.3 强类和弱类语言：  
- A. Java：强类  
```Java
Java
public double sum(double num1, double num2) {
    return num1 + num2
}
```
>说明：
>- return是什么类型，一定要做一个严格的标注。
>- 传进来的参数是什么类型也要做一个严格的标注。

- B. Javascript语言
```js
js
function sum(a, b) {
    return a + b;
}  
```
>说明：
>- 并没有定义一个return值。
>- 参数上并没有加任何的限制。

#### 5.1.4. 脚本语言与非脚本语言的区别：***（面试题）***  
- JS - script language脚本语言（解释语言）  
- ***解释语言***：有一个运行环境，如chrome，可以理解JS，可以通过某一种形式把JS转换成另一种chrome可以理解的东西来运行。  
- Java - compile language编译语言    
- ***compilation***：把任何一个编译语言转换成计算机能读懂的语言的过程就叫做编译。
- 对于编译语言来讲，在运行之前有一个编译的过程，这个编译的过程可以覆盖到我们计算机所有的代码中。也就是当你把代码写好之后，在运行的时候，系统或编译器会扫描这个代码将要触碰到的所有内容，把这个内容先进行一个编译的过程。如果在编译中碰到任何的错误，会报错。
- 解释语言不是，解释语言没有编译这样一个步骤，其实就是把JS直接丢到chrome浏览器上，运行一步解释一步。
>面试题：JS（弱类语言）和Java（强类语言）相比，优势在哪里？
- 直接优势：写起来非常快。比较轻量、简单、开发起来比较快。
- （脚本角度）解释语言和编译语言的优劣对比：  
答：无编译，执行快。（不在点上）  
对于终端、客户端没有苛刻的配置需求。JS在浏览器中就可以运行。写完之后可以直接部署，可以直接用。对于客户端没有任何的要求。

#### 5.1.5 JavaScript is one of the three core technologies of web development
- Client-side: Browser
- Server-side: Node.js  
（node技术研发后，js既可以写前端，也可以写后端，但是node写后端相比其他语言，并不是很有优势，可以上网查看）

#### 5.1.6 JS简单历史

### 5.1.7 ES5和ES6
- 后者比前者有质的飞跃
- ES6可以理解为主版本的更新
- 这节课主要学习ES5

### 5.1.8 chrome点击inspect，找到console
- 可以报错，简单的代码测试
```Javascript
js
console.log('hello world')
```
![JS-helloWorld](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/JS-helloWorld.png)

### 5.2 变量 Variable

#### 5.2.1 变量 Variable
- 储存数据的容器
- 声明一个变量，使用关键词var
```js
js
// declaration 声明
var name;
```
- 赋值
```js
js
// assignment 赋值
name = 'Jessie';
```

#### 5.2.2 安装nodejs
Ubuntu安装：  
sudo apt-get install nodejs
sudo apt-get install npm  
再在vscode里安装插件code runner

#### 5.2.3 重新赋值
```js
js
// re-assignment 重新赋值
name = 'Emily';
```

#### 5.2.4 多个赋值
```js
js
var student1, student2, student3;
student1 = 'Jim';
student2 = 'Tom';
student3 = 'Jack';

console.log(student1);
console.log(student2);
console.log(student3);
```

>结果：
![JS-多个赋值结果](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/JS-%E5%A4%9A%E4%B8%AA%E8%B5%8B%E5%80%BC%E7%BB%93%E6%9E%9C.png)

#### 5.2.5 数字、字符、布尔输出结果
```js
js
var a = 0; // numeric value
a = 'a string value';
a = true;
console.log(a);
```
>结果：
![js-数字、字符、布尔输出结果](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%E6%95%B0%E5%AD%97%E3%80%81%E5%AD%97%E7%AC%A6%E3%80%81%E5%B8%83%E5%B0%94%E5%80%BC%E8%BE%93%E5%87%BA%E7%BB%93%E6%9E%9C.png)

#### 5.2.6 工程化代码：
- 变量的属性不要变来变去，不要一会儿是数字，一会儿是字符，一会儿又是布尔值。要单一。否则随着代码量越来越大，代码会很难看出到底是什么。
- 学react的时候，会着重讲一下工程化代码的概念。
- 从react开始学写简单、易懂、工程化代码的一个好习惯。
- 可读性、可维护性、可扩展性。

#### 5.2.7 hoisting变量提升
```js
js
car = 'Honda Civic';
console.log(car);
var car;
```
>结果：
![js-hoisting](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-hoisting.png)

>说明：
- JavaScript引擎的⼯作⽅式是，先解析代码，获取所有被声明的变量，然后再⼀⾏⼀⾏地运⾏。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做***变量提升***。*（junior常考面试题）*

### 5.3 命名规则Naming convention
#### 5.3.1 Cases
- UPPERCASE, （会有一些）
- camelCase（经常用这个，主要用法）, 
- PascalCase, 
- under_score, （会有一些）
- hy-phen
- const （ES6）
#### 5.3.2 Starting character:
- no number, 
- no symbol (except for _ and $)
#### 5.3.3 Reserved words:
- if, 
- else, 
- instanceof, 
- true, 
- switch … more

### 5.4 数据类型 Data type

#### 5.4.1 数值（number）：
- 整数和⼩数（⽐如1, 3.14 , NaN, infinity无限大）
```js
js
// not a number
aNum = NaN;

if (isNaN(aNum)) {
    console.log('It is not a number...');
}
```
>结果：
![js-aNum](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-aNum.png)

#### 5.4.2 字符串（string）：字符组成的⽂本（⽐如”jiangren”）
    - both string and character
    - 单引号和双引号都可以用，效果是一样的。

#### 5.4.3 布尔值（boolean）：true（真）和false（假）两个特定
```js
js
var amIAGuy = true;
var amIAWoman = false;

console.log(amIAGuy);
console.log(amIAWoman);
```
>结果：
![js-布尔输出](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%E5%B8%83%E5%B0%94%E8%BE%93%E5%87%BA.png)

#### 5.4.4 undefined：表示“未定义”或不存在，即⽬前没有定义。
    - 不存在

#### 5.4.5 null：表示⽆值，即此处的值就是“⽆”的状态。
    - 被声明过
```js
js
var age = undefined;
var gender = null;

console.log(age);
console.log(gender);
```
>结果：
![js-undefined&null](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-undefined%26null.png)

>以上称为基础数据类型（primitive values）

#### 5.4.6 对象（object）：各种值组成的集合

- object显示方法一

```js
//object显示方法一：
var teacher = {}

teacher = {
    teacherName: 'Jing',
    age: 18,
    gender: 'male',
    expertise: 'frontend',
    onDuty: true
};

console.log(teacher);
```
>结果：
![js-object1](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-object1.png)

- object显示方法二

```js
// object显示方法二：
var teacher = {};

teacher.age = 18;
teacher.onDuty = true;
console.log(teacher);
```
>结果：
![js-object2](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-object2.png)

- object显示方法三

```js
// object显示方法三：
var teacher = {};

teacher.age = 18;
teacher.onDuty = true;
//用另外一种方式加入一个变量：
teacher['gender'] = 'male';
console.log(teacher);
```
>结果：gender的语句与其他语句类型不一致，但是也可以加入进来。
![js-object3](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-object3.png)

- object显示方法四

```js
// object显示方法四：
var teacher = {};
var gender = 'gender';

teacher.age = 18;
teacher.onDuty = true;
//用另外一种方式加入一个变量：
teacher[gender] = 'male';
console.log(teacher);
```
>结果：gender的语句与其他语句类型不一致，但是也可以加入进来。
![js-object4](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-object4.png)


- object输出方式：

```js
js
var teacher = {};
var gender = 'gender';

teacher.age = 18;
teacher.onDuty = true;
//这时的gender是一个变量，所以[]内不用加引号。
teacher[gender] = 'male';
console.log(teacher);

console.log(teacher.age);
console.log(teacher[gender]);
```
>结果：gender的语句与其他语句类型不一致，但是也可以加入进来。
![js-object输出](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-object%E8%BE%93%E5%87%BA.png)

***- object总结***  
1. object是一个复杂类，由多个primitive value变量组成的。
2. 需要一个大括号把它括起来{} 。  刚开始用一个{}来定义基本的变量，里面是空的。
3. 可以用key:value形式来赋值。
4. 也可以用.age来赋值。
5. 也可以用[ ]来赋值。[ ]里面允许我们使用变量。


#### 5.4.7 数组(Array) : ⼀种允许你存储多个值在⼀个引⽤⾥的结构。

- 显示方法

```js
// array显示方法一
var students = ['Jing', 'Emily', 'Holly', 'Shawn'];

console.log(students[0]);
console.log(students[1]);
console.log(students[2]);
console.log(students[3]);
```
>结果：
![js-array1](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-array1.png)

- 显示方法二

```js
// array显示方法二
var students = [{
    studentName: 'Jing'
}, {
    studentName: 'Emily'
}, {
    studentName: 'Holly'
}];

console.log(students[2]);
```
>结果：
![js-array2](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-array2.png)

### 5.5 运算符

#### 5.5.1 "+"号
```js
js
var sum = 2 + 3;
console.log(sum);
var concat = '2' + '3';
console.log(concat);
var concat = 'hello' + ' ' + 'world';
console.log(concat);
```
>结果：
![js-加法](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%E5%8A%A0%E6%B3%95.png)

#### 5.5.2 减法、乘法、除法
```js
js
var divide = 8 / 4;
var minus = 8 - 4;
var times = 2 * 2;
console.log(divide);
console.log(minus);
console.log(times);
```
>结果：
![js-减法、乘法、除法](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%E5%87%8F%E6%B3%95%E3%80%81%E4%B9%98%E6%B3%95%E3%80%81%E9%99%A4%E6%B3%95.png)

#### 5.5.3 严格和不严格相等 / 严格和不严格不等
```js
js
var equalNonStrict = 2 == '2'; //non-strict comparison
var equalStrict = 2 === '2';

console.log(equalNonStrict);
console.log(equalStrict);
```
>结果：
![js-严格和不严格相等](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%E4%B8%8D%E4%B8%A5%E6%A0%BC%E5%92%8C%E4%B8%A5%E6%A0%BC%E8%B5%8B%E5%80%BC.png)

***注意：***
- 两个等号是不允许使用的。

#### 5.5.4 练习

- 练习一：数字+字符

```js
js
console.log(4 + 3 + '3'); 
// 4 + 3 + '3' => 
// 7 + '3' => 
// '7' + '3' => 73
```

- 练习二：字符+数字 ***（面试题）***
```js
js
console.log('4' + 3 + 3); 
// '4' + 3 + 3 => 
// '4' + '3' + 3 => 
// '43' + 3 => '43' + '3' 
// => '433'
```

- 练习三：小数相加
```js
js
console.log(0.1 + 0.2);
// =>0.30000000000000004
```

***原理：***  
- 整数 十进制 -> 二进制  

| 除2   | 商  |余数 |bit位|
| ------| ----| ----| -----|
| 10    |     |     |      |
| 10/2  | 5   | 0   | 0    |
| 5/2   | 2   | 1   | 1    |
| 2/2   | 1   | 0   | 2    |
| 1/2   | 0   | 1   | 3    |  

    - 10 -> 1010  
    - 1 0 1 0 -> 1 x 2^3 + 0 x 2^2 + 1 x 2^1 + 0 x 2^0 = 10  
  
    
- 小数 十进制 -> 二进制  
  
| 乘2    | 积   | 取整|
| ------ | ---- | ----| 
| 0.2    |      |     |
| 0.2*2  | 0.4  | 0   | 
| 0.4*2  | 0.8  | 0   | 
| 0.8*2  | 1.6  | 1   | 
| 0.6*2  | 1.2  | 1   |  
| 0.2*2  |      |     | 

- 练习四：
```js
js
console.log(1 + null); 
// null其实被当作0,记住就可以。
console.log(1 + undefined); 
//一个数字+一个不存在
// NaN(not a num)
// 不存在
```

### 5.6 数组

#### 5.6.1 增删
```js
js
var names = ['Jing', 'Emily', 'Holly', 'Jack'];
// push and pop adds or removes the last element
names.push('Tom');//添加一个元素
names.pop();//就是移除最后一个
// unshift and shift adds or removes the first element
names.unshift('Tom');
names.shift();
//数组中原来的第三个位置被Tom所替代
names[2] = 'Tom';

console.log(names);
```

>结果：
![js-数组增删](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%E6%95%B0%E7%BB%84%E5%A2%9E%E5%88%A0.png)

#### 5.6.2 数组长度
```js
js
var names = ['Jing', 'Emily', 'Holly', 'Jack'];
names.push('Tom');
// length: last index + 1
names[101] = 'Tom';
console.log(names.length);
```
>结果：
![js-数组长度](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%E6%95%B0%E7%BB%84%E9%95%BF%E5%BA%A6.png)

#### 5.6.2 如何定位一个数字在数组中的位置
```js
js
var twoDimentionalArray = [[1, 2, 3], [4, 5, 6], [7, 8, 9]];
// 输出6的位置
console.log(twoDimentionalArray[1][2]);
```
>注意：   
如果想进大厂，算法是非常重要的。  
二维数组是个常用的数组结构。

### 5.7 条件语句

- if...else...
```js
js
var age = 18;
// if...else...语句
if (age < 18) {
    console.log('You are under 18!');
} else {
    console.log('You are over 18!');}

// 三联运算符
console.log(age < 18 ? 'You are under 18!' : 'You are over 18!');
```
>结果：
![ifElse&三联](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-ifElse%26%E4%B8%89%E8%81%94%E8%BF%90%E7%AE%97%E7%AC%A6.png)

### 5.8 Falsey value
    * false
    * NaN
    * undefined
    * null
    * ""和" "
    * 0
```js
js
// 以下0的位置可以换成是false、NaN、undefined、null、、""、" "。  
// 除了" "和"0"的输出是pass，其他都是fail。
if ("0") {
    console.log('Pass');
} else {
    console.log('Fail');
}
```
>说明：
- "0"和" "（空格字符串），都算是附了一个值。虽然空格是没有，但是在双引号下，也算是赋值了，所以这俩都是pass。  
- false、NaN、undefined、null、""（空字符串）这些都是fail。
- ""（空字符串）和" "（空格字符串）的区别：
    - " "（空格字符串）相当于赋值了，只不过赋值是空格，所以输出是pass。
    - ""（空字符串）也赋值了，但是计算机习惯把空字符串的bool值算为0，所以输出为fail。

### 5.9 循环语句

#### 5.9.1 for循环语句
```js
js
for (var i = 0; i < 10; i++) {
    console.log(i);
}
```
>结果:
![js-循环语句](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%E5%BE%AA%E7%8E%AF%E8%AF%AD%E5%8F%A5.png)

#### 5.9.2 i++和++i
***i++: i = i + 1***  
***++i***

- i++
```js
js
var i = 42;
console.log(i++);
console.log(i);
```
>结果：
![js-i++](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-i%2B%2B.png)


- ++i

```js
js
i = 42;
console.log(++i);
console.log(i);
```
>结果：
![js-++i](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-%2B%2Bi.png)

>***说明：***
- the 2 operators work the same way
- but returns different values
- i++ returns the old value
- ++i returns the new value

- **问：hello会被打出来多少次？**
```js
js
for (var i = 0; i < 10; i++) {
    for (var j = 0; j < 10; j++) {
        console.log('hello');
    }
}
```
>结果：100次。  
i是0~9共10次，j也是0~9共10次，10*10=100次。

#### 5.9.3 while循环语句
```js
js
var i = 0;
while(i < 10) {
    if (i === 8) {
        i++;
        continue;
    }
    console.log(i);
    i++;
}
```
>结果：0~9.

#### 5.9.4 break和continue

- **requirements: not printing 8**
```js
js
var i = 0;
while(i < 10) {
    if (i === 8) {
        i++;
        continue;
    }
    console.log(i);
    i++;
}
```
>说明：当遇到8的时候，continue直接进入到下一个循环里。

- **requirements: when i is 5 terminate**
```js
js
var i = 0;
while(i < 10) {
    if (i === 5) {
        console.log(i);
        break; // break out of the loop
    }
    console.log(i);
    i++;
```
>结果：0 1 2 3 4 5

- **Quiz：在0-100之间，找出前⼗个，是4的倍数，但不是5的倍数的数字。（可尝试运⽤break和
continue）将最终结果打印出来：
[ 4, 8, 12, 16, 24, 28, 32, 36, 44, 48 ]**
***（可以当面试题）***  
老师答案：
```js
js
const res = [];
for (var i = 1; i<=100; i++) {
    if (res.length === 10) {
        break;
    }
    if (i % 4 === 0 && i % 5 !==0) {
        res.push(i);
    }
}


console.log(res);
```

>结果：
 [ 4, 8, 12, 16, 24, 28, 32, 36, 44, 48 ]

>总结：
- 可读性代码不一定性能最优。
- 性能最优的代码不一定可读。
- 结合上下文、语境、context等来判断，到底是可读性重要or性能更重要。
- 本题100个数字，运算比较简单，故可读性重要一些。

### 5.10 函数

#### 5.10.1 定义
- function命令声明的代码区块，就是⼀个函数。function命令后⾯是函数名，函数名后⾯是⼀对圆括号，⾥⾯是传⼊函数的参数。函数体放在⼤括号⾥⾯。  
函数很重要，有了函数就可以复⽤代码
```js
// 把以上Quiz用函数写出来
function firstTen() {
    const res = [];
    for (var i = 0; i<= 100; i++) {
        //终止条件
        if (res.length === 10) {
            break;
        }

        if (i % 4 === 0 && i % 5 !== 0 ) {
            res.push(i);
        }
    }
    return res;
}

console.log(firstTen());
```
>结果：
![js-function1](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-function1.png)
- 结果一定要有传入和传出的东西，不要忘记return或者console.log。

#### 5.10.2 参数化
```js
js
function firstTen(param1, param2, param3) {
    const res = [];
    for (var i = 0; i <= param3; i++) {
        //终止条件
        if (res.length === 10) {
            break;
        }
        
        if (i % param1 === 0 && i % param2 !== 0) {
            res.push(i);
        }
    }
    return res;
}

console.log(firstTen(4, 5, 100));
```

```js
// 书写方式二
function firstTen(param1, param2, param3) {
    const res = [];
    for (var i = 0; i <= param3; i++) {
        //终止条件
        if (res.length === 10) {
            break;
        }
        
        if (i % param1 === 0 && i % param2 !== 0) {
            res.push(i);
        }
    }
    // 直接输出res
    console.log(res);
}
// 调用函数firstRen
firstTen(4, 5, 100);
```

>结果都是：
![js-function2](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-function2.png)

>说明：
- 可以随意定义变量：上面代码就是找出能被4整除，但是不能被5整除，0~100之间的前10个数字。定义的变量就是：
    - 4（param1）
    - 5（param2）
    - 100（param3）

#### 5.10.3 function declaration和function expression
```js
js
// Function declaration 
function add(a, b) { 
return a + b; 
} 

// Function expression 
var add = function (a, b) { 
return a + b; 
};

// Almost identical, but hoisting!
```
>说明：
- 结果是一样的。
- function add(a, b)这种形式是直接规范function。
- var add = function (a, b)这种形式，是把function以不记名的形式assign到一个var里面。

#### 5.10.4 作用域scope
- 作⽤域（scope）指的是变量存在的范围。
- Javascript只有两种作⽤域：
    - ⼀种是全局作⽤域，变量在整个程序中⼀直存在，所有地⽅都可以读取；
    - 另⼀种是函数作⽤域，变量只在函数内部存在。
- 在函数外部声明的变量就是全局变量（global variable），它可以在函数内部读取。
- 在函数内部定义的变量，外部⽆法读取，称为“局部变量”（local 
variable）。

```js
js
var globalVar =“I am Global variable”;
function f() {
var localVar = “I am local variable”;
console.log (globalVar) 
// Ok 
}
console.log(localVar) 
//ReferenceError: localVar is not defined
```

>结论：
- 在global作用域中，所有的var会提升到global的头段。
- 在function作用域中，所有的var会提升到function的头段。
