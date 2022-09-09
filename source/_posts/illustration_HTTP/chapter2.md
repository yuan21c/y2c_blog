---
title: 《图解HTTP》第二章 简单的 HTTP 协议
date: 2022-09-09 14:59:27
updated: 2022-09-09 14:59:27
categories: 图解HTTP
tags: 
    - web
    - HTTP
    - WWW
description: 
top_img: https://iili.io/66LbYF.jpg
cover: https://iili.io/66LxqB.jpg
---

## HTTP 协议用于客户端和服务器端之间的通信

在两台计算机之间使用 HTTP 协议通信时，在一条通信线路上必定有一端是客户端，另一端则是服务器端。 HTTP 协议能够明确区分哪端是客户端，哪端是服务器端。

## 通过请求和响应的交换达成通信

![HTTP 请求与响应](https://iili.io/P93e4a.jpg)

下面是从客户端发送给某个 HTTP 服务器端的请求报文中的内容。

``` plain
GET /index.htm HTTP/1.1 
Host: hackr.jp
```

+ 起始行开头的GET表示请求访问服务器的类型，称为方法（method）。
+ 随后的字符串 /index.htm 指明了请求访问的资源对象，也叫做请求 URI（request-URI）。
+ 最后的 HTTP/1.1，即 HTTP 的版本号，用来提示客户端使用的 HTTP 协议功能。

综合来看，这段请求内容的意思是：请求访问某台 HTTP 服务器上的 `/index.htm` 页面资源。

请求报文是由**请求方法**、**请求 URI**、**协议版本**、**可选的请求首部字段**和**内容实体构成的**。

![请求报文的构成](https://iili.io/P9fjQS.jpg)

接收到请求的服务器，会将请求内容的处理结果以响应的形式返回。

```plain
HTTP/1.1 200 OK
Date: Tue, 10 Jul 2012 06:50:15 GMT
Content-Length: 362 
Content-Type: text/html

<html>
……

```

+ 起始行开头的 HTTP/1.1 表示服务器对应的 HTTP 版本。
+ 紧挨着的 200 OK 表示请求的处理结果的状态码（status code）和原因短语（reason-phrase）。
+ 下一行显示了创建响应的日期时间，是首部字段（header field）内的一个属性。
+ 接着以一空行分隔，之后的内容称为资源实体的主体（entity body）。

响应报文基本上由**协议版本**、**状态码**（表示请求成功或失败的数字代码）、用以解释状态码的**原因短语**、可选的**响应首部字段**以及**实体主体**构成。

![响应报文的构成](https://iili.io/P9qot2.jpg)

## HTTP 是不保存状态的协议

HTTP 是一种不保存状态，即无状态（stateless）协议。这是为了更快地处理大量事务，确保协议的可伸缩性，而特意把 HTTP 协议设计成如此简单的。

HTTP/1.1 虽然是无状态协议，但为了实现期望的保持状态功能，于是引入了 Cookie 技术。有了 Cookie 再用 HTTP 协议通信，就可以管理状态了。

## 请求 URI 定位资源

指定请求 URI 的方式有很多。

![以 http://hackr.jp/index.htm 作为请求的例子](https://iili.io/P9xXTb.jpg)

除此之外，如果不是访问特定资源而是对服务器本身发起请求，可以用一个 * 来代替请求 URI。下面这个例子是查询 HTTP 服务器端支持的 HTTP 方法种类。

```plain
OPTIONS * HTTP/1.1
```

## 告知服务器意图的 HTTP 方法

### GET ：获取资源

GET 方法用来请求访问已被 URI 识别的资源。指定的资源经服务器端解析后返回响应内容。也就是说，如果请求的资源是文本，那就保持原样返回；如果是像 CGI（Common Gateway Interface，通用网关接口）那样的程序，则返回经过执行后的输出结果。

|||
|--|--|
|**请求**| GET /index.html HTTP/1.1 </br> Host: www.hackr.jp |
|**响应**| 返回 index.html 的页面资源                          |

|||
|--|--|
|**请求**| GET /index.html HTTP/1.1 </br> Host: www.hackr.jp </br> If-Modified-Since: Thu, 12 Jul 2012 07:30:00 GMT |
|**响应**| 仅返回2012年7 月12日7 点30分以后更新过的index.html页面资源。如果未有内容更新，则以状态码304 Not Modified作为响应返回|

### POST：传输实体主体

虽然用 GET 方法也可以传输实体的主体，但一般不用 GET 方法进行传输，而是用 POST 方法。虽说 POST 的功能与 GET 很相似，但 POST 的主要目的并不是获取响应的主体内容。

|||
|--|--|
|请求|POST /submit.cgi HTTP/1.1 </br> Host: www.hackr.jp </br> Content-Length: 1560（1560字节的数据）|
|响应|返回 submit.cgi 接收数据的处理结果|

### PUT：传输文件

PUT 方法用来传输文件。就像 FTP 协议的文件上传一样，要求在请求报文的主体中包含文件内容，然后保存到请求 URI  指定的位置。

但是，鉴于 HTTP/1.1 的 PUT 方法自身不带验证机制，任何人都可以上传文件 , 存在安全性问题，因此一般的 Web 网站不使用该方法。若配合 Web 应用程序的验证机制，或架构设计采用 REST（REpresentational State Transfer，表征状态转移）标准的同类 Web 网站，就可能会开放使用 PUT 方法。

|||
|--|--|
|请求|PUT /example.html HTTP/1.1 Host: www.hackr.jp </br> Content-Type: text/html </br> Content-Length: 1560（1560 字节的数据）|
|响应|响应返回状态码 204 No Content（比如 ：该 html 已存在于服务器上）|

### HEAD：获得报文首部

HEAD 方法和 GET 方法一样，只是不返回报文主体部分。用于确认 URI 的有效性及资源更新的日期时间等。

|||
|--|--|
|请求|HEAD /index.html HTTP/1.1 </br> Host: www.hackr.jp|
|响应|返回index.html有关的响应首部|

### DELETE：删除文件

DELETE 方法用来删除文件，是与 PUT 相反的方法。DELETE 方法按请求 URI 删除指定的资源。

|||
|--|--|
|请求|DELETE /example.html HTTP/1.1 </br> Host: www.hackr.jp|
|响应|响应返回状态码 204 No Content（比如 ：该 html 已从该服务器上删除）|

### OPTIONS：询问支持的方法

OPTIONS 方法用来查询针对请求 URI 指定的资源支持的方法。

|||
|--|--|
|请求|OPTIONS * HTTP/1.1 </br> Host: www.hackr.jp|
|响应|HTTP/1.1 200 OK </br>Allow: GET, POST, HEAD, OPTIONS </br> （返回服务器支持的方法）|

### TRACE：追踪路径

TRACE 方法是让 Web 服务器端将之前的请求通信环回给客户端的方法。

发送请求时，在 Max-Forwards 首部字段中填入数值，每经过一个服务器端就将该数字减 1，当数值刚好减到 0 时，就停止继续传输，最后接收到请求的服务器端则返回状态码 200 OK 的响应。

客户端通过 TRACE  方法可以查询发送出去的请求是怎样被加工修改/ 篡改的。这是因为，请求想要连接到源目标服务器可能会通过代理中转，TRACE 方法就是用来确认连接过程中发生的一系列操作。
但是，TRACE  方法本来就不怎么常用，再加上它容易引发XST（Cross-Site  Tracing，跨站追踪）攻击，通常就更不会用到了。

|||
|--|--|
|请求|TRACE / HTTP/1.1 </br> Host: hackr.jp </br> Max-Forwards: 2 |
|响应|HTTP/1.1 200 OK </br> Content-Type: message/http</br>Content-Length: 1024 </br></br> TRACE / HTTP/1.1 </br> Host: hackr.jp </br> Max-Forwards: 2（返回响应包含请求内容）

### CONNECT：要求用隧道协议连接代理

CONNECT 方法要求在与代理服务器通信时建立隧道，实现用隧道协议进行 TCP 通信。主要使用 SSL（Secure Sockets Layer，安全套接 层）和 TLS（Transport Layer Security，传输层安全）协议把通信内容加 密后经网络隧道传输。

|||
|--|--|
|请求|CONNECT proxy.hackr.jp:8080 HTTP/1.1 </br> Host: proxy.hackr.jp|
|响应|HTTP/1.1 200 OK（之后进入网络隧道）|

## 使用方法下达命令

向请求 URI 指定的资源发送请求报文时，采用称为方法的命令。

![使用方法下达命令](https://iili.io/P9hnn4.jpg)

|方法|说明|支持的 HTTP 协议版本|
|--|--|--|
|GET|获取资源|1.0、1.1|
|POST|传输实体主体|1.0、1.1|
|PUT|传输文件|1.0、1.1|
|HEAD|获得报文首部|1.0、1.1|
|DELETE|删除文件|1.0、1.1|
|OPTIONS|询问支持的方法|1.1|
|TRACE|追踪路径|1.1|
|CONNECT|要求用隧道协议连接代理|1.1|
|LINK|建立和资源之间的联系|1.0|
|UNLINE|断开连接关系|1.0|

## 持久连接节省通信量

HTTP 协议的初始版本中，每进行一次 HTTP 通信就要断开一次 TCP 连接。

以当年的通信情况来说，因为都是些容量很小的文本传输，所以即使这样也没有多大问题。可随着 HTTP 的普及，文档中包含大量图片的情况多了起来。

比如，使用浏览器浏览一个包含多张图片的 HTML 页面时，在发送请求访问 HTML 页面资源的同时，也会请求该 HTML 页面里包含的其他资源。因此，每次的请求都会造成无谓的 TCP 连接建立和断 开，增加通信量的开销。

### 持久化连接

为解决上述 TCP 连接的问题，HTTP/1.1 和一部分的 HTTP/1.0 想出了持久连接（HTTP Persistent Connections，也称为 HTTP keep-alive 或 HTTP connection reuse）的方法。

***只要任意一端没有明确提出断开连接，则保持 TCP 连接状态。***

**持久连接的好处**在于减少了 TCP 连接的重复建立和断开所造成的额外开销，减轻了服务器端的负载。另外，减少开销的那部分时间，使 HTTP 请求和响应能够更早地结束，这样 Web 页面的显示速度也就相应提高了。

![持久连接旨在建立 1 次 TCP 连接后进行多次请求和响应的交互](https://iili.io/P9wEyF.jpg)

### 管线化

管线化技术不用等待响应亦可直接发送下一个请求。

这样就能够做到同时并行发送多个请求，而不需要一个接一个地等待响应了。

![不等待响应，直接发送下一个请求](https://iili.io/P9w1v1.jpg)

### 使用 Cookie 的状态管理

HTTP 是无状态协议

+ 优点：减少服务器的 CPU 及内存资源的消耗。

+ 缺点：无法进行状态的管理。

解决方法： Cookie 技术。

Cookie 技术通过在请求和响应报文中写入 Cookie 信息来控制客户端的状态。

![没有 Cookie 信息状态下的请求](https://iili.io/P9One9.jpg)

![第 2 次以后（存有 Cookie 信息状态）的请求](https://iili.io/P9OC57.jpg)

HTTP 请求报文和响应报文的内容如下:

1. 请求报文（没有 Cookie 信息的状态）

    ```plain
    GET /reader/ HTTP/1.1
    Host: hackr.jp
    *首部字段内没有Cookie的相关信息
    ```

2. 响应报文（服务器端生成 Cookie 信息）

    ```plain
    HTTP/1.1 200 OK
    Date: Thu, 12 Jul 2012 07:12:20 GMT
    Server: Apache
    ＜Set-Cookie: sid=1342077140226724; path=/; expires=Wed, 10-Oct-12 07:12:20 GMT＞
    Content-Type: text/plain; charset=UTF-8
    ```

3. 请求报文（自动发送保存着的 Cookie 信息）

    ```plain
    GET /image/ HTTP/1.1
    Host: hackr.jp
    Cookie: sid=1342077140226724
    ```
