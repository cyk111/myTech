### netty 技术系统学习
#### 知识大纲
- 学习知识依赖
	- Java oop编程
	- java 多线程编程
	- Java IO编程
	- Java 网络编程
	- Java设计模式(观察者、命令模式、责任链模式) 常用数据结构(如 链表)
- java 三种网络编程模型 IO模式
	- BIO  blocking i/o 阻塞io                - 食堂排队打饭
	- NIO non-blocking i/o 非阻塞 i/o  -  点单 等待被叫
	- AIO asyn i/o  异步i/o   - 外卖点单 包厢模式

>  阻塞 非阻塞
>  同步 异步
>  BIO NIO AIO 
>  阻塞 耗资源 效率低
>  
>  netty 暴露更多的可控参数  jdk默认实现水平触发 netty 是边缘触发(默认)和水平触发 可切换
>  netty 实现的垃圾回收更少，性能更好
>  BIO 代码简单 特定场景 连接数 并发度低 BIO性能不输于NIO
>  模式切换
>  EventLoopGroup   底层实现 反射工厂+ 泛型








#### 整体介绍
- 本质: 网络应用程序框架
- 实现: 异步、事件驱动
- 特性：高性能、可维护、快速开发
- 用户：开发服务器和客户端

#### netty 好处
- 支持常用应用层协议
- 解决传输问题：粘包 半包现象
- 支持流量整形
- 完善的断连、idle等异常处理

> 什么是Reactor 及三种版本
> 如何在netty中使用Reactor模式
> 解析netty对Reactor模式支持

