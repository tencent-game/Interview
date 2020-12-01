# Ⅰ- 壹 - BOM浏览器对象模型
 1. 浏览器对象模型提供了可以与浏览器窗口进行互动的对象结构。 

 2. BOM由多个对象组成，其中代表浏览器窗口的Window对象是BOM的顶层对象，其他对象都是该对象的子对象。

 3. BOM提供了一些访问窗口对象的一些方法，我们可以用它来移动窗口位置，改变窗口大小，打开新窗口和关闭窗口，弹出对话框，进行导航以及获取客户的一些信息如：浏览器品牌版本，屏幕分辨率。但BOM最强大的功能是它提供了一个访问HTML页面的一入口——document对象，以使得我们可以通过这个入口来使用DOM的强大功能！！！

## 一 window与BOM的关系

#### 1. BOM:浏览器对象模型。 window 对象:它代表浏览器的窗口。

所有全局 JavaScript 对象，函数和变量自动成为 window 对象的成员。
全局变量是 window 对象的属性。document 对象也是 window 对象属性。
全局函数是 window 对象的方法。


#### 2. document是DOM的核心对象，window则是BOM的核心对象，而又有：**

```javascript
console.log(window.document === document);    //true
```

因为document是DOM的根节点，而以上代码又表明：document在window对象中是作为其一个属性而存在的，因此从这个角度来说，BOM包含了DOM。与此类似，你还可以验证如下代码：

```javascript
console.log(window.location === location);    //true
console.log(window.navigator === navigator);    //true
console.log(window.screen === screen);    //true
console.log(window.history === history);    //true
console.log(window.window === window);    //true
```
location navigator screen history和window一样，都是BOM提供的对象，只不过它们和document对象一样，都同时以属性的形式存在于window中。
#### 3. 当你在浏览器中console.log(window)，你应该能大体归纳出其构成如下图：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701112528342.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

可以看到，window可不仅仅是BOM中的那个浏览器窗口对象而已，它实际上包含了某个页面所在的窗口中与JavaScript相关的方方面面


**标注** ：  **以上取自**  https://www.jianshu.com/p/f5409202a835


# Ⅱ - 贰 -BOM对象
![在这里插入图片描述](https://img-blog.csdnimg.cn/2020010319363982.png)

| 编号 | 对象             | 简述           |
| ---- | ---------------- | -------------- |
| 1.   | window.document  | Document  文档 |
| 2.   | window.location  | 本地信息       |
| 3.   | window.history   | 历史           |
| 4.   | window.screen    | 屏幕           |
| 5.   | window.navigator | 浏览器信息     |



## 一 window对象
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701114110960.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)
#### 1 window 窗口尺寸

|                                       |                                                            |
| ------------------------------------- | ---------------------------------------------------------- |
| window.innerWidth、window.innerHeight | 浏览器窗口可视区高度（不包括浏览器控制台、菜单栏、工具栏） |
| window.outerWidth、window.outerHeight | 可以获取浏览器窗口的整个宽                                 |



#### 2 window 窗口方法

 * window.open() : 打开新窗口
 * window.close() : 关闭当前窗口
* window.moveTo() : 移动当前窗口
 * window.resizeTo() : 重新调整当前窗口

#### 3 定时器
js 定时器有以下两个方法：
| 定时器        | 简介                                                         |
| ------------- | ------------------------------------------------------------ |
| setInterval() | 按照指定的周期（以毫秒计）来调用函数或计算表达式。方法会不停地调用函数，直到 clearInterval() 被调用或窗口被关闭。 |
| setTimeout()  | 在指定的毫秒数后调用函数或计算表达式。                       |

###### 1 setTimeout()

- setTimeout(function, milliseconds)在等待指定的毫秒数后执行函数。
-  clearTimeout()取消setTimeout设置。

```javascript
let timeer = setTimeout(function () {
    console.log("123");
}, 1000);

clearTimeout(timeer);
```

###### 2 setInterval()

- setInterval(function, milliseconds)每隔指定的毫秒数执行代码
- clearInterval()取消setInterval()设置

```javascript
let timer = setInterval(function () {
    console.log("123");
}, 1000);
clearTimeout(timer);
```

## 二  location对象

