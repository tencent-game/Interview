

# BOM

**全称Browser Object  Model**

window对象

​	location:本地

​	history：历史

​	screen：屏幕

​	navigator：信息

### Window对象：

Window是客户端JavaScript程序的全局对象

1.打开，关闭窗口的方法

```js
document.onmousemove=function(){
            // close();
            open("http://www.163.com","网易","width=400,height=400");
        }
```

2.浏览器页面大小以及窗口大小

```js
console.log(innerWidth,innerHeight);
console.log(outerWidth,outerHeight);
```

3.窗口左上角距离屏幕左上角的距离

```js
console.log(screenLeft,screenTop);
        console.log(screenX,screenY);
```

### location属性

window对象location属性引用的是Location对象，他表示该窗口中当前显示的文档的URL，并定义方法使窗口载入新的文档

```js
location.reload();//重载，刷新当前界面
location.href="http://www.163.com";//可以设置跳转当前页面地址
location.assign("http://www.163.com");//可以设置跳转当前页面地址
location.replace("http://www.163.com");//不产生历史记录
console.log(location.hash);//返回#和后面的url片段字符串
console.log(location.search);//查询部分，返回？号后面的参数
console.log(location.hostname);//返回url的主机名部分
console.log(location.port);//返回url的端口部分，这个属性是一个字符串，而不是数字
console.log(location.pathname);//返回url的路径名部分
console.log(location.protocol);//返回url的协议部分
console.log(location.host);//返回URL的主机名和端口部分
console.log(location.href);//返回文档的URL的完整文本
```

### history属性

Window对象的history属性引用的是该窗口的History对象，History对象是用开把窗口的浏览历史用文档和文档状态列表的形式表示

```js
history.back();//回退
history.forward();//前进
history.go(-1);//回退1
history.go(0);//刷新
history.go(1);//前进1
history.pushState(data,string title,[string url])//添加历史记录in
history.replaceState(data,string title,[string url])//刷新
```

### screen属性

提供有关窗口显示的大小和可用颜色数量的信息

```js
   console.log(screen.availWidth,screen.availHeight);//不包含任务栏宽高
   console.log(screen.width,screen.height);//整个屏幕宽高
```

### navigator属性

引用Navigator对象，Navigator对象包含一些描述正在其中运行代码的web浏览器的属性

```js
console.log(navigator.userAgent);//浏览器用于HTTP请求的user-agent头信息的值
console.log(navigator.appName);//浏览器的名字
console.log(navigator.appVersion);//浏览器版本及平台信息
console.log(navigator.platform)；//运行当前浏览器的操作系统
```



# DOM

全称Document Object  Model（文档对象模型），表示和操作HTML和XML文档内容的基础API。

### 元素继承树

所有元素都是DOM类型，是对象类型。

### 节点（node）

节点包括标签，注释，文本，文档。

节点类型：

1. 元素节点：每个HTML标签都是一个元素节点，  值为数字1
2. 属性节点：元素节点的属性 ，，值为数字2
3. 文本节点：元素节点或属性节点中的文本内容。。值为数字3
4. 注释节点：表示文本注释。值为数字8
5. 文档节点：表示整个文档（DOM的4树的根节点，即document）。值为数字9

任何标签的nodename都是该标签的大写字母

#### 节点属性

![image-20200717191605330](C:\Users\86178\AppData\Roaming\Typora\typora-user-images\image-20200717191605330.png)

##### 标签的内容属性

- innerHTML

**以 HTML 代码格式获取或设置节点的内容**

获取标签内容的时候，不管标签还是文本，都能获取到  innerHTML设置内容的时候，覆盖原来内容，标签也能生效，浏览器能解析这个标签

- innerText

**获取或设置节点的文本内容**

获取标签内容的时候，只会获取文本，标签扔掉了 设置标签内容的时候，覆盖原来内容，对标签进行转义（目的：把标签直接当文本来用）

区别：

相同点：都是用来获取和设置标签内容的

不同点：

- nnerHTML可以用于获取和设置标签的所有内容，包括标签和文本内容
- innerText只识别文本，标签会被转义。（可以防止 xss 攻击）

#### 节点的属性

分别是 nodeName（节点名称）nodeValue（节点值）nodeType（节点类型）

#####  nodeName（节点名称）

**获取节点名称，只读属性** 

各个节点的返回值

| 节点类型           | nodeName          |
| ------------------ | ----------------- |
| 文档节点(Document) | 返回 #document    |
| 元素节点(Element)  | 返回 大写元素名称 |
| 属性节点(Attr)     | 返回 属性名称     |
| 文本节点(Text)     | 返回 #text        |

##### nodeValue（节点值）

获取或设置节点的值

各个节点的返回值**
说明：文档节点、元素节点此属性返回 null，并且为只读。

