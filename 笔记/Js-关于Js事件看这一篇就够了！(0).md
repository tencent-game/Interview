# Ⅰ- 壹 - 事件对象基础
**1. js事件是事件驱动性语言，可分为系统派发事件，自定义派发事件**
**2. javascript 中系统事件自动抛发。分类有：**

- MouseEvent（鼠标事件）
- InputEvent （input事件）
- KeyboardEvent（键盘事件）
- WheelEvent （滚轮事件）
- Event对象
- FocusEvent对象

**3. 各个事件中具备自身独立的属性，**
比如clientX、clientY只属于mouseEvent；keyCode只属于KeyboardEvent等。
**4. Event称为事件基类，基类的属性是最少的。**

**5. 事件是通知和监听组合完成的，先监听后通知，执行对应的函数**

**6. 只有DOM可以做事件监听**

## 一 事件基础
**事件分为系统派发事件和自定义派发事件。**

> addEventListener();//事件侦听方法，仅用于EventTarget对象
> removeEventListener(type,fn,false);   //这里 fn 必须是原有绑定的函数，否侧解除无效

> dispatchEvent();//抛发事件方法，派发事件，仅用于EventTarget对象


1. 必须要先侦听再派发
2. 侦听和派发的对象是同一个，可以是DOM元素，也可以是EventTarget，或者继承EventTarget的类
3. 侦听和派发的事件类型完全相同，其实事件类型就是一个任意字符串
4. 系统派发的事件字符串是固定的，自定义派发的事件，字符串可以任意
5. 事件侦听回调函数，不能传参,因此事件回调函数中有且仅有一个参数,这个参数即为事件对象
6. 事件都可以手动派发，手动派发的话，页面加载完后就会执行

```javascript

//document就是侦听派发的对象
//click就是这里的事件类型
document.addEventListener("click",clickHandler);

//div元素的继承为下：
//Object-->EventTarget-->Node-->Element-->HTMLElement-->HTMLDivElement

//EventTarget叫事件目标对象
var target=new EventTarget();
target.addEventListener("chilema",clickHandler);//执行创建的事件对象
//Event实例的对象叫事件对象  创建一个事件对象 chilema
var evt=new Event("chilema");
evt.num=10;
target.dispatchEvent(evt);//派发事件
//
function clickHandler(e){
	//e.type为派发的事件类型
   console.log(e.type);
}

```


## 二 事件原理（三个阶段）

-  事件捕获（由外到内）
- 目标阶段
- 事件冒泡（由内到外）

事件冒泡(event bubbling)，即事件开始时由最具体的元素（文档中嵌套层次最深的那个节点）接收，然后逐级向上传播到较为不具体的节点（文档）。即子标签发生事件后,向父级发送该事件,一直追溯到document。如:点击一个嵌套在 body中的button,则该button的onclick事件也会传递给body、document中,触发他们的onclick里触发的函数。

#### 1 理解事件原理：

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701143711910.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

```javascript
var div1 = document.getElementById("div1");
var div2 = document.getElementById("div2");
var div3 = document.getElementById("div3");
div1.addEventListener("click", clickHandler1);
div2.addEventListener("click", clickHandler2);
div3.addEventListener("click", clickHandler3);
function clickHandler1(e) {
    console.log("div1")
}
function clickHandler2(e) {
    console.log("div2")
}
function clickHandler3(e) {
    console.log("div3")
}

```



####  2 目标阶段

- e.currentTarget 是事件侦听事件对象（什么对象执行addEventListener函数就是谁）

- e.target 事件的目标对象 事件实际触发的目标阶段最后对象，

- e.srcElement 事件的目标对象，兼容IE

- 事件函数中this默认等同于e.currentTarget

  

e. target--->e. srcElement--->e. toElement 事件点击的目标对象

e. currentTarget--->事件侦听的对象---->this      在事件监听的时候this指向的就是事件监听的对象

## 三 阻止事件冒泡

