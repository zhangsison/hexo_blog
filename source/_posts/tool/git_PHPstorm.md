---

title: Git PHPstorm
date: 2016-09-07
categories: [tool]
tags: [PHPstorm, Git]

---

# 本地Git(版本控制)的搭建 #

使用PHPstorm以及PortableGit自带的Git工具,进行版本控制的搭建

- 打开PHPstorm的设置

![Alt text](https://box.kancloud.cn/502ea2a4f5ea71a8635eab3654205951_405x410.png '迪拜de天空')


- 点击右侧"+"添加, 选择你的项目文件夹 和 选择 git
- 
- 点击 "Configure VCS",选择设置好 你自己的 PortableGit Git文件地址即可
  ![](https://box.kancloud.cn/d4308b5563ba83954b1cc626c3e25286_725x386.png)
- 关闭重启PHPstorm,git服务就可以生效
![](https://box.kancloud.cn/e30ac42f571d8b39d3ae9504ecaf9914_770x490.png)
- 在项目文件点右键 既可以使用
![](https://box.kancloud.cn/128d3c24261ec55438ed69d21484a839_711x330.png)
也可以在左下角的版本控制面板中使用

# 本地项目推送远程GIT仓库 #
## 使用PHPSTORM推送项目到远程仓库 ##
![](https://box.kancloud.cn/e6e98a73adff63139869e9bff8f9040b_777x492.png)
## 初始化版本控制 ##
![](https://box.kancloud.cn/9d0a1b4dd61441249241c2159dee5679_675x407.png)
## 选择git ##
![](https://box.kancloud.cn/06a336dc378e67ccc30881144c568aa9_625x235.png)

## 添加文件到本地GIT库 ##
> 用鼠标选择你要添加到版本库的文件

![](https://box.kancloud.cn/59fc80e492bd670fec6789158828e797_499x478.png)


> 选择成功后 在选择的文件上点击右键 选择 git ----add

![](https://box.kancloud.cn/fc3e2685ad3fd98aa7145455ca786531_743x789.png)


> 添加到版本库的文件 他的颜色会变成绿色

![](https://box.kancloud.cn/d99f20fb7b2fb91897069aed315a0662_454x512.png)
标注文件并推送到远程仓库


> 在项目主点击右键 或者 VCS上选择 git----Commit Dir

![](https://box.kancloud.cn/30d719b9712fd002a763a70308b91761_692x773.png)



> 点击默认推送的 Define remote

![](https://box.kancloud.cn/48a210cf0a4090a22cfd448c51c4a371_590x566.png)



> 填写你远程仓库的别名和地址

![](https://box.kancloud.cn/84868ddefeee47df69f0a0c28302a8a6_602x568.png)

> 填写你远程仓库的密码

![](https://box.kancloud.cn/171c7859b66a48fecd720a756850f796_602x568.png)

# 使用PHPSTORM拉取全新的项目 #

> 注意 拉取全新的项目 会自动创建一个新目录 无需自己创建目录
> 通过欢迎界面的或者菜单中的 Create out from Version Control 创建

![](https://box.kancloud.cn/7510863c96b4c46cd5199e9bdd747bd4_487x441.png)
![](https://box.kancloud.cn/3c2cd8b168c880e455a476e8a44ffcd5_573x519.png)

## 填写仓库地址 和存储名称 ##
![](https://box.kancloud.cn/7148c80d87c50143043067aa06bf9e5b_542x197.png)

## 打开存储目录即可 ##
![](https://box.kancloud.cn/f151c8b3c7e7b23dc74d94d604d46a2e_790x650.png)

## 使用命令行创建远程仓库 ##

> 现在的git仓库很多 你可以使用主流共用的git仓库 如github.com等
> 当然 有条件也可以自己搭建个人的git仓库
> 我现在 就已经创建了一个私有远程git仓库

# git初始化 #



> 打开 PhpStorm的Terminal 快捷键 Alt+F12
>     使用windows命令行也可以

![](https://box.kancloud.cn/b2fb4bd5b4ca52b5337afdf1a2a415ef_449x371.png)


> Git初始化命令是
> git init

运行成功的后为
![](https://box.kancloud.cn/79ea98198a6042b87f7dbd0af29497fc_558x237.png)

- 如果git命令无法执行 请安装git并添加环境变量

把文件添加到版本库中

使用命令 git add .添加到暂存区里面去，不要忘记后面的小数点“.”，意为添加文件夹下的所有文件(夹)
> git add .

		也可以使用rm 命令剔除部分内容 例如runtime文件夹
		
		在本地仓库删除文件
		$ git rm 我的文件
		在本地仓库删除文件夹
		$ git rm -r 我的文件夹/
		
		git rm -r  runtime/
		
		填写本次GIT提交的描述信息
		
		git commit  -m "项目初始化"






- 为远程GIT仓库创建用户名或者别名

	git remote add origin git@github.com:yourname/仓库名.git
	origin为你为这个远程仓库定义的默认名字 当然你也可以添加其他的别名
	名字你可以随便起 当存在多个远程时候 他就是区分仓库的身份标识
	这里 我把我自己的仓库定义为mikkle
	
	git remote add mikkle http://123@git.123.cn/server/study.git

## 首次提交代码 ##

		进行第一次提交 命令为 git push -u origin master
		origin 为用户默认名,我的用的别名为mikkle,
		master 为主分支
		如果推送到默认的仓库 也可以不使用 -u 参数
		
		git push -u mikkle master  


输入你的密码即可 你也可以使用ssh方式


推送成功