| 节点类型           | nodeType           |
| ------------------ | ------------------ |
| 节点类型           | nodeValue          |
| 文档节点(Document) | 只读，返回 null    |
| 元素节点(Element)  | 只读，返回 null    |
| 属性节点(Attr)     | 获取或设置属性的值 |
| 文本节点(Text)     | 获取或设置文本的值 |

##### nodeType（节点类型）

**返回节点类型，只读属性**

- **各个节点的返回值**


| 节点类型           | nodeType |
| ------------------ | -------- |
| 文档节点(Document) | 9        |

| 元素节点(Element)	| 1
| 属性节点(Attr)	| 2| 
| 文本节点(Text)	| 3| 

### 获取文档元素

```js
document.getElementById("id");//通过id获取元素
var list=document.getElementsByTagName("div");
通过标签名获取标签列表，只能通过document获取,HTMLCollection

var list=document.getElementsByClassName("div1") 
通过Class名获取标签列表，任何标签都可以获取其子项中Class列表,HTMLCollection
console.log(list)

var list=document.getElementsByName("sex");
通过name属性获取节点列表，只能通过document获取,NodeList
NodeList
```

### 选择器

选择选择器列表中的第一个元素

```js
var div=document.querySelector(所有选择器)
var div=document.querySelector("#div0");
var div=document.querySelector(".div1");
var div=document.querySelector("[type=text]");
var div=父容器.querySelector()
```

*选择选择器可以获取的所有元素*

```js
var div=document.querySelectorAll(所有选择器)
```

##### 1。getElementById()

**获取指定 ID 的元素。**

- 参数：元素 ID。
- 返回值：元素节点对象。若没有找到，返回 null。
- HTML 元素 ID 是区分大小写的。
- 若没有找到指定 ID 的元素，返回 null。
- 若一个父节点下面有多个相同 ID 元素时，默认选取第一个(而不是层级最高的)。

2. ##### getElementByTagName()

   **获取指定标签的元素。**

   - 参数：name 名称。
   - 返回值：符合条件的元伪素数组。若没有找到符合条件的，返回空数组。
   - getElementsByTagName()方法返回元素的顺序是它们在文档中的顺序。
   - 返回值有没有获取到元素，都是一个伪数组，即便元素只有一个。
   - 传递给getElementsByTagName()方法的字符串可以不区分大小写。
   - 如果把特殊字符串 “*” 传递给getElementsByTagName()方法，它将返回文档中所有元素的列表，元素排列的顺序就是它们在文档中的顺序。

   ##### 3.getElementsByClassName()

   **获取所有指定类名的元素。**

   - 参数：class 名称。
   - 返回值：符合条件的元素伪数组。若没有找到符合条件的，返回空数组。
   - getElementsByClassName( )方法在几个重要的浏览器中支持的最低版本

   4. ##### getElementsByTagName()

   **通过标签名获取元素。**

   - 参数：标签名称。如：div、a 等等
   - 返回值：符合条件的元素伪数组。若没有找到符合条件的，返回空数组。
   - 返回值有没有获取到元素，都是一个伪数组，即便元素只有一个

   5. ##### querySelector()

   **根据选择器获取一个元素。**

   - 参数：选择器
   - 返回值：一个元素。

   6.querySelectorAll()

   **根据选择器获取全部元素。**

   - 参数：选择器
   - 返回值：符合条件的元素伪数组。若没有找到符合条件的，返回空数组。

### nodelist

```js
        var  forms=document.getElementById("form0");
        console.log(forms)
        var list=forms.getElementsByName("sex");
        console.log(list);
        var list=document.getElementsByName("sex");
        list.forEach(function(item){
            console.log(item);
        })
```

### 节点遍历

```js
console.log(document.body.children);//所有子元素的列表
console.log(document.body.childNodes);//所有子节点列表
console.log(document.body.firstChild);//第一个子节点
console.log(document.body.firstElementChild);//第一个子元素
console.log(document.body.lastChild);//最后一个子节点
console.log(document.body.lastElementChild);//最后一个子元素
console.log(document.body.lastElementChild.previousSibling);//上一个兄弟节点
console.log(document.body.lastElementChild.previousElementSibling);//上一个兄弟元素
console.log(document.body.firstElementChild.nextSibling);//下一个兄弟节点
console.log(document.body.firstElementChild.nextElementSibling);//下一个兄弟元素
console.log(document.body.firstChild.parentNode);//父节点
console.log(document.body.firstChild.parentElement);//父元素
```

## dmo的创建

创建新的Element节点可以使用Document对象的creatElement()方法，给方法传递元素的标签名：对HTML文件来说该名字不区分大小写，对XML文档则区分大小写。

createTextNode()  **创建文本节点** 

appendChild() 追加新子节点



```js
var script=document.createElement("script");
var img=document.createElement("img");
var table=document.createElement("table");
```