当对子元素添加了事件侦听后，执行的时候会触发父元素相同类型的事件，此时需要阻止事件冒泡。
早期IE是没有捕获阶段的，只有冒泡，cancelBubble为阻止冒泡。后来的stopPropagaiton，既有阻止冒泡的功能，也有阻止捕获的功能，但如果译为阻止传播，那么跟cancel就是两个东西了，所以还是叫做阻止冒泡。阻止事件冒泡（传播）的方法是：

- e.stopPropagation();
- e.cancelBubble=true; IE8及以下浏览器


```javascript
var div1 = document.getElementById("div1");
var div2 = document.getElementById("div2");
var div3 = document.getElementById("div3");
div1.addEventListener("click", clickHandler1);
div2.addEventListener("click", clickHandler2);
div3.addEventListener("click", clickHandler3);
function clickHandler1(e) {
	e.stopPropagation();//阻止事件冒泡
	// e.cancelBubble=true;//阻止事件冒泡   IE8一下浏览器
    console.log("div1")
}
function clickHandler2(e) {
    console.log("div2")
}
function clickHandler3(e) {
    console.log("div3")
}

```





## 四 事件委托

事件侦听添加（注册事件）占有内存的，尽量减少事件侦听的数量，将子元素的事件委托给父元素来执行，叫做事件委托。
当删除对象时，一定要将对象上的侦听事件移除，否则会造成内存泄露。




### 1 绑定事件 addEventListener()和事件的清除removeEventListener
- **参数**：addEventListener(事件类型，事件回调函数，是否捕获阶段执行（默认false）||对象{once:true})//是否只执行一次

```javascript
//给body侦听点击事件，冒泡阶段执行
 document.body.addEventListener("click", clickHandler);
 //给body侦听点击事件，捕获阶段执行
 document.body.addEventListener("click", clickHandler,true);
 //给body侦听点击事件，只执行一次
 document.body.addEventListener("click", clickHandler,{once:true});

```

- **事件侦听添加（注册事件）占有内存的，所以当删除对象时，一定要将对象上的侦听事件移除**
- **参数:**   removeEventListener(事件类型,删除事件侦听的回调函数)

```javascript
 document.body.removeEventListener("click", clickHandler);
```

**案例：点击 li ，让其子元素 ul 切换显示。**

**HTML**

```javascript
<ul id="menu">
   <li>北京
        <ul>
            <li>海淀</li>
            <li>昌平
                <ul>
                    <li>沙河</li>
                    <li>回龙观</li>
                    <li>天通苑</li>
                </ul>
            </li>
            <li>朝阳</li>
            <li>东城</li>
        </ul>
    </li>
    <li>河北</li>
    <li>天津</li>
    <li>河南</li>
    <li>山西</li>
</ul>

```
**Js**

```javascript
var menu=document.querySelector("#menu");
//给最外层的ul侦听点击事件
menu.addEventListener("click",clickHandler);

function clickHandler(e){
	//如果点击的不是li标签，直接退出
    if(e.target.constructor!==HTMLLIElement)return;
    //如果点击的li没有子元素，直接退出
    if(!e.target.firstElementChild) return;
    //阻止事件冒泡
    e.stopPropagation();
    //控制li下的ul显示隐藏
    if(!e.target.bool) e.target.firstElementChild.style.display="none";
    else e.target.firstElementChild.style.display="block";
    e.target.bool=!e.target.bool;
}

```

### 2 addEventListener() 和 onclick的区别：

- onclick 不能同时执行两个函数，addEventListener()可以执行两个不同的函数
- 移除事件侦听的方式不同

```javascript
document.onclick=function(){
	document.onclick=null;//移除事件侦听
    console.log("a")
}
//事件会覆盖上面的事件
document.onclick=function(){
    console.log("b");
}

document.addEventListener("click",clickHandler1);
document.addEventListener("click",clickHandler2);
function clickHandler1(e){
	//移除事件侦听
	document.removeEventListener("click",clickHandler1);
    console.log("a");
}
function clickHandler2(e){
   console.log("b")
}

```
- onclick事件匿名函数的不断迭代就会造成回调地狱，而使用事件注册时用的是命名函数就会减少造成回调地狱

