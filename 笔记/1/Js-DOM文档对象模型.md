# Ⅰ- 壹 - DOM文档对象模型

> 1.    DOM ( Document Object Model ) 文档对象模型, 是W3C组织推荐的一套操作网页元素的应用程序接口(API)。

>  2. document是DOM的核心对象，HTML DOM 定义了访问和操作HTML文档的标准方法

> 3.  我们可以通过JavaScript操作DOM，可以对节点实现增删改查操作，可以动态添加标签，属性等。

## 元素的继承树
 所有的标签都是DOM元素 是Object类型



> Object–>EventTarget–>Node–>Element–>HTMLElement–>HTMLDivElement

> //div的继承树 //
> Object-->EventTarget-->Node-->Element-->HTMLElement-->HTMLDivElement

> //a的继承树 //
> Object-->EventTarget-->Node-->Element-->HTMLElement-->HTMLAnchorElement

> //span的继承树 //
> Object-->EventTarget-->Node-->Element-->HTMLElement-->HTMLSpanElement

> //ul的继承树 //
> Object-->EventTarget-->Node-->Element-->HTMLElement-->HTMLUListElement

> //li的继承树 //
> Object-->EventTarget-->Node-->Element-->HTMLElement-->HTMLLIElement

>      ..........................

# Ⅱ - 贰 -DOM 节点

> HTML 文档中的每个成分都是一个节点，如：HTML 里整个文档、每个标签、每个标签的属性和文本都可作为一个节点。

##  一 节点分类与层次关系
### 1 节点分类

① 文档节点(Document)：整个 XML、HTML 文档

② 元素节点(Element)：每个 XML、HTML 元素

③ 属性节点(Attr)：每个 XML、HTML 元素的属性

④ 文本节点(Text)：每个 XML、HTML 元素内的文本

⑤ 注释节点(Comment)：每个注释

### 2 层次关系
**节点层次关系-节点彼此都有等级关系.**
**节点彼此都有等级关系：父节点、兄弟节点、子节点等等。** 
HTML 文档中的所有节点组成了一个文档树（或节点树）。HTML 文档中的每个元素、属性、文本等都代表着树中的一个节点。树起始于文档节点，并由此继续伸出枝条，直到处于这棵树最低级别的所有文本节点为止。
<head> 和 <body> 的父节点是 <html> 节点。

当节点分享同一个父节点时，它们就是同辈（同级节点）。

节点也可以拥有后代，后代指某个节点的所有子节点，或者这些子节点的子节点。

节点也可以拥有先辈。先辈是某个节点的父节点，或者父节点的父节点，以此类推。比方说，所有的文本节点都可把 <html> 节点作为先辈节点。

**HTML DOM 模型被构造为对象的树**
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200630160643571.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

## 二 DOM 节点属性
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200630161236420.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

### 1 标签的内容属性
##### （1）innerHTML
**以 HTML 代码格式获取或设置节点的内容**

获取标签内容的时候，不管标签还是文本，都能获取到 
innerHTML设置内容的时候，覆盖原来内容，标签也能生效，浏览器能解析这个标签
##### （2）innerText
**获取或设置节点的文本内容**

获取标签内容的时候，只会获取文本，标签扔掉了 设置标签内容的时候，覆盖原来内容，对标签进行转义（目的：把标签直接当文本来用）

**兼容性**

innerText是 IE 提出来的属性，因此低版本的火狐浏览器不支持这个属性。
火狐有一个textContent属性，效果跟innerText一样，但是 IE678 不支持这个属性
innerText 的兼容性代码:

```javascript
function getInnerText(element){
  if(typeof element.innerText === "string"){
    return element.innerText;
  } else {
    return element.textContent;
  }
}
```

##### （3）区别
**共同点** : 都是用来获取和设置标签的内容的
**区别** : 

- innerHTML可以用于获取和设置标签的所有内容，包括标签和文本内容
- innerText只识别文本，标签会被转义。（可以防止 xss 攻击）


## 三 节点的属性
**分别是 nodeName（节点名称）nodeValue（节点值）nodeType（节点类型）**


#### 1 nodeName（节点名称）
**获取节点名称，只读属性** 
- **各个节点的返回值**

| 节点类型           | nodeName          |
| ------------------ | ----------------- |
| 文档节点(Document) | 返回 #document    |
| 元素节点(Element)  | 返回 大写元素名称 |
| 属性节点(Attr)     | 返回 属性名称     |
| 文本节点(Text)     | 返回 #text        |

