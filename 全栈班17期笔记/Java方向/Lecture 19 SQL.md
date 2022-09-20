## SQL

### 数据库
- Data Persistence
- Why?
- Compared with file
非关系型数据库(NoSQL)：MongoDB，LevelDB……
关系型数据库(SQL)：Sqlite，MySQL，PostgreSQL，SQL Server……
 
### 数据库表
- ⼀个数据库通常包含⼀个或多个表。每个表由⼀个名字标识（例如“客户”或者“订单”）。
- 表包含带有数据的记录（⾏）。 下⾯的例⼦是⼀个存个⼈信息的表：
 
### SQL
- 结构化查询语⾔ (SQL) 是⽤于访问SQL数据库的标准语⾔
- SQL 是⼀⻔ ANSI 的标准计算机语⾔，⽤来访问和操作数据库系统。
- SQL 语句⽤于取回和更新数据库中的数据。
- SQL 可与数据库程序协同⼯
- 存在着很多不同版本的 SQL 语⾔，但是为了与 ANSI 标准相兼容，它们必须以相似的⽅式共同地来⽀持⼀些主要的关键词（比如 SELECT、UPDATE、DELETE、INSERT、WHERE 等等）
- 除了 SQL 标准之外，⼤部分 SQL 数据库程序都拥有它们⾃⼰的私有扩展
 
### SQL语法
* SQL 对⼤⼩写不敏感！
* 某些数据库系统要求在每条 SQL 命令的末端使⽤分号。
分号是在数据库系统中分隔每条 SQL 语句的标准⽅法，这样就可以在对服务器的相
同请求中执⾏⼀条以上的语句。
* 可以分⾏
 
### 安装数据库
* Postgres docker version
* pgAdmin Client
 
### SQL 数据定义语⾔ (DDL)
- CREATE DATABASE 创建数据库
- CREATE TABLE 创建新表
- ALTER TABLE 变更（改变）数据库表
- DROP TABLE 删除表
- CREATE INDEX 创建索引（搜索键）
- DROP INDEX 删除索引

### CREATE DATABASE 语句
CREATE DATABASE ⽤于创建数据库。
SQL CREATE DATABASE 语法
CREATE DATABASE database_name
 
### CREATE TABLE 语句
CREATE TABLE 语句⽤于创建数据库中的表
SQL CREATE TABLE 语法
  ```
    CREATE TABLE 表名称
    (
    列名称1 数据类型,
    列名称2 数据类型,
    列名称3 数据类型,
    ....
    )
  ```
 
### CREATE TABLE 语句
- SQL 数据类型
- 数据类型（data_type）规定了列可容纳何种数据类型。
- 下⾯的表格包含了SQL中最常⽤的数据类型：
![data type](image/j12.png)
 
### CREATE TABLE 语句
SQL 约束
可以在创建表时规定约束（通过 CREATE TABLE 语句），或者在表创建之后也可以（通过 ALTER TABLE 语句）。
常⻅以下⼏种约束：
- NOT NULL： 不可为空
- UNIQUE：不可重复
- PRIMARY KEY：主键
- FOREIGN KEY：外键，⼀个表中的 FOREIGN KEY 指向另⼀个表中的
PRIMARY KEY（语法取决于数据版本）
- CHECK：值约束（语法取决于数据版本）
- DEFAULT：默认值
 
### CREATE TABLE 语句
创建⼀个价格历史数据表
CREATE TABLE "price_history" (
`ID` INTEG R PRIMARY KEY AUTOINCREMENT UNIQUE,
`datetime` INTEGER NOT NULL,
`exchange` TEXT,
`symb` TEXT,
`price` REAL
)
 
### CREATE INDEX 语句
创建索引
```sql
CREATE INDEX `datetime` ON `price_history` (`datetime` )
```
 
### SQL 数据操作语⾔ (DML)
- SELECT - 从数据库表中获取数据
- UPDATE - 更新数据库表中的数据
- DELETE - 从数据库表中删除数据
- INSERT INTO - 向数据库表中插入数据
 
### SELECT 语句
SELECT 语句⽤于从表中选取数据。
结果被存储在⼀个结果表中（称为结果集）。
语法
SELECT 列名称 FROM 表名称
以及：
SELECT * FROM 表名称
注释：SQL 语句对⼤⼩写不敏感。SELECT 等效于 select。
 
### SELECT 语句
SQL SELECT 实例
SELECT datetime, price FROM price_history
SQL SELECT * 实例
请使⽤符号 * 取代列的名称，就像这样：
SELECT * FROM price_history
 
### Limit 语句
SELECT * FROM price_history LIMIT 10
 
### SELECT DISTINCT 语句
在表中，可能会包含重复值。
关键词 DISTINCT ⽤于返回唯⼀不同的值。
语法：
SELECT DISTINCT 列名称 FROM 表名称
使⽤ DISTINCT 关键词
SELECT DISTINCT exchange FROM price_history
 
### WHERE ⼦句
SELECT * FROM pri e_history where exchange = 'OKCoin'
引号的使⽤
* SQL 使⽤单引号来环绕⽂本值（⼤部分数据库系统也接受双引号）
* 如果是数值，不要使⽤引号。
 
AND & OR 运算符
AND 和 OR 可在 WHERE ⼦语句中把两个或多个条件结合起来。
如果第⼀个条件和第⼆个条件都成立，则 AND 运算符显⽰⼀条记录。
如果第⼀个条件和第⼆个条件中只要有⼀个成立，则 OR 运算符显⽰⼀条记录。
 
