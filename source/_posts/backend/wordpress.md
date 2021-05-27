---

title: wordpress
date: 2019-10-08
categories: [php]
tags: [wordpress]

---



# wordpress 



## wordpress主题

>https://wordpress.org/themes/


## 解决wordpress打开慢

```php
$open_sans_font_url = "https://fonts.googleapis.com/css?family=Open+Sans:300italic,400italic,600italic,300,400,600&subset=$subsets"; $open_sans_font_url = "https://fonts.useso.com/css?family=Open+Sans:300italic,400italic,600italic,300,400,600&subset=$subsets";
```
## 加速网站 ##
WPJAM BASIC插件加速网站

使用CDN加速网站 可参考《[wordpress如何使用阿里云CDN加速网站？](https://aliyun.gaomeluo.com/414.html)》

1安装静态插件，生成html静态页。我推荐使用WP Fastest Cache插件，具体查看《[wordpress真正静态化插件WP Fastest Cache如何设置使用](https://aliyun.gaomeluo.com/424.html)》

2、wordpress开启Memcached缓存，具体查看《[wordpress如何开启Memcached缓存来加速网站？](https://aliyun.gaomeluo.com/435.html)》

3、使用Cachify插件，具体查看《[如何解决wordpress站waiting ttfb时间过长](https://aliyun.gaomeluo.com/444.html)》

## WordPress版微信小程序安装 ##
![Fc3Uqs.png](https://s1.ax1x.com/2018/12/25/Fc3Uqs.png)
WordPress的插件里，有个json api 的插件


- 配置微信小程序的服务器域名和业务域名
- 配置HTTPS [参考](https://www.watch-life.net/wordpress/wordpress-https-link.html)
- 安装Wordpress版微信小程序