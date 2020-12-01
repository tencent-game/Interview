# Ⅰ- 壹 - 数组基础

对象和数组的区别

     1.     对象是一种松散型结构，对象是键值对存储，当删除一个元素时，
            对象的其他值不会发生变化,对象是没有元素的个数，也就是对象长度
            对象中不知道存储了多少个元素，插入和删除不会影响其他数据，所以
            时间复杂度极低，因为通过key去一一对应存储一个值，所以获取时，只需要
            根据key去取值就可以了，所以时间复杂度极低。对于对象来说，因为
            每个数据都是独立存在,不存在关联关系,更不能排序,所以不找因关联关系找到
            对应的值



     2.     数组是紧密型结构，只用下标存储对应的值，当删除一个元素是
            因为紧密解构的关系，就会将后面的元素向前递进，数组是有长度
            数组中可以知道存储了多少元素，因为插入和删除都会影响数组的元素
            的位置和解构，因此插入和删除都会影响数组的运行效率时间复杂度较高
            数组的存储是依靠下标的，所以如果需要查找一个值，就需要遍历数组的
            每个元素，已到达找到目标元素，因此时间复杂度也是极高的。数组在使用
            时，因为是紧密性解构，我们可以根据上一个内容找到与其相关联的其他元素
            例如我们可以利用数组排序，找一个最小值，还可以迅速找第二位最小值。

## 一 创建数组的三种方式

-    如果构造函数创建数组时，仅有一个参数且这个参数是一个大于等于0
     的正整数，这个数就是这个新数组的长度，并且没有元素。如果负数
     或者小数，就会报错.如果是非数值类型，就会将这个元素放在数组的第0位






	var arr=[];
	var arr=new Array();
	var arr=new Object([]);

## 二 数组特点

-  数组是一个引用列表， 
-  列表的特点：顺序，只有值，紧密，速度慢。
-  将无序的数进行有序的排列

-  数组只有值存储，只能遍历获取值
-  当插入arr[-1]=10时，不会增加长度。
-  可以一半是数组一半是对象
-  如果据需添加则不会覆盖，因为长度发生变化
 -  数组长度不能为负值
 -  arr=[]  不能清空，这是更换引用地址 

| 数组length用法          | 简介                                                      |
| ----------------------- | --------------------------------------------------------- |
| arr.length=arr.length-1 | 如果长度比原来少一个，就会删除最末尾元素                  |
| arr.length--            | 表示删除最后一个元素                                      |
| arr.length++            | 表示在最后添加一个空元素                                  |
| arr.length=0            | 表示清空数组                                              |
| arr.length=true         | 如果给的不是数值，会隐式转换为数值，如果值是NaN，就会报错 |
| arr[arr.length]=10      | 在数组的末尾增加一个元素 10                               |

## 三 数组属性：

函数（数组名）或者   函数（数组名，值，值）

| 数组属性      | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| unshift()     | 向数组的开头添加一个或更多元素，并返回新的长度               |
| push()        | 向数组的末尾添加一个或者更多元素，并返回新长度               |
| pop()         | 删除并返回数组的最后一个元素                                 |
| shift()       | 删除并返回数组的第一个元素                                   |
| join()        | 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分割 |
| concat()      | 连接两个或更多的数组，并返回结果。复制，给新数组添加新元素   |
| splice ()     | 删除元素，并向数组添加新元素                                 |
| slice()       | 从某个已有的数组返回选定的第一个元素                         |
| indexOf()     | 查找元素在数组中的下标，如果么有查找到就返回-1               |
| lastIndexOf() | 从后向前查找                                                 |
| reverse()     | 颠倒数组中元素的顺序                                         |
| sort()        | 对数组进行排序，方法用于对数组的元素进行排序。对数组的引用。会改变原数组 |
| es6 方法      | es6  方法                                                    |
| some()        | 对数组的每个元素判断是否满足条件，如果都不满足就返回false，如果有一个满足的就返回true，并且不再判断后面的内容 |
| every()       | 对数组的每个元素判断是否满足条件，如果有一个不满足条件就返回false，全满足时就返回true |
| reduce()      | 方法对累加器和数组重点每个元素（从左到右）应用一个函数，将其简化为单个值 |
| filter()      | 方法创建一个新数组,其包含通过所提供函数实现的测试的所有元素，原数组的每个元素传入回调函数中，回调函数中有return返回值，若返回值为true，这个元素保存到新数组中；若返回值为false，则该元素不保存到新数组中；原数组不发生改变。 |
| fill()        | 方法用于将一个固定值替换数组的元素                           |


### 1.数组的删除和添加属性

##### （1）unshift（）

1. unshift（）在数组最前面追加若干个新元素
2. unshift（）参数直接写，数组元素都可以
3. unshift（）返回结果是新数组的长度
4. 原数组会发生改变


***重构属性***

