# cookie

### cookie的机制

cookie技术是客户端的解决方案，cookie就是由服务器发送给客户端的特殊信息。当用户浏览一个支持cookie的网页时，用户会提供包括用户名在内的个人信息提交至服务器，接着服务器在向客户端回传相应的超文本时会发会这些信息，这些信息存放在HTTP响应头中(Response Header).当浏览器客户端收到服务器响应的信息后，会将这些信息存储在一个统一的位置。自此，客户端再次向服务器中发送信息时，都会把相应的cookie发送到服务器中。通过这样的技术手段，服务器可以在接收到客户端的请求后可以通过分析存放在请求头中的cookie信息，动态的生成相对应的内容。例如在登陆时勾选技术用户名与密码就会在下次登陆时直接进入，减去了那些繁琐的登陆环节。

因为HTTP协议是一种无状态的协议，在数据交接完成后客户端与服务端的连接会中断，再次交换数据需要建立新的连接，这就意味着服务器无法从连接上跟踪会话，也就是当服务器与客户端再次连接时，服务器无法判断上次的交换行为是属于那个客户端的，所以为了弥补HTTP协议的不足引进了cookie这种机制。

一个cookie的设置和发送过程分为四部：

① 客户端发送一个http到服务器

②服务器发送一个http响应客户端，其中包括setCookie头部

③客户端发送一个http请求到服务器，其中包括Cookie头部，提供给服务器端可以用来唯一标识客户端身份的信息

④服务器发送一个http响应客户端

###### 定义：cookie是客户端请求服务器，服务器要记录该用户状态，使用response向客户端浏览器颁发一个cookie，客户端浏览器将其保存起来，当浏览器再次请求该网站时，浏览器将请求的网址与cookie一同发给服务器，服务器检查cookie以此来验证用户身份

cookie 只能作为临时存储，当浏览器关闭，就会丢失

   cookie 的作用域为当前域，有文件夹路径的区分,域中的文件夹存储

   http:*//www.jd.com/paimai/index.html 在这个域中任何文件都可以写cookie，*

   存储的位置都是以这个域作为存储空间的，别的域不能访问

​    1、刷新页面是可以使用

​    2、跳转到当前域所在另外页面时可以获取前面cookie存储的数据内容

### 设置cookie的所有属性

- String name：该Cookie的名称。Cookie一旦创建，名称便不可更改。

- Object value：该Cookie的值。如果值为Unicode字符，需要为字符编码。如果值为二进制数据，则需要使用BASE64编码。
- int maxAge：该Cookie失效的时间，单位秒。如果为正数，则该Cookie在>maxAge秒之后失效。如果为负数，该Cookie为临时Cookie，关闭浏览器即失效，浏览器也不会以任何形式保存该Cookie。如果为0，表示删除该Cookie。默认为–1。
-  boolean secure：该Cookie是否仅被使用安全协议传输。安全协议。安全协议有HTTPS，SSL等，在网络>上传输数据之前先将数据加密。默认为false。 
- String path：该Cookie的使用路径。如果设置为“/sessionWeb/”，则只有contextPath为“/sessionWeb”的程序可以访问该Cookie。如果设置为“/”，则本域名下contextPath都可以访问该Cookie。注意最后一个字符必须为“/”。
- String domain：可以访问该Cookie的域名。如果设置为“.google.com”，则所有以“google.com”结尾的域名都可以访问该Cookie。注意第一个字符必须为“.”。
- String comment：该Cookie的用处说明。浏览器显示Cookie信息的时候显示该说明。
- int version：该Cookie使>用的版本号。0表示遵循Netscape的Cookie规范，1表示遵循W3C的RFC 2109规范

### cookie的有效期

maxAge决定了Cookie的有效期，单位为秒

Cookie中通过getMaxAge()方法与setMaxAge(int maxAge)方法来读写maxAge属性。 如果maxAge属性为正数，则表示该Cookie会在maxAge秒之后自动失效。浏览器会将maxAge为正数的Cookie持久化，即写到对应的Cookie文件中。无论客户关闭了浏览器还是电脑，只要还在maxAge秒之前，登录网站时该Cookie仍然有效。

如果maxAge为负数，则表示该Cookie仅在本浏览器窗口以及本窗口打开的子窗口内有效，关闭窗口后该Cookie即失效。maxAge为负数的Cookie，为临时性Cookie，不会被持久化，不会被写到Cookie文件中。Cookie信息保存在浏览器内存中，因此关闭浏览器该Cookie就消失了。Cookie默认的maxAge值为–1。

如果maxAge为0，则表示删除该Cookie。Cookie机制没有提供删除Cookie的方法，因此通过设置该Cookie即时失效实现删除Cookie的效果。失效的Cookie会被浏览器从Cookie文件或者内存中删除

