# 总结

## HTML语义化
指对文本内容的结构化（内容语义化），选择合乎语义的标签（代码语义化），便于开发者阅读，维护和写出更优雅的代码的同时，让浏览器的爬虫和辅助技术更好的解析。

可访问性、可检索性、国际化、互用性。

常用语义化便签：header nav main article section aside footer

---

## meta viewport
~~~
<meta name="viewport" content="width=device-width, user-scalable=no, initial-scale=1.0, maximum-scale=1.0, minimum-scale=1.0">
~~~

作用：控制页面在移动端不要缩小显示。在移动端能正常地显示。

---

## canvas

canvas 是 HTML5 新增的元素，可用于通过使用JavaScript中的脚本来绘制图形。

~~~
<canvas id="canvas"></canvas>

var canvas = document.getElementById('canvas');
var ctx = canvas.getContext('2d'); // 这个方法是用来获得渲染上下文和它的绘画功能

ctx.fillStyle = 'green';
ctx.fillRect(10, 10, 100, 100);
~~~

## SVG
可缩放矢量图形，是一种用来描述二位矢量图形的 XML 标签语言，SVG 面向图形，HTML面向文本。

canvas 是非矢量，svg 放大不模糊，且拥有更丰富的效果。

canvas 不支持事件处理器，svg 支持。

canvas 弱的文本渲染能力，适合图像密集型的游戏。

svg 不适合游戏应用，适合带大型渲染区域的应用。

----

## 盒模型 （box-sizing）

- content-box : 

    width = 内容的宽度，height = 内容的高度。
    
    宽度和高度都不包含内容的边框（border）和内边距（padding）。
- border-box :

    width = border + padding + 内容的  width，
    
    height = border + padding + 内容的 height。

---

## 居中

### 水平居中
- 行内元素, 给其父元素设置 text-align:center, 即可实现行内元素水平居中.
- 块级元素
    - 定宽 
    1. 该元素设置 margin:0 auto 即可。
    2. 使用绝对定位方式,
        ~~~
        position:absolute; 
        width:固定; 
        left:50%; 
        margin-left:-0.5宽度;
        ~~~
    3. 使用绝对定位方式
        ~~~
        position:absolute; 
        width:固定; 
        left:0; 
        right:0;
        margin:0 auto;
        ~~~
    - 不定宽
    1. 父元素设置 
        ~~~
        display: flex; 
        justify-content: center;
        ~~~
    2. transform属性
        ~~~
        position:absolute; 
        left:50%; 
        transform:translate(-50%,0);
        ~~~

### 垂直居中
- 单行文本, 则可设置 line-height 等于父元素高度
- 行内块级元素
    ~~~
    .parent::after, .son{
        display:inline-block;
        vertical-align: middle;
    }
    .parent::after{
        content: '';
        height: 100%;
    }
    ~~~
- 元素高度不定 
    1. 使用 table ，自带垂直居中
    2. div display: table
        ~~~
        父元素
        display:table;

        子元素 
        display: table-cell;
        vertical-align: middle;
        ~~~
    3. 使用 flex
        ~~~ 
        display: flex;
        justify-content: center;
        align-items: center;
        ~~~
    4. 绝对定位 和 transform 
        ~~~
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%,-50%);
        ~~~
- 元素高度固定
    1. 绝对定位
        ~~~
        .son{
            position:absolute;
            top:50%;
            height: 固定;
            margin-top: -0.5 * height;
            width: 固定;
            margin-left: -0.5 * width;
        }
        ~~~
    2. 绝对定位
        ~~~
        .son{
            position:absolute;
            height: 固定;
            width: 固定;
            top: 0;
            bottom: 0;
            left: 0;
            right: 0;
            margin: auto 0;
        }
        ~~~

---

## 选择器优先级
- 选择器越具体，优先级越高。便签 大于 #xxx 大于 .yyy
- 同样优先级，写在后面的覆盖前面的。
- !important 优先级最高。

---
        
## 清除浮动
.clearfix 清除浮动写在爸爸身上
~~~
.clearfix::after {
    content: '';
    display: block; 
    clear: both;
}
.clearfix {
    zoom: 1; /* IE 兼容 */
}
~~~

