---
title: "git log"
date: 2015-08-15
categories: [server]
tags: [GitHub]

---




## 如果你在git上提交了错误的commit，不要慌，通过下面的方法可以回退到之前的commit



## git log ##



> 通过git log可以查看我们之前提交的commit_id：


> 复制你需要回滚的commit_id。不过windows下的命令行是不能复制文本的，为此你可以到github上查看仓库的commit历史，上面是可以直接复制的：

![kTQBtA.png](https://s2.ax1x.com/2019/02/27/kTQBtA.png)

复制好后在命令行执行：git reset --hard commit_id



> 执行: git push origin HEAD --force 提交当前HEAD

这样就能够将错误的提交删除，回滚至其之前的代码

但是如果当你回滚代码以后发现commit_id复制错了或者回滚错了怎么办呢？不要慌，按下面的方法做：




> 执行：git reflog

你能在命令行中看到你的历史操作，复制你要恢复操作最前面的hash值
![kTQspt.png](https://s2.ax1x.com/2019/02/27/kTQspt.png)


> 执行 git reset --hard hash

命令中最后要输的hash就是你要恢复的历史记录最前面黄色部分的hash值

比如 git reset --hard 4458e09

