# Lecture 20 MongoDB


## 主要知识点
- [Lecture 18 MongoDB](#Lecture-18-mongodb)
  - [20.1 数据库类型](#201-数据库类型)
  - [20.2 MongoDB](#202-mongodb)
  - [20.2.1 Structure Terminology](#2021-structure-terminology)
  - [20.2.2 Document and data types](#2022-document-and-data-types)
  - [20.2.3 Start mongo server](#2023-start-mongo-server)
  - [20.2.4 MongoDB Command](#2024-mongodb-command)
  - [Quiz](#quiz)


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
- Name: Text(string)
- Hobbies:array(array of string)
- Address: object(embeded document)
- Wishes: array(array of documents)
- 其他常见data类型：
  - Boolean
  - Number(int32,int64,float)
  - Date(ISODate,timestamp)
#### 20.2.3 Start mongo server
- Run the following command in separate terminals
  - mongod 在当前的命令行里启动并管理database server(把terminal和mongo进程绑在一起）
  - mongo 
- 把MongoDB当作服务启动：
  - 每次电脑启动时都会把MongoDB自动启动
> 'mongod' is not recognized as an internal command解决方法：把`mongod.exe`所在的路径贴到命令行上，或加入系统环境变量
- mongo shell：基于javascript的运行环境  
#### 20.2.4 MongoDB Command
- 显示当前数据库的databases
  - `show dbs`
- 显示当前数据库的集合
  - `show collections` 
- 使用数据库(可以使用当前存在的或者不存在的） 
  - `use school`
  - 当数据库中有数据时，才会显示在db列表中
- 输入数据
  - 添加一个数据`db.students.insertOne({name:"mason"})`  name加不加双引号都可以，因为类似javascript，但是存起来之后是json格式，所以加了引号
    - `db` 指向了当前的数据库 
    - `students`对collection students进行操作
    - `insertOne()`添加一个文档
    - `{
        "acknowledged" : true,
        "insertedId" : ObjectId("62adbcb4fd2f44f3aa3e8111") 
      }` 如果没有指定id，MongoDB会帮我们自动生成一个id,id的生成没有规律
  - 添加多个数据 `db.students.insertMany([{},{}])` 
      
- 查找数据
  - `db.students.find()`
  - `db.students.find({name:"mason"})` 找到所有包含name:mason的数据

> { "_id" : ObjectId("629342745c178724d96c2a26"), "name" : "mason" } 与 { "_id" : "629342745c178724d96c2a26", "name" : "mason" } 是不同的数据类型
- 更新数据
  -`db.students.updateOne({name:"mason"},{$set:{name: "james"}})` 
  - `db.students.updateOne({name:"mason"},{$set:{age: 20}})` 
  - `db.students.updateOne({name:"mason"},{$set:{age: 20}},{upsert:true})` 找到就添加，没有找到就添加一个新的document包含我们想要的字段
    - `{
        "acknowledged" : true,
        "matchedCount" : 0,
        "modifiedCount" : 0,
        "upsertedId" : ObjectId("62adcd1d0a0a4e438830a79c")
       }`  
    - `{ "_id" : ObjectId("62adcd1d0a0a4e438830a79c"), "name" : "jason", "age" : 20 }`
  - update 找到第一个符合条件的document就更新了
- 删除数据
  - `db.students.deleteOne({name:"mason"})`
  - `db.students.deleteMany({name:{$exists:true}})` 

#### Quiz

- `db.students.insertOne({name:"mason",dob:new Date()})`
- `db.students.insertMany([{name:"jason",dob:new Date()},{name:"eden",dob:new Date()}])` 
- `db.students.updateOne({},{$set:{results:[80,90,100]}})`
- `db.students.updateOne({name:"jason"},{$set:{results:[80,90,100]}})`
- `db.students.updateOne({name:"eden"},{$set:{results:[90,100]}})`
- `db.students.find({results:90},{name:1,result:1,_id:0})`
- `db.students.deleteMany({})`
- `db.students.drop()`

> 如果一个db里没有数据，它是不会显示在db list里的

#### 20.2.5 Relations
- 表和表的关系(建立在站在谁的角度上看的）
  - 1 to 1 (相对的，对于某个student来说，其和address的关系是1对1）
  - 1 to many
  - Many to many （一个A可以对应多个B，一个B可以对应多个A）
    - 学生和课程 多对多
    - 一个课程只允许一个老师，一个老师只允许上一个课程 1对1
    - 一个课程允许多个老师，一个老师只允许上一个课程 1对多 
- 表达关系的形式
  - Embedded 嵌入式
  - Reference 引用式  
 - Example：
  - 1 to 1 Embedded
    - id
    - name
    - address
      - city
      - address
      - postcode
  - 1 to 1 Reference
    - id
    - name
    - address：（ address id）
    -（in another collection）
    - id
    - city
    - address
    - postcode
    - student：（student id）
  - 1 to many Embedded
    - id
    - name
    - addresses
      - object 0
        - city
        - address
        - postcode
      - object 1
        - city
        - address
        - postcode
  - 1 to many Reference
    - id
    - name
    - address
      - 0
      - 1
    - (in another collection)
    - id: object 0
    - city
    - address
    - postcode
    - student: (student id) 
    - id: object 1
    - city
    - address
    - postcode
    - student: (student id)  
  - many to many 
  ![many to many](./img/图50.jpg）       
