## 模块化开发

#### 模块基础写法

##### 普通方法

优点：直接调用
缺点：变量可能会出现重复造成的污染，并且无法进行结构性分类

```
function a() {
            console.log("a");
 }
 function b() {
            console.log("b");
 }
a();
b();
```

##### 对象的写法

优点：变量不会被直接污染，并且易于分类描述内容
缺点：会暴露所有成员，内部状态可以被外部改写。

```
var obj={
    _a:false,
    a:function () {
       console.log("a");
    },
    b:function () {
     console.log("b");
    }
};
obj.a();
obj.b();
obj._a=3;
```

##### 立即执行函数

优点：外部代码无法读取到里面的_num变量，保证了变量不被污染
基本上这种就是模块的写法了，但是单纯的这样描述仍然不算完美，因此我们在其基础上进行了一下的修改

```
var obj=(function () {
    var _num=3;
    return{
        a:function () {
            console.log(a);
        },
        set num(value){
            _num=value;
        },
        get num(){
            return _num;
        }
    }
})();
obj.num=5;
console.log(obj.num)//5;
console.log(obj._num)//undefined
obj.a();//a
```

###### 放大模式

```
var module=(function () {
      return {
          a:1,
          b:2,
          c:function () {

          }
      }
})();
module=(function (mode) {
    mode.d=10;
   return mode;
})(module);	//将上边的自执行函数作为参数带入
```

###### 宽放大模式

如果module没有定义或者没有加载进入，这时候我们可以在带入参数的时候给参数时判断是否存在，不存在给一个空对象。与"放大模式"相比，＂宽放大模式＂就是"立即执行函数"的参数可以是空对象。

```
var model=(function(){
    var a=10;
    return {
        a:1,
        b:function(){

        }
    }
})();

var  model1=(function(model){
    var c=20;
    model.d=10;
    model.e=function(){

    }
    return model;
})(model || {})
console.log(model1===model);//true
```

#### CommonJS

##### CommonJS规范

2009年，美国程序员Ryan Dahl创造了node.js项目
这标志"Javascript模块化编程"正式诞生.当时在浏览器环境下，没有模块也不是特别大的问题，毕竟网页程序的复杂性有限；但是在服务器端，一定要有模块，与操作系统和其他应用程序互动，否则根本没法编程。ode.js的模块系统，就是参照CommonJS规范实现的。在CommonJS中，有一个全局性方法require()，用于加载模块。假定有一个数学模块math.js，就可以像下面这样加载。

```
var math = require('math');
math.add(2,3); // 5
```

注意此处是同步

##### 加载方式

定义模块

```
// main.js
var http=require("http");
var querystring=require("querystring");
function createServers(route){
    var server=http.createServer(function(req,res){
        var data="";
        req.on("data",function(_data){
           data+=_data;
        });
        req.on("end",function(){
            // console.log(req.headers.abc);
            if(data.trim().length===0) data=req.url.split("?")[1];   
            else{
                try{
                    data=JSON.parse(data);
                }catch(error){
    
                }
            }
            if(typeof data==="string"){
                try{
                    data=querystring.parse(data);
                }catch(error){
                    res.end("错误的消息");
                    return;
                }
            }
            if(!data){
                res.end("错误的消息");
                return;
            }
            res.writeHead(200,{
                "content-type":"text/html;charset=utf-8",
                // "Access-Control-Allow-Headers":"*",//请求头跨域
                 "Access-Control-Allow-Origin":"*",
                //  cors跨域
                });
                switch(req.url.split("?")[0]){
                    case "/a":
                        route.a(res,data);
                        break;
                    case "/b":
                        route.b(res,data);
                        break;
                }
               
        })
    });
    server.listen(4006);
}
module.exports=createServers;
```

```
//	a.js
var obj={
    a:1,
    init:function(res,data){
        console.log("执行了a.js");
        res.write((data.user? data.user : "你没有user")+"欢迎光临");
        res.end();
    }
}
module.exports=obj;//这个导出一个
// exports.obj=obj;//这个可以导出多个
```

```
//	b.js
var obj={
    a:1,
    init:function(res,data){
        console.log("执行了b.js");
        res.write((data.user? data.user : "你没有user")+"欢迎再次光临");
        res.end();
    }
}
module.exports=obj;
```

加载模块

```
// 通过 require 引入依赖
var cs=require("./main");
//node路由
var route={
    a:require("./a").init,
    b:require("./b").init
}
cs(route);
```

