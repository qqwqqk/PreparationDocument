# HTTP请求

## 请求报文
HTTP请求报文由三部分组成：请求行，请求头，请求体

![HTTPrequest](HTTPrequest.svg)

* 请求行：
    * <span style="color:#EE0000">请求方法</span>: HTTP/1.1 定义的请求方法有8种：GET、POST、PUT、DELETE、PATCH、HEAD、OPTIONS、TRACE。最常的两种GET和POST，如果是RESTful接口的话一般会用到GET、POST、DELETE、PUT。
    * <span style="color:#EECC00">请求地址</span>: URL:统一资源定位符，是一种自愿位置的抽象唯一识别方法。组成：<协议>：//<主机>：<端口>/<路径> 注：端口和路径有时可以省略（HTTP默认端口号是80）
    * <span style="color:#CCCC00">HTTP协议版本</span>: 协议版本的格式为：HTTP/主版本号.次版本号，常用的有HTTP/1.0和HTTP/1.1
    * PS: 分隔符以空格表示，不可省略

* 请求头：
    * <span style="color:#39C5BB">请求报头</span>: 请求头部为请求报文添加了一些附加信息，由“名/值”对组成，每行一对，名和值之间使用冒号分隔。

* 空行：
    * PS: 请求头与请求体之间的空行不可省略

* 请求体：
    * <span style="color:#00EE00">请求数据</span>: 请求数据也叫主体，可以添加任意的其他数据。 

# OPTION请求
* 获取服务器支持的HTTP请求方法；也是黑客经常使用的方法。
* 用来检查服务器的性能。例如：AJAX进行跨域请求时的预检，需要向另外一个域名的资源发送一个HTTP OPTIONS请求头，用以判断实际发送的请求是否安全。