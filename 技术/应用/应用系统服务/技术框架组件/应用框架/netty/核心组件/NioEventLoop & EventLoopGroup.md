### NioEventLoop & EventLoopGroup

> EventLoop 是一种事件等待和处理程序的模型，可以解决多线程资源消耗高的问题
> 
> 每当事件发生时，应用程序都会将产生的事件放入事件队列当中，然后 EventLoop 会轮询从队列中取出事件执行或者将事件分发给相应的事件监听者执行。事件执行的方式通常分为
> **立即执行、延后执行、定期执行**几种。

#### 主从线程模型
- ![[Pasted image 20220426142014.png]]

- 主从多线程模型有多个Reactor线程组成，每个Reactor线程都有独立的Selector对象，mainReactor负责处理客户端Accept事件，连接成功后新创建的对象注册到subReactor，在有线程池中的IO线程与其链接绑定。
- Reactor 线程模型的步骤，连接注册，事件轮询，事件分发，任务处理![[Pasted image 20220426144652.png]]

#### EventLoop 概念
- EventLoop是什么
	- 是一种事件等待和处理的程序模式，可以处理多线程资源消耗高的问题
	- 事件执行的方式，立即执行、延后执行、定期执行
![[Pasted image 20220426144918.png]]

- 如何实现EventLoop
	- EventLoop可以理解为Reactor线程模型事件处理引擎，
	- 每个 EventLoop 线程都维护一个 Selector 选择器和任务队列 taskQueue。
	- 它主要负责处理 I/O 事件、普通任务和定时任务
- NioEventLoop处理流程包含
	- 事件轮循select
	- 事件处理 processSelectedKeys
	- 任务处理 runAllTasks
- 事件处理机制
![[Pasted image 20220426145813.png]]
- 任务处理机制
	- 普通任务
	- 定时任务
	- 尾部队列

#### EventLoop 最佳实践
- 网络连接建立中三次握手，安全认证的过程会消耗不少时间，使用Boss线程负责处理连接，worker 负责处理
- Reactor线程模式适合耗时短的任务场景，对线程过长的channelHandler可以考虑维护一个业务线程池，将编码后的数据封装成Task进行异步处理，避免channelHandler阻塞而造成EventLoop不可用
- 如果业务逻辑执行端，则直接在handler中执行，避免过渡设计造成架构的复杂性
- channenHandler注意分层之间的界限

-   MainReactor 线程：处理客户端请求接入。
-   SubReactor 线程：数据读取、I/O 事件的分发与执行。
-   任务处理线程：用于执行普通任务或者定时任务，如空闲连接检测、心跳上报等。