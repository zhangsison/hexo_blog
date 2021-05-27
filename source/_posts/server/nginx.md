---

title: nginx
date: 2016-08-20
categories: [server]
tags: [nginx]

---


## nginx

命令: nginx -c /usr/local/nginx/conf/nginx.conf

重启服务： service nginx restart

快速停止或关闭Nginx：nginx -s stop

正常停止或关闭Nginx：nginx -s quit

配置文件修改重装载命令：nginx -s reload


## 反向代理
什么是反向代理？ 互联网应用基本都基于CS基本结构，即client端和server端。代理其实就是在client端和真正的server端之前增加一层提供特定服务的服务器，即代理服务器。

### 正向代理
反向代理不好理解，正向代理大家总有用过，翻墙工具其实就是一个正向代理工具。它会把
们访问墙外服务器server的网页请求，代理到一个可以访问该网站的代理服务器proxy，这个代理服务器proxy把墙外服务器server上的网页内容获取，再转发给客户

### 反向代理 
在反向代理中（事实上，这种情况基本发生在所有的大型网站的页面请求中），客户端发送的请求，想要访问server服务器上的内容。但将被发送到一个代理服务器proxy，这个代理服务器将把请求代理到和自己属于同一个LAN下的内部服务器上，而用户真正想获得的内容就储存在这些内部服务器上

### 为什么要Nginx反向代理
使用反向代理最主要的两个原因：
1.安全及权限。可以看出，使用反向代理后，用户端将无法直接通过请求访问真正的内容服务器，而必须首先通过Nginx。可以通过在Nginx层上将危险或者没有权限的请求内容过滤掉，从而保证了服务器的安全。
2.负载均衡,例如一个网站的内容被部署在若干台服务器上，可以把这些机子看成一个集群，那么Nginx可以将接收到的客户端请求“均匀地”分配到这个集群中所有的服务器上（内部模块提供了多种负载均衡算法），从而实现服务器压力的负载均衡


## 负载均衡
### 均衡策略
nginx的负载均衡策略可以划分为两大类：内置策略和扩展策略。内置策略包含加权轮询和ip hash，在默认情况下这两种策略会编译进nginx内核，只需在nginx配置中指明参数即可。扩展策略有很多，如fair、通用hash、consistent hash等，默认不编译进nginx内核。

- 加权轮询 第一，如果可以把加权轮询算法分为先深搜索和先广搜索，那么nginx采用的是先深搜索算法，即将首先将请求都分给高权重的机器，直到该机器的权值降到了比其他机器低，才开始将请求分给下一个高权重的机器；第二，当所有后端机器都down掉时，nginx会立即将所有机器的标志位清成初始状态，以避免造成所有的机器都处在timeout的状态，从而导致整个前端被夯住

- ip hash是nginx内置的另一个负载均衡的策略，流程和轮询很类似，只是其中的算法和具体的策略有些变化

- fair策略是扩展策略，默认不被编译进nginx内核。其原理是根据后端服务器的响应时间判断负载情况，从中选出负载最轻的机器进行分流。

- 通用hash、一致性hash ,这两种也是扩展策略，在具体的实现上有些差别，通用hash比较简单，可以以nginx内置的变量为key进行hash，一致性hash采用了nginx内置的一致性hash环，可以支持memcache

- session_sticky 此种策略就是一次会话内的请求都会落到同一个结点上

## nginx 跨域 ##



Nginx可以纯前端解决请求跨域问题。 特别是在前后端分离调试时， 经常需要在本地起前端工程， 接口希望拉取服务端的实际数据而不是本地的mock本地起一个nginx server。server_name是mysite-base.com，比如现在需要请求线上www.kaola.com域下的线上接口 www.kaola.com/getPCBanner… 的数据，当在页面里直接请求，浏览器会报错为了绕开浏览器的跨域安全限制，现在需要将请求的域名改成mysite-base.com。同时约定一个url规则来表明代理请求的身份，然后Nginx通过匹配该规则，将请求代理回原来的域。Nginx配置如下：


		#请求跨域，这里约定代理请求url path是以/apis/开头
		location ^~/apis/ {
		    # 这里重写了请求，将正则匹配中的第一个()中$1的path，拼接到真正的请求后面，并用break停止后续匹配
		    rewrite ^/apis/(.*)$ /$1 break;
		    proxy_pass https://www.kaola.com/;
		}  
	
	//直接请求nginx也是会报跨域错误的这里设置允许跨域;如果代理地址已经允许跨域则不需要这些, 否则报错(虽然这样nginx跨域就没意义了)
	
	add_header Access-Control-Allow-Origin *;
	add_header Access-Control-Allow-Headers X-Requested-With;
	add_header Access-Control-Allow-Methods GET,POST,OPTIONS;
在页面代码里，把请求url换成http://mysite-base.com/apis/getPCBannerList.html 。这样就可以正常请求到数据

