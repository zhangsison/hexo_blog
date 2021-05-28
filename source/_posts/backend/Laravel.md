---

title: Laravel
date: 2017-02-05
categories: [php]
tags: [Laravel]

---

# Laravel


Laravel

artisan 命令

命令说明

php artisan key:generate生成 App Key

php artisan make:controller生成控制器

php artisan make:model生成模型

php artisan make:policy生成授权策略

php artisan make:seeder生成 Seeder 文件

php artisan migrate执行迁移

php artisan migrate:rollback回滚迁移

php artisan migrate:refresh重置数据库

php artisan db:seed填充数据库

php artisan tinker进入 tinker 环境

php artisan route:list查看路由列表

## 运行原理概述

Laravel 框架的入口文件 index.php

1、引入自动加载 autoload.php 文件

2、创建应用实例，并同时完成了

```
基本绑定($this、容器类Container等等)、

基本服务提供者的注册（Event、log、routing）、

核心类别名的注册(比如db、auth、config、router等)
```
3、开始 Http 请求的处理
```
make 方法从容器中解析指定的值为实际的类，比如 $app->make(Illuminate\Contracts\Http\Kernel::class); 解析出来 App\Http\Kernel 

handle 方法对 http 请求进行处理

实际上是 handle 中 sendRequestThroughRouter 处理 http 的请求

首先，将 request 绑定到共享实例

然后执行 bootstarp 方法，运行给定的引导类数组 $bootstrappers，这里是重点，包括了加载配置文件、环境变量、服务提供者、门面、异常处理、引导提供者等

之后，进入管道模式，经过中间件的处理过滤后，再进行用户请求的分发

在请求分发时，首先，查找与给定请求匹配的路由，然后执行 runRoute 方法，实际处理请求的时候 runRoute 中的 runRouteWithinStack 

最后，经过 runRouteWithinStack 中的 run 方法，将请求分配到实际的控制器中，执行闭包或者方法，并得到响应结果
```