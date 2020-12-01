# jQuery

jquery针对DOM处理

jQuery1.0 兼容各个浏览器

jQuery2.0不支持IE6/7/8

jQuery3.0

### jQuery的功能

1.像CSS那样访问和操作DOM

2.修改CSS控制页面外观

3.简化JavaScript代码操作

4.事件处理更加容易

5.各种动画效果使用方便

6.让Ajax技术更加完美

7。基于jQuery大量插件

8.自行拓展功能插件

### jQuery的优势

jQuery的最大优势是特别方便，jQuery代码兼容性好，不需要考虑不同浏览器的兼容问题

### jQuery对象与DOM对象的区别

jQuery对象是一个列表对象，操作内容是针对列表中的所有元素的

jQuery对象不能使用DOM的方法和事件，他的方法也是针对jQuery对象使用的DOM对象不能使用

将jQuery转换为DOM元素

```js
$("div")[0]
```

获取jQuery对象的DOM数组

```
$("div").get()
```

将DOM转换为jQuery,

```js
$(div)
$(divs)//多个元素转换
```

如果希望将DOM转换为jQuery直接放在$（）函数中就可以

```js
 var div=document.querySelector("div");
    //  console.log( $(div));
```

将nodeList或者HTMLCollection转换为jQuery列表

将jQuery列表中第几个元素筛选出jQuery新对象

```js
  console.log( $("div").eq(0));
```



### jQuery选择器

标签名选择器$("div")