```javascript
var arr = [3, 6, 2, 9];
	1、
	function unshift(arr) {
		//创建个变量储存参数的最大长度减一（索引0存放的为数组，要从索引1开始查找）
		//所以let值为2
		var len=arguments.length-1;//2
		//递减循环，i的初始值为arr长度减一，i结束值为0；（arr索引是从0开始的），
		//0 1 2 3索引值
		for (var i =arr.length-1; i >=0 ; i--) {
			//arr[i+len]增加数组的长度。
			//第一次循环  i=3  arr[i+len]长度为5   
			//及arr[5]=arr[3]赋值，arr索引为3的值赋值给arr索引5
			arr[i+len]=arr[i];
		}
		//现在的arr为
		// console.log(arr);//Array(6) [ 3, 6, 3, 6, 2, 9 ]
		//把参数值传给数组
		//从索引为1的开始既（23,5）到参数的最大长度；
		for (var j = 1; j < arguments.length; j++) {
			//第一次循环： j=1;\
			//arr[0]=arguments[1];
			//既把参数索引值为1的值赋值给arr中索引0；
			arr[j-1]=arguments[j];
		}
		//返回现在的长度
		return arr.length;
	}
	2、
	function unshift(arr){
            var len=arguments.length-1;
            for(var i=arr.length-1;i>=0;i--){
                arr[i+len]=arr[i];
                arr[i]=null;
            }
           for(var j=1;j<arguments.length;j++){
               arr[j-1]=arguments[j];
           }
           return arr.length;
        } 
	unshift(arr,23,5);
	console.log(arr);//Array(6) [ 23, 5, 3, 6, 2, 9 ]
	console.log(unshift(arr));//6
```

##### （2）push（）

在数组尾部添加一个或者多个新元素，并且返回数组新长度；

1. push（）在数组尾部追加新元素
2. push（）参数直接写，数组元素都可以
3. push（）返回结果是新数组的长度
4. 原数组会发生改变


***重构属性***

```javascript
		var arr=[3,6,2,9];
		function push(arr) {
			//arguments.length  参数的长度  这里指arr数组的长度；
			for (var i = 0; i < arguments.length; i++) {
				// 每次循环，都会把arr数组索引为i的值赋值给arr的最大长度，长度加一；		
				arr[arr.length]=arguments[i];				
			}
			return arr.length;
		}		
		push(arr);
		console.log(push(arr));//  6
		
```



##### （3）shift(（）

 删除数组的第一个元素，并且返回这个元素

1. shift（）删除数组第一个元素

2. shift（）没有参数

3. shift（）返回结果是删除的那个元素

4. 原数组会发生改变
   
   
   
   ***重构属性***

```javascript
	var arr = [3, 6, 2, 9];
	1、
		function shift(arr) {
			//保存arr索引为0的值
			var len=arr[0];
			//遍历数组  arr长度减一为 arr的最长索引
			for (var i = 0; i < arr.length-1; i++) {
				//第一次循环：arr[0]=arr[1];
				//第二次：arr[1]=arr[2];
				//把后值赋值给前值
				//
				arr[i]=arr[i+1];
				
				
			}
			console.log(arr);//Array(4) [ 6, 2, 9, 9 ]
			//数组长度减一，最后一个值赋值给arr最大长度索引
			arr.length=arr.length-1;
			
			return len;
		}
	2、
	 function shift(arr){
            var elem=arr[0];
            for(var i=1;i<arr.length;i++){
                arr[i-1]=arr[i];
            }
            if(arr.length>0) arr.length--;
            return elem;
        } 


		console.log(arr); //Array(3) [ 6, 2, 9 ]
		console.log("数组长度"+arr.length);//3
		console.log("返回元素"+shift(arr)); //3
	
```

##### （4）pop（）

1. 删除数组的最后一个元素
2. pop（）返回删除的元素
3. pop（） 没有参数
4. 原数组会发生变化

***重构属性***

```javascript
var arr = [3, 6, 2, 9];
1、
function pop(arr) {
	//用变量储存数组的最后索引的值
	var len=arr[arr.length-1];
	//数组长度减一
	arr.length--;
	
	return len;
}

2、
    function pop(arr){
            var elem=arr[arr.length-1];
            if(arr.length>0) arr.length--;
            return elem;
        }


console.log(arr); //Array(4) [ 3, 6, 2, 9 ]
console.log("数组长度"+arr.length);//4
console.log("返回元素"+pop(arr)); //9
```

### 2 数组的拼接与数组的分割

##### （1）join（）

1. 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分隔，转换为字符串
2. join（）返回拼接的字符串
3. join（）参数为分割的某个字符
4. 如果连接符没有参数，默认以逗号连接

***重构属性***
	

```javascript
var arr = [1, 2, 3];
1、
	function join(arr, type) {
		//定义变量赋值为空字符串。
		var str = "";
		//遍历数组，
		for (var i = 0; i < arr.length; i++) {
			//+=都转换为字符串，
			str += arr[i] + type;
		}
		//去掉最后面的符号  
		 if (type) str = str.substr(0, str.length - 1);

		return str;
	}	
2、
  function join(arr,separator){
            if(separator===undefined) separator=",";
            separator=String(separator);
            var str="";
            for(var i=0;i<arr.length;i++){
               if(i!==arr.length-1) str+=arr[i]+separator;
               else str+=arr[i];
            }
            return str;
        }



	console.log(join(arr, "#"))//1#2#3
```

##### （2）concat（）

  1. 数组连接若干个数组或者元素
 2. concat（）返回一个新的连接完成的数组，与原数组无引用关系



***重构属性***

