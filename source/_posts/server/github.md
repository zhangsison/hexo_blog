---

title: github访问慢的解决办法
date: 2017-03-01
categories: [server]
tags: [github, CDN]

---

# 站长工具
都是搞开发的，都会用F12看看网络或者资源请求的地址是什么，以上面耗时最慢的地址为例，
域名为：github.githubassets.com
打开站长工具的PING功能，地址为：http://ping.chinaz.com/github.githubassets.com

# GitHub 镜像访问三个最常用的镜像地址

<https://github.com.cnpmjs.org>

<https://hub.fastgit.org>

<https://github.91chifun.workers.dev>

~~git@github.com:~~ zhangsison/hh.git

> https://github.com.cnpmjs.org/zhangsison/hh.git



## 网页输入加速下载地址

http://toolwa.com/github/

https://github.zhlh6.cn/



## GitHub raw 加速

GitHub raw 域名并非 github.com 而是 raw.githubusercontent.com，上方的 GitHub 加速如果不能加速这个域名，那么可以使用 Static CDN 提供的反代服务。
将 raw.githubusercontent.com 替换为 raw.staticdn.net 即可加速或者使用谷歌插件镜像



# stackoverflow、github访问慢的解决办法

获取GitHub官方CDN地址
打开https://www.ipaddress.com/

#   加速网址

151.101.193.69     stackoverflow.com
104.25.15.31       codepen.io
117.23.61.137      www.topthink.com
47.95.164.112      www.csdn.net
47.95.47.253       blog.csdn.net
104.25.212.20      www.gitbook.com
220.170.53.27      www.v2ex.com
115.159.21.113     coding.net
104.25.213.20      legacy.gitbook.com
14.215.177.38      www.baidu.com
58.223.168.56      www.v2ex.com
14.21.42.99        github.com
151.101.72.133     assets-cdn.github.com
151.101.193.194    github.global.ssl.fastly.net
178.128.123.58     www.jpdaka.com
206.189.89.118     www.jpdaka.com


> http://tool.chinaz.com/dns?type=1&host=github.com&ip=

> 在运行文本框输入c:\windows\system32\drivers\etc，点击确定按钮

# 打开hosts文件添加 #

>  52.74.223.119    https://github.com

> 国内ipTTL值小的IP址     https://stackoverflow.com/

# Google Hosts #
![Google Hosts](https://camo.githubusercontent.com/20ff616e6fdca147e0fd26da415cec2cacce290a/68747470733a2f2f7777772e676f6f676c652e636f6d2f6c6f676f732f646f6f646c65732f323031382f686f6c69646179732d323031382d736f75746865726e2d68656d697370686572652d6461792d332d353636323338313038393735313034302d3278612e676966)

- https://github.com/googlehosts/hosts

- 此处的文字仅用于说明，条款以LICENSE文件中的内容为准。

- 请在遵守当地相关法律法规的前提下使用本项目，由此产生的问题我们不负任何责任。
