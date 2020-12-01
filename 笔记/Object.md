# Object

## 原型链

_proto _  这是除null外的每一个对象都会有的属性，这个属性指向该对象的原型

对象的原型指向另一个对象，本对象的属性继承自他的原型对象

通过关键字new和构造函数调用创建的对象的原型就是构造函数的prototype属性的值

constructor：每个原型都有这个属性，指向该关联的构造函数

原型链是指每个对象都有自己的原型_proto _ ，而这个原型也有自己的·原型，从而形成的链叫原型链

## 对象的创建

##### 对象：万物皆对象

任何的对象的原型都是对于上级对象的引用

不允许直接修改原型链的属性

所有对象中的key必须是String或者Symbol类型，如果不是就会隐式转换为string

```js
var o={a:1};//字面量创建
var o1=Object.create(o)

var o={a:1};
var o1=Object.create(o);
var o2=Object.create(o);
//以o为原型创造o1，o1的原型指向o，相当于引用同一个地址。

var a=Object.create(null);
console.log(a);//No properties
```

当设置对象属性时。直接设置的是对象的自身属性（对象属性）

如果获取时，首先查看该对象有没有这个名称的对象属性，如果有直接返回这个属性的值，如果没有向下查找紧邻的原型链中的属性是否具有该属性名，查找到距离该对象最近的原型链中属性名后返回其值

Object.create()使用它创建新对象，第一个参数为这个对象的参数。这是一个静态函数，使用时只需传入所需的原型对象即可。可以通过传入参数null来创建一个没有原型的对象，通过这种方法创建的对象不能继承任何东西，包括基础方法，例如toString()

创建对象时不要使用var obj=Object.create({})      因为创建时相当于创建了两层object原型

在对象的属性下，this将指向对象外的this指向

所有的类型都有toString，任何类型都有constructor

## 对象的属性操作

### assign(浅复制)

```js
var o={a:1,b:2};
var o1=Object.assign({},o)
```

创建一个新对象，并且将o上的属性复制到这个新对象上，然后返回这个新的对象

浅复制是指仅把第一层的属性复制到新对象上，如果第一层的属性值可引用类型，则会把引用地址赋值

Object.assign()  将一个或者多个对象中的可枚举属性复制到第一层时，如果后面的对象属性与前面的对象属性相同时，则会覆盖前面对象的属性值

Object.assign()是在原对象中增加复制的属性，引用地址不变

#### Object.assign()与Object.create()的区别

Object.assign(target,...sources)方法用于将自身所有可枚举属性（继承而来的属性不行）的值（原始类型会被包装为对象，只有字符串的包装对象才可能有自身可枚举属性）从一个或多个源对象复制到目标对象（不会跳过值为null或undefined的源对象），并且返回一个新的目标对象（目标对象自身也会被改变）。

Object.create(proto,[propertiesObject])创建一个新对象，使用现有的对象来提供新创建的对象的_proto_原型，第二个参数是添加到新创建的对象的可枚举属性（是自身的属性，不是原型链上的属性）对象的属性描述符以及相应的属性的名称，属性分成数据属性（configurable\writable\enumerable\value，除了value外，其他特性默认为false）和访问器属性(configurable\enumerable\get\set)，



### 对象属性的创建

##### Object.defineProperty()      Object.defineProperties()

```js
var obj={}
//Object.defineProperty三个参数。  对象，属性，该对象的描述对象
Object.defineProperty(obj,"a",{
    configurable:true,//该属性是否可以被删除，并且该属性的描述对象是否可以更改
    enumerable:true,//该对象是否是可枚举属性。当其为flase时，for循环循环不到，且使用.assign复制时不可复制   使用...复制时解构时也不能解构
    writable:true,//该对象是否是可写（只读）
    value:10,//值或者方法
})
```

Object.defineProperty()描述对象是可以省略的。描述属性省略时默认属性都是false。

对象对立的是空对象。空对象不在堆中占位。

想要设置属性的特性或者想要新建属性拥有某种特性，调用Object.defineProperty()方法，传入要修改的对象，要创建或者修改的属性的名称以及属性描述符的对象。



```js
Object.defineProperties(obj, {
            a:{
                enumerable:false,
                writable:true,
                configurable:true,
                value:20,
            },
            b:{
                writable:true,
                configurable:true,
                value:function(){

                }
            },
            c:{
                configurable:true,
                value:10
            }
        })
```

