### netty 实现自定义通信协议

#### 通信协议的设计
- 通用的协议
	- http、https、json-rpc、FTP、IMAP、Protobuf
	- 原则：极致性能、扩展性、安全性
- 通信协议的基本要素
	- 魔数，防止任何人随便向服务器上的端口发送数据
	- 协议版本号，不同版本不同解析方式
	- 序列化算法，json、hessian、java自带序列化
	- 报文类型
	- 长度域字段，请求数据的长度
	- 请求字段，数据序列化后的二进制流
	- 状态，标识请求是否正常
	- 保留字段
#### netty自定义通信协议
- 常用编码器类型
	- MessageToByteEncoder 对象编码成字节流
	- MessageToMessageEncoder 一种类型编码成另外一个类型
- 常用解码器类型
	- ByteToMessageDecoder/RepalyingDecoder 字节流解码为消息对象
	- MessageToMessageDecoder 一种消息类型解码为另外一种消息类型
- 编解码器
	- 一次编解码器，用于解决TCP拆包粘包问题，按照协议解析得到字节数
		- MessageToByteEncoder/ByteToMessageDecoder
	- 二次编解码器 字节流数据转变对象模型
		- MessageToMessageEncoder/MessageToMessageDecoder
- 
