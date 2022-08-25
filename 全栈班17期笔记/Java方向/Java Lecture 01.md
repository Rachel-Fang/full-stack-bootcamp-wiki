### 1.0 Server-side application
#### What is backend development?
- 后端开发意味着在服务器端软件上工作，该软件专注于您在网站上看不到的所有内容。后端开发人员确保网站正常运行，重点关注数据库、后端逻辑、应用程序编程接口 （API）、体系结构和服务器。它们使用可帮助浏览器与数据库通信、存储、理解和删除数据的代码。

- 后端偏逻辑，而逻辑在不同语境下有不同的含义，也就是说要理解环境，程序运行在不同的地方的时候，不一定可以顺利运行. 
>建议：
	- 去了解production怎么部署的，怎么看到它的Log，怎么保证它是正确运行的(可以请Devops的同学帮忙).
	- 工作后了解production或UAT的环境，对production的环境有敬畏之心.
	- 重要：做项目对Dev的要求，要求了解不同的隔离环境。CI/CD pipeline 比如 jenkins怎么一步步部署的steps,怎么 login 到production，怎么去做trouble shooting，知道自己的DB在哪里，production run在哪里，Cache Deployment. 
![developing-process](./img/Developing_process.png)

### 2.0 Backend Roadmap
#### [文章版](https://www.geeksforgeeks.org/back-end-developer-roadmap-2022/)
#### [图片版](https://roadmap.sh/backend)

![Roadmap1](./img/Roadmap1.png)
- Internet 部分
> HTTP怎么去work？面试常问 http的get 和post的区别?
> 后面还会涉及到 rest and point，那怎么样去设计一个好的rest API?
> Domin name做P3的时候会用到，需要知道怎么去处理它
> Hosting了解就可以
> HTML CSS 和 JavaScript吃饭的东西必须会
- OS 部分
> Java开发的绝大部分的环境都是Linux的，所以就要会用一部分terminal的命令
> Basic Terminal Commands是需要会用的
> 我们现在写那个shell的机会少，不用特别的关注. 
> 其余了解即可
- Version Control 部分
> 概念需要清楚，什么应该放在Version Control里面，像git ignore，比如pipeline相关的这种file，还有一些script，docker file相关的需要放。
> 比如，Java这种只放source其他不放，所有的output过程中，Build出来的.class和炸包，这些必须全部都exclusive的. 这样一来，如果dependency管理和code维护的好，那么使用一样的JDK和gradle可以和本机build出来一样的class
![Roadmap2](./img/Roadmap2.png)
- DB部分
> NodeJS常用NoSQL,而我们Java用Relational DB多，我们的课会将PostgreSQL作为例子.
> 数据库的ORMs,ACID,Transactions,N+1 Problem,等都比较重要，Database Normalization, Database indexes是比较基础的东西必须会. 其他简单了解。
- API 部分
> 绝大部分涉及到的是REST Api，Json API也会涉及到一些
> Authentication这类加密解密的，安全相关课程中不会特别多的讲到，大家知道P3中是怎么用就好了
![Roadmap3](./img/Roadmap3.png)
- Testing 部分
>  Integration Testing，Unit Testing，Functional Testing我们都会涉及到.
>  TDD（Test-drive development）参考作业
> 
> 劳神的补充：没有test cases的保证，代码根本就无法保证，甚至难以修改，因为改完了也不知道是否有问题
- CI/CD 部分
> CI/CD pipeline这个东西，不要求大家一定会写，但一定要知道它每步做什么，这个流程要非常的清楚
- Design and development principles 部分
>  1. SOLID
>      Single Responsibility
		Open/Closed
		Liskov Substitution
		Interface Segregation
		Dependency Inversion