##### Object.freeze()冻结

```js
obj.a=10;
    obj.b=20;
    Object.freeze(obj);
    delete obj.a;
    obj.a=100;
    console.log(obj);
```

Object.freeze()可以将该对象的属性转化为静态属性。相当于是将变量转化为常量。将其设置为不可扩展，将其所有的自有属性设置为不可配置。除此之外，将所有的非继承属性设置为只读，不可操作。冻结对象是一个永久性的操作，一旦冻结就不可解除。这个方法不会影响到继承属性

注意这个方法是一个全局函数，不可以在具体的对象上调用，必须传入一个对象

#####  **Object**.getOwnPropertyNames()

获取对象的所有独有属性名，返回的是一个所有非继承属性的名字的数组，包括那些不可枚举的属性

#####  **Object**.getOwnPropertyDescriptor

获取对象的描述对象

##### Object.is（a，b）

判断a与b是否相等

```js
var a=NAN;
var b=NAN;
console.log(Object.is(a,b))//===
//和===不同在于 NAN判断NAN是相同的
```

##### **Object**.**hasOwnproperty**()

判断属性是否是自我属性，也就是不是继承来的属性 。in也可以判断

对象原型链上的属性不是他的属性

但是in是可以将当前对象和对想的原项链中所有属性都可以判断

**Object**.**hasOwnproperty**()只能判断当前对象的属性，不能判断原型链上的属性

##### .isPrototypeOf

判断前一个是不是在后面的原型链下

判断是不是html标签

```js
HTMLElement.isPrototypeOf(     .constructor())
```

##### objpropertyIsEnumberable("")

查询属性是否是可枚举属性

##### **instanceof**判断类别

type of的缺陷有时无法正确区分null与object。而instanceof则不会有这样的问题。而使用constructor也可以区别null与object，只不过这种方法在执行时会报错，影响程序的使用，并不推荐使用

### 对象深复制

```js
function cloneObj(source,target){
            if(target==undefined) target={};//如果target没有被定义，target为空
            var names=Object.getOwnPropertyNames(source);//得到原对象的自我属性的名字
            for(var i=0;i<names.length;i++){
                var desc=Object.getOwnPropertyDescriptor(source,names[i]);//获取原对象的自我属性的描述符·
                if(typeof desc.value==="object" && desc.value!==null){//判断自我属性是object且不是null
                    var obj;
                   switch(true){
                       case desc.value.constructor===Date://如果是日期
                       obj=new Date(desc.value.toString());
                       break;
                       case desc.value.constructor===RegExp://如果是正则表达式
                       obj=new RegExp(desc.value.source,desc.value.flags);
                       break;
                       case HTMLElement.isPrototypeOf(desc.value.constructor)://如果是标签属性
                       obj=document.createElement(desc.value.nodeName);
                       break;
                       default:
                       obj=new desc.value.constructor()
                   }
                    Object.defineProperty(target,names[i],{//设置复制的对象的属性
                        enumerable:desc.enumerable,
                        writable:desc.writable,
                        configurable:desc.configurable,
                        value:obj
                    });
                    cloneObj(desc.value,obj);
                }else{
                    Object.defineProperty(target,names[i],desc)//用自我属性的描述符创建一个属性
                } 
            }
            return target;
        }
```



## 函数

### 函数执行

```js
//第一种
function abc(){
    
}
abc();

//第二种
(function abc(){
    
})();

//第三种call
function fn(){
   console.log(this) 
}
var obj={a:1};
fn.call(obj);//将obj带入到函数替代函数this的指向，原来的this指向obj
fn.apply(obj);//和call一样
//如果call和apply带入的不是对象，会自动转化为对象

//求数组中最小数
var arr=[1,2,3,4,5];
            var min=Math.min.apply(null,arr);
            var Maths={
                min:function(){
                    if(arguments.length===0) return;
                    var min=arguments[0];
                    if(arguments.length===1) return min;
                    for(var i=1;i<arguments.length;i++){
                        min=min>arguments[i] ? arguments[i] : min;
                    }
                    return min;
                }
            }
            Maths.min.apply(null,arr)
```

call中的第一个参数是函数中this的指向的对象，后面会按照顺序带入·参数

apply只有两个参数，第一个参数是this指向，第二个参数是一个数组