---

## JS 数据类型
string number bool undefined null object symbol

object 包括了数组、函数、正则、日期等对象

---

## AJAX 
“Asynchronous JavaScript and XML”（异步的JavaScript与XML技术）

Ajax 是以异步的方式向服务器提交需求，能在不更新整个页面的前提下维护数据。
~~~
let xhr = new XMLHttpRequest()
 xhr.open('POST', '/xxxx')
 xhr.onreadystatechange = function(){
     if(xhr.readyState === 4 && xhr.status === 200){
         console.log(xhr.responseText)
     }
 }
 xhr.send('a=1&b=2')
~~~

---

## 闭包
「函数」和「函数内部能访问到的变量」（也叫环境）的总和，就是一个闭包。
~~~
function foo(){
  var local = 1     // 函数内部能访问到的变量 
  function bar(){   // 函数
    local++
    return local
  }
  return bar
}

var func = foo()
func()
~~~
一般情况下，需要这个变量是局部变量，所以用一个函数（foo）来包住闭包，然后return 里面的函数（bar），这样就可以让外面访问到里面的函数（bar）。

作用是隐藏一个变量，不让外部直接改变这个变量，但可以读取这个变量。另一个作用是，让这些变量的值始终保持在内存中。原因就在函数（bar）被赋给了一个全局变量，这导致函数（bar）始终在内存中，而函数（bar）的存在依赖于函数（foo），因此函数（foo）也始终在内存中，不会在调用结束后，被垃圾回收机制（garbage collection）回收。

所以，闭包也理解为能够读取其他函数内部变量的函数。

---

## this
记住就是 call 的第一个参数，this 只有在传参的时候才能确定

- fn() 里面的 this 就是 window
- fn() 是 strict mode，this 就是 undefined
- a.b.c.fn() 里面的 this 就是 a.b.c
- new F() 里面的 this 就是新生成的实例
- 箭头函数 里面 this 跟外面的 this 的值一模一样

---


## call apply bind
### call / apply
fn.call(asthis, p1, p2) 这样是函数正确的调用方式
当不确定参数的个数时，就使用apply

### bind
返回一个新函数（并没有调用原来的函数），这个新函数会call原来的函数，call的参数由你来指定。（一般用来指定 this）

---


## 立即执行函数
~~~
 ;(function (){
     var name
 }())
 ;(function (){
     var name
 })()
 !!!!!!!function (){
     var name
 }()
 ~function (){
     var name
 }()
~~~
造出一个函数作用域，防止污染全局变量

ES 6 新语法
~~~
 {
     let  name
 }
~~~

---


## Promise 
- then
~~~
  $.ajax(...).then(成功函数, 失败函数)
~~~
- 链式 then
~~~
  $.ajax(...).then(成功函数, 失败函数).then(成功函数2, 失败函数2)
~~~
- 如何自己生成 Promise 对象
~~~
  function xxx(){
      return new Promise(function(resolve, reject){
          setTimeout(()=>{
              resolve() 或者 reject()
          },3000)
      })
  }
  xxx().then(...)
~~~

---

## async / await
- async 确保了函数返回一个 promise，即使其中包含非 promise。
- promise 前面的 await 关键字能够使 JavaScript 等待，直到  promise 处理结束。然后：
    1. 如果它是一个错误，异常就产生了，就像在那个地方调用了 throw error 一样。
    2. 否则，它会返回一个结果，我们可以将它分配给一个值

---

## 原型
原型，也可以理解为共用属性，也就是每个对象都有的属性，而这些属性存在同一个地址里，那么所有的对象都可以去调用这个共用对象。其实，为的是不要浪费重复属性。

那么，原型怎么调用呢，在每一个对象里都会有一个隐藏属性 __proto__ ，这个属性存储的就是共用属性的地址。当对象调用共用属性的时候，就找到自己的 __proto__ 所指向的地址，在该地址找到要调用的属性。

---

