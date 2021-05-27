---

title: docker
date: 2017-07-01
categories: [server]
tags: [docker,laradock]

---

# docker laradock 环境

> https://laradock.io/
> https://laradock.linganmin.cn/zh/getting-started/


```bash

docker-compose build nginx

docker-compose restart nginx

docker-compose up -d mysql phpmyadmin

docker-compose up -d nginx mysql phpmyadmin redis workspace 

docker-compose ps

docker-compose stop 


docker-compose down

```


## 文档地址
> http://houdunren.gitee.io/note/wamp/laradock.html#php

## 视频
[laradock视频](https://www.bilibili.com/video/BV1m4411P7er/)



# 国内镜像

>https://developer.aliyun.com/composer

```bash
{
"debug": true,
"registry-mirrors": [
"https://naxeb9hk.mirror.aliyuncs.com"
],
"experimental": true
}
```





## docker

```bash

docker run -it 启动镜像

docker attach d22d6945e23c 进入镜像

docker inspect 917d356d6353

docker commit 创建镜像

docker start ID 启动容器

docker exec -i -t 9f4d4764b641 /bin/bash 进入已启动的容器

sudo mkdir

docker port NAME查看端口映射情况

docker run -it -d -p 5000:80 --name centos7 centos:7.4.1708

```

## 下载最新版的docker-compose文件 

> $ sudo curl -L https://github.com/docker/compose/releases/download/1.16.1/docker-compose-`uname -s`-`uname -m` -o /usr/local/bin/docker-compose

添加可执行权限 

```bash

$ sudo chmod +x /usr/local/bin/docker-compose

docker stop 停止运行中容器

docker stop $(docker ps -qa) 停止所有运行中的容器

docker restart 重启容器

docker ps -a 查看所有容器

docker rm 移除处于终止状态的容器

docker rmi $(docker images -q)删除所有镜像

docker rm $(docker ps -qa) 移除处于终止状态的容器

docker logs 从容器中去日志

docker diff 列出容器中被改变的文件或者目录

docker top 显示运行容器的进程信息

docker cp 从容器中拷贝文件或者目录到本地

docker inspect 查看容器详细信息

docker images 显示本地已有镜像

docker info 显示docker系统信息

docker commit -m -a 提交更新后的镜像

docker build 通过Dockerfile来构建镜像

docker import 本地导入镜像

docker search 查找仓库中镜像

docker push 将镜像推送到仓库

docker pull 将仓库中镜像下载到本地

docker save -o mysql_5.6.tar mysql:5.6 导出镜像到本地

docker load < mysql_5.6.tar 载入镜像

docker rmi 移除镜像

docker attach 运行中容器的stdin，进行命令执行的动作

docker history 显示镜像的历史

docker run -d -p 8080:80 --name webserver nginx

镜像名称是nginx，--name表示为这个容器取个名称叫webserver

创建一个最简单的Dockerfile文件

mkdir mynginx

cd mynginx

touch Dockerfile

docker build .

docker build -t nginx:v3 .

```

