### 01 Exception handling
#### The Error Class and the Exception Class
- The **Error** class is used to indicate a serious problem that the application should _not_ try to handle.
- The **Exception** class is used when there is a less catastrophic event that the application _should_ try to handle.

#### The Throwable Class
- Throwable类是整个Java异常体系的超类，都有的异常类都是派⽣生⾃自这个类。包含Error和 Exception两个直接⼦子类。
> - Error表⽰示程序在运⾏行行期间出现了了⼗十分严重、不可恢复的错误，在这种情况下应⽤用程序只能中⽌止运⾏行行，例例如JAVA虚拟机出现错误。在程序中不⽤用捕获Error类型的异常。⼀一般情况下，在程序中也不应该抛出Error类型的异常。
> - Exception是应⽤用层⾯面上最顶层的异常类，包含RuntimeException（运⾏行行时异常）和 Checked Exception（受检异常）。

#### Checked vs Unchecked Exceptions
未经检查的异常
- **未经检查**的异常是编译器未知的异常。
- 因为这些异常只在运行时才知道，所以它们也被称为_运行时异常_。
- 它们是编程错误的结果，通常是算术错误（例如除以 0）。
- 当我们期望方法的调用者无法从异常中恢复时，使用未经检查的异常。
  
>RuntimeException是⼀一种Unchecked Exception，即表⽰示编译器不会检查程序是否对RuntimeException作了了处理理，在程序中不必捕获RuntimException类型的异常，也不必在⽅方法     体声明抛出RuntimeException类。⼀一般来说，RuntimeException发⽣生的时候，表⽰示程序中出现了了编程错误，所以应该找出错误修改程序，⽽而不是去捕获RuntimeException。常⻅见的
  RuntimeException有NullPointException、ClassCastException、IllegalArgumentException、IndexOutOfBoundException等。

检查异常
- **编译器知道已检查**的异常。
- 如果我们调用的方法可能会引发检查异常，则_必须_对其进行处理（否则我们会从编译器中得到一个错误）。
- 当我们期望方法的调用者_可以_从异常中恢复时，使用检查的异常。

>Checked Exception是相对于Unchecked Exception⽽而⾔言的，所有继承⾃自Exception并且不是 RuntimeException的异常都是Checked Exception。JAVA 语⾔言规定必须对checked Exception 作处理理，编译器会对此作检查，要么在⽅方法体中声明抛出checked Exception，要么使⽤用catch 语句句捕获checked Exception进⾏行行处理理，不然不能通过编译。常⽤用的Checked Exception有
  IOException、ClassNotFoundException等。
 
#### Exception handling
要处理异常，我们需要编写一个**异常处理程序。**这涉及三个主要组成部分：
-   一块`try` block
-   一块`catch` block
-   一块`finally` block
```java
try {
    read();
}
catch (FileNotFoundException ex){
    ex.getLocalizedMessage();
}
finally {
}
```
NB: 在实际工作项目中，Exception handling一般要占据代码总量的30%甚至40%.
 原则性问题-异常处理理机制初衷：
>1.将不可预期异常的处理理代码和正常的业务逻辑处理理代码分离。
   2.异常只应该⽤用于处理理非正常情况，不要⽤用异常处理理来代替正常流程控制。（对于完全可知的、处理理⽅方式清晰的错误，程序本应该提供相应的错误代码，⽽而不是笼统称为异常）
   3.先捕获⼩小异常，再捕获⼤大异常（Exception e ⽤用此表⽰示未知异常）
   4.对于完全已知的错误应该编写处理理这种错误的代码，增加程序健壮性。
   企业应⽤用做法：程序先捕获原始异常，然后抛出⼀一个新的业务异常，新的业务异常中包含对⽤用户的提⽰示信息	这种做法叫异常转译。因为核⼼心是：`在合适的层级处理理异常。`
 
### 02 Log
- Log 分为很多level：
	- DEBUG：指定对调试应用程序最有用的细粒度信息事件。
	- INFO：指定在粗粒度级别突出显示应用程序进度的信息性消息。
	- WARN：指定可能有害的情况。
	- ERROR：指定可能仍允许应用程序继续运行的错误事件。
	- FATAL：指定可能导致应用程序中止的非常严重的错误事件。
- In production, do not use System.out as log tool
- Log4j, logback
- Use log configuration
- And suggest to use slf4j: slf4j是⼀一套包装Logging 框架的界⾯面程式， 以外观模式实现。可以在软件部署的时候决定要使⽤用的  Logging  框架，⽬目前主要⽀支援的有Java Logging API、log4j及logback等框架。https://zh.wikipedia.org/wiki/SLF4J

