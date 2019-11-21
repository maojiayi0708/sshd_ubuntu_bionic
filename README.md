带sshd的ubuntu bionic镜像
============

使用
-----

执行以下命令创建ubuntu-ssh镜像

	docker build -t maojiayi0708/sshd:bionic .



运行
--------------------

从前面创建的\镜像运行一个容器,在所有接口绑定到端口2222,执行:

	docker run -d -p 0.0.0.0:2222:22 maojiayi0708/sshd:bionic


第一次你运行你的容器,将为用户“root”生成一个随机密码，通过查看容器运行的日志来查看密码:

	docker logs <CONTAINER_ID>

你将看到一个如下输出:

	========================================================================
	You can now connect to this Ubuntu container via SSH using:

	    ssh -p <port> root@<host>
	and enter the root password 'U0iSGVUCr7W3' when prompted

	Please remember to change the above password as soon as possible!
	========================================================================

在这种情况下, `U0iSGVUCr7W3` 就是分配给`root`用户的密码

完成!


设置一个特定的root帐户密码
------------------------------------------------

如果你想使用一个预设的密码,而不是一个随机生成的一个,你可以在运行容器时设置环境变量“ROOT_PASS”设置一个特定密码:

	docker run -d -p 2222:22 -e ROOT_PASS="mypass" maojiayi0708/sshd:bionic


添加SSH授权密钥
--------------------------

如果你想用你的SSH密钥登录,您可以使用“AUTHORIZED_KEYS”环境变量。你可以添加多个公共密钥对:

    docker run -d -p 2222:22 -e AUTHORIZED_KEYS="`cat ~/.ssh/id_rsa.pub`" maojiayi0708/sshd:bionic

