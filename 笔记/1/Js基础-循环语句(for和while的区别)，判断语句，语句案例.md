# Ⅰ- 壹 - 条件语句
## 一 if
- if就是 “如果”的意思。
- 表达式值为真时，执行if控制的语句
- 语句体只有一条语句时,可以不加{}
- 条件表达式会隐式转换为布尔类型

语法格式1
```javascript
if ( 条件表达式) {
	语句1
}
```
语法格式2

如果上面条件满足则不会判断下面内容。
配合函数 return将会很少使用这个用法
```javascript
if(条件表达式){
	语句1
}else{
	语句2
}
```

**if 嵌套**

```javascript
if(条件){
	if(条件){
	}
}
```

## 二 switch case
- 判断 switch中的表达式中 是否绝对等于（===）。 既数值和数值类型相等
- break  跳出，如果不写break不判断值2是否相等，直接穿越

```javascript
switch(表达式){
            case 值1:
            // 当表达式绝对等于值1时执行这里的内容
            // break  跳出，如果不写break不判断值2是否相等，直接穿越
            break;
            case 值2:
              // 当表达式绝对等于值2时执行这里的内容
            break;
            case 值3:
              // 当表达式绝对等于值3时执行这里的内容
            break;
            case 值4:
              // 当表达式绝对等于值4时执行这里的内容
            break;
            default:
            // 默认以上条件都不满足时执行这里
        }
```

**工作原理**：首先设置表达式 （通常是一个变量）。随后表达式的值会与结构中的每个 case 的值做比较。如果存在则执行与该 case关联的代码块。请使用 break 来阻止代码自动地向下一个 case 运行。

- case 当做表达式进行选择

```javascript
var score=prompt("请输入你的成绩");
switch(true){
            case score>=90 && score<=100:
             console.log("优秀");
            break;
            case score>=80:
            break;
            case score>=70:
            break;
            case score>=60:
            break;
            default:
            
        }
```

# Ⅱ - 贰 - 循环语句
## 一 while
- 条件表达式都是将结果转换为布尔值
- while语句是一种先判断，后运行的循环语句。也就是说，必须满足条件了之后，方可运行循环体
- 循环体有可能一次也不执行。
- 循环体应包含有使循环趋向结束的语句；
- 下列情况，退出while循环
	1. 条件表达式不成立
	2. 循环体内遇 break 

语法格式：

```javascript
while（判断语句）｛
	循环体；
｝
```

语句1
例如：

```javascript
var i=1; //赋初值语句
while(i<=10)//控制循环条件
{
	document.write("hello world!<br/>");  //循环体
	i++; //循环增量
}
```


## 二 do while

- do...while语句是一种先运行，后判断的循环语句。也就是说，不管条件是否满足，至少先运行一次循环体。
- ++i 最好用于累加


语法格式
```javascript
赋初值1；
do
{
   循环体;2    
   循环增量;3   

}while(循环条件);4
```

语句

```javascript
var i=1;
do{
	document.write("hello world!<br/>");  //循环体
	i++;
}while(i<=10);
```
++i

```javascript
var i=0;
do{
	document.write("hello world!<br/>");  //循环体
	i++;
}while(++i<10);
```


## 三 for
- 循环三要素：即表达式1，表达式2，表达式3
           （循环变量赋初值，循环判定条件，循环增量）

- 循环体：需要重复执行的语句。
- 双层循环时，不要再内层的判断中，改变外层变量
- 循环是同步的，会造成堵塞。循环次数不能超过10亿次，循环嵌套不能嵌套太多。一般不超过三次







语法格式

```javascript
for（表达式1；判断表达式2；表达式3）
｛
		循环体；
｝
```

语句

```javascript
//0-9累加
var sum=0;
for(var i=0;i<10;i++){
sun+=i; //累加器
	console.log(i)
}
```

循环嵌套：外层循环一次内层循环一遍

```javascript
for(var i=0;i<10;i++){
   for(var j=0;j<10;j++){
		console.log(i,j,i*j)
	}
}
```
## 四 for 和 while 的区别
-  当循环的次数确定时，使用for循环和while循环差别不大，但是当循环次数不确定时，while方法使用起来更加方便（已知循环次数用for循环，未知循环次数用while循环）


- 在处理大量数据的时候用while，比较合适。for 中需要定义初始变量 在遍历大量数据的时候效率低一点 





# Ⅲ - 叁 - 其他
#### 1 break
break语句会立即退出循环，强制继续执行循环后面的语句，结束本层循环。
一般出现在循环语句和  switch中

- 可以当做锚点使用

```javascript
    var str = "";
    var j = 0;
    // 设置锚点位置
    AB: while (j < 10) {
        str += "<ul>";
        var i = 0;
        while (i < 10) {
          str += "<li>项目"+ i + " </li>";
          i++;
          //跳出到锚点位置
          if (i === 4 && j === 4) break AB;
        }
        str += "</ul>";
        j++;
    }
    document.write(str);
```



#### 2 continue
- continue语句仅用于循环语句。虽然也是立即退出循环，但退出循环后会从循环的顶部继续执行，结束本次循环进行下一次。
- 出现在循环语句中
- continue跳出最近的循环

```javascript
for (var box = 1; box <= 10; box++) {
	if (box == 5) break;//如果box是5，就退出循环
	document.write(box);
	document.write('<br />');
}

for (var box = 1; box <= 10; box++) {
	if (box == 5)
	 continue;//如果box是5，就退出当前循环
	document.write(box);
	document.write('<br />');
}
```
#  Ⅳ - 肆 - 案例
## 一 打印三角形
1
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200708194434956.png)

