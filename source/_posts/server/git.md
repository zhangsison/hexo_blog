---

title: git
date: 2015-08-08
categories: [server]
tags: [git]

---







## 一、新建代码库 ##


    # 在当前目录新建一个Git代码库
    $ git init
    
    # 新建一个目录，将其初始化为Git代码库
    $ git init [project-name]
    
    # 下载一个项目和它的整个代码历史
    $ git clone [url]

## 二、配置 ##

Git的设置文件为.gitconfig，它可以在用户主目录下（全局配置），也可以在项目目录下（项目配置）。


    # 显示当前的Git配置
    $ git config --list
    
    # 编辑Git配置文件
    $ git config -e [--global]
    
    # 设置提交代码时的用户信息
    $ git config [--global] user.name "[name]"
    $ git config [--global] user.email "[email address]"

## 三、增加/删除文件 ##


    # 添加指定文件到暂存区
    $ git add [file1] [file2] ...
    
    # 添加指定目录到暂存区，包括子目录
    $ git add [dir]
    
    # 添加当前目录的所有文件到暂存区
    $ git add .
    
    # 添加每个变化前，都会要求确认
    # 对于同一个文件的多处变化，可以实现分次提交
    $ git add -p
    
    # 删除工作区文件，并且将这次删除放入暂存区
    $ git rm [file1] [file2] ...
    
    # 停止追踪指定文件，但该文件会保留在工作区
    $ git rm --cached [file]
    
    # 改名文件，并且将这个改名放入暂存区
    $ git mv [file-original] [file-renamed]

## 四、代码提交 ##


    # 提交暂存区到仓库区
    $ git commit -m [message]
    
    # 提交暂存区的指定文件到仓库区
    $ git commit [file1] [file2] ... -m [message]
    
    # 提交工作区自上次commit之后的变化，直接到仓库区
    $ git commit -a
    
    # 提交时显示所有diff信息
    $ git commit -v
    
    # 使用一次新的commit，替代上一次提交
    # 如果代码没有任何新变化，则用来改写上一次commit的提交信息
    $ git commit --amend -m [message]
    
    # 重做上一次commit，并包括指定文件的新变化
    $ git commit --amend [file1] [file2] ...

## 五、分支 ##


    # 列出所有本地分支
    $ git branch
    
    # 列出所有远程分支
    $ git branch -r
    
    # 列出所有本地分支和远程分支
    $ git branch -a
    
    # 新建一个分支，但依然停留在当前分支
    $ git branch [branch-name]
    
    # 新建一个分支，并切换到该分支
    $ git checkout -b [branch]
    
    # 新建一个分支，指向指定commit
    $ git branch [branch] [commit]
    
    # 新建一个分支，与指定的远程分支建立追踪关系
    $ git branch --track [branch] [remote-branch]
    
    # 切换到指定分支，并更新工作区
    $ git checkout [branch-name]
    
    # 切换到上一个分支
    $ git checkout -
    
    # 建立追踪关系，在现有分支与指定的远程分支之间
    $ git branch --set-upstream [branch] [remote-branch]
    
    # 合并指定分支到当前分支
    $ git merge [branch]
    
    # 选择一个commit，合并进当前分支
    $ git cherry-pick [commit]
    
    # 删除分支
    $ git branch -d [branch-name]
    
    # 删除远程分支
    $ git push origin --delete [branch-name]
    $ git branch -dr [remote/branch]

## 六、标签 ##


    # 列出所有tag
    $ git tag
    
    # 新建一个tag在当前commit
    $ git tag [tag]
    
    # 新建一个tag在指定commit
    $ git tag [tag] [commit]
    
    # 删除本地tag
    $ git tag -d [tag]
    
    # 删除远程tag
    $ git push origin :refs/tags/[tagName]
    
    # 查看tag信息
    $ git show [tag]
    
    # 提交指定tag
    $ git push [remote] [tag]
    
    # 提交所有tag
    $ git push [remote] --tags
    
    # 新建一个分支，指向某个tag
    $ git checkout -b [branch] [tag]

