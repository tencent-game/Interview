# Ⅰ- 壹 - javaScript简述

## 一 javaScript组成：

**DOM属于BOM**

![在这里插入图片描述](https://img-blog.csdnimg.cn/20200707190237526.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

### 1 核心(ECMAScript)

ECMAScript是一个标准 。
因为网景的布兰登(Brendan Eich)开发了JavaScript，为了让JavaScript成为全球标准，几个公司联合ECMA（European Computer Manufacturers Association）组织定制了JavaScript语言的标准，被称为ECMAScript标准。

### 2 文档对象模型(DOM)

Document Object Model。文档对象模型，后边我们会有专门的课程来讲解DOM操作

### 3 浏览器对象模型(BOM)

Browser Object Model。浏览器对象模型，后边我们也会专门来讲bom操作

## 二 JavaScript引入及写法

对于HTML来说从上向下同步解释性文档

### 1 内部书写

在html文件中直接进行代码的书写

body內。head內 。html內

### 2 外部引入

所有的<script>元素都放在页面的<head>元素中。

### 3 直接写在标签内


```javascript
<p onclick="alert('你好');">点击我</p>
```


## 三 JavaScript注意点

#### 1 js语言每行结束时必须使用;结束，必须是半角

#### 2 js代码中大小写必须严格按照规定

#### 3 一般首字母都是小写，除了类。都是用驼峰式命名规则

除了第一个以外，每个单词的首字母大写，其他字母小写
setWorkDay驼峰式

#### 4 alert('弹出内容');     方法一般包括 方法名(参数...).都必须是英文半角

#### 5 一般首字母都是小写，除了类。都是用驼峰式命名规则

除了第一个以外，每个单词的首字母大写，其他字母小写
setWorkDay驼峰式


# Ⅱ - 贰 - Js常用对象

##  一 常用对象

#### 1 常用方法 

**省略了 window.**

###### （1）alert()  警告消息框

###### （2）confirm()    确认消息框

###### （3）prompt()    提示消息框----就是专门用来给用户提供输入窗口的

####  2  常用属性
###### （1）document.write（“value”） 文档中写入字符**
- value:值可以是标签

```javascript
 document.write("<a href='#'>超链接</a>")
```
- value:值可以是数组
```javascript
 document.write("10","20","30"); // 102030
```

###### （2）document.body.innerHTML="value";//赋值，对象的属性需要赋值
- 可以 修改dom元素内容
```javascript

var div0=document.getElementById("div0");
div0.innerHTML="sadasd";
//div0.innerHTML="<div>sadasd</div>";
```
- 可以给body 添加 标签
```javascript
document.body.innerHTML="<div></div>";
```


#  Ⅲ - 叁 - Js数据类型
 数据的分类  字符类型，数值类型，布尔类型，未定义型，空值，对象型
## 一 简单类型与复杂类型(引用类型)
**简单类型又叫做基本数据类型或者值类型,复杂类型又叫做引用类型。**
- 值类型:简单数据类型/基本数据类型,在存储时变量中存储的是值本身,因此叫做值类型
string , number , boolean , undefined , null
- 引用类型: 复杂数据类型,在存储时变量中存储的仅仅是地址(引用) ,因此叫做引用数据类型
通过new关键字创建的对象(系统对象、自定义对象) , 如Object. Array、 Date等

#### 1 基本数据类型

 1. number:常规数字和NaN;
 2. String:字符串类型 用  “”  ''    ES6的``
 3. boolean:布尔类型     true/false
 4. null:空对象指针
 5. undefined：未定义

#### 2  引用数据类型

###### （1）对象数据类型：object
1. {}：普通对象
2. [ ]:数组对象
3. Math：数学函数对象
..........

###### （2） 函数数据类型
1. function
		 


## 二 堆和栈空间
-  栈(操作系统) :由操作系统自动分配释放存放函数的参数值、局部变量的值等。其操作方式类似于数据结构中的栈。简单数据类型存放到栈里面**
-  堆(操作系统) :存储复杂类型(对象) , - -般由程序员分配释放,若程序员不释放,由垃圾回收机制回收。复杂数据类型存放到堆里面


#### 1 简单类型的内存分配

- 值类型 (简单数据类型) : string , number , boolean , undefined , null
- 值类型变量的数据直接存放在变量(栈空间)中
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200629131145381.png)

- 简单类型传参：

函数的形参也可以看做是一个变量 ,当我们把一个值类型变量作为参数传给函数的形参时 ,其实是把变量在栈空间里的值复制了一份给形参,那么在方法内部对形参做任何修改,都不会影响到的外部变量


#### 2 复杂类型的内存分配

- 引用类型(复杂数据类型) : 通过new关键字创建的对象(系统对象、自定义对象) , 如Object. Array. Date等
- 引用类型变量(栈空间)里存放的是地址,真正的对象实例存放在堆空间中