- **示例：**

```javascript
console.log( document.nodeName ); // => #document：文档节点
console.log( document.body.nodeName ); // => BODY：元素节点

// => DIV：元素节点
console.log( document.getElementById('div').nodeName ); 

// => style：属性节点
console.log( document.getElementById('div').attributes.style.nodeName ); 
```



#### 2 nodeValue（节点值）
**获取或设置节点的值**

- **各个节点的返回值**
说明：文档节点、元素节点此属性返回 null，并且为只读。

| 节点类型           | nodeType           |
| ------------------ | ------------------ |
| 节点类型           | nodeValue          |
| 文档节点(Document) | 只读，返回 null    |
| 元素节点(Element)  | 只读，返回 null    |
| 属性节点(Attr)     | 获取或设置属性的值 |
| 文本节点(Text)     | 获取或设置文本的值 |


- **示例：**

```javascript
<div style="width:200px;height:100px;border:1px solid black" id="div">
<span>文本1</span>
文本2
</div>
console.log( document.nodeValue ); // => null：文档节点

console.log( document.body.nodeValue ); // => null：元素节点

console.log( document.getElementById('div').nodeValue ); // => null：元素节点

// => width:200px;height:100px;border:1px solid black;：style属性的值
console.log( document.getElementById('div').attributes.style.nodeValue ); 

// 设置style属性的值
document.getElementById('div').attributes.style.nodeValue = ' width:200px;height:200px'; 
```





####  3 nodeType（节点类型）
**返回节点类型，只读属性**
- **各个节点的返回值**


| 节点类型           | nodeType |
| ------------------ | -------- |
| 文档节点(Document) | 9        |
| 元素节点(Element)	| 1
| 属性节点(Attr)	| 2| 
| 文本节点(Text)	| 3| 


- **示例：**

```javascript
console.log( document.nodeType ); // => 9：文档节点
console.log( document.body.nodeType ); // => 1：元素节点
console.log( document.getElementById('div').nodeType ); // => 1：元素节点
console.log( document.getElementById('div').attributes.style.nodeType ); // => 2：属性节点
```

## 四 获取元素的方法

| 编号 | 方法                              | 简述                     |
| ---- | --------------------------------- | ------------------------ |
| 1    | document.getElementById()         | 获取指定 ID 的元素。     |
| 2    | document.getElementByTagName()    | 获取指定标签的元素。     |
| 3    | document.getElementsByClassName() | 获取所有指定类名的元素。 |
| 4    | document. getElementsByTagName()  | 通过标签名获取元素。     |
| 5    | document.  querySelector()        | 根据选择器获取一个元素。 |
| 6    | document. querySelectorAll()      | 根据选择器获取全部元素。 |



#### 1 getElementById()

**获取指定 ID 的元素。**

- 参数：元素 ID。

- 返回值：元素节点对象。若没有找到，返回 null。

**示例：**

```javascript
document.getElementById()
//功能：通过id 获取元素
document : 文档对象
get : 得到
element:元素
by:通过
id:id值
// 参数 : 字符串类型的id
//返回值 : 一个元素 一个对象
var div = document.getElementById('div');
console.dir(div);
```

**注意：**

- HTML 元素 ID 是区分大小写的。

- 若没有找到指定 ID 的元素，返回 null。

- 若一个父节点下面有多个相同 ID 元素时，默认选取第一个(而不是层级最高的)。

#### 2 getElementByTagName()

**获取指定标签的元素。**

- 参数：name 名称。

- 返回值：符合条件的元伪素数组。若没有找到符合条件的，返回空数组。

**示例：**

```javascript
var ps = document.getElementsByTagName('p');
```

**注意：**

-  getElementsByTagName()方法返回元素的顺序是它们在文档中的顺序。

-  返回值有没有获取到元素，都是一个伪数组，即便元素只有一个。

-  传递给getElementsByTagName()方法的字符串可以不区分大小写。

-  如果把特殊字符串 “*” 传递给getElementsByTagName()方法，它将返回文档中所有元素的列表，元素排列的顺序就是它们在文档中的顺序。

#### 3 getElementsByClassName()

**获取所有指定类名的元素。**

- 参数：class 名称。

- 返回值：符合条件的元素伪数组。若没有找到符合条件的，返回空数组。

示例：

```javascript
// 返回一个class包含show的元素数组
var show = document.getElementsByClassName('show'); 
```

**注意**：

