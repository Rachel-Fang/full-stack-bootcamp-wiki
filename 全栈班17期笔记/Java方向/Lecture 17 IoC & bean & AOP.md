## Spring IOC and AOP
### What is Inversion of Control?
Inversion of Control i a principle in software engineering and IoC enables a framework
to take control of the flow of a program and make calls to our custom code. To enable
this, frameworks use abstractions with additional behaviour built in. If we want to add
our own behaviour, we need to extend the classes of the framework or plugin our
own classes.
- The advantages of this architecture are:
  - decoupling the execution of a task from its implementation
  - making it easier to switch between different implementations
  - greater modularity of a pr gram
  - greater ease in testing a program by isolating a component or mocking its
  - dependencies and allowing components to communicate through contracts
IoC 主要的作⽤就是解耦各个组件，让⾼层模块不依赖底层模块，⽽是让两者依赖接⼝和
抽象来实现。Ioc的思想最核⼼的地⽅在于，资源不由使⽤资源的双⽅管理，⽽由不使⽤
资源的第三⽅管理，这可以带来很多好处。
1. 资源集中管理，实现资源的可配置和易管理。
2. 降低了使⽤资源双⽅的依赖程度，也就是我们说的耦合度。
 
### What is Dependency Injection?
- Dependency injection is a pattern through which to implement IoC, where the control
being inverted is the setting of object’s dependencies.
The act of connecting objects with other objects, or “injecting” objects into other objects,
is done by an assembler rather than by the objects themselves.
 
- DI and IoC work together
Downside of DI: management of dependencies is inconvenient
If we want to add another dependency to MyClass2, we have to change code by ourselves.
public class Main {
  public static void main(Str ng[] args) {
    MyClass4 myClass4 = new MyClass4();
    MyClass3 myClass3 = new MyClass3();
    MyClass2 myClass2 = new MyClass2(myClass3, myClass4);
    MyClass1 myClass1 = new MyClass1(myClass2);
    myClass1.doSomething();
  }
}
 
### DI and IoC work together
With IoC, the dependencies are managed by the container, and the programmer is relieved of that burden.Using annotations like @Autowired, the container is asked to inject a dependency where it is needed, and the programmers do not need to create/
manage those dependencies by themselves.
  ```
    public class MyClass2 {
      @Autowired
      private MyClass3 myClass3;
      @Autowired
      private MyClass4 myClass4;
      public void doSomething(){
        myClass3.doSomething();
        myClass4.doSomething();
      }
    }
  ```
 
### Spring开发的策略
Spring最根本的使命：简化Java开发。
为了降低Java开发的复杂性，Spring采取以下4种关键策略：
- 基于POJO的轻量级和最⼩侵入性编程
- 通过依赖注入和⾯向接⼝实现松耦合
- 基于切⾯和惯例进⾏声明式编程
- 通过切⾯和模版减少样板⽰代码
 
### IOC
IoC（Inversion of Control，控制倒转），是spring的核⼼，贯穿始终。所谓IoC，对于spring框架来说，就是由spring来负责控制对象的⽣命周期和对象间的关系。所有的类都会在spring容器中登记，告诉spring你是个什么，你需要什么，然后spring会在系统运⾏到适当的时候，把你要的东⻄主动给你，同时也把你交给其他需要你的东⻄。所有的类的创建、销毁都由 spring来控制，也就是说控制对象⽣存周期的不再是引⽤它的对象，⽽是spring。对于某个 体的对象⽽⾔，以前是它控制其他对象，现在是所有对象都被spring控制，所以这叫控制反转。
IoC 容器需要具备两个基本的功能：
- 通过描述管理 Bean，包括发布和获取 Bean；
- 通过描述完成 Bean 之间的依赖关系。
 
### The Spring IoC Container
Spring中将IoC容器管理的对象称为Bean，这个和JavaBean并没有什么关系。。
- BeanFactory：在 Spring 的定义中，它要求所有的 IoC 容器都需要实现接⼝BeanFactory，它是⼀个顶级容器接⼝。Bean⼯⼚，借助于配置⽂件能够实现对JavaBean的配置和管理，⽤于向使⽤者提供Bean的实例。
- ApplicationContext：ApplicationContext构建在BeanFactory基础之上，提供了更多的实⽤功能。 在现实中我们使⽤的⼤部分Spring IoC 容器是 ApplicationContext 接⼝的实现类
 
### 通过扫描装配Bean
- 如果⼀个个的 Bean 使⽤注解@Bean 注入 Sprin IoC 容器中，很⿇烦。 Spring 允许我们进⾏扫描装配 Bean 到 IoC 容器中，对于扫描装配⽽⾔使⽤的注解是@Component 和@ComponentScan。@Component 是标明哪个类被扫描进入 Spring IoC 容器，⽽@ComponentScan 则是标明采⽤何种策略去扫描装配 Bean。

