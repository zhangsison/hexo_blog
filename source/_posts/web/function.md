---
title: 常用函数
date: 2020-02-24
categories: [web]
tags: [function]


---



# function



## JS数组对象排序

```
var person = [{name:"Rom",age:12},{name:"Bob",age:22},{name:"Ma",age:5},{name:"Tony",age:25}]

person.sort((a,b)=>{ return a.age-b.age})//升序

person.sort((a,b)=>{ return b.age-a.age})//降序
```