- getElementsByClassName( )方法在几个重要的浏览器中支持的最低版本

#### 4 getElementsByTagName()

**通过标签名获取元素。**

- 参数：标签名称。如：div、a 等等

- 返回值：符合条件的元素伪数组。若没有找到符合条件的，返回空数组。

**示例：**

```javascript
document.getElementsByTagName('div'); // 返回一个标签为div的元素数组
```

**注意：**

- 返回值有没有获取到元素，都是一个伪数组，即便元素只有一个

#### 5 querySelector()

**根据选择器获取一个元素。**

- 参数：选择器
- 返回值：一个元素。

**示例：**

**var li = document.querySelector('.u1 li');**

#### 6 querySelectorAll()

**根据选择器获取全部元素。**

- 参数：选择器
- 返回值：符合条件的元素伪数组。若没有找到符合条件的，返回空数组。

**示例：**

```javascript
var lis = document.querySelectorAll('.u1 li');
```

## 五 节点的操作
### 1 节点查找/节点遍历
| 编号 | 节点方法                        | 简述                       |
| ---- | ------------------------------- | -------------------------- |
| 1    | document.childNodes             | 获取所有子节点（包括注释） |
| 2    | document.children               | 获取所有子元素             |
| 3    | document.parentElement          | 获取已知节点的父元素       |
| 4    | document.parentNode             | 获取已知节点的父节点       |
| 5    | document.firstElementChild      | 第一个子元素               |
| 6    | document.firstChild             | 第一个子节点               |
| 7    | document.lastElementChild       | 最后一个子元素             |
| 8    | document.lastChild              | 最后一个子节点             |
| 9    | document.nextElementSibling     | 下一个兄弟元素             |
| 10   | document.nextSibling            | 下一个兄弟节点             |
| 11   | document.previousElementSibling | 上一个兄弟元素             |
| 12   | document.previousSibling        | 上一个兄弟节点             |


#### （1）找子节点/元素

```javascript
// 找孩子
var ul = document.querySelector('ul');

//1. childNodes 获取所有的子节点
console.log(ul.childNodes);

//2. children 获取所有的子元素
onsole.log(ul.children);

//3. firstChild  第一个子节点
console.log(ul.firstChild);

//4. firstElementChild  第一个子元素
console.log(ul.firstElementChild);

//5. lastChild 最后一个子节点
console.log(ul.lastChild);

//6. lastElementChild 最后一个子元素
console.log(ul.lastElementChild);

//7. children[2]  任意一个
console.log(ul.children[2]);
```

#### （2）找兄弟节点/元素

```javascript
// 找兄弟 sibling 兄弟姊妹
var l2 = document.querySelector('.l');

//1. nextSibling  下一个兄弟节点
console.log(l2.nextSibling);

//2. nextElementSibling 下一个兄弟元素
console.log(l2.nextElementSibling);

//3. previousSibling 上一个兄弟节点
// previous 上一个
console.log(l2.previousSibling);

//4. previousElementSibling 上一个兄弟元素
console.log(l2.previousElementSibling);
```

#### （3）找父节点/元素

```javascript
// 找父亲
//1. parentElement 父元素 ie9+
console.log( son.parentElement);

//2. parentNode   父节点  (下面的 ) ie6789+
console.log(son.parentNode);
```


### 2 节点的创建和插入
#### （1） createElement() **创建元素节点**
**创建一个元素节点（具体的一个元素）**
结构 : var element = document.createElement(‘标签名’)；

#### （2） createTextNode()  **创建文本节点** 
**创建一个文本节点** 
结构 ：var element = document.createTextNode(“文本”);

#### （3）appendChild() 追加新子节点



**在指定节点的最后一个子节点列表之后添加一个新的子节点，（向元素末尾插入一个元素）**

- 结构 : 父元素.appendChild(子元素)

**示例：**

```javascript
<ul>
    <li class="l1">1</li>
    <li class="l2">2</li>
    <li class="l3">3</li>
</ul>
<hr>
<p>哈哈</p>

var ul = document.querySelector('ul');
var p = document.querySelector('p');
// 添加
ul.appendChild(p);//将p追加到ul里面的最后面
```

注意点：
1. 如果要添加的子元素在网页中本来就存在, appendChild 就相当于一个剪切
2. 会添加到所有子元素的最后面
3. innerHTML会覆盖之前的内容 ，而appendChild不会

###### **碎片容器 ** createDocumentFragment

var elem=document. createDocumentFragment( )

