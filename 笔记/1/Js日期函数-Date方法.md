# Ⅰ- 壹 - Date对象
## 一 Date对象简介
     日期和时间，在Web应用中随处可见，也必不可少。
     JS脚本内置了Date对象，该对象为我们提供了一些列操作时间和日期的方法。

#### 1 使用时必须使用new来调用创建我们的日期对象（既构造对象）
构造当前时间对象主要有以下4中方法：

> var MyDate = new Date()
> var MyDate = new Date(milliseconds)
> var MyDate = new Date(string)
> var MyDate = new Date(y, m, d, h, min, sec, ms)

#### 2 创建date的时候，传入要设置的时间参数
 **参数形式有以下5种：**

| 参数                                | 格式（以2006年1月12日）               |      |
| ----------------------------------- | ------------------------------------- | ---- |
| new Date(“month dd,yyyy hh:mm:ss”); | new Date("January 12,2006 22:19:35"); |      |
| new Date(“month dd,yyyy”);          | new Date("January 12,2006");          |      |
| new Date(yyyy,mth,dd,hh,mm,ss);     | new Date(2006,0,12,22,19,35);         |      |
| new Date(yyyy,mth,dd);              | new Date(2006,0,12);                  |      |
| new Date(ms);                       | new Date(1137075575000);              |      |
**参数简述**

* month:用英文 表示月份名称，从January到December
* mth:用整数表示月份，从0（1月）到11（12月）
* dd:表示一个 月中的第几天，从1到31
* yyyy:四位数表示的年份
* hh:小时数，从0（午夜）到23（晚11点）
* mm: 分钟数，从0到59的整数
* ss:秒数，从0到59的整数
* 	ms:毫秒数，为大于等于0的整数


## 二 JS的时间标准

> 以GTM时间1970年1月1日零点为标准零点，JS脚本中采用UNIX系统存储的时间，存储从标准零点到当前系统时间的毫秒数。注意，JS在读取当前时间时，依赖于客户端的系统时间，如果客户端系统时间有误，可能会带来一定的问题。



# Ⅱ - 贰 -日期时间方法

**使用new Date获取一个时间对象：var date = new Date()**

##  一 时间对象

| Date方法                  | 简介                 | 使用                                                         |
| ------------------------- | -------------------- | ------------------------------------------------------------ |
| date，                    | (中国标准时间)       | console.log(date);//Wed Jan 01 2020 22:12:29 GMT+0800 (中国标准时间) |
| date.toUTCString()        | 获取格林尼治日期时间 | console.log(date.toUTCString());//Wed, 01 Jan 2020 14:12:29 GMT |
| date.toLocaleString()     | 获取本地日期时间     | console.log(date.toLocaleString());//2020/1/1 下午10:12:29   |
| date.toLocaleDateString() | 获取本地日期         | console.log(date.toLocaleDateString());//2020/1/1            |
| date.toLocaleTimeString() | 获取本地时间         | console.log(date.toLocaleTimeString());//下午10:12:29        |
## 二 时间的获取方法
| Date方法 | 简介 | 使用|
|--|--|--|
|date.getDate()，|返回几号 (1 ~ 31)。|console.log(date.getDate());//1
|date.getDay()，|返回星期几 (0 ~ 6)，星期日为0。|console.log(date.getDay());//3
|date.getMonth()，|返回月份 (0 ~ 11)，从0开始。|console.log(date.getMonth());//0
|date.getFullYear()，|返回四位数字的年份。|console.log(date.getFullYear());//2020
|date.getYear()，|两位数的年份，从1900年开始。|console.log(date.getYear());//120
|date.getHours()，|返回小时 (0 ~ 23)。|console.log(date.getHours());//22
|date.getMinutes()，|返回分钟 (0 ~ 59)。|console.log(date.getMinutes());//12
|date.getSeconds()，|返回秒 (0 ~ 59)。|console.log(date.getSeconds());//29
|date.getMilliseconds()，|返回毫秒(0 ~ 999)。|console.log(date.getMilliseconds());//0
|date.getTime()，|返回 1970 年 1 月 1 日至今的毫秒数。|console.log(date.getTime());//1577887949000 |





