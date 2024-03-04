# CORS

> **跨源资源共享**（[CORS](https://developer.mozilla.org/zh-CN/docs/Glossary/CORS)，或通俗地译为跨域资源共享）是一种基于 [HTTP](https://developer.mozilla.org/zh-CN/docs/Glossary/HTTP) 头的机制，该机制通过允许服务器标示除了它自己以外的其他[源](https://developer.mozilla.org/zh-CN/docs/Glossary/Origin)（域、协议或端口），使得浏览器允许这些源访问加载自己的资源。跨源资源共享还通过一种机制来检查服务器是否会允许要发送的真实请求，该机制通过浏览器发起一个到服务器托管的跨源资源的“预检”请求。在预检中，浏览器发送的头中标示有 HTTP 方法和真实请求中会用到的头。

人话：为了安全考虑，不允许跨源发请求，需要先派大使沟通。

#### 触发条件

我们先说基本的条件，请求和响应需要被允许进行。请求头带上**Origin**表示自己的来源，响应头带上**Access-Control-Allow-Origin**表示允许来的源，两者相符，则被允许进行通信。

然后判断是否符合同源策略，同源就是域名、协议、端口一致，直接进行通信，否则需要继续判断。

最后判断是否为简单跨来源请求，快速来说方法只采用`GET`、`POST`、`HEAD`，携带头只有`Accept`、`Accept-Language`、`Content-Language` 或 `Content-Type`（值只能是 `application/x-www-form-urlencoded`、`multipart/form-data` 或 `text/plain`）， 符合全部条件，则为简单跨来源请求，允许直接通信，若不符合，则触发一般跨来源请求。

#### 流程

首先派大使进行沟通，这里大使是指预检请求。预检请求是一个OPTIONS方法，携带不符合简单跨来源请求的头（比如'Content-TYPE': application/json），用来询问服务器是否允许这样的头？若允许则进行后续正常通信。

流程图如下: ![图片.png](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/dc9d62964c3b41678fd4ccc99cb86728\~tplv-k3u1fbpfcp-jj-mark:0:0:0:0:q75.image#?w=1024\&h=1076\&s=138399\&e=png\&b=fefefe)

#### 更多阅读

推荐阅读:

* [MDN资料](https://developer.mozilla.org/zh-CN/docs/Web/HTTP/CORS)
* [深入了解CORS](https://www.shubo.io/what-is-cors/)