## 七、查看信息 ##


    # 显示有变更的文件
    $ git status
    
    # 显示当前分支的版本历史
    $ git log
    
    # 显示commit历史，以及每次commit发生变更的文件
    $ git log --stat
    
    # 搜索提交历史，根据关键词
    $ git log -S [keyword]
    
    # 显示某个commit之后的所有变动，每个commit占据一行
    $ git log [tag] HEAD --pretty=format:%s
    
    # 显示某个commit之后的所有变动，其"提交说明"必须符合搜索条件
    $ git log [tag] HEAD --grep feature
    
    # 显示某个文件的版本历史，包括文件改名
    $ git log --follow [file]
    $ git whatchanged [file]
    
    # 显示指定文件相关的每一次diff
    $ git log -p [file]
    
    # 显示过去5次提交
    $ git log -5 --pretty --oneline
    
    # 显示所有提交过的用户，按提交次数排序
    $ git shortlog -sn
    
    # 显示指定文件是什么人在什么时间修改过
    $ git blame [file]
    
    # 显示暂存区和工作区的代码差异
    $ git diff
    
    # 显示暂存区和上一个commit的差异
    $ git diff --cached [file]
    
    # 显示工作区与当前分支最新commit之间的差异
    $ git diff HEAD
    
    # 显示两次提交之间的差异
    $ git diff [first-branch]...[second-branch]
    
    # 显示今天你写了多少行代码
    $ git diff --shortstat "@{0 day ago}"
    
    # 显示某次提交的元数据和内容变化
    $ git show [commit]
    
    # 显示某次提交发生变化的文件
    $ git show --name-only [commit]
    
    # 显示某次提交时，某个文件的内容
    $ git show [commit]:[filename]
    
    # 显示当前分支的最近几次提交
    $ git reflog
    
    # 从本地master拉取代码更新当前分支：branch 一般为master
    $ git rebase [branch]

## 八、远程同步 ##


    # 下载远程仓库的所有变动
    $ git fetch [remote]
    
    # 显示所有远程仓库
    $ git remote -v
    
    # 显示某个远程仓库的信息
    $ git remote show [remote]
    
    # 增加一个新的远程仓库，并命名
    $ git remote add [shortname] [url]
    
    # 取回远程仓库的变化，并与本地分支合并
    $ git pull [remote] [branch]
    
    # 上传本地指定分支到远程仓库
    $ git push [remote] [branch]
      git push -u origin master
    
    # 强行推送当前分支到远程仓库，即使有冲突
    $ git push [remote] --force
    
    # 推送所有分支到远程仓库
    $ git push [remote] --all

## 九、撤销 ##


    # 恢复暂存区的指定文件到工作区
    $ git checkout [file]
    
    # 恢复某个commit的指定文件到暂存区和工作区
    $ git checkout [commit] [file]
    
    # 恢复暂存区的所有文件到工作区
    $ git checkout .
    
    # 重置暂存区的指定文件，与上一次commit保持一致，但工作区不变
    $ git reset [file]
    
    # 重置暂存区与工作区，与上一次commit保持一致
    $ git reset --hard
    
    # 重置当前分支的指针为指定commit，同时重置暂存区，但工作区不变
    $ git reset [commit]
    
    # 重置当前分支的HEAD为指定commit，同时重置暂存区和工作区，与指定commit一致
    $ git reset --hard [commit]
    
    # 重置当前HEAD为指定commit，但保持暂存区和工作区不变
    $ git reset --keep [commit]
    
    # 新建一个commit，用来撤销指定commit
    # 后者的所有变化都将被前者抵消，并且应用到当前分支
    $ git revert [commit]
    
    # 暂时将未提交的变化移除，稍后再移入
    $ git stash
    $ git stash pop

## 十、 版本退回 ##
     git log退出方法 
     英文状态下按Q
    如果嫌输出信息太多，看得眼花缭乱的，可以试试加上--pretty=oneline参数：git log --pretty=oneline
    git reset --hard origin/master 
    重新退回最新的版本 git reflog
    Git提供了一个命令git reflog用来记录你的每一次命令

## 十一、 解决冲突 ##

我们可以直接查看冲突文件的内容：

	Git is a distributed version control system.
	Git is free software distributed under the GPL.
	Git has a mutable index called stage.
	Git tracks changes of files.
	<<<<<<< HEAD
	Creating a new branch is quick & simple.
	=======
	Creating a new branch is quick AND simple.
	>>>>>>> feature1
	
	Git用<<<<<<<，=======，>>>>>>>标记出不同分支的内容，我们修改如下后保存：
	
	Creating a new branch is quick and simple.
	
	再提交就ok了

