## Spring Data JPA
- 对象关系映射（Object Relational  Mapping，简称  ORM）模式是⼀一种为了了解决⾯面向对象与关系数据库存在的互不匹配的现象技术。简单的说，ORM 是通过使⽤用描述对象和数据库之间映射的元数据，将程序中的对象⾃自动持久化到关系数据库中
- 当开发⼀一个应⽤用程序的时候（不使⽤用 O/R  Mapping），你可能会写不少数据访问层的代码，⽤用来从数据库保存、删除、读取对象信息等。在 DAL 中写了了很多的⽅方法来读取对象数据、改变状态对象等任务，⽽而这些代码写起来总是重复的。 针对这些问题
ORM 提供了了解决⽅方案，简化了了将程序中的对象持久化到关系数据库中的操作。
- ORM 框架的本质是简化编程中操作数据库的编码，在 Java 江湖中发展到现在基本上就剩两家，⼀一个是宣称可以不⽤用写⼀一句句 SQL 的 Hibernate，⼀一个是以动态 SQL ⻅见⻓长的MyBatis，两者各有特点。在企业级系统开发中可以根据需求灵活使⽤用，发现⼀一个有趣的现象：传统企业⼤大都喜欢使⽤用 Hibernate，⽽而互联⽹网⾏行行业通常使⽤用 MyBatis。
- JPA（Java Persistence API）是 Sun 官⽅方提出的 Java 持久化规范，它为 Java 开发
⼈人员提供了了⼀一种对象/关联映射⼯工具来管理理 Java 应⽤用中的关系数据，它的出现主要是为了了简化现有的持久化开发⼯工作和整合 ORM 技术，结束现在 Hibernate、TopLink、
- JDO 等 ORM 框架各⾃自为营的局⾯面。值得注意的是，JPA 是在充分吸收了了现有
Hibernate、TopLink、JDO 等 ORM 框架的基础上发展⽽而来的，具有易易于使⽤用、伸缩性强等优点。从⽬目前的开发社区的反应上看，JPA 受到了了极⼤大的⽀支持和赞扬，其中就包括了了 Spring 与 EJB3.0 的开发团队。
- 注意：JPA 是⼀一套规范，不是⼀一套产品，像  Hibernate、TopLink、JDO  他们是⼀一套产品，如果说这些产品实现了了这个 JPA 规范，那么我们就可以叫他们为 JPA 的实现产品。
 
### Spring	Data	JPA
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
 
### 基本查询
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
  ```

不需要和数据库映射的属性
正常情况下实体类上加入注解	@Entity，就会让实体类和表相关连，如果其中某个属性我们不需要和数据库来关联只是在展示的时候做计算，只需要加上 @Transient 属性既可。
```
@Transient
private String fullName;
@Transient private int age;
```

### 连接多个数据源
在项目开发中，常常需要在一个项目中使用多个数据源，因此需要配置 Spring Data JPA 对多数据源的使用，一般分为以下三步：
- 配置多数据源
- 不同源的 repository 放入不同包路径
 
- SQL注入是比较常⻅见的⽹网络攻击⽅方式之⼀一，它不是利利⽤用操作系统的BUG来实现攻击，⽽而是针对程序员编程时的疏忽，通过SQL语句句，实现⽆无帐号登录，甚⾄至篡改数据库。
比如在⼀一个登录界⾯面，要求输入⽤用户名和密码： 可以这样输入实现免帐号登录：
⽤用户名： ‘or 1 = 1 --
密 码：
点登陆,如若若没有做特殊处理理,那么这个非法⽤用户可以登陆进去。从理理论上说，后台认证程序中会有如下的SQL语句句：
  ```
  String sql = "select * from user_table where username= ' "+userName+" ' and password=' "+password+" '";
  ```
当输入了了上⾯面的⽤用户名和密码，上⾯面的SQL语句句变成： 
  ```
  SELECT * FROM user_table WHERE username= '’or 1 = 1 -- and password='’
  ```

1.	永远不要信任⽤用户的输入，要对⽤用户的输入进⾏行行校验，可以通过正则表达式，或限制⻓长度，对单引号和双"-"进⾏行行转换等。
2.	永远不要使⽤用动态拼装SQL，使⽤用参数化的SQL或者直接使⽤用存储过程进⾏行行数据查询存取。
3.	永远不要使⽤用管理理员权限的数据库连接，为每个应⽤用使⽤用单独的权限有限的数据库连接。
4.	不要把机密信息明⽂文存放，请加密或者hash掉密码和敏感的信息。
5.	应⽤用的异常信息应该给出尽可能少的提⽰示，最好使⽤用⾃自定义的错误信息对原始错误信息进⾏行行包装，把异常信息存放在独立的表中。
