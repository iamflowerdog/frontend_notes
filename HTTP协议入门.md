## 一、HTTP/0.9

* 超文本传输协议： `hypertext transfer protocol`
* HTTP 协议是互联网的基础协议，也是网页开发的必备知识，最新版本 HTTP/2 更是让它成为技术热点。
* HTTP 是基于 TCP/IP 协议的应用层协议。它不涉及数据包（packet）传输，主要规定了客户端和服务器之间的通信格式，默认使用80端口。

* 最早版本1991年，0.9版，只有一个命令 `get`

```
GET /index.html
```
* 上面命令表示，TCP链接建立后，客户端向服务器请求网页 `index.html`。
* 协议规定，服务器只能回应HTML格式的字符串，不能回应别的格式

```
<html>
  <body>Hello World</body>
</html>

```

* 服务器发送完毕，就关闭TCP连接

#### 二、HTTP/1.0

* 1996年发布，协议内容增加，可以发送任何格式的内容，图像、视频、二进制文件；
* 除了 `get` 命令，还引入了 `post` 和 `HEAD` 命令，丰富了浏览器和服务器的互动手段
* 再次，HTTP请求和回应格式也变了，除了数据部分，每次通信必须包含头信息 (HTTP header),用来描述一些元数据
* 请求格式：

```
GET / HTTP/1.0
User-Agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_10_5)
Accept: */*
```

* 第一行是请求命令，必须在尾部添加协议版本(`HTTP/1.0`)
* 后面就是多行头信息，描述客户端的情况

* 回应格式：

```
HTTP/1.0 200 OK 
Content-Type: text/plain
Content-Length: 137582
Expires: Thu, 05 Dec 1997 16:00:00 GMT
Last-Modified: Wed, 5 August 1996 15:55:28 GMT
Server: Apache 0.84

<html>
  <body>Hello World</body>
</html>
```

* 回应的格式是"头信息 + 一个空行（\r\n） + 数据"。其中，第一行是"协议版本 + 状态码（status code） + 状态描述"。
* 下面是一些常见的 `Content-Type`字段的值

```
text/plain
text/html
text/css
image/jpeg
image/png
image/svg+xml
audio/mp4
video/mp4
application/javascript
application/pdf
application/zip
application/atom+xml

```
* 这些数据类型总称为 `MIME type` , 每个值包括一级类型和二级类型，之间用斜杠分隔

* Content-Encoding 字段

* 服务端可以把数据压缩后再发送

```
Content-Encoding: gzip
Content-Encoding: compress
Content-Encoding: deflate
```

* 客户端在请求时，用 `Accept-Encoding` 字段说明自己可以接受哪种压缩方法

```
Accept-Encoding: gzip, deflate
```

#### 缺点

* HTTP/1.0 版的主要缺点是，每个TCP连接只能发送一个请求，发送数据完毕，连接就关闭，如果还要请求其他资源，就必须新建一个连接。
* TCP连接新建成本很高，因为需要客户端和服务端三次握手，并且开始时发送速率比较慢 (slow start)
* 非标准 `Connection` 字段

```
Connection: keep-alive
```

* 这个字段要求服务器不要关闭TCP连接，以便其他请求复用，服务器也同样回应这个字段

```
Connection: keep-alive
```

* 一个可以复用的TCP连接就建立了，直到客户端或服务器主动关闭连接。但是，这不是标准字段，不同实现的行为可能不一致，因此不是根本的解决办法。

#### 三、HTTP/1.1

* 1997年一月，HTTP/1.1版本发布，一直沿用至今
* 持久化连接 `persistent connection`,不用声明`Connection: keep-alive`;
* 客户端和服务器发现对方一段时间灭有活动，就主动关闭连接，不过规范的做法时，客户端在最后一个请求时，发送 `Connection: close`,明确要求服务器关闭TCP连接
* 目前，对于同一个域名，大多数浏览器允许同时建立6个持久连接。

#### 管道机制

* 同一个TCP连接里面，客户端可以同时发送多个请求，服务端还是按顺序先回应A请求，再回应B请求
* 
* Content-length 区分数据包是属于哪一个回应的

```
Content-Length: 3495
```

* 上面代码告诉浏览器，本次回应的长度是3495字节，后面的字节就属于下一个回应了

#### 分块传输编码

* 使用 `Content-length` 字段的前提条件是，服务器发送回应之前，就必须指导回应的数据长度，耗时，效率不高

* 使用 分块传输编码 chunked transfer encoding

```
Transfer-Encoding: chunked
```
* 每个非空的数据块之前，会有一个16进制的数值，表示这个块的长度。最后是一个大小为0的块，就表示本次回应的数据发送完了。下面是一个例子。

```
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

0

```

#### 其他功能

* 1.1还新增了许多动词方法： PUT、PATCH、HEAD、 OPTIONS、DELETE。
* 客户端请求的头信息新增了 HOST字段，用来指定服务器的域名

```
Host: www.example.com
```

* 有了Host字段，可以 将请求发往同一台服务器上不同的网站，为虚拟主机的星期打下了基础

#### 缺点

* TCP连接里面，所有的数据通信是按次第进行的，服务器只有处理完一个回应，才会进行下一个回应
* 要是前面回应的特别慢，后面就会请求排队等着，队头堵塞(Head-of-line blocking)
* 解决办法 ：一是减少请求数，二是同时多开持久连接。
* 优化网页的技巧：

    1. 合并脚本和样式表，将图片嵌入CSS代码
    2. 域名分片 (domain sharding)

* 如果HTTP协议设计的更好一些，这些额外工作是可以避免的












