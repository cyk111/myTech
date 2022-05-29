####  http返回结构状态码

#### 状态码
- 1XX 信息性状态码，接收的请求正在处理
- 2XX Success  成功状态码，请求正常处理完毕
	- 200 ok
	- 204 
	- 206
- 3XX Redirection 重定向状态码，需要进行附加操作以完成请求
	- 301 永久重定向
	- 302 临时重定向
	- 303
	- 304 not Modified 
	- 307
- 4XX Client Error 客户端错误状态码 服务器无法处理请求
	- 400 bad Request
	- 401 Unauthorized
	- 403 Forbidden 
	- 404 Not Found``
- 5XX Server  Error 服务器错误状态码，服务器处理请求出错
	- 500 Internal Server Error
	- 503 Servcie Unavailable
