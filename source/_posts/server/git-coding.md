---

title: GitHub和Coding同步的方法
date: 2016-06-10
categories: [server]
tags: [git,Coding]

---



# GitHub和Coding同步的方法

## win
> /c/Users/Administrator/.ssh/id_rsa

## mac
> cd /.ssh

复制秘钥到git和coding生成新的秘钥即可



# 远程仓库

## 关联GitHub远程库

这里我用的是 SSH 的方式，至于如何管理并配置 SSH，你可以参考这里

注意，远程库的名称叫 github，不叫 origin 了！

> git remote add github git@github.com:jpdaka.git

## 关联Coding远程库

同样注意，远程库的名称叫 coding，不叫 origin 了！

> git remote add coding git@e.coding.net:jpdaka/test.git

现在，我们用 git remote -v 查看远程库信息，可以看到两个远程库

```git
git add .
git commit -m "First commit"
```


## push到远程仓库

如果要 push 到 GitHub，使用命令：

> git push github master

如果要 push 到 Coding，使用命令：

> git push coding master




# 获取自己的GitHubpages地址对应的IP

> 配置域名解析添加两条A解析记录，主机名分别是@和www
对应值填写更改获取到的IP
## Coding

> 配置域名解析
添加两条cname解析记录，主机名分别是@和www
对应值填写更改获取到的IP
绑定域名
这样就可以同步两边的内容了


> ssh-keygen -t rsa -C 你的邮箱
git config -l 查看配置 
运行ssh-keygen -t rsa 查看配置