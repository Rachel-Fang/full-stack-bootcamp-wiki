## 目录





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
![图片1](/img/)
>说明：
- 左边用户，中间浏览器，右边static assets和backend server
- 我们的用户是如何跟static assets和backend server进行交互的呢？
    - 在用户浏览页面的时候，首先浏览器会请求static assets。（这里所说的场景是前后端分离开发、前后端分离部署。）
    - 前端开发好后，会打包好一个个静态文件，这些静态文件就是HTML、CSS、JS、images、icons等assets。静态打包好，再部署到一个静态服务器上。
    - 我们在请求一个页面的时候，浏览器首先回去请求这些静态物件，然后前端进行一个相应的渲染。
    - 其中JS的运行的时候，可能涉及到某一个数据页面上没有，需要请求服务器，从服务器取回相应的数据。（图片变成如下：）
    ![图片2](/img/)
    - 假如从静态服务器里面取出来的数据，长成中间图片的样子。
    - 搜索框所涉及到的功能，它会搜索最新的新闻，但是这些新闻不属于静态文件，它是动态更新的。所以这些数据是一直更新的状态。
    - 如果我们想搜索，这个请求会进入到backend server，server进行一些相应的逻辑处理之后，会返回到一些数据显示在页面上。
    - 在请求的过程当中，会对前端页面进行处理，也就是在请求过程当中，会有一个loading的effect：（即请求发出，显示loading）
    ![图片3](/img/)
    - 等到数据回来，可以显示出来了，我们把loading去掉，显示实际的新闻。
    - 以上是完整的请求流程。
- 我们想了解Nodejs，首先要明白backend server具体发生了什么。
    ![图片4](/img/)
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
    - 比如漏了一些
- Often used for building back-end services 
- Fast and scalable 