```javascript
// 事件匿名函数的不断迭代就会造成回调地狱
document.onclick=function(){
    var bn=document.querySelector("button");
    bn.onclick=function(){
        console.log("aaa");
    }
}

```
- addEventListener可以在捕获阶段和冒泡阶段触发，而onclick只能冒泡阶段触发

```javascript
 document.body.addEventListener("click", clickHandler);//冒泡阶段执行
 document.body.addEventListener("click", clickHandler,true);//捕获阶段执行
```

- onclick支持IE低版本，addEventListener不支持IE8一下，低版本的IE使用 attachEvent 进行事件侦听；使用 detachEvent 移除事件侦听。

```javascript
document.attachEvent("onclick",clickHandler);//IE8及以下使用，其他版本和其他浏览器不支持
function clickHandler(e){
    console.log("aaa");
    document.detachEvent("onclick",clickHandler);//移除事件侦听
}
```
### 3 事件委托和事件区别

  

 1. 如果侦听函数调用（addEventListener被使用），就会在内存中添加存储
 2. 尽量减少事件的侦听，因此就会将事件委托给父容器做侦听，以达到减少事件侦听的存储
 3. e.currentTarget 是事件侦听事件对象（什么对象执行addEventListener函数就是谁）
 4.  e.target 事件的目标对象 事件实际触发的目标阶段最后对象，e.srcElement兼容IE
 5. 事件函数中this默认等同于e.currentTarget

```javascript
  function clickHandler(e){
        // if(e.target.nodeName!=="LI") return;  判断是不是li标签  第一种方法
        //判断是不是li标签  第二种方法
        if(e.target.constructor!==HTMLLIElement) return;
        // console.log(e);
        // e.currentTarget 是事件侦听事件对象（什么对象执行addEventListener函数就是谁）
        // e.target 事件的目标对象 事件实际触发的目标阶段最后对象，e.srcElement兼容IE
        // 事件函数中this默认等同于e.currentTarget
        // console.log(e.currentTarget,e.target,e.srcElement);
        console.log(e.target.textContent);
    }
```



# Ⅱ - 贰 - MouseEvent（鼠标事件）

## 一 MouseEvent的类别
| 事件类别    | 简述     |
| ----------- | -------- |
| mousedown   | 鼠标按下 |
| mouseup     | 鼠标释放 |
| click       | 左键单击 |
| dblclick    | 左键双击 |
| mousemove   | 鼠标移动 |
| mouseover   | 鼠标经过 |
| mouseout    | 鼠标滑出 |
| mouseenter  | 鼠标进入 |
| mouseleave  | 鼠标离开 |
| contextmenu | 右键菜单 |

- 执行顺序：mousedown —> mouseup —> click
- 区别：mouseover和mouseout子元素也会触发，可以冒泡触发
- 区别：mouseenter和mouseleave是针对侦听的对象触发，阻止了冒泡

## 二 阻止鼠标的默认事件
- e.preventDefault()
- e.returnValue=false;//IE8 及以下兼容写法
- return false;//IE兼容写法，只用作on事件阻止默认事件

#### 1.去除单击右键菜单

```javascript
document.body.addEventListener("contextmenu",clickHandler);
function clickHandler(e){
    e.preventDefault();//阻止事件默认行为
    console.log(e.type);
}

```
#### 2 阻止图像默认拖拽

```javascript
var img=document.querySelector("img");
img.addEventListener("mousedown",mouseHandler);
function mouseHandler(e){
    e.preventDefault();
}

```

#### 3 阻止文字的拖拽和选择

```javascript
document.body.addEventListener("mousedown",mouseHandler);
function mouseHandler(e){
    e.preventDefault();
}

```

#### 4 阻止表单提交及重设