#### AMD

##### AMD规范

有了服务器端模块以后，很自然地，大家就想要客户端模块。而且最好两者能够兼容，一个模块不用修改，在服务器和浏览器都可以运行。
但是，由于一个重大的局限，使得CommonJS规范不适用于浏览器环境。

```
var math = require('math');
math.add(2, 3);
```

第二行math.add(2, 3)，在第一行require('math')之后运行，因此必须等math.js加载完成。也就是说，如果加载时间很长，整个应用就会停在那里等。
这对服务器端不是一个问题，因为所有的模块都存放在本地硬盘，可以同步加载完成，等待时间就是硬盘的读取时间。但是，对于浏览器，这却是一个大问题，因为模块都放在服务器端，等待时间取决于网速的快慢，可能要等很长时间，浏览器处于"假死"状态。
因此，浏览器端的模块，不能采用"同步加载"（synchronous），只能采用"异步加载"（asynchronous）。这就是AMD规范诞生的背景。

AMD是"Asynchronous Module Definition"的缩写，意思就是"异步模块定义"。

##### 加载方式

```
//HTML
<script src="./require.js" data-main="./AMD/index" async defer></script>
```

定义模块

```
//	a.js
define((function(){
    var a=1;
    return {
        b:2,
        init:function(){
            console.log(a);
            console.log(this.b);
        }
    }
})());
```

```
//	b.js
define((function(){
    return {
        init:function(a,b){
            console.log(a+b);
        }
    }
})());
```

```
//	c.js
define(["./Utils"],function(Utils){
   var div= Utils.ce("div",{
        width:"50px",
        height:"50px",
        backgroundColor:"red"
    });
    return div;
});
```

加载模块

```
require(["./a","./b","./c"],function(obj,obj2,div){
    // console.log(obj);
    obj.init();
    // fn(10,obj.b);
    obj2.init(10,obj.b);
    document.body.appendChild(div);
})
```

## SASS

#### 安装

##### ruby

​	sass基于Ruby语言开发而成，因此安装sass前需要安装Ruby
​	安装过程中请注意勾选Add Ruby executables to your PATH添加到系统环境变量。

##### SASS安装

​	gem install sass
​	gem install compass

##### SASS转换CSS

​	单文件  sass input.scss output.css
​	多文件  sass --watch assets/sass:dist/sass

#### sass和scss

##### sass

Sass 是一门高于 CSS 的元语言，它能用来清晰地、结构化地描述文件样式，有着比普通 CSS 更加强大的功能

扩展名是.sass

书写：

```
$color:red
div
  :color $color
span
  color: $color
```

这两种写法都是可以的，但是注意不能使用{}和；
		:color $color  指出该样式是这个元素的
		 color: $color 普通css写法

##### scss

Scss 是 Sass 3 引入新的语法，是Sassy CSS的简写，是CSS3语法的超集，也就是说所有有效的CSS3样式也同样适合于Sass

扩展名是.scss

书写:

```
$color:red;
div{
  color: $color;
}
span{
  color: $color;
}
```

贴近于CSS的写法

Scss就是Sass的升级版

#### sass的语法

##### 变量的声明

```
$color:red;
$width:300;
div{
   color: $color;
   width: $width+px;
}
span{
  color: $color;
}
```

##### 选择器的嵌套

```
$color_1:red;
$color_2:blue;
div{
  span{color: $color_1}
  div{color: $color_2}
}
```

##### 夫选择器

这里的&就是span自身这个选择器给它自己加了hover

```
span{
   color: red;
  &:hover{
    color: blue;
  }
}
```

##### 各种选择器的嵌套

```
article {
  ~ article { border-top: 1px dashed #ccc }
  > section { background: #eee }
  dl > {
    dt { color: #333 }
    dd { color: #555 }
  }
  nav + & { margin-top: 0 }
}
```

##### 属性嵌套

这是嵌套了属性，border-style被拆分

```
nav {
  border: {
  style: solid;
  width: 1px;
  color: #ccc;
  }
}
```

##### 导入文件

a.scss

```
$r:50px;
div{
  width: $r;
  height: $r;
  border-radius: $r/2;
}
```

main.scss

```
@import "a";

div{
  span {color: red}
  & {@import "a";}
}
```

这里导入以后就会有把a中的定义内容导入
如果写在标签中，那么导入的内容将会作为这个标签的后代元素样式进入

##### 混合器

###### 普通类型混合器

