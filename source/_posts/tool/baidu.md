---
title: 搜索技巧
date: 2020-06-07
categories: [tool]
tags: [百度, seo]


---



# 百度搜索



## 搜索方式可复合使用 



1.去广告搜索：intitle:（关键词）



2.搜索文件：（关键词）filetype:（文件类型）

* 常见文件类型->〔pdf〕PDF文件 , xls, ppt, doc, txt

  

3.关键词包含在正文中 : intext:（关键词）



4.限定搜索网站:（关键词）inurl:（网站类型）

* 常见网站类型 com net edu

  

5.限定搜索时间 : 2018..2019   如需搜索2018-2019年



![百度搜索](https://i.loli.net/2021/06/05/EbrYaOWhj6dkKJz.png)



5.使用引号强制精确匹配

如：`"what is javascript"`



6.单个站点内进行搜索

如：`site:freecodecamp.org`   关键词



7.shodan语法

country:"CN" 搜索指定的国家

org:"google" 搜索指定的组织或公司

isp:"China Telecom" 搜索指定的ISP供应商

version:"1.6.2" 搜索指定的软件版本



8.搜索被链接的目标

“`link:`”，搜索所有链接到该网址的页面

## github搜索语法

### 常用词含义

> +   watch：会持续收到该项目的动态
> +   fork：复制某个仓库到自己的Github仓库中
> +   star：可以理解为点赞
> +   clone：将项目下载至本地
> +   follow：关注你感兴趣的作者，会收到他们的动态

> 搜索 GitHub 时，可以构建匹配特定数字和单词的查询。

### 查询大于或小于另一个值的值

> 可以使用 >、>=、< 和 <= 搜索大于、大于等于、小于以及小于等于另一个值的值。

| 查询 | 示例                                                                           |
| ---- | ------------------------------------------------------------------------------ |
| \>n  | spring-boot stars:>2000 匹配含有 "spring-boot" 字样、星标超过 1000 个的仓库。  |
| \>=n | spring-boot topics:>=5 匹配含有 "spring-boot" 字样、有 5 个或更多主题的仓库。  |
| <n   | spring-boot size:<10000 匹配小于 10 KB 的文件中含有 "spring-boot" 字样的代码。 |
| <=n  | spring-boot stars:<=50 匹配含有 "spring-boot" 字样、星标不超过 50 个的仓库。   |

> 还可以使用范围查询搜索大于等于或小于等于另一个值的值。

| 查询  | 示例                                                                                                       |
| ----- | ---------------------------------------------------------------------------------------------------------- |
| n..\* | spring-boot stars:5000..\* 等同于 stars:>=5000 并匹配含有 "spring-boot" 字样、有 5000 个或更多星号的仓库。 |
| \*..n | spring-boot stars:\*..20 等同于 stars:<=20 并匹配含有 "spring-boot" 字样、有不超过 20 个星号的仓库。       |

### 查询日期

> 可以通过使用 >、>=、<、<= 和范围查询搜索早于或晚于另一个日期，或者位于日期范围内的日期。 日期格式必须遵循 ISO8601标准，即 YYYY-MM-DD（年-月-日）。

| 查询                   | 示例                                                                                                          |
| ---------------------- | ------------------------------------------------------------------------------------------------------------- |
| \>YYYY-MM-DD           | spring-boot created:>2016-04-29 匹配含有 "spring-boot" 字样、在 2016 年 4 月 29 日之后创建的议题。            |
| \>=YYYY-MM-DD          | spring-boot created:>=2017-04-01 匹配含有 "spring-boot" 字样、在 2017 年 4 月 1 日或之后创建的议题。          |
| <YYYY-MM-DD            | spring-boot pushed:<2012-07-05 匹配在 2012 年 7 月 5 日之前推送的仓库中含有 "spring-boot" 字样的代码。        |
| <=YYYY-MM-DD           | spring-boot created:<=2012-07-04 匹配含有 "spring-boot" 字样、在 2012 年 7 月 4 日或之前创建的议题。          |
| YYYY-MM-DD..YYYY-MM-DD | spring-boot pushed:2016-04-30..2016-07-04 匹配含有 "spring-boot" 字样、在 2016 年 4 月末到 7 月之间推送的仓库 |
| YYYY-MM-DD..\*         | spring-boot created:2012-04-30..\* 匹配在 2012 年 4 月 30 日之后创建、含有 "spring-boot" 字样的议题。         |
| \*..YYYY-MM-DD         | spring-boot created:\*..2012-07-04 匹配在 2012 年 7 月 4 日之前创建、含有 "spring-boot" 字样的议题。          |

### 排除特定结果

> 可以使用 `NOT 语法`排除包含特定字词的结果。 `NOT 运算符只能用于字符串关键词`， `不适用于数字或日期`。

| 查询 | 示例                                                               |
| ---- | ------------------------------------------------------------------ |
| NOT  | hello NOT world 匹配含有 "hello" 字样但不含有 "world" 字样的仓库。 |

### 使用用户名的查询

> 如果搜索查询包含`需要用户名`的限定符，例如 `user`、`actor` 或 `assignee`，您可以使用任何 GitHub 用户名指定特定人员，或使用 `@me` 指定当前用户。

| 查询               | 示例                                               |
| ------------------ | -------------------------------------------------- |
| QUALIFIER:USERNAME | author:nat 匹配 @nat 创作的提交。                  |
| QUALIFIER:@me      | is:issue assignee:@me 匹配已分配给结果查看者的议题 |

> @me 只能与限定符一起使用，而不能用作搜索词，例如 @me main.workflow。


### 按仓库名称、说明或自述文件内容搜索

> 通过 `in` 限定符，您可以将搜索限制为`仓库名称`、`仓库说明`、`自述文件内容`或这些的`任意组合`。 如果省略此限定符，则只搜索`仓库名称和说明`。

| 限定符          | 示例                                                                  |
| --------------- | --------------------------------------------------------------------- |
| in:name         | seckill in:name 匹配仓库名称中含有 "seckill" 的仓库。                 |
| in:description  | seckill in:name,description 匹配仓库名称或说明中含有 "seckill" 的仓库 |
| in:readme       | seckill in:readme 匹配仓库自述文件中提及 "seckill" 的仓库。           |
| repo:owner/name | repo:codingXiaxw/seckill 匹配特定仓库名称。                           |

### 按主题搜索

> 可以找到按特定主题分类的所有仓库。

| 限定符      | 示例                                           |
| ----------- | ---------------------------------------------- |
| topic:TOPIC | topic:jekyll匹配已归类为 "jekyll" 主题的仓库。 |


### 按仓库可见性搜索

> 可以根据`仓库的可见性`过滤搜索。

| 限定符      | 示例                                                             |
| ----------- | ---------------------------------------------------------------- |
| is:public   | is:public org:github 匹配 GitHub 拥有的公共仓库。                |
| is:internal | is:internal test 匹配您可以访问并且包含单词 "test" 的内部仓库。  |
| is:private  | is:private pages 匹配您可以访问并且包含单词 "pages" 的私有仓库。 |

> **推荐一个很好用的GitHub chrome插件：** `Octotree`

![19.gif](https://p6-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/520d26792ea54bcaae765fda6b394957~tplv-k3u1fbpfcp-watermark.image)