1. createDocumentFragment()`方法，是用来创建一个虚拟的节点对象，或者说，是用来创建文档碎片节点。它可以包含各种类型的节点，在创建之初是空的。

2. `DocumentFragment`节点不属于文档树，继承的`parentNode`属性总是null。它有一个很实用的特点，当请求把一个`DocumentFragment`节点插入文档树时，插入的不是`DocumentFragment`自身，而是它的所有子孙节点，即插入的是括号里的节点。这个特性使得`DocumentFragment`成了占位符，暂时存放那些一次插入文档的节点。它还有利于实现文档的剪切、复制和粘贴操作。
3. 如果使用`appendChid`方法将原dom树中的节点添加到`DocumentFragment`中时，会删除原来的节点。



- appendChild() 每次追加都会从新打开DOM树 在创建的数量过多时候，效率特别低下
- createDocumentFragment（）会起到优化作用，存在于内存中，并不在DOM树中，所以将子元素插入到文档片段时不会引起页面回流(reflow)(对元素位置和几何上的计算)
-  documentFragment 被所有主流浏览器支持
- 最后通过appendChild（）添加

```javascript
var ul = document.getElementById("ul");
var fragment = document.createDocumentFragment();
for (var i = 0; i < 20; i++) {
    var li = document.createElement("li");
    li.innerHTML = "index: " + i;
    fragment.appendChild(li);
}
ul.appendChild(fragment);

```

取自：[https://blog.csdn.net/weixin_43606809/article/details/97916174?ops_request_misc=%257B%2522request%255Fid%2522%253A%2522159479952719195265904194%2522%252C%2522scm%2522%253A%252220140713.130102334..%2522%257D&request_id=159479952719195265904194&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v3~pc_rank_v3-1-97916174.pc_ecpm_v3_pc_rank_v3&utm_term=createDocumentFragment](https://blog.csdn.net/weixin_43606809/article/details/97916174?ops_request_misc=%7B%22request%5Fid%22%3A%22159479952719195265904194%22%2C%22scm%22%3A%2220140713.130102334..%22%7D&request_id=159479952719195265904194&biz_id=0&utm_medium=distribute.pc_search_result.none-task-blog-2~all~first_rank_ecpm_v3~pc_rank_v3-1-97916174.pc_ecpm_v3_pc_rank_v3&utm_term=createDocumentFragment)

#### （4）insertBefore() 之前插入新子节点
**在已有的子节点前插入一个新的子节点。**

- 结构： 父级节点.insertBefore( 要插入的节点，指定节点 )

**示例：**

```javascript
var ul = document.querySelector('ul');
var l1 = document.querySelector('.l1');
var l2 = document.querySelector('.l2');
var l3 = document.querySelector('.l3');
var p = document.querySelector('p');

ul.insertBefore(p,l3);//把p插入到l3之前
ul.insertBefore(p,null);//把p添加到最后
ul.insertBefore(p,ul.children[0]);//添加到子元素最前面  (不获取l1)
ul.insertBefore(p,l2.nextElementSibling)//添加到l2之后,不获取l3的情况下
```



### 3 节点的替换replaceChild ()
**替换节点**

- 结构 : 父元素.replaceChild(newChild, oldChild) 
- 参数：
newChild：必须。你要插入的节点对象。
oldChild：必须。你要移除的节点对象。

```javascript


//将div1替换div2
var replaceChild = document.body.replaceChild(div1,div2);
```

### 4 节点的删除removeChild()和remove()

- 在页面中删掉事件还会存在
- 需要在设置null之前，将事件也需要删除

###### （1）removeChild()

**从子节点列表中删除某个节点。**

- 结构：父容器.removeChild(删除的子元素)
- 返回值：返回被删除的节点，如失败，则返回 NULL。
- 父容器删除子元素

**示例：**

```javascript

// 方式1 :  父元素.removeChild(子元素)
father.removeChild(son);

// 方式2 :  子元素.parentNode.removeChild(子元素)
son.parentNode.removeChild(son);


```



###### （2）remove()

**从子节点列表中删除某个节点。**

- 结构：需要删除的元素.remove();

  

**示例：**

```javascript

需要删除的元素.remove();

elem.removeChild();
elem=null
removeEventListener(事件名)

