---

title: php获取访问者浏览器
date: 2015-12-06
categories: [php]
tags: [php]

---



# 获取访问者浏览器

```php


	functionbrowse_infor() {
		$browser = "";
		$browserver = "";
		$Browsers = array("Lynx", "MOSAIC", "AOL", "Opera", "JAVA", "MacWeb", "WebExplorer", "OmniWeb");
		$Agent = $GLOBALS["HTTP_USER_AGENT"];
		for ($i = 0; $i <= 7; $i++) {
			if (strpos($Agent, $Browsers[$i])) {
				$browser = $Browsers[$i];
				$browserver = ""
			}
		}
		if (ereg("Mozilla", $Agent) && !ereg("MSIE", $Agent)) {
			$temp = explode("(", $Agent);
			$Part = $temp[0];
			$temp = explode("/", $Part);
			$browserver = $temp[1];
			$temp = explode("", $browserver);
			$browserver = $temp[0];
			$browserver = preg_replace("/([\d\.]+)/", "\1", $browserver);
			$browserver = "$browserver";
			$browser = "NetscapeNavigator"
		}
		if (ereg("Mozilla", $Agent) && ereg("Opera", $Agent)) {
			$temp = explode("(", $Agent);
			$Part = $temp[1];
			$temp = explode(")", $Part);
			$browserver = $temp[1];
			$temp = explode("", $browserver);
			$browserver = $temp[2];
			$browserver = preg_replace("/([\d\.]+)/", "\1", $browserver);
			$browserver = "$browserver";
			$browser = "Opera"
		}
		if (ereg("Mozilla", $Agent) && ereg("MSIE", $Agent)) {
			$temp = explode("(", $Agent);
			$Part = $temp[1];
			$temp = explode(";", $Part);
			$Part = $temp[1];
			$temp = explode("", $Part);
			$browserver = $temp[2];
			$browserver = preg_replace("/([\d\.]+)/", "\1", $browserver);
			$browserver = "$browserver";
			$browser = "InternetExplorer"
		}
		if ($browser != "") {
			$browseinfo = "$browser$browserver"
		} else {
			$browseinfo = "Unknown"
		}
		return$browseinfo
	}

//调用方法$browser=browseinfo();直接返回结果

## PHP定时执行任务的实现PHP定时执行任务的实现



	ignore_user_abort();
	set_time_limit(0);
	$sleep_time = 5;
	$switch = include 'switch.php';
	while ($switch) {
		$switch = include 'switch.php';
		$fp = fopen('test.txt', 'a+');
		fwrite($fp, "这是一个php博客：phpddt.com $switch \n");
		fclose($fp);
		sleep($sleep_time)
	}
	exit();
```
