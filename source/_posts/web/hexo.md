---

title: Hexo
date: 2017-12-06
categories: [web]
tags: [hexo]

---



# hexo 主题

https://butterfly.js.org



## Hexo优化与常用命令 ##

安装

> npm install hexo -g #安装
>
> npm update hexo -g #更新
>
> hexo init #初始化

## 模版 ##
```bash

hexo new "postName" #新建文章

hexo new page "pageName" #新建页面

hexo generate #生成静态页面至public目录

hexo server #开启预览访问端口（默认端口4000，'ctrl + c'关闭server）

hexo deploy #将.deploy目录部署到GitHub

清空hexo静态文件和缓存，并重新生成

hexo clean&&hexo g  //清空缓存并生成静态文件

本地预览，确没有问题再进行发布

hexo s -p 4000 或者 hexo s  //启动本地服务默认
```

## 部署发布 ##
```bash
hexo clean #清除缓存 网页正常情况下可以忽略此条命令

hexo d 或者  hexo deploy#部署

hexo d 或者 gulp deploy //部署发布

## 完成后部署 ##

两个命令的作用是相同的

hexo generate --deploy

hexo deploy --generate
```

## seo优化 ##

让百度收录你的站点

我们首先要做的就是让各大搜索引擎收录你的站点，我们在刚建站的时候各个搜索引擎是没有收录我们网站的，在搜索引擎中输入site:<域名>,如果如下图所示就是说明我们的网站并没有被百度收录。我们可以直接点击下面的“网址提交”来提交我们的网站

