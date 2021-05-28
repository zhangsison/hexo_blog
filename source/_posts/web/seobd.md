---

title: seo自动推送百度
date: 2016-12-06
categories: [web]
tags: [百度]

---



# SEO链接提交


## 链接提交 ##

百度搜索资源平台为站长提供链接提交通道，您可以提交想被百度收录的链接，百度搜索引擎会按照标准处理，但不保证一定能够收录您提交的链接。

**1.百度站长入口** 

> http://zhanzhang.baidu.com/linksubmit/index  

**2.数据提交方式**

> 主动推送（实时）、自动推送、 sitemap、 手动提交

## 主动推送接口 ##

- 数据类型选择


- 接口调用地址： http://data.zz.baidu.com/urls?site=www.jpdaka.com&token=SADASDASDASD 

- php推送

		$urls = array(
		'http://www.example.com/1.html',
		'http://www.example.com/2.html',
		);
		$api = 'http://data.zz.baidu.com/urls?site=www.jpdaka.com&token=SADASDASDASD';
		$ch = curl_init();
		$options =  array(
		CURLOPT_URL => $api,
		CURLOPT_POST => true,
		CURLOPT_RETURNTRANSFER => true,
		CURLOPT_POSTFIELDS => implode("\n", $urls),
		CURLOPT_HTTPHEADER => array('Content-Type: text/plain'),
		);
		curl_setopt_array($ch, $options);
		$result = curl_exec($ch);
		echo $result;
   



## 自动推送百度 ##
```
	(function(){
	
	var bp = document.createElement('script');
	
	bp.src = '//push.zhanzhang.baidu.com/push.js';
	
	var s = document.getElementsByTagName("script")[0];
	
	s.parentNode.insertBefore(bp, s);
	
	})();
```
## 改良版本 ##
```
	<script>
	(function(){
		var canonicalURL, curProtocol;
		//Get the <link> tag
		var x=document.getElementsByTagName("link");
		//Find the last canonical URL
		if(x.length > 0){
			for (i=0;i<x.length;i++){
				if(x[i].rel.toLowerCase() == 'canonical' && x[i].href){
					canonicalURL=x[i].href;
				}
			}
		}
		//Get protocol
	    if (!canonicalURL){
	    	curProtocol = window.location.protocol.split(':')[0];
	    }
	    else{
	    	curProtocol = canonicalURL.split(':')[0];
	    }
	    //Get current URL if the canonical URL does not exist
	    if (!canonicalURL) canonicalURL = window.location.href;
	    //Assign script content. Replace current URL with the canonical URL
		!function(){var e=/([http|https]:\/\/[a-zA-Z0-9\_\.]+\.baidu\.com)/gi,r=canonicalURL,t=document.referrer;if(!e.test(r)){var n=(String(curProtocol).toLowerCase() === 'https')?"https://sp0.baidu.com/9_Q4simg2RQJ8t7jm9iCKT-xh_/s.gif":"//api.share.baidu.com/s.gif";t?(n+="?r="+encodeURIComponent(document.referrer),r&&(n+="&l="+r)):r&&(n+="?l="+r);var i=new Image;i.src=n}}(window);})();
	</script>
```
## sitemap提交推送 ##

请填写数据文件地址


> a. 一次最多提交10个文件地址；

> b. 文件地址格式为txt或xml，每个地址文件最多包含50,000个网址且需小于10MB；

> c. 如果验证了网站的主域，那么sitemap文件中可包含该网站主域下的所有网址。