```javascript
var arr = [2, 9];
1、
function concat(arr) {
	var array = [];//创建一个空数组，存放参数数组
	var index=0;//这里表示array 的下标是从0开始的
	
	//把arr数组里的值赋值到新数组array，    index为array长度  等同于arr的数组长度
	for (var i = 0; i < arr.length; i++,index++) {
		array[index]=arr[i];
	}
	console.log(index);
	//如果有除了arr数组意外的参数，arguments获取参数长度从零开始，所以for初始值为1 既下标为1，
	//上一次循环结束后  index为4
	for (var j = 1; j < arguments.length; j++,index++) {
		//判断是不是数组
		if(arguments[j].constructor===Array){
			//arguments[j].length:表示参数是数组的的最大长度，
			for (var k = 0; k < arguments[j].length; k++,index++) {
				//j=1； 参数下标为一的对象，k表示下标为1的参数的对象索引值，
				//array[5]=arguments[1][0]
				//array[5]=arguments[1][1]
				//......
				//赋值给新数组
				array[index]=arguments[j][k];
			}
			
		}else{
			//如果不是数组，直接赋值 ，这里的j表示不是数组的下标索引
			//然后赋值给新数组，执行之后  新数组的索引值加一长度
			
			array[index]=arguments[j];
			index++;
		}
	}
	//返回这个新数组
	return array;
}

2、
   function concat(arr){
            var arr1=[];
            for(var i=0;i<arr.length;i++){
                arr1[i]=arr[i];
            }
            if(arguments.length===1) return arr1;
            for(var j=1;j<arguments.length;j++){
                if(arguments[j]!==null && arguments[j].constructor===Array){
                    for(var k=0;k<arguments[j].length;k++){
                        arr1[arr1.length]=arguments[j][k];
                    }
                }else{
                    arr1[arr1.length]=arguments[j];
                }
            }
            return arr1;
        }



console.log(concat(arr,[3,4,5],67))
```


### 3 数组的操作

##### （1）splice（）

1. 将数组中从第几位开始删除多少个元素，并且返回被删除的元素组成的新数组
2. 将数组中从第几个位开始删除多少个元素后，并且在该位置插入新的若干元素，返回删除元素组成的新数组
3. 在数组的第几位开始插入若干个元素，并且返回空的新数组
4. arr.splice(从什么位置开始，删除多少元素，添加的元素...);
5. 会改变原数组

**属性详解：**
假设有个数组  var arr=[3,6,8,3,7,9];

| 用法                            | 详解                                                         |
| ------------------------------- | ------------------------------------------------------------ |
| var arr1=arr.splice();          | 创建一个空数组；不删除返回一个空数组                         |
| vsr arr1=arr.splice(0);         | 将数组的所有元素传递给新数组                                 |
| vsr arr1=arr.splice(1);         | 删除到尾部  返回被删除的元素数组                             |
| vsr arr1=arr.splice(-1);        | 从后向前删除  返回被删除的元素数组                           |
| var arr1=arr.splice(-2);        | 从数组的倒数第二位开始截取到尾部  返回被删除的元素数组       |
| var arr1=arr.splice(-2，3);     | 从数组的倒数第二位删除三个元素  返回被删除的元素数组         |
| var arr1=arr.splice(2,2);       | 从第二位开始删除2个元素  返回被删除的元素数组                |
| var arr1=arr.splice(2,0,12,14); | 插入元素12,14  插入在第二位开始  改变原数组 无返回值         |
| var arr1=arr.splice(2,2,34,12); | 替换元素，删除两位并且插入12,14  改变原数组 无返回值         |
| var arr1=arr.splice(1,0,0);     | 在第一位插入一个元素0，不删除，返回空数组   改变原数组 无返回值 |

***重构属性***
		

```javascript
var arr=[3,6,8,3,7,9];
		function splice(arr,start,count) {
			//创建个数组，用于存放，为返回的数组
			var a=[];
			//将参数转换成数值型保证参数的正确性；
			start=Number(start);//2     从什么位置开始
			count=Number(count);//1      删除几位
			//判断参数的值是不是数值型，如果不是 就返回这个a数组
			if(isNaN(start)) return a;
			//如果有参数并且大于零 参数就等于数组的最大长度  
			if(start<0) start+=arr.length;//8
			//判断参数的值是不是数值型，count就被赋值为arr数组的
			//最大长 度减掉start（从什么位置开始）（count：删除多少元素）
			if(isNaN(count)) count=arr.length-start;//4
			
			//start=8，arr.length=6  count=1  
			for (var i = start,j=0; i < arr.length; i++,j++) {
				//push：在数组尾部添加一个或者多个新元素，并返回数组的新长度
				//
				if(j<count)a.push(arr[i]);
				arr[i]=arr[i+count];
			}
			//arguments.length-3=6  参数第三位之后的参数长度，使arr数组长度加参数长度
			for (var k = 0; k < arguments.length-3; k++) {
				for (var h = arr.length-1; h >=start+k; h--) {					
					arr[h+1]=arr[h];
				}
			}
			//
			for (var n = 3; n < arguments.length; n++) {
				//从参数第三位开始的，值付给 arr数组 从第 start（2）开始，依次赋值 长度增加
				arr[start+n-3]=arguments[n];
				
			}
			console.log(arr);
			//删除arr数组的长度count（1）
			for (var s = 0; s < count; s++) {
				arr.length--;
			}
			return a;
		}
		var arr1=splice(arr,2,1,12,13,12,24,12,12);
		console.log(arr1,arr);
```

##### （2）slice（）


