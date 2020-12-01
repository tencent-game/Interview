------





# promise

### 同步和异步

###### 同步：停止等待运行结束，继续后续的运行

###### 异步（async）：需要等待一个内容完成后继续执行后后面的内容，但是不能够将后面的内容写在等待函数外，否则就会同时执行两个

同步按照顺序依次执行，异步是同时分开一起执行。计算机的同步异步与人的同步异步相反。

同步的情况：

异步的情况：1.操作性事件（概念中不叫异步）需要时间，

​					   2.load事件

​						3.setTimeout事件

​						4.setinterval事件

​						5.requestAnimationFrame()事件

js的一大特点就是单线程，在同一时间就只能做一件事，同步与异步的差别在与在单线程中的各个流程的执行顺序不同。单线程意味着所有任务需要排队，前一个任务执行完成后后一个任务才能执行。

同步任务是指在主线任务上排队执行的任务只有前一个任务执行完毕才能执行。异步任务是指不进入主线程，而进入“任务列表”的任务，只有等主线任务执行完毕后，任务队列才会请求进入主线程执行



异步机制：

（1）所有的同步任务都在主线程上执行，形成一个执行栈

（2）主线程外还存在“任务队列”，只有异步任务有了运行结果，就在任务队列中放置一个事件

（3）一旦执行栈中的所有同步任务执行完毕，任务系统就会读取“任务队列”。看里面有哪些事件，哪些对应的异步任务，于是结束等待状态，进入执行栈，开始执行

（4）主线程不断重复上面的第三步

### promise基础

promise  解决回调地狱

###### promise的格式

```js
var p=new Promise(function(resolve,reject){
            var img=new Image();
               img.src="./img/17.jpg";
               img.onload=function(){
                   resolve(img);
               }
               img.onerror=function(){
                   reject(img.src+"地址错误");
               }
          });
p.then(function(a){
            console.log(a);//执行resolve执行这个函数
          },function(b){
            console.log(b);//执行reject执行这个函数
          })
```

promise主要用于异步计算，可以将异步操作队列化，按照期望的顺序执行，返回符合预期的结果，在对象之间传递和操作promise，帮助我们处理队列。

resolve作用是，将Promise对象的状态从“未完成”变为“成功”（即从 pending 变为 resolved），在异步操作成功时调用，并将异步操作的结果，作为参数传递出去；
 reject作用是，将Promise对象的状态从“未完成”变为“失败”（即从 pending 变为 rejected），在异步操作失败时调用，并将异步操作报出的错误，作为参数传递出去。

promise有三个状态：
 1、pending[待定]初始状态
 2、fulfilled[实现]操作成功
 3、rejected[被否决]操作失败
 当promise状态发生改变，就会触发then()里的响应函数处理后续步骤；
 promise状态一经改变，不会再变。

Promise对象的状态改变，只有两种可能：
从pending变为fulfilled
从pending变为rejected。
这两种情况只要发生，状态就凝固了，不会再变了。

#### .then

1、接收两个函数作为参数，分别代表fulfilled（成功）和rejected（失败）
 2、.then()返回一个新的Promise实例，所以它可以链式调用
 3、当前面的Promise状态改变时，.then()根据其最终状态，选择特定的状态响应函数执行
 4、状态响应函数可以返回新的promise，或其他值，不返回值也可以我们可以认为它返回了一个null；
 5、如果返回新的promise，那么下一级.then()会在新的promise状态改变之后执行
 6、如果返回其他任何值，则会立即执行下一级.then()

##### .then()里面有.then()的情况

1、因为.then()返回的还是Promise实例
2、会等里面的then()执行完，再执行外面的

##### Promise.all() 批量执行

Promise.all([p1, p2, p3])用于将多个promise实例，包装成一个新的Promise实例，返回的实例就是普通的promise
 它接收一个数组作为参数
 数组里可以是Promise对象，也可以是别的值，只有Promise会等待状态改变
 当所有的子Promise都完成，该Promise完成，返回值是全部值得数组
 有任何一个失败，该Promise失败，返回值是第一个失败的子Promise结果

