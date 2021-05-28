---

title: ftp
date: 2015-07-09
categories: [server]
tags: [ftp]

---


# ftp

## 步骤一：安装 vsftpd

> yum install vsftpd -y

安装完成后，启动 FTP 服务：

## 步骤二：启动 vsftpd 服务 ##

> service vsftpd start

启动后，可以看到系统已经

监听了 21 端口


> netstat -nltp | grep 21

## 配置 FTP 权限

目前 FTP 服务登陆允许匿名登陆，也无法区分用户访问，我们需要配置 FTP 访问权限

了解 VSFTP 配置

vsftpd 的配置目录为 /etc/vsftpd，包含下列的配置文件：

vsftpd.conf 为主要配置文件

ftpusers 配置禁止访问 FTP 服务器的用户列表

user_list 配置用户访问控制

匿名访问和切换根目录都会给服务器带来安全风险，我们把这两个功能关闭。

编辑 /etc/vsftpd/vsftpd.conf，

找到下面两处配置并修改：

## 禁用匿名用户

> anonymous_enable=NO

## 禁止切换根目录

> chroot_local_user=YES

编辑完成后，按Ctrl + S保存配置，重新启动 FTP 服务，如：

> service vsftpd restart

创建 FTP 用户

创建一个用户ftpuser：


> useradd ftpuser

添加用户。本例添加名为 ftpuser1 的用户。输入命令：useradd -m -d /home/ftpuser1 -s /sbin/nologin ftpuser1

设置用户登录密码。本例为 ftpuser1 用户设置登录密码。输入命令：passwd ftpuser1，输入密码并确认即可。

![](https://mc.qcloudimg.com/static/img/f8912544914d11dfc1dd7e0a6db16f11/image.png)

## 为用户ftpuser设置密码 ：

> echo "IMyC7eKy" | passwd ftpuser --stdin


> userdel

限制该用户仅能通过 FTP 访问

限制用户ftpuser只能通过 FTP 访问服务器，而不能直接登录服务器：

	usermod -s /sbin/nologin ftpuser
	
	useradd -d /alidata/www/test test      //增加用户test，并制定test用户的主目录为/alidata/www/test

passwd test      为test用户设置密码

## 3.更改用户相应的权限设置：

	usermod -s /sbin/nologin test      //限定用户test不能telnet，只能ftp
	usermod -s /sbin/bash test      //用户test恢复正常
	usermod -d /test test      //更改用户test的主目录为/test

为用户分配主目录

为用户ftpuser创建

主目录

并约定：

	/data/ftp为主目录, 该目录不可上传文件
	
	/data/ftp/pub文件只能上传到该目录下
	
	mkdir -p /data/ftp/pub

## 创建登录欢迎文件 ：

    echo "Welcome to use FTP service." /data/ftp/welcome.txt

**设置访问权限：**

	chmod a-w /data/ftp && chmod 777 -R /data/ftp/pub
	
	Redirecting to /bin/systemctl restart vsftpd.service 解决以下
	
	$ systemctl enable vsftpd.service
	
	$ systemctl start vsftpd.service
	
	systemctl stop vsftpd.service
	
	systemctl restart vsftpd.service

## 使用 FTP 工具登录主机 ##

![](https://mc.qcloudimg.com/static/img/bceea82794b39dc24b9d37dc2d1c9891/1.png)



## linux下利用vsftp设置ftp账号 ##

> 新建一个ftp账号

useradd 用户名 -s /sbin/nologin
passwd 用户名

> 修改用户根目录

vim /etc/passwd
将里面账号对应的登录根目录，修改成你想要的。
> 修改vsftp.conf配置

vi /etc/vsftpd/vsftpd.conf

将里面一些内容修改成以下对应的选项，如果不存在的，则需要追加进去：

	    userlist_enable=YES
	    userlist_deny=NO
	    tcp_wrappers=YES
	    # 这一句是设置允许FTP登录的用户，一会编辑这个文件，将用户名写入即可
	    userlist_file=/etc/vsftpd/user_list 
	    chroot_local_user=YES
	    chroot_list_enable=YES
	    # (default follows)
	    chroot_list_file=/etc/vsftpd/chroot_list
	    allow_writeable_chroot=YES

> 重启vsftp生效

service vsftpd restart