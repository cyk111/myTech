#### https


- http 缺点
	- 通信使用明文，不加密，内容可能被窃听
	- 不验证通信方的身份，可能遭遇伪装
	- 无法证明报文的完整性，所以可能被篡改


#### 通信使用明文可能被窃听
- 通信加密 SSL TLS
- 内容加密

#### 不验证通信方的身份可能遭遇伪装
- 任何人都可以发起请求
- 查明对方的证书

####  无法证明报文完整性，可能已遭篡改
- 接收的内容可能有误
- 如何防止篡改


#### HTTPS = http + 加密+认证+完整性保护