这里的@mixin定义语句块，@include调用语句块

```
$r:50px;
@mixin divRadius{
  width: $r;
  height: $r;
  border-radius: $r/2;
}

div{
  @include divRadius;
}
```

###### 传参混合器

```
@mixin divRadius($r){
  width: $r;
  height: $r;
  border-radius: $r/2;
}

div{
  @include divRadius(50px);
  div{
    @include divRadius(25px)
  }
}
```

###### 混合器传参的默认值

```
@mixin divRadius($r:100px){
  width: $r;
  height: $r;
  border-radius: $r/2;
}

div{
  @include divRadius;
  div{
    @include divRadius(50px)
  }
}
```

##### 继承

这里使用@extend 继承了类div0的样式

```
.div0
{
  $r:100px;
  width: $r;
  height: $r;
  border-radius: $r/2;
}

div{
  div{
    @extend .div0;
  }
}
```

## gulp

#### gulp安装

npm初始化，新建package.json

```
npm init -y
```

先安装全局

```
npm install gulp -g
```

再需要在当前项目中安装

```
npm install gulp
```

装两遍是为了版本的灵活性

#### 开始使用Gulp

在根目录下新建gulpfile.js文件

这个文件就是配置运行文件。我们先尝试写一个最简单的内容

```
var gulp=require("gulp");
gulp.task("init",function () {
    console.log("init");
});
```

1、require就是讲刚才下载的gulp模块加载导入进来

2、gulp下有一个方法task用来定义任务，第一个参数是任务名，第二个参数是任务执行后的执行函数

3、在命令行输入gulp init这个init就是刚才起的任务名，执行后就会执行函数，打印出init

#### Gulp的方法

##### gulp工作方式

gulp实际工作是使用nodejs中的stream来处理的，简单来说，如果需要合并两个文件，就需要讲两个文件都加载进来，然后再处理将文件合并，注意这里加载进来的文件并不是文本形式加载，而是以二进制数据流的方式，也就是steam加载进入。被加载进入的文件是以二进制数据流模式存在的，内容中除了含有文件内容，还包括了文件的地址，文件名等等一系列相关信息。然后再将所有的数据流处理生产新文件。因此这里就用到了nodejs中stream的方法pipe

###### pipe

管道，流向的意思，可以在这里理解为写入到

a.pipe(b) 将a写入到b中

##### src方法

读取文件的数据流

gulp.src(globs)

globs参数是读取文件的筛选条件，可以写入字符串，也可以是数组，数组含有多个读取条件

gulp.src("js/a.js") 读取一个文件

gulp.src(["js/a.js","js/b.js"]) 读取两个文件

 gulp.src("js/*.js") js文件夹下所有的js文件

匹配条件

匹配文件路径中的0个或多个字符，但不会匹配路径分隔符，除非路径分隔符出现在末尾

** 匹配路径中的0个或多个目录及其子目录,需要单独出现，即它左右不能有其他东西了。如果出现在末尾，也能匹配文件。也就是能匹配某个目录下所有文件包括其子目录下的所有内容

? 匹配文件路径中的一个字符(不会匹配路径分隔符)

[...] 匹配方括号中出现的字符中的任意一个，当方括号中第一个字符为^或!时，则表示不匹配方括号中出现的其他字符中的任意一个，类似js正则表达式中的用法

```
!(pattern|pattern|pattern) 匹配任何与括号中给定的任一模式都不匹配的
?(pattern|pattern|pattern) 匹配括号中给定的任一模式0次或1次，类似于js正则中的(pattern|pattern|pattern)?
+(pattern|pattern|pattern) 匹配括号中给定的任一模式至少1次，类似于js正则中的(pattern|pattern|pattern)+
*(pattern|pattern|pattern) 匹配括号中给定的任一模式0次或多次，类似于js正则中的(pattern|pattern|pattern)*
@(pattern|pattern|pattern) 匹配括号中给定的任一模式1次，类似于js正则中的(pattern|pattern|pattern)
```

##### dest方法

给文件写入数据流

```
gulp.dest(path)
```

path参数是要写入文件存放的路径

```
gulp.task("init",function () {
    gulp.src("./js/*.js").pipe(gulp.dest("./dist/"))
});
```

这样就会将当前目录下，js文件夹下所有的js读入，然后写入到当前目录的dist文件夹下

用gulp.dest()把文件流写入文件后，文件流仍然可以继续使用。

##### tast方法

定义任务