```javascript
var bn=document.querySelector("[type=submit]");
bn.addEventListener("click",clickHandler);
function clickHandler(e){
    e.preventDefault();
}

//或者对form来写
var form=document.querySelector("form");
form.addEventListener("submit",submitHandler);
function submitHandler(e){
    e.preventDefault();
    //e.returnValue=false;//IE8 及以下兼容写法
} 


```

## 三 鼠标位置和按键点击
**打印出MouseEvent对象内容：**

```javascript
document.body.addEventListener("mousedown",clickHandler);
function clickHandler(e){
    console.log(e);
}
```

**打印结果如下（只截取了部分内容）：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701153132542.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

- altKey ctrlKey shiftKey metaKey 是否按键点击
- button buttons which用来判断是鼠标的哪个键操作的
左键对应的值为 0、1、1
中键对应的值为 1、4、2
右键对应的值为 2、2、3
- timeStamp 从页面打开开始到触发事件的时间


#### 1 鼠标位置
###### （1）clientX和clientY与x，y
- clientX和clientY与x，y一样的，都是客户区域坐标，指鼠标的坐标，以浏览器显示区域的左上角开始，x,y是新浏览器支持

**以下截图打印的结果都是div2元素的左上顶点（从边框开始）的位置坐标。**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701153342768.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

###### （2）offsetX，offsetY
- offsetX，offsetY 针对目标元素的左上角坐标（e.target）

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701153502809.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)






###### （3）layerX,layerY
- layerX,layerY 往上找有定位属性的父元素的左上角（自身有定位属性的话就是相对于自身），都没有的话，就是相对于body的左上角
- layerX,layerY 如果e.target（目标对象）不是定位元素，这个值就是相对侦听事件对象父容器的左上角，如果定位与offsetX，和offsetY相似

**当元素及它的父级都没有定位属性时，以body的左上角为原点**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701153627857.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)
**当元素的父级都有定位属性时，以父级的左上角为原点：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701153719183.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)
**当元素自身有定位属性时，以自身的左上角为原点：**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701153731194.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)



###### （4）pageX，  pageY
- pageX， pageY相对页面左上角的距离

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701154257467.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)




###### （5） screenX screenY  
-  screenX screenY  相对屏幕左上角的位置

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701154324570.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)


# Ⅲ - 叁 - InputEvent (input事件)、FocusEvent对象 （焦点相关的事件）、KeyboardEvent（键盘事件）

- 通常情况下  这三个事件一起使用

## 一 FocusEvent对象 （焦点相关的事件）
- 主要针对所有表单元素和超链接，当 input 聚焦时触发 focus 事件，失去焦点时触发 blur 事件。

| 事件名称 | 简述     |
| -------- | -------- |
| focus    | 获得焦距 |
| blur     | 失去焦距 |

- 事件对象中 relatedTarget 为上一个失焦对象


```javascript
<input type="text" name="text" id="user">
<script>
var user=document.getElementById("user");
user.addEventListener("focus",focusHandler);
function focusHandler(e){
    // e.relatedTarget  上一个失焦对象
    console.log(e);
}
</script>

```


## 二 InputEvent (input事件)
- 当 input 在输入内容时，就会触发 input 事件。

**事件对象的 inputType 属性的值有：**
| 事件名称              | 简述                     |
| --------------------- | ------------------------ |
| insertCompositionText | 使用输入法的插入文本     |
| historyUndo           | 历史返回                 |
| insertText            | 不用输入法的插入文本     |
| deleteContentBackward | 删除前一个 backspace删除 |
| deleteContentForward  | 删除后一个 delete删除    |
| deleteByCut           | 剪切删除                 |
| insertFromPaste       | 粘贴插入                 |

```javascript
<input type="text" name="text" id="user">
<script>
var user=document.getElementById("user");
user.addEventListener("input",inputHandler);
    function inputHandler(e){
        console.log(e);
        // e.data: "s"  本次输入的内容
        // e.isComposing: false  输入法是否启动
        // e.inputType 输入的类型
        // insertCompositionText 输入插入
        // historyUndo 历史返回
        // insertText  插入文本
        // deleteContentBackward 退格删除（删除前一个）
        // deleteContentForward  delete删除（删除后一个）
        // deleteByCut 剪切删除
        // insertFromPaste 粘贴插入
    }
</script>

```

