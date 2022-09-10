## 1.龙哥上课风格
https://au.linkedin.com/in/long-zhao-32a96916a
- 15年毕业起开始做freelancer
- 17年程序员正式出道
- 17-21 程序之路磨破滚打，从lead到Qantas Senior，又到EL管理层
- Full Stack, 会Ruby, JAVA, python, 主要方向是前端，前端问题随便问
- 选择匠人，明智的选择
  - 课上讲的东西，会100%，work-related，会按照Qantas代码标准
  - 课上没有ppt，但会总结归纳出两份markdown
  - js.md: 2400行要全看
  - Markdown Language:标记语言
- 对标记语言的认识
  - HTML: 超文本标记语言，通过代码(tag)描述了一个网页的布局；例如，通过`<p>`标签及后面的文本，对段落结构进行描述；像这样，通过高于文本的文字描述，一般文本做不到的事情(布局)，这就叫标记
  - Markdown Language: 通过标记文本，实现文本样式布局
- 对阅读材料的再次提醒
  - JS.pdf要看完，2000多行看完后，能使你达到一个production-ready/work-ready的状态
  - React.pdf，从4000行缩到了2000多行，也要看完
- 讲课思路 ：
  - 授人鱼不如授人以渔
  - 与其说我们学的是知识和技术，不如说我们学的是写代码的方式和能力
  - 希望带给大家的，并不是教会你React怎么写，而是教会你：好的东西是什么样的，对的东西是什么样的，工作中用到的东西是什么样的
  - <font color=red> `所以我们的课，是面向bug学习，第一遍教你的东西是不对的，第二遍教你的东西是不工作的，第三遍教你的东西是不好的，最后再总结，归纳，写出对的，优雅的代码(elegant code)`</font>
  - 因为知识更新太快，每天焦虑学不过来，是一种错的状态，教给大家面向bug学习，是希望大家学会感受痛点，理解痛点，解决痛点
  - 弱类型 vs Java, C++, C#
  - 脚本语言 vs Java, C++, C#
  - 龙哥不会给你看P1的代码，因为再完美，也不是一个production ready的代码，因为<font color=red> `代码的技术已经过时了，但是为什么还要让大家去写，就是为了让大家感受痛点，去体会html, css中的坑，才会体会到es6的改进之处，再学完react，然后一遍遍深究，一遍遍反思，通过第一遍很难受很难看的代码，来总结出原来新知识新技术是为解决这些问题存在的`</font>
  - 通过上面的方法，来汲取新技术，才能永远站在知识的前沿；新技术只是为了解决问题应运而生
  > 总结就是，首先要学会面向bug的学习，代码写三遍，不断改进，然后学习新知识，知道新知识究竟改变和解决了原来代码的哪些问题，再应用，再复写，如此循环。

  ## 2.JS复习：JavaScript中必须要理解的几个概念
  JavaScript是弱类型脚本语言
  ### 2.1 弱类型 vs 强类型
    - 弱类型（JavaScript）：对用到的东西，不需要去关心它的类型，对很多类型有自动转换功能
    - 强类型（java, c++, c#）：要求声明每一个变量/参数/返回值的类型
  ### 2.2 脚本语言 vs 编译语言
    - 脚本语言（JavaScript）：解释性语言，不需要编译，直接通过运行器(runtime)运行
    - 编译语言(java, c++, c#)：代码需要编译(compile)然后才能运行(run)；经常会看到compile error
   
  ### 2.3 Keywords
    - `break, continue, debugger, do...while, for, function, if...else, return, switch, try...catch, var`
  ### 2.4 Statements
    - JavaScript 程序的执行单位为行(line)，也就是一行一行地执行。一般情况下，每一行就是一个语句
    - 语句以分号结尾，一个分号就表示一个语句结束。多个语句可以写在一行内，如果他们加了分号。
    - 如果严格遵循以一行为一个单位，则`;`可以省略
  ### 2.5 Variable 
    - JavaScript 的变量名区分大小写， `Name` 和 `name` 是两个不同的变量
    - 简单数据类型：`number, string, boolean, undefined, null`
    - 复杂数据类型：`object`
    > `function`,`array`在JavaScript 中的类型是`object`;在JavaScript 中有一句老话：everything is object, 你遇到的绝大多数东西都是作为`object`来处理的，所有东西都是object

    > ANZ 网考原题： function是以下哪种类型：  
    a.Function b.Object c.No types D:undefined

    > class是以下哪种类型：  
    a.Class b.Object c.No types D:undefined

    > 答案：b,b
  ### 2.6 变量提升(Hoisting)
    - 传统语言（python, ruby等）中，我们的习惯都是先声明再调用
    - 在JavaScript 我们可以先调用，再声明
    - JavaScript 的历史：
      - 碰瓷Java ，改名叫 JavaScript; 刚出来的时候不叫JavaScript ，但是不火，无人问津，后来改名JavaScript ，趁着Java 的大火，开始火起来
      - 碰瓷AI 编译，声称自己是人工智能编译；现在还没有很智能化的语言，如以下代码，是没有语言可以靠人工智能实现编译的：因为调用写在了声明和赋值前
      ```js
        console.log(result);
        a = 1;
        result = a + b;
        b = 1;
      ```
      但是JavaScript 做了一点妥协，实现了
      ```js
        a = 1;
        b = 1;
        result = a + b;
        var a, b, result;
      ```
      看上去比Java 的先声明再调用高级了一些，虽然JavaScript 的变量提升 意味着变量和函数的声明会在物理层面移动到代码的最前面， 实际上变量和函数声明在代码里的位置是不会动的，而是在编译阶段被放入内存中。只有声明是被提升的。
      正常代码只要运行一遍,逐行运行，就可以，比如
      ```js
        var a = 1; //写内存 a01
        var b = 1; //写内存 a02
        var result = a + b; //读内存 a01, a02 -> cpu -> 写内存a03
        console.log(result); //读内存 a03 -> cpu ->gpu 
      ```
      但是为了实现，JavaScript运行了两遍，第一遍遍历所有变量声明，写内存， 第二遍才是运行
  
      >虽然JavaScript 为实现代码，运行了两遍，但实际性能却变更好了；因为这样碰巧达到了现在`读写分离`的标准，先统一写内存，再读取进行运算。

  ### 2.7 Identifier(命名方式)
    - 第一个字符不可以是数字，不能包含星号，加号，减号或连词线
    - 中文是合法的标识符，可以用作变量名。

  ### 2.8 条件语句
     -  if...else
     -  `===` （严格相等判断的是内存地址）和 `==`比较
     -  switch...case
     -  三元表达式：`(条件) ? 表达式_左 : 表达式_右`
  ### 2.9 短路计算
    -  短路不代表死循环，意思是跳开/断开
    -  例如，
    ```js 
      const isOwnedACat = false;
      const myCatName = isOwenedACat && 'Luna';
      console.log(myCatName);
    ```
    `&&`如并联，一断均断，  
    false and anything -> false;   
    true and anything -> anything;
    ```js 
      const aNewDog = 'Kiera';
      const myNewPet = aNewDog || aNewCat;
      console.log(myNewPet);
    ```
    上面因为aNewDog已经有值了，所以js将不再关心aNewDog  
    `||`如串联，一通具通   
    true or anything ->true  
    false or anything -> anything
    - 短路计算是从左到右读
    - 短路计算举例
    ```js
        赚10000
        var 回家 = 出门捡到一万块钱 || 赚到了1000块钱 || 到了凌晨3点 || 老婆喊我回家

        if (出门捡到一万块钱 || 赚到了1000块钱 || 到了凌晨3点 || 老婆喊我回家) {
           回家();
        }

        if (没有看到老同学 && &&) {
          摆摊();
        }
   
    ```
    - 如果`出门捡到一万块钱, 赚到了1000块钱, 到了凌晨3点, 老婆喊我回家`中任一个为`true`，那就`回家（）`
    - 还有如`react`里显示dropdown:
    ```js 
        显示Dropdown
        显示Dropdown && (<div>My Dropdown</div>)
    ```
    如果Dropdown不存在，那就不显示，如果存在那就显示My Dropdown 
      
  ### 2.10 JavaScript 鸭子原则
    - 鸭子原则：如果一个东西，长得像鸭子，走路像鸭子，叫声像鸭子（即使不是鸭子），他一定就是鸭子 
    - 比如以下值所代表的
      - `undefined`: 空，虚无，没有，未定义
      - `null`: 空，虚无，没有，没有赋值
      - `''`: 空，没有值
      - `0`: 空
      - `false`: 没有
    - 它们长得很相像，走路很相像，叫声也很相像，所以有个统一的名字就叫`falsy`
    - 以上，它们长得很相像（类型可以不一样），走路很相像，叫声也很相像（行为一样），所以是一种东西
    - 用另外一种说法概括就是，如果一个东西，类型不一样，但是行为一样，那就是一种东西
      - 所以就引申出了，强比较(`===`)和弱比较(`==`)
    - 观察法所得，不是falsy的东西就是truthy


  ### 2.11 循环语句
    - `while`
    - `do...while`
    - `for`
    - `break / continue`
   
  ### 2.12 Function
    - 函数的声明：
    ```js
    function name(parameter1, parameter2, parameter3) { 
    }
    ```
    - 参数的省略：函数参数不是必需的，Javascript 允许省略参数
    ```js
    function f(a, b) { 
      return a;
    }

    f(1, 2, 3); // 1 
    f(1); // 1
    f(); // undefined 
    ```
    - 匿名函数与立即执行函数：
    ```js
    // 声明时没有给函数名
    var myFunction = function() {
      console.log(a.b);
    }

    myFunction();

    // 立即执行函数（IIFE），假设function只执行一次，没有任何复用性
    // 效果等于上面五行代码
    (function() {
      console.log(a.b);
    })()

    // 命名函数表达式的好处是当我们遇到错误时，堆栈跟踪会显示函数名，容易寻找错误。
    var myFunction = function namedFunction(){
    console.log(a.b);
    }
    ```

## 3.课上作业：感受痛点
作业一 FlightStops
```
given by an array of flights, returns stops statement to user.
ex.
flights: [{ origin: 'MEL', destination: 'CAN' }] -> Direct
flights: [{ origin: 'MEL', destination: 'CAN' }, { origin: 'CAN', destination: 'PVG' }] -> 1 stop
flights: [{ origin: 'MEL', destination: 'HKG' }, { HKG - CAN }, {}, { origin: 'CAN', destination: 'PVG' }] -> 3 stops
flights: [{ origin: 'MEL', destination: 'HKG' }, { HKG - CAN }, { CAN - SNG }, { origin: 'CAN', destination: 'PVG' }] -> n stops

Qantas 推出了一个环游世界的产品，当flights数量为27时，stops要返回 ‘Around The World';

Qantas 推出了一个太平洋梦想专线产品，当flights数量为11时，stops要返回 ‘The Dreamline';

Qantas 未来计划推出至少15个类似产品;


const flights = [{ origin: 'MEL', destination: 'CAN' }];
getStops(flights) // 'Direct'

arr.length 1 -> Direct 2 -> 1 stop 3 -> 2 stops 4 -> 3 stops 5 -> 4 stops n -> ... stop
```
作业二 TaxCalculation
|Income thresholds | Rate | Tax payable on this income |
|------------------|------|----------------------------|
|$0 – $18,200      |  0%  | Nil|
|$18,201 – $37,000 |  19% | 19c for each $1 over $18,200|
|$37,001 – $90,000 | 32.5%| $3,572 plus 32.5% of amounts over $37,000|
|$90,001 – $180,000| 37%  | $20,797 plus 37% of amounts over $90,000|
|$180,001 and over | 45%  | $54,096 plus 45% of amounts over $180,000|
ATO 由于疫情，调整了缴税比例，大幅下调了 3W7 到9W的税率，调低为 23.5%， 9W和 18W也要做到相应的下调
 ```js
 function calculateTaxPayable(income){

 }
 ```
 ### 3.1 课堂练习(第一遍)
 课堂练习（作业一）第一遍
 ```js
 function A(flights){
  let index = array.length;
  if (index === 1) {
    return "Direct";
  } else if (index === 2) {
    return "1 stop";
  } else {
  if (index === 27) {
    return "Around The World";
  } else if (index === 11) {
    return "The Dreamline";
  } else {
    return index + " stops";
  }
 }


 function B(flights){
  const stop = flights.length() - 1;
  let result;
  switch (stop){
  case 0:
    result = "direct";
    break;
  case 1:
    result = "1 stop";
    break;
  case 11:
    result = "The Dreamline";
    break;
  case 27:
    result = "Around The world";
    break;
  default:
    result = stop + "stops";
  }
  return result;

}
 ```
 每写一个If else扇自己一个耳光
   ```js
let flights = [{origin:"MEL", destination:"HKG"}];
let stopMapping = {
    1:"Direct",
    2:"1 stop"
}

function getStop (flights)
{
    return stopMapping[flights.length] || (flights.length - 1) + "stops" 
}
  ```

 课堂练习（作业二）第一遍：
 ```js
function calculateTax(income)
{
    var tax = 0;
    if (0 <= income && income <= 18200) {
    
    }

    else if (18201 <= income && income <= 37000){
        tax = (income - 18200) * 19 / 100;
    }

    else if (37001 <= income && income <= 90000) {
        tax = 3572 + (income - 37000) * 32.5 / 100;    
    }

    else if (90001 <= income && income <= 180000) {
        tax = 20797 + (income - 90000) * 37 / 100;
    }

    else if (180001 <= income) {
        tax = 54096 + (income - 180000) * 45 / 100;
    }

    return tax;
}
```
### 3.2 作业讲解
#### 3.2.1 RMR结合作业一详解
   首先记住三个单词：<font color=red> `Readable, Maintainable, Reusable`</font>（RMR）
  -  可读性，可维护性，可复用性（好的代码是有RMR特性的）
  > Q: 什么是好的代码  
    A： Readable, Maintainable, Reusable
  - 对`课堂练习（作业一）第一遍`，从可读性的角度来看，B要好于A
    - 好的代码写三遍
    - 第二遍，进行A,B的简化
    ```js
          function A(flights){
            let index = array.length - 1;
            if (index === 0) {
              return "Direct";
            }  
            
            if (index === 1) {
              return "1 stop";
            } 

            if (index === 11) {
              return "The Dreamline";
            } 
            if (index === 27) {
              return "Around The World";
            }  
              return index + " stops";         
          }


          function B(flights){
            const stop = flights.length() - 1;

            switch (stop){
            case 0:
              return "Direct";
            case 1:
              return "1 stop";
            case 11:
              return "The Dreamline";
            case 27:
              return "Around The world";
            default:
              return = stop + "stops";
            }
          }
    ``` 
    - 代码怎么写都能工作，但我们面试的时候，被刷下去的原因就是代码质量和细节
    - 如果有20个产品，第二遍的代码会增加20个`if...else`或者`case`，显然不好，那好的代码怎么写：第三遍
    ```js
       function getStops(flights){
         const stop = flights.length() - 1;

         const specialCases = {
           0: 'Direct',
           1: '1 stop',
           7: '',
           11: 'The Dreamline',
           12: '',
           27: 'Around The World`,
         };

         const specialCase = speciaCases[stop];

         if (specialCases){
           return specialCases;
         }

         return stop + 'stops';
       }
    ```
    - 上面这份代码为什么好，因为<font color=red> `符合人类正常思维`</font>，首先我们想它是不是在special case里，如果是，返回什么；如果不是在special case里，将直接返回什么
    > 为什么第三遍代码更优雅呢，因为它更符合人类正常思维 
    - 如果想写的更好，那就要<font color=red> `更符合语言的设计思路`</font>
      - 首先我们可以短路一下
      ```js
          function getStops(flights){
          const stop = flights.length() - 1;

          const specialCases = {
            0: 'Direct',
            1: '1 stop',
            7: '',
            11: 'The Dreamline',
            12: '',
            27: 'Around The World`,
          };

          const specialCase = speciaCases[stop]; 

          return specialCase || stop + 'stops';
        }
      ``` 
      - 我们为什么要声明一个变量，是因为我们希望把它保存起来以后再用，但明显这里specialCase与specialCases用不到，使用替换法，进一步精简代码，第四遍
      ```js
          function getStops(flights){
            const stop = flights.length() - 1;

            return {
              0: 'Direct',
              1: '1 stop',
              7: '',
              11: 'The Dreamline',
              12: '',
              27: 'Around The World`,
            }[stop] || stop + 'stops';
          }
      ``` 
      - 是要可读性还是要更高级
        - 如果写的是一种耳熟能详的语法，就没有牺牲它的可读性
        - 要把握住可读性与高级间的平衡点，不能为了高级而高级
      - 这种代码，你也可以写出来，首先要放弃一个观点：这个东西很简单，这样写这样写就可以（思而不学则怠）；也不能说我写出来了，能工作了，就够了（学而不思则罔）
        - 简单说就是，<font color=red> `要能够自我否定，好的代码写三遍`</font>
        > 自我否定就是：我写完了，但我就是写的不好，我尝试要写好它，我怎么才能写好它，我要绞尽脑汁的想怎么才能写好它，这个过程就是fishing的过程，要专注于过程。
#### 3.2.2 RMR结合作业二优化
  - 对`课堂练习（作业二）第一遍`的优化
    - 按照正常思维，A问B 我收入8w5, 我的工资多少；B会找到8W5的阶梯，通过8W5的阶梯计算税
    - 因此，首先我们要有一个taxTable, 然后通过我们注入的收入，查表，找到该收入所在的行来进行计算
    ```js
        const getMyIncomeTax2 = (income) => {
          const taxTable = [
            { min: 0, max: 18200, accumulate: 0, rate: 0 }, { min: 18200, max: 37000, accumulate: 0, rate: 0.19 },
            { min: 37000, max: 90000, accumulate: 3572, rate: 0.325 },
            { min: 9000, max: 120000, accumulate: 20797, rate: 0.37 }
            { min: 120000, max: 180000, accumulate: 22311, rate: 0.39 }
            {
              min: 180000,
              max: Number.POSITIVE_INFINITY,
              accumulate: 54097,
              rate: 0.45, 
            },
          ];

          for (let i = 0; i < taxTable.length; i++) {
            if (income <= taxTable[i].max)
              return (
              taxTable[i].accumulate + (income - taxTable[i].min) * taxTable[i].rate);
          }
        }；
    ```
    - 然后还可以更进一步按照`人类正常思维`优化，将更新的要求改完：
    ```js
      const TAX_TABLE_2020 = [{
            min: 0,
            max: 18200,
            floor: 0,
            base: 0,
            rate: 0,
        }, {
         min: 18201,
         max: 37000,
         floor: 18200,
         base: 0,
         rate: 0.19
        }, {
         min: 37001,
         max: 90000,
         floor: 37000,
         base: 3572,
         rate: 0.325
        }, {
         min: 90001,
         max: 180000,
         floor: 90000,
         base: 20797,
         rate: 0.37
        },{
         min: 180001,
         max: Number.POSITIVE_INFINITY,
         floor: 180000,
         base: 54096,
         rate: 0.45
        }];

      const calculateTax = (taxTable, income) => {
          
      let row;
  
      for(let i = 0; i < taxTable.length; i ++) {
        if (income > taxTable[i].min && income <= taxTable[i].max) {
          row = taxTable[i];

          break;
        }
      }

      const { floor, base, rate } = row; 
      return (income - floor) * rate + base;

    }
    ```

## 4.SOLID 原则
- 写P1，要符合人类思考方式（肯定是虚无缥缈的，但一定不是if...else,非黑即白肯定是不对的
- 代码中出现if...else 一定是有问题！这种有问题的感觉，我们称为
  - I'm feeling a bad smell in your code
  - 不能把这种小问题，称为issue/bug
- 把P1打回重写，有多少人，愿意去做（Refactor 重构），很难，因为大家自带舒适圈，永远觉得自己的代码写的挺好的。怎么打破这个舒适圈，就是SOLID原则。
- 掌握SOLID, 黄金秘籍，外挂, 半本(SOD)武功秘籍 也能走天下！
### 4.1 S:单一职责 Single Responsibility
  -  认为对象/功能/一段代码应该仅具有一种单一功能
  -  例如`课堂练习（作业一）第一遍：`，functionB中，每一个case的职责是不是都一样的，一样的有没有抽出来处理？好的代码写三遍！
  ```js
     function B(flights){
      const stop = flights.length() - 1;

      //单一抽出来处理呢？
      //没有 ！
      switch (stop){
        case 0:
          //职责？
          return "Direct";
        case 1:
          //职责？
          return "1 stop";
        case 11:
          //职责？
          return "The Dreamline";
        case 27:
          //职责？
          return "Around The world";
        default:
          //另一个职责
          return = stop + "stops";
      }
     }
  ```
  因此，职责分离可以修改为
  `[stop] || stop + 'stops'`  
### 4.2 O:开闭原则 Open/Close
  -  软件体应该是，对于扩展是开放的，对于修改是封闭的
  -  例如`课堂练习（作业一）第一遍：`，functionB中，当要增加或扩展功能的时候，是不是要改动核心代码块(switch)？对于更改是需要核心代码open的，就违背了O原则
  ```js
     function B(flights){
      const stop = flights.length() - 1;

      //当要增加或扩展功能的时候，是不是要改动核心代码块?
      //是 ！
      switch (stop){
        case 0:
          //职责？
          return "Direct";
        case 1:
          //职责？
          return "1 stop";
        case 11:
          //职责？
          return "The Dreamline";
        case 27:
          //职责？
          return "Around The world";
        default:
          //另一个职责
          return = stop + "stops";
      }
     }
  ```   
  Open/Close部分可以修改为  
  ```js
      return {
              0: 'Direct',
              1: '1 stop',
              11: 'The Dreamline',
              12: '',
              27: 'Around The World`,
            }
  ```
  这样扩展新功能，如增加12时，核心的逻辑完全没有动，只是更新了接口
 ### 4.3 L:里式替换
  -  程序中的对象，应该是可以在不改变程序正确性的前提下被它的子类所替换
### 4.4 I:接口隔离
  -  多个特定客户端接口，要好于一个宽泛用途的接口
### 4.5 D:依赖注入 Dependencies injection
  -  一个方法应该遵从“依赖于抽象而不是一个实例”
  -  例如`课堂练习（作业一）第一遍：`，functionB中，有没有依赖/需要一个东西，帮我们生成一个数据，这个依赖有没有单独提出来？
  ```js
     function B(flights){
      const stop = flights.length() - 1;

      //代码里面有没有依赖？（一个数据源去生成数据）依赖有没有单独提出来
      //有依赖，没有提出来 ！
      switch (stop){
        case 0:
          //职责？
          return "Direct";
        case 1:
          //职责？
          return "1 stop";
        case 11:
          //职责？
          return "The Dreamline";
        case 27:
          //职责？
          return "Around The world";
        default:
          //另一个职责
          return = stop + "stops";
      }
     }
  ```  
  依赖部分可以修改为
  ```js
            return {
              0: 'Direct',
              1: '1 stop',
              7: '',
              11: 'The Dreamline',
              12: '',
              27: 'Around The World`,
            }[stop] || stop + 'stops'; 
  ```
