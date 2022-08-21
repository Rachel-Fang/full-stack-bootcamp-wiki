## 目录

- [5.1 函数function](#51-函数function)
    - [5.1.1 Function declaration and function expression](#511-function-declaration-and-function-expression)
    - [5.1.2 primitive与object的区别](#512-primitive与object的区别)
- [5.2 Object](#52-object)
    - [5.2.1 object reference](#521-object-reference)
    - [5.2.2 Javascript Data Type](#522-javascript-data-type)
    - [5.2.3 Reference Types - Object 或 Array](#523-reference)
    - [5.2.4 function programming](#524-function-programming)
    - [5.2.5 object概念](#525-object概念)
    - [5.2.6 for...in...](#526-forin)
    - [5.2.7 Quiz](#527-quiz)
- [5.3 DOM（网页的编程接口）](#53-dom)
    - [5.3.1 基本概念](#531-基本概念)
    - [5.3.2 Common JS methods for DOM Manipulation](#532-common-js-methods)


### 5.1 函数function

#### 5.1.1 Function declaration and function expression

```js
js
// when define a function by function expression, we can treat this function as a var.

// assignment
function sum(num1, num2) {
    return num1 + num2;
}

// re-assignment
var newSum = sum;

//first sum two nums, then double the result
function firstSumThenDouble(sumFunc, num1, num2) {
    var sum = sumFunc(num1, num2);
    return sum * 2;
}

console.log(firstSumThenDouble(newSum, 2, 3))
```
>结果：10

>结论：
- 一般情况下，是可以把function当作var来使用的。
- 当我们需要把function当作参数传入到另一个function里面，或其他任何一个地方的时候，我们需要用function expression的方法把它提前定义为一个var。
- 在function expression这样一个表达式的情况下，function可以当作var来使用。这个时候的function继承了var所有功能和特性。

#### 5.1.2 primitive与object的区别

- Mutable（可以改变）和immutable（不可以改变） in Javascript
    - Mutability def: Mutable is a type of variable that can be changed. 
    - In JavaScript, only objects and arrays are mutable, not primitive values.

### 5.2 Object

#### 5.2.1 object reference

- 在object中
```js
js
var personObject = {
    personName: 'Jing Zhou',
    age: '18',
    occupation: 'dev'
};

var jing = personObject;

personObject.age = '19';

console.log(jing.age);
```
>结果：19

- primitive中

```js
js
var aString = 'know';
var anotherString = aString;

aString = 'unknown';
console.log(anotherString);
```
>结果：know

>说明：
- 事情是一样的，区别在于data type不一样。
- 在primitive data type中，value是不能传递的。
- 在object中，把object re-assign给另外一个variable，这时，我只要改变原object值，新的被re-assign的variable的值也会做一个相应的改变。
- 在primitive data type中，改变原variable的值，被re-assign的variable是不会改变或更新的。
- var object储存的并不是一个值，而是一个内存地址，而这个内存地址是指向被指向的东西。
- 当把personObject赋值给jing的时候，并没有reassign实际的值，而是把object里面的内存地址赋值到jing这个variable里面。
- personObject和jing相同的是内存地址，而不是里面的值。

#### 5.2.2 Javascript Data Type

![js-dataType](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-dataType.png)

- 老师讲解网址：https://blog.devgenius.io/mutable-and-immutable-in-javascript-78a3cbc6187c

>老师上课讲解：value types  
- stack里的数据可以被非常快速的进行调取。有点类似于内存。硬盘大，读取速度慢；内存小，但是读取速度快。
- 在做reassignment的时候，值可以被复制粘贴，会被作为一个新的内容添加到stack上。被reassignment的variable从此就有了自己独立的stack空间，那里储存的就是实际的值。相当于粘贴复制。

![js-valueTypes](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-valueTypes.png)

>图片说明：
- 开始有个name叫Maya，var name这个variable会指向stack中的某一段，这个段实际储存了Maya的值。
- 当我们做reassignment的时候，Maya的值被复制粘贴，又被放到stack之间，这时新的variable（var newName）指向新的值上。

#### 5.2.3 Reference Types - Object 或 Array

- Heap与Stack的异同：
    - 都是储存空间。
    - Heap空间更大。但是读取速度更慢。
    - Stack相当于内存，Heap相当于硬盘。

- 在primitive世界当中，我们只需要用到stack，在reference types（object或array）中，stack和heap都会用上。

![js-referenceTypes](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-referenceTypes.png)
```js
js
var Person = {name: "Maya", age: "29"}
var newPerson = Person;
```

>图片说明：
- 中间粉色的是stack；
- 上面绿色的部分heap，储存person信息，一个实际的值；
- 粉色最上面的是一个指针，personpointer，是一个memoryAdress，内存地址，这个内存地址储存在stack当中。
- 实际在调用variable过程中的步骤：
    - 通过在stack中相对应的位置来找到内存地址；
    - 通过内存地址再到heap里面找到实际的值。

![js-heap&stack](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/img/js-heap%26stack.png)

>图片说明：
- stack储存粘贴过后的值，因为这两个值是相等的，所以他们最终指向的是一个地方，那个地方储存object，是被共享的。
- 这个时候，不管是改变newPerson还是person的值，所有拥有这个reference的variable都会受影响。
- 多对一的关系。
- 以上是primitive和非primitive在储存机制上的本质区别。

#### 5.2.4 function programming

- OO：把我们的程序拆分成一个一个的对象，对象之间的交互来完成我们之间的逻辑。
- JS：在JS语句当中，React、Angular变成当中，尤其是React，提倡function programming，在这里的基本单位不是object，而是function。
- function programming：interactions between functions。
- immutable functions (pure functions) - no side effects (不改变，不影响不属于我的东西)

```js
js
var person = {
    name: 'Jing',
    age: 18,
};

// function会改变外界传给我们的一个参数。
function increaseAgeByOne(person) {
    //update person's age to +1:
    person.age += 1;
}
```

>说明：side effects
- function会做一个什么事情：
    - 会改变外界传给我们的一个参数。
- person属于function这个函数吗？
    - 不属于
- function目的是什么？
    - person不管是谁丢给我的，并不属于我这个function。
    - 但是我在function里却改变了person的实际内容。
- 这种person不属于function，但function却改变了person内容的情况，叫做side effects。
- 这时这个function并不是一个pure function。它有side effects，它会改变并不属于它function的一些内容或东西。


****如何把一个有side effects的function变成一个pure function呢？***
- 三步走：
    - copy
    - mutate
    - return

```js
js
function increaseAgeByOne(person) {
    // copy and update
    var myPerson = {
        name: person.name,
        age: person.age + 1
    };
    return myPerson;
}
```
>说明：
- 你传进来的参数，你外界的东西，我没有做任何的改变，我也达到了我需要的功能。

****为什么要些pure function呢？***
- 老师答：当function programming写到后面的时候，function里面会有非常非常多的内容，如果不加pure function的这样一个限制，基本上每个function都会给我们传进来的参数做删改，结果是无法预期的。
- React的时候会非常着重这个概念。

#### 5.2.5 object概念：
- 对象（object）是JavaScript的核⼼概念，也是最重要的数据类型。JavaScript的所有数据都可以被视为对象。
- 所谓对象，就是⼀种⽆序的数据集合，由若⼲个“键值对”key-value）构成。
- 例子：
```js
var obj = {
    key: 'string value',
    myArray : [1,2,3,4],
    myArrayLength : function() { 
        return this.myArray.length()
    }
}
console.log(obj.key); // string value
console.log(obj.myArray[0])
```

- **this会在之后的ES6里面讲。**

#### 5.2.6 for...in...

- 用for...in...循环来遍历一个对象的全部属性。

```js
js
var person = {
    name: 'Jing',
    age: 18,
    occupation: 'Dev'
};

function increaseAgeByOne(person) {
    // copy and update
    var myPerson = {
        name: person.name,
        age: person.age + 1
    };
    return myPerson;
}

for (var key in person) {
    console.log(person[key]);
}
```
>结果：  
Jing  
18  
Dev

#### 5.2.7 Quiz
- 在⼀个升序,⽆重复数的数组中，给定⼀个⽬标值，找出哪两个数的和为这个⽬标值(任意⼀个组合），并返回这两个数的序号（index）  
- 要求：写⼀个function， 输⼊为⼀个数组和⼀个数字，输出为⻓度为2的数组，⽐如：  
Array = [1,3,4,6,7,8,10,14,15]  
Target = 14  
[2,6] or [3,5]

```js
// 需求：打出所有pair结果（去重）
function getSumIndices (array, target) {
    // 特殊判断：if fail, fail fast
    // 先做特判是一个反直觉性的东西
    if (!array || array.length < 2) {
      console.log([]);
    }
    // 如果特判没有把任何的异常揪出来，就可以开始正式的操作了。
    // 第一步做一个遍历，扫描所有的element。这个过程中，为了可读性，把index1和2用两个不同的variable来hold住。不是100%必要。
    // i代表index的数字
    for (var i = 0; i < array.length; i++) {
      var index1 = i;
      var index2 = array.indexOf(target - array[i]);
  
      if (index2 !== -1) {
        console.log([index1, index2]);
      }
    }
}

  getSumIndices([1,3,4,6,7,8,10,14,15], 14);
  ```

****indexOf( ):***  
当我们用indexOf的时候，丢进去的查找目标，如果存在的话，这个目标的index会被揪出来，如果不存在，它就会等于-1.

***作业**（经典、中等难度的算法题）   
1. Quiz打出所有的pair结果（去重）。

### 5.3 DOM（网页的编程接口）

#### 5.3.1 基本概念

- DOM是JavaScript操作⽹⻚的接⼝，全称为“⽂档对象模型”（Document Object Model）。它的作⽤是将⽹⻚转为⼀个JavaScript对象，从⽽可以⽤脚本进⾏各种操作（⽐如增删内容）。
- 浏览器会根据DOM模型，将结构化⽂档（⽐如HTML和XML）解析成⼀系列的节点，再由这些节点组成⼀个树状结构（DOM Tree）。所有的节点和最终的树状结构，都有规范的对外接⼝。所以，DOM可以理解成⽹⻚的编
程接⼝。
- DOM的最⼩组成单位叫做节点（node）。⽂档的树形结构（DOM树），就是由各种不同类型的节点组成。每个节点可以看作是⽂档树的⼀⽚叶⼦。
- Document：整个⽂档树的顶层节点
= Element：⽹⻚的各种HTML标签（⽐如`<body>`、`<a>`等）
- Attribute：⽹⻚元素的属性（⽐如class="right"）
- Text：标签之间或标签包含的⽂本
- Comment：注释

#### 5.3.2 Common JS methods for DOM Manipulation

1. querySelector
	return the first element found or null
2. querySelectorAll
	return all elements as NodeList object, or empty object
3. addEventListener
	assign function to certain event
4. removeEventListener
5. createElement
	create a new HTML element using the name of HTML tag
6. appendChild
	add an element as the last child to the element that is invoking this method
7. removeChild
8. insertBefore
	add an element before a child element
9. setAttribute
	add a new attribute to an HTML elemen

```html
html
<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <title>My counter</title>
  <link rel="stylesheet" href="style.css">
</head>
<body>
  <div class="container">
    <div class="row">
      <div class="col-sm">
        <div class="card">
          <div class="card-content">
            <h1 class="card-title">This is a counter</h1>
            <button class="btn btn-plus" id="control-plus">+</button>
            <p class="number" id="control-num">0</p>
            <button class="btn btn-minus" id="control-minus">-</button><br />
            <button class="btn btn-reset" id="control-reset">Reset</button>
          </div>
        </div>
      </div>
    </div>
  </div>
  <script src="main.js"></script>
</body>
</html>
```

```js
js
var plusButton = document.querySelector('#control-plus');
var minusButton = document.querySelector('#control-minus');
var resetButton = document.querySelector('#control-reset');
var resParagraph = document.querySelector('#control-num');

var counter = 0;
plusButton.addEventListener('click',function) {
    counter ++;
    resParagraph.inner = counter;
};
```
