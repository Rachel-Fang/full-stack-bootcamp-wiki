# Lecture 10 Express.js

## 主要知识点

- [Lecture 10 Express.js](#lecture-10-expressjs)
	- [主要知识点](#主要知识点)
	- [课堂笔记](#课堂笔记)
		- [10.1 Microservices](#101-microservices)
			- [10.1 NPM](#101-npm)
			- [10.2 Semantic version](#102-semantic-version)
			- [10.3 Nodemon](#103-nodemon)
			- [10.4 express](#104-express)
		- [作业](#作业)


## 课堂笔记

***sequence diagram：时序图*** 
![SequenceDiagram](/img/SequenceDiagram.png)

![restService](/img/restService.png)


### 10.1 Microservices
![microServices](/img/microServices.png)
-  一种服务端的设计架构
- monolith server
- 原本的每个服务会单独拆分出来(根据用户访问量等),每个service都有它自己独立的数据库和server,所有的请求由api gateway转发给不同的server
- service互相调用数据的话必须通过该对应的servcer的api接口去调用
- 嵌套结构，/library/{libId}/book
- 优点：其中任何一个service挂掉，不会影响整体的工作，如Product坏了，用户的注册不会受到任何的影响

- Q：什么是Lambda？
- A：相当于server里的一个具体的逻辑，讲其抽出来放到server上

- Q：GraphQL为什么没有取代Restful API？
- A：GraphQL学习成本更高，且有很多不支持的功能，如文件上传

#### 10.1 NPM
- (Node package manager) 用来安装node相关的包
- 代码可以上传到仓库，告诉npm我想要发布到npm上，提交给npm后就可以通过npm进行下载
- npm express：https://www.npmjs.com/package/express
- 注意：在进行typescript开发时，要选择支持typescript的package
- 可以通过Readme里的示例代码来上手package, Readme越详细，代表越在乎开发者体验
- 选package的注意点：
	- 看star，issue和pull request来确定是否使用，issues是否有被解决，被开发者回复，看pull request最后一次merge是什么时候
	- 用示例代码试一下是否符合自己要求
- npm命令行操作:
	- 注意使用命令行之前，切换到相对应的文件夹下操作 
	- 使用 `npm init -y`  指跳过所有问题创建package.json文件 -y指只要碰到选择题，都选择yes
	- `npm install` = `npm i`用来安装package
	- package-lock.json会记录安装packages时的版本号，并lock住，主要用处就是确定pachages的版本
	- 为什么 package.json / package-lock.json 这么重要？
		- 我们会运行npm来安装项目所需的依赖项，但我们怎么看一个项目有多少依赖项呢？就是通过看package.json，安装时，npm会优先按照package-lock.json里的对应版本来安装
		- 如果误删，需要重新运行npm install重新生成，或者通过git revert的方式回到原来版本
		- 为什么需要固定版本？
			- 新的版本意味着新的bug，不把版本lock住的话，不能百分之百保证没有新的问题 
	- gitignore文件会放在相应的项目文件夹的根目录下面
	- create-react-app 脚手架工具会帮你把配置全部设置好，后期常用 
	- 删除package `npm uninstall`
	**不能手动修改dependencies，想要修改的话，使用`npm i`重新安装**
	- dependencies 和devDependencies的区别：
		- dev dependency，只有开发环境使用的package 
		- dependencies，缺少了项目就无法运行的依赖项
		- 运行 `npm install`dependencies和devDependencies都会装
		- `npm i -D`只安装devDependencies
	- `npm i -g` 全局安装，装到当前机器的操作系统上常用的，在命令行中可以直接使用，现在不太使用
	- 全局安装不写进package.json，有可能导致scripts找不到package导致报错 
	- 现在不支持全局安装了，使用npx代替，随着npm一起安装，将原本需要全局安装的package用npx运行，npx可以帮助获取最新的版本，会做缓存（不放在package.json里），但不长期保留，帮助释放了硬盘空间而且不需要手动更新
	- pachage.json的`”scripts“`包含一些alias快捷方式，可以通过`npm run {scripts}`使用命令
		- `npm run {scripts}`可以简写为`npm {script}`

#### 10.2 Semantic version
`”dependencies“：{
	”express“：”^4.16.4"
	//       major.minor.patch`
- major:大版本更新，break change
- minor：增加新功能，feature change
- patch：小版本更新，补丁操作，修复小问题 bug fix
- 在没有package-lock.json的时候，大家借用yarn这个package manager，并且保留了相当大的市场至今

#### 10.3 Nodemon
- `npm i -D nodemon` 自动监听代码改变，自动重启服务器
- 使用 `nodemon index.js`来使用
- `--inspect` 在需要测试的代码地方增加断点，会在断点位置停止，并可以查看断点是各个变量的内容

#### 10.4 express
- Fast, unopinonated,minimalist web framework for Node.js
- 调用express创建一个app
```js
const express = require("express")；

const app = express()；

app.get（‘/’，（req，res）=>{
	res.send('hello world');
});
app.listen(3000);
```

- `const express = require("express")` 导入
- `const app = express()` 应用
	- method为HTTP method例如`GET POST`等
- `app.listen()` 监听一个端口
	- 常用端口: 3000 4200 8080 9000
- `app.method(path, route handler => callback)` 事件绑定
	- `app.post('/:id',(req, res) => callback)` 
- 如何从request里取数据？
	1. `req.body` -> POST, PUT, PATCH 创建修改数据时使用，不可见，必须使用express.json() middleware)
```js
app.use（express.json());

app.post（'/',(req,res)=> {
	const { name } = req.body;
	
	res.send({name});
});
```
这时如果使用postman给网址url发一个post请求，body为`{"name":"mason"}`, server会返回`{"name":"mason"}`


   2. `req.params` -> GET, POST, PUT, PATCH, DELETE 只从url里面取，取问号后的变量 需要定义才能取到值 常用于id
      - `req.query` -> GET 筛选
```js
app.post('/:id',(req,res)=>{
	const{ name } = req.body;
	const{ title } = req.query;
	const{ id } = req.params;
	
	res.send({name.title,id});
});
```
网址url为 `localhost:3000/?title=mr` 继续使用上面的post请求，会返回
```js
{
	"name":"mason"，
	"title":"mr"
}
```
 3. `route param` 去在url中，问号前的数据
```js
app.post('/:id',(req,res)=>{
	const{ name } = req.body;
	const{ title } = req.query;
	const{ id } = req.params;
	
	res.send({name.title,id});
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
- 只传送json格式的数据：
`res.json（）`
- 只返回 status code：
`res.sendStatus(204);`
- 只设置status code（不返回），并且返回json： 
`res.status(201).json({data})`
- 状态码加数据response 如果不加`status()`默认返回200

### 作业
- https://jr-todos.herokuapp.com/api-docs/
- 按照document创建RESTful API
- 可以使用`const data = []`的方式创建一个临时数据库，服务器重启时会刷新