## 三 KeyboardEvent（键盘事件）
| 事件名称 | 简述                                                         |
| -------- | ------------------------------------------------------------ |
| keyCode  | 属性的值与ASCII码中对应小写字母或数字的编码相同。字母中大小写不影响。 |
| keydown  | 键盘按下时触发，如果键盘一直按下，则会一直触发这个事件       |
| keyup    | 键盘抬起时触发                                               |

- 常用的几个键码：13（回车）、37（左）、38（上）、39（右）、40（下）


```javascript
document.addEventListener("keydown",keyHandler);
document.addEventListener("keyup",keyHandler);
var type="";
function keyHandler(e){
	e.code: "KeyS" // 按下的键
	e.key: "a"  //按下的键
	e.keyCode:// 16 键码   	
	e.which: //65 等同于keyCode
} 

```
keydown表示键盘按下时触发，如果键盘一直按下，则会一直触发这个事件。我们希望当键盘按下后，不管按了多久，都只触发一次keydown事件，可以这么来写：

```javascript
document.addEventListener("keydown",keyHandler);
document.addEventListener("keyup",keyHandler);
var type="";
function keyHandler(e){
	//第一次按下时，type为空，不满足条件，执行下面的代码
	//将当前的e.type赋值给type
	//因为键盘一直是按下状态，所以会一直触发函数，此时type=e.type，所以直接跳出
    if(type===e.type)return;
    type=e.type; 
    console.log(e)
}

```
## 四 节流和防抖
#### 1 节流
**为什么要节流？** 
- 文本框在输入的时候，如果每输入一次就判断一次，会造成效率太低，我们让它每间隔一段时间，再去验证。即指连续触发事件但是在 n 秒中只执行一次函数。


**实现原理**


- 给 input 设置一个属性，第一次触发事件时，属性值为 false，则往下执行，500毫秒后获取 input 的值，同时删除 ids 的值；第二次输入时，当500毫秒还没到时，ids 为 true ，则直接跳出，不去获取 value 值 。在500毫秒中，只执行一次函数。


###### (1) 节流的定时器写法

```javascript
<input type="text" name="text" id="user">
<script>
	init();
	function init(){
	    var user=document.getElementById("user");
	     user.addEventListener("input",inputHandler);
	}
	function inputHandler(e){
	    //判断，如果input.ids为false,则往下执行
	    if(this.ids) return;
	    //500毫秒后，执行showValue函数，同时删除ids的值
	    this.ids=setTimeout(function(elem){
	    	//因为定时器函数会改变this指向，这里将this以参数的形式传进来
	        clearTimeout(elem.ids);
	        elem.ids=null;
	        showValue(elem.value);
	    },500,this);
	}
	//打印出input的值
	function showValue(txt){
	    console.log(txt);
	}
</script>

</script>

```

###### (2) 节流的时间戳写法

```javascript
<input type="text" name="text" id="user">
<script>
	init();	
	function init() {
	    var user = document.getElementById("user");
	    user.addEventListener("input", inputHandler);
	}
	var lastTime=0;
	function inputHandler(e) {
	    //每次触发事件获取当前时间
	   let nowTime=new Date().getTime();
	   //若时间间隔大于500毫秒，则执行代码
	   if(nowTime-lastTime>500){
	       //重新计时
	       lastTime=nowTime;
	       showValue(this.value);
	   }
	}
	//打印出input的值
	function showValue(txt) {
	    console.log(txt);
	}
</script>

```

#### 2 防抖
**什么是防抖？**
- 防抖就是指触发事件后在 n 秒内函数只能执行一次，如果在 n 秒内又触发了事件，则会重新计算函数执行时间。

