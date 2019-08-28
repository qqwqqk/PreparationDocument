# HTTP请求

## 请求报文
HTTP请求报文由三部分组成：请求行，请求头，请求体

    <span color=#EE0000>POST</span>    <span color=#EECC00>/chapter17/user.html</span>    <span color=#CCCC00>HTTP/1.1</span>
    <span color=#39C5BB>Accept: image/jpeg, application/x-ms-application, ..., */*</span>
    <span color=#39C5BB>Referer: http://localhost:8088/chapter17/user/register.html?code=100&amp;time=123</span>
    <span color=#39C5BB>Accept-Language: zh-CN</span>
    <span color=#39C5BB>User-Agent: Mozilla/4.0 (compatible; MSIE 8.0; Windows NT 6.1; )</span>
    <span color=#39C5BB>Content-Type: application/x-www-form-urlencoded</span>
    <span color=#39C5BB>Host:localhost:8088</span>
    <span color=#39C5BB>Content-Length: 112</span>
    <span color=#39C5BB>Connection: Keep-Alive</span>
    <span color=#39C5BB>Cache-Control: no-cache</span>
    <span color=#39C5BB></span>
    <span color=#39C5BB>Cookie: JSESSIONID=24DF2688E37EE4F66D9669D2542AC17B</span>
    <span color=#00EE00>name=tom&amp;password=1234&amp;realName=tomson</span>
    
* 请求行：
    * <span color=#EE0000>请求方法</span>: HTTP/1.1 定义的请求方法有8种：GET、POST、PUT、DELETE、PATCH、HEAD、OPTIONS、TRACE。最常的两种GET和POST，如果是RESTful接口的话一般会用到GET、POST、DELETE、PUT。
    * <span color=#EECC00>请求地址</span>: URL:统一资源定位符，是一种自愿位置的抽象唯一识别方法。组成：<协议>：//<主机>：<端口>/<路径> 注：端口和路径有时可以省略（HTTP默认端口号是80）
    * <span color=#CCCC00>HTTP协议版本</span>: 协议版本的格式为：HTTP/主版本号.次版本号，常用的有HTTP/1.0和HTTP/1.1
    * PS: 分隔符以空格表示，不可省略

* 请求头：
    * <span color=#39C5BB>请求报头</span>: 请求头部为请求报文添加了一些附加信息，由“名/值”对组成，每行一对，名和值之间使用冒号分隔。

* 空行：
    * PS: 请求头与请求体之间的空行不可省略

* 请求体：
    * <span color=#00EE00>请求数据</span>: 请求数据也叫主体，可以添加任意的其他数据。 