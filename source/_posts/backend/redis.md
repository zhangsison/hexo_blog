---

title: redis
date: 2017-12-10
categories: [php]
tags: [redis]

---


# redis启动 
redis 支持多种类型的数据结构，常用的有 5 种 ，分别是 strings，hashes， lists， sets，sorted sets

```
- 本地启动：redis-cli

- 远程启动：redis-cli -h host -p port -a password

- 前端启动的关闭 强制关闭 ctrl+c 正常关闭 ./redis-cli shutdown

- **PING**
- 查看服务是否运行

- **QUIT** 
- 关闭当前连接

- **SELECT index** 
- 切换到指定的数据库

## 数据类型 ##
**String 类型**

赋值 set key value

127.0.0.1:6379> set test 123
OK

取值 get key

127.0.0.1:6379> get test
"123"

复制代码取值并赋值 getset key value

127.0.0.1:6379> getset test 321
"123"
127.0.0.1:6379> get test
"321"

设置获取多个键值

mset key value [key value...]
mget key [key...]

127.0.0.1:6379> mset k1 v1 k2 v2 k3 v3
OK
127.0.0.1:6379> mget k1 k2
1) "v1"
2) "v2"

删除 del key

127.0.0.1:6379> del test
(integer) 1

获取 redis 中所有的 key 可用使用 *
查找以 w3c 为开头的 key：

127.0.0.1:6379> KEYS w3c*
1. "w3c3"
2. "w3c1"
3. "w3c2"


递增数字
当存储的字符串是整数时，Redis提供了一个实用的命令INCR，其作用是让当前键值递增，并返回递增后的值。

语法：incr 

key127.0.0.1:6379> set num 1
OK
127.0.0.1:6379> incr num
(integer) 2
127.0.0.1:6379> incr num
(integer) 3
127.0.0.1:6379> incr num
(integer) 4

增加指定的整数
incrby key increment

127.0.0.1:6379> incrby num 2
(integer) 4
127.0.0.1:6379> incrby num 2
(integer) 6

递减数值

decr key

127.0.0.1:6379> decr num
(integer) 10
127.0.0.1:6379> decr num
(integer) 9

减少指定的数值

decryby key 

decrement127.0.0.1:6379> decrby num 2
(integer) 6
127.0.0.1:6379> decrby num 2
(integer) 4

向尾部追加值 APPEND的作用是向键值的末尾追加value
如果键不存在则将该键的值设置为value，即相当于 SET key value

127.0.0.1:6379> set str www
OK
127.0.0.1:6379> append str "qqq"
(integer) 10
127.0.0.1:6379> get str
"wwwqqq"

获取字符串长度 STRLEN

127.0.0.1:6379> strlen str
(integer) 6


## Hash 散列类型 ##

Redis hash 是一个string类型的field和value的映射表，hash特别适合用于存储对象。
Redis 中每个 hash 可以存储 232 - 1 键值对（40多亿）。


一次只设置一个字段值
语法：hset key field value
127.0.0.1:6379> hset user username zhangsan
(integer) 1

一次设置多个字段值
语法：hmset key field value [field value...]
127.0.0.1:6379> hmset user age 20 username lisi
OK

**获取hash值**

一次获取一个字段值

语法：hget key field
127.0.0.1:6379> hget user username
"lisi"

一次可以获取多个字段值

语法：hmget key field [field...]
127.0.0.1:6379> hmget user age username
1. "20"
2. "lisi"

获取所有字段值

语法：hgetall key127.0.0.1:6379> hgetall user
1. "username"
2. "lisi"
3. "age"
4. "20"

删除字段 可以删除一个或多个字段 
语法：hdel key field [field...]

127.0.0.1:6379> hdel user age
(integer) 1
127.0.0.1:6379> hdel user age username
(integer) 1

增加数字语法：hincrby key field increment
127.0.0.1:6379> hincrby user age 2
(integer) 2

复制代码判断字段是否存在语法：hexists key field
127.0.0.1:6379> hexists user age
(integer) 1


获取字段数量 语法：hlen key

127.0.0.1:6379> hlen user
(integer) 1

获取信息

127.0.0.1:6379> hgetall items:1001
1. "id"
2. "3"
3. "name"
4. "apple"
5. "price"
6. "5.00"

```


## Redis的回收策略 ##

volatile-lru：从已设置过期时间的数据集（server.db[i].expires）中挑选最近最少使用的数据淘汰

volatile-ttl：从已设置过期时间的数据集（server.db[i].expires）中挑选将要过期的数据淘汰

volatile-random：从已设置过期时间的数据集（server.db[i].expires）中任意选择数据淘汰

allkeys-lru：从数据集（server.db[i].dict）中挑选最近最少使用的数据淘汰

allkeys-random：从数据集（server.db[i].dict）中任意选择数据淘汰

no-enviction（驱逐）：禁止驱逐数据


## Redis 持久化 ##

Redis 提供了多种不同级别的持久化方式：

RDB 持久化可以在指定的时间间隔内生成数据集的时间点快照（point-in-time snapshot）。
AOF 持久化记录服务器执行的所有写操作命令，并在服务器启动时，通过重新执行这些命令来还原数据集。 AOF 文件中的命令全部以 Redis 协议的格式来保存，新命令会被追加到文件的末尾。 Redis 还可以在后台对 AOF 文件进行重写（rewrite），使得 AOF 文件的体积不会超出保存数据集状态所需的实际大小。
Redis 还可以同时使用 AOF 持久化和 RDB 持久化。 在这种情况下， 当 Redis 重启时， 它会优先使用 AOF 文件来还原数据集， 因为 AOF 文件保存的数据集通常比 RDB 文件所保存的数据集更完整。
你甚至可以关闭持久化功能，让数据只在服务器运行时存在。