SELECT * FROM price_history where exchange = 'OKCoin'
and datetime > 1510933571
SELECT * FROM price_history where exchange = 'OKCoin' or
exchange = 'Bitfinex'
结合 AND 和 OR 运算符
我们也可以把 AND 和 OR 结合起来（使⽤圆括号来组成复杂的表达式）:
SELECT * FROM price_history
where
(exchange = 'OKCoin' or exchange = 'Bitfinex')
and datetime > 1510933571
 
LIKE 操作符
LIKE 操作符⽤于在 WHERE ⼦句中搜索列中的指
定模式。
SQL LIKE 操作符语法
SELECT column_name(s)
FROM table_name
WHERE column_name LIKE pattern
 
SELECT * FROM price_history
where
symb like '%AUD'
SELECT * FROM price_history
where
symb not like '%AUD'
 
BETWEEN 操作符
操作符 BETWEEN ... AND 会选取介于两个值之间的数据范围。这些值可以是数值、⽂
本或者⽇期。
SQL BETWEEN 语法
SELECT column_name(s)
FROM table_name
WHERE column_name
BETWEEN value1 AND value2
 
WHERE ⼦句
SELECT * FROM price_history
where dat time
BETWEEN 1510933500 AND 1510933550
 
ORDER BY ⼦句
ORDER BY 语句⽤于根据指定的列对结果集进⾏排序。
ORDER BY 语句默认按照升序对记录进⾏排序。
如果希望按照降序对记录进⾏排序，可以使⽤ DESC 关键字。
 
ORDER BY ⼦句
SELECT * FROM price_history SELECT * FROM price_history
order by datetime
order by datetime, exchange
SELECT * FROM price_history
order by datetime DESC
SELECT * FROM price_history
order by datetime, exchange desc
 
INSERT INTO 语句
INSERT INTO 语句⽤于向表格中插入新的⾏。
语法
INSERT INTO 表名称 VALUES (值1, 值2,….)
我们也可以指定所要插入数据的列：
INSERT INTO table_name (列1, 列2,...) VALUES (值1, 值2,....)
 
INSERT INTO 语句
插入新的⾏
SQL 语句：
INSERT INTO exchange VALUES (1, 'Bitfinex', 'https://www.bitfinex.com/', '')
在指定的列中插入数据
SQL 语句：
INSERT INTO exchange (name,url) VALUES ('Bitstamp', 'https://www.bitstamp.net')
 
UPDATE 语句
Update 语句⽤于修改表中的数据。
语法：
UPDATE 表名称 SET 列名称 = 新值 WHERE 列名称 = 某值
 
更新某⼀⾏中的若⼲列
更新某⼀⾏中的⼀个列
UPDATE exchange
UPDATE exchange
SET url = 'https://
www.bitstamp.net/', comments = 'OK'
WHERE name = 'Bitstamp'
SET url = 'https://
www.bitstamp.net/'
WHERE name = 'Bitstamp'
 
DELETE 语句
DELETE 语句⽤于删除表中的⾏。
语法
DELETE FROM 表名称 WHERE 列名称 = 值
 
DELETE 语句
删除所有⾏
删除某⾏
可以在不删除表的情况下删除所有的⾏。这意味着表的结构、
属性和索引都是完整的：
DELETE FROM
exchange
WHERE
DELETE FROM table_name
或者：
ID = 3
DELETE * FROM table_name
 
SQL JOIN
引⽤两个表
SELECT *
FROM exchange, price_history
WHERE exchange.name = price_history.exchange
使⽤ Join
SELECT *
FROM price_history
INNER JOIN exchange
ON exchange.name = price_history.exchange
 
SQL JOIN
不同的 SQL JOIN
除了我们在上⾯的例⼦中使⽤的
INNER JOIN（内连接），我们还可
以使⽤其他⼏种连接。
- JOIN: 如果表中有⾄少⼀个匹
配，则返回⾏
- LEFT JOIN: 即使右表中没有匹
配，也从左表返回所有的⾏
- RIGHT JOIN: 即使左表中没有
匹配，也从右表返回所有的⾏
- FULL JOIN: 只要其中⼀个表中
存在匹配，就返回⾏
 
UNION 操作符
SQL UNION 操作符
UNION 操作符⽤于合并两个或多个 SELECT 语句的结果集。
请注意，UNION 内部的 SELECT 语句必须拥有相同数量的列。列也必须拥有相似
的数据类型。同时，每条 SELECT 语句中的列的顺序必须相同。
SQL UNION 语法
```sql
SELECT column_name(s) FROM table_name1
UNION
SELECT column_name(s) FROM table_name2
```
 
GROUP BY 语句
语法
⽤于结合合计函数，根据⼀个或多个列对结果集进⾏分组。
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
 
GROUP BY 语句
⽰例
```sql
SELECT *,COUNT(price) FROM price_history
GROUP BY exchange
```
不⽤GROUP BY会对所有⾏进⾏计算
```sql
SELECT *,COUNT(price) FROM price_history
```
 
GROUP BY 语句
计算平均
```sql
SELECT *,avg(price) FROM price_history
GROUP BY exchange, symb
```
 
HAVING ⼦句
在 SQL 中增加 HAVING ⼦句原因是，WHERE 关键字⽆法与合计函数结果⼀起使⽤。
记录超过30条的交易所
错误⽰例：
正确⽰范
```sql
```sql
SELECT *,COUNT(price) FROM SELECT *,COUNT(price) FROM
price_history
GROUP BY exchange
WHERE COUNT(price) > 30
```
price_history
GROUP BY exchange
HAVING COUNT(price) > 30
```
 
HAVING ⼦句
HAVING 语法
```sql
SELECT column_name, aggregate_function(column_name)
FROM table_name
WHERE column_name operator value
GROUP BY column_name
HAVING aggregate_function(column_name) operator value
```
