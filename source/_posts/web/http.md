---

title: http
date: 2016-02-06
categories: [web]
tags: [http]

---





## http



请求：Accept-Encoding

响应：Content-Encoding

取值：gzip、deflate、sdch

作用：对请求体和响应体进行压缩，压缩文本数据能减少带宽并加快显示速度。压缩的时间会远小于传输的时间，所以不用担心压缩。

请求头

响应头

Connection

请求：Connection

响应：Connection

取值范围：

Keep-Alive、Close

作用：

Keep-Alive：可以减少TCP建立成本，销毁成本。（长连接），但是占用端口时间长，高并发时需要考虑。

Close：每次连接将使用新的TCP连接

在请求一个网址时，返回最终页面的内容大多数有多个请求组成(css、js、png等资源的请求），所以如果开启keep-alive可以让页面的所有请求都在一次tcp连接建立后传输。

请求

响应头

Cookie

响应：Set-Cookie

如：sid = test; path=/;    键值对形式

请求：Cookie

如：sid = test;

特殊值：expires：失效时间，path:该Cookie适用于哪些请求路径，domain：试用于哪些域名。

当服务端Set-Cookie时，浏览器记录此键值对的值并在下次请求时提交上去。

session通过Cookie实现

Cookie大小客户端服务端实现有可能不一样，一般4K.

响应头

请求头

Accept-Language

请求：Accept-Language

取值范围：

en,zh-CN,zh;q=0.8,zh;q=0.6,zh-TW;q=0.4

其中q代表权重，en默认权重为1

作用：

客户端接收的语言。根据此值做本地化判断，如：英文与中文页面的切换。

image.png

Referer

请求：Referer

客户端请求时添加此值，标识从哪个网站跳过来的。

可做资源防盗链时使用。

referer

User-Agent

请求：User-Agent

值如：

Mozilla/5.0 (Windows NT 6.1; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/60.0.3112.90 Safari/537.36

客户端的一些信息，包括：客户端硬件信息，操作系统，浏览器信息等。

作用：

根据这个值做一些数据统计分析，如果是手机端则推送适合手机的内容。

User-Agent

Modified-Since

请求：If-Modified-Since

响应：Last-Modified

值如：Fri, 23 Oct 2015 05:36:06 GM

作用：

客户端先保存服务端的Last-Modified与此资源信息到本地，当此资源以后请求时，把此值设为If-Modified-Since并请求到服务器。

服务端判断此值未变或不需要更新时返回304，表明客户端可直接使用缓存。

请求头

响应头

Cache-Control

响应：cache-control

值如：max-age=121737619或private, max-age=0, no-cache

max-age设置缓存多少时间，max-age=0就是没有缓存。

作用：

控制缓存时间，相对时间长度。

image.png

image.png

Expires

响应：Expires

值如：Wed, 25 Oct 2017 09:05:12 GMT

设置绝对时间

作用：

指定到特定时间过期。

image.png

Etag

响应：Etag

请求：if-none-match

值如：“zdsfsdf”

作用：

Last-Modified类似，服务端给文件生成一个标识，下次客户端存在if-none-match中提交到服务端，服务端进行比较来判断文件是否改变，从而做出是否缓存决定。

Etag 主要为了解决 Last-Modified 无法解决的一些问题。

比如： 一些文件也许会周期性的更改，但是他的内容并不改变(仅仅改变的修改时间)，这个时候我们并不希望客户端认为这个文件被修改了，而重新GET;

请求头

响应头

Via

响应：via

作用：存放路由信息,CDN中常用。

image.png

Content-Length

请求：Content-Length

响应：content-length

值：数字

作用：代表请求体的大小，或者响应体内容的大小。

image.png

Content-Range

请求：Range,

格式Range:(unit=first byte pos)-[last byte pos]

指定第一个字节的位置和最后一个字节的位置，

响应：Content-range，

格式Content-Range: bytes (unit first byte pos) - [last byte pos]/[entity legth]

指定整个实体中的一部分的插入位置，他也指示了整个实体的长度

值如：

Range:bytes=0-801

Content-Range: bytes 0-800/801

