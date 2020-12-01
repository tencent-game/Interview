# node.js

```js
var http=require("http");//加载HTTP
var querystring=require("querystring");
var req,res;
var server=http.createServer(serverHandler);
server.listen(4008,"10.9.62.243",listenHandler);
```

### node事件

```js
req.on("end",endHandler)//为end添加时间侦听
req.off("end",endHandler)// 删除事件
```

使用node.js创建新的服务端(创建一个server.js文件)

```js
var http=require("http")//导入“http”模块，此模块在node中默认安装
var querystring=require("querystring");
var req,res;//将req与res设为全局变量，只有服务创建时才会使用
var server=http.createServer(serverHandler);//创建一个服务器
function serverHandler(_req,_res){
    //req 请求        客户端请求服务端
    //res 响应        服务端响应客户端
    req=_req;
    res=_res;
    req.on("data",dataHandler)//当数据很多时执行data
    req.on("end",endHandler)//数据接收完成以后的结果
}
server.listen(4008,"10.9.62.243",listenHandler);//第一个参数为端口号，第二个参数为ip地址

function dataHandler(_data){
    
}

function endHandler(){
    if(req.url.indexOf("/favicon.icon")>-1){
        res.end();//将请求图标消息屏蔽掉
        return;
    }
    var obj=querystring.parse(req.url.split("?")[1]);//将字符串转换为对象
    res.writeHeader(200,{"content-type","text/html;charset=utf-8"});//写入响应头，200表示相应成功，对象中为所有的响应头设置
    res.write();//服务端写入消息
    res.end();//将消息发回给客户端 
}

function listenHandler(){
    console.log("已连接")
}
//在终端上输入node ./js/server
//显示”已连接“表示服务器已经启动
```

------

```js
var http=require("http");
var querystring=require("querystring");
var server=http.createServer(function(req,res){
    req.on("data",function(_data){

    });
    req.on("end",function(){
        var obj=querystring.parse(req.url.split("?")[1]);
        console.log(obj.user);
        res.writeHead(200,{
            "content-type":"text/html;charset=utf-8",
             "Access-Control-Allow-Origin":"*"
            //  cors跨域
            });
        res.write(obj.user+"欢迎光临");
        res.end();
    })
});
server.listen(4002);
```

