---

title: php函数
date: 2015-12-04
categories: [php]
tags: [php图片]

---





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



