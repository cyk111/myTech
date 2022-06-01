### HTTP知识

- [[远程服务调用]]

- **超文本传输协议**（英语：**H**yper**T**ext **T**ransfer **P**rotocol，缩写：**HTTP**）是一种用于分布式、协作式和[超媒体](https://zh.wikipedia.org/wiki/%E8%B6%85%E5%AA%92%E9%AB%94 "超媒体")信息系统的[应用层](https://zh.wikipedia.org/wiki/%E5%BA%94%E7%94%A8%E5%B1%82 "应用层")[协议]，HTTP是[万维网](https://zh.wikipedia.org/wiki/%E5%85%A8%E7%90%83%E8%B3%87%E8%A8%8A%E7%B6%B2 "万维网")的数据通信的基础。
	- 应用层协议 非传输协议
	- rest 是http的抽象，或者说http 是restful的实现 ，rest 与 http 类似于 接口与实现类

- http 是客户端能与服务器端之间请求和应答的标准，通常使用TCP 协议


- 请求方法
	- get 
	- head
	- post
	- put
	- delete
	- tracke
	- options
	- connect
- 状态码
	-   [1xx消息](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#1xx%E6%B6%88%E6%81%AF "HTTP状态码")——请求已被服务器接收，继续处理
	-   [2xx成功](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#2xx%E6%88%90%E5%8A%9F "HTTP状态码")——请求已成功被服务器接收、理解、并接受
	-   [3xx重定向](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#3xx%E9%87%8D%E5%AE%9A%E5%90%91 "HTTP状态码")——需要后续操作才能完成这一请求
	-   [4xx请求错误](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#4xx%E8%AF%B7%E6%B1%82%E9%94%99%E8%AF%AF "HTTP状态码")——请求含有词法错误或者无法被执行
	-   [5xx服务器错误](https://zh.wikipedia.org/wiki/HTTP%E7%8A%B6%E6%80%81%E7%A0%81#5xx%E6%9C%8D%E5%8A%A1%E5%99%A8%E9%94%99%E8%AF%AF "HTTP状态码")——服务器在处理某个正确请求时发生错误