1. 从一个已知数组返回选定的元素
2. 不会改变原数组
3. var arr1=arr.slice(从什么位置开始，截取到什么位置之前);
4. 返回被截取的元素数组  不会改变原数组

**属性详解：**

| 用法                   | 详解                                                         |
| ---------------------- | ------------------------------------------------------------ |
| var  arr1=arr.slice(); | 复制原数组到新数组没有引用关系，可以复制数组var arr1=arr.splice(0) 一样 |
| var arr1=arr.slice(1); | 从第几项复制到尾部                                           |
| var arr1=arr.slice(-2)  2;| 从倒数第二位复制到尾部|
| var arr1=arr.slice(2,3);| 从第二位复制到第三位之前，不包括第三位只复制第二位|
| var arr1=arr.slice(-3,-1);| 从倒数第三位复制到倒数第一位之前|
| var arr1=arr.slece(2,-1);| 正数第二位到倒数第一位之前|

***重构属性***

```javascript
var arr = [3, 6, 8, 3, 7, 9];   
1、
		function slice(arr, start, end) {
			//转换成数值型
			start = Number(start);
			end = Number(end);
			//不是数值型  start=0
			if (isNaN(start)) start = 0;
			//不是数值型 end为arr数组的长度
			if (isNaN(end)) end = arr.length;
			//
			//start, end有参数
			//start  arr数组长度加上实参；
			if (start < 0) start = start + arr.length;
			//arr数组长度加上实参；
			if (end < 0) end = end + arr.length;
			var a = [];
			//若，start，end都没有填则，复制一个arr数组，为a
			//start, end有参数
			//start, end有参数   索引值为start（2）开始，索引值为end（4）之前结束不包括索引为4；
			for (var i = start, j = 0; i < end; i++, j++) {
				//i=2,j=0     i < 4
				//......
				//a[0] = arr[2];
				//arr数组2-4之间的值赋值给a数组；
				a[j] = arr[i];
			}
			return a
		}

2、
   function slice(arr,start,end){
        if(start===undefined) start=0;
        if(end===undefined) end=arr.length;
        start=Number(start);
        end=Number(end);
        if(!isNaN(end) && isNaN(start)) start=0;
        if(isNaN(start)) return [];
        if(start<0) start=arr.length+start;
        if(end<0) end=arr.length+end;
        var arr1=[];
        for(var i=start;i<end;i++){
            arr1[i-start]=arr[i];
        }
        return arr1;
    }


		var arr1 = slice(arr, 2, 4);
		console.log(arr1, arr);
```

### 4 数组索引方法

##### （1）indexOf（）