1. location对象提供了与当前窗口中加载的文档有关的信息,还提供了一些
导航的功能,它既是window对象的属性,也是document对象的属性。
2. location最有用的对象之一；既是window对象的属性又是document对象的属性
3. window.location 本地信息

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701115804830.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

**location的属性**
|                   |                                                              |
| ----------------- | ------------------------------------------------------------ |
| location.hash     | 返回url中的hash（#后的锚点字符），如果url中不包含，则返回空字符串 |
| location.host     | 返回服务器名称和端口号                                       |
| location.hostname | 返回不带端口号的服务器名称,返回 web 主机的域名               |
| location.href     | 返回当前加载页面的完整url。（location对象的toString()也返回这个值）可以产生历史记录，可以获取。可以设置 |
| location.pathname | 返回url中的目录和文件名(返回当前页面的路径和文件名)          |
| location.port     | 返回url指定的端口号，如果不包含则返回空字符串(返回 web 主机的端口 （80 或 443）) |
| location.protocol | 返回页面使用的协议。通常为http:或者https                     |
| location.search   | 返回url查寻字符串 ，？后面的                                 |
| location.assign   | 可以产生历史记录，可以获取。可以设置                         |


**reload()方法：** 重新加载当前页面

```javascript
setTimeout(function(){
        location.reload();
 },3000) 
 //   重载刷新当前页面
```

**href：** 获取当前页面地址，也可以设置当前页面地址，达到跳转页面

```javascript
location.href = "https://www.baidu.com/";
// console.log(location.href);//当前页面的地址
// location.href="http://www.163.com";//href获取当前页面地址，也可以设置当前页面地址，达到跳转页面
//location.assign("http://www.163.com");//只能跳转页面
// location.replace("http://www.163.com");//替换当前页面，跳转页面

//点击按钮跳转到什么页面,当服务器返回处理完成数据后要求页面跳转到那里
document.onclick=function(){
   // location.href="http://www.163.com";
   // location.assign("http://www.163.com");
   	location.replace("http://www.163.com");//不能产生历史记录
    }
```
## 三 history对象
1. history对象保存了用户在浏览器中访问页面的历史记录

2. 有历史记录的时候可以使用

3. window.history 历史
  ![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701115826531.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

  
|                        |                           |
| ---------------------- | ------------------------- |
| history.go(0)          | 刷新页面                  |
| history.go(1)          | 向前一个                  |
| history.go(-1)         | 向后一个                  |
| history.back           | 向后退一页                |
| history.forward        | 向前进一页                |
| history.onpopstate     | 事件监听。                |
| history.pushState()    | 参数的可以作为历史记录    |
| history.replaceState() | 可以跳转页面 改变当前内容 |

使可以使用back()和forward()可以代替go()方法



####  1 history.pushState() 和 history.replaceState()

history.replaceState()会跳转页面 ，修改之前的地址

history.pushState()不会跳转页面

可以通过history.state获取 值

其他功能和用法 基本一致

```javascript
window.history.pushState(data, title, targetURL);
@状态对象：传给目标路由的信息,可为空
@页面标题：目前所有浏览器都不支持,填空字符串即可
@可选url：目标url，不会检查url是否存在，且不能跨域。如不传该项,即给当前url添加data

window.history.replaceState(data, title, targetURL);
@类似于pushState,但是会直接替换掉当前url,而不会在history中留下记录

history.pushState({page: 1}, 'title 1', '?page=1')
// URL 显示为 http://example.com/example.html?page=1
history.state可以获取 第一个参数的值

history.pushState({page: 2}, 'title 2', '?page=2');
// URL 显示为 http://example.com/example.html?page=2


history.back()
// URL 显示为 http://example.com/example.html?page=1

history.back()
// URL 显示为 http://example.com/example.html

history.go(2)
// URL 显示为 http://example.com/example.html?page=3
```














## 四 screen对象
- screen对象包含有关客户端显示屏幕的信息

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701115839765.png)

**screen属性**

|                    |                                        |
| ------------------ | -------------------------------------- |
| screen.availHeight | 屏幕的高度像素减去系统部件高度之后的值 |
| screen.availWidth  | 屏幕的宽度像素减去系统部件宽度后的值   |
| screen.height      | 屏幕的高度像素                         |
| screen.width       | 屏幕的宽度像素                         |