### 碎片容器

 createDocumentFragment

var elem=document. createDocumentFragment( )

1. createDocumentFragment()`方法，是用来创建一个虚拟的节点对象，或者说，是用来创建文档碎片节点。它可以包含各种类型的节点，在创建之初是空的。
2. `DocumentFragment`节点不属于文档树，继承的`parentNode`属性总是null。它有一个很实用的特点，当请求把一个`DocumentFragment`节点插入文档树时，插入的不是`DocumentFragment`自身，而是它的所有子孙节点，即插入的是括号里的节点。这个特性使得`DocumentFragment`成了占位符，暂时存放那些一次插入文档的节点。它还有利于实现文档的剪切、复制和粘贴操作。
3. 如果使用`appendChid`方法将原dom树中的节点添加到`DocumentFragment`中时，会删除原来的节点。



- appendChild() 每次追加都会从新打开DOM树 在创建的数量过多时候，效率特别低下
- createDocumentFragment（）会起到优化作用，存在于内存中，并不在DOM树中，所以将子元素插入到文档片段时不会引起页面回流(reflow)(对元素位置和几何上的计算)
- documentFragment 被所有主流浏览器支持
- 最后通过appendChild（）添加

```js
var con=document.createDocumentFragment();


     var ul=document.createElement("ul");
  
    for(var i=0;i<10;i++){
        var li=document.createElement("li");
        li.innerHTML=i;
        ul.appendChild(li);
    }
    document.body.appendChild(ul); 

     var con=document.createDocumentFragment();
    for(var i=0;i<10;i++){
        var div=document.createElement("div");
        con.appendChild(div);
    }
    document.body.appendChild(con); 
```

### DOM插入复制和删除替换

#### DMO插入

使用appendChild()或insertBefore()插入。

appendChild()是在需要插入的Element节点上调用的，它插入的节点使其成为那个节点的最后一个子节点

```js
document.body.appendChild(div);
```

insertBefore()两个参数，第一个参数是待插入的节点，第二个参数是已存在的节点，新节点插在该节点的前面，如果使用null作为第二个参数，将节点插入在最后。

```js
document.body.insertBefore(div,document.body.firstChild)

var span=document.createElement("span");
var div0=document.querySelector("#div0");
div0.appendChild(span);// 插入在子元素的最尾部
div0.insertBefore(span,div0.firstChild); // 插入在子元素的最前面
div0.parentElement.insertBefore(span,div0);// 插入在元素的兄弟项前面
div0.parentElement.insertBefore(span,div0.nextSibling);// 插入在元素的兄弟项后面
// 给指定元素列表中的内容增加外容器
         function warp(elemType,newType){
            var elems=document.querySelectorAll(elemType);
            elems.forEach(function(item){
                var parent=document.createElement(newType);
                item.parentElement.insertBefore(parent,item);
                parent.appendChild(item);
            })
        }
        warp("span","div");
//给span添加外容器
         function warpAll(elemType,newType){
            var elems=document.querySelectorAll(elemType);
            if(elems.length===0) return;
            var parent=document.createElement(newType);
            elems[0].parentElement.insertBefore(parent,elems[0]);
            elems.forEach(function(item){
                parent.appendChild(item);
            })
        }
        warpAll("span","div");

// 创建文本节点
        var txt=document.createTextNode("你好");
        div0.insertBefore(txt,div0.firstElementChild);


```

#### DOM替换删除

```js
 var p=document.createElement("p");
 // 父容器.replaceChild(新的子元素，要替换掉旧元素);
 div0.replaceChild(p,div0.firstElementChild);


// 删除节点
// 父容器.removeChild(子元素);

// 子元素.remove()
// 在删除时，元素仅仅是从页面中删除，不是从内存删除
div0.addEventListener("click",clickhandler);
function clickhandler(){
console.log("aaa");
} 
div0.remove();
div0=null;//需要在设值null之前将事件也需要删除
document.body.appendChild(div0);
// 如果在没有清楚内存的情况下还可以加入回去
```

#### DOM复制

```js
// 复制  复制元素=复制目标.cloneNode(深浅复制) 
        // true  深复制  复制元素和元素的所有子元素和节点
        // false  浅复制 仅复制当前元素
            var span1=document.querySelector("#span1");
            var span2=span1.cloneNode(true);
            // 复制标签时，会标签的属性一起复制
            span2.id="span2";
            div0.appendChild(span2);
