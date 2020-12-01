# Ⅰ- 壹 - Js对象
一个对象是一组简单数据类型（有时是引用数据类型）的无序列表，被存储为一系列的名-值对(name-value pairs)。这个列表中的每一项被称为 属性（如果是函数则被称为 方法）。

**特点：**
- 对象引用存储，对象储存在堆中
- 对象类型的key隐式转换为字符串类型
- 当以变量为key的时候 需要加  [  ]   
- 当以一个对象类型为key的时候 这个对象都会转换为字符串（[object Object]），
## 一 Js对象的创建
#### 1 构造函数创建法

```javascript
var obj=new Object();
```

#### 2 字面量创建法

```javascript
 var obj={};
```
## 二 使用
- 点语法拒绝使用非字符类型属性
- 在对象中key除了字符类型以外只能支持symbol


**示例：**
```javascript
var a="keys"
var obj={
     // key:value
      name:"xietian",
      // 字符型key
  // "name":"xietian",
      [a]:16,
     // 变量型key
       5:10
 }
console.log(obj.name);
 console.log(obj.keys);
console.log(obj.5);//点语法拒绝使用非字符类型属性
console.log(obj[5]);//在对象中key除了字符类型以外只能支持symbol
```

#### 1 JSON数据和对象之间的转换

###### （1）JSON.stringify()  对象转换为JSON格式的字符串

```javascript
var str=JSON.stringify(obj);
```

###### （2）JSON.parse()   将JSON格式字符串转换为对象

```javascript
var s='{"a":1,b:2,"c":"xietian","checked":true,"o":{"a":1}}';
console.log(str);
// 将JSON格式字符串转换为对象
var o=JSON.parse(s);
console.log(o);

```
###### 注意
- JSON方法不可以将对象中方法进行转换

```javascript
         var obj={
             a:1,
             b:true,
             c:function(){

             }
         }

        // JSON方法不可以将对象中方法进行转换
         var str=JSON.stringify(obj);
         console.log(str);
```

#### 2 内存管理
- 内存分配：当我们申明变量、函数、对象的时候，系统会自动为他们分配内存
- 内存使用：即读写内存，也就是使用变量、函数等
- 内存回收：使用完毕，由垃圾回收自动回收不再使用的内存
###### （1）垃圾回收机制
- 在堆中的对象可能被若干个变量引用其地址，如果这个对象在后面的内容中不再使用
- 我们需要将堆中的这个对象清除，否则，不会被浏览器自动清除，这样就会造成垃圾产生
- 当不断产生这种垃圾时，我们就把这种情况叫内存泄漏

###### （2）如何处理内存泄漏
- 先创建每个对象的管理池，针对每个对象所引用它的变量做统一存储管理，如果
-  需要清理该对象时,将引用它的所有变量设置为null,当内存上限达到峰值时,系统
- 会通过垃圾回收车将这些堆中无引用的对象全部清除回收，这就是垃圾回收机制


## 三 对象的遍历 for in
- 对象的遍历是通过添加属性的先后顺序遍历的
```javascript
var obj={
    c:3,
    d:4,
    a:1,
    b:2, 
    e:5,
    f:{
        a:1,
        b:2,
        c:3
    }
}

 for(var prop in obj){
     console.log(prop,obj[prop]);
      }
// 对象的遍历是通过添加属性的先后顺序遍历的
console.log(obj);
```





- 删除对象的属性

```javascript
var obj={a:3,b:4}

delete obj.a;

也可以根据键值删除对象下的属性。
```



#### 1 对象的复制

```javascript
        var obj={
            c:3,
            d:4,
            a:1,
            b:2, 
            e:5,
            f:{
                a:1,
                b:2,
                c:3
            }
        }
```

###### （1）浅复制

```javascript

  var obj1={};
        for(var prop in obj){
            // console.log(prop);
            obj1[prop]=obj[prop];
        }
        obj.a=10;
        // 对象复制
        console.log(obj1); 


```

###### （2）深复制

```javascript
        // 对象的深复制
var obj1=JSON.parse(JSON.stringify(obj));
obj.f.a=100;
 console.log(obj1);
        // 不可枚举属性
```






# Ⅱ - 贰 - 函数

- 函数也是一个对象；它是可以重复执行的代码块；是可以完成特定功能的一段代码；使用typeof检查一个函数对象时，会返回function。
- 什么是函数：函数又叫方法，在程序里面函数是用来执行某些特定功能的代码。

- 封装到函数中的代码不会立即执行；函数中的代码会在函数调用的时候执行 ；调用函数语法：函数对象() ；调用函数时，函数中封装的代码会按照顺序执行
- 在加载页面的时候函数就已经创建完成，可以任意的地方调用
- 函数可以被覆盖 覆盖后不可以被执行
- 函数中如果不写return  就会返回undefined


## 一 函数创建的方法
- 函数是一个对象，存储在堆中的
- 如果函数中没有使用return关键词，函数返回一个undefined值

声明：

```javascript
function 函数名(参数变量列表){

       函数体；

       return   返回值；

}
```

#### 1 匿名函数创建