**为什么要使用防抖？**
- keydown事件，当键盘按下时触发，如果键盘一直按下，则会一直触发这个事件，我们并不希望在事件持续触发的过程中那么频繁地去执行函数。这种情况防抖是比较好的解决方案。


**实现原理**
- 当持续触发keydown事件时，事件处理函数handle只在停止按键500毫秒之后才会调用一次，也就是说在持续触发keydown事件的过程中，事件处理函数handle一直没有执行。

###### (2) 防抖写法

```javascript
<input type="text" name="text" id="user">
<script>
	init();
	function init() {
	    var user = document.getElementById("user");
	    user.addEventListener("input", inputHandler);
	}
	var ids=null;
	function inputHandler(e) {
		//每次输入，把前面的定时器清除，重新开启定时器
	    if(ids !== null) clearTimeout(ids);
	    ids=setTimeout(function(){
	        showValue(this.value);
	    },500)
	}
	//打印出input的值
	function showValue(txt) {
	    console.log(txt);
	}
</script>

```

###### (2) 防抖的封装

```javascript
 function debounce(fn, wait) {
    var timeout = null; //定义一个定时器
    return function () {
        if (timeout !== null)
            clearTimeout(timeout); //清除这个定时器
        timeout = setTimeout(fn, wait);
    }
}
// 处理函数
function handle() {
    console.log(Math.random());
}
// 侦听事件
document.addEventListener("keydown", debounce(handle, 1000));

```
#### 3 防抖和节流的区别
- 防抖是将多次执行变为最后一次执行
- 节流是将多次执行变为每隔一段时间执行


# Ⅳ - 肆 - WheelEvent （滚轮事件）

**滚轮滚动时，会触发滚轮事件，这个事件可以在任何元素上触发，如果不阻止冒泡的话，最终都会冒泡到document对象上面。**

- 在使用滚轮事件时，一般只需要知道是向上或者向下滚动就可以。
- 火狐浏览器使用 DOMMouseScroll
- 其他浏览器使用 mousewheel

火狐浏览器滚轮向下滚动（页面往上）时，e.detail为3；滚轮向上滚动（页面往下）时，e.detail为-3。

chrome浏览器滚轮向下滚动（页面往上）时，e.deltaY为正数；滚轮向上滚动（页面往下）时，e.deltaY为负数。

可以根据这两个值来判断页面是向上还是向下滚动。

案例：当滚轮滚动时，让div随着滚轮滚动的方向移动：

```javascript
document.addEventListener("DOMMouseScroll",mouseHandler);   
document.addEventListener("mousewheel",mouseHandler);   
var div=document.querySelector("div");
function mouseHandler(e){
	var detail;
	if(e.detail!==0)detail=e.detail;
	else detail=e.deltaY<0 ? -3 : 3;
	div.style.top=div.offsetTop+detail+"px";
}
```




# Ⅴ - 伍 - Event对象事件
- Event称为事件基类，基类的属性是最少的。
- Event对象代表事件的状态，比如事件在其中发送的元素、键盘按键的状态、鼠标的位置、鼠标按钮的状态。

## 一 Event事件的类别

| 事件类别 | 简述             |
| -------- | ---------------- |
| change   | 修改事件         |
| submit   | 提交事件         |
| reset    | 重设事件         |
| select   | 选择文字事件     |
| resize   | 重新修改大小事件 |
| scroll   | 滚动条事件       |
| load     | 加载事件         |
| unload   | 卸载事件         |
| error    | 错误事件         |


## 二 事件详解
#### 1 change 修改事件
change 是修改事件，主要用于表单元素，当表单元素被修改时，失去焦点时才会触发事件

input、checkbox、radio都可触发



###### （1）input 的 change 事件：
- 只有当 input 的 value 有修改时，才会触发事件

```javascript
<input type="text" id="user" name="user">
<script>
var user=document.getElementById("user");
user.addEventListener("change",changeHandler);
function changeHandler(e){
	console.log(e);
}
</script>

```
###### （2）select 的 change 事件：

