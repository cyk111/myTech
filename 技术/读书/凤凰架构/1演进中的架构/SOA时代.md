### SOA 时代


- SOA 架构 Service-Oriented Architecture 面向服务的架构



 - 烟筒式架构 Information Silo Architecture 
	 - 信息孤岛，完全不与其他其他系统交互，不与其他系统协调工作，真实环境中不可行，一个公司系统 人员、组织、权限需要公用
 - 微内核架构 microkernel Architecture 
	 - 也称作插件式架构 plug-in Architecture ,将公共的资源 数据 服务集中到一块，让其他业务系统调用，也就是微核心
	 - 适合二次开发，局限在于各个插件模块之间互补认知，不可预知系统安装的模块
	
![[Pasted image 20220510162129.png]]
	
 - 事件驱动架构 Event-Driven Architecture
	 - 为了让子系统互相通信，建立事件队列管道，系统外部的消息以事件的形式发送至管道中，子系统对事件感兴趣，读取事件进行处理，当然也可以发送事件
	 ![[Pasted image 20220510162554.png]]


- SOAP 协议的诞生

- SOA 架构时代
	- 服务的封装性
	- 自治
	- 松耦合
	- 注册
	- 发现
	- 治理
	- 隔离
	- 编排
	- 可重用
	- 可组合
	- 无状态
- SOAP 协议族 WSDL UDDI WS-**  来完成服务端 发现、发布、治理
	- ESB (Enterprise Service Bus) 企业服务总线  消息管道实现各个子系统的通信交互
	- 各个子系统技能实现送耦合
	- 又可以进一步实现业务流程编排 Bussiness process Management BMP 
	- 使用服务数据对象SDO  Service Data Object 表示数据
	- SCA Sercvice Compent Architecture 定义服务封装的形式和服务运行的容器
 