- 变量什么时候创建 函数才会在堆中创建
- 在变量之前调用会报错

```javascript
   // fn2();//这里调用会报错
     var fn2=function(){
        // 匿名函数创建，创建好的匿名函数赋值给fn2这个变量
        // 变量什么时候定义，这个变量才能在栈中产生，才可以被调用
        console.log("aaa");
    } 

     fn2();
```

####  2 自执行函数创建
- 自动执行
- 只能执行一次
- 执行完一次自动销毁，因为在堆中没有储存，除非return

```javascript
    (function(){
        console.log("aa");
        // 会自动执行，以后永远不能再调用
    })()
```

#### 3 构造函数创建函数

- 构造函数创建每个参数都是字符串，除了最后一个是语句块之外，前面所有的参数都是该函数的参数
- 需要进行一系列反射，所以执行速度最慢。
- 所有字符串都可以转换成函数，可以达到一个动态创建函数（后端传输数据），优点函数固定化

```javascript
    var fn=new Function("a","b","console.log(a+b)");
 	fn(3,4);
 	
	//转换成这种
    //function fn(a,b){
    //    console.log(a+b);
    //} 
  
```


## 二 函数参数
- 函数括号里面的变量  及描述为形参
- 由执行填入的参数为实参
- 参数是为了解决函数的不同问题
- 在设计函数时，尽量不让函数内部与外部有关联。尽量让函数内部是一个独立的个体
- 抽象，不去具体解决一个事情根据填入的需求改变内容
- ES5版本中 js中参数不能设置初始值，不填写参数就是undefined
- 这里执行时填入的参数叫做实参，实参是按照形参顺序一一赋值给形参,如果实参数量小于形参数量，后面的形参值就是undefined
```javascript
function fn(a, b) {}
fn(3,4)
```

#### 1 arguments   ES6舍弃

- parameter是形参，体现在函数定bai义中，当出现在整个du函数内都是可以使用的， 要是离开该函数则不能使用 
- 方法名.length  也可以查看形参的参数长度
- arguments.callee .length也可以查看形参的参数长度

- argument是实参，体现在主调函数中，当进入被调函数后，实参变量也不能使用

 - 定义函数时没有定义参数
- 如果实参数量大于形参数，使用arguments
- arguments只能出现在函数语句块中
- 用于当前函数的参数不固定数量

arguments   常用属性



| 属性                     | 简介                   |
| ------------------------ | ---------------------- |
| arguments                | 直接打印所有参数       |
| arguments[下标]          | 通过下标获取参数       |
| arguments.length         | 获取 参数长度          |
| arguments.callee .length | 查看当前函数的形参     |
| arguments.callee         | 当前函数               |
| arguments.callee.name    | 当前函数的名字         |
| arguments.callee.caller  | 调用当前函数的外部函数 |


- arguments.callee 用于匿名函数使用
```javascript
 var i=0;
    (function(){
        i++;
        if(i<5) arguments.callee();
    })(); 
```

#### 2 return

- return 语句会终止函数的执行并返回函数的值。
- return 是javascript里函数返回值的关键字，一个函数内处理的结果可以使用return 返回，这样在调用函数的地方就可以用变量接收返回结果。
- return 关键字内任何类型的变量数据或表达式都可以进行返回，甚至什么都不返回也可以
- 打印函数的时候如果没有return则返回undefined 

return 也可以作为阻止后续代码执行的语句被使用，例如

```javascript
function abc(){

	if(bool) return;

}
```

这样可以有效的控制语句在一定的条件下执行，不过一定要与break区分，break是用在条件当中，跳出的也仅仅是条件和循环，但是return 却可以跳出函数，仅仅是针对函数使用，如果没有函数是不能使用return的。

- 当判断条件过多时候可以利用switch 穿越功能进行判断

```javascript
 var sum=fn(3,5,"*");
        console.log(sum);

        function fn(a,b,type){
            if(isNaN(a) || isNaN(b)) return "错误的数字";
            switch(type){
                case "+":return fn1(a,b);
                case "-":return fn2(a,b);
                case "*":return fn3(a,b);
                case "/":return fn4(a,b);
                default:
                return "错误的符号";
            }
        }

        function fn1(a,b){
            return a+b;
        }
        function fn2(a,b){
            if(a<0) a=0;
            return a-b;
        }
        function fn3(a,b){
            return a*b;
        }
        function fn4(a,b){
            if(b===0) return "错误除数";
            return a/b
        }
```

函数执行中执行其他函数，另一个函数中的内容执行完成后才会继续执行当前函数
当需要并列执行多个时，我们可以在一个函数中统一调配执行的顺序

###### 3 setTimeout 定时器和setInterval延时器



在一定时间之后执行
- var id=setTimeout(超时执行的函数,超时时间,执行函数的参数)  返回一个id数
- clearTimeout(id)  清除定时器

间隔一段时间执行
- var id=setInterval(超时执行的函数,超时时间,执行函数的参数)  返回一个id数
- clearInterval(id)  清除延时器