```





### 5 节点的克隆cloneNode()

**克隆节点 (复制 拷贝)**

结构 :

- 节点.cloneNode(isdeep)

- 参数：isdeep(Boolean)

  true : 深拷贝，克隆节点及其属性，以及后代
  false : 浅拷贝(默认)，只克隆节点及其后代

- 返回值：返回一个克隆之后的节点

- 在克隆的标签有id时候必须修改，因为会将标签属性一起复制

**示例：**

```javascript
  <div class="father">
    <div class="son">
      <div class="sun"></div>
    </div>
  </div>

var father = document.querySelector('.father');

// 浅拷贝:只拷贝自己的一层 (内容没有拷贝)
var newFather = father.cloneNode(false);

// 深拷贝:更深入一层的拷贝, 内容全部拷贝  (整体拷贝)
// 深拷贝最常用
var newFather1 = father.cloneNode(true);

// 默认值:默认是false（浅拷贝）
var newFather2 = father.cloneNode();
```
```javascript
var lis = document.querySelectorAll('.u1 li');
```

# Ⅲ - 叁 -DOM 属性和DOM对象



- 分为自定义属性和原Dom属性

- 查看原有的对象属性，例如：console.dir(div);

- Dom对象的原属性与Dom 对象标签属性，部分对应
- 每个标签的属性都是不一样的  例如 input中有name,checked,placeholder其他属性都没有
- 对象可以添加自定义属性  例如  div.aa=234  console.log(div.aa) 打印234 

## 一 DOM 常见内置属性



| 编号 | DOM常用属性               | 简介            |
| ---- | ------------------------- | --------------- |
| 1    | document. body            | 获取 body       |
| 2    | document. documentElement | 获取 html       |
| 3    | document.head             | 获取 head       |
| 4    | document.title            | 获取 title      |
| 5    | document.styleSheets      | 获取css样式对象 |
| 6    | document.URL              | 获得完整的URL   |
| 7    | document.domain           | 获取域名        |

```javascript

console.log(document.body);//body标签
console.log(document.title);//title标签
console.log(document.head);//head标签
console.log(document.styleSheets);//css样式对象
console.log(document.URL);//当前地址
console.log(document.domain);//当前域
```







## 二 DOM操作节点的标签属性
| 编号 | DOM操作节点的属性     | 简介                                 |
| ---- | --------------------- | ------------------------------------ |
| 1    | getAttribute(属性)    | 获取节点上的属性，获取标签的属性     |
| 2    | setAttribute(属性,值) | 给节点创建一个新属性，设置标签的属性 |
| 3    | removeAttribute(属性) | 删除节点上的属性                     |
**自定标签属性时**

1. 命名单词之间使用-连接，不适用使用下划线区分

2. 标签属性值必须是字符串 ，都是小写

3. 不区分大小写





```javascript
var div=document.querySelector("div");

//获取标签属性  属性值都是字符串
div.getAttribute("name");

//自定标签属性时，1、命名单词之间使用-连接,2、标签属性值必须是字符串
div.setAttribute("toggle-data","30");

//删除标签属性
div.removeAttribute("toggle-data");
```



## 三 DOM对象的样式（HTML DOM Style 对象）


#### 1 设置DOM对象的样式
[所有的样式对象](https://www.w3school.com.cn/jsref/dom_obj_style.asp)： https://www.w3school.com.cn/jsref/dom_obj_style.asp 

**行内样式通过dom.style…来获取和设置，不能获取CSS中的样式
需要注意，如果样式属性中有 ”-“ 连接符，需要将连接符省略，后面的第一个字母用大写。**
**例：**

```javascript
var div=document.getElementById("div");
//设置行内样式
div.style.backgorundColor="red";
// 获取行内样式，不能获取CSS样式
console.log(div.style.backgroundColor)
```


#### 2 获取计算后的DOM样式
**计算后样式，即CSS样式和行内样式合并计算后的样式**，
- 非IE所支持的获取非行间样式的方法：
用法：getComputedStyle(对象，伪类).样式名
例：getComputedStyle(oDiv,null).color
- IE所支持的获取非行间样式的方法
用法：对象.currentStyle.样式名
例：oDiv.currentStyle.width

```javascript
var div=document.getElementById("div");
//仅适用于IE浏览器
console.log(div.currentStyle.width)
//IE8以下不支持，谷歌火狐支持
console.log(getComputedStyle(div).width);

