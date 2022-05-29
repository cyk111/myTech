### web及网络访问基础

#### 背景
- 借助多文档相关关联形成超文本，连接成可以互相订阅的WWW  world wide web 万维网
	- SGML standard generalized markup language ---> HTML
	- 文档传输的协议 HTTP (HyperText Transfer Protocol )
	- 指定文档所在地址 URL ( Uniform Resource Locator 统一资源定位符)



#### 网络基础TCP/IP

- TCP/IP协议族
	-  Http DNS  FTP TCP UDP IP  SMTP FDDI PPPoE IP 
- 分层管理
	- 应用层：决定了向用户提供应用服务时通信的活动
		- FTP、DNS、HTTP 
	- 传输层: 提供处于网络连接中的两台计算机之间的数据传输
		- TCP 传输控制协议 UDP 用户数据报协议
	- 网络层：用户处理网络上流动的数据包，数据包是网络中最小的数据单位,规定通过怎样的路径到达对方计算机，选择通信线路
		- IP 
	- 链路层：用来处理连接网路的硬件部分，包括操作系统 NIC，硬件驱动


![[Pasted image 20220529163222.png]]


- 发送端在层与层之间传输数据时，都要打上一个该层所属的头部信息，封装（encapsulate）
![[Pasted image 20220529163238.png]]


#### 负责传输的IP协议 ，
- 作用是把各种数据包传送个对方， 需要满足两个条件 IP地址，MAC地址(media Access control Address)
- ARP 协议(address resolution protocol) 地址解析协议，更具通信方ip地址反查出对应的mac地址
- routing  路由

#### 确保可靠的TCP协议
- tcp 位于传输层，提供可靠的字节流服务，所谓字节流服务为了方便传输，将大块数据分割成报文段 segment为单位的数据包进行管理
- 确保数据能到达目标，三次握手

#### 负责域名解析的DNS服务


#### URI 与URL 
- URI  统一资源标识符，有某个协议方案表示的资源的定位标识符
	- Uniform 
	- Resource
	- Identifier 
	- 某个协议 可以 http  ftp 等
- URL 表示指定的URI
	-  协议、登录信息、服务器地址、服务器端口号、带层次的文件路径、查询字符串、片段标识符