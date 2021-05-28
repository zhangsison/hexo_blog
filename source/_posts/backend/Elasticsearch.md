---

title: Elasticsearch
date: 2019-12-09
featuredImage: "/images/server.jpg"
categories: [php]
tags: [Elasticsearch]

---


# 资料文档

```bash

- 中文版的

https://es.xiaoleilu.com/  

- 英文版的

https://www.elastic.co/guide/en/elasticsearch/reference/current/index.html 

- 中文版的

https://es.xiaoleilu.com/  

- Elasticsearch-PHP

https://www.elastic.co/guide/cn/elasticsearch/php/current/_quickstart.html#_quickstart

- 全文搜索引擎 Elasticsearch 入门教程
https://www.ruanyifeng.com/blog/2017/08/elasticsearch.html

- Elasticsearch-PHP 中文文档
https://learnku.com/docs/elasticsearch-php/6.0

```


# 安装并运行Elasticsearch

安装 Elasticsearch 之前，你需要先安装一个较新版本的 Java，最好的选择是，你可以从 www.java.com 获得官方提供的最新版本的Java。
你可以从 elastic 的官网 elastic.co/downloads/elasticsearch 获取最新版本的Elasticsearch。解压文档后，按照下面的操作，即可在前台(foregroud)启动 Elasticsearch：

> cd elasticsearch
> 
> ./bin/elasticsearch

此时，Elasticsearch运行在本地的9200端口，在浏览器中输入网址“http://localhost:9200/”，如果看到以下信息就说明你的电脑已成功安装Elasticsearch：


```bash
{
  "name" : "YTK8L4q",
  "cluster_name" : "elasticsearch",
  "cluster_uuid" : "hB2CZPlvSJavhJxx85fUqQ",
  "version" : {
    "number" : "6.5.4",
    "build_flavor" : "default",
    "build_type" : "tar",
    "build_hash" : "d2ef93d",
    "build_date" : "2018-12-17T21:17:40.758843Z",
    "build_snapshot" : false,
    "lucene_version" : "7.5.0",
    "minimum_wire_compatibility_version" : "5.6.0",
    "minimum_index_compatibility_version" : "5.0.0"
  },
  "tagline" : "You Know, for Search"
}

```

# Kibana
Kibana 是一个开源的分析和可视化平台，旨在与 Elasticsearch 合作。Kibana 提供搜索、查看和与存储在 Elasticsearch 索引中的数据进行交互的功能。开发者或运维人员可以轻松地执行高级数据分析，并在各种图表、表格和地图中可视化数据。
  你可以从 elastic 的官网 https://www.elastic.co/downloads/kibana 获取最新版本的Kibana