### Setter-Based Dependency Injection
For setter-based DI, the container will call sett r methods of our class, after invoking a no-argument nstructor or no-argument static factory method to instantiate the bean. Let’s create t s configuration using annotations:
Constructor-based and setter-based types of injection can be combined for the same bean. The Spring documentation recommends using constructor-based injection for mandatory dependencies, and setter-based injection for optional ones.
 
### Field-Based Dependency Injection
- we can inject the dependencies by marking them with an @Autowired annotation
  ```
    public class Store {
    @Autowired
    private Item item;
    }
  ```
- While constructing the Store object, if there’s no constructor or setter meth d to inject the Item bean, the container will use reflection to inject Item into Store. This approach might look simpler and cleaner but is not recommended to use because it has a few drawbacks such as:
- This method uses reflection to inject the dependencies, which is costlier than constructor-based or setter-based injection
- It’s really easy to keep adding multiple dependencies using this approach. If you were using constructor injection having multiple arguments would have made us think that the class does more than one thing which can violate the Single Responsibility Principle.

### Autowired注解
@Autowired 的缺省规则：⾸先它会根据类型找到对应的 Bean，如果对应类型的 Bean 不是唯⼀的，那么它会根据其属性名称和 Bean 的名称进⾏匹配。如果匹配得上，就会使⽤该 Bean；如果还⽆法匹配，就会抛出异常。
 
### Autowired注解
- 消除歧义性——@Primary和@Quelifier
- @Primary 的含义告诉 Spring IoC 容器，当发现有多个同样类型的 Bean 时，请优先
使⽤这个进⾏注入
- @Qualifier 的配置项 value 需要⼀个字符串去定义，它将与@Autowired 组合在⼀起，
通过类型和名称⼀起找到 Bean。
 
### 带有参数的构造⽅法类的装配
使⽤@Autowired注解对构造⽅法的参数进⾏注入
  ```
    @Component
    public cla s BussinessPerson implements Person {
      private Animal animal = null;

      public BussinessPerson(@Autowired @Qualifier("dog") Animal
      animal) {
        this.animal = animal;
      }
      @Override
      public void service() {
        this.animal.use();
      }
      @Override
      public void setAnimal(Animal animal) {
        this.animal = animal;
      }
    }
  ```
 
### Bean 的⽣命周期的过程
- Spring IoC 初始化和销毁 Bean 的过程，这便是 Bean 的⽣命周期的过程，它⼤致分为 Bean 定义、Bean 的初始化、Bean 的⽣存期和 Bean 的销毁4个部分。
- Bean 定义过程⼤致如下：
  - Spring通过我们的配置，如@ComponentScan 定义的扫描路径去找到带有@Component 的类，这个过程就是⼀个资源定位的过程。
  - ⼀旦找到了资源，那么它就开始解析，并且将定义的信息保存起来。注意，此时还没有初始化 Bean，也就没有 Bean 的实例，它有的仅仅是 Bean 的定义。
  - 然后就会把定义发布到容器中。此时，IoC 容器也只有Bean的Bean

### Spring IoC
定义，还是没有 Bean 的实例⽣成。
- 完成了这3步只是⼀个资源定位并将 Bean 的定义发布到 IoC 容器的过程，还没Bean 实例的⽣成，更没有完成依赖注入。在默认的情况下，Spring 会继续去完成
Bean 的实例化和依赖注入，这样从 IoC 容器中就可以得到⼀个依赖注入完成的Bean。
 
### Bean 的初始化流程
- ComponentScan 中还有⼀个配置项 lazyInit，只可以配置 Boolean 值，且默认值为false，也就是默认不进⾏延迟初始化，因此在默认的情况下 Spring 会对 Bean 进⾏实例化和依赖注入对应的属性值。
 
### 使⽤属性⽂件
- 在 Spring Boot 中使⽤属性⽂件，可以采⽤其默的 application.properties，也可以使⽤⾃定义的配置⽂件。
  ```
    compileOnly "org.springframework.boot:spring-boot-configuration-processor"
    @Value("${database.driverName}")
    @ConfigurationProperties("database")
  ```

### 使⽤@Profile 指定不同环境
- 启动的时候选择选项 -Dspring.profiles.active 配置的值记为{profile}，则它会⽤application-{profile}.properties ⽂件去代替原来默认的 application.properties ⽂件，通过这样就能够有效地切换各类环境，如开发、测试和⽣产。
JAVA_OPTS="-Dspring.pr files.active=dev"
 
### AOP
- Aspect Oriented Programming
- ⾯向切⾯编程是⾯向对象编程的有益补充。aop是将那些与业务⽆关，却为业务模块所
共同调⽤的逻辑或责任进⾏封装。
- 应⽤AOP的功能举例：
Authentication 权限
Caching 缓存
Context passing 内容传递
Error handling 错误处理
Lazy loading　懒加载
Debugging　　调试


