### channelPipeline

#### ChannelPipeline概述
##### 定义
- pipeline 字面意思是管道、流水线，netty中它是核心处理链，用于实现网络事件的动态编排和有序传播

##### 内部结构
- netty的核心编排组件，负责调度各种类型的channelHandler，实际数据加工处理操作则是ChannnelHandler完成
- 可以看做 ChannelHandler的容器载体，有channelHandler实例组成，内部通过双向链表链接在一起
- 每个channel会绑定一个ChannelPipeline
- channelPipeline 对多个 ChannelHandlerContext
- 多个channelHandlerContext组成双线链表
- channelHandlerContext 与 channelHandler 一对一
- channelHanderContext 用于保存channelcontext上下文，管理生命周期如，connect、bind、read、flush、write、flush等

![[Pasted image 20220426151613.png]]

- 根据网络数据流向，channelPipeline分为 出站 channelOutboundhandler 入站 channelInboundHandler 两种处理器
- 客户端到服务器端 称为出站  Encoder
- 服务器端到客户端 成为入站  Decoder 
![[Pasted image 20220426152624.png]]


#### 接口设计
- channelHandler是围绕IO事件的生命周期所设计的，如建立链接，读数据，写数据，链接销毁
- channelInboundHandler 入站事件方法
	- channelRegister
	- channelUnRegister
	- ChannelActive
	- ChanelInactive
	- channelRead
	- channelReadComplete
	- userEventTriggered
	- channelWritabilityChanged
	
- channelOutboundHandler 出站
	- bind
	- close
	- connect
	- deregister
	- disconnect
	- flush
	- read
	- write
	
#### 事件传播机制
- inbound 事件和 Outbound 事件的传播方向是不一样的。
	- Inbound 事件的传播方向为 Head -> Tail
	- Outbound 事件传播方向是 Tail -> Head
#### 异常传播机制
- 对异常统一拦截，根据业务实际场景完成异常处理机制
- 在ChannelPipeline 自定义处理器的末端添加统一的异常处理器
``` Java
public class ExceptionHandler extends ChannelDuplexHandler {

    @Override
    public void exceptionCaught(ChannelHandlerContext ctx, Throwable cause) {
        if (cause instanceof RuntimeException) {
            System.out.println("Handle Business Exception Success.");
        }
    }
}
```