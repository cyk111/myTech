
- web  service 是一个软件系统，用于支持网络间不同机器的互动操作

- SOAP 
	- 基于xml的可扩展消息封装格式，同时绑定网络传输协议，如http  smtp xmpp
- WSDL 
	- 一个xml 格式文档，用于描述服务端口访问方式，和试用协议的细节
- UDDI
	- 一个用来发布和搜索web服务的协议，应用程序可在此协议运行时找到WEB服务器
- 扩展协议
	- WS-security WS安全 定义如何在soap中使用xml加密 ,来保护消息传输，类似 https
	- WS-Reliability  WS信赖性， 用来提供可信赖的web服务消息
	- WS-Addressing 寻址，定义SOAP消息内描述发送和接送方地址的方式
	- WS-Transcation 定义事务处理方式



![[Pasted image 20220517225036.png]]




- 使用web服务的方式
	- 远程过程调用 RPC
		- 提供分布式函数或方法接口供用户调用
	- 服务导向架构 SOA
		- 有消息驱动，而不是动作，面向消息的服务
		- 与RPC 区别，SOA更关注如何去连接服务，而不是去特定某个实现细节，WSDL定义网络服务的必要内容
	- 表述性状态转移 REST
		- 以资源的形式提供服务，可以通过WSDL来描述SOAP消息内容，通过HTTP限定动作接口；或者完全在SOAP中对动作进行抽象


-  [Http方式发送Soap报文调用WebService](https://www.1024sou.com/article/198556.html)
-  [cxf动态构建webservice](https://sillybilly-share.top/cxf%E5%8A%A8%E6%80%81%E6%9E%84%E5%BB%BAwebservice.html)]