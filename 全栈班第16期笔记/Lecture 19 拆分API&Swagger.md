# Lecture 19 拆分API&Swagger

## 主要知识点
- [Lecture 19 拆分API&Swaager](#lecture-19-拆分apiswagger)


## 课堂笔记 

#### 19.1 拆分api 

- Nodejs常见项目拆分结构
```
-- package.json
-- package-lock.json
-- src
  |-- index.js 入口文件(server.js.app.js)
  |-- routes
    |-- tasks.js(taskRouter)(task.route.js)
    |-- users.js(userRouter)
    |-- index.js(把上面所有的router导入进来，再做一个统一的导出
  |-- controllers (逻辑处理部分）
    |-- tasks.js(taskController)(task.controller.js)
    |-- users.js
  |--models
    |--tasks.js(Task.js) 数据库中Task这个数据的格式设计 -ORM （object relational mapping），跟数据库交互
  |--middleware
    |--error-middleware
      |-- xxxErrorHandler.js
    |-- authGuard
    |-- cors
  |-- utils (Helper function, shared function, db)
  |-- db
  |-- config 项目配置（环境变量的处理）
```
- 上述拆分方向有时会把routes和controller合并，或者增加services文件夹，来应对更加复杂的逻辑： 
- 第二种拆分方向
```
src
- users
  -- user.controller.js
  -- user.model.js
- tasks
```
- 拆分好的文件库：https://github.com/LazeBear/jr-todos-api-walkthrough

#### 19.2 Other Useful Packages
- cors
  - 提供 Connect/Express 中间件, 解决跨域问题
```
const cors = require('cors')
app.use(cors())
```
- morgan
  - 输出请求日志
```
const morgan = require('morgan');
app.use(morgan('dev'));
```
- dotenv
  - 配置环境变量
```
//index.js 中
require('dotenv').config();
PORT = process.env.PORT || 3000;
//.env 文件中
PORT=4000
```

- helmet
  - Helmet 通过设置各种 HTTP Header来帮助保护Express
  
winston
