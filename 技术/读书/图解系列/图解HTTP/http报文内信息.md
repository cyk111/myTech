#### http 报文

用户HTTP协议交互的信息称为HTTP报文

- 请前端  请求报文
	- 请求行
		-  请求的方法，请求的URI和HTTP版本
	- 请求首部字段
	- 通用首部字段
	- 实体首部字段
	- 其他
	- **请求和响应的各种条件和属性的各类首部**
- 响应段  响应报文
		- 状态行
			- 响应结果的状态码、原因短语、http版本
	- 响应首部字段
	- 通用首部字段
	- 实体首部字段
	- 其他

#### 编码提升传输速率
- 报文主体和实体主体
	- 报文和实体
- 压缩传输的内容编码
	- gzip
	- compress
	- deflate(zlib)
	- identity(不编码)
- 分割发送的分块传输编码

#### 发送多种数据的多部分对象集合
- multipart/form-data  在 Web 表单文件上传时使用
- multipart/byteranges 部分范围内容请求

#### 内容协商返回最合适的内容
- Accept 
- Accept-Charset
- Accept-Encoding 
- Accept-Language 
- Content-Language
- 服务器驱动协商
- 客户端驱动协商
- 透明协商