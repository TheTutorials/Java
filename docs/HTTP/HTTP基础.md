# Web 基础

## 因特网的多媒体信使
> 每天，都有数以亿万计的 JPEG 图片、HTML 页面、文本文件、MPEG 电影、WAV
音频文件、Java 小程序和其他资源在因特网上游弋。HTTP 可以从遍布全世界的
Web 服务器上将这些信息块迅速、便捷、可靠地搬移到人们桌面上的 Web 浏览器
上去。

* HTTP 使用的是可靠的数据传输协议

## Web 客服端和服务器
* 客服端负责向服务端发送 `HTTP` 请求，请求可以携带服务端所需要的数据信息
* 服务端负责在 `HTTP` 中响应数据信息

下面的图展示了客服端和服务端请求和相应的

<img src="images/客服端服务器模型.svg">

生活中有很多常见的Web客服端，如微软的 `IE`、`Edge`、以及谷歌的 `Chrome`，`Firefox`、苹果的 `Safari`、基本搜索手机上也是预装了很多的Web 客服端（浏览器）

## Web 资源（Web resource)
* Web 静态资源: 如 `HTML`、图片，音视频文件等
* 动态资源: 如 `PHP`、`JSP`、`API`

## 多用途互联网邮件扩展（英语：Multipurpose Internet Mail Extensions，缩写：MIME）是一个互联网标准，它扩展了电子邮件标准

内容类型（Content-Type），这个标头区域用于指定资讯的类型。一般以下面的形式呈现。

``` 
Content-Type: [type]/[subtype]; parameter
```

* Text：用于标准化地表示的文字讯息，文字讯息可以是多种字符集和或者多种格式的；
* Multipart：用于连接消息体的多个部分构成一个消息，这些部分可以是不同类型的资料；
* Application：用于传输应用程序资料或者二进制资料；
* Message：用于包装一个E-mail讯息；
* Image：用于传输静态图片资料；
* Audio：用于传输音频或者音声资料；
* Video：用于传输动态影像资料，可以是与音频编辑在一起的视讯资料格式。

subtype用于指定type的详细形式。content-type/subtype配对的集合和与此相关的参数，将随着时间而增长。为了确保这些值在一个有序而且公开的状态下开发，MIME使用Internet Assigned Numbers Authority (IANA)作为中心的注册机制来管理这些值。常用的subtype值如下所示：

* HTML 格式的文本文档由 text/html 类型来标记。
* 普通的 ASCII 文本文档由 text/plain 类型来标记。
* JPEG 格式的图片为 image/jpeg 类型。
* GIF 格式的图片为 image/gif 类型。
* Apple 的 QuickTime 电影为 video/quicktime 类型。
* 微软的 PowerPoint 演示文件为 application/vnd.ms-powerpoint 类型。

## 统一资源定位符
统一资源定位符（英语：Uniform Resource Locator，缩写：URL，或称统一资源定位器、定位地址、URL地址），俗称网页地址，简称网址，是因特网上标准的资源的地址（Address），如同在网络上的门牌。它最初是由蒂姆·伯纳斯-李发明用来作为万维网的地址，现在它已经被万维网联盟编制为因特网标准

统一资源定位符的标准格式如下：
> [协议类型]://[服务器地址]:[端口号]/[资源层级UNIX文件路径][文件名]?[查询]#[片段ID]

