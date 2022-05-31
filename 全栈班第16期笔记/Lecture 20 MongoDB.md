# Lecture 20 MongoDB


## 主要知识点
- [Lecture 18 MongoDB](#Lecture-18-mongodb)
  - [20.1 数据库类型](#201-数据库类型)
  - [20.2 MongoDB](#202-mongodb)
  - [20.2.1 Structure Terminology](#2021-structure-terminology)
  - [20.2.2 Document and data types](#2022-document-and-data-types)


## 课堂笔记

#### 20.1 数据库类型
- SQL structured qurey language
关系型数据库
- No SQL / not only sql
非关系数据库 

- SQL sample
  - MySQL
  - PostgresQL
  - SQLite

- non-SQL sample
  - document-orientated -> mongodb 数据库中的数据以一个个的document的形式存储
  - key-value -> redis
  - graph-oriented -> neo4j
  - column-family -> cassandra
  
#### 20.2 MongoDB
- humongous 庞大的
- No-SQL 非关系型数据库
- Stores data in JSON-like documents
  - _id: ObjectId 
  - BSON - Binary JSON
- Flexibility and schemaless
  - 可以处理数据格式不一致（schemaless）的数据,如下
```
[
  {
    _id: xxx1,
    name:yyy，
    age:10,
    dob:xxxx
  },
  {
    _id:xxx2,
    username:yyy
   }
]
```

- schemaless 的优势：数据容易迭代和更新,可以很容易地修改数据的格式，但修改数据时会出现修改前后数据不一致的问题，这时候需要写一个script进行计算
- schemaless 的劣势：无法方便地遍历数组，需要进行各种判断
#### 20.2.1 Structure Terminology
- Database Server中有许多数据库（Database1，Database2），数据库中有许多的collection（User collection、Task collection），collection中有多个document，同样的类型的document会组成一个collection，document中有许多fields
- document 格式：`{_id:xxx,name:"mason"}`
!(structure)(./img/图50.png）
- client与server连接
  - cli - mongo shell
  - gui - mongo compass
  - script - mongo-client,mongoose
- 命令行输入`mongo`，如果server已经打开，则会显示连接成功
#### 20.2.2 Document and data types
- _id: 自动生成，不指定类型，默认用 ObjectID
- data types：
  - Boolean
  - Number(int32,int64,float)
  - Date(ISODate,timestamp)
#### 20.2.3 Start mongo server
- Run the following command in separate terminal
  - mongod 在当前的命令行里启动并管理database server
  - mongo 
- 把MongoDB当作服务启动：
  - 每次电脑启动时都会把MongoDB自动启动
> 'mongod' is not recognized as an internal command解决方法：把`mongod.exe`所在的路径贴到命令行上，或加入系统环境变量
- mongo shell：基于javascript的运行环境  
#### 20.2.4 MongoDB Command
- 使用数据库(可以使用当前存在的或者不存在的） 
  - `use school`
- 输入数据
  - `db.student.insertOne({name:"mason"})`
- 查找数据
  - `db.student.find()`
- 查看collection
  - 'show collection`
> { "_id" : ObjectId("629342745c178724d96c2a26"), "name" : "mason" } 与 { "_id" : "629342745c178724d96c2a26", "name" : "mason" } 是不同的数据类型
- 更新数据
- 



