### Bootstrap

 > BootStrap 引导器，netty客户端和服务端的程序入口
#### 服务端启动步骤
##### 配置线程池
- 单线程模式
```java
EventLoopGroup group = new NioEventLoopGroup(1);
ServerBootstrap b = new ServerBootstrap();
b.group(group);
```
![[Pasted image 20220426141912.png]]


- 多线程模式,默认会启动  2倍cpu的线程数
```java
EventLoopGroup group = new NioEventLoopGroup();
ServerBootstrap b = new ServerBootstrap();
b.group(group);
```
![[Pasted image 20220426141936.png]]


- 主从多线程模式
```java
EventLoopGroup bossGroup = new NioEventLoopGroup();
EventLoopGroup workGroup = new NioEventLoopGroup();
ServerBootstrap b = new ServerBootstrap();
b.group(bossGroup,workGroup);
```
![[Pasted image 20220426142014.png]]

- Reactor线程模型运行机制的四个步骤
	- 连接注册： Channel建立后，注册到Reactor线程中的Selector选择器
	- 事件轮循：轮询Selector选择器中已注册的所有channel的IO事件
	- 事件分发：为准备就绪的IO事件分配响应的处理线程
	- 任务处理：Reactor 线程还负责任务队列中的非 I/O 任务，每个 Worker 线程从各自维护的任务队列中取出任务异步执行


##### Channel初始化
- 设置Channel
	- - 可以切换Channel实现类，如OioServerSocketChannel 、EpollServerSocketChannel
```
 b.channel(NioServerSocketChannel.class);
```

- 注册Channel 
	- ServerBootstrap 的 childHandler() 方法需要注册一个 ChannelHandler。**ChannelInitializer**是实现了 ChannelHandler**接口的匿名类**，通过实例化 ChannelInitializer 作为 ServerBootstrap 的参数
``` java
// HTTP 编解码
.addLast("codec", new HttpServerCodec())
// HttpContent 压缩
.addLast("compressor", new HttpContentCompressor())      
// HTTP 消息聚合
.addLast("aggregator", new HttpObjectAggregator(65536))   
// 自定义handler
.addLast("handler", new HttpServerHandler());  
```

- 设置channel参数
	- ServerBootStrap 设置channel属性有 option和childOption两种方法，option主要负责Boss线程组，childOption负责worker线程组
	- SO_KEEPALIVE 设置为true,tcp主动探测链接状态即连接保活
	- SO_BLCKLOG 已经完成三次握手请求队列最大长度
	- TCP_NODELAY 默认true，表示立即发送数据
	- SO_SNDBUF tcp数据发送缓冲区大小
	- SO_RCVBUF tcp数据接收缓冲区大小
	- SO_LINGER 设置延迟关闭的时间，等待缓存区数据发送完成
	- CONNECT_TIMEOUT_MILLS  建立超时链接时间

##### 端口绑定
```
ChannelFuture f = b.bind().sync();
```

#### 客户端

```Java
public class HttpClient {

    public void connect(String host, int port) throws Exception {

        EventLoopGroup group = new NioEventLoopGroup();

        try {

            Bootstrap b = new Bootstrap();

            b.group(group);

            b.channel(NioSocketChannel.class);

            b.option(ChannelOption.SO_KEEPALIVE, true);

            b.handler(new ChannelInitializer<SocketChannel>() {

                @Override

                public void initChannel(SocketChannel ch) {

                    ch.pipeline().addLast(new HttpResponseDecoder());

                    ch.pipeline().addLast(new HttpRequestEncoder());

                    ch.pipeline().addLast(new HttpClientHandler());

                }

            });

            ChannelFuture f = b.connect(host, port).sync();

            URI uri = new URI("http://127.0.0.1:8088");

            String content = "hello world";

            DefaultFullHttpRequest request = new DefaultFullHttpRequest(HttpVersion.HTTP_1_1, HttpMethod.GET,

                    uri.toASCIIString(), Unpooled.wrappedBuffer(content.getBytes(StandardCharsets.UTF_8)));

            request.headers().set(HttpHeaderNames.HOST, host);

            request.headers().set(HttpHeaderNames.CONNECTION, HttpHeaderValues.KEEP_ALIVE);

            request.headers().set(HttpHeaderNames.CONTENT_LENGTH, request.content().readableBytes());

            f.channel().write(request);

            f.channel().flush();

            f.channel().closeFuture().sync();

        } finally {

            group.shutdownGracefully();

        }

    }

    public static void main(String[] args) throws Exception {

        HttpClient client = new HttpClient();

        client.connect("127.0.0.1", 8088);

    }
}
```


```java
public class HttpClientHandler extends ChannelInboundHandlerAdapter {

    @Override

    public void channelRead(ChannelHandlerContext ctx, Object msg) {

        if (msg instanceof HttpContent) {

            HttpContent content = (HttpContent) msg;

            ByteBuf buf = content.content();

            System.out.println(buf.toString(io.netty.util.CharsetUtil.UTF_8));

            buf.release();

        }

    }

}
```