##### Promise.race() 类似于Promise.all() ，区别在于它有任意一个完成就算完成

asyns随便加

defer一般放在最后一个

async 函数执行后返回一个Promise对象

await只能写在async函数中

await 只能处理promise对象的异步等待

async 函数中使用return返回的内容可以通过then来获取





### 宏任务微任务

同步和异步都是在完成任务列的内容

同步任务条逐条进行

固定时间：setTimeout  setInterval requestAnimationframe(帧时间固定)

非固定时间：

#### 宏任务与微任务的定义

宏任务指将当前任务挪到  **下一个新的任务列**  的最顶端执行

微任务指将当前任务列的内容挪至当前任务列的最底端执行

```js
Promise.resolve().then(function(){
            setTimeout(function(){
                console.log("b");
            },0)
        })
        setTimeout(function(){
            Promise.resolve().then(function(){
                console.log("a");
            })
        },0) 
//首先是一个微任务，将setTimeout挪至当前任务列的最底端，因为下面一个大的setTimeout是一个宏任务所以将其中的promise放入下一个任务列。此时当前任务列中是settimeout...b.所以将其放入第三个任务列中，第二个任务列中的promise微任务将a放入第二个任务列的最低端，所以先打印a再打印b
```

![image-20200807214125227](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20200807214125227.png)

事件抛发都是同步及时触发的

```js
   var i=0;
        fn();
        function fn(){
            fn1();
            document.addEventListener("abc",function(){
                console.log("d");//先抛发后侦听所以不能打印d
            });
            console.log("a");
            fn2();
        }
        function fn1(){
            console.log("b");
            var evt=new Event("abc");
            document.dispatchEvent(evt);
        }
        function fn2(){
            console.log("c");
            i++;
            if(i<5) fn2();
        } 
//b  a c c c c c
```

微任务内的微任务优于微任务执行

```js
async function async1() {
    console.log( 'async1 start' )
    await async2()
    console.log( 'async1 end' )
}
async function async2() {
    console.log( 'async2' )
}
async1()
console.log( 'script start' )

执行结果
async1 start
async2
script start
async1 end
```

一旦遇到await 就立刻让出线程,阻塞后面的代码

等候之后,对于await来说分两种情况

- 不是promise 对象
- 是promise对象

**如果不是promise,await会阻塞后面的代码,先执行async外面的同步代码,同步代码执行完毕后,在回到async内部,把promise的东西,作为await表达式的结果**

**如果它等到的是一个 promise 对象，await 也会暂停async后面的代码，先执行async外面的同步代码，等着 Promise 对象 fulfilled，然后把 resolve 的参数作为 await 表达式的运算结果。**

**如果一个 Promise 被传递给一个 await 操作符，await 将等待 Promise 正常处理完成并返回其处理结果。**

```js
async function async1() {
            console.log( 'async1 start' ) //2
            await async2()
            console.log( 'async1 end' )//7
        }
        async function async2() {
            console.log( 'async2' )//3
        }
        console.log( 'script start' ) //1
        setTimeout( function () {
            console.log( 'setTimeout' )//8
        }, 0 )
        async1();
        new Promise( function ( resolve ) {
            console.log( 'promise1' )//4
            resolve();
        } ).then( function () {
            console.log( 'promise2' ) //6
        } )
        console.log( 'script end' )//5
```

```js
 new Promise( ( resolve, reject ) => {
                console.log( "promise1" )
                resolve()
            } )
            .then( () => {
                console.log( 1 )
            } )
            .then( () => {
                console.log( 2 )
            } )
            .then( () => {
                console.log( 3 )
            } )

        new Promise( ( resolve, reject ) => {
                console.log( "promise2" )
                resolve()
            } )
            .then( () => {
                console.log( 4 )
            } )
            .then( () => {
                console.log( 5 )
            } )
            .then( () => {
                console.log( 6 )
            } )
        // 1 4 2 5 3 6
```