id选择器$(#div1)

class选择器$(".div0")

通配符选择器$("*")

后代选择器$("div.div1")

子代选择器$("div>div1")

下一个兄弟选择器$(".div+div")

下面所有的兄弟选择器$(".div~div")

```js
$("div.div1");//div中类名是div1的div
$("div .div1")//div后代中类名是div1的元素
$(".div1>*");//类名是div1所有的子元素
conloge.log($(".div1>*").length);//div1子元素的数量
conloge.log($(".div1>*").length);//div1子元素的数量
$(".div+*")//div1下一个任意兄弟元素
$(".div+")//div1下一个任意兄弟元素

$(".div1").next();//等同于$(".div1+")  下一个兄弟元素
$(".div1").nextAll();//等同于$(".div1~")  标记元素后面的所有兄弟元素
$(".div1").nextUntil(".div2")//div1到div2之间的所有兄弟元素

$(".div1").prev();//向上的一个兄弟元素
$(".div1").prevAll();//向上的所有兄弟元素
$(".div1").prevUntil(".div2");//向上到div2的所有兄弟元素

$(".div1").find("span");//等同于$(".div1  span")    div1中的span元素
$(".div1").children();//相当于$(".div>");   div1的所有子元素
```

##### 属性选择器

```js
console.log($("div[a]"));//[a]表示是否具备标签属性a
conloge.log($("[a]"))//表示具备标签属性a
conloge.log($("[a=1]"));//标签必须具备a属性，并且属性值为1
conloge.log($("[a^=1]"));//属性值开头是1的元素
$("[b|=ab]").css("color","red");//值是ab或者以ab起头的后面使用-来连接的元素
$("[b~=ab]").css("color","red");//值是ab或者以空格分隔内容中包括ab的元素

//一般用于Class的多个样式选择
$("[b$=b]")//值以b结尾的元素
$("[b!=-ab]")//值不是ab的元素
$("[b*=c]");//值中包含c这个字符的元素
$("[a][b]");//有属性a和属性b的元素
```

### jQuery过滤器

```js
//将所有li放在一个列表中筛选出第一个元素
$("li:first").css()
$("li").first()
$("li:first-child").css()//选择每个li中父元素中的第一个子元素，如果是li的筛选出来
$("li:first-of-type").css()//将每一个li父元素中的第一个li类型的子元素筛选出来

//将所有li放在一个列表中，筛选出最后一个元素
$("li:last")
$("li").last()
$("li:last-child")//选择每个li中父元素中的最后一个子元素，如果是li的筛选出来
$("li:last-of-type")//将每一个li父元素中的最后一个li类型的子元素筛选出来

$("ul>:not(li)")//ul所有子元素中不是li元素的
$("ul>").not("li")//等同于上面的
$("li:even")//li的父元素的子元素列表的偶数项，这种是从0开始计数的
$("li:odd")//li的父元素的子元素列表的奇数项

$("li:nth-child(2)").css("color","red");//将每个li父元素中的第二个元素筛选出来
$("li:nth-of-type(3)").css("color","red")//将每个li父元素中第三个li筛选出来
$("li:nth-child(even)")//li的父元素的子元素列表的偶数项，列表从1开始计数
$("li:nth-of-type(even)")//li的父元素中的所有li组成一个列表中的偶数项，列表从1开始计数
$("li:nth-child(odd)")//li的父元素的子元素列表的奇数，列表从1开始技术
$("li:nth-of-type(odd)")//li的父元素中的所有li组成一个列表中的奇数项列表从1开始计数
$("li:nth-child(2n)")//li的父元素的子元素的偶数项，列表从1开始计数
$("li:nth-child(2n-1)")//li的父元素的子元素的奇数，列表从1开始计数
$("li:eq(2)").css("color","red");//选出li父元素的子元素列表中的第二个子元素，并将第一个父元素中的筛选出来，列表从0开始计数
$("li").eq(2)
$("li:gt(2)").css("color","red");//将所有的li放在一个列表中。筛选出列表中下标大于2的所有元素
$("li:lt(2)").css("color","red");//将所有的li放在一个列表中。筛选出列表中下标小于2的所有元素

$(":header");//所有h1-h6的元素
$(":animated");//所有使用aniamte动画的元素
$(":focus"); //聚焦元素
console.log( $(":empty"));//没有内容或者子元素的元素
console.log($(".div1:has(.div2)"));//含有div2的内容的div1元素
console.log($(".div2:parent"));//判断div2有子元素的或者有内容的
$(".div2").parent()//获取div2的父元素
$(".div2").parents()//获取div2的所有父元素
$(".div2").parentsUntil("html")//获取div2的所有父元素中到什么之前的
$(".div1:contains(1)")//判断元素的后代中有1这个内容的元素
$(".div4:hidden")//隐藏元素，针对display:none或者是不显示的元素         visibility: hidden;不是隐藏，因为它占位了
$(":visible")//显示元素
$(":only-child") //只有一个子元素的元素
$("div").is(".div1")//这个方法得到一个布尔值，是否在div中有类名是div1的元素
$("div").hasClass("div1")//这个方法得到一个布尔值，是否在div中类名是div1的元素
$("li").slice(2,4)//div列表中选择从第2个到第4个之前的元素
$(":input")//
$(":text");//type=text的input
$(":password");

$(":disabled");//不可用
$(":enabled");//可用
$(":checked");//用于input中checkbox和radio
$(":selected");//用于下拉菜单的元素
```

### jQuery遍历

```js
var arr=[1,2,3,4];
        $.each(arr,function(index,item){
            console.log(index,item);
        });

var obj={a:1,b:2,c:3};
        $.each(obj,function(key,value){
            console.log(key,value);
        }) 

//静态方法
 $.each($("div"),function(index,item){
            console.log(index,item);
        })
//实例化元素方法
 $("div").each(function(index,item){
            console.log(index,item);
        })
```

### jQuery内容

```js
$("div").html("");//div.innerHTML=""
$("div").html("<span>你好</span>");//增加span元素
console.log($("div").html());//获取列表中第一个元素的内容
console.log( $("div").text());//将所有列表中的元素的内容和为一个字符串返回
$("div").text("你好");//为每个div添加相同内容

//为每个div添加不同的内容
var arr=["北京","上海","深圳","天津"];
        $("div").text(function(index){
            return arr[index];
        })

//将每次输入的内容打印出来
$("input").on("input",function(){
            console.log($(this).val());
            // console.log(this.value)
        }) 


 $("input").val(10);//将每个input的内容都添加为10

//为每个input的内容添加为当前index+1
$("input").val(function(index){
            return index+1;
        })
```



### jQuery属性

attr     prop    data   

attr是设置在DOM标签上的属性

prop是设置在DOM对象上的属性

data是在设在jQuary映射对象上的属性，为了不污染DOM对象属性

```js
console.log($("div").attr("a"))//只能获取到列表中第一个元素a的属性值
 $("div").attr("b","10");//为每个div添加一个b的属性属性值为10

//为每个div添加一个c的属性，属性值为当前index+1
$("div").attr("c",function(index,item){
        return index+1;
    })

//为div设置不同的属性
 $("div").attr({
        b:"1",
        c:function(index,item){
            return index+1;
        }
    })

$("div").prop("b",10);//设置了jQuery列表中所有DOM的对象属性增加b
console.log($("div").prop("b"));//从列表中取第一个元素的DOM对象属性b的值

//多选框
$(":checkbox").attr("checked","checked")
    .on("click",function(){
        $(this).removeAttr("checked");
    }) 

$("div").data("abc",10);//设置在一个jQuery映射对象上
$("div").removeAttr("a");//删除jQuery列表中所有DOM的对象属性的a属性
```

### jQuary的CSS样式

```js
为每一个div的class添加一个div1$("div").css("width",50);
$("div").css("width","50px");
$("div").css("width","50");//都能设置宽度

//设置div的宽度为index+1再乘以50
$("div").css("width",function(index,item){
    return (index+1)*50
})
//不但可以获取行内样式的值，也可以获取css设置计算后的样式
cosole.log($("div").css("width"))

console.log($("div").css(["width","height",
                          "backgroundColor"]));// 获取第一个元素的指定样式值，返回一个对象
 $("div").addClass("div1");//为每一个div的class添加一个div1
 $("div").addClass("div1 div2");//为每个div的class添加一个div1 div2
 $("div").removeClass("div1");//为每一个div的class删除一个div1
$("div").removeClass("div1 div2");//为每个div的class删除一个div1 div2

//当点击时删除原有的div
 var bool=false;
        $("div").on("click",function(){
            bool=!bool;
           if(bool) $(this).removeClass("div1").addClass("div2");
           else $(this).removeClass("div2").addClass("div1");
        }) 

//同上
$("div").on("click",function(){
            $(this).toggleClass("div2");
        }) 

console.log($("div").width());//内容宽度width
 $("div").innerWidth(100);//设置内容宽度+padding
console.log( $("div").innerWidth())；//获取内容宽度+padding
/console.log($("div").outerWidth());//offsetWidth,width+padding+border
$("div").outerWidth(100);//设置outerWidth
 console.log($("div").outerWidth(true));//width+padding+border+margin  只能获取不能设置
console.log($(".div3").offset());//元素相对页面左上角的位置
console.log($(".div3").position());//得到的是定位位置，和offsetLeft，offsetTop  不能设置
console.log($(".div2").scrollTop())// 获取和设置滚动条位置
```

### jQuery的DOM

append

```js
$("body").append("<div></div>"); // 这种写法返回body的jQuery的对象
```

appendTo

```js
$("<div></div>").appendTo("body");
 // 这种写法返回的是div的jQuery对象
```

```js
//在每个div加入span
$("div").append(function(index,item){
            return "<span>"+index+"</span>";
        })

$("<div></div>").prependTo(".div1");
// 插入父元素的第一个子元素位置
$(".div1").prepend("<div></div>");

// 插入在兄弟元素后面
$(".div1").after("<div></div>");
$("<div></div>").insertAfter(".div1");

// 插入在兄弟元素前面
$(".div1").before("<div class='divs'></div>")
$("<div></div>").insertBefore(".div1");

$("div").wrap("<a></a>");//给每个元素外面的包裹一个a标签
$("div").wrapAll("<a></a>");//给所有元素外面包裹一个a标签
$("span").unwrap();//将包裹的父元素删除
$("div").wrapInner("<a></a>");//给每个div的内容包裹一个a标签

//复制（全是深复制）
$("div").clone(false);//false不复制事件
$("div").clone(true);//true就是连带事件一起复制

//删除元素
div.remove();//删除元素的时候会将所有元素的事件也删除注销
div.detach();//仅删除元素，事件保留
$(".div1").empty();//清除元素的所有子元素和内容

//将div1转化为a
$(".div1").replaceWith("<a></a>");
$("<a></a>").replaceAll(".div1");
```



### jQuery事件

jQuery绑定事件的方法：

①bind    这两个函数的含义就是匹配页面元素进行相关事件的处理。 bind的第一个参数代表的含义是事件类型（注意前面步需要加on）function中的代码就是要执行的逻辑，代码中可以绑定多个事件，时间名之间用空格隔开         使用unbind解除事件

```js
$("#id").bind('click',function(){});
$('a').bind('click mouseover',function(){})          
```

②one    为每一个匹配元素的特定事件(像click)绑定一个一次性的事件处理函数，该方法与bind方法的参数一样，与bind方法的区别就是只对匹配元素的事件处理执行一次，执行完之后，以后再也不会执行，当然重新发起web请求时他又会执行一次

```js
$('a').one('click',function(){
alert('a');
});
//单击页面上的a元素后，弹出消息，除非用户发起第二次请求，否则再次点击a元素不会弹出消息对话框
```

③live     该方法要是能处理动态添加的元素，给那些后添加的元素也绑定了一样的事件。这个方法用到了事件委托的概念来处理事件大的绑定

```js
$("button").live("click",function(){
  $("p").slideToggle();
});
```

④on      尽量使用on，因为其他方法都是内部调用用on来完成，直接使用on可以提高效率，而且完全可以用on来代替其他写法。   使用off解除绑定

```js
$("div").on("click.a",function(e){
            console.log("a");
            $(this).off("click.a");
        })
```

​    

```js
$("div").on("click.a",function(e){
            // console.log(e);
            console.log("a");
            $(this).off("click.a");//命名空间可以解决删除事件的问题
            // 将所有click事件的内容全部删除
        }).on("click.b",function(){
            console.log("b");
        })

 var obj={
           a:1,
           b:function(){

                // $("div").on("click",this,function(e){
                // //    console.log(e);
                //     // e.data就是obj 也就是上面传入的this
                //  })

                 $("div").on("click",{a:this.a,b:10},function(e){
                   console.log(e.data);
                    // e.data就是obj 也就是上面传入的this
                 })
           }
       }
       obj.b();


   $("form").trigger("submit");//会触发默认事件
   $("form").triggerHandler("submit");//这个不会触发默认事件
  
//拖拽
$("div").mousedown(function(e){
        var div=$(this);
        e.preventDefault();
        $(document).mousemove(function(e1){
            div.css({
                left:e1.clientX-e.offsetX,
                top:e1.clientY-e.offsetY,
            })
        }).mouseup(function(){
            $(this).off("mousemove mouseup");//移除多个事件
        })
    })


 $(document).ready(function(){
        // 当DOM全部创建完成后，图片没有加载完成前
      })
      window.onload=function(){

      } 

//设置鼠标划入时变成绿色，划出时变成红色
//hover()方法时结合了.mouseenter()方法和.mouseleave方法，并非是.mouseover()和.mouseout()方法
 $("div").hover(function(){
          $(this).css("backgroundColor","green")
      },function(){
        $(this).css("backgroundColor","red")
      })
```

##### .trigger()与.triggerHandler()的区别

1、.triggerHandler()并不会出发时间的默认行为，而.trigger()会

```js
$("form").trigger("submit");//模拟用户执行提交，并跳转到执行页面
$("form").triggerHandler("submit");//模拟用户执行提交，并阻止事件的默认行为
//如果我们希望使用.trigge()来模拟用户提交，并且阻止事件的默认行为，则可以这么写
$("form").submit(function(e){
    e.preventDefault();//阻止默认事件
}).trigger("submit")
```

2、.triggerHandler()方法只会影响到第一个匹配到的元素而.trigger()会匹配到所有

3、.triggerHandler()方法会返回当前事件执行的返回值，如果没有返回值，则返回undefined。而.trigger()返回当前包含事件触发元素的jQuery对象

4、.trigger()在创建事件的时候会冒泡。但这种冒泡是自定义事件才能体现出来，是jQuery拓展于DOM的机制，并非DOM的特性。而.triggerHandler()不会冒泡



### jQuery动画

##### 隐藏与显示

```js
 $("div").hide(2000)//隐藏
 .show(2000);//显示
```

在无参数时，两个都是硬性的显示内容和隐藏内容

**注意**：hide()方法其实是在行内设置css代码：disolay：none

而show()是根据原来元素是区块还是内联来决定的。如果是区块，则设置css代码：display：block；如果内联，则设置css代码：display：inline

```js
 $("div").hide(2000,function(){
            $(this).toggle(2000);
        })
```

toggle()可以改变在上面他的元素的可视状态，如果隐藏就调用show()，如果显示就调用hide()。给toggle()传入true和不带参数调用show()是一样的，给toggle()传入false和不带参数调用hide()是一样的。



```js
$("div").slideUp(2000).slideDown(2000).slideToggle(2000);
```

slideUp会隐藏jQuery对象中的元素.方法是使其高度动态变为0，然后设置display的属性为none

slideDown会显示jQuery对象中的元素，进行反向操作

slideToggle会改变jQuery对象的中元素的原始状态实现向上滑动或者向下滑动

##### 

```js
$("div").fadeOut(1000).fadeIn(1000);//透明度设置
$("div").fadeTo(2000,0.4);//透明到多少
```

fadeOut和fadeIn简单改变css的opicaty属性来实现显示或者隐藏元素

fadeTo会将opicaty属性变到给定的值第一个参数是时常或者给定对象，第二个参数是opicaty属性值

#### 自定义动画

```js
$("div").animate({
            left:400,
            top:400
        },2000)

//为document设置点击事件当点击时div移动到鼠标指定位置并改变div的宽高
$(document).on("click",function(e){
            $("div").animate({
                left:e.clientX-25,
                top:e.clientY-25,
                width:100,
                height:100
            },500)
        })

//设置div移动
  $("div").animate({
            left:100
        },500).animate({
            top:100
        },500).animate({
            left:0
        },500).animate({
            top:0
        },500)
```

### jQuery插件

```js
 $.fn.widths=function(w){
           if(w===undefined) return parseFloat(this.css("width"));
           w=parseFloat(w)
           if(isNaN(w)) return;
           this.css({
               width:w+"px"
           })
        }
```

编写一个jQuery插件的方法:   $.fn.name()。通过对name()的定义我们可以在任何jQuery对象上调用name()方法

$.extend()向jQuery添加函数

```js
$.extend({
            a:function(){
                console.log("aa");
            }
        })；
        $.a();


$.extend({
            eachs:function(list,fn){
                switch(list.constructor){
                    case Array:
                    case jQuery:
                    case HTMLCollection:
                    case NodeList:
                    for(var i=0;i<list.length;i++){
                        fn(i,list[i]);
                    }
                    break;
                    case Object:
                        for(var prop in list){
                            fn(prop,list[prop]);
                        }
                    break;
                    
                    case Set:
                        for(var value of list){
                            fn(value,value);
                        }
                    break;
                    case Map:
                         for(var value of list){
                            fn(value[0],value[1]);
                        }
                    break;
                }
            }
        })
```

##### jQuery插件开发步骤

1、使用闭包。 避免全局依赖。避免第三方破坏。兼容jquery操作符$和jQuery

2、拓展。 $.extend用于自身方法

​				$.fn.extend用于拓展jquery类

3、选择器。  尽量使用id选择器。样式选择器应该尽量明确指定的标签名



### jQuery的AJAX

```js
//最顶层
$.getJSON();
$.getScript();
//中间层
$("div").load();
$.get();
$.post()
//最底层
$.ajax();

//加载json
 $.getJSON("./config.json",function(data){
            console.log(data);
        }) 

//加载js
  $.getScript("./a.js",function(){
            obj.c();
        }) 

//通过get方式请求服务
$.get("http://localhost:4006?user=xietian&age=30",function(data){
            console.log(data);
        });

$.get("http://localhost:4006","user=xietian&age=30",function(data,success,xhr){
            // console.log(data,success,xhr);
        }); 
//通过post方法请求服务
$.post("http://localhost:4006",{user:"xietian",age:30},function(data){
            console.log(data);
        })

//ajax
$.ajax({
            url:"http://localhost:4006?user=xietian&age=30",
            success:function(data){
                console.log(data);
            }
        })
//使用post方式
$.ajax({
            url:"http://localhost:4006",
            type:"POST",
            data:{user:"xietian",age:30},
            success:function(data){
                console.log(data);
            }
        })
//使用get方式
 $.ajax({
            url:"https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=谢天&json=1&p=3&sid=22084_1436_13548_21120_22036_22073&req=2&csor=0&cb=callback",
            type:"GET",
            dataType:"jsonp",//响应数据的预期数据类型是jsonp，
        })

        function callback(data){
            console.log(data);
        }
```