![在这里插入图片描述](https://img-blog.csdnimg.cn/20200629131817114.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)


- 复杂类型传参：

函数的形参也可以看做是一个变量，当我们把引|用类型变量传给形参时,其实是把变量在栈空间里保存的堆地址复制给了形参,形参和实参其实保存的是同一个堆地址,所以操作的是同一个对象。





#  Ⅳ - 肆 - 数据类型的转换

**数值转换分为强制转换和隐式转换两种**



## 一 数值类型与数值类型的转换
>         var num1 = 1;//正整型
>         var num2 = -1;//负整型
>         var num3 = 1.3;//浮点型
>         var num4 = 056;//8进制数值,0起头，数值不能大于7
>         var num5 = 0xFF;//16进制数值，0x起头，单个数值不能大于F
>         var num6 = 1.2e+3;//科学计数法
>         var num7 = 1.2e-3;//科学计数法
#### 1 数值转字符串

```javascript
var a=15.234
```

###### （1） 强制转换 为字符串类型 String（）

```javascript
 var b=String(a);//类型强制转换  
 console.log(b) // 15.234

a=String(a);将a转换为字符串覆盖原有变量a
```
###### （2）隐式转换 

```javascript
 a=a+"";//利用隐式转换方式，没有强制转换，根据运算特征自动转换为字符串，隐式转换
```

隐式转换所使用的转换方法是自动执行String（）这个方法

###### （3）字符串方法
- toString()  返回字符串
实际上是Object对象的方法，因此，万物皆对象，任何类型都可以调用这个方法

```javascript
 a=a.toString(16);//参数必须是2-36之间，否则报错,转换为指定的进制数
```

- toFixed(小数点位数)  
转换为字符串，并且保留小数点位数，自动四舍五入

```javascript
a=a.toFixed(2);
console.log(a); //15.23
```

- parseInt()---将字符串转化为整型
- parseFloat()—将字符串转化为浮点数

```javascript
let str = '12.5px' ;
console.log(Number(str)); //=>NaN
console. log(parseInt(str)); //=>12
console.log(parseFloat(str)); //=>12.5
console. log(parseFloat( 'width:12.5px')); //=>NaN
```

#### 2 数值转换为布尔值

- 除了0以外所有的数值转换为布尔值都是true
- 0转换为布尔值是false

```javascript
var  a=0;
a=Boolean(a);
console.log(a);//false
```

#### 3 数值转换为对象  Object（e）

- 转为数值型对象 存放在堆中

- 具备数值的特征  但是是对象  ===不相等  有引用地址  必须赋值为null才能清理

```javascript
var a=0;
a=Object(a);//数值型对象，存储在堆中
console.log(typeof a);
```



## 二 字符串类型和字符串类型转换


#### 1 字符串转换为数值

·转换的字符串  两边的空格自动清除  中间的空格默认为是字符串


######  （1）强制转换数值类型Number（） 

```javascript
var a="3.2"
a=Number(a);//强制转换为数值类型  
```
######  （2）数值方法
-   parseInt()---转换为整数  可以转换进制
- parseFloat()---转换为浮点数   不可以转换进制
```javascript
var a="3.2"
var b = parseInt(a); //转换为整数
console.log(b) // 3


var b=parseFloat(a);//转换为浮点数   
console.log(b) // 3.2

a=parseInt(a,2);//将字符串转换为2进制
```

#### 2  字符串转换为布尔值

仅空字符串转换为布尔值时（空格不是空字符串），是false 除此之外全都是true

```javascript
var str="";
str=Boolean(str);
console.log(str);//false
```


#### 3 字符串转换为对象Object ()   
- 转换为字符串对象

```javascript
var str="aaa";
str=Object(str);
// 转换为字符串对象
 console.log(str);
```
打印结果：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200707202650512.png)


## 三 布尔值类型和布尔值类型转换


#### 1 布尔转换为数值

- true转换为1，false转换为0
```javascript
 var b=true;
 b=Number(b);
console.log(b);//.1
```

#### 2 布尔转换为字符

转换后就是字符串true和false

#### 3 布尔转换为对象
转换后就是布尔值对象
#### 4 任何类型转换为布尔值
只有“”，null,undefined，0，NaN，false转换为false其他值都转换为true


## 四 其他转换

#### 一 undefined null转换为字符串和数值

```javascript
var a;
 var b=null;
 a=String(a);
 b=String(b);
 console.log(b);

 a=Number(a);//转换为数值是NaN
 b=Number(b);//转换为数值是0

 a=parseInt(a);//NaN
 b=parseInt(b);//NaN
 console.log(a,b);



undefined == null // true
```
#### 二  

```javascript
 console.log(3+[])//3    字符3
        console.log(3+undefined)//NaN  
        console.log(3+null)//3      数值3
        console.log(3+{})//3[object object]
        console.log([]+{})//[object object]
        console.log(undefined+{})//undefined[object object]
        console.log(undefined+[])//undefined
        console.log(toString(["1",2]));//[object undefined]
        console.log(toString({}));//[object undefined]
        console.log(String([]));//空
        console.log(String({}));//[object object] 
```

 


# 0 - 0 - 知识点：
## 一  var a=3和 a=3

```javascript
 console.log(var a=3);//一旦使用var是不可以返回的
console.log(a=3);// 没有使用var会被赋值的结果返回
```
## 二 对象清空

```javascript
var obj={};//空对象
obj=null;//设值为空
```
## 三 str.trim()   清除字符串前后空格 

```javascript
 var str=" a a  ";
  str=str.trim();//清除字符串前后空格
console.log(str);//aa
```