- 当 select 为多选时，可以用下面这两个属性来获取被选中的值

| 属性            | 简述                           |
| --------------- | ------------------------------ |
| selectedIndex   | 下拉菜单被选中的索引值         |
| selectedOptions | 下拉菜单中被选的option标签列表 |

```javascript
<!--multiple 设置select多选-->
<select id="city" name="city" multiple>
    <option>北京</option>
    <option>西安</option>
    <option>上海</option>
</select>
<script>
var city=document.getElementById("city");
city.addEventListener("change",changeHandler);
function changeHandler(e){
	console.log(this.selectedIndex);//获得被选中的索引值
	console.log(this.selectedOptions);//获得被选的option标签列表
}
</script>

```

当 select 为多选时，向后台提交数据，会看到请求数据中 city 被传了两个值，这样传参是不正确的，我们可以在提交表单的时候，将 select 的值合并一下。

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701164511965.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)


去掉 select 的 name 属性，同时在页面中放入一个隐藏的 input，name 为 citySelect，将 select 被选中的值以符号分隔传给 input。

```javascript
<input type="text" name="citySelect" id="citySelect">
<select id="city"  multiple>
    <option>北京</option>
    <option>西安</option>
    <option>上海</option>
</select>
<script>
var city=document.getElementById("city");
var citySelect=document.getElementById("citySelect");
city.addEventListener("change",changeHandler);
function changeHandler(e){
	var selectStr=Array.from(this.selectedOptions).reduce(function(value,item){
								return value+(value.length===0 ? "" :",")+item.textContent;
           				 },"");
	citySelect.value=selectStr;
}

</script>

```

提交表单后，就可以看到数据可以正确传递了
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200701164536824.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)









#### 2 submit 提交事件、reset 重设事件
- submit 和 reset，表单的事件类型，只能作用于form元素
- 当给 form 侦听 submit 事件后，点击 form 里的 button 按钮或者 submit 按钮，都会触发 submit 提交事件。
- 提交submit时,没有name的表单不会被提交
- e. preventDefault() ; 阻止默认事件   页面跳转
```javascript
<form action="#" method="GET">
<input type="text" id="user" name="user">
</form>
<script>
var form=document.querySelector("form");
var user=document.getElementById("user");
form.addEventListener("submit",submitHandler);
form.addEventListener("reset",resetHandler);
function submitHandler(e){
    e. preventDefault() ;阻止默认事件，组阻止提交的时候跳转
	//提交处理
}           
function resetHandler(e){
    e. preventDefault() ;
	//重置
}
</script>
```

#### 3 select 选择文字事件
select 文本选择事件，主要针对于 input 或者 <textArea></texttArea> 中的文本选择，与下拉菜单没有关系，主要是选择文本框中的文本内容时触发事件。

**可以用 input 的以下属性来获取选中的值：**

| 属性               | 简述                                                    |
| ------------------ | ------------------------------------------------------- |
| selectionStart     | 选中值的开始位置下标                                    |
| selectionEnd       | 选中值的结束位置下标                                    |
| selectionDirection | 有两个值：forward为从左到右选择、backward为从右到左选择 |


```javascript
<input type="text" id="user" name="user">
<script>
var user=document.getElementById("user");
user.addEventListener("select",selectHandler);
function selectHandler(e){
    console.log(user.selectionStart);//开始位置的索引
    console.log(user.selectionEnd);//结束位置的索引
    console.log(user.selectionDirection);//选择的方向        
}
</script>

```
**案例：** 将 input 或者 textarea 中选中的小写字母改成大写字母

```javascript
//接上一段代码
function selectHandler(e){
	user.value=user.value.slice(0,user.selectionStart)+user.value.slice(user.selectionStart,user.selectionEnd).toUpperCase()+user.value.slice(user.selectionEnd)
}

```



#### 4 resize 重新修改大小事件
resize 重新修改大小事件，主要针对window事件，作用于window和<textArea></textArea>，窗口被改变大小时事件被触发