//可以合并写为
var style=getComputedStyle(div) || div.currentStyle;
```


#### 3 利用Object.assign（） 设置样式



复制对象浅复制，无引用关系

```javascript
Object.assign(元素.style,{

	样式

})
```

#### 4 styleSheets  获取Css样式  style标签内

document.styleSheets[0]

## 四 DOM常用属性

#### 1 DOM元素、HTML、body宽高

[详见](https://blog.csdn.net/Charissa2017/article/details/103837572) ：  https://blog.csdn.net/Charissa2017/article/details/103837572

| 编号 | 对象     | 简介                                                         |
| :--: | -------- | ------------------------------------------------------------ |
|      |          |                                                              |
|  1   | DOM元素  | 即通过DOM获取的元素例，如var elem=document.querySelector("div"); |
|  2   | HTML标签 | document.documentElement                                     |
|  3   | body标签 | document.body                                                |



------

| 对象名                     | 简介                     |
| -------------------------- | ------------------------ |
| clientWidth 、clientHeight | 客户宽高（自身到浏览器） |
| offsetWidth 、offsetHeight | 自身偏移宽高             |
| scrollWidth 、scrollHeight | 滚动内容的宽高           |



###### （1）DOM元素宽高

**自身偏移宽高**

|                   |                                                              |
| ----------------- | ------------------------------------------------------------ |
| 元素.offsetWidth  | 水平方向 width + 左右padding + 左右border-width-(如果有滚动条会减掉) |
| 元素.offsetHeight | 垂直方向 height + 上下padding + 上下border-width-(如果有滚动条会减掉) |

**客户宽高**

|                   |                                                      |
| ----------------- | ---------------------------------------------------- |
| 元素.clientWidth  | 水平方向 width + 左右padding-(如果有滚动条会减掉)    |
| 元素.clientHeight | 垂直方向 height + 上下padding  -(如果有滚动条会减掉) |

**滚动内容的宽高**

|                   |                                                              |
| ----------------- | ------------------------------------------------------------ |
| 元素.scrollWidth  | 元素内容真实的宽度，内容不超出盒子高度时为盒子的clientWidth  |
| 元素.scrollHeight | 元素内容真实的高度，内容不超出盒子高度时为盒子的clientHeight |



###### （2）HTML标签宽高



|                                                              |                                                          |
| ------------------------------------------------------------ | -------------------------------------------------------- |
| document.documentElement.clientWidth、document.documentElement.clientHeight | 当前文档的可视宽高-(如果有滚动条，减去滚动条宽高)        |
| document.documentElement.offsetWidth、document.documentElement.offsetHeight | 当前文档的内容宽高-(如果有滚动条，减去滚动条宽高)        |
| document.documentElement.scrollWidth、document.documentElement.scrollHeight | 当前文档的可视宽高、如果有滚动条，就是实际body撑开的宽高 |

###### （3） body标签宽高

|                                                       |                                 |
| ----------------------------------------------------- | ------------------------------- |
| document.body.clientWidth、document.body.clientHeight | 实际body的宽度和高度-滚动条宽高 |
| document.body.offsetWidth、document.body.offsetHeight | 实际body的宽度和高度-滚动条宽高 |
| document.body.scrollWidth、document.body.scrollHeight | 实际body中内容的宽高            |



#### 2 DOM位置

|                      |                              |
| -------------------- | ---------------------------- |
| clientLeft clientTop | 客户位置                     |
| offsetLeft offsetTop | 自身偏移位置（自身到浏览器） |
| scrollLeft scrollTop | 滚动条位置（可写）           |



###### （1） 元素标签位置

|                                 |                                                              |
| ------------------------------- | ------------------------------------------------------------ |
| 元素.clientLeft、元素.clientTop | 边线的宽高                                                   |
| 元素.offsetLeft、元素.offsetTop | 当前元素到父容器左上角的距离（父容器是定位），它和position的left和top是相同的 |
| 元素.scrollLeft、元素.scrollTop | 当前元素的滚动条位置、（可写）                               |



###### （2） body和HTML位置

body、html中clientLeft ,offsetLeft 不考虑、页面中的滚动是html的scrollTop和scrollLeft控制

HTML可以控制浏览器滚动条的位置 document.documentElement.scrollTop=200;

元素.offsetTop  获取当前元素到 定位父节点 的top方向的距离  元素.offsetLeft  获取当前元素到 定位父节点 的left方向的距离



# 0 - 0 - 知识点：
##### 1 设置CSS样式不可用

```javascript
document.styleSheets[0].disabled=true;
```

##### 2 trim（）去掉字符串的前后空格
##### 3 元素.textContent=内容：给元素添加内容，不能设置HTML

##### 4 元素.className 设置元素类名

