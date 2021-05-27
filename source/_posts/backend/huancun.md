---

title: 全页面静态化缓存
date: 2015-08-06
categories: [php]
tags: [cacha]

---




## 全页面静态化缓存



#### 页面部分缓存

该种方式，是将一个页面中不经常变的部分进行静态缓存，而经常变化的块不缓存，最后组装在一起显示；可以使用类似于ob_get_contents的方式实现

#### 数据缓存

当用商品id去请求时，就会得出包括店铺信息、商品信息等数据，此时就可以将这些数据缓存到一个php文件中，文件名包含商品id来建一个唯一标示；下一 次有人想查看这个商品时，首先就直接调这个文件里面的信息，而不用再去数据库查询；其实缓存文件中缓存的就是一个php数组之类；

#### 查询缓存

将查询得到的数据缓存在一个文件中，下次遇到相同的查询时，就直接先从这个文件里面调数据，不会再去查数据库；但此处的缓存文件名可能就需要以查询语句为基点来建立唯一标示

#### 按内容变更进行缓存

这个也并非独立的缓存技术，需结合着用；就是当数据库内容被修改时，即刻更新缓存文件

#### 内存式缓存

提到这个，可能大家想到的首先就是Memcached；memcached是高性能的分布式内存缓存服务器。 一般的使用目的是，通过缓存数据库查询结果，减少数据库访问次数，以提高动态Web应用的速度、 提高可扩展性。

它就是将需要缓存的信息，缓存到系统内存中，需要获取信息时，直接到内存中取；比较常用的方式就是 key–>value方式；

```php
 $memcachehost ='192.168.6.191';   $memcacheport =11211;    $memcachelife =60;    

 $memcache =newMemcache;    

  $memcache->connect($memcachehost,$memcacheport)ordie("Could not connect");    

  $memcache->set('key','缓存的内容');    

  $get = $memcache->get($key);  
  ```

#### apache缓存模块

apache安装完以后，是不允许被cache的。如果外接了cache或squid服务器要求进行web加速的话，就需要在htttpd.conf里进行设置，当然前提是在安装apache的时候要激活mod_cache的模块。

安装apache时：./configure –enable-cache –enable-disk-cache –enable-mem-cache

#### php APC缓存扩展

Php有一个APC缓存扩展，windows下面为php_apc.dll，需要先加载这个模块，然后是在php.ini里面进行配置

```php

[apc]    

 extension=php_apc.dll

     apc.rfc1867 = on
    
     upload_max_filesize =100M  
    
    post_max_size =100M  

   apc.max_file_size =200M    

  upload_max_filesize =1000M    

  post_max_size =1000M    

  max_execution_time =600;  
  ```

 每个PHP页面运行的最大时间值(秒)，默认30秒    

 max_input_time =600;  

    每个PHP页面接收数据所需的最大时间，默认60      memory_limit =128M;    

  每个PHP页面所吃掉的最大内存，默认8M

#### Opcode缓存

比较知名的是XCache、Turck MM Cache、PHP Accelerator等