>   2. KISS - Keep It Simple, Stupid
>   3. YAGNI - You Aren't Going to Need It
>   4. DRY - Don't Repeat Yourself 
>   5. Separate of concern - Separating a computer program into distinct sections. Each section addresses a separate concern
- Architectural patterns 部分
> 我们在最后一节课会讲到, Microservices怎么用是什么到时候会讲
> junior职位对这个要求不高
- Search engines和Message Brokers 部分我们基本不涉及
- Containerization vs. Virtualization 部分
> Docker一定会用到的, 现在基本会把backend deploy到AWS去.所以会用到打包
> 
- GraphQL 部分会简单涉及到
- 不会涉及到Graph database 和Websockets, Web servers
- Building for Scale 我们会涉及到一些

### 3.0 Java Basic
#### 3.1 Java History
**两个优点**

1. 写一次，run everywhere Run在JVM上
2. Gabbage collection  避免了内存泄漏（没写好还是会存在内存泄漏）

**Java 8 - Java 17改进**


#### 3.2 Java Roadmap

![java roadmap](/roadmap.png)
- 多线程在澳洲找工作和实际使用中出现频率不高

> 其中使用场景比较多的包括：
    Streams,Collection,Serialization, Build Tools, Spring, Spring Boot, Logging(能帮助debug的log)
    
#### 3.3 Development Environment
**Java 17**

本期开发使用

**Intellij IDEA**

使用Analyze->Inspect Code检查代码

**Google Java Style Guide**

格式化代码

#### 3.4 How does Java work
Source code-> Java compiler-> Byte Code -> Java Virtual machine（JVM）<-> OS

JDK包含JRE包含JVM

![java roadmap](/JVM.png)

