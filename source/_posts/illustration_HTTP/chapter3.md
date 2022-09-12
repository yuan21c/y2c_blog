---
title: 《图解HTTP》第三章 HTTP 报文内的 HTTP 信息
date: 2022-09-10 14:51:09
updated: 2022-09-10 14:51:09
categories: 图解HTTP
tags: 
    - web
    - HTTP
    - WWW
description: 
top_img: https://iili.io/66LbYF.jpg
cover: https://iili.io/66LxqB.jpg
---

## HTTP 报文

用于 HTTP 协议交互的信息被称为 **HTTP 报文**。

请求端（客户端）的 HTTP 报文叫做**请求报文**。

响应端（服务器端）的 HTTP 报文叫做**响应报文**。

HTTP 报文本身是由多行（用 CR+LF 作换行符）数据构成的字符串文本。

![请求报文（上）和响应报文（下）的结构](https://iili.io/PFiCQa.jpg)

![请求报文（上）和响应报文（下）的实例](https://iili.io/PFioCJ.jpg)

### 报文头部内容的组成

+ **请求行**

    包含用于请求的方法、请求 URI 和 HTTP 版本。

+ **状态行**

    包含 HTTP 版本、表明响应结果的状态码、原因短语。

    一般有 4 种首部，分别是：**通用首部**、**请求首部**、**响应首部**和**实体首部**。

+ **首部字段**

    包含表示请求和响应的各种条件和属性的各类首部。

+ **其他**

    可能包含 HTTP 的 RFC 里未定义的首部（Cookie 等）。

## 编码提升传输速率

+ **报文（message）**

    是 HTTP 通信中的基本单位，由 8 位组字节流（octet sequence，其中 octet 为 8 个比特）组成，通过 HTTP 通信传输。

+ **实体（entity）**

    作为请求或响应的有效载荷数据（补充项）被传输，其内容由实体首部和实体主体组成。

HTTP 报文的主体用于传输请求或响应的实体主体。

通常，报文主体等于实体主体。只有当传输中进行编码操作时，实体主体的内容发生变化，才导致它和报文主体产生差异。

> 理解：
>
> 实际需要传输的内容即为**实体主体**。
> **实体头部**是对实体主体的描述，实体头部和实体主体一起构成了**实体**。
> 实体头部保存在**报文首部**，实体主体包含在**报文主体**内。
> **报文首部**包含请求行、请求首部字段、通用首部字段、**实体首部**字段等。
> 如果没有编码，则**报文主体**和**实体主体**相同。
> 如果有编码，**实体主体**则是**报文主体**的一部分。
>
> 参考：[http报文和实体的差别？ - 知乎用户的回答 - 知乎](https://www.zhihu.com/question/263752229/answer/614142472)

## 压缩传输的内容编码

内容编码指明应用在**实体**内容上的编码格式，并保持实体信息原样压缩。内容编码后的实体由客户端接收并负责解码。

> 编码的是**实体主体**

常用的内容编码有以下几种。

+ gzip（GNU zip）
+ compress（UNIX 系统的标准压缩）
+ deflate（zlib）
+ identity（不进行编码）

## 分割发送的分块传输编码

在 HTTP 通信过程中，请求的编码实体资源尚未全部传输完成之前，浏览器无法显示请求页面。在传输大容量数据时，通过把数据分割成多块，能够让浏览器逐步显示页面。

这种把*实体主体*分块的功能称为**分块传输编码（Chunked Transfer Coding）**。

分块传输编码会将实体主体分成多个部分（块）。每一块都会用十六进制来标记块的大小，而实体主体的最后一块会使用“0(CR+LF)”来标记。

> CR: Carriage Return, 回车符， 16 进制 0x0d
> LF: Line Feed, 换行符， 16 进制 0x0a

示例：

```http
HTTP/1.1 200 OK
Content-Type: text/plain
Transfer-Encoding: chunked

25
This is the data in the first chunk

1C
and this is the second one

3
con

8
sequence

0(CR+LF)
```

## 发送多种数据的多部分对象集合

HTTP 协议采用了多部分对象集合(Multipart)，允许发送的一份报文主体内可含有多类型实体。通常是在图片或文本等上传文件时使用。

多部分对象集合包含的对象如下：

+ multipart/form-data

    在 Web 表单文件上传时使用

    ```http
    Content-Type: multipart/form-data; boundary=AaB03x

    --AaB03x
    Content-Disposition: form-data; name="field1"

    Joe Blow
    --AaB03x
    Content-Disposition: form-data; name="pics"; filename="file1.txt" Content-Type: text/plain

    ...（file1.txt的数据）...
    --AaB03x--

    ```

+ multipart/byteranges

    状态码 206（Partial Content，部分内容）响应报文包含了多个范围的内容时使用。

    ```http
    HTTP/1.1 206 Partial Content
    Date: Fri, 13 Jul 2012 02:45:26 GMT
    Last-Modified: Fri, 31 Aug 2007 02:02:20 GMT
    Content-Type: multipart/byteranges; boundary=THIS_STRING_SEPARATES


    --THIS_STRING_SEPARATES
    Content-Type: application/pdf Content-Range: bytes 500-999/8000

    ...（范围指定的数据）...
    --THIS_STRING_SEPARATES
    Content-Type: application/pdf Content-Range: bytes 7000-7999/8000

    ...（范围指定的数据）...
    --THIS_STRING_SEPARATES--

    ```

在 HTTP 报文中使用多部分对象集合时，需要在首部字段里加上 Content-type。

使用 boundary 字符串来划分多部分对象集合指明的各类实体。在
boundary   字符串指定的各个实体的起始行之前插入 `--` 标记（例如：`--AaB03x`、`--THIS_STRING_SEPARATES`），而在多部分对象集合对应的字符串的最后插入 `--` 标记（例如：`--AaB03x--`、`--THIS_STRING_SEPARATES--`）作为结束。

多部分对象集合的每个部分类型中，都可以含有首部字段。另外，可以在某个部分中嵌套使用多部分对象集合。有关多部分对象集合更详细的解释，请参考 [RFC 2046](https://www.rfc-editor.org/rfc/rfc2046)。

## 获取部分内容的范围请求

执行范围请求时，会用到首部字段 Range 来指定资源的 byte 范围。byte 范围的指定形式如下。

+ 5001~10 000 字节

    ```http
    Range: bytes=5001-10000
    ```

+ 从 5001 字节之后全部的

    ```http
    Range: bytes=5001-
    ```

+ 从一开始到 3000 字节和 5000~7000 字节的多重范围

    ```http
    Range: bytes=-3000, 5000-7000
    ```

针对范围请求，响应会返回状态码为 206 Partial Content 的响应报文。

对于多重范围的范围请求，响应会在首部字段 Content- Type 标明 multipart/byteranges 后返回响应报文。

如果服务器端无法响应范围请求，则会返回状态码 200 OK 和完整的实体内容。

## 内容协商返回最合适的内容

**内容协商机制**是指客户端和服务器端就响应的资源内容进行交涉，然后提供给客户端最为适合的资源。内容协商会以响应资源的*语言*、*字符集*、*编码方式*等作为判断的基准。

包含在请求报文中的某些首部字段（如下）就是判断的基准。

+ Accept
+ Accept-Charset
+ Accept-Encoding
+ Accept-Language
+ Content-Language

内容协商技术有以下 3 种类型：

+ 服务器驱动协商（Server-driven  Negotiation）

    由服务器端进行内容协商。以请求的首部字段为参考，在服务器端自动处理。但对用户来说，以浏览器发送的信息作为判定的依据，并不一定能筛选出最优内容。

+ 客户端驱动协商（Agent-driven  Negotiation）

    由客户端进行内容协商的方式。用户从浏览器显示的可选项列表中手动选择。还可以利用 JavaScript 脚本在 Web 页面上自动进行上述选 择。比如按 OS 的类型或浏览器类型，自行切换成 PC 版页面或手机版页面。

+ 透明协商（Transparent Negotiation）

    是服务器驱动和客户端驱动的结合体，是由服务器端和客户端各自进行内容协商的一种方法。
