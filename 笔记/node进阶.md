# node进阶

### node的定义

*node:*

  *+ 官方: 基于 Chrome V8 的 JS 运行时环境*

  *+ 私人: 就是一个 "软件", 只不过这个软件是用来执行 js 文件*

   *=> 环境: 配置再你电脑里面的一个程序, 不存在桌面图标, 依靠命令行*



 *和 前端 js 有什么区别*

  *+ 前端:*

   *=> DOM - 文档对象模型*

​    *-> html 给的, 因为你的 js 文件是在 html 文件里面被引入执行的*

   *=> BOM*

​    *-> 浏览器 给的, 因为你的 js 文件是在浏览器环境下运行的*

   *=> ECMAScript*

​    *-> js 的语法, 代码怎么写*

  *+ 后端:*

   *=> ECMAScript*

​    *-> js 的语法*

   *=> 操作电脑的能力*

​    *-> node 给的, 因为你的 js 文件是在命令行运行, 再电脑系统里面运行*



 *为什么学习 node*

  *1. 面试需求: 面试要求掌握 node*

  *2. 全栈开发: 了解后端的工作过程*

  *3. 防止甩锅*



 *开始学习 node*

  *1. node 怎么运行 js 文件*

   *1-1. 打开命令行, 输入 node 回车*

​    *-> 表示已经运行 node 这个 "软件"*

​    *-> 你就可以再命令行输入 js 代码来执行*

​    *-> 缺点: 代码留不下来*

   *1-2. 打开命令行, 输入 node 你要执行的文件 回车*

​    *-> 把 js 代码写在一个 .js 后缀的文件里面*

​    *-> 通过命令行运行*

  *2. 模块化开发*

   *+ 前端:*

​    *=> js 文件是引入再 html 文件中使用的*

​    *=> 多个 js 文件时引入再一个 html 文件中*

​    *=> 我们共享一个 window*

​    *=> 你需要再其他文件里面使用的方法*

​    *=> 你直接挂载再 window 上, 或者就直接写在全局*

   *+ node:*

​    *=> 每一个 js 文件都是相对独立的*

​    *=> 互相之间没有任何关系, 我们没有一个统一调配的东西*

​    *=> 我们只能靠模块化开发*



 *模块化分类*

  *1. 什么是模块*

   *=> 一个 js 文件就是一个模块*

   *=> 我们把一类方法放在一个 js 文件里面, 这个 js 文件就变成了一个模块*

   *=> 再需要哪一类方法的时候, 引入这个 js 文件就好了*

  *2. 什么是模块化*

   *=> 再开发的过程中, 尽可能把开发方式趋近于模块的方式*

   *=> 把我们所有的内容都按照类别分好文件*

   *=> 按需引入*

  *3. 模块化的分类*

   *3-1. 自定义模块*

​    *-> 我们自己按照模块化的语法, 开发的 js 文件*

​    *-> 自己定义模块, 自己再需要的时候导入模块使用*

​    *-> 自己决定模块内哪些内容向外暴露*

   *3-2. 内置模块*

​    *-> node 这个环境天生自带的一些模块("一个一个的 js 文件")*

​    *-> 你需要使用的时候, 直接引入使用就好了*

   *3-3. 第三方模块*

​    *-> 其他人把一些常用的功能直接封装好*

​    *-> 做了一个开源*

​    *-> 我们使用的时候先下载下来, 直接导入按照人家的规则使用*



 *第三方模块的使用*

  *1. 下载, 使用 npm 下载*

   *+ 确定好一个目录进行下载*

   *+ 在一个项目里面, 把所有的第三方包都放在一个目录下*

   *+ paths: [*

​    *'E:\\BK_GP_19\\01_第一周\\01_DAY\\01_代码\\04_第三方模块\\node_modules',*

​    *'E:\\BK_GP_19\\01_第一周\\01_DAY\\01_代码\\node_modules',*

​    *'E:\\BK_GP_19\\01_第一周\\01_DAY\\node_modules',*

​    *'E:\\BK_GP_19\\01_第一周\\node_modules',*

​    *'E:\\BK_GP_19\\node_modules',*

​    *'E:\\node_modules'*

   *]*

   *+ 只要你的 node_module 文件夹在这些里面 他都可以找到*

  *2. 在你需要的位置导入*

   *+ 直接 require(包名)*

   *+ 不需要 .js 后缀*

  *3. 第三方包的使用么有规则*

   *+ 你要去官网看*

