---

title: 检查文章是否被百度收录
date: 2017-01-08
categories: [php]
tags: [baidu, php]

---


# 检查文章是否被百度收录

网站都有个后台，后台发表新闻与产品，发完后如果你要去查看该页面有没有被百度收录，还要通过第三方工具或直接去百度搜。最近在做SEO，每天都要查看前一天发的文章有没有被收录，就这个工作就是一个很繁琐的工作。所以我在网上找了一段代码，通过地址就可以知道有没有被百度收录，很是方便

```php

function checkBaidu($url) {

    $url= 'http://www.baidu.com/s?wd='. $url;

    $curl= curl_init();

    curl_setopt($curl, CURLOPT_URL, $url);

    curl_setopt($curl, CURLOPT_RETURNTRANSFER, 1);

    $rs= curl_exec($curl);

    curl_close($curl);

    $arr= parse_url($url);

    if(strpos($arr['query'], 'http://')) {

        $arr['query'] = str_replace('http://', '', str_replace('wd=', '', $arr['query']));

    } else{

        $arr['query'] = str_replace('wd=', '', $arr['query']);

    }

    if(strpos($arr['query'], '?')) {

        $str= strstr($arr['query'], '?');

        $arr['query'] = str_replace($str, '', $arr['query']);

    }

    if(strpos($arr['query'], '/')) {

        $narr= explode('/', $arr['query']);

        $arr['query'] = $narr[0];

    }

    if(strpos($rs, ''.$arr['query'].'')) {

        return1;

    } else{

        return0;

    }

}

```