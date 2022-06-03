# Lecture 21 Mongoose&Promise

## 主要知识点
- [Lecture 12 Mongoose&Promise](#Lecture-12-mongoosepromise)


## 课堂笔记

#### 21.1 Promise
- call back function 回調函數：當一個函數接受另外一個函數作爲參數時，把該參數稱爲回調函數，
```
//模拟从url中获取数据连接并用cb函数获取数据
function fetchData(url,cb){
    setTimeout(()=> {
        cb(url);
    
    },1000)
}
```
- 实际使用中，在从第一个请求获取数据后，马上要发第二个请求，从而保证请求顺序正确，进行函数的嵌套，由于逻辑的复杂，代码最终呈现效果会非常之乱，难以Debug，这样嵌套太多层的代码，被称为回调地狱
```
//每多嵌套一层，代码就会缩进一次，如果嵌套层次太多，会超过屏幕宽度限制
fetchData('example.com', (data)=> {
//
//实际使用中这里会嵌套许多的逻辑和if-else
//
//if（）{}
    fetchData('example.com/2',(data2) => {
        fetchData('example.com/3',(data3) => {
            fetchData('example.com/3',(data4) => {})
        })
    });
})

```
- Promise 
  - 用于表示一个异步操作的最终完成（或失败）及其结果值 
  - 一个 Promise 必然处于以下几种状态之一：
    - 待定（pending）：初始状态，既没有被兑现，也没有被拒绝。
    - 已兑现（fulfilled）：意味着操作成功完成。
    - 已拒绝（rejected）：意味着操作失败。
 ```
 const promise = new Promise((res,rej) => {
    res([]);
})
```
  - 待定状态的 Promise 对象要么会通过一个值被兑现，要么会通过一个原因（错误）被拒绝。当这些情况之一发生时，我们用 promise 的 then 方法排列起来的相关处理程序就会被调用。
```
//promise chain
promise.then((data) => {
    //data = []

    return {};
    // return new Promise() // async call
}).then().catch((err) => {//.catch()用于抓取或监听错误,返回一个pending状态的promise
    //err = {}
    return {}; //promise
}).then().catch()
```
  - Promise 的链式调用
    - 我们可以用 Promise.prototype.then()、Promise.prototype.catch() 和 Promise.prototype.finally() 这些方法将进一步的操作与一个变为已敲定状态的 promise 关联起来。
- 把上面嵌套多层的回调地狱转换成promise
#### 21.1.1 对比Promise和callback函数
- 将下列callback函数执行的功能用promise重写：
```
function fetchData(url,cb){
    setTimeout(()=> {
        console.log('cb: '+ url)
        cb(url);
    
    },1000)
}

fetchData('example.com/1', (data)=> {
    fetchData('example.com/2',(data2) => {
        fetchData('example.com/3',(data3) => {
            fetchData('example.com/4',(data4) => {})
        })
    });
})

//change above function to 
function fetchDataPromise(url) {
    return new Promise((res,rej) => {
        // setTimeout(() => {
            console.log('promise: ' + url)
            res(url);
            //if(){
                //rej()
            //}
        // },1000);
    });
}

const promise = fetchDataPromise('example.com/1');
promise
    .then((data1) => {
    return fetchDataPromise('example.com/2');
}).then((data2) => {
    return fetchDataPromise('example.com/3')
}).then((data3) => {
    return fetchDataPromise('example.com/4')
}).then((data4) => {
    return fetchDataPromise('example.com/5')
});

```
- console 输出如下：
```
promise: example.com/1
promise: example.com/2
promise: example.com/3
promise: example.com/4
promise: example.com/5
cb: example.com/1
cb: example.com/2
cb: example.com/3
cb: example.com/4
```
- promise永远在callback function之前执行，因为promise会被放在micro task queue里，在macro task queue之前执行
- macro task queue执行到一半，如果micro task queue里加入了新的task，那macro task queue里的task也会优先执行
- 执行顺序：synchronous call -> microtask -> macrotask
- example:
```
console.log(1);
// The first line executes immediately, it outputs `1`.
// Macrotask and microtask queues are empty, as of now.

setTimeout(() => console.log(2));
// `setTimeout` appends the callback to the macrotask queue.
// - macrotask queue content:
//   `console.log(2)`

Promise.resolve().then(() => console.log(3));
// The callback is appended to the microtask queue.
// - microtask queue content:
//   `console.log(3)`

Promise.resolve().then(() => setTimeout(() => console.log(4)));
// The callback with `setTimeout(...4)` is appended to microtasks
// - microtask queue content:
//   `console.log(3); setTimeout(...4)`

Promise.resolve().then(() => console.log(5));
// The callback is appended to the microtask queue
// - microtask queue content:
//   `console.log(3); setTimeout(...4); console.log(5)`

setTimeout(() => console.log(6));
// `setTimeout` appends the callback to macrotasks
// - macrotask queue content:
//   `console.log(2); console.log(6)`

console.log(7);
// Outputs 7 immediately.
```

#### 21.2 async await
- 语法糖，用来简化.then()和.catch()的情况，底层代码实现依旧是promise，但是代码可读性更高
- 用await 替换之前的.then()
- 一旦用到await,一定要在包裹这个await的function前加上async关键字
- 有await就一定有async
```
async function main(){
    //fetchDataPromise().then().then()
    //代码会在await处等待执行Promise的结果，是一个异步操作
    const result = await fetchDataPromise();
    const result2 = await fetchDataPromise();
    // ...
}
main();
```
- console 输出结果
```
promise: example.com/1
promise: undefined
promise: example.com/2
promise: undefined
promise: example.com/3
promise: example.com/4
promise: example.com/5
cb: example.com/1
cb: example.com/2
cb: example.com/3
cb: example.com/4
```
- 当Promise 被拒绝时，console会抛出大量的错误信息，为了梳理这些信息，在.then中需要加.catch（）把错误抓取住，在async await时，使用try catch为promise重新做处理
```
//change above function to 
function fetchDataPromise(url) {
    return new Promise((res,rej) => {
        // setTimeout(() => {
            console.log('promise: ' + url)
            rej(url);
            //if(){
                //rej()
            //}
        // },1000);
    });
}

async function main(){
    //fetchDataPromise().then().then()
    //代码会在await处等待执行Promise的结果，是一个异步操作
    try{
    	const result = await fetchDataPromise();
    	const result2 = await fetchDataPromise();
    } catch (e) {
      console.log(e);
    }
    // ...
}

main();
```

#### 21.3 finally
- 不接收任何参数，放在promise chain的最后面
```
const promise = fetchDataPromise('example.com/1');
promise
    .then((data1) => {
    return fetchDataPromise('example.com/2');
}).then((data2) => {
    return fetchDataPromise('example.com/3')
}).then((data3) => {
    return fetchDataPromise('example.com/4')
}).then((data4) => {
    return fetchDataPromise('example.com/5')
}).catch( err => {
	console.log(err);
}).finally(() => {
	isLoading = false;
})
```
#### Quiz
```js
setTimeout(() => console.log(1)); 
//macro task queue
Promise.resolve().then(()=> console.log(2));
//micro task queue
setTimeout(() => {
	console.log(3);
	Promise.resolve().then(() => console.log(3.1));
	//micro task queue {2, 3.1}
})
//macro task queue { console.log(1), setTimeout(3) }
setTimeout(() => console.log(4));
//macro task queue {console.log(1), setTimeout(3),setTimeout(4)}
Promise.resolve().then(() => {
	console.log(5);
	Promise.resolve().then(() => console.log(5.1));
	setTimeout(() => console.log(5.2));
});
//micro task queue {Promise(2),Promise(5)}
Promise.resolve().then(()=> console.log(6));
//micro task queue {Promise(2),Promise(5),Promise(6)}

//micro task queue {Promise(2),Promise(5),Promise(6)}
//macro task queue {console.log(1), setTimeout(3),setTimeout(4)}
//micro task queue executed first 
//micro{Promise(6),Promise(5.1)}
//macro{console.log(1), setTimeout(3),setTimeout(4),setTimeout(5.2)}
Output:2 5 6 5.1 1 3 3.1 4 5.2
```
#### 21.4 Mongoose
- 是MongoDB专用的ORM (object relational mapper)
- SQL 数据库使用Sequelize  https://sequelize.org/
- 基于Mongo Client

#### 21.4.1 Schema vs Models vs Documents

```
const schema = new mongoose.Schema({name:String});//数据的格式，schemaless数据易于迭代（如储存传感器数据），但是不容易管理
const Model = mongoose.model('Model',schema); //在mongoose里注册的一个模型，存到数据库中时，默认把Collection命名为model的名字复数小写，如models
const document = new Model({name;'document'})
```
- 如果mongoDB的数据里有age field ，但是mongoose没有声明age，那么去除的数据也是没有age的
- 当server发请求给数据库时，数据库会把数据以JSON的格式返回回来，mongoose把JSON转换成一个mongoose object
- 当想要存储object时，mongoose会把object转换成JSON，放在数据库里
#### 21.4.2 设计数据库
- er diagram
- 推荐画图软件：https://app.diagrams.net/
