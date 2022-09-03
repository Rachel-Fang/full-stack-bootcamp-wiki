### 01 Spring Boot 背景
- 从 Spring 说起，2000 年左右 Java 行业中都是 EJB 的天下， 但是 EJB 本身比较庞大复杂，各企业使用起来并不是很便利。
- Rod Johnson认为企业开发应该更简单，没有必要全部使用EJB，企业开发应该是一个统一的、高效的方式构造整个应用， 并且可以将单层框架以最佳的组合揉和在一起建立一个连贯的体系。
- Rod Johnson 2002 年编写了Expert One-on-One J2EE Design and Development》。这本书是Rod Johnson的成名著 作 ， 非 常 经 典 ， 从 这 本 书 中 的 代 码 诞 生 了 S p r i n g Framework。
- Spring 在不断发展的过程中也出现了一些问题，随着 Spring 边界不断扩张，需要的配置文件也越来越多，使用起来也越复杂， 项目中也经常因为配置文件配置错误产生很多问题。慢慢Spring  变成了一个大而全的框架，背离它简洁开发的理念。随着微服务的概念兴起， Spring 开发了一个全新的技术栈： Spring Boot。
 
### 02 Spring Boot Framework
Spring Boot 是由 Pivotal 团队提供的全新框架，其设计⽬目的是⽤用来简化新 Spring 应⽤用的初始搭建以及开发过程。该框架使⽤用了了特定的⽅方式来进⾏行行配置，从⽽而使开发⼈人员不再需要         定义样板化的配置。采⽤用 Spring Boot 可以⼤大⼤大的简化开发模式，所有你想集成的常⽤用框架，它都有对应的组件⽀支持。

https://spring.io/projects/spring-boot 官网介绍：
Spring Boot makes it easy to create stand-alone, production-grade Spring based Applications that you can "just run".
We take an opinionated view of the Spring platform and third-party libraries so you can get started with minimum fuss. Most Spring Boot applications need very little Spring configuration.
 
Spring Boot 是⼀一套全新的框架，它来⾃自于 Spring ⼤大家族，因此 Spring 所有具备的功能它都有，⽽而且更更容易易使⽤用；Spring Boot 以约定⼤大于配置的核⼼心思想，默认帮我们进⾏行行了了很多设置，多数 Spring Boot 应⽤用只需要很少的 Spring 配置。Spring Boot 开发了了很多的应⽤用集成包，⽀支持绝⼤大多数开源软件，让我们以很低的成本去集成其他主流开源软件。

Spring Boot 特性
- 使⽤用 Spring 项⽬目引导⻚页⾯面可以在⼏几秒构建⼀一个项⽬目
- ⽅方便便对外输出各种形式的服务，如 REST API、WebSocket、Web、Streaming、Tasks
- 非常简洁的安全策略略集成
- ⽀支持关系数据库和非关系数据库
- ⽀支持运⾏行行期内嵌容器，如 Tomcat、Jetty
- 强⼤大的开发包，⽀支持热启动
- ⾃自动管理理依赖
- ⾃自带应⽤用监控
- ⽀支持各种 IED，如 IntelliJ IDEA 、NetBeans
 
### 03 Why Spring Boot
- 从软件发展的⾓角度来讲，越简单的开发模式越会流⾏行行。简单的开发模式解放出更更多⽣生   产⼒力力，让开发⼈人员可以将精⼒力力集中在业务上，⽽而不是各种配置、语法所设置的⻔门槛上。Spring Boot 就是尽可能的简化应⽤用开发的⻔门槛。
- Spring Boot 所集成的技术栈，⼏几乎都是各互联⽹网公司在使⽤用的技术，按照 Spring
Boot 的路路线去学习，基本可以了了解国内外互联⽹网公司的技术特点。
- Spring Boot 和微服务架构都是未来软件开发的⼀一个⼤大趋势，越早参与其中受益越⼤大。
 
### 04开始第⼀一个项⽬目
  - 访问 SPRING INITIALIZR http://start.spring.io/。
  - 选择构建⼯工具 Gradle, Spring Boot 版本 2.1.1 及⼀一些⼯工程基本信息，可参考下图

#### com.company.project 目录下：
- ProjectNameApplication.java：建议放到根目录下面，是项目的启动类，Spring Boot 项目只能有一个 main() 方法。
- util/comm：目录建议放置公共的类，如全局的配置文件、工具  类等。
- domain/model/entity：目录主要用于实体（Entity）与数据访问层（Repository）。
- repository：数据库访问层代码。
- service：该层主要是业务类代码。
- web/controller：该层负责页面访问控制。
- factory, handler, builder⋯
- resources 目录下：
  - static：目录存放 Web 访问的静态资源，如 JS、CSS、图片等。
  - templates：目录存放页面模板。
  - application.properties：项目的配置信息。
- test ⽬目录存放单元测试的代码