**/*

## node的模块

##### 1.自定义模块

###### 定义模块

 *定义模块*

  *+ 在每一个 js 文件里面*

  *+ 天生自带一个变量, 叫做 module, 表示模块*

  *+ 用来描述这个文件(模块)的*

  *+ 我们这个文件定义好以后, 你想让别人使用的东西, 就放在 module.exports 里面*

  *+ 再设计的时候, 给我们提供了两种其他方式*

   *1. 给 module.exports 从新赋值*

​    *=> 赋值为一个新的对象或者数组或者任何其他数据类型*

   *2. exports 也是每一个 js 文件天生自带的一个变量*

​    *=> 每一个 js 文件里面相当于有一句代码 var exports = module.exports*

​    *=> 注意: 如果你需要给 module.exports 从新赋值, 那么不能使用 exports*

定义模块导出方式

```js
// 1. 标准导出
// 如果我想让 fn1 方法别人也可以使用
 module.exports.fn1 = fn1
 module.exports.num = 100
// 此时 我的 module.exports = { fn1: function () {}, num: 100 }


// 2. 给 module.exports 从新赋值
module.exports = {
   fn1: fn1,
   num: 100
 }



// 3. 利用 exports 向外暴露内容
 exports.fn1 = fn1
 exports.num = 200
 exports.str = 'hello world'
//如果之后module.exports重新赋值，那export将会不好使，
```

###### 使用模块

  *+ 就是把其他模块导入到自己的文件里面*

  *+ 使用另一个文件导出的内容*

  *+ 每一个 js 文件里面天生自带一个方法*

  *+ 叫做 require()*

   *=> 语法: require('要导入的 js 文件路径')*

​    *-> 如果后缀是 .js 可以省略不写*

   *=> 返回值: 被导入文件里面的 module.exports*

  *+ 导入以后, 你就可以使用 01 这个文件里面向外暴露的内容*

导入我们定义好的模块

```js
const modA = require('./01_定义模块')
modA.fn1()
```

### 内置模块

### fs模块

 fs 模块 - file system 文件系统模块

  => 这个模块里面封装的方法都是和操作 文件 和 文件夹 相关的内容

  => node 天生自带的一个模块

  => 我们直接导入使用



###### readFile()

  => 异步读取文件

  => 语法: fs.**readFile**(路径, 读取格式, 回调函数)

   -> 路径: 你要读取的文件的路径, 如果路径不存在, 会出现错误

   -> 读取格式: 选填, 默认是 buffer, 我们可以选填 'utf8'

   -> 回调函数: 读取成功以后会执行的函数

```js
fs.readFile('./test.txt', 'utf8', function (err, data) {
  // err 就是读取失败的时候的错误信息
  // data 就是读取成功的时候的读取内容
  if (err) return console.log(err)

  console.log('读取成功')
  console.log(data)
})
```



###### readFileSync()

  => 同步读取文件

  => 语法: fs.**readFileSync**(路径, 读取格式)

  => 返回值: 读取的文件内容

  => 注意: 读取路径不存在, 或者没有权限的时候, 会报错, 打断程序的继续执行

```js
const res = fs.readFileSync('./test1.txt', 'utf8')
console.log('读取完成')
console.log(res)
```

同步读取会阻塞后续代码的执行，而异步读取则不会



######   **writeFile**()

  => 异步写入文件

  => 语法: fs.**writeFile**(路径, 要写入的内容, 回调函数)

   -> 路径: 你要写入文件的路径, 如果路径文件不存在, 会创建一个这个文件再写入

   -> 写入的内容: 你自己定义

   -> 回调函数: 写入成功以后执行的函数, 必填

  => 注意: 完全覆盖式的写入

```js
fs.writeFile('./test.txt', '你好 世界', function () {
  console.log('写入完成')
})
```



###### writeFileSync()

  => 同步写入文件

  => 语法: fs.**writeFileSync**(路径, 要写入的内容)

  => 注意: 完全覆盖式的写入

注意如果在同步写入之前进行异步写入，那么同步写入的内容将不会写入到文件中，在同步之后进行异步写入则会显示一异步插入的内容

```js
fs.writeFileSync('./test.js', 'hello node')
console.log('写入完成')
```



######   **appendFile**()

  => 异步追加内容

  => 语法: fs.**appendFile**(路径, 追加的内容, 回调函数)

   -> 路径: 写入文件的路径, 没有该路径, 自己创建

   -> 追加的内容

   -> 回调函数: 必填

```js
fs.appendFile('./test1.txt', 'hello world', () => {})
```



######  appendFileSync()

  => 同步追加内容

  => 语法: fs.**appendFileSync**(路径, 追加的内容)

同步追加比异步追加要快

```js
fs.appendFileSync('./test1.txt', '你好 世界')
```



######   readdir()

  => 异步读取文件夹

  => 语法: fs.**readdir**(路径, 回调函数)

```js
fs.readdir('../02_自定义模块', (err, data) => {
  if (err) return console.log(err)

  console.log('读取文件夹成功')
  console.log(data)
})
```



######  readdirSync()

  => 同步读取文件夹

  => 语法: fs.**readdirSync**(路径)

```js
const res = fs.readdirSync('../02_自定义模块')
console.log(res)
```



######   mkdir()

  => 异步创建文件夹

  => 语法: fs.**mkdir**(路径, 回调函数)

```js
fs.mkdir('./a', (err) => {
  if (err) return console.log(err)

  console.log('创建文件夹成功')
})

```



######   mkdirSync()

  => 同步创建文件夹

  => 语法: fs.**mkdirSync**(路径)

```js
fs.mkdirSync('./b')
```



######  rmdir()

  => 异步删除文件夹

  => 语法: fs.**rmdir**(路径, 回调函数)

```js
fs.rmdir('./a', err => {
  if (err) return console.log(err)
})
```



######   rmdirSync()

  => 同步删除文件夹

  => 语法: fs.**rmdirSync**(路径)

```js
fs.rmdirSync('./b')
```



######   unlink()

  => 异步删除文件

  => 语法: fs.**unlink**(路径, 回调函数)

```js
fs.unlink('./test1.txt', err => {
  if (err) return console.log(err)
})
```



######  unlinSync()

  => 同步删除文件

  => 语法: fs.**unlinkSync**(路径)

```js
fs.unlinkSync('./test123.txt')
```



######   stat()

  => 异步查看

  => 语法: fs.**stat**(路径, 回调函数)

   -> 回调函数里面可以接收一个 data

   -> 表示你查看的这个路径的内容

```js
fs.stat('./test.txt', (err, data) => {
  if (err) return console.log(err)

  console.log(data)
  console.log(data.isFile())
  console.log(data.isDirectory())
})
```



######  statSync()

  => 同步查看

  => 语法: fs.**statSync**(路径)

  => 返回值: 查看该路径的结果

```js
const res = fs.statSync('../02_自定义模块')
console.log(res)
console.log(res.isFile())
console.log(res.isDirectory())
```



######  isFile()

  => 注意: 只有 stats 可以调用

   -> stat 的 回调函数中的 data

   -> statSync 的返回值

  => 语法: stats.**isFile**()

  => 返回值: 一个布尔值

######  isDirectory()

  => 注意: 只有 stats 可以调用

   -> stat 的 回调函数中的 data

   -> statSync 的返回值

  => 语法: stats.**isDirectory**()

  => 返回值: 一个布尔值

### path模块

 *+ node 自带的一个内置模块*

  *+ 里面封装的都是一些操作路径的或者和路径相关的方法*

  *+ 使用的时候直接导入就可以了*

###### join()

  + 拼接相对路径

  + 语法: path.join(路径1, 路径2, 路径3, ...)

  + 返回值: 拼接好的路径结果

  + 注意:

   => 拼接规则是后一个参数是前一个参数的子级

   => 除非你写 ../

```js
const path1 = path.join('a', './b', '/c', 'd')
console.log(path1)

const path2 = path.join('a', './b', '/c', 'd', '../e')
console.log(path2)

```



######   resolve()

  + 拼接绝对路径

  + 语法: path.resolve(路径1, 路径2, 路径3, ...)

  + 返回值: 拼接好的绝对路径

  + 注意:

   => 拼接规则是每一个参数都是相对独立的一个参数

   => 如果你写 /xx, 直接回到根目录

​    -> xx 当前目录下

​    -> ./xx 当前目录下

​    -> ../xx 上一级目录

​    -> /xx 根目录*

```js
const path1 = path.resolve('a', './b')
console.log(path1)
const path2 = path.resolve('a', './b', '/c')
console.log(path2)

```



######  3. extname()

  + 获取文件后缀名

  + 语法: path.extname(文件名)

+ 返回值: 该文件的后缀名*

```js
const ext = path.extname('abc.html')
console.log(ext)

```



######  4. isAbsolute()

  + 判断路径是不是绝对路径

  + 语法: path.isAbsolute(路径)

  + 返回值: 一个布尔值

  + 路径区分:

   => 绝对路径: 从根目录开始的路径

   => 相对路径: 不是从根目录开始的路径*

```jsjs
const res = path.isAbsolute('/a/b')
console.log(res)
```



######  5. parse()

  + 解析路径信息

  + 语法: path.parse(路径)

  + 返回值: 一个对象, 里面包含该路径的所有信息

```js
const res = path.parse(__filename)
console.log(res)
```



 每一个 js 文件里面自带两个变量

  1. __dirname: 表示该文件所在的文件夹的绝对路径

  2. __filename: 表示该文件的绝对路径

### url内置模块

  \+ node 自带的一个内置模块

  \+ 里面封装的都是和 url 地址栏相关的方法

  \+ 使用的时候直接导入使用



######  . **parse**()

  \+ 解析 url 地址的方法

  \+ 语法: url.**parse**(url 地址, 是否解析查询字符串)

   -> 地址: 要解析的地址

   -> 是否解析查询字符串: 默认是 false, 选填 true

​    => 会把地址里面的查询字符串解析成一个对象的形式

  \+ 返回值: 是一个对象, 里面包含整个 url 地址的所有信息

```js
const url = require('url')
xujiangtao
const res = url.parse('http://www.xujiangtao.com:8080/a/b/c/hello.html?a=100&b=200#abc', true)
console.log(res)

//post 请求是在请求体携带参数
  a=100&b=200&c=300
const str = 'a=100&b=200&c=300'
const res = url.parse('?' + str, true)
console.log(res)
```

### http模块

 http 模块

  \+ 也是 node 内置的一个 模块

  \+ 主要是用来创建一个 http 服务的模块

  \+ 需要使用的时候直接导入使用



######  **createServer**()

  => 创建服务的方法

  => 语法: http.**createServer**(function () {})

   -> 每一个请求进来的时候, 都会触发函数

  => 返回值: 一个服务



######   **listen**()

  => 注意: 需要使用 **服务**(createServer 的返回值) 来调用

  => 语法: 服务.**listen**(端口号, 回调函数)

   -> 端口号: 0 ~ 65535, 尽量不使用 1024 以下

   -> 域名: 默认是本机 localhost || 127.0.0.1

  => 当 listen 执行以后

   -> 你的 命令行, 就会被变成了一个服务器

   -> 一个什么都没有的服务器

   -> 当你访问 localhost:8080 的时候, createServer 后面的函数就会执行



 开发文档:

  \1. /abc

   => 表示 index.html

  \+ 前端: 如果我想要 index.html 文件

   => 发送请求: path 位置书写 /abc

  \+ 后端: 当我接收到 /abc 这个请求的时候

   => 我要去读取 index.html 文件, 把内容返回给前端

```js
const http=require('http')
const fs=require('fs')

const server=http.createServer(function(req,res){
    console.log(req.url);
    if(req.url==='/abc'){
        fs.readFile('./index.html',(err,data)=>{
            if(err)return console.log(err);
            res.end(data);
        })
    }
        // console.log("有请求进来了");
})

server.listen(8080, () => {
    console.log('running at port 8080! ^_^ ')
  })
```

## 第三方模块

### moment模块

 moment 是一个第三方插件

  \+ 专门用来格式化时间

  \+ 官方: https:*//momentjs.com/*



 使用

  \+ **moment**(时间对象).**format**(格式化规则)

  \+ 在你导入包以后, 使用方法之前, 设置一下语言环境

```js
const moment = require('moment')
// 把格式化包换成中文
moment.locale('zh-cn')

// 拿到当前时间
const time = new Date()

// 把当前时间进行格式化
const res = moment(time).format('MMMM Do YYYY, h:mm:ss a')
console.log(time)
console.log(res)
```

### nodemailer模块

nodemailer 模块

  \+ 第三方模块, 专门用来发邮件

  \+ 下载使用



 使用:

  \1. 使用 nodemailer 创建一个 **发送器**(邮差)

   => 语法: nodemailer.**createTransporter**(配置文件{})

​    -> 参数位置: 需要一些内容

​    -> 对邮件发送放的配置

​    -> 直接在包里面找到 -> nodemailer -> lib -> well-known

   => 返回值: 就是一个发送器

  \2. 使用发送器去发送邮件

   => **sendmail**(邮件的配置{}, 回调函数) 方法

​    -> from

​    -> to

​    -> subject: '标题'

​    -> text: '' 文本内容

​    -> html: 超文本内容

```js
const nodemailer = require('nodemailer')
const transporter = nodemailer.createTransport({
    "host": "smtp.qq.com",
    "port": 465,
    "secure": true,
    auth:{
        user:"1871230468@qq.com",
        pass:"hrojhqfveyvadbic",
    }
})

transporter.sendMail({
    from:"1871230468@qq.com",
    to:"1911124543@qq.com",
    subject:"漂流瓶",
    text:"",
    html:"轩姐，╰(￣ω￣ｏ)"
    
},function(err,info){
    if(err)return console.log(err);

    console.log("发送成功");
    console.log(info);
})
```

