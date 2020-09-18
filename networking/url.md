> 订阅 [TheTutorials/Java](https://github.com/TheTutorials/Java) 学习更多 Java 相关的知识

# `URL` 教程

![URL](../images/url.jpg)

## 什么是 `URL`
Wikipedia: https://zh.wikipedia.org/wiki/%E7%BB%9F%E4%B8%80%E8%B5%84%E6%BA%90%E5%AE%9A%E4%BD%8D%E7%AC%A6
> 统一资源定位符（英语：Uniform Resource Locator，缩写：URL；或称统一资源定位器、定位地址、URL地址，俗称网页地址或简称网址）是因特网上标准的资源的地址（Address），如同在网络上的门牌。它最初是由蒂姆·伯纳斯-李发明用来作为万维网的地址，现在它已经被万维网联盟编制为因特网标准RFC 1738。

超文本传输协议的统一资源定位符将从因特网获取信息的五个基本元素包括在一个简单的地址中：

1. 传送协议。
2. 层级URL标记符号(为[`//`],固定不变)
3. 访问资源需要的凭证信息（可省略）
4. 服务器。（通常为域名，有时为IP地址）
5. 端口号。（以数字方式表示，若为默认值可省略）
6. 路径。（以 `/` 字符区别路径中的每一个目录名称）
7. 查询。（GET模式的窗体参数，以 `?` 字符为起点，每个参数以 `&` 隔开，再以 `=` 分开参数名称与资料，通常以UTF8的URL编码，避开字符冲突的问题）
8. 片段。以 `#` 字符为起点

以https://zh.wikipedia.org:443/w/index.php?title=Special:随机页面为例, 其中：

1. https，是协议；
2. zh.wikipedia.org，是服务器；
3. 443，是服务器上的网络端口号；
4. /w/index.php，是路径；
5. ?title=Special:随机页面，是询问。

大多数网页浏览器不要求用户输入网页中“https://”的部分，因为绝大多数网页内容是超文本传输协议文件。同样，“80”是超文本传输协议文件的常用端口号，因此一般也不必写明。一般来说用户只要键入统一资源定位符的一部分（zh.wikipedia.org/w/index.php?title=Special:随机页面）就可以了。


## `URL` 的使用

* 常用构造函数
    ``` java
    URL(String protocol, String host, int port, String file)
    URL(String spec)
    ```
* 常用方法
    ``` java
    URL url = new URL("https://zh.wikipedia.org:443/w/index.php?title=Special:随机页面为例");

    assert url.getProtocol().equals("https");
    assert url.getAuthority().equals("zh.wikipedia.org:443");
    assert url.getHost().equals("zh.wikipedia.org");
    assert url.getPort() == 443 && url.getDefaultPort() == 443;
    assert url.getPath().equals("/w/index.php");
    assert url.getFile().equals("/w/index.php?title=Special:随机页面为例");
    assert url.getQuery().equals("title=Special:随机页面为例");
    ```