response对象提供的Cookie操作方法只有一个添加操作add(Cookie cookie)。要想修改Cookie只能使用一个同名的Cookie来覆盖原来的Cookie，达到修改的目的。删除时只需要把maxAge修改为0即可。

注意：从客户端读取Cookie时，包括maxAge在内的其他属性都是不可读的，也不会被提交。浏览器提交Cookie时只会提交name与value属性。maxAge属性只被浏览器用来判断Cookie是否过期。

### Cookie的修改删除

Cookie并不提供修改、删除操作。如果要修改某个Cookie，只需要新建一个同名的Cookie，添加到response中覆盖原来的Cookie。如果要删除某个Cookie，只需要新建一个同名的Cookie，并将maxAge设置为0，并添加到response中覆盖原来的Cookie。注意是0而不是负数。负数代表其他的意义。读者可以通过上例的程序进行验证，设置不同的属性。

注意：修改、删除Cookie时，新建的Cookie除value、maxAge之外的所有属性，例如name、path、domain等，都要与原Cookie完全一样。否则，浏览器将视为两个不同的Cookie不予覆盖，导致修改、删除失败。

### cookie的域名

Cookie是不可跨域名的。域名www.google.com颁发的Cookie不会被提交到域名www.baidu.com去。这是由Cookie的隐私安全机制决定的。隐私安全机制能够禁止网站非法获取其他网站的Cookie。

正常情况下，同一个一级域名下的两个二级域名如www.helloweenvsfei.com和images.helloweenvsfei.com也不能交互使用Cookie，因为二者的域名并不严格相同。如果想所有helloweenvsfei.com名下的二级域名都可以使用该Cookie，需要设置Cookie的domain参数，

注意：domain参数必须以点(".")开始。另外，name相同但domain不同的两个Cookie是两个不同的Cookie。如果想要两个域名完全不同的网站共有Cookie，可以生成两个Cookie，domain属性分别为两个域名，输出到客户端。

# Session

### Session机制

Session是服务器端使用的一种记录客户端状态的机制，使用上比Cookie简单一些，相应的也增加了服务器的存储压力。Session技术则是服务端的解决方案，它是通过服务器来保持状态的。由于Session这个词汇包含的语义很多，因此需要在这里明确一下 Session的含义。首先，我们通常都会把Session翻译成会话，因此我们可以把客户端浏览器与服务器之间一系列交互的动作称为一个 Session。从这个语义出发，我们会提到Session持续的时间，会提到在Session过程中进行了什么操作等等；其次，Session指的是服务器端为客户端所开辟的存储空间，在其中保存的信息就是用于保持状态。从这个语义出发，我们则会提到往Session中存放什么内容，如何根据键值从 Session中获取匹配的内容等。

### 定义

Session是另外一种记录客户状态的机制，不同的是cookie保存在客户端浏览器中，而Session保存在服务器中，客户端浏览器访问服务器的时候，服务器把客户端信息以某种形式记录在服务器上。这就是Session。客户端浏览器再次访问时只需要从该Session中查找该客户的状态就可以了。

如果将Cookie比作是服务器给客户端发放的通行证的话，Session就是服务器给客户端定的一份档案，当客户端访问时只需要检查客户档案中是否存在此客户就行

## Cookie与Session的区别

1. cookie数据存放在客户的浏览器上，session数据放在服务器上；
2. cookie不是很安全，别人可以分析存放在本地的COOKIE并进行COOKIE欺骗，考虑到安全应当使用session；
3. session会在一定时间内保存在服务器上。当访问增多，会比较占用你服务器的性能。考虑到减轻服务器性能方面，应当使用COOKIE；
4. 单个cookie在客户端的限制是3K，就是说一个站点在客户端存放的COOKIE不能超过3K；

### stroage存储

```js
localStorage.removeItem("name");//删除某个数据
localStorage.clear();//清除所有数据
```

### localStorage与sessionStorage

localStorage与sessionStorage都代表同一个Storage对象-------一个持久化关联数组，使用字符串索引，存储的值也都是字符串形式的

localStorage与sessionStorage两者的区别在于存储的有效期和作用域不同（即数据存储多少时间和谁有数据的访问权）

localStroage存储的数据是永久性的。作用域是限定在文档源级别的。同源的文档间共享同样的localStroage数据，他们可以相互读取对方的数据，甚至可以覆盖对方的数据。但是非同源的是绝对不行的，即便他们运行的脚本来自同一台第三方服务器也不行。

sessionStorage存储的数据的有效期与最顶层好的窗口或者浏览器的标签页相同，一旦窗口或标签页被永久关闭，那么通过sessionStorage保存的数据也会被删除。其作用域与localStroage相同都是限定在档案源级别。非同源文档间不可共享sessionStorage，sessionStorage作用域还被限定在窗口上，如果同源的文档渲染不同的浏览器标签页，他们之间拥有的各自的sessionStorage数据，无法共享。

注意这里说的·sessionStorage限定的窗口说的是顶级窗口