### 05 Spring Data JPA
- 对象关系映射（Object Relational  Mapping，简称  ORM）模式是⼀一种为了了解决⾯面向对象与关系数据库存在的互不匹配的现象技术。简单的说，ORM 是通过使⽤用描述对象和数据库之间映射的元数据，将程序中的对象⾃自动持久化到关系数据库中
- 当开发⼀一个应⽤用程序的时候（不使⽤用 O/R  Mapping），你可能会写不少数据访问层的代码，⽤用来从数据库保存、删除、读取对象信息等。在 DAL 中写了了很多的⽅方法来读取对象数据、改变状态对象等任务，⽽而这些代码写起来总是重复的。 针对这些问题
ORM 提供了了解决⽅方案，简化了了将程序中的对象持久化到关系数据库中的操作。
- ORM 框架的本质是简化编程中操作数据库的编码，在 Java 江湖中发展到现在基本上就剩两家，⼀一个是宣称可以不⽤用写⼀一句句 SQL 的 Hibernate，⼀一个是以动态 SQL ⻅见⻓长的MyBatis，两者各有特点。在企业级系统开发中可以根据需求灵活使⽤用，发现⼀一个有趣的现象：传统企业⼤大都喜欢使⽤用 Hibernate，⽽而互联⽹网⾏行行业通常使⽤用 MyBatis。
- JPA（Java Persistence API）是 Sun 官⽅方提出的 Java 持久化规范，它为 Java 开发
⼈人员提供了了⼀一种对象/关联映射⼯工具来管理理 Java 应⽤用中的关系数据，它的出现主要是为了了简化现有的持久化开发⼯工作和整合 ORM 技术，结束现在 Hibernate、TopLink、
- JDO 等 ORM 框架各⾃自为营的局⾯面。值得注意的是，JPA 是在充分吸收了了现有
Hibernate、TopLink、JDO 等 ORM 框架的基础上发展⽽而来的，具有易易于使⽤用、伸缩性强等优点。从⽬目前的开发社区的反应上看，JPA 受到了了极⼤大的⽀支持和赞扬，其中就包括了了 Spring 与 EJB3.0 的开发团队。
- 注意：JPA 是⼀一套规范，不是⼀一套产品，像  Hibernate、TopLink、JDO  他们是⼀一套产品，如果说这些产品实现了了这个 JPA 规范，那么我们就可以叫他们为 JPA 的实现产品。
 
### 06 Spring Data JPA
- Spring Data JPA 是 Spring 基于 ORM 框架、JPA 规范的基础上封装的⼀一套 JPA 应⽤用框架，可使开发者⽤用极简的代码即可实现对数据的访问和操作。它提供了了包括增、删、改、查等在内的常
⽤用功能，且易易于扩展。学习并使⽤用 Spring Data JPA 可以极⼤大提高开发效率。
- Spring Data JPA 让我们解脱了了 DAO 层的操作，基本上所有CRUD 都可以依赖于它来实现。

- 添加依赖：
  ```
    compile('org.springframework.boot:spring-boot-starter-data-jpa') 
    compile('mysql:mysql-connector-java') 
    compile('org.apache.commons:commons-lang3:3.1')
  ```
- 添加配置⽂文件：
  ```
    Spring.datasource.url=jdbc:mysql://localhost:3306/test 
    Spring.datasource.username=root 
    Spring.datasource.password=root
    Spring.datasource.driver-class-name=com.mysql.jdbc.Driver

    Spring.jpa.properties.hibernate.hbm2ddl.auto=update 
    Spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5InnoDBDialect 
    Spring.jpa.show-sql= true
  ```

- 添加配置⽂文件： hibernate.hbm2ddl.auto 参数的作⽤用主要⽤用于：⾃自动创建|更更新|验证数据库表结构，有四个值：
  - create：每次加载 hibernate 时都会删除上⼀一次的⽣生成的表，然后根据你的 model 类再重新来⽣生成新表，哪怕两次没有任何改变也要这样执⾏行行，这就是导致数据库表数据丢失的⼀一个重要原因。
  - create-drop ：每次加载 hibernate 时根据 model 类⽣生成表，但是 sessionFactory ⼀一关闭，表就
⾃自动删除。
  - update：最常⽤用的属性，第⼀一次加载 hibernate 时根据 model  类会⾃自动建立起表的结构（前提是先建立好数据库），以后加载 hibernate 时根据 model类⾃自动更更新表结构，即使表结构改变了了， 但表中的⾏行行仍然存在，不会删除以前的⾏行行。要注意的是当部署到服务器后，表结构是不会被⻢马上建立起来的，是要等应⽤用第⼀一次运⾏行行起来后才会。
  - validate ：每次加载 hibernate 时，验证创建数据库表结构，只会和数据库中的表进⾏行行比较，不会创建新表，但是会插入新值。
- dialect 主要是指定⽣生成表名的存储引擎为 InnoDB；
- show-sql 是否打印出⾃自动⽣生产的 SQL，⽅方便便调试的时候查看。
 
### 07 基本查询
- 基本查询也分为两种，一种是 Spring Data 默认已经实现，一种是根据查询的方法来自动解析成 SQL。

- 复杂查询
在实际的开发中需要⽤用到分⻚页、筛选、连表等查询的时候就需要特殊的⽅方法或者⾃自定义SQL。

- ⾃自定义 SQL 查询
使用 Spring Data 大部分的 SQL 都可以根据方法名定义的方式来实现，但是由于某些原因我们想使用自定义的 SQL 来查询，Spring Data 也可以完美支持；在SQL的查询方法上面使用  @Query 注解，如涉及到删除和修改需要加上  @Modifying。也可以根据需要添加  @Transactional对事物的支持，查询超时的设置等。

- 多表查询
多表查询在 Spring Data JPA 中有两种实现⽅方式，第⼀一种是利利⽤用 Hibernate 的级联查询来实现， 第⼆二种是创建⼀一个结果集的接⼝口来接收连表查询后的结果，这⾥里里主要使⽤用第⼆二种⽅方式。
特别注意这里的 SQL 是 HQL，需要写类的名和属性
 
- More
使用枚举的时候，如果选择数据库中存储的是枚举对应的 String 类型，而不是枚举的索引值，需要在属性上面添加
@Enumerated(EnumType.STRING) 注 解 ：
  ``` 
    @Enumerated(EnumType.STRING) 
    @Column(nullable = true)
    private UserStatus status;