## 十二、搭建Git服务器 ##

	第一步，安装git：
	
	$ sudo apt-get install git
	
	第二步，创建一个git用户，用来运行git服务：
	
	$ sudo adduser git
	
	第三步，创建证书登录：
	
	收集所有需要登录的用户的公钥，就是他们自己的id_rsa.pub文件，把所有公钥导入到/home/git/.ssh/authorized_keys文件里，一行一个。
	
	第四步，初始化Git仓库：
	
	先选定一个目录作为Git仓库，假定是/srv/sample.git，在/srv目录下输入命令：
	
	$ sudo git init --bare sample.git
	
	Git就会创建一个裸仓库，裸仓库没有工作区，因为服务器上的Git仓库纯粹是为了共享，所以不让用户直接登录到服务器上去改工作区，并且服务器上的Git仓库通常都以.git结尾。然后，把owner改为git：
	
	$ sudo chown -R git:git sample.git
	
	第五步，禁用shell登录：
	
	出于安全考虑，第二步创建的git用户不允许登录shell，这可以通过编辑/etc/passwd文件完成。找到类似下面的一行：
	
	git:x:1001:1001:,,,:/home/git:/bin/bash
	
	改为：
	
	git:x:1001:1001:,,,:/home/git:/usr/bin/git-shell
	
	这样，git用户可以正常通过ssh使用git，但无法登录shell，因为我们为git用户指定的git-shell每次一登录就自动退出。
	
	第六步，克隆远程仓库：
	
	现在，可以通过git clone命令克隆远程仓库了，在各自的电脑上运行：
	
	$ git clone git@server:/srv/sample.git
	Cloning into 'sample'...
	warning: You appear to have cloned an empty repository.
	
	管理公钥
	
	如果团队很小，把每个人的公钥收集起来放到服务器的/home/git/.ssh/authorized_keys文件里就是可行的。如果团队有几百号人，就没法这么玩了，这时，可以用Gitosis来管理公钥
	
	管理权限
	Gitolite这个工具





git init

git add .

git commit -m

添加远程推送地址
git remote add origin https://github.com/zhangsison/chongdianbao

git push -u origin master

git clone

git status -s

缺少README.md

git pull --rebase origin master

删除文件

git rm --cached filename

git add .

git commit -m "提交的信息"

git remote add origin 远程仓库地址

失败先删除远程 Git 仓库  git remote rm origin

git push -u origin 分支名

新建分支

git branch 分支名

切换分支

git checkout 分支名

git查看远程仓库地址命令：

git remote -v

添加所以含txt文件  git add *.txt

撤销1.2个文件          git checkout head wewe.txt

撤销所有txt文件        git checkout head *.txt

撤销所以文件            git checkout head

列出所有本地分支git branch列出所有远程分支git branch -r列出所有本地分支和远程分支git branch -a新建一个分支，但依然停留在当前分支git branch [branch-name]

从远程库获取  git pull origin  git fetch origin

直接从暂存区删除文件，工作区则不做出改变git rm --cached

查看文件修改后的差异git diff [files]

git config --system--list#查看当前用户（global）配置git config --global  --list#查看当前仓库配置信息git config --local--list

设置Git的user name和email：

$ git config --global user.name "xuhaiyan"

$ git config --global user.email "haiyan.xu.vip@gmail.com"

设置秘钥

$ ssh-keygen -t rsa -C “email@email.com”

cd : 改变目录。

cd . . 回退到上一个目录，直接cd进入默认目录

pwd : 显示当前所在的目录路径。

ls(ll): 都是列出当前目录中的所有文件，只不过ll(两个ll)列出的内容更为详细。

touch : 新建一个文件 如 touch index.js 就会在当前目录下新建一个index.js文件。

rm: 删除一个文件, rm index.js 就会把index.js文件删除。

mkdir: 新建一个目录,就是新建一个文件夹。

rm -r : 删除一个文件夹, rm -r src 删除src目录， 好像不能用通配符。

mv 移动文件, mv index.html src index.html

reset 重新初始化终端/清屏。

clear 清屏。

history 查看命令历史。

help 帮助。

exit 退出。

