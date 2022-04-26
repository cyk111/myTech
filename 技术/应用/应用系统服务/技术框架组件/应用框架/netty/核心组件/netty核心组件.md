### netty 核心组件

- [[Bootstrap]]
- [[channel]]
- [[channelHandler]]
- [[channelPipeline]]
- [[NioEventLoop & EventLoopGroup]]

#### netty 整体架构
- 核心层
	-  网路通信的抽象与实现，可扩展的事件模型，通用统一API  支持 零拷贝ByteBuf等
- protocol support 协议支持层
	- 主流协议的编解码实现，http SSL protobuf 压缩 大文件传输  websocket 文本 二进制 自定义协议
- transprot service  传输服务层
	- 网路传输能力的定义和实现方法，支持socket http 隧道 虚拟机管道，tcp udp 封装
- ![[Pasted image 20220426101916.png]]

#### netty 逻辑架构
![[Pasted image 20220426103858.png]]
- 网络通信层
	- 职责是执行网络IO操作，支持多种网络协议和IO模型的连接操作，数据读取到内核缓冲区后，触发网络事件，然后分发给事件调度层处理
	- 核心组件 BootStrap、ServerBootStrap、Channel 三个组件
	- BootStrap 负责整个Netty程序的启动、初始化、服务器链接等过程
		- BootStrap负责客户端引导，用户链接远端服务器，只绑定一个EventLoopGroup
		- ServerBootStrap 负责服务器端引导,服务器启动本地端口，会绑定两个EventLoopGroup, 一个Boss,一个Work,Boss接收新的链接，worker处理链接 
	- channel 通道，网络通信的载体，与socket通信，channel提供基本api，用于网络IO操作，如 register、bind、connect、read 、wtite、flush,netty封装为 NIOChannel
		- NioServerSocketChannel 异步TCP服务端
		- NioSocketChannel 异步TCP客户端
		- OioServerSocketChannel 同步TCP服务端
		- OioSocketChannel 同步TCP客户端
		- NioDatagramChannel 异步UDP链接
		- OioDatagramChannel 同步UDP链接、

		- channel状态
			- channelRegistered
			- channelUnRegistered
			- channelActive
			- channelInactive
			- channelRead
			- channelReadComplete
 - 事件调度层
	 - 主要啧啧是通过Reactor线程模型对各类事件进行聚合处理，通过Selector主循环线程，集成多种事件（IO事件、信号事件、定时事件），实际业务有服务编排的相关handler完成
	 - 核心组件 EventLoopGroup EventLoop
		 - EventLoopGroup本质是一个线程池，主要负责IO请求，并分配线程执行处理请求
			 - 一个EventLoopGroup 包含一个或者多个EventLoop,EventLoop用于处理Channel生命周期的所有IO事件，如 accept connect read write
			 - EventLoop 同一时间会与一个线程绑定，每个EventLoop负责处理多个Channel
			 - 每创建一个Channel,EventGroupChannel选择一个EventGroup 与其绑定，可以多次绑定解绑
		 -  **单线程模型**：EventLoopGroup 只包含一个 EventLoop，Boss 和 Worker 使用同一个EventLoopGroup
		 - **多线程模型**：EventLoopGroup 包含多个 EventLoop，Boss 和 Worker 使用同一个EventLoopGroup
		 -  **主从多线程模型**：EventLoopGroup 包含多个 EventLoop，Boss 是主 Reactor，Worker 是从 Reactor，它们分别使用不同的 EventLoopGroup，主 Reactor 负责新的网络连接 Channel 创建，然后把 Channel 注册到从 Reactor
		 - ![[Pasted image 20220426114518.png]]
- 服务编排层
	- 服务编排层的职责是负责组装各类服务， 用以实现网络事件的动态编排和有序传播
	- 核心组件 ChannelPipeline、ChannelHandler、ChannelHandlerContext
		- ChannelPipeline 组装 各种ChannelHandler
		- ChannelPipeline 是线程安全的，因为每一个新的 Channel 都会对应绑定一个新的 ChannelPipeline。一个 ChannelPipeline 关联一个 EventLoop，一个 EventLoop 仅会绑定一个线程
		- 客户端出站（请求数据）、服务端入站（解析数据并执行业务逻辑）、服务端出站（响应结果）
		- ![[Pasted image 20220426115004.png]]
		- **ChannelHandler & ChannelHandlerContext**
			- channelHandlerContext 用于保存handler上下文
		- 组件之间关系
		- ![[Pasted image 20220426115406.png]]

- netty-transport 模块可以说是 Netty 提供数据**处理和传输的核心模块**。该模块提供了很多非常重要的接口，如 Bootstrap、Channel、ChannelHandler、EventLoop、EventLoopGroup、ChannelPipeline 等。
	- Bootstrap 负责客户端或服务端的启动工作，包括创建、初始化 Channel 等；
	- EventLoop 负责向注册的 Channel 发起 I/O 读写操作；
	- ChannelPipeline 负责 ChannelHandler 的有序编排