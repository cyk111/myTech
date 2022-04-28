### docker 使用

- docker 下安装redis并设置密码
	- docker search redis
	- docker pull redis
	- docker run -d --name database_redis -p 16379:6379 redis --requirepass 123456
	- 端口 16379 ，密码：123456