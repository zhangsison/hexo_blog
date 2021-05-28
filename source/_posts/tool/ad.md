---

title: ApacheBench 测压工具
date: 2016-09-07
categories: [tool]
tags: [ApacheBench , ad]

---

# ApacheBench  #

输入 ab -n 100 -c 20 http://localhost:8080/（-n发出100个请求，-c模拟20并发，相当100人同时访问，后面是测试url）

输入 ab -n 100 -c 20 http://localhost:8080/test?str=AA （传入一个参数）

输入 ab -t 60 -c 20 http://localhost:8080/index.html （ 在60秒内发请求，一次20个请求）

