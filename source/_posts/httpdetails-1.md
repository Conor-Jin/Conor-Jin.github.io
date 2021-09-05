---
title: http详解
tags: []
id: '1'
categories:
  - - 网络
date: 2018-09-05 00:19:34
---

## **什么是http协议：**

引用百度百科的话说来就是：http协议其实就是超文本传输协议，超文本传输协议 (HTTP-Hypertext transfer protocol) 是一种详细规定了浏览器和万维网服务器之间互相通信的规则，通过因特网传送万维网文档的数据传送协议。目前我们使用的http版本是http/1.1其前身是http/1.0。关于两个版本不同，下面会不时提及。在整个iso传输层次模型中http处于最高层次，而tcp是处于下面一层传输层，也就是说http是基于tcp协议建立的连接，所以http传输建立之前需要先建立tcp连接，也就是三次握手，在建立tcp连接之后方可真正请求响应请求。

## **http传输过程详解：**

当我们发送一个ajax请求，或者地址栏输入url后，我们的浏览器就给web服务器发送一个request，之后服务器处理完成后返回响应的response给浏览器。之后浏览器拿到数据进行解析里面数据从而生成我们页面或者组装数据。 期间传输还有可能经历了代理服务器（目前很多很多网站都用代理服务器，主要原因是其隐蔽。。）从而实现服务器端文件缓存。 http传输是面向连接的，也就是说如果连接没有中断，可以继续发送请求，这个设置可以在请求头Connection来设置，例如：我通过一个url请求了一个html页面之后， 经解析，html页面中包含对图片的请求，则会直接再向服务器发起请求而不必重新建立tcp连接。等到所有请求都就绪，方可完成一次页面加载或者请求完毕。

## **url详解：**

无论是ajax请求还是地址栏输入url，都要用到请求地址，请求地址用来描述需要请求的资源位置以及筛选方式：大体结构如下 http://www.jindk.wang/blog/index.php/2018/09/05/duplicateremoval/index.html?name=yuchao&age=26#modfiled 这个url分为几个部分： http：表示底层使用的协议（如http、https、ftp） www.jindk.wang：表示服务器域名（或者是ip地址） /blog/index.php/2018/09/05/duplicateremoval/：表示资源路径 ?name=yuchao&age=26：发送给服务器数据 #modfiled：锚点  

## http消息结构：

