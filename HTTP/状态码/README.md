# HTTP状态码

1. [常见状态码](#常见状态码)
2. [1XX 消息](#1XX-消息)
3. [2XX 成功](#2XX-成功)
4. [3XX 重定向](#3XX-重定向)
5. [4XX 请求错误](#4XX-请求错误)
6. [5XX 服务器错误](#5XX-服务器错误)

## 常见状态码
### 200 OK 
一切正常
### 301 Moved Permanently 
被请求资源已永久移动到新位置，后续相同地址的访问应该使用本响应返回的若干个URI之一
### 400 Bad Request 
语义有误当前请求无法被服务器理解，或请求参数有误
### 404 Not Found 
请求失败，请求所希望得到的资源未被在服务器上发现
### 409 Conflict 
由于和被请求的资源的当前状态之间存在冲突，请求无法完成
### 410 Gone 
被请求的资源在服务器上已经不再可用，且没有任何已知的转发地址
### 500 Internal Server Error 
服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理


## 1XX 消息
### 100 Continue 
客户端应当继续发送请求
### 101 Switching Protocols 
服务器已经理解了客户端的请求并通知客户端采用不同的协议来完成这个请求
### 102 Processing 
由WebDAV RFC 2518扩展的状态码，代表处理将被继续执行

## 2XX 成功
### 200 OK 
请求成功，响应头或数据体随此响应返回
### 201 Created 
请求被实现，新资源建立其URI已经随Location头信息返回
### 202 Accepted 
服务器已接受请求，但尚未处理
### 203 Non-Authoritative Information 
请求成功处理，返回元信息不是在原始服务器上有效的确定集合
### 204 No Content 
请求成功处理，不返回任何实体内容而返回更新了的元信息
### 205 Reset Content 
请求成功处理，且没有返回任何内容
### 206 Partial Content 
部分GET请求成功处理，常用于断点续传
### 207 Multi-Status 
由WebDAV(RFC 2518)扩展的状态码，代表之后的消息体将是一个XML消息

## 3XX 重定向
### 300 Multiple Choices 
被请求资源有多个可选回馈信息，每个都有特定的地址和浏览器驱动的商议信息
### 301 Moved Permanently 
被请求资源已永久移动到新位置，后续相同地址的访问应该使用本响应返回的若干个URI之一
### 302 Move Temporarily 
请求的资源临时从不同的URI响应请求
### 303 See Other 
对应当前请求的响应可以在另一个URL上被找到，而且客户端应当采用GET的方式访问那个资源
### 304 Not Modified 
客户端发送一个带条件的GET请求且该请求已被允许，而文档的内容并没有改变
### 305 Use Proxy 
被请求的资源必须通过指定的代理才能被访问
### 306 Switch Proxy 
在最新版的规范中，306状态码已经不再被使用
### 307 Temporary Redirect 
请求的资源临时从不同的URI响应请求

## 4XX 请求错误
### 400 Bad Request 
语义有误当前请求无法被服务器理解，或请求参数有误
### 401 Unauthorized 
当前请求需要用户验证
### 402 Payment Required 
该状态码是为了将来可能的需求而预留的
### 403 Forbidden 
服务器已经理解请求，但是拒绝执行它
### 404 Not Found 
请求失败，请求所希望得到的资源未被在服务器上发现
### 405 Method Not Allowed 
请求行中指定的请求方法不能被用于请求相应的资源
### 406 Not Acceptable 
请求的资源的内容特性无法满足请求头中的条件，因而无法生成响应实体
### 407 Proxy Authentication Required 
与401响应类似，区别为客户端必须在代理服务器上进行身份验证
### 408 Request Timeout 
请求超时
### 409 Conflict 
由于和被请求的资源的当前状态之间存在冲突，请求无法完成
### 410 Gone 
被请求的资源在服务器上已经不再可用，且没有任何已知的转发地址
### 411 Length Required 
服务器拒绝在没有定义Content-Length头的情况下接受请求
### 412 Precondition Failed 
请求的头字段中的先决条件验证未通过
### 413 Request Entity Too Large 
请求实体数据过大，服务器拒绝处理
### 414 Request-URI Too Long 
请求URI长度过长，服务器拒绝对处理
### 415 Unsupported Media Type 
请求实体格式不被支持，服务器拒绝处理
### 416 Requested Range Not Satisfiable 
请求指定的首字节位置超过了当前资源的长度
### 417 Expectation Failed 
在请求头Expect中指定的预期内容无法被服务器满足
### 418 I'm a teapot 
我是一个茶壶
### 421 Too Many Connections 
从当前客户端所在的IP地址到服务器的连接数超过了服务器许可的最大范围
### 422 Unprocessable Entity 
请求格式正确，但是由于含有语义错误，无法响应
### 423 Locked 
当前资源被锁定
### 424 Failed Dependency 
由于之前的某个请求发生的错误，导致当前请求失败
### 425 Too Early 
该请求可能会被“重放”，从而造成潜在的重放攻击
### 426 Upgrade Required 
客户端应当切换到TLS/1.0
### 449 Retry With 
由微软扩展，代表请求应当在执行完适当的操作后进行重试
### 451 Unavailable For Legal Reasons 
该请求因法律原因不可用

## 5XX 服务器错误
### 500 Internal Server Error 
服务器遇到了一个未曾预料的状况，导致了它无法完成对请求的处理
### 501 Not Implemented 
服务器不支持当前请求所需要的某个功能
### 502 Bad Gateway 
作为网关或者代理工作的服务器尝试执行请求时，从上游服务器接收到无效的响应
### 503 Service Unavailable 
由于临时的服务器维护或者过载，服务器当前无法处理请求
### 504 Gateway Timeout 
网关或者代理工作的服务器尝试执行请求超时
### 505 HTTP Version Not Supported 
服务器不支持，或者拒绝支持在请求中使用的 HTTP 版本
### 506 Variant Also Negotiates 
由RFC2295扩展，代表服务器存在内部配置错误
### 507 Insufficient Storage 
服务器无法存储完成请求所必须的内容
### 509 Bandwidth Limit Exceeded 
服务器达到带宽限制，这不是一个官方的状态码但是仍被广泛使用
### 510 Not Extended 
获取资源所需要的策略并没有被满足
### 600 Unparseable Response Headers 
源站没有返回响应头部，只返回实体内容