1. 查找元素在数组中的下标，如果么有查找到就返回-1；
2. indexOf（）参数是查找的元素 
3. indexOf(要搜索的元素,从第几个下标开始搜索）


**重构函数**

```javascript
   function indexOf(arr,search,index){
            if(index===undefined) index=0;
            for(var i=index;i<arr.length;i++){
                if(arr[i]===search) return i;
            }
            return -1;
        } 
```



##### （2）lastIndexOf（）

1. arr.indexOf(查找的元素，从第几位开始查找被包含);
2. 从后向前查找


**应用：**

```javascript
var arr=[1,2,2,4,3,4,5,4,2,6,2,7];
	
	//
	var index=-1;
	//查找元素2，查到就返回索引值
	while (~(index=arr.indexOf(2,index+1))){
		console.log(index);
	}
```

```javascript
if (~indexof(2)) {   //找到2进去
				
			}
```

##### （3）fill(（）

1. 填充方法用于将一个固定值替换数组的元素。
2. fill（）只能用于有长度的数组，如果不给与开始位置和结束位置，就会全部填充覆盖	
3. fill（） 参数是要填充的值
4. fill(要填充的值,从什么位置开始,到什么位置之前结束);


**应用**

```javascript
//创建一个长度为五的空数组
var arr=new Array(5);
//给每个属性赋值为10
arr.fill(10);
console.log(arr);//Array(5) [ 10, 10, 10, 10, 10 ]
```





​			 

# Ⅱ - 贰 -数组遍历

## 一 四种遍历数组

| 遍历     | 说明                                 |
| -------- | ------------------------------------ |
| for      | 遍历数组                             |
| for in   | 循环可以吧数组的可枚举属性遍历到     |
| forEachr | 不遍历空数组，也不遍历属性           |
| Map      | 结果返回到新数组中可以进行数值的递增 |

### 1  for,for in

**for in:循环可以吧数组的可枚举属性遍历到，不能遍历数组的空元素。**


```javascript
   var arr=[1,2,3,,4,5,6];
for(var i=0;i<arr.length;i++){
    console.log(i,arr[i]);
}
// for in 循环可以把数组的可枚举属性遍历到
// for in不能遍历到数组的空元素
for(var prop in arr){
    console.log(prop,arr[prop]);
} 
```

**in  判断键值是否 存在**

```javascript
for(var i=0;i<arr. length;i++){
// console. log(arr[i]===undefined);
console.1og(i in arr);
}
```

可以判断对象中这个key对应的值是否存在，
在数组中下标就相当于对象中的key，可以判断他的对应值是否存在

**for  和for in**

数组使用for循环遍历，会将所有下标遍历，不遍历数组的对象属性
但是会遍历到空元素，遍历是下标都是数值


数组使用for in循环遍历，会将所有的可枚举属性遍历，如果该属性
没有值就不遍历，例如数组中下标为空元素的，就不会被遍历，但是
数组的对象属性会被遍历，遍历时都是将下标转换为字符串



### 2 forEach:

1. 不遍历空数组，也不遍历属性，foreach是匿名函数，无法阻止，循环中断，循环跳出。
2. forEach不能返回任何内容
3. 和for in 比较 不会遍历到数组的属性
4. 和for比较，不会遍历空元素
5. 缺点是 会改变  this 的指向


```javascript
var arr = [2, 4, 6, 8, 10, , 12, 14, 16, 18, 20];
//item:；index：索引值
//用法：
arr.forEach(function (item,index,a) {
	console.log(item,index,a.length);
})
```

***重构属性，桥接模式***

```javascript
1、
function forEace(arr,fn) {
	for (var i = 0; i < arr.length; i++) {
		//如果没有值就跳出这次循环进入下一次循环
		if(arr[i]===undefined) continue;			
		//递归
		fn(arr[i],i,arr);
	}
}
2、
 function forEach(arr,fn){
            for(var i=0;i<arr.length;i++){
                if(i in arr) fn(arr[i],i,arr);
            }
        } 


//执行函数。
//这种称之为   桥接模式
forEach(arr,function (item,index,a) {
	console.log(item,index,a);
})
```

### 3 Map

1. 遍历数组，并且使用return 返回元素，这些被返回的元素会被放在一个新数组中
2. 新数组的长度和原数组长度相同


***用法：***

```javascript
var arr = [2, 4, 6, 8, 10 , 12, 14, 16, 18, 20];

var a=arr.map(function (item,index,a) {
	// console.log(item,index,a);
	return item+100;//a[102,104,106,108...]
})
console.log(a);
```


**重构属性**

```javascript
var arr = [2, 4, 6, 8, 10 , 12, 14, 16, 18, 20];
1、
	function map(arr,fn) {
		//创建个空数组，用于储存返回的数组
		var a=[];
		//遍历数组
		for (var i = 0; i < arr.length; i++) {
			//数组中没有值，则跳出本次循环进入下次循环
			if(arr[i]===undefined) continue;
			//
			a[i]=fn(arr[i],i,arr);
		}
		return a;
	}
2、
   function map(arr,fn){
            var arr1=[];
            for(var i=0;i<arr.length;i++){
                if(i in arr) arr1[i]=fn(arr[i],i,arr);
            }
            return arr1;
        }



	//执行函数
	var a=map(arr,function(item,index,a) {
			return item+100;
	});
	 console.log(a);
```


### 4 forEach和map的区别

区别在于 

1. forEach没有返回值

2. map 有返回值



## 二 数组属性遍历方法（es6）

以下属性都用到了桥接模式，现在先简单的介绍一下桥接模式

Gof的定义，桥接模式的作用在于“将抽象与其实现隔离开来，以便二者独立变化“。这种模式对javascript中常见的事件驱动的编程有裨益。



##### （1）some（）

 对数组的每个元素判断是否满足条件，如果都不满足就返回false，如果有一个满足的就返回true，并且不再判断后面的内容

**用法：**

```javascript 
 //some：遍历数组，查找是否有满足条件（返回结果如果是true）
	//用法：
	 var arr=[1,2,3,4,5,6];
	var bool=arr.some(function(item,index,a){
	    return item>4;
	})
	console.log(bool);//true
```

**重构属性**

```javascript
var arr=[1,2,3,4,5,6];
1、
function some(arr,fn) {
	for (var i = 0; i < arr.length; i++) {
		if(arr[i]===undefined) continue;
		if(fn(arr[i],i,arr)) return true;
	}
	return false;
}
2、
function some(arr,fn){
            for(var i=0;i<arr.length;i++){
                if(i in arr && fn(arr[i],i,arr)) return true; 
            }
            return false;
        }

//执行
var bool=some(arr,function (item) {
	return item>4;
});
console.log(bool);
```

##### （2）every（） 

对数组的每个元素判断是否满足条件，如果有一个不满足条件就返回为false，全部满足时返回true
***用法:***

```javascript
var arr = [1, 2, 3, 4, 5, 6];
var bool = arr.every(function(item) {
	return item > 4;
});
console.log(bool); //false
```

**重构属性**

```javascript
var arr = [1, 2, 3, 4, 5, 6];
1、
function every(arr, fn) {
	for (var i = 0; i < arr.length; i++) {
		if (!fn(arr[i], i, arr)) return false;
	}
	return true;
}
2、
  function erery(arr,fn){
            for(var i=0;i<arr.length;i++){
                if(i in arr && !fn(arr[i],i,arr)) return false; 
            }
            return true;
        }



//执行
var bool = every(arr, function(item) {
	return true;
})
console.log(bool);
```

##### （3）filter（）

1. 方法创建一个新数组,其包含通过所提供函数实现的测试的所有元素，原数组的每个元素传入回调函数中，回调函数中有return返回值，若返回值为true，这个元素保存到新数组中；若返回值为false，则该元素不保存到新数组中；
2. 筛选 数组
3. 返回的是数组    注意 是有下标获取
4. 原数组不发生改变。不会改变原数组
   	

**应用：**
1

```javascript
var arr=[1,2,3,4,5,6,7];
var arr1=arr.filter(function (item,index,a) {
	//返回数组中大于四的值
	return item>4;
})
console.log(arr1);
```

2

```javascript
    var data=[
    {id:1001,icon:"img/1.png",name:"餐饮0",num:1,price:10},
    {id:1002,icon:"img/2.png",name:"餐饮1",num:1,price:20},
    {id:1003,icon:"img/3.png",name:"餐饮2",num:1,price:30},
    {id:1004,icon:"img/4.png",name:"餐饮3",num:1,price:40},
    {id:1005,icon:"img/5.png",name:"餐饮4",num:1,price:50},
    {id:1006,icon:"img/6.png",name:"餐饮5",num:1,price:60},
    {id:1007,icon:"img/7.png",name:"餐饮6",num:1,price:70},
    {id:1008,icon:"img/8.png",name:"餐饮7",num:1,price:80},
    {id:1009,icon:"img/9.png",name:"餐饮8",num:1,price:90},
    {id:1010,icon:"img/10.png",name:"餐饮9",num:1,price:100}
];

//执行1
var arr=data.filter(function(item){
    return item.price>60;
})
console.log(arr);
//执行2
    var item=data.filter(function(item){
        return item.id==1006;
    })[0];
    console.log(item);
```

执行1结果为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200101141532188.png)
执行2结果为：
![在这里插入图片描述](https://img-blog.csdnimg.cn/20200101141846992.png)
**重构属性**

```javascript
var arr=[1,2,3,4,5,6,7];
1、
function filter(arr,fn) {
	var a=[];
	for (var i = 0; i < arr.length; i++) {
	//执行后将会被挂起，执行匿名函数判断条件是否为true，若是将在a数组尾部添加上arr数组当前值
		if(fn(arr[i],i,arr)) a[a.length]=arr[i];
	}
	return a;
}
2、
function filter(arr,fn) {
    if(arr.length===0) return arr1;
	var arr1=[];
	for (var i = 0; i < arr.length; i++) {
	
		if(fn(arr[i],i,arr)) arr1.push(arr[i])
	}
	return arr1;
}


//执行
var arr1=filter(arr,function (item) {
	return item>3;
});
console.log(arr1);//Array(4) [ 4, 5, 6, 7 ]
```

##### （4）reduce（）

 1. 如果没有设置初始值，上次归并值初始值为数组的第0项，本次遍历将从下标1开始。遍历的第二次时候value就是就会是上次return返回的值

 2. 如果设置了初始值，上次归并值初始值是初始化值，本次遍历将从下标0开始

 3. 形成一个对象,不仅仅限于求和，可以return所有单个体对象

 4. 当数组的每个元素完成后将会把最后一次的返回值返回到外面

 

​    


**应用：**

```javascript
var arr = [1, 2, 3, 4, 5];
//(上次归并的值，本次遍历的元素，索引值，数组)
var sum = arr.reduce(function(value, item, index, a) {
	//    console.log(value,item);
	//    return 10;
	console.log(value, item);
	return value + item;
}, 100);//100 为初始值
console.log(sum);


//  最大值  最小值
   var arr=[1,2,3,40,5,6,7];
        var obj=arr.reduce(function(value,item){
            if(value.max==undefined) value.max=item;
            if(value.min==undefined) value.min=item;
            if(value.max<item) value.max=item;
            if(value.min>item) value.min=item;
            return value;
        },{});  //初始值为{}  及 value是{}
        console.log(obj);


```

**构造属性**

```javascript
var arr = [1, 2, 3, 4, 5];
function reduce(arr,fn,initValue) {
	var start=0;
	
	if(initValue===undefined){
		initValue=arr[0];
		start++;
	}
	for (var i = start; i < arr.length; i++) {
		initValue=fn(initValue,arr[i],i,arr)
	}
	return initValue;
}
//执行
var sum=reduce(arr,function (value,item) {
	return value+item;
});
console.log(sum);
```


## 三 案例

### 1 随机乱序生成验证码

```javascript
var arr=[1,2,3,4,5,6,7,8];
        arr.sort(function(a,b){
            // 随机生成0-1直接的浮点数，不包括1
            return Math.random()-0.5
        });
        console.log(arr); */

      /* function getSecurityCode() {
        var arr = [];
        var i = 47;
        while (i++ < 122) {
          if (i > 57 && i < 65) continue;
          if (i > 90 && i < 97) continue;
          arr.push(String.fromCharCode(i));
        }
        arr.sort(function(){
            return Math.random()-0.5;
        });
        arr.length=4;
        return arr.join("");
      }

      console.log(getSecurityCode()); 
```

### 2 全选按钮

HTML

```javascript
    <input type="checkbox" id="all" /><label for="all">全选</label><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
    <input type="checkbox" /><br />
```

js

```javascript
var all,list;
        init();
        function init(){
            list=document.getElementsByTagName("input");
            list=Array.from(list);
            all=list.splice(0,1)[0];
            all.onclick=clickHandler;
            list.forEach(function(item){
                item.onclick=clickHandler;
            })
        }

        function clickHandler(){
            // console.log(this);//在点击事件中this是被点击的元素
            if(this===all){
                list.forEach(function(item){
                    item.checked=all.checked;
                })
            }else{
                all.checked=list.every(function(item){
                    return item.checked;
                })
            }
        } 
```



# Ⅲ - 叁 -数组排序

## 一 数组排序属性

### 1 reverse倒序

1. 只倒序，不排序
2. 原数组改变，返回原数组

***用法：***

```javascript
 var arr=[1,4,6,2,3,8,7,6,5,3,9];
 arr.reverse();
 console.log(arr);//Array(11) [ 9, 3, 5, 6, 7, 8, 3, 2, 6, 4, … ]
```

```javascript
var arr=["a","b","c","d"];
 arr.reverse();
 console.log(arr);//Array(4) [ "d", "c", "b", "a" ]
```

**重构属性**

```javascript
	var arr=[1,4,6,2,3,8,7,6,5,3,9];
	1、
function reverse(arr){
     var len=parseInt(arr.length/2);
     for(var i=0;i<len;i++){
         // arr[arr.length-1-i]=arr[i];
         var temp=arr[arr.length-1-i];
         arr[arr.length-1-i]=arr[i];
         arr[i]=temp;
     }
     return arr;
 }
 2、
  function reverse(arr){
           var arr1=[];
           for(var i=0;i<arr.length;i++){
               if(i in arr){
                  arr1[i]=arr[i];
               }
           }
           arr.length=0;
           for(var j=arr1.length-1;j>=0;j--){
                if(j in arr1){
                  arr[arr1.length-j-1]=arr1[j];
               }
           }
           return arr;
        }

 reverse(arr);

 console.log(arr);
```

### 2 sort排序

1. 方法用于对数组的元素进行排序。对数组的引用。
2. 会改变原数组

***用法***
sort解决方案：

```javascript
var arr=[1,4,6,2,3,8,7,6,5,3,9,10];
         arr.sort();//bug，不可以直接用
        arr.sort(function(a,b){
            //return a-b;//升序
            return b-a;//降序
        })
         console.log(arr);
```

```javascript
//随机排列0-100个数
var arr=[];
for(var i=0;i<100;i++){
    arr.push(i);
}
arr.sort(function(){
    return Math.random()-0.5;
});
console.log(arr);
```

## 二 三种数组排序 

### 1 冒泡排序：

1、从后向前循环
2、内部从前向后循环到外层变量
3、判断前值是否大于后值，交换

```javascript
 var arr=[1,4,6,2,3,8,7,6,5,3,9,10];
function sort(arr) {
	var len=arr.length;
	while(len>0){
		for (var i = 0; i < len; i++) {
			if(arr[i]>arr[i+1]){
				var temp=arr[i];
				arr[i]=arr[i+1];
				arr[i+1]=temp;
			}
		}
		len--;
	}
}
//执行
sort(arr);
console.log(arr);
```

### 2 选择排序

   先找出最小或者最大的索引值，然后用当前的下标的元素与这个最小的元素交换
        1、遍历数组
        2、设置最小的索引值为当前的索引值
        3、从当前的下一项开始遍历到数组的尾部
        4、判断所有遍历的值中最小的值得索引值
        5、交换当前值和最小索引值的元素

```javascript
function sort(arr) {
	var mIndex;
	for (var i = 0; i < arr.length; i++) {
		mIndex=i;
		for (var j = i+1; j < arr.length; j++) {
			mIndex=arr[mIndex]<arr[j]?mIndex:j;
		}
		var trmp=arr[i];
		arr[i]=arr[mIndex];
		arr[mIndex]=trmp;
	}
}
//执行
sort(arr);
console.log(arr);
```

### 3 快排(快速排序)

	        1、删除数组中间的元素，并且，将这个元素返回一个变量
	        2、创建两个空数组，一个是left，一个是right，遍历这个数组，将
	        小于中间元素的数据存入left，大于中间元素的数据存入right
	        3、将left数组递归与中间元素和right数组递归的结果合并返回
	        4、在函数最顶部，一定要写数组长度小于等于1，返回该数组

```javascript
var arr = [1, 4, 2, 2, 3, 10];
//把结果赋值给arr数组；
arr = sort(arr);
function sort(arr) {
	//这个数组长度小于一则返回这个数组
	if (arr.length <= 1) return arr;
	var left = [];
	var right = [];
	//
	var item = arr.splice(parseInt(arr.length / 2), 1)[0];
	for (var i = 0; i < arr.length; i++) {
		//如果arr[i]的值
		//小于item的值 把arr[i]这个值追加到left这个数组的尾部
		//大于item的值 把arr[i]这个值追加到right这个数组的尾部
		if (arr[i] < item) {
			left.push(arr[i]);
		}else{
			right.push(arr[i]);
		}
	}
	//把两个数组通过concat()数组属性拼接起来，返回新数组
	var arrtow=sort(left).concat(item,sort(right));
	return arrtow;
}
//执行
sort(arr);
console.log(arr);
```

# Ⅳ - 肆 - 数组去重

## 一 普通去重

```javascript
 var arr=[1,2,2,4,3,4,5,4,2,6,2,7];
				 var arr1=[];
				 //循环arr数组
				 for (var i = 0; i < arr.length; i++) {
				 	var bool=false;
					//第二次  arr[1]的值传递给arr 数组  长度为1 进入循环
					for (var j = 0; j < arr1.length; j++) {
						//arr[1]===arr1[0]   true
						//
						if(arr[i]===arr1[j]){
							//当有值相等的时候改变bool为true  不在添加值
							bool=true;
							break;
						}
					}
					
					if(!bool){
						//第一次循环
						//为true的时候，复制arr数组到arr1
						arr1.push(arr[i]);
					}	
				 }
				console.log(arr,arr1);
```

## 二 indexOf去重

```javascript

 var arr=[1,2,2,4,3,4,5,4,2,6,2,7];
	var arr1=[];
	for (var i = 0; i < arr.length; i++) {
	//把找到的数复制给新数组
		if(arr1.indexOf(arr[i])<0) arr1.push(arr[i]);
		}
	arr=arr1.splice(0);
	arr1=null;
	console.log(arr); 

```

## 三 数组去重  indexOf  和delete

```javascript
//delete删除数组元素，不会造成数组的自动收缩，紧密，数组的长度不会发生改变
var arr=[1,2,2,4,3,4,5,4,2,6,2,7];
	for (var i = 1; i < arr.length; i++) {
		
		//indexOf找到之后会删除当前的值，依次查找，
		//从前开始查找
		if(arr.indexOf(arr[i],i+1)>-1) delete arr[i];
		//从后开始查找
		if(arr.lastIndexOf(arr[i],i-1)>-1) delete arr[i];
	}
	var arr1=[];
	//
	for (let prop in arr) {
		arr1.push(arr[prop]);
	}
	arr=arr1.splice(0);
	arr1=null;
	console.log(arr);
```

## 四 filter，indexOf去重

```javascript
   arr=arr.filter(function(item,index,arr){
                    return arr.indexOf(item,index+1)<0;
            });
      arr.join(" ");
```

## 五 indexOf 和delete 去重

```javascript
  var arr=[1,3,3,6,8,2,3,5,6,3,7,9,8,3,6,7,3,8,9];
        for(var i=0;i<arr.length;i++){
            var index=i;
            while(index>-1){
                index=arr.indexOf(arr[i],index+1);
                if(index>-1)delete arr[i];//使用delete会变成松散型数组
            }
        }
        // var arr1=arr.map(function(item){
        //     return item;
        // });
        var arr1=[];
        arr.forEach(function(item){
            arr1.push(item);
        })


        console.log(arr1); 
```

# Ⅴ - 伍  - 数组判断与转换

## 一 判断数组

```javascript
ES6:
console.log(Array.isArray(arr));
ES5:
console.log(Object.prototype.toString.call(arr)==="[object  Array]");
console.log(arr.constructor===Array);
```

## 二 转化为数组

1. Array.from(); 参数为转换的实参

```javascript
Array.from();
Array.prototype.slile.call()
[].slice.call()

```

#  0 - 0 - 知识点：

### 桥接模式

链接  https://blog.csdn.net/shanyongxu/article/details/47727471

### **arguments**

ECMAScript函数不介意传递进来多少参数，也不会因为参数不统一而错误，实际上，函数体内可以通过arguments对象来接收传递进来的参数。
arguments对象的length属性可以得到参数的数量
我们可以利用length这个属性，来智能的判断有多少参数，然后把参数进行合理的应用，比如，要实现一个加法运算，将所有传递来的数字累加，而数字的个数又不确定。

### 数组与JSON 字符串之间的转换

JSON.stringify()的作用是将 JavaScript 对象转换为 JSON 字符串，而JSON.parse()可以将JSON字符串转为一个对象。
简单点说，它们的作用是相对的，我用JSON.stringify()将对象a变成了字符串c，那么我就可以用JSON.parse()将字符串c还原成对象a。

### 数组属性归纳

| 数组属性      | 说明                                                         |
| ------------- | ------------------------------------------------------------ |
| unshift()     | 向数组的开头添加一个或更多元素，并返回新的长度               |
| push()        | 向数组的末尾添加一个或者更多元素，并返回新长度               |
| pop()         | 删除并返回数组的最后一个元素                                 |
| shift         | 删除并返回数组的第一个元素                                   |
| join()        | 把数组的所有元素放入一个字符串。元素通过指定的分隔符进行分割 |
| concat()      | 连接两个或更多的数组，并返回结果。复制，给新数组添加新元素   |
| splice ()     | 删除元素，并向数组添加新元素                                 |
| slice()       | 从某个已有的数组返回选定的第一个元素                         |
| indexOf()     | 查找元素在数组中的下标，如果么有查找到就返回-1               |
| lastIndexOf() | 从后向前查找                                                 |
| reverse()     | 颠倒数组中元素的顺序                                         |
| sort()        | 对数组进行排序，方法用于对数组的元素进行排序。对数组的引用。会改变原数组 |
| es6           | es6                                                          |
| some()        | 对数组的每个元素判断是否满足条件，如果都不满足就返回false，如果有一个满足的就返回true，并且不再判断后面的内容 |
| every()       | 对数组的每个元素判断是否满足条件，如果有一个不满足条件就返回false，全满足时就返回true |
| reduce()      | 方法对累加器和数组重点每个元素（从左到右）应用一个函数，将其简化为单个值 |
| filter()      | 方法创建一个新数组,其包含通过所提供函数实现的测试的所有元素，原数组的每个元素传入回调函数中，回调函数中有return返回值，若返回值为true，这个元素保存到新数组中；若返回值为false，则该元素不保存到新数组中；原数组不发生改变。 |
| fill()        | 方法用于将一个固定值替换数组的元素                           |