### 03 Object Oriented Programming
#### Inheritance
- **继承**是一个类从另一个类获取属性和方法。以下是您应该记住的有关继承的一些关键点：
>  1.我们想从_一般到具体。_**父**类或**超类**是最通用的，子**类**或**子类**是更具体的。
     2.通过**扩展**超类，您声明子类属于_超类类型_。当我们不确定子类是否继承自父类时，我们可以使用“is a”测试（例如，汽车_是_车辆）。
     3.超类和子类之间的关系_只有一种方式_。子类需要知道超类，但超类永远不应该知道它的子类。
     
超`Object`类
- 每个类都继承自超类`Object`。因为所有对象都继承自`Object`类，所以所有对象都有一些方法，无论它们是什么类型。

#### Polymorphism
在 Java 中，可以使用任何类型的继承来支持多态性。在我们的车辆示例中，每个车辆都有两种形式——例如，一个`Car`对象既是 a`Car`也是 a `Vehicle`（因为它继承自`Vehicle`类）。因此，任何`Car`对象都有两种形式。这就是多态性。

如果我们想获得所有`Car`, `Boat`, 和`Plane`对象的速度，我们可以很容易地做到这一点，因为多态性——我们只需创建一个包含所有类型对象的列表，`Vehicle`并获取每个`Vehicle`对象的速度，不管其他任何类型可能是的对象。
举例：
```java
// Create an array of size 3 and type Vehicle
Vehicle [] vehicles = new Vehicle[3];

// Instantiate three new objects and add them to the array.
// It looks like these are all different types (Car, Plane, and Boat),
// but they all inherit from the Vehicle class, so in addition to the types
// they get from their subclasses, they are also all Vehicle objects.
vehicles[0] = new Car(); 
vehicles[1] = new Plane();
vehicles[2] = new Boat();

// Iterate over the array and print the speed
// of each of the Vehicle objects.
for (int i = 0; i < vehicles.length; i++) {
    vehicles[i].speed();
}
```
#### Abstract Classes
**抽象类**具有以下关键特征：

-   它定义了每个子类的行为，但我们不能直接实例化抽象类本身。
-   它允许我们创建**抽象方法**。
		-   抽象方法是不包含实现主体的方法。相反，它只是为该方法提供了一个标头。
	    -   扩展抽象类的子类需要覆盖所有抽象方法并提供特定的实现。
**重要**！ Functional Interfaces:
- An interface that has a single abstract method is called a functional interface

举例：
```java
public class FunctionInterfaces {  
  
  @FunctionalInterface  
  public interface Foo {  
    String method(String string);  
  }  
  
  private String add(String string, Foo foo) {  
    return foo.method(string);  
  }  
  
  public String tryFunction() {  
    Foo foo = parameter -> parameter + " from lambda";  
    return add("Message", foo);  
  }  
  
  private boolean isPersonEligibleForVoting(Person person, Predicate<Person> predicate){  
    return predicate.test(person);  
  }  
  
  public void testPredicate() {  
    Person person = new Person("Alex", 23);  
    // Created a predicate. It returns true if age is greater than 18.  
    Predicate<Person> predicate = p -> p.age > 18;  
  
    boolean eligible = isPersonEligibleForVoting(person , predicate);  
    System.out.println("Person is eligible for voting: " + eligible);  
  }  
  
  public void tryFunctions() {  
    Function<String, Integer> lengthFunction = str -> str.length();  
    System.out.println("String length: " + lengthFunction.apply("This is awesome!!"));  
  
    Function<Integer,Integer> increment = x -> x + 10;  
    Function<Integer,Integer> multiply = y -> y * 2;  
  
    // Since we are using compose(), multiplication will be done first and then increment will be done.  
    System.out.println("compose result: " + increment.compose(multiply).apply(3));  
  
    // Since we are using andThen(), increment will be done first and then multiplication will be done.  
    System.out.println("andThen result: " + increment.andThen(multiply).apply(3));  
  }  
  
  public void tryBiFunction() {  
    BiFunction<Integer, Integer, String> add = (a, b) -> String.valueOf(a + b);  
  
    System.out.println("Sum = " + add.apply(2, 3));  
  }  
  
  
  class Person {  
    String name;  
    int age;  
  
    Person(String name, int age){  
      this.name = name;  
      this.age = age;  
    }  
  
    public int getAge() {  
      return age;  
    }  
  
    public void setAge(int age) {  
      this.age = age;  
    }  
  }  
}
```

### 04 单元测试
![unit test](./img/unit_test.png)
![utPriciple](./img/ut_principle.png)