```

### DOM属性

#### 对象属性

​			DOM的对象属性分为自定义型和原DOM对象属性，DOM的对象原属性与DOM对象的标签属性部分对应，部分有差别

#### 标签属性

 			DOM的标签属性是用来设置标签的属性和值，值和属性都必须是字符类型，DOM的标签属性命名，不能使用大小写区分不适用下划线划分，属性名必须全小写字母，并且使用-区分每个单词

```js
// 获取标签属性
console.log(div.getAttribute("shop-data"));
console.log(div.getAttribute("class"));
// 删除标签属性
div.removeAttribute("shop-data");
document.URL   //当前页面地址
document.domain  //域名
```

#### DOM对象和属性

-  分为自定义属性和原Dom属性

- 查看原有的对象属性，例如：console.dir(div);Dom

- 对象的原属性与Dom 对象标签属性，部分对应每个标签的属性都是不一样的  例如 input中有name,checked,placeholder其他属性都没有

- 对象可以添加自定义属性  例如  div.aa=234  console.log(div.aa) 打印234 

#### DOM常见内置属性

| 编号 | DOM常用属性               | 简介            |
| ---- | ------------------------- | --------------- |
| 1    | document. body            | 获取 body       |
| 2    | document. documentElement | 获取 html       |
| 3    | document.head             | 获取 head       |
| 4    | document.title            | 获取 title      |
| 5    | document.styleSheets      | 获取css样式对象 |
| 6    | document.URL              | 获得完整的URL   |
| 7    | document.domain           | 获取域名        |

###### 添加class样式

```js
div0.className="div1";
div0.className+=" div2";
 div0.className=div0.className.replace("div1","");
// 如果DOM的行内样式有内容，可以通过这个方式获取对于的行内样式
// 如果DOM的样式在CSS中，这时候还没有渲染所以无法计算CSS的样式，这种style获取是不能获得CSS样式的
// 想要获取计算后样式，就需要使用getComputedStyle获取元素的样式
console.log(getComputedStyle(div0).width);//不支持IE8及以下
console.log(div0.currentStyle.width);
```

#### DOM对象的常见属性

DOM的宽高

```js
clientWidth  clientHeight   //客户宽高     计算后宽高=宽高+padding-(如果有滚动条，减去滚动条宽高)
offsetWidth  offsetHeight   //偏移宽高    计算后宽高=宽高+padding+border
scrollWidth  scrollHeight   //滚动内容宽高   如果没有超出 等同于clientWidth和clientHeight
                            //如果超出就是实际内容所占的宽高，但是padding没有右侧和下侧
                   //如果超出就是实际内容所占的宽高，但是padding没有右侧和下侧-(如果有滚动条，减去滚动条宽高)
```

```js
console.log(document.body.clientWidth,document.body.clientHeight);//实际body的宽度和高度-滚动条宽高
console.log(document.body.offsetWidth,document.body.offsetHeight);//实际body的宽度和高度-滚动条宽高
console.log(document.body.scrollWidth,document.body.scrollHeight);//实际body中内容的宽高

            console.log(document.documentElement.clientWidth,document.documentElement.clientHeight);//当前文档的可视宽高-(如果有滚动条，减去滚动条宽高)
            console.log(document.documentElement.offsetWidth,document.documentElement.offsetHeight);//当前文档的内容宽高-(如果有滚动条，减去滚动条宽高)
            console.log(document.documentElement.scrollWidth,document.documentElement.scrollHeight);//当前文档的可视宽高。如果有滚动条，就是实际body撑开的宽高     
```

dom的位置

```js
 // clientLeft  clientTop   客户位置
 // offsetLeft  offsetTop    偏移位置
 // scrollLeft  scrollTop    滚动条位置
 
 var div2=document.querySelector(".div2");
div2.addEventListener("scroll",scrollHandler);
 console.log(div2.clientLeft,div2.clientTop);//边线的宽高
 console.log(div2.offsetLeft,div2.offsetTop);//当前div到父容器左上角的距离（父容器是定位），
                                             // 它和position的left和top是相同的
console.log(div2.scrollLeft,div2.scrollTop);//当前元素的滚动条位置
        //  前面的这些属性都是只读，但是这个是可以修改的
div2.scrollLeft=100;//滚动条位置设置
var rect=div2.getBoundingClientRect();
console.log(rect);
rect.x===rect.left;
rect.y===rect.top;  // 当前元素到可视窗口左上角的位置
  // html和body的clientLeft ,offsetLeft 不考虑
document.body.scrollTop=100;
// 页面中的滚动是html的scrollTop和scrollLeft控制
// 早期的浏览器是body控制
document.documentElement.scrollTop=200;
```

### this的指向问题

情况一：如果一个函数中由this，但是他没有被上一级对象所调用，那么this指向的是undefined，

情况二：如果一个函数中有this，这个函数有被上一级所调用，那么this指向的就是上一级对象

情况三：如果一个函数中有this，这个函数包含多个对象，尽管这个函数是被最外层的对象所调用，this指向的也只是它上一级的对象

new操作符会改变this的指向

当this遇见return时，如果返回值是一个对象，那么this指向的就是那个返回的对象，如果返回值是一个对象那么this还是指向函数的实例