## 原型链
那么原型链就是也可以看作一个节点指向上一级节点再指向上一级节点到最后的这么一个过程。

例如，定义了一个 Number，那么它内存里的 __proto__ 就是一个节点，指向Number的原型，而它的 __proto__ 指向的是 Object的原型，而他的 __proto__ 指向的是 null ， 因为已经是最后了。这样就是一个原型链。

---

## 继承 
- 原型链
~~~
  function Animal(){
      this.body = '肉体'
  }
  Animal.prototype.move = function(){}

  function Human(name){
      Animal.apply(this, arguments)
      this.name = name
  }
  // Human.prototype.__proto__ = Animal.prototype // 非法
  Human.prototype = Object.create(Animal.prototype)

  Human.prototype.useTools = function(){}

  var frank = new Human()
~~~
- extends 关键字
~~~
  class Animal{
      constructor(){
          this.body = '肉体'
      },
      move(){}
  }
  class Human extends Animal{
      constructor(name){
          super()
          this.name = name
      },
      useTools(){}
  }
  var frank = new Human()
~~~

---

## new
语法糖 可以省略构造函数的一堆固定代码，直接定义特有属性和共有属性就好了。
- 不用创建临时对象，因为 new 会帮你做（你使用「this」就可以访问到临时对象）；
- 不用绑定原型，因为 new 会帮你做（new 为了知道原型在哪，所以指定原型的名字为 prototype）；
- 不用 return 临时对象，因为 new 会帮你做；
- 不要给原型想名字了，因为 new 指定名字为 prototype。

---

## 事件委托

- 监听父元素，看触发事件的元素是哪个子元素，这就是事件委托。
- 可以监听动态生成的元素，省监听器。
~~~
function listen(element, eventType, selector, fn){
 element.addEventListener(eventType, e=>{
     if(e.target.matches(selector)){
         fn.call(el, e, el)
     }
 })
}
~~~

---

## HTTP 状态码 
100	Continue  	继续。客户端应继续其请求

101	Switching Protocols	切换协议。

200	OK	请求成功。一般用于GET与POST请求

201	Created	已创建。成功请求并创建了新的资源

202	Accepted	已接受。已经接受请求，但未处理完成

204	No Content	无内容。服务器成功处理，但未返回内容。在未更新网页的情况下，可确保浏览器继续显示当前文档

301	Moved Permanently	永久移动。请求的资源已被永久的移动到新URI，返回信息会包括新的URI，浏览器会自动定向到新URI。今后任何新的请求都应使用新的URI代替

302	Found	临时移动。与301类似。但资源只是临时被移动。客户端应继续使用原有URI

400	Bad Request	客户端请求的语法错误，服务器无法理解

403	Forbidden	服务器理解请求客户端的请求，但是拒绝执行此请求

404	Not Found	服务器无法根据客户端的请求找到资源（网页）。通过此代码，网站设计人员可设置"您所请求的资源无法找到"的个性页面

405	Method Not Allowed	客户端请求中的方法被禁止

408	Request Time-out	服务器等待客户端发送的请求时间过长，超时

409	Conflict	服务器完成客户端的PUT请求是可能返回此代码，服务器处理请求时发生了冲突

500	Internal Server Error	服务器内部错误，无法完成请求

501	Not Implemented	服务器不支持请求的功能，无法完成请求

502	Bad Gateway	作为网关或者代理工作的服务器尝试执行请求时，从远程服务器接收到了一个无效的响应

503	Service Unavailable	由于超载或系统维护，服务器暂时的无法处理客户端的请求。延时的长度可包含在服务器的Retry-After头信息中

504	Gateway Time-out	充当网关或代理的服务器，未及时从远端服务器获取请求

505	HTTP Version not supported	服务器不支持请求的HTTP协议的版本，无法完成处理

---

## HTTP 缓存
- 在请求头中加'cache-Control': 'max-age=10000'， 表示在请求后的10000秒内再次请求同样的 URL，就直接在内存里返回。当资源需要升级的时候就改一下URL。
- E-Tag 如果这次请求的 E-tag 与上次的是一样，就不下载资源了，但依然会发出请求。