## 三 回调
- 将一个函数以参数的形式传入到另一个函数中，并且在那个函数执行（当前函数调用另一个函数）
- 回调一般用于当处理某件事情需要等待时，设置回调
- 当不需要关心具体后续需要处理的事情时，设置回调




#### 案例
**红绿灯**

```javascript
红绿灯
       var id;
      function setLight() {
        arguments[0](arguments[1], arguments[2]);
      }
      function redLight(fn, fn2) {
        clearTimeout(id);
        console.log("红灯");
        id = setTimeout(fn, 2000, fn2, arguments.callee);
      }
      function yellowLight(fn, fn2) {
        clearTimeout(id);
        console.log("黄灯");
        id = setTimeout(fn, 2000, fn2, arguments.callee);
      }
      function greenLight(fn, fn2) {
        clearTimeout(id);
        console.log("绿灯");
        id = setTimeout(fn, 2000, fn2, arguments.callee);
      }

      setLight(yellowLight, redLight, greenLight); 
```
**1-100数字累加**

```javascript
 function fn1(fn, i, sum) {
        if (i === undefined) (i = 1), (sum = 1);
        i++;
        if (i > 100) {
          return sum;
        }
        return fn(arguments.callee, i, sum);
      }

      function fn2(fn, i, sum) {
        sum += i;
        return fn(arguments.callee, i, sum);
      }
      function fn3(fn, i, sum) {
        sum *= i;
        return fn(arguments.callee, i, sum);
      }

      var sum = fn1(fn3);
      console.log(sum);
```

## 四 递归

- 自己调用自己


#### 1 深层复制

```javascript
var obj={
	 a:1,
            b:2,
            c:{
                a:1,
                b:2,
                c:{
                    a:1,
                    b:2,
                    c:{
                        a:1,
                        b:2,
                        c:3
                    }
                }
         }
}
var obj1={}
        
   function cloneObj(obj,target){
            target=target || {};
            for(var prop in obj){
                if(typeof obj[prop]==="object" && obj[prop]!==null){
                    target[prop]={};
                    cloneObj(obj[prop],target[prop])
                }else{
                    target[prop]=obj[prop];
                }
            }
            return target;
        }

        var obj1=cloneObj(obj);
        console.log(obj1); 
```



#  Ⅲ - 叁 - 变量的作用域


- 变量只能在局部中使用，因此叫做局部变量
- 在任何地方都能使用的变量叫做全局变量

- 在函数中只要看到使用var定义的变量，这个变量就一定是局部变量，而且这个变量被优先

- 并且变量不能被保存在函数执行完成后还能使用
 不能在外部使用，作用：仅用于函数内部，内部实行微循环
- 优先使用局部变量

- 全局变量属于window  ES6禁止使用



被定义在函数内部的变量，使用范围仅在函数内部
```javascript
  		var a=10;
        function fn(){
            // 被定义在函数内部的变量，使用范围仅在函数内部
            // 并且当前函数执行完成以后，这个变量会被销毁
            // 下一次这个函数再执行时，会重新定义这个变量
            // 并且变量不能被保存在函数执行完成后还能使用
            var a=1;
            console.log(a);//优先局部变量  打印1
            // console.log(a+window.a)//ES6被禁止
        }

        fn(); 
        // console.log(a,"_____"); // 打印10
```
如果当前函数内没有定义与全局变量相同的局部变量名
```javascript
		var a=10;
        function fn(){
            // 如果当前函数内没有定义与全局变量相同的局部变量名
            // 这里直接调用全局变量
            console.log(a);//打印 10
        }

        fn(); 
```
遵照局部变量优先原则
在函数中只要看到使用var定义的变量，这个变量就一定是局部变量，而且这个变量被优先
```javascript
 var a=10;
        function fn(){
            var a;
            console.log(a);//遵照局部变量优先原则 打印 undefined
        }

        fn(); 
```


```javascript
 		var a=10;
        function fn(){
            // 打印变量早于定义该局部变量之前，打印undefined
            console.log(a);//任然遵照局部变量优先原则 
            var a=4; 
        }

        fn(); 
```

```javascript
		var a=10;
        function fn(){
            console.log(a);//这里没有使用var，当前a是全局的  打印 10
             a=4; 
        }

        fn(); 
```

```javascript
 		var a=10;
        function fn(a){
            // 当在函数中设置了参数，
            // 那么就相当于，这个参数就是被var定义好的局部变量
            console.log(a); // 打印 5
        }

        fn(5);

        console.log(a);
```
因为参数本身就是局部变量，所以重新定义不赋值不起作用
```javascript
		var a=100;
        function fn(a){
            console.log(a);//6
            var a;//因为参数本身就是局部变量，所以重新定义不赋值不起作用
            console.log(a);//6
            a=10;
            console.log(a);//10
        }

        fn(6); 
```

```javascript
     function fn(f){
            var x=20;
            f(x);
        }

        function fn1(x){
            console.log(x); //打印  20
        }

        fn(fn1); 
```



# 0 - 0 - 知识点：

在函数内 只要是var 定义一个变量并且添加数据就会作用域当前函数，