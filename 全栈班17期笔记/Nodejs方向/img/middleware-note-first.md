# Lecture 12 Express.js

## 主要知识点

- [Lecture 10 Express.js](#Lecture-10-express.js)
- [主要知识点](#主要知识点)
  - [课堂笔记](#课堂笔记)
    - [10.1 express](#101-express)
	- [10.2 Middleware](#102-Middleware)
  - [作业](#作业)


## 课堂笔记

#### 10.1 express
- Fast, unopinonated,minimalist web framework for Node.js
  - 基础入门的框架
  - 可以达到CRUD的所有功能
  - 有一个很容易扩展的基础
- Alternatives: Koa
  - 语法 80% 一样（课上不会提到）
- Framework build from express: Loopback, keystoneJS
```js
const express = require("express")；

const app = express()；

app.get（‘/’，（req，res）=>{
	res.send('hello world');
});
app.listen(3000);
```

- `const express = require("express")` 导入
- `const app = express()` 通过express创建了一个app对象，不接受参数
	- method为HTTP method例如`GET POST`等
- `application.http-method(path, callback => route handler)` 绑定middleware
  - `app.get('/',(req, res) => {res.send('ok!!!!');})` 
	- req->request res->response 一般不用缩写除非被整个行业公认
    - path 字符串或者正则表达式Regex 
	  - 上面的代码对应下来就是 GET /
	  - GET / 开发时不用在乎 / 之前的域名是什么，/之后的部分才是需要关心的
	  - express使用path matcher机制来检测当前的请求有没有能够符合提前在代码里写好的，并且method也是一样的，如果有就会触发相应的callback function；如果没有则不会触发
    - callback function
	  - `res.send()` 
		- return data back to client
		- 使用最广泛的
	  - `res.json()`
		- 专门用来返回json格式的数据，default status code是200，想要改变用`res.status()`
		- `res.send()`和`res.json()`区别： 
		  - `res.send()`里有逻辑检测，检测传给send的参数是什么类型。如果监测到是一个object的形式，他会把他转化成json并调用`res.json()`返回回去
		  - `res.json()`会简化上述步骤
	  - `res.sendStatus()` Staus -> staus code
		- 如果在返回body里不想返回任何内容，可以返回status code
	  - `res.status()` 又想设置status（不返回statuscode）又想返回body
		- `res.status(201).json({})`
	- `app.listen()` 监听一个端口
	- 常用端口: 3000 4200 8080 9000
- 如何从request里取数据？
	1. `req.body` -> POST, PUT, PATCH 创建修改数据时使用，不可见，必须使用express.json() middleware
```js
app.use（express.json());

app.post（'/',(req,res)=> {
	const { name } = req.body;
	
	res.send({name});
});
```
这时如果使用postman给网址url发一个post请求，body为`{"name":"mason"}`, server会返回`{"name":"mason"}`


   2. `query.params /？query=value` -> 一般只有GET会使用 只从url里面取，取问号后的变量 需要定义才能取到值 常用于id
      - `req.query` -> GET 筛选
```js
app.post('/ users',(req,res)=>{
	const{ name } = req.body;
	const{ title } = req.query;
	
	res.json({name, title});
});
```
网址url为 `localhost:3000/?title=mr` 继续使用上面的post请求，会返回
```js
{
	"name":"mason"，
	"title":"mr"
}
```
 3. `route param / books/:id` 什么方法都可以使用 去在url中，问号前的数据
```js
app.post('/:id',(req,res)=>{
	const{ name } = req.body;
	const{ title } = req.query;
	const{ id } = req.params;
	
	res.json({name.title,id});
});
```
网址url为 `localhost:3000/abc123?title=mr` 继续使用上面的post请求，会返回
```js
{
	"name":"mason"，
	"title":"mr"，
	"id"："abc123"
}
```

#### 10.2 Middleware
- Middleware像是一个function，有三个参数req， res和next middleware function，这三个参数就是app的request-response cycle的组成
```js
app.post('/:id',(req,res)=>{
	const{ name } = req.body;
	const{ title } = req.query;
	const{ id } = req.params;
	
	res.json({name.title,id});
});
```
- route handler还有一个名字叫middleware function；一些处理针对某个路径某个method的middleware function叫做route handler.

```js
app.post('/:id',(req,res, next)=>{
	const{ name } = req.body;
	const{ title } = req.query;
	const{ id } = req.params;
	
	res.json({name.title,id});
});
```
  - 这里也可以写next参数，但是js允许将不使用的最后一位参数省去；如果不使用的参数是中间的参数是不可以省去不写的
  - express是有一系列middleware function组成的，意味着请求在处理的时候会调用一系列middleware function。
  - next middleware function指明的是下一个执行的middleware function
- middleware function执行下列操作：
	- 执行代码
	- 对 request和response body做出改变 (读+写都可）
	- 结束 request-response cycle
	- call stack中的下一个middleware function
	- 注意：如果现有的middleware function没有结束request-response循环，它必须call next（）把控制权交给下一个middleware function. Otherwise，这个请求就会left hanging（请求搁置），永远不会返回 

- ![route](./img/图40.jpg)
  ![cycle](./img/图41.jpg)
  - 浏览器发出请求，server进行路径匹配，匹配成功触发callback，否则404；
	- ![path](./img/middlewarep-pathpic.jpg)
  
  	  middleware一系列是怎么挨个触发的（重点看菱形节点-路径分叉口的位置）
  	  - 0个-无限个middleware function可以注册到节点上, 多个节点也可注册相同的middleware function
      - 在请求进来后，根据请求的路径，会触发一系列的middleware function，middleware chain的排列顺序是根据请求的路径来看的
      - ![function](./img/图42.jpg)
      - middleware function的触发顺序是由路径决定的，最终到达route handler
  - 匹配method
	- 注册middleware时可以选择根据path进行注册，也可以选择根据method进行注册
	- `app.get/post`和`app.use`的区别
	  - app.get/post 只能匹配与method类型完全相同，路径完全相同的请求
	  - app.use 所有以该路径开头的请求，都能匹配成功
		- 如app.use(express.json())就相当 app.use('*',express.json()),等于所有路径,即application level middleware 
		- app.use('/users', middleware1) --- 所有start with‘/users’(即/users*) 都会触发middleware1
		  app.get('/users', middleware1) --- 一定要完全匹配‘/users’才会触发

    - 注册Middleware：
	```js
	//注册application level的Middleware，匹配所有路径
	app.use(express.json());
	//对start with’/‘路径注册middleware
	app.use('/',m1);
	//对路径‘/’，method get注册middleware
	app.get('/',m1)
	