##### call与apply的缺陷

call与apply是立即执行。所有的回调函数如果需要替换this不能使用call与apply，使用bind()

### bind()

```js
 function fn(){
            console.log(this);
        }

        var f=fn.bind({a:1});
        fn();
        f();
```

bind()作用是将函数绑定到某对象上。当在函数f()上调用bind()方法并传入一个对象o作为参数，这个方法将返回一个新的函数。

除了第一个参数外，传入this的参数也会绑定至this

通过bind可以对于回调函数传参，this就是bind绑定的内容

## this

ES5非严格模式 ，代码中全局中的this与函数中的this都指向window

ES5严格模式，ES6中，全局this仍然指向window，函数中的this指向undefined



变量会发生引用改变，而this不会因为变量改变而改变

对象没有创建完成时，this还没有生成this就指向对象外的this指向

### 回调函数中的this

只要有回调函数，不管是什么模式下this都会发生改变

1.fn()

对调函数中如果直接指向的回调函数this指向最外层的window

2.arguments()

如果通过arguments直接使用参数执行函数，this则指向当前函数的arguments

3.call，apply，bind

如果回调函数通过call，apply，bind重新指向新的对象时，this就是这个新对象

### 事件中的this

```js
var obj={
    a:function(){
     document.addEventListener("click",this.clickHandler)
    },
    clickHandler:function(e){
        console.log(this);//指向事件侦听对象，也就是e,currenttarge
    }
}
```

### ES5面向对象中的this

```js
function Box(){
    console.log(this);
}
Box.prototype.play=function(){
    console.log(this)//this指向该执行方法的实例化对象
}
Box.run=function(){
    console.log(this)//this指向Box
}

//Box()//非严格模式下指向window  严格模式下指向undefined
```

### 箭头函数

```js
var obj={
   a:function(){
       setTimeout(()=>{
           console.log(this);//this是当前箭头函数的指向
           //指向箭头函数外的上下文环境中的this
       })
   } 
}
```

### call apply  bind

```js
function fn(){
    console.log(this)
}
var obj={a:1}
fn.call(obj);//this指向obj
fn.apply(obj);//this指向obj
fn.bind(obj)//this指向obj

//如果使用call apply bind代入得是null，将会把这里的this重新指向window
```

# setter与getter

set有且仅有一个参数，将复制表达式右侧的值当作参数传入set中

get不允许有参数

```js
var obj={
            a:1,
            _c:0,
            b:function(){},
            set c(value){
                document.documentElement.style.backgroundColor=document
                "#"+value.tostring(16);
                this._c=value;
            },
            get c(){
                return this._c;
            }
        }
```

如果仅有set，没有get，这个属性就是一个只写属性

如果仅有get，没有set，这个属性就是一个只读属性

ES6常量的写法

```js
class Box{
    constructor(){
        
    }
    static get EVENT_ID(){
        return "EVENT_ID"
    }
}
```

对象在初始创建时具有set与get，当想要追加这两种属性时使用Object.defineProperty

```js
div._width=0;
            Object.defineProperty(div,"width",{
                enumerable:true,
                set:function(_value){
                    this.style.width=_value.toString().indexOf("px")>-1 ? _value : _value+"px";
                    this._width=_value;
                },
                get:function(){
                    return this._width;
                }
            });
```

如果只是为了存储，就是用属性不要使用set get

##### set get的缺陷

当给里面添加内容使用get  set时，无法使用添加删除，因为在添加删除时没有改变引用地址，无论如何操作都默认没有改变，不会进行操作

###### 对象的深比较

```js
  _data = {
        a: 1,
        b: 2,
        c: {
          a: 2,
          b: 5,
          d: {
            a: 1,
            b: 2,
            c: [1, 2, 3],
          },
        },
      };
      constructor() { }
      set data(value) {
        // console.log(this.compareData(value, this._data))
        if (this.compareData(value, this._data)) return;
        this.render();
        this._data = value;
      }
      get data() {
        return this._data;
      }
      render() { }
      compareData(target, source) {
        for (var prop in target) {
          if (typeof target[prop] === "object" && target[prop] !== null) {
            return this.compareData(target[prop], source[prop]);
          } else {
            if (target[prop] !== source[prop]) return false;
          }
        }
        return true;
      }
    }
```



 















































