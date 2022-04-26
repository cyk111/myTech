### netty 技术系统学习


####  学习知识依赖
- Java oop编程
- java 多线程编程
- Java IO编程
- Java 网络编程
- Java设计模式(观察者、命令模式、责任链模式) 
- 常用数据结构(如 链表)
#### 整体介绍
- 本质: 网络应用程序框架
- 实现: 异步、事件驱动
- 特性：高性能、可维护、快速开发，低延时
- 用户：开发服务器和客户端

#### netty 好处
- 支持常用应用层协议
- 解决传输问题：粘包 半包现象
- 支持流量整形
- 完善的断连、idle等异常处理

#### netty 书籍
- 《netty in Action》
- 《netty 权威指南》

#### 选择netty原因
- 高效的远程NIO网络框架，减少网络应用的开发过程
- 易用性 jdk NIO编程需要了解一些复杂概念，如channels selectors sockert buffer，封装了开箱即用的功能，如行解码器 长度域解码器
- 稳定性，解决select 空转导致cpu消耗100% TCP断线重连 keep-alive 检测重连等问题
- 可扩展性，可以定制线程模型 boss worker，可扩展的事件驱动模型,框架层和业务层分离
- 对象池复用技术，复用对象，避免频繁创建销毁队形
- 零拷贝技术
- 更多的通信协议支持，tomcat主要解决http协议层的传输，netty不仅支持http,还支持 ssh tls/ssl  tcp等 

#### netty关注核心点
- IO模型,线程模型和事件处理机制
- 易用API接口
- 对数据协议，序列化的支持


#### IO调用及Linux 5种主要IO模式
- IO 请求分两个阶段
	- 1 IO调用阶段，用户进程向内核系统发起调用
	- 2 IO执行阶段，内核等待IO请求处理完成返回，数据就绪，IO设备获取数据到内核缓冲区，数据从内核缓冲区拷贝到用户态缓冲区

![[Pasted image 20220426065635.png]]
- 5种IO模式
	- 同步阻塞IO (BIO)
		- [[BIO相关]]
		- blocking i/o 阻塞io 
		- 类似食堂排队打饭
	- 同步非阻塞IO (NIO)
		- [[NIO相关]] 
		- non-blocking i/o 非阻塞 i/o   
		-  点单 等待被叫
	- IO多路复用
		- [[多路复用相关]]
	- 信号驱动IO
		- [[信号驱动IO]]
		- 半异步
	- 异步IO
		- asyn i/o  异步i/o
		- [[异步IO]]  
		-  外卖点单 包厢模式

####  Netty的IO 模型
- 基于NIO实现，底层依赖JDK NIO的多路复用器 Selector,一个selector 同时可以轮循多个channel,采用epoll模式，一个线程负责Selector的轮循，就可以接入成千上万的客户端
- 数据处于就绪状态后，需要事件分发器 Event Dispather,负责将读写事件分发给对应的事件处理器 Event Handler，事件分发器两种模式 Reactor 采用同步IO Proactor 采用异步IO
- Reactor 实现简单，适合耗时短的场景，对于耗时长的IO 容易祖册
- Proactor 性能更高，但是逻辑复杂，主流事件驱动模型依赖 select或epoll 实现
![[Pasted image 20220426100025.png]]

#### netty 应用场景
-   服务治理：Apache Dubbo、gRPC。
-   大数据：Hbase、Spark、Flink、Storm。
-   搜索引擎：Elasticsearch。
-   消息队列：RocketMQ、ActiveMQ。