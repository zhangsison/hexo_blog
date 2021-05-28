---

title: php函数
date: 2015-08-06
categories: [php]
tags: [php函数]

---





## php函数



## php把文本转换成图片



```php

header("Content-type: image/png");

$string = $_GET['text'];

$im= imagecreatefrompng("images/button.png");

$color= imagecolorallocate($im, 255, 255, 255);

$px = (imagesx($im) - 7.5 * strlen($string)) / 2;

$py= 9;

$fontSize= 1;

imagestring($im, fontSize, $px, $py, $string, $color);

imagepng($im);

imagedestroy($im);

?>
```



## php转发数量 ##
```
function tweetCount($url) {
$content = file_get_contents("http://api.tweetmeme.com/url_info?url=".$url);
$element = new SimpleXmlElement($content);
$retweets = $element->story->url_count;
if($retweets){
    return $retweets;
} else {
    return 0;
}
}

语法：
$url= "http://blog.koonk.com";
$count= tweetCount($url);
return $count;
```

## PHP生成随机字符串函数 ##
```
function generateRandomString($length = 10) {
  $characters = '0123456789abcdefghijklmnopqrstuvwxyzABCDEFGHIJKLMNOPQRSTUVWXYZ';
  $randomString = '';
  for ($i = 0; $i < $length; $i++) {
      $randomString .= $characters[rand(0, strlen($characters) - 1)];
  }
  return $randomString;
}
```

## PHP 数组函数 ##



1. 取指定键名

```php
<?php
$raw = ['id' => 1, 'name' => 'zane', 'password' => '123456'];
// 自己用 PHP 实现
function onlyKeys($raw, $keys) {
    $new = [];
    foreach ($raw as $key => $val) {
        if (in_array($key, $keys)) {
            $new[$key] = $val;
        }
    }
    

    return $new;
}
// 用 PHP 内置函数实现
function newOnlyKeys($array, $keys) {
    return array_intersect_key($array, array_flip($keys));
}
var_dump(onlyKeys($raw, ['id', 'name']));
// 结果 ['id' => 1, 'name' => 'zane']
var_dump(newOnlyKeys($raw, ['id', 'name']));
// 结果 ['id' => 1, 'name' => 'zane']

```
```
1. 移除指定键名

<?php
$raw = ['id' => 1, 'name' => 'zane', 'password' => '123456'];
// 用 PHP 内置函数实现
function removeKeys($array, $keys) {
  return array_diff_key($array, array_flip($keys));
}
// 移除 id 键
var_dump(removeKeys($raw, ['id', 'password']));
// 结果 ['name' => 'zane']


3. 数组去重


<?php
$input = ['you are' => 666, 'i am' => 233, 'he is' => 233, 'she is' => 666];
$result = array_unique($input);
var_dump($result);
// 结果 ['you are' => 666, 'i am' => 233]

4. 清除空值

<?php
$input = ['foo', false, -1, null, '', []];
var_dump(array_filter($input));
// 结果 [0 => 'foo', 2 => -1]

5. 数组中重复次数最多的值

<?php
$data = [6, 11, 11, 2, 4, 4, 11, 6, 7, 4, 2, 11, 8];
$cv = array_count_values($data);
// $cv = [6 => 2, 11 => 4, 2 => 2, 4 => 3, 7 => 1, 8 => 1]
arsort($cv);
$max = key($cv);
var_dump($max);
// 结果 11


```

