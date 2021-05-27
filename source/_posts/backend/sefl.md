---

title: self
date: 2015-12-18
categories: [php]
tags: [php函数]

---


## php安全函数 ##



## mysql_real_escape_string() ##

这个函数在PHP中防止SQL注入攻击时很实用。这个函数会对一些比如单引號、双引號、反斜杠等特殊字符加入一个反斜杠以确保在查询这些数据之前，用户提供的输入是干净的。但要注意。你是在连接数据库的前提下使用这个函数。

可是如今已经不推荐使用mysql_real_escape_string()了，全部新的应用应该使用像PDO一样的函数库运行数据库操作，也就是说。我们能够使用现成的语句防止SQL注入攻击。

## addslashes() ##

这个函数的原理跟mysql_real_escape_string()相似。可是当在php.ini文件里，“magic_quotes_gpc“的值是“on”的时候，就不要使用这个函数。magic_quotes_gpc 的默认值是on。对全部的 GET、POST 和 COOKIE 数据自己主动执行 addslashes()。不要对已经被 magic_quotes_gpc 转义过的字符串使用 addslashes()。由于这样会导致双层转义。你能够使用get_magic_quotes_gpc()函数来确定它是否开启。

## htmlentities() ##

这个函数对于过滤用户输入的数据很实用。

它会将一些特殊字符转换为HTML实体。比如，用户输入<时，就会被该函数转化为HTML实体<（&lt）。输入>就被转为实体&gt.(HTML实体对比表：http://www.w3school.com.cn/html/html_entities.asp)。能够防止XSS和SQL注入攻击。

## htmlspecialchars() ##

在HTML中。一些特定字符有特殊的含义，假设要保持字符原来的含义，就应该转换为HTML实体。这个函数会返回转换后的字符串，比如‘&’ (ampersand) 转为’&amp‘

## strip_tags() ##

去除字符串中全部的HTML，JavaScript和PHP标签

## md5() ##

md5()函数能够产生给定字符串的32个字符的md5散列。并且这个过程不可逆，即你不能从md5()的结果得到原始字符串。

## sha1() ##

这个函数与md5()类似，可是它使用了不同的算法来产生40个字符的SHA-1散列（md5产生的是32个字符的散列）。也不要把绝对安全寄托在这个函数上，否则会有意想不到的结果。

## intval() ##

intval()函数是将变量转成整数类型，你能够用这个函数让你的PHP代码更安全，特别是当你在解析id，年龄这种数据时。