## 1.0 ES6引入的新功能
### 1.1 class 在ES6中的使用
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
   
### 1.2 let/const 在ES6中的使用
- ES6 新增了let/const命令，用来声明变量。它的用法类似于var，但是所声明的变量，只在let/const命令所在的代码块内有效。
  - 以后要严格的遵循，先声明，再调用的原则 
  - let->变量，const->常量
  - 基本上const用的多，let用的少
### 1.3 Template String 模板字符串（反引号）在ES6中的使用
- 字符串操作在JavaScript中是非常繁琐的，ES6中可以用反引号直接，${}, 花括号里的是JavaScript statement，例如
   ```js 
    const greeting = `Hello ${name}`;
    const multiLinesGreeting = ` 
    Hello,
    My Name is ${name}.
    Nice to meet you.
    `;
   ```
### 1.4 函数参数的默认值
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

### 1.5 Destructuring 解构赋值(重要!)
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

### 1.5.1 Array的解构赋值
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
### 1.5.2 解构赋值标准用法中的简写
#### 1.5.2.1 多层取值的简写
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
### 1.5.3 解构赋值的进阶学习
#### 1.5.3.1 语法糖 spread
可以把想要的拿出来，剩下的分发出去，用...，例如以下代码
```js
    Alice {
      护照,
      行李:[大箱子，小箱子，电脑包],
    };

    const { 护照, 行李: [托运行李, ...其他行李]} = Alice;

    console.log(其他行李); // 小箱子 电脑包
```
## 2.0 JavaScript中的 this (最重要最无聊又最没用)
最重要：JavaScript的核心理论；有时候有莫名其妙的错误，可能就是`this`的导向造成的  
最没用：太过于高级，以至于现在没人愿意去用它了
## 3.0 函数是一等公民
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