整个http消息结构分为request以及response两部分：为了便于讲解，我从w3c截取一个图如下： ![](http://jindk.wang/blog/wp-content/uploads/2018/09/20131226161724328-300x197.png)                       这是从chrome的Network截图，且不管每个浏览器将其如何区分，按照我们看到的来分组： 上面第一部分是请求资源地址以及请求方式属于request部分 第二部分是返回状态码，属于response部分 第三部分是request部分，第四部分是response部分。 总体来说整个请求分为两个部分我们来分析里面主要的结构如下：

## **request部分分析：**

请求的url即我们地址栏输入的url或者ajax请求的那个参数url。 请求方式：常用的有get、post以及head请求： head请求：head请求是一种返回不呈现数据的请求，也就是只请求一个报文头，通常用于请求一个文件去判断文件是否更新或者在我的项目中去请求服务器时间。 get与post比较： get请求一般都会用来查询资源信息，post请求一般会用来更新资源信息。 get提交数据方式是将参数放置url之后用&来分开例如http://www.temas.com/myBlog/file/date.php?**name=yuchao&age=26，** post请求可以以对象字面量形式进行参数传输：{name:"yuchao";age:"26"}，所以通过post方式发送的请求中包含内容这一项，而get请求直接将内容附在url之后 正是由于数据传输方式不同导致get传输数据量需要在url字节限制范围之内，而post几乎无限制。同时get参数放置于url中也不利于安全。 Accept：表示浏览器可以接受的类型，一般浏览器都会发给服务器\*表示通配所有类型。text/html类型就表示我们常说的html文档。 当我们规定了一种类型时候而服务器没有这种类型可以返回，则会抛出一个406状态码的错误(no acceptable) Accept-Encoding：浏览器自身声明接受的编码方式，通常是压缩方法； Accept-Language：浏览器自身声明可以接受的语言例如中文：zh-CN； cookie:将cookie数据发送给服务器 Connection：可选值有： keep-alive:当一个网页打开完成后，客户端和服务器之间用于传输HTTP数据的TCP连接不会关闭，如果客户端再次访问这个服务器上的网页，会继续使用这一条已经建立的连接， 重新向该服务器发送请求时候不会重新经过三次握手建立链接，而是直接可以进行请求，这个请求时间段可以由服务器端Keep-Alive字段进行设置， 当过了这个时间段之后没有任何请求则关闭该连接。http1.0中默认是close，而目前应用的1.1版本中默认是keep-alive长连接。具体应用看下面response介绍该key； Connection: close  代表一个Request完成后，客户端和服务器之间用于传输HTTP数据的TCP连接会关闭， 当客户端再次发送Request，需要重新建立TCP连接。 User-Agent：客户端使用的浏览器以及操作系统 Cache-Control：浏览器缓存机制，一般会有max-age=值，或者no-cache或者public、private； If-Modified-Since：浏览器缓存内容最后修改时间; if-None-Match:和ETag一起工作，比较两者值 获取内容是否改变。  

## **response部分分析：**

status：返回状态码， HTTP/1.1中定义了5类状态码， 状态码由三位数字组成，第一个数字定义了响应的类别 100-199  提示信息 - 表示请求已被成功接收，继续处理 200-299  成功 - 表示请求已被成功接收，理解，接受 300-399  重定向 - 要完成请求必须进行更进一步的处理 400-499  客户端错误 -  请求有语法错误或请求无法实现 500-599  服务器端错误 -   服务器未能实现合法的请求 我们来看一下一些常见的状态码： 200：OK，表明请求成功完成，所有资源成功发送给客户端； 302：重定向，例如google在中国被黑掉之后，只能转战利用香港服务器去请求，我们输入www.google.com， 服务器就会返回302 Found，并且客户端接收到的response中location字段包含一个新的url地址，然后浏览器会根据这个地址重新发送一个新url的request； 304：使用的缓存文件 400：客户端请求与语法错误，不能被服务器解读； 403：服务器拒绝服务； 404：请求资源不存在； 500 Internal Server Error 服务器发生了不可预期的错误503 Server Unavailable 服务器当前不能处理客户端的请求，一段时间后可能恢复正常 Keep-Alive:**长连接**设置的值，如下图截图： ![](http://jindk.wang/blog/wp-content/uploads/2018/09/20131227131225609-300x86.jpg)   有两个值：timeout以及max，例如：Keep-Alive:timeout=5,max=100，只有当connection为keep-alive并且服务端支持时候才会生效。 其中timeout表示超时时间，max表示最大连接数。即：在5秒之内服务器始终保持空闲连接，在这五秒之内可以发送请求不必重新建立连接，超过这个时间则会重新建立连接进行请求。 在保持持久连接之间每发送一个请求max值就会减少一个，直到为0为止则会自动断开连接。 一般实际开发中，这个值的设置要根据具体网页中嵌入的请求个数去设置：例如网页中有20个图片，五个外部脚本，三个css样式表。则可以根据传输速度设置超时时间5-20秒之内，max值设置为30-100； 这样设计初衷就是为了既能减少不必要的tcp连接，又能避免频繁的请求造成服务器连接池冗余。 这个值从根本上来说跟前端没有太多关系，但是在网站性能优化很是关键。选择多次建立tcp连接还是选择空余一段时间请求被浪费，就要看实际需求以及能否设置出一个合理的Keep-Alive值 Conent-Length：表示返回实体内容长度大小，一般应用在返回静态页面或者一张图片并且数据量不大时候被设置；大小为bite字节；例如一张图片的请求：Connent-Length：630；请求一个图片截图如下： ![](http://jindk.wang/blog/wp-content/uploads/2018/09/20131227131410171-300x114.jpg) Transfer-Encoding：即服务器端不是一个已知的固定的返回实体时候，服务器会一边产生数据，一边发送给客户端， 这时候服务器就需要用Transfer-Encoding：chunked分块编码来代替Conent-Length，设置该key后Content-Length就失效了。 对于前段来说只需关心返回的状态是否是成功即可，但是对于后台需要用到这个设置来判断客户端是否接受完全部数据。[详细请参考](http://blog.csdn.net/zfrong/article/details/6070608) Date：服务器返回数据时间，我经常就用这个值来取得服务器时间 Etag：与if-modified-since配合使用； Last-Modified:作用： 用于指示资源的最后修改日期和时间。一般都用来处理缓存， Content-Type：作用：WEB服务器告诉浏览器自己响应的对象的类型和字符集,例如:Content-Type: text/html; charset=utf-8，Content-Type: image/jpeg server：指明服务器软件版本； Referer：告诉服务器该请求是在哪个链接发过来的，据此可以统计从某个页面跳转过来次数； X-powered0by：表示该网站开发技术  

## **ajax修改获取header：**

利用xmlHttp.setRequestHeader来设置request请求头：例如：xmlHttp.setRequestHeader('cache-control','no-cache'); 利用xmlHttp.getResponseHeader来获取response头信息;例如：xmlHttp.getResponseHeader("Date")； 另外 request.setCharacterEncoding("UTF-8")也可以设置发送到服务端数据编码格式（一般来说发送的编码格式跟服务端解析格式必须是一致的）  

## **链接参考：**

https://blog.csdn.net/u012545279/article/details/17579155