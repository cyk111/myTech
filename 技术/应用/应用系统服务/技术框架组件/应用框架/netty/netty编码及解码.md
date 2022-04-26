### netty编码及解码

#### netty支持常用的解码器
- 固定长度解码器 FixedLengthFrameDecoder
- 特殊分隔符解码器 DelimiterBasedFrameDecoder
- 长度域解码器 LengthFieldBasedFrameDecoder

#### writhAndFlush
- 客户端向服务端发送请求，或者服务器端响应客户端请求都属于出站行为，channeloutboundhandler,调用writeAndFlush 数据一定会在Pipeline中进行传播

-   writeAndFlush 属于出站操作，它是从 Pipeline 的 Tail 节点开始进行事件传播，一直向前传播到 Head 节点。不管在 write 还是 flush 过程，Head 节点都中扮演着重要的角色。
-   write 方法并没有将数据写入 Socket 缓冲区，只是将数据写入到 ChannelOutboundBuffer 缓存中，ChannelOutboundBuffer 缓存内部是由单向链表实现的。
-   flush 方法才最终将数据写入到 Socket 缓冲区