```javascript
//去除了任务栏的宽高
 console.log(screen.availWidth,screen.availHeight);
 //全屏幕宽高
 console.log(screen.width,screen.height);
```



## 五 navigator对象
1. window.navigator  浏览器信息
2. 检测显示网页的浏览器类型；常用的是检测是否安装了特定插件；
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701115854844.png)
**navigator属性**

| 属性       | 简介                                         |
| ---------- | -------------------------------------------- |
| userAgent  | 返回由客户机发送服务器的 user-agent 头部的值 |
| appName    | 返回浏览器的名称。                           |
| appVersion | 返回浏览器的平台和版本信息。                 |
| platform   | 返回运行浏览器的操作系统平台。               |

```javascript
console.log(navigator.userAgent);//获取浏览器信息
console.log(navigator.platform);//区分操作系统
```

# Ⅲ - 叁 -应用
## 一 分解地址
- navigator (navigator.userAgent)
- screen (screen.width / screen.heigght)
- location
- history (history.back() / history.forward())

```javascript
//示例
https://segmentfault.com/search?q=web#mid=100

//整个url
location.href
"https://segmentfault.com/search?q=web#mid=100"

//协议
location.protocol
"https:"

//域名
location.host
"segmentfault.com"

//路径
location.pathname
"/search"

//参数
location.search
"?q=web"

//哈希
location.hash
"#mid=100"
```
## 二 检验浏览器的类型

**navigator.userAgent**

```javascript
var ua = navigator.userAgent;
var isChrome = ua.indexOf('Chrome');
console.log(isChrome );
```
## 三 解析url
#### 1 手动解析

```javascript
function getQueryStringArgs(url){
        url = url == null ? window.location.href : url;
        var qs = url.substring(url.lastIndexOf("?") + 1);
        var args = {};
        var items = qs.length > 0 ? qs.split('&') : [];
        var item = null;
        var name = null;
        var value = null;
        for(var i=0; i<items.length; i++){
            item = items[i].split("=");
            //用decodeURIComponent()分别解码name 和value（因为查询字符串应该是被编码过的）。
            name = decodeURIComponent(item[0]);
            value = decodeURIComponent(item[1]);

            if(name.length){
                args[name] = value;
            }
        }

        return args;
    }
console.log(getQueryStringArgs('https://www.baidu.com/baidu?tn=monline_3_dg&ie=utf-8&wd=12306%E7%81%AB%E8%BD%A6%E7%A5%A8%E7%BD%91%E4%B8%8A%E8%AE%A2%E7%A5%A8%E5%AE%98%E7%BD%91'));
    // Object {tn: "monline_3_dg", ie: "utf-8", wd: "12306火车票网上订票官网"}
```

#### 2 使用正则

```javascript
function getQueryStringArgs(url){
        url = url == null ? window.location.href : url;
        var qs = url.substring(url.lastIndexOf("?") + 1);
        var args = {};
        var items = qs.length > 0 ? qs.split('&') : [];
        var item = null;
        var name = null;
        var value = null;
        for(var i=0; i<items.length; i++){
            item = items[i].split("=");
            //用decodeURIComponent()分别解码name 和value（因为查询字符串应该是被编码过的）。
            name = decodeURIComponent(item[0]);
            value = decodeURIComponent(item[1]);

            if(name.length){
                args[name] = value;
            }
        }

        return args;
    }
console.log(getQueryStringArgs('https://www.baidu.com/baidu?tn=monline_3_dg&ie=utf-8&wd=12306%E7%81%AB%E8%BD%A6%E7%A5%A8%E7%BD%91%E4%B8%8A%E8%AE%A2%E7%A5%A8%E5%AE%98%E7%BD%91'));
    // Object {tn: "monline_3_dg", ie: "utf-8", wd: "12306火车票网上订票官网"}
```


# 0 - 0 - 知识点：

### addEventListener 监听器

```javascript
document.querySelector("button").addEventListener("click",clickHandler);
根据标签名获取button这个元素添加一个监听事件click，第二个参数为一个函数
 function clickHandler(e){
}
```

###  e.clientX,e.clientY  //鼠标点击的坐标
###  Array.from(列表);转化为数组
###  trim（）去掉字符串的前后空格