## 三 时间的设置方法
| Date方法                  | 简介                    |
| ------------------------- | ----------------------- |
| date.setDate(x)，         | x设置几号 (1 ~ 31)。    |
| date.setMonth(x)，        | x设置月份 (0 ~ 11)。    |
| date.setFullYear(x)，     | x设置年份（四位数字）。 |
| date.setHours(x)，        | x设置小时 (0 ~ 23)。    |
| date.setMinutes(x)，      | x设置分钟 (0 ~ 59)。    |
| date.setSeconds(x)，      | x设置秒 (0 ~ 59)。      |
| date.setMilliseconds(x)， | x设置毫秒 (0 ~ 999)。   |
| date.setTime(x)，         | x以毫秒设置 Date 对象。 |



任何设置，如果数值大于该值域的最大值时就会进位

new data 的时候就已经固定时间

# Ⅲ - 叁 -Date扩展
## 一 格式化日期 
#### 1 xxxx年xx月xx日星期x (2020年6月29日星期一)
- 封装

```javascript
 Date.prototype.format1st = function (fmt) {
    var arr = ['星期日', '星期一', '星期二', '星期三', '星期四', '星期五', '星期六'];
    var o = {
      "M+": this.getMonth() + 1 + '月', //月份
      "d+": this.getDate() + '日', //日
      "a+": arr[this.getDay()]
    };

    if (/(y+)/.test(fmt)) {
      fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "年").substr(4 - RegExp.$1.length));
    }
    for (var k in o) {
      if (new RegExp("(" + k + ")").test(fmt)) {
        fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ?
          (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
      }
    }
    return fmt;
  }
```
- 使用
格式化输出当前时间

```javascript
 //2020年6月29日星期一    
   console.log((new Date()).format1st("yyyyMda"));
```

#### 2 xxxx-xx-xx xx:xx:xx (2020-01-01 08:00:07.523)
     对Date的扩展，将 Date 转化为指定格式的String
     月(M)、日(d)、小时(h)、分(m)、秒(s)、季度(q) 可以用 1-2 个占位符， 
     年(y)可以用 1-4 个占位符，毫秒(S)只能用 1 个占位符(是 1-3 位的数字) 


**为方便我们对日期（Date）进行格式化输出，先对 Date 进行扩展，增加 format 方法。以后调用 Date 对象的 format 方法即可将日期转换成我们指定格式的字符串（String）。**
- 封装：
```javascript
Date.prototype.format2nd = function (fmt) {
  var o = {
      "M+": this.getMonth() + 1, //月份
      "d+": this.getDate(), //日
      "h+": this.getHours(), //小时
      "m+": this.getMinutes(), //分
      "s+": this.getSeconds(), //秒
      "q+": Math.floor((this.getMonth() + 3) / 3), //季度
      "S": this.getMilliseconds() //毫秒
  };
  if (/(y+)/.test(fmt)) {
    fmt = fmt.replace(RegExp.$1, (this.getFullYear() + "").substr(4 - RegExp.$1.length));
  }
  for (var k in o) {
    if (new RegExp("(" + k + ")").test(fmt)) {
      fmt = fmt.replace(RegExp.$1, (RegExp.$1.length == 1) ?
        (o[k]) : (("00" + o[k]).substr(("" + o[k]).length)));
    }
  }
  return fmt;
}

```
- 使用
格式化输出当前时间

```javascript
  // 2020-01-01 18:25:58.978
  console.log((new Date()).format2nd("yyyy-MM-dd hh:mm:ss.S"));
// 2020-1-29 18:27:30.259
  console.log((new Date()).format2nd("yyyy-M-d h:m:s.S"));     
```

格式化输出指定时间

```javascript
var date = new Date("2019-03-31 15:40:16.0");
 console.log(date.format2nd("MM-dd hh:mm"));  //03-31 15:40``
```

# 0 - 0 - 知识点：
## 时间算法
1. d = parseInt(总秒数/ 60/60 /24);//计算天数
2. h = parseInt(总秒数/ 60/60 %24)//计算小时
3. m = parseInt(总秒数 /60 %60 );//计算分数
4. 4.s=parseInt(总秒数%60);//计算当前秒数

## RegExp 

RegExp 是javascript中的一个内置对象。为正则表达式。


RegExp.$1是RegExp的一个属性,指的是与正则表达式匹配的第一个 子匹配(以括号为标志)字符串，以此类推，RegExp.$2，RegExp.$3，..RegExp.$99总共可以有99个匹配