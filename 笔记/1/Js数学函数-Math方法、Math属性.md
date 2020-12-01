# Ⅰ- 壹 - Math简介
- Math全部都是静态属性和方法 Math是一种静态类
- 不需要创建对象
- 该类别不能实例化  var met=new Math()//错误
- Math 是数学函数，但又属于对象数据类型 typeof Math => ‘object’ 

# Ⅱ - 贰 -Math属性
| Math属性名   | 介绍                                              |
| ------------ | ------------------------------------------------- |
| Math.E       | 返回算术常量 e，即自然对数的底数（约等于2.718）。 |
| Math.LN2     | 返回 2 的自然对数（约等于0.693）。                |
| Math. LN10   | 返回 10 的自然对数（约等于2.302）。               |
| Math.LOG2E   | 返回以 2 为底的 e 的对数（约等于 1.414）。        |
| Math.LOG10E  | 返回以 10 为底的 e 的对数（约等于0.434）。        |
| Math.PI      | 返回圆周率（约等于3.14159）。                     |
| Math.SQRT1_2 | 返回返回 2 的平方根的倒数（约等于 0.707）。       |
| Math.SQRT2   | 返回 2 的平方根（约等于 1.414）。                 |

* Math的属性用法

```javascript
console.log(Math.PI);//3.141592653589793
console.log(Math.SQRT2);//1.4142135623730951
```


# Ⅲ - 叁 -Math方法
## 一 Math方法总汇
| Math方法    | 描述             |
| ----------- | ---------------- |
| Math.abs(x) | 返回数的绝对值。 |
| Math.acos(x)	| 返回数的反余弦值。
| Math.asin(x)| 	返回数的反正弦值。
| Math.atan(x)	| 以介于 -PI/2 与 PI/2 弧度之间的数值来返回 x 的反正切值。
| Math.atan2(y,x)	| 返回从 x 轴到点 (x,y) 的角度（介于 -PI/2 与 PI/2 弧度之间）。
| Math.ceil(x)	| 对数进行上舍入。
| Math.cos(x)	| 返回数的余弦。
| Math.exp(x)	| 返回 e 的指数。
| Math.floor(x)	| 对数进行下舍入。
| Math.log(x)	| 返回数的自然对数（底为e）。
| Math.max(x,y)| 	返回 x 和 y 中的最高值。
| Math.min(x,y)	| 返回 x 和 y 中的最低值。
| Math.pow(x,y)| 	返回 x 的 y 次幂。
| Math.random()	| 返回 0 ~ 1 之间的随机数。
| Math.round(x)	| 把数四舍五入为最接近的整数。
| Math.sin(x)	| 返回数的正弦。
| Math.sqrt(x)	| 返回数的平方根。
| Math.tan(x)	| 返回角的正切。


## 二 常用Math方法
#### 0 随机数方法 Math.random()
**该方法用于生成一个随机数0~1之间的小数  包含0不包含1  (0=<x<1)，方法没有参数**


- **生成随机数的封装**
```javascript
// Math . floor (Math. random() * (max -min + 1)) + min;
function getRandom(min, max) {
return Math. floor (Math. random() * (max-min + 1)) + min;
}
//生成1-10的随机数
console . log(getRandom(1, 10));
```

#### 1 绝对值方法
 **Math.abs(x)	 返回数的绝对值。** 

```javascript
console .1og(Math. abs(1)); // 1
console . log(Math.abs(-1)); // 1 
console. log(Math.abs('-1')); //隐式转换会把字符串型-1转换为数字型
console. log(Math.abs('pink')); // NaN 
```

#### 2 三个取整方法
###### (1) Math. floor()  向下取整往最小了取值

```javascript
console .1og(Math. floor(1.1)); // 1
console .1og(Math. floor(1.9)); // 1
```
###### (2) Math.ceil() 向上取整 往最大了取值
```javascript
console . log(Math.cei1(1.1)); // 2
console.1og(Math.ceil(1.9)); // 2 I
```
###### (3) Math. round() 四舍五入 负数往大了取

```javascript
console. log (Math. round(1.1)); // 1
console . log(Math. round(1.5)); // 2
console.1og(Math.round(1.9)); // 2

console. log (Math. round( -1.1)); // -1
console. log(Math.round( -1.5)); //这个结果是-1
```
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200629165150488.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3dlaXhpbl80Mjg2MzgwMA==,size_16,color_FFFFFF,t_70)



# 0 - 0 - 知识点：
## 静态方法
上面说 Math 全部都是静态属性和方法，下面来回顾一下什么叫静态方法：
静态方法也叫类的方法，是指把构造函数看成对象，增加的方法。例如数组中的 Array.from ( )、Array.isArray ( ) 。
除此之外还有实例化方法，例如 forEach()、map()。

```javascript
var arr=new Array(1,2,3);
//或者 var arr=[1,2,3]
arr.forEach(function(){

})
```
简单来记，静态方法都是 类型.方法名（Array.from())**