---

title: php检查文章是否被百度收录
date: 2017-01-08
categories: [php]
tags: [baidu, php]

---


# php检查文章是否被百度收录



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