### 外部API模式

[[网关gateway]]

- 移动端扮演API组合器弊端
	- 多次客户端请求导致用户体验不佳
	- 缺乏封装导致前后端代码耦合严重
	- 服务端对客户端提供的通信机制不一致，导致客户端调用复杂

- web端应用程序的API设计难题
	- 前后端耦合，web端无法有效组合服务的APi

- 第三发提供API
	- 使用API组合效率低下

![[Pasted image 20220623180943.png]]

#### API Gateway
- 外部进入程序的入口点，负责请求路由、api组合、身份验证、流量监控、速率控制
- [[外观模式]] facade 
- api组合负责协议转换
- 实现边缘功能
	- 身份验证
	- 访问授权
	- 速率限制
	- 缓存
	- 指标收集
	- 请求日志
- BFF 后端前置
- 组合查询
- 响应式编程