## 适配PC与移动环境 ##
Nginx可以通过内置变量$http_user_agent，获取到请求客户端的userAgent，从而知道用户处于移动端还是PC，进而控制重定向到H5站还是PC站

	   location / {
	        # 移动、pc设备适配
	        if ($http_user_agent ~* '(Android|webOS|iPhone|iPod|BlackBerry)') {
	            set $mobile_request '1';
	        }
	        if ($mobile_request = '1') {
	            rewrite ^.+ http://mysite-base-H5.com;
	        }
	    }  

## 合并请求 ##
前端性能优化中重要一点就是尽量减少http资源请求的数量 本地server mysite-base.com为例，static/js文件夹下有三个文件，文件内容很简单，分别为： 
Nginx配置如下：
	    # js资源http-concat
	    # nginx-http-concat模块的参数远不止下面三个，剩下的请查阅文档
	    location /static/js/ {
	        concat on; # 是否打开资源合并开关
	        concat_types application/javascript; # 允许合并的资源类型
	        concat_unique off; # 是否允许合并不同类型的资源
	        concat_max_files 5; # 允许合并的最大资源数目
	    }
复制代码当在浏览器请求http://mysite-base.com/static/js/??a.js,b.js,c.js 时，发现三个js被合并成一个返回了

## 图片处理 ## 

在前端开发中，经常需要不同尺寸的图片要用到ngx_http_image_filter_module模块。这个模块是非基本模块，需要安装。 下面是图片缩放功能部分的Nginx配置：


    # 图片缩放处理
    # 这里约定的图片处理url格式：以 mysite-base.com/img/路径访问
    location ~* /img/(.+)$ {
        alias /Users/cc/Desktop/server/static/image/$1; #图片服务端储存地址
        set $width -; #图片宽度默认值
        set $height -; #图片高度默认值
        if ($arg_width != "") {
            set $width $arg_width;
        }
        if ($arg_height != "") {
            set $height $arg_height;
        }
        image_filter resize $width $height; #设置图片宽高
        image_filter_buffer 10M;   #设置Nginx读取图片的最大buffer。
        image_filter_interlace on; #是否开启图片图像隔行扫描
        error_page 415 = 415.png; #图片处理错误提示图，例如缩放参数不是数字
    }

此外，可以通过proxy_cache配置Nginx缓存，避免每次请求都重新处理图片，减少Nginx服务器处理压力；还以可以通过和nginx-upload-module一起使用加入图片上传的功能等


## 快速实现简单的访问限制 ##

    location / {
        deny  192.168.1.100;
        allow 192.168.1.10/200;
        allow 10.110.50.16;
        deny  all;
    }
其实deny和allow是ngx_http_access_module模块（已内置）中的语法。采用的是从上到下匹配方式，匹配到就跳出不再继续匹配。上述配置的意思就是，首先禁止192.168.1.100访问，然后允许192.168.1.10-200 ip段内的访问（排除192.168.1.100），同时允许10.110.50.16这个单独ip的访问，剩下未匹配到的全部禁止访问。实际生产中，经常和ngx_http_geo_module模块（可以更好地管理ip地址表，已内置）配合使用。

## 请求过滤 ##

		根据状态码过滤
		
		error_page 500 501 502 503 504 506 /50x.html;
		    location = /50x.html {
		        #将跟路径改编为存放html的路径。
		        root /root/static/html;
		    }
		根据URL名称过滤，精准匹配URL，不匹配的URL全部重定向到主页。
		location / {
		    rewrite  ^.*$ /index.html  redirect;
		}
		根据请求类型过滤
		
		if ( $request_method !~ ^(GET|POST|HEAD)$ ) {
		        return 403;
		    }

## nginx如何实现负载均衡 ##

Upstream指定后端服务器地址列表

	upstream balanceServer {
	    server 10.1.22.33:12345;
	    server 10.1.22.34:12345;
	    server 10.1.22.35:12345;
	}
	
	复制代码在server中拦截响应请求，并将请求转发到Upstream中配置的服务器列表。
	
	    server {
	        server_name  fe.server.com;
	        listen 80;
	        location /api {
	            proxy_pass http://balanceServer;
	        }
	    }

轮询策略

	upstream balanceServer {
	    server 10.1.22.33:12345;
	    server 10.1.22.34:12345;
	    server 10.1.22.35:12345;
	}


## 反向代理 ##

		upstream tomcats {
		    server 127.0.0.1:9001;
		    server 127.0.0.1:9002;
		}
		
		server {
		    listen 80;
		    server_name  www.lianggzone.com;
		    location / {
		        proxy_pass_header Server;
		        proxy_set_header Host $http_host;
		        proxy_set_header X-Real-IP $remote_addr;
		        proxy_set_header X-Scheme $scheme;
		        proxy_pass http://tomcats;
		    }
		}