```javascript
      var j = 0,
        row=10,
        col=20,
      i,n;
    while (j++ < row) {
      n = 0;
      while (n++ < row-j) document.write("&ensp;");
      i = 0;
      while (i++ < j*2-1) document.write("*");
      document.write("<br>");
    } 
```
1.1
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200708205933739.png)

```javascript
  var j = 10,
    row = 10,
    col = 20,
    i, n;
  while (j-- > 0) {

    i = row;
    while (i-- >= j) {
      document.write("&nbsp;");

    }

    n = 0;
    console.log(j)
    while (n++ < j) {
      document.write(" * ");

    }

    document.write("<br>");
  }
```


2
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200708195426478.png)



```javascript
  var j = 0,
    row = 10,
    col = 20,
    i, n;
  while (j++ < row) {
    n = 0;
    while (n++ <= row - j) document.write(" ");
    i = 0;
    while (i++ < j ) document.write(" * ");
    document.write("<br>");
  }
```
3
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200708195811412.png)

```javascript
  var j = 0,
    row = 10,
    col = 20,
    i, n;
  while (j++ < row) {
    n = 0;
    while (n++ <= row - j) document.write(" * ");
    i = 0;
    while (i++ < j ) document.write("  ");
    document.write("<br>");
  }
```

## 二 表格和 99乘法表
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200708194923531.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)
css

```javascript
    table {
      border-collapse: collapse;
      width: 800px;
    }

    td,
    th {
      height: 30px;
      line-height: 30px;
      font-size: 18px;
      text-align: center;
      border: 1px solid #000000;
    }
```

js

```javascript
    //   9*9 乘法表格
     var col = 9,
      row = 9,
      i = 0,
      j = 0;
    document.write("<table>");
    while (j++ < row) {
      i = 0;
      document.write("<tr>");
      while (i++ < j) document.write("<td>" +j+"*"+i+"="+j*i + "</td>");
      document.write("</tr>");
    }

    document.write("</table>"); 

```
打印表格
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200711094848873.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)

```javascript
    var col = arr.length,
      row = 9,
      i = 0,
      j = 0;

    document.write("<table>");

    while (j++ < row) {
      i = 0;


      for (; i < col; i++) {

        document.write("<td>");
        document.write("33");
        document.write("</td>");
      }
      document.write("</tr>");
    }

    document.write("</table>");

```

## 三 求0-100所有质数
while
```javascript
// 求0-100所有质数
      var j = 1,i=2,bool=true;
     while (j++ < 100) {
         i = 2;
        bool = true;
        while (i < j) {
          if (j % i === 0) {
            bool = false;
            break;
          }
          i++;
        }
        if (bool) console.log(j);
      } 
```













## 四 打印列表
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200708205006272.png)

```javascript
 var j = 0,
    i;
  document.write("<ul>");
  while (j++ < 10) {
    i = 0;
    document.write("<li>第" + j + "章<ul>");
    while (i++ < 10) document.write("<li>第" + i + "节</li>");
    document.write("</ul></li>");
  }
  document.write("</ul>");
```





## 五 水仙花数

```javascript
for(var i=100,a,b,c;i<1000;i++){
	a=parseIne(i/100);
	b=parsrInt(i/10)%10;
	c=i%10;
	if(a*a*a+b*b*b+c*c*c===i) console.log(i);
}
```


## 六 字符串倒装

```javascript
var str "asdfsdfsdf";
console.log(str.length);//获取字符串长度
var s="";
for(var i=str.length-1;i>=0;i--){
	s+=str[i]
}
console.log(s)
```




# 0 - 0 - 知识点：

## 一 ascll码值和数值转换
- 字符串.charCodeAt（字符串下标）: 获取字符串的ascll码值
- String.formCharCode(ascll码值)   :  ascll码值对应的值


| 字符 | ascll码范围 |
| ---- | ----------- |
| a-z  | 97-122      |
| A-Z  | 65-90       |
| 0-9  | 48-57       |
所有码表地址     http://ascii.911cha.com/
```javascript
console.log("azAZ09".charCodeAt(5));//57
console.log(String.fromCharCode(97));//a
```


## 二 &emsp；&ensp；&nbsp； 区别
- &emsp； 汉字宽
它叫“全角空格”，全称是Em Space，em是字体排印学的计量单位，相当于当前指定的点数。例如，1 em在16px的字体中就是16px。此空格也传承空格家族一贯的特性：透明的，此空格也有个相当稳健的特性，就是其占据的宽度正好是1个中文宽度，而且基本上不受字体影响。

- &ensp；字母宽
它叫"半角空格"，全称是En Space，en是字体排印学的计量单位，为em宽度的一半。根据定义，它等同于字体度的一半（如16px字体中就是8px）。名义上是小写字母n的宽度。此空格传承空格家族一贯的特性：透明的，此空格有个相当稳健的特性，就是其占据的宽度正好是1/2个中文宽度，而且基本上不受字体影响。

- -&nbsp；不换行空格

它叫不换行空格，全称No-Break Space，它是最常见和我们使用最多的空格，大多数的人可能只接触了&nbsp;，它是按下space键产生的空格。在HTML中，如果你用空格键产生此空格，空格是不会累加的（只算1个）。要使用html实体表示才可累加，该空格占据宽度受字体影响明显而强烈。



**标注：** https://www.jianshu.com/p/160e5cb0209c