**案例：**当窗口改变时，将 html 字体大小成比例缩小：

```javascript
 window.addEventListener("resize",resizeHandler);
function resizeHandler(e){
    var scale=document.documentElement.clientWidth/screen.width;
    document.documentElement.style.fontSize=100*scale+"px";
}
```

#### 5 scroll 滚动条事件
scroll 滚动事件,可以针对任何具备滚动条的容器进行侦听。


**注意：**

- 滚轮滚动不是滚动事件触发的方式，滚轮滚动改变了滚动条的位置，才会触发滚动事件。滚轮滚动属于间接触发滚动条事件
- 只有滚动条位置的改变才能触发滚动事件
- 如果要设置flash中的滚动条不改变外部的滚动条，需要在flash的标签上设置停止冒泡，flash标签有<embed></embed><object></object>
- 当元素滚动，页面滚动条不滚动时，需要设置滚动元素的阻止默认事件

```javascript
document.body.addEventListener("scroll",scrollHandler);
function scrollHandler(e){
	//如果要设置flash中的滚动条不改变外部的滚动条，需要在flash的标签上设置停止冒泡
	e.stopPropagation();
} 

```



#### 6 unload 卸载事件
unload 卸载事件，关闭窗口、原有的页面在刷新时，原有的页面会被卸载掉，这个时候触发事件。

**注意：**

- 关闭当前浏览器标签时被触发，关闭浏览器时不被触发
- e.preventDefault()，不能阻止卸载事件

```javascript
window.addEventListener("unload",unloadhandler);
function unloadhandler(e){
	console.log(e);
}
```



#### 7 load 加载事件和 error 错误事件

- load和error用于图片的加载，

- load用于window加载创建完成，会造成以下情况

  1. 所有的DOM都加载完成
  2. 所有的图片已经加载完成

  

load 加载事件，给window增加load事件，页面中所有的元素被加载完成后触发该事件，包括图片，页面元素过多的话，加载时间会很长，所以不建议这么写


```javascript
 window.onload=function(e){
     console.log(e);
}

var img=new Image();//等同于docmument.createElement(img)   图片加载是异步的
img.addEventListener("load",loadHanlder)


//给window绑定事件
var img=new Image();//等同于docmument.createElement(img)   图片加载是异步的
window.addEventListener("load",loadHanlder)

function loadHanlder(){
    console.log(img)
}
//任何内容没有放在页面中不能调用clientWidth,offsetWidth,scrollWidth这样的数据

```

error 错误事件，比如地址错误造成的加载失败会触发

给 img 添加 src 后，触发 img 的 load 事件。先侦听再派发，所以要把事件侦听写在派发的上面。

```javascript
var img=new Image();
img.addEventListener("load",loadHanlder)
img.addEventListener("error",errorHanlder);
img.src="./img/"+num+"-.jpg";
function loadHanlder(e){
	console.log(e);
}
function errorHanlder(e){
    console.log(e);
}

```

# Ⅵ - 陆 - 番外PopStateEvent对象



当用户在浏览器点击进行后退、前进，或者在js中调用`histroy.back()`，`history.go()`，`history.forward()`等，会触发popstate事件；但pushState、replaceState不会触发这个事件。

- 只有在后退或者前进 触发事件
- e.state可以获取history.pushState第一个参数的值



```javascript
        document.addEventListener("click",clickHandler);
        // PopStateEvent   popstate事件 历史记录被回退和前进时触发
     window.addEventListener("popstate",popstateHandler)
        function clickHandler(e){
            history.pushState({a:1},"","#1");
        }

        function popstateHandler(e){
            console.log(e);
        }
```



# 0 - 0 - 知识点：

#### 一 图片创建  var img=new Image();

等同于docmument.createElement(img)   图片加载是异步的

#### 二 try  catch 错误处理

```javascript
 function addEventListen(elem,type,callback){
            try{
                elem.addEventListener(type,callback)
            }catch(e){
                elem.attachEvent("on"+type,callback);
            }
        }
```















