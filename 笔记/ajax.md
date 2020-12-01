# Ajax

### json

##### 简介

JSON是以纯文本结构组织所要传送的数据，数据内容包括字符串、数字、数组和对象等，由于JSON易读以及纯文本格式的特性，可以非常容易地与其他程序进行沟通与数据交换。JSON文件的文件类型是“.json”

JSON数据结构通过大括号，中括号，逗号和冒号来组织数据。

冒号代表的是一个键值对应一个值

大括号内代表的是“对象”对象代表的是一系列“键：值”的集合。不同的信号之间用逗号隔开。

中括号内代表的是“数组”数组内可以存放数字，文字，布尔值，数组，对象等变量。

```js
var obj=eval('('+str+')')//由JSON字符串转换为JSON对象
var obj=JSON.parse(str);//由JSON字符串转换为JSON对象
var last=JSON.stringify(obj)//将JSON对象转换为JSON字符
```



### Ajax概述

它是浏览器提供的一套办法，可以实现页面无刷新更新数据，提高用户浏览网站应用的体验

### Ajax运行原理

Ajax相当于浏览器发送请求与接受响应的代理人，以实现在不影响用户浏览页面的情况下，局部更新页面数据，从而提高用户体验。

![image-20200808193247043](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20200808193247043.png)

Ajax的实现步骤

```js
 var xhr=new XMLHttpRequest();//XMLHTTPRequest，创建一个AJAX
xhr.addEventListener("load",loadHandler);//执行loadHandler函数
xhr.open("GET","http://10.9.65.239:4006?user=xietian");//添加访问方式以及访问地址
xhr.send();
```