---

## Cookie / Session 
### Cookie
- HTTP响应通过 Set-Cookie 设置 Cookie
- 浏览器访问指定域名是必须带上 Cookie 作为 Request Header
- Cookie 一般用来记录用户信息
### Session
- Session 是服务器端的内存（数据）
- Session 一般通过在 Cookie 里记录 SessionID 实现
- SessionID 一般是随机数

1. 访问 URL 时，通过 Cookie 将 SessionID 发给服务端。
2. 服务端读取 SessionID，在服务端保存了所有 Session 的内存里，根据 SessionID 得到对应用户的隐私信息。

### Cookie 与 LocalStorage 区别
- LocalStorage 跟 http 无关。
- HTTP 不会带上 LocalStorage 的值 ，但会带 Cookie。
- 只有相同域名的页面才能互相读取 LocalStorage。
- 每个域名 LocalStorage 最大存储量为 5mb 左右, Cookie 大小一般4k以下。
- LocalStorage 永久有效，除非用户清除。
- SessionStorage 和 LocalStorage 唯一区别，SessionStorage 关闭页面后失效。

---

## GET / POST 的区别    
- 参数。GET 的参数放在 url 的查询参数里，POST 的参数（数据）放在请求消息体里。
- 安全（扯淡）。GET 没有 POST 安全（都不安全）
- GET 的参数（url查询参数）有长度限制，一般是 1024 个字符。POST 的参数（数据）没有长度限制（扯淡，4~10Mb 限制）
- 包。GET 请求只需要发一个包，POST 请求需要发两个以上包（因为 POST 有消息体）（扯淡，GET 也可以用消息体）
- GET 用来读数据，POST 用来写数据，POST 不幂等（幂等的意思就是不管发多少次请求，结果都一样。）

GET和POST本质上就是TCP链接，并无差别。但是由于HTTP的规定和浏览器/服务器的限制，导致他们在应用过程中体现出一些不同。 

---

## 跨域
- ### JSONP
请求方：frank.com 的前端程序员（浏览器）

响应方：jack.com 的后端程序员（服务器）

请求方创建 script，src 指向响应方，同时传一个查询参数  ?callbackName=yyy

响应方根据查询参数callbackName，构造形如

yyy.call(undefined, '你要的数据')

yyy('你要的数据')

这样的响应

浏览器接收到响应，就会执行 yyy.call(undefined, '你要的数据')
那么请求方就知道了他要的数据

这就是 JSONP

JSONP 不支持 POST 请求，因为是动态创建 script 的，动态创建 script 的时候只能用 GET，没办法用POST

~~~
// 原生 
button.addEventListener('click', (e)=>{
    let script = document.createElement('script')
    let functionName = 'frank'+ parseInt(Math.random()*10000000 ,10)
    window[functionName] = function(){  // 每次请求之前搞出一个随机的函数
        amount.innerText = amount.innerText - 0 - 1
    }
    script.src = '/pay?callback=' + functionName
    document.body.appendChild(script)
    script.onload = function(e){ // 状态码是 200~299 则表示成功
        e.currentTarget.remove()
        delete window[functionName] // 请求完了就干掉这个随机函数
    }
    script.onerror = function(e){ // 状态码大于等于 400 则表示失败
        e.currentTarget.remove()
        delete window[functionName] // 请求完了就干掉这个随机函数
    }
})

// jQuery 
$.ajax({
 url: "http://jack.com:8002/pay",
 dataType: "jsonp",
 success: function( response ) {
     if(response === 'success'){
     amount.innerText = amount.innerText - 1
     }
 }
 })

 $.jsonp()
~~~

- ### CORS
是一个W3C标准，全称是"跨域资源共享"（Cross-origin resource sharing）。

在请求头设置
setHeader('Access-Control-Allow-Origin': 'http://.....')

CORS与JSONP的使用目的相同，但是比JSONP更强大。

JSONP只支持GET请求，CORS支持所有类型的HTTP请求。JSONP的优势在于支持老式浏览器，以及可以向不支持CORS的网站请求数据。

- ### postMessage  

---