![jpdaka.com](https://s1.ax1x.com/2018/12/07/F1vEid.png "jpdaka.com")


## 生成网站地图 ##

我们需要使用npm自动生成网站的sitemap，然后将生成的sitemap提交到百度和其他搜索引擎
安装sitemap插件

> npm install hexo-generator-sitemap --save      
> npm install hexo-generator-baidu-sitemap --save



## 链接提交 ##

使用说明

1. 链接提交工具是网站主动向百度搜索推送数据的工具，本工具可缩短爬虫发现网站链接时间，网站时效性内容建议使用链接提交工具，实时向搜索推送数据。本工具可加快爬虫抓取速度，无法解决网站内容是否收录问题
2. 百度搜索资源平台为站长提供链接提交通道，您可以提交想被百度收录的链接，百度搜索引擎会按照标准处理，但不保证一定能够收录您提交的链接

![enter description here](https://s1.ax1x.com/2018/12/07/F1vfeO.png)

**主动推送**

> 安装插件npm install hexo-baidu-url-submit --save

然后再根目录的配置文件中新增字段

> baidu_url_submit: count: 100 # 提交最新的一个链接

> host: www.cherryblog.site # 在百度站长平台中注册的域名

> token: 8OGYpxowYnhgVsUM # 请注意这是您的秘钥， 所以请不要把博客源代码发布在公众仓库里!

> path: baidu_urls.txt # 文本文档的地址， 新链接会保存在此文本文档里

 

**在加入新的deploye**

> deploy:
>
> - type:baidu_url_submitter


这样执行hexo deploy的时候，新的链接就会被推送了

**自动推送工具代码**

请将以下代码安装在网站页面中，安装完成后即可实现链接自动推送功能

```bash
    (function(){
    var bp = document.createElement('script');
    var curProtocol = window.location.protocol.split(':')[0];
    if (curProtocol === 'https') {
    bp.src = 'https://zz.bdstatic.com/linksubmit/push.js';
    }
    else {
    bp.src = 'http://push.zhanzhang.baidu.com/push.js';
    }
    var s = document.getElementsByTagName("script")[0];
    s.parentNode.insertBefore(bp, s);
    })();

```

## 让google收录你的站点 ##

> 相比于百度，google的效率实在不能更快，貌似十分钟左右站点就被收录了，其实方法是和百度是一样的，都是先验证你的站点所有权，然后提交sitemap
> google站点平台：https://www.google.com/webmasters/，然后就是注册账号、验证站点、提交sitemap，被google收录了 


![](https://s1.ax1x.com/2018/12/07/F1xzDK.png)

## 优化你的url ##

seo搜索引擎优化认为，网站的最佳结构是用户从首页点击三次就可以到达任何一个页面,打开_config.yml编辑

> url: http://xxx.com

> root: /

> permalink: :title.html


> https://www.jpdaka.com/hexos/git-coding.html



**robots.txt文件**

在source文件夹中新建文件robots.txt，可以参考我的：

> User-agent: * Allow: /
> Allow: /archives/
> Disallow: /vendors/
> Disallow: /categories/
>
>
> Sitemap: http://www.xxx.com/sitemap.xml
> Sitemap: http://www.xxx.com/baidusitemap.xml

**获取关键词**

现在搜关键词全是广告，其实百度已经提供了一个接口，每次使用过百度搜索的时候下面的下拉条会出现一堆相关的关键词，这下关键词的权重是非常高的，采集这些关键词然后用在自己的文章中效果还可以，但是要记住不能堆砌关键词。

接口：

> https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=

比如：

> https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=dibai   

搜过结果：
```js
window.baidu.sug({q:"dibai",p:false,s:["迪拜","迪拜旅游","迪拜航空","迪拜时间","迪拜塔","迪拜天气","迪拜签证","迪拜时差","迪拜是哪个国家的","迪拜机场"]});
```
一般回显10个关键词

提取代码如下：
```bash
coding:utf-8 import requests import time print unicode('Langzi.Fun 关键词采集开启....','utf-8') #time.sleep(0.5) key = raw_input(unicode('输入关键词:','utf-8')) site_url = 'https://sp0.baidu.com/5a1Fazu8AA54nxGko9WTAnF6hhy/su?wd=' + (str(key)) r = requests.get(site_url) print r.content.replace('window.baidu.sug({q:','').replace('});','').replace(',p:false,s:','').replace('"','').replace(str(key),'')
```

## 使用gulp压缩代码 ##

**全局安装gulp**

> npm install gulp -g

我们需要的是使用gulp压缩我们的代码

**新建package.json**

使用npm init就可以创建package.json文件 

```js

    {
      "name": "hexo-site",
      "version": "0.0.0",
      "private": true,
      "hexo": {
    "version": "3.7.1"
      },
      "dependencies": {
    "ejs": "^2.5.5",
    "hexo": "^3.7.0",
    "hexo-abbrlink": "^2.0.4",
    "gulp-htmlclean": "^2.7.22",
    "gulp-htmlmin": "^5.0.1",
    "gulp-imagemin": "^5.0.3",
    "gulp-minify-css": "^1.2.4",
    "gulp-uglify": "^3.0.1",
    "hexo-clean-css": "0.0.3",
    "hexo-deployer-git": "^0.3.1",
    "hexo-generator-archive": "^0.1.5",
    "hexo-generator-baidu-sitemap": "^0.1.2",
    "hexo-generator-category": "^0.1.3",
    "hexo-generator-feed": "^1.2.2",
    "hexo-generator-index": "^0.2.1",
    "hexo-generator-json-content": "^2.2.0",
    "hexo-generator-seo-friendly-sitemap": "0.0.21",
    "hexo-generator-sitemap": "^1.2.0",
    "hexo-generator-tag": "^0.2.0",
    "hexo-html-minifier": "0.0.2",
    "hexo-imagemin": "^0.1.0",
    "hexo-renderer-ejs": "^0.3.1",
    "hexo-renderer-less": "^0.2.0",
    "hexo-renderer-marked": "^0.3.2",
    "hexo-renderer-stylus": "^0.3.3",
    "hexo-server": "^0.3.1",
    "hexo-uglify": "0.0.5"
      },
      "devDependencies": {
    "gulp-htmlclean": "^2.7.15",
    "gulp-htmlmin": "^3.0.0",
    "gulp-minify-css": "^1.2.4",
    "gulp-notify": "^3.0.0",
    "gulp-path": "^3.0.3",
    "gulp-plumber": "^1.1.0",
    "gulp-rename": "^1.2.2",
    "gulp-rev-append": "^0.1.8",
    "gulp-sequence": "^0.4.6",
    "gulp-uglify": "^2.0.0",
    "gulp-watch": "^4.3.11",
    "jshint-stylish": "^2.2.1",
    "gulp": "^3.9.1",
    "gulp-autoprefixer": "^6.0.0",
    "gulp-jshint": "^2.1.0",
    "gulp-less": "^4.0.1",
    "jshint": "^2.9.6"
      }
    }
```

## 安装gulp插件 ##

本站使用 Snippet主题 （ Gulp入门指南）安装所需要的插件即可

> 在Hexo根目录下创建一个名为 gulpfile.js 的文件：
>
> require('./themes/hexo-theme-snippet/gulpfile');
>
> 运行 gulp：
>
> gulp 或者 gulp default   //执行打包任务
>
> 清空hexo静态文件和缓存，并重新生成
>
> hexo clean && hexo g  //清空缓存并生成静态文件
>
> 本地预览，确没有问题再进行发布
>
> hexo s -p 4000 或者 hexo s  //启动本地服务默认


## DNS加速你的网站 ##

Cloudflare 提供DNS解析服务，而且速度很快，它提供了免费的https服务(但不是应用SSL证书)
需要把我们购买域名的那个地方的解析删掉，替换cloudflare给你的DNS解析服务器
回到clouldflare 上面选择crypto选项然后下面选择full或者是Flexible


## 使用Netlify部署博客及部署自动化 ## 

Netlify 是一个提供静态资源网络托管的综合平台

> 能够托管服务，免费 CDN
>
> 能够绑定自定义域名
>
> 能够启用免费的TLS证书，启用HTTPS
>
> 支持自动构建
>
> 提供 Webhooks 和 API


首先使用你的 GitHub 账号登陆 Netlify，登陆后进入空间管理中心，，点击New site from git按钮开始部署你的博客然后根据自己的托管平台，可以选择GitHub、GitLab或者BitBucket点击GitHub之后会弹出一个让你授权的窗口，给 Netlify 授权后，就会自动读取你 GitHub选择仓库后，Netlify 会自动识别到 hexo，并填入相关信息，这时候只要无脑点击 Deploy site就可以如果你要绑定自己买的域名，就直接点击第二步Set up custom domain Netlify 会提示你去域名DNS解析处，修改域名的CNAME记录

## hexo GitHub coding 404页面 ##


GitHub Pages有提供制作404页面的指引：[Custom 404 Pages](https://help.github.com/articles/creating-a-custom-404-page-for-your-github-pages-site/)

直接在根目录下创建自己的404.html或者404.md就可以

## hexo部署到GitHub成功，但是无法访问 ##

查看Pages 服务或GitHub 的域名是否有部署设置绑定域名，coding有时候会自动删除域名需要手动重新绑定

[![kFYLgx.md.png](https://s2.ax1x.com/2019/01/22/kFYLgx.md.png)](https://imgchr.com/i/kFYLgx)