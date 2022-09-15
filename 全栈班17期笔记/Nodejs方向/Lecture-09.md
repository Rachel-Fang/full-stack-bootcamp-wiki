
- [Fundamental of Node.js](#fundamental-of-nodejs)
- [RESTful API](#restful-api)
  - [9.1 Node.js](#91-nodejs)
  - [9.1.1 About Node.js](#911-about-nodejs)
  - [9.1.2 Node.js Architecture](#912-nodejs-architecture)
  - [9.1.3 Node.js Version](#913-nodejs-version)
  - [9.1.4 Coding](#914-coding)
  - [9.2 Protocol协议](#92-protocol协议)
  - [9.3 URL的组成](#93-url的组成)
  - [9.4 HTTP Methods](#94-http-methods)
  - [9.5  HTTP Headers](#95--http-headers)
  - [9.6 Response (status) code](#96-response-status-code)
  - [9.7 JSON](#97-json)
  - [9.8 SOAP](#98-soap)
  - [9.9 API](#99-api)
  - [9.10 REST (Representational state transfer)](#910-rest-representational-state-transfer)
  - [9.11 Restful API 设计规范](#911-restful-api-设计规范)
  - [9.12 Microservices](#912-microservices)
  - [9.13 Practice](#913-practice)


***PPT内容***

## Fundamental of Node.js
- About the course
- Front end vs Back end vs Full stack
- About Node.js
- Node.js Architecture
- Event Loop in browser
- Node versions
- Let’s coding

## RESTful API
- Protocol
- Url
- HTTP Headers
- Common used HTTP Methods
- HTTP Headers
- Some Common used HTTP Headers
- Authorization Header
- Common used Response code
- JSON
- Exchanging data
- SOAP
- API
- REST Service
- REST API
- Microservices
- API Authentication & Authorization
- Practice
- QUIZ
- Practice CRUD
- Loading JSON usingAJAX

>Q&A:
1. 为什么用var声明的变量，会把它的变量直接写到Windows里面？而const不行？
- A：var是functional scope。
- 在一个文件里，如果没有任何的function，它其实等同于global scope。
- var的特性在于，你不在function里面，你就相当于global。var就会把属性加到Windows上。
- 我们的function是可以通过window.functionName的方式调用的，这个和var是function scope有关。
- 在没有现在这些框架之前，JS文件是一个一个导入到HTML页面上的，这样就会导致不同文件之间的变量会被替换掉，或者说被覆盖掉。
- 现在不会有这些问题了，因为现在我们用框架，框架帮我们做模块化处理。
- 这也是为什么我们用let和const替换var的原因。

### 9.1 Node.js

>说明：
- Nodejs是用来做后端开发。
- 做实际的后端开发之前，我们首先要了解，后端到底是怎么工作的。
- 或者说我们到最终开发出来的server，到底是怎么回事？

>看图：
![图片1](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/%E5%9B%BE%E7%89%871.png)
>说明：
- 左边用户，中间浏览器，右边static assets和backend server
- 我们的用户是如何跟static assets和backend server进行交互的呢？
    - 在用户浏览页面的时候，首先浏览器会请求static assets。（这里所说的场景是前后端分离开发、前后端分离部署。）
    - 前端开发好后，会打包好一个个静态文件，这些静态文件就是HTML、CSS、JS、images、icons等assets。静态打包好，再部署到一个静态服务器上。
    - 我们在请求一个页面的时候，浏览器首先回去请求这些静态物件，然后前端进行一个相应的渲染。
    - 其中JS的运行的时候，可能涉及到某一个数据页面上没有，需要请求服务器，从服务器取回相应的数据。（图片变成如下：）
    ![图片2](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/%E5%9B%BE%E7%89%872.png)
    - 假如从静态服务器里面取出来的数据，长成中间图片的样子。
    - 搜索框所涉及到的功能，它会搜索最新的新闻，但是这些新闻不属于静态文件，它是动态更新的。所以这些数据是一直更新的状态。
    - 如果我们想搜索，这个请求会进入到backend server，server进行一些相应的逻辑处理之后，会返回到一些数据显示在页面上。
    - 在请求的过程当中，会对前端页面进行处理，也就是在请求过程当中，会有一个loading的effect：（即请求发出，显示loading）
    ![图片3](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/%E5%9B%BE%E7%89%873.png)
    - 等到数据回来，可以显示出来了，我们把loading去掉，显示实际的新闻。
    - 以上是完整的请求流程。
- 我们想了解Nodejs，首先要明白backend server具体发生了什么。
    ![图片4](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/%E5%9B%BE%E7%89%874.png)
    - 请求从浏览器发出，最终达到server。
    - JS代码是怎么能够监听从客户端（浏览器）发过来的请求？把请求接收到之后，又进行相应的处理，给它返回回去，是怎么做到的？
    - 想要能够实现通讯，也就是浏览器能够发请求到server上，server需要打开一个端口，这个端口涉及到了硬件，我们需要在机器上开一个端口，然后实现端口对端口的通讯。
    - 浏览器也是这样，他要发出一个请求，他也是需要开一个端口，在这个端口上和另外一台机器的端口进行通讯。
    - 这个操作存在于物理层，在硬件层上。JS是不可能访问到硬件层的，JS本身没法操控硬件。那它是如何实现用JS的方式开启一个端口的呢？
    - 这就涉及到JS和硬件之间有一些C/C++的library。C/C++是专门操控硬件的。比如我们用C/C++把一个端口打开，然后在每个端口进行监听。
    - 我们所会的只是JS代码，而我们要用的、实际打开端口的这一个代码是在C++上面，怎么样让JS代码触发C++的代码，最终把端口打开呢？这个就是Nodejs在干的事情。
    - Nodejs 70%的代码，都是C/C++的library，这些library提供了一系列JS本身不支持的功能。
    - 其中一个library就是http：它能做的事情就是，打开一个端口，并且监听这个端口。
    - 而Nodejs所干的另一件事情，就是它会有一个mapping：mapping就是把JS代码转换成C++的代码，反之亦然。
    - 有了这个mapping之后，我们可以在编辑器里，打出JS代码，用JS代码触发C++的逻辑，最终实现我们想要做的打开这个端口。***这就是Nodejs提供的功能。***

- 我们可以用这个代码片段来创建一个server：
```js
{
const http = require('http')

const server = http.createServer
((req, res) => {
    // const news = [...];
    res.write(news);
    res.end();
    return;
})

server.listen(3000);
}
```
- 这个server就可以监听3000端口，任何请求发送到这个端口，这个事件就会被触发，函数就会被执行。  
- 他是怎么被执行的呢？
    - 在调用http这个模块的时候，在Nodejs里我们会有一系列的模块，这些模块可能是nodejs自带的，也有可能是第三方开发的，这里只涉及到自带的模块。
    - http.createServer这样一个模块，它所做的事情就是调用C/C++里面的http这个模块，有一个叫做createServer，createServer接收一个callback function，相当于一个function reference。
    - 当3000端口收到一个事件请求的时候，它其实就直接调用了传入的这个function reference，function reference就是这段代码。每一次有请求到3000端口，就会触发callback function，这个callback function就会执行。
    - 这个function接收两个参数，分别是request=>req（和请求相关的所有信息，放在request这个对象里）, response=>res（如果我们想要进行返回，需要调用response它里面的一些method，比如write&end）。把想要返回的信息写在response里面，然后进行返回。
- 以上就是一个真实的案例看一下nodejs到底在做什么。 


### 9.1.1 About Node.js
- A JavaScript runtime environment build on Chrome’s V8 engine
- Asynchronous
    - 异步，看上去干多件事情，其实只是干了一件事情；
- event driven
    - 每一个请求进来，都是所谓的event；
    - 当event被触发之后，我们会用相应的function，针对这个event进行处理。
- Non-blocking I/O（input and output）
    - I/O就是Asynchronous的request。
    - 比如从我们的本地磁盘漏了一些files，这些就是I/O（input and output）
- Often used for building back-end services 
    - 我们一般用nodejs来搭建我们后端的server，但它并不是绝对的，我们也可以用nodejs来做很多其他的事情。
    - 比如我们可以用nodejs写一个脚本，它不是server，它只是一个，只执行一次的脚本。它会从上到下执行代码。等所有逻辑执行完，没有任何事件了，它就会退出。这是一个**脚本**。
    - 同时也可以用它来开发桌面单的**应用程序**。比如VScode，它也是用Nodejs开发的。只不过这种桌面端的应用程序，会用到一个**framework：Electron**。（有兴趣可以自己了解一下）
- Fast and scalable 
    - Fast体现在它的开发上面。前端开发一定是JS。当前后端用一种语言的时候，开发效率很快。
        - 响应也是要分场景来看。nodejs弊端是一个单线进程，跟JS一样，一次只能执行一段了逻辑。如果在执行中，如果遇到了非常耗费资源的计算，整个线程（thread）是被block住的。这样对于server是非常不好的事情。所以对于nodejs来说，我们会尽量避免把一些heavy computing的操作写在主线程里，或者不放nodejs里面。我们可以通过调用其他程序的方式，一些heavy computing放到其他语言里面来做，通过调用进行执行。简单来说，我们不像在node里，或者JS里处理heavy computing的操作。
    - scalable （容不容易扩展）
        - 1w个用户，1个server处理；10w用户，需要增加9个server来处理。这就涉及到server是否容易scale。
        - 用nodejs来开发，整个server都处于stateless（API中会讲到）的状态。即server本身没有状态，不记录任何状态，它容易scale up（增加新server，处理新请求）。


### 9.1.2 Node.js Architecture

***主要分为三层***
- Application（APP）
    - 我们所有开发几乎都是在这层进行的。涉及到package的调用，这时会用到API和mapping。
- API
- C/C++ Library
    - 底层逻辑。

>说明：
- 比较资深的nodejs开发，可以写C++的代码，加一层bindings，用JS的方式调用C/C++所使用的逻辑。所以可以进行一些插件的开发或者C/C++ libraries的开发。
- Nodejs里，70%的代码是C/C++代码，30%是JS代码。新手可以看看它的原代码，在Github上有。


***Event Loop in Browser***
![EventLoopInBrowser](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/EventLoopInBrowser.png)


>***Q&A***
1. *render queue*
    - Render Queue就是控制什么时候执行JS代码，什么时候UI可以渲染。
2. *callback queue*
    - callback：在创建eventListener时，会传入一个callback function，这个callback function不会立即执行，只有当事件触发的时候，才会执行。但是callback function不会事件触发的时候立马执行，因为当前stack可能在执行其他逻辑，所以我们需要有一个排队的机制，确保只有stack为空，可以执行新的代码了，才会把callback function放到里面执行。
    - 这样的机制需要我们有一个队列，来给这些等待被执行的任务进行排序。
    - 如果有10个callback需要被执行，谁先谁后？需要callback queue机制，谁先好，谁先执行。
3. *render queue的优先级高于callback queue*
    - 是的。
4. microtasks queue和macrotasks queue
    - microtasks queue(promise queue)
    - macrotasks queue(setTimeout, setInterval, callback queue)


### 9.1.3 Node.js Version

- **目前最新版到了18**
![NodejsVersion](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/NodejsVersion.png)
    - 当前维护版本是14（Maintenance）：提供被动更新
    - 当前活跃版本是16（active）：主动进行修复
    - 最新版本是18（current）：当前正在开发的版本

- 单数是Nodejs的一个测试版本，它不是稳定版本。如果想要研究nodejs最新的一些功能，可以用它的测试版。
- 企业项目，一定用稳定版，双数版本。
- 选择版本的时候，不会选择current版本，通常是从active选。确保已经过更新，已经稳定的版本。当前来说用16.
- 企业项目需要更新nodejs版本的时候，要先研究nodejs的版本代码是否会对企业代码产生影响，然后再更新。
- nvm：node version management
- 快速切换node版本：nvm use 版本号


### 9.1.4 Coding

```js
index.js

const module = { exports : {} }; 

( function (module) {
    const msg = 'secret message';

    function getMsg() {
        return msg;
    }

    module.exports = { getMsg };
})(module);
```
>**说明：**
- module是个对象，对象里有个属性叫exports；
- 然后声明一个变量，同时创建了一个函数；
- 使用传入function的一个参数module；
- 把module的exports属性，赋值为一个object；
- 在object里面，把getMsg放在引号里。

- 可以理解为刚开始的时候，module里什么也没有；
- 执行完括号内之后，module里面有个exports属性；
- exports属性，就会有一个getMsg属性，它是一个function；
- 通过执行这个function，可以得到'secret message'.



```js
index.js

const obj = { exports : {} }; 

( function (module) {
    let msg = 'secret message';

    // msg = '123';

    function getMsg() {
        return msg;
    }
    module.exports = {getMsg}
})(obj);

obj.exports.getMsg();
```
>**说明：**
- 用括号的目的是把一些变量隐藏起来，变成一个私有变量的概念。
- 为了外部能访问到msg，我们传入一个object叫module。
- 让module的reference不变，改变exports这个属性，让exports得到一个新的reference。
- 达到目的：我们想要把function导出，同时隐藏msg这个变量。




```js
index.js

const msg = 'secret message';

function getMsg() {
    return msg;
}
    
module.exports = {getMsg}

```
>**说明：**
- 括号内的处理，是nodejs帮我们做的。
- nodejs就是把每一个JS文件，通过一个括号，把它打包起来。
- module会传exports、_dirname、_filename、require，这些参数都会通过括号的方式传给我们。
- 最常见的是module和require。 
- 建议大家用module.exports方式进行导出。
- require是当我们想要导入一些模块/module的时候，想在其他地方使用它：
```js
app.js

const msg = require('./index');
// msg.getMsg();
const msg = getMsg();
console.log(msg);
```

**几种常见的module**
- commonJS：进行模块化处理
- ES module：前端进行模块化处理
- AMD：前端行模块化处理
- UMD




### 9.2 Protocol协议
 
- protocol协议相当于一个固定的格式，双方之间交流沟通的前提：
	- 如写信的时候要写收信人的姓名地址电话，才知道谁来收这封信 

- TCP （Transmission Control Protocol）和 IP（Internet Protocol）最大的用处是：
	- IP 让我们知道请求的目标地在哪里，TCP帮助我们把请求安全有序地传递到目标位置
	- TCP 建立链接需要三次挥手，断开连接需要四次挥手：
		- [TCP 3-Way Handshake Process](https://www.geeksforgeeks.org/tcp-3-way-handshake-process/)
		- [Why TCP Connect Termination Need 4-Way-Handshake?](https://www.geeksforgeeks.org/why-tcp-connect-termination-need-4-way-handshake/?ref=rp) 
		- A：连接终止的时候需要四次挥手，因为TCP是一个全双工连接，一端发送完了数据不代表另一端没有数据要发送了，所以需要双方各自关闭一次，而连接的时候为什么只需要三次握手呢，是因为第二次握手的过程是同时包含了SYN和ACK的，因为连接的时候没有必要像断开那样分两个方向断开连接，因为连接都还没建立，双方肯定没有数据在发送

	- 了解更底层的知识可以了解什么是[OSI mode](https://www.forcepoint.com/cyber-edu/osi-model)

- HTTP（HyperText Transmission Protocol）是我们最熟悉的协议：
	- 打开Chrome浏览器的地址栏，前面会有https的前缀，这个前缀就是该网站的协议，https相比http，加上了一层安全层，给数据进行加密
	- 最常用的http协议是 http1.1 和 http2，我们在开发阶段会使用http1.1的协议，https需要我们自己加一个验证来保证数据是保密的，且https是基于http2协议上的，***p3会需要我们给server买域名，到那时我们可以考虑要不要使用http2协议***

### 9.3 URL的组成

![URL](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/URL.png)

- URL全称：Uniform Resource Identifier 统一资源标识符
	- Protocol协议部分：包括http、MongoDB协议，省略不写一般是https协议 
	- auth验证部分：用户尝试访问加密资源时，传入用户名和密码证明是权限用户，会用@符号和host部分隔开，现在不常用，
	- host域名部分：hostname会通过DNS域名解析转换成IP地址，写成英文是为了容易记忆，后面有时会加上port端口号，指明了会和该地址的那一个端口进行通信，又是端口可以省略不写，因为协议会有默认端口，如https为53，http为80
	- path路径部分：通过路径分析到底是哪一个资源，search部分表示对这个资源有哪一些搜索的条件或要求，search后会有一个问号 ‘’？“代表问号后面是搜索参数，query代表了搜索框里的东西，q是query的缩写，q=string
	- hash锚点部分：只在浏览器中有用，目的是让浏览器在渲染时直接跳转到当前锚点所在的位置

- Q:  现在的验证用户不用auth的方法了，那他们现在用的是什么方法呢？
- A：使用token，用户登陆时会发一个请求携带用户名和密码，这个请求发到后端会返回一个token，任何携带该token的用户都等于该用户本人，token可以进行加密

### 9.4 HTTP Methods
- GET 一般发送请求时，取得数据
- POST 数据添加
- PUT 更新数据，数据替换
- DELETE 删除数据
- PATCH 更新部分数据 与PUT类似 按公司规定使用

### 9.5  HTTP Headers
- 可以使用curl命令查看HTTP request， linux和MacOS可以直接使用，Windows需要安装
- Request Headers部分：
	- 第一行格式：GET / HTTP/2     METHOD PATH PROTOCOL
	- Host：www.google.com 请求的网站地址
	- User-Agent：curl/7.64.1 client通过哪个方式和浏览器访问
	- Accept: */* 接收什么样格式的数据，有时只写html、css、javascript，告诉server自己接收什么样的信息
	- 总结：Header部分是为了让client和server相互之前通信时有一个标准的格式

- [扩展阅读](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/Messages)
- 常用的HTTP Headers
	- Content-Type: text/html 数据类型
	- Allow: GET, PUT, POST 允许的请求类型
	- Referer: 告诉信息收集平台，用户从哪里来的，例如Google，程序会收集headers来分析用户来源比
	- User-Agent: 用户通过哪个浏览器访问
	- Access-Control-Allow-Origin： **开发时会碰到** 以下错误 如果client发的请求返回的数据，没有‘access-control-allow-origin’ header会被浏览器拦截，属于跨域访问，使用CORS anywhere可以设定允许哪些跨域访问
	![Acces-Control-Allow-Origin](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/accessControlAllowOrigin.png) 
- Authorization Header: `<Type> <credentials>`
	- Type部分：
  		- `Basic` username and password
  		- `Bearer` Oauth 2.0 protected resources through bearer token  在我们之后的开发中常用
	- 其他
  	- header的信息是可以伪造的,所以不能百分百相信.
  	- x-custom : 自定义的header, 明确告诉server这个是自定的/server要求自定义header以用作其他用途 


***这节课一定要记住的内容：***
- URL
- HTTP Methods
- Authorization Header


### 9.6 Response (status) code
- 200 OK 表示请求发送成功
- 201 Created 表示post请求的添加操作成功了
- 204 No content 表示请求发送成功但是不返回任何内容，delete request表示删除成功会发这个
- 209 Conflicts 用户名重复
- 304 Not Modified 并不很常用
- 400 Bad Request 请求有错误 客户端有问题
- 401 Unauthorized 用户没有权限访问
- 404 Not Found 找不到数据或资源
- 500 Internal Server Error 服务端内部错误，尽量不要出现在生产环境


### 9.7 JSON
- XML和JSON的区别：JSON语法更简单，使用key value pair，可读性更高，XML有open tag closing tag，在JSON之前使用XML格式，现在已经渐渐被JSON取代
- 序列化与反序列化：javascript 的一个object转化成一个字符串（json），字符串（json）转换成 javascript object
- Json 不支持 undefined 的 value, 所以如果当数据里有undefine的情况, 它的key会消失(或者说就不存在了)
- 以下做法会经常被使用在深拷贝上：
`console.log(JSON.stringfy(course));`
`console.log(JSON.parse(JSON.stringify(course)));`


### 9.8 SOAP
- Simple Object Access Protocol , 这个protocol比较注重权限和安全性,在设计上会比较复杂
- 一个安全性很高的协议，银行，政府会使用


### 9.9 API
- Application programming interface 应用程序编程接口
- 可被外部访问的接口被称为public API，或web service网络服务
- 它对一些复杂的逻辑进行了封装和解释,记录函数/组件的使用方法(可以的话尽量做到”代码即注释“)



### 9.10 REST (Representational state transfer)
- 本身概念很难理解，作为开发者只需要理解如何使用
- 可以通过看URL大概知道该请求是做什么的，如：GET /books
- Rest可以帮助定位我们想要的资源，并且进行相应的操作
- Stateless 无状态：
	- 有两个请求A和B，A和B发送的先后顺序不同，得到的结果是一模一样的，现在的server端开发基本都是无状态
- Stateful 有状态：
	- A和B发送顺序错误会导致访问不到  



### 9.11 Restful API 设计规范
1. versioning（版本）出现在url后面，版本号后面跟实际的资源(加上版本控制确保改动不波动到所有用户正在运营的项目P)
- 例如
	- example.com/api/v1
	- example.com/v1
	- example.com/v2/books

2. url 里，尽量使用名词noun，不要使用动词，资源尽量使用复数形式
- 例如：
	- GET /v1/books
	- GET /v1/getBooks x
  
3. 保证GET 不会对资源进行修改（污染）
- 例如：
	- GET /v1/books（只读数据，而不作更新或修改）

4. url 推荐使用嵌套结构
- 例如：
	- GET /posts/:postId/comments
	- GET /posts/{postId}/comments 
	- GET /posts/post123/comments 
  
5. 对返回的数据进行分页（注意返回的大小）
- 如果有1000个数据，取回来也不可能全部显示在页面上，用户也不大可能把数据全部看完，为了避免浪费和更长的传输时间， 因此需要对返回的数据进行分页
	- 例如：
		- GET /v1/books ->该请求永远只返回10个数据
		- GET /v1/books?page=26pageSize=100 ->给该请求加query frame 每页100个数据 
  
6. 使用正确的status code来表示返回的结果

7. 尽量返回人性化的文本信息（错误信息）
- 例如：
	- {”error“：”invalid password“}
	- {”error“：1001} // 不友好的 error code




### 9.12 Microservices
![monolith](https://github.com/australiaitgroup/full-stack-bootcamp-wiki/blob/main/%E5%85%A8%E6%A0%88%E7%8F%AD17%E6%9C%9F%E7%AC%94%E8%AE%B0/Nodejs%E6%96%B9%E5%90%91/img/Microservices.jpg)
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


### 9.13 Practice  
- Use postman to practice api calls
- https://newsapi.org/
- 开发时先用注释表示流程，有助于面试思路