先执行同步代码 promise1, promise2,此时微任务有两个任务 log(1)和log(4)

执行完log(1)和log(4)此时任务中有log(2)和log(5)两个微任务

执行log(2)和log(5)此时任务中有log(3)和log(6)两个微任务

连续的几个`then()`回调，并不是连续的创建了一系列的微任务并推入微任务队列，因为`then()`的返回值必然是一个`Promise`，而后续的`then()`是上一步`then()`返回的`Promise`的回调

`new Promise`在实例化的过程中所执行的代码都是同步进行的，而`then`中注册的回调才是异步执行的。在同步代码执行完成后才回去检查是否有异步任务完成，并执行对应的回调，而微任务又会在宏任务之前执行。

```js
new Promise(function (res) {//promise中的是同步任务，优先执行
    console.log(1);//---1
    res();
    Promise.resolve().then(function () {
        console.log(2);//---3//同步任务中的微任务被优先插入到当前任务列的最底端执行
    });
    new Promise(function (res) {
        res();
    }).then(function () {
        console.log(-1);//---4
    });
    console.log(0);//-----2
})
    .then(function () {
    console.log(3);//---5
    Promise.resolve().then(function () {
        console.log(4);//---7
    });
})
    .then(function () {
    console.log(5);//---8//5与7是同一级因为5在7前所以先执行5
});
Promise.resolve().then(function () {
    console.log(6);//---6//同级微任务中的同步优先级高于微任务所以6优先于4执行
    Promise.resolve().then(function () {
        console.log(7);//----9
    });
});

setTimeout(function () {//宏任务将其内容放入新第二个任务列头部
    setTimeout(function () {//宏任务将其内容放入新第四个任务列头部
        console.log(8);//---12
    }, 0);
    Promise.resolve().then(function () {//微任务，将其放在第二个任务列的尾部
        console.log(9);//---10
    });
}, 0);
setTimeout(function () {//宏任务将其内容放入新第三个任务列头部
      console.log(10);//---11
    }, 0);
```

------





```js
console.log(1);   // 1      //同步任务优先执行
    new Promise(function (res, rej) {
      console.log(2); //2      //同步任务
      res();
    })
      .then(function () {
        console.log(3); //5
        Promise.resolve().then(function () {
          console.log(5);//6 //微任务的微任务比微任务优先级更高，所以5在4前面
          setTimeout(function () {//宏任务，放在第五个任务列中
            console.log(6);//15
            Promise.resolve().then(function () {
              console.log(7);//16
            });
            setTimeout(function () {//宏任务放在第七个任务列中
              console.log(8);//18
            }, 0);
          }, 0);
        });
      })
      .then(function () {
        console.log(4);//7
      });
    setTimeout(function () {//等级最高的宏任务放在第二个任务列中
      console.log(9);//8
      new Promise(function (res) {
        res();
        console.log(10);//9
      }).then(function () {
        console.log(11);//10
      });
    });
    Promise.resolve().then(function () {
      setTimeout(function () {//宏任务，放在第五个任务列中
        Promise.resolve().then(function () {
          console.log(12);//14
        });
        console.log(13);//13
      }, 0);
    });
    setTimeout(function () {//宏任务放在第三个任务列中
      setTimeout(function () {//宏任务，放在第六个任务列
        setTimeout(function () {//宏任务放在第八个任务列中
          Promise.resolve().then(function () {
            console.log(14);//20
          });
          console.log(15);//19
        }, 0);
        console.log(16);//17
      }, 0);
      console.log(17);//11
    }, 0);
    console.log(18);//3 //同步任务
    new Promise(function (res) {
      console.log(19);//4    //同步任务
      setTimeout(function () {//宏任务  因为他的上一级是同步任务，所以他与最大的宏任务是同一级的所提放在第四个任务列中
        console.log(20);//12
      }, 0);
    });
//1，2，18，19，3，5，4，9，10，11，17，20，13，12，6，7，16，8，15，14，
```

