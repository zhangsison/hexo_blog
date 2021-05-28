---

title: travis-ci
date: 2019-08-30
categories: [server]
tags: [travis-ci]

---

Travis CI 提供的是持续集成服务（Continuous Integration，简称 CI）。它绑定 Github 上面的项目，只要有新的代码，就会自动抓取。然后，提供一个运行环境，执行测试，完成构建，还能部署到服务器。

持续集成指的是只要代码有变更，就自动运行构建和测试，反馈运行结果。确保符合预期以后，再将新代码"集成"到主干。

持续集成的好处在于，每次代码的小幅变更，就能看到运行结果，从而不断累积小的变更，而不是在开发周期结束时，一下子合并一大块代码。

## travis-ci

- 获取 travis-ci 项目的 ID 跟 slug
- https://api.travis-ci.org/owner/zhangsison/repos


![](https://i.loli.net/2019/12/12/If2npYciqNCgdPK.png)


## .travis.yml

Travis 要求项目的根目录下面，必须有一个.travis.yml文件。这是配置文件，指定了 Travis 的行为。该文件必须保存在 Github 仓库里面，一旦代码仓库有新的 Commit，Travis 就会去找这个文件，执行里面的命令

## Travis 的运行流程都会经过两个阶段

- install 阶段：安装依赖
- script 阶段：运行脚本

通过命令构建项目，本地构建完成复制流程命令，放到构建命令中