[Baeldung](https://www.baeldung.com/)

[JDK文档](https://docs.oracle.com/en/java/javase/17/docs/api/)

推荐Java阅读群里资料

#### 3.5 Java 语法
#### Variables and Types

#### All Primitives in Java
- byte
- short
- int
- long
- float
- double
- char
- boolean

#### Array
- Always prefer lists to array
	写算法的时候才常用，不推荐实际项目中使用
	实际项目中推荐使用List<>
	Java 是面向对象的语言，实际项目中希望list of sth更有意义，但是数组有限制而且表示的意义不清晰

#### Conditions
- 条件越多，程序复杂度越高。
	把程序写简单是非常难的
	我们的目标是写 self-explained code 

#### Loop
- for, while, forEach
``` java

public void forEach() {

        int[] primes = {2, 3, 5, 7, 11, 13};

  

        for (int p : primes) {

            System.out.println(p);

        }

        List.of(2, 3, 5, 7, 11, 13).forEach(System.out::println);

        List.of(2, 3, 5, 7, 11, 13).forEach(i -> System.out.println(i));

        Arrays.stream(primes).forEach(System.out::println);
    }

```
#### Class
- 面向对象
	*Always override hashCode when you override equals*
	Class Object(JDK)
	面试：具体项目中或者业务相关的class
	看JDK上的equals和hashcode（重写hashcode）

***作业一***
NB: Class name必须是名词，对应的function name，method name.

#### Methods and FUnctions
- public 
- private 
- protected
	建议先加private再根据场景改public
> protected 场景
> 默认是protected，一般会限制在package里。

*Minimisse the accessibility of classes and members*

NB: **method/function name必须是动词或者动词加名词**

#### String
-  **Immutable**创建出了以后无法改变
-  需要熟悉String的相关操作：indexOf, subString, concat,etc.
- 正则表达式：校验，查找

*Be ware the performance of string concatenation*
注意连接string的性能，使用“+”会影响性能
其他常用包括split

#### Java Collections Framework

![](/collection.png)

实际使用的是紫色的class

其中会包含一些算法，比如sort

面试常问：

*LinkedList vs ArrayList*

***作业二***

Set: 当需要返回所有都是unique
Deque: 需要使用双端队列的时候，会使用linkedlist
ArrayList: 允许有重复数据

#### Map

场景是因为像字典，查询更快，用空间换时间

  

*Item64: Refer to objects by their interface*

定义的部分（等号左边）是interface

``` java

// Good

Set<Book> books = new LinkedHashSet<>();

Map<String, String> authorBookMap = new HashMap<>();

List<String> sentences = new ArrayList<>();

```

  

定义的时候就是用class，不灵活

```

// Bad - uses class as type!

LinkedHashSet<Book> books = new LinkedHashSet<>();

HashMap<String, String> authorBookMap = new HashMap<>();

ArrayList<String> sentences = new ArrayList<>();

```

#### 序列化和反序列化

I/O操作

序列化：在硬盘上传输，或网络层上传输。

反序列化：嫁给你二进制转化为对象读取

场景：数据库读写，网络传输

  

**I/O操作通常是系统中操作最慢的地方**

log数量多少也会影响系统的性能

  

影响开发程序中：

1.自己调用其他的api，要加timeout，并且考虑性能问题

2.数据库读写，操作性能，所以尽可能减少对数据库访问的次数

  

#### Java 8 lambda

在String中用的比较多

  

#### Java 9 Optional

避免空指针异常

三种构造方式：

Optional.of(obj),Optional.ofNull(obj),Optional.empty()

  

存在即返回

  

*TIPS:使用 Optional 时尽量不直接调用Optional.get() 方法, Optional.isPresent()更应该被视为一个私有方法, 应依赖于其他像 Optional.orElse(),Optional.orElseGet(), Optional.map() 等这样的方法.*

  

```java

    private int getValue() {

        System.out.println("Called here");

        return 20;

    }

  

    public void useOptional() {

        Optional<Integer> a = Optional.of(10);

        int result = a.orElse(getValue());

        int anotherResult = a.orElseGet(() -> getValue());

    }

```

a.orElse(getValue())

当写一个函数在orElse里，不管a的value，一定先回跑一边里面的函数

但是orElseGet()只有在a是empty的情况下才会跑里面的函数

  

举例：

```java

    private int getValue() {

        System.out.println("Called here");

        return 20;

    }

  

    public void useOptional() {

        Optional<Integer> a = Optional.of(10);

        int result = a.orElse(getValue());

        a = Optional.empty()

        int anotherResult = a.orElseGet(() -> getValue());

    }

```

  

#### Java 8 Stream

将需要处理的元素集合看作一种流，流在管道上传输，并且可以在管道节点中处理，比如排序，筛选等。

  

Example:

```java

    public void generateStream() {

        List<String> strings = List.of("abc", "", "bc", "efg", "abcd", "", "jkl");

        List<String> filtered = strings.stream().

                filter(s -> !s.isEmpty()).

                collect(Collectors.toList());

        filtered.forEach(System.out::println);

    }

  

    public void mapExample() {

        List<Integer> numbers = List.of(3, 2, 2, 3, 7, 3, 5); // 获取对应的平方数

        List<Integer> squaresList = numbers.stream()

                .distinct()

                .map(i -> i * i)

                .collect(Collectors.toList());

    }

```

map:映射每个元素对应的结果

filter通过设置条件过滤出元素

limit：获取指定数量的流

sorted：排序

Collectors:实现了归约操作，将流转化为集合和聚合元素

统计：一些产生统计结果的收集器也很有用，主要用于int,double,long

  

*Item46: Prefer side-effect-free functions in streams*

*Item47: Prefer Collection to Stream as a return type*

  

Example:

``` java

 public void mapExample() {

        List<Integer> numbers = List.of(3, 2, 2, 3, 7, 3, 5); // 获取对应的平方数

        List<Integer> squaresList = numbers.stream()

                .distinct()

                .map(i -> i * i)

                .collect(Collectors.toList());

  

        AtomicInteger count = new AtomicInteger();

        squaresList.forEach(i -> count.getAndIncrement());

    }

```

  

**How to rewrite the following code**

  
  
  

```java

    public String merge(int high, int low) {

        List<String> results = new ArrayList<>();

        for (int index = high; index >= low; index--) {

            results.add("test " + index);

        }

        return String.join("\n", results);

    }

```

  

Solution:

```java

    public String enhancedMerge(int high, int low){

        return IntStream.rangeClosed(low,high)

                .mapToObj(i -> "test" + (high -i + low))

                .collect(Collectors.joining("\n"));

    }

```