如果需要有多个任务操作时就需要定义任务

gulp.task(任务名,任务所依赖前面任务名的数组,任务执行的函数);

```
gulp.task("default",function () {
    console.log("aaa");
});
这是默认执行，执行gulp就可以，无需输入任务名
```

```
gulp.task("one",function () {
    console.log("one");
});
gulp.task("two",["one"],function () {
    console.log("two")
});

如果执行 gulp two 这时候就会先执行任务one，再执行任务two
```

##### watch方法

监听文件变法

```
gulp.task("default",function () {
    gulp.watch('js/*.js', function(event){
        console.log(event.type); //变化类型 added为新增,deleted为删除，changed为改变
        console.log(event.path); //变化的文件的路径
    });
});
这里启动任务后，会开始监视，如果js文件夹下那个文件修改了，或者删除，增加，这里都会打印出来
```

#### 一些常用的gulp插件

##### 自动加载插件

```
gulp-load-plugins
```

```
npm install --save-dev gulp-load-plugins
```

##### 压缩文件

可以将文件中的空格去除

```
gulp-uglify
```

```
npm install --save-dev gulp-uglify
```

```
gulp.task("default",function () {
   gulp.src("./js/a.js")
       .pipe(uglify())
       .pipe(gulp.dest("./dist"))
});
```

##### 重命名

可以重新给文件起名

```
gulp-rename
```

```
npm install --save-dev gulp-rename
```

```
gulp.task('rename', function () {
    gulp.src('js/jquery.js')
    .pipe(uglify())  //压缩
    .pipe(rename('jquery.min.js')) //会将jquery.js重命名为jquery.min.js
    .pipe(gulp.dest('js'));
});
```

##### css文件压缩

```
gulp-minify-css
```

```
npm install --save-dev gulp-minify-css
```

```
var gulp = require('gulp'),
    minifyCss = require("gulp-minify-css");
 
gulp.task('minify-css', function () {
    gulp.src('css/*.css') // 要压缩的css文件
    .pipe(minifyCss()) //压缩css
    .pipe(gulp.dest('dist/css'));
});
```

##### html文件压缩

```
gulp-minify-html
```

```
npm install --save-dev gulp-minify-html
```

```
var gulp = require('gulp'),
    minifyHtml = require("gulp-minify-html");

gulp.task('minify-html', function () {
    gulp.src('html/*.html') // 要压缩的html文件
    .pipe(minifyHtml()) //压缩
    .pipe(gulp.dest('dist/html'));
});
```

##### 文件合并

```
gulp-concat
```

```
npm install --save-dev gulp-concat
```

```
var gulp = require('gulp'),
    concat = require("gulp-concat");
 
gulp.task('concat', function () {
    gulp.src('js/*.js')  //要合并的文件
    .pipe(concat('all.js'))  // 合并匹配到的js文件并命名为 "all.js"
    .pipe(gulp.dest('dist/js'));
});
```

##### sass解析

```
gulp-sass
```

```
npm install --save-dev gulp-sass
```

```
var gulp = require('gulp'),
    sass = require("gulp-sass");
 
gulp.task('compile-sass', function () {
    gulp.src('sass/*.sass')
    .pipe(sass())
    .pipe(gulp.dest('dist/css'));
});
```

##### 图片压缩

```
gulp-imagemin
```

```
npm install --save-dev gulp-imagemin
```

```
var gulp = require('gulp');
var imagemin = require('gulp-imagemin');
 
gulp.task('default', function(){
		gulp.src('src/images/*')
        .pipe(imagemin())
        .pipe(gulp.dest('dist/images'))
    }
);
```

##### 静态服务器搭建

使用browser.init创建服务位置和端口

browser-sync是静态服务器，create()开启创建

使用gulp.watch做监听，并且重新执行js的合并压缩打包等处理，最后当存储完成后，刷新网页browser.reload是重载页面

```
var gulp=require("gulp");
var load=require("gulp-load-plugins")();

var browser=require("browser-sync").create();
gulp.task("save",function(done){
    gulp.src("./src/**/*.js")
    .pipe(load.babel({
        presets:['@babel/env']
    }))
    .pipe(load.concat("main.min.js"))
    .pipe(load.uglify())
    .pipe(gulp.dest("./dist"))
    .on("end",browser.reload);
});
gulp.task("server",function(){
    browser.init({
        server:"./",
        port:3009
    })
    gulp.watch("./src/**/*.js",gulp.series("save"));
})
```

