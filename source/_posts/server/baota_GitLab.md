---

title: GitLab进行托管宝塔代码
date: 2017-07-29
categories: [server]
tags: [GitLab]

---


## GitLab进行托管宝塔代码 ##


具体操作：

1. 登录阿里云code代码托管平台，地址是：code.aliyun.com

2. 登录上之后是这个页面，按照截图说明操作

3. 新建项目之后是这个样子，按照截图说明操作


4. 这个时候就可以在本地克隆项目了，修改代码之后push就可以了，这个时候只是push到code代码仓库里面了，还没有更新到服务器上，此时需要在服务器上安装git，安装方式yum安装，yum install git，即可，但是这个安装的版本比较低，如果需要高版本git，请自行谷歌安装。

5. 在服务器上克隆此项目，切换到服务器的站点目录，克隆成功之后，这只是手动克隆到服务器上，最重要的来了(敲黑板)，下一步需要在宝塔上配置钩子，才能真正做到git自动化，同时更新代码到服务器。

6. 配置钩子第一步：

![](https://s2.ax1x.com/2019/03/27/AaGrgs.png)

7. 点击webhook钩子的设置，是这个界面，如果是第一次，里面就是空的，按照截图说明操作即可。

![](https://s2.ax1x.com/2019/03/27/AaGgbV.png)

8. 执行的脚本填写内容为：

  cd /www/wwwroot/项目目录名称

  git pull

  chown -R www:www ./*


9. 最重要的一步来了，配置钩子的地址，如下图：

![](https://s2.ax1x.com/2019/03/27/AaG58J.png)

10. 点击之后是下图界面：

![](https://s2.ax1x.com/2019/03/27/AaG7K1.png)

11. 最终组成的钩子地址形式为:

http://123.206.70.236:8888/hook?access_key=UG79Q6ovput6X7J1J2eSnun5mG23h1uWiLTSpxoCTfrPsObp


12. 将此地址添加到code里面的WebHook里面即可。

![](https://s2.ax1x.com/2019/03/27/AaGOUO.png)

至此，整个git自动化配置完毕，即可开始多人合作开发的愉快之旅！