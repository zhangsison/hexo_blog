---

title: foreach
date: 2015-12-08
categories: [php]
tags: [foreach]

---




## 实现将一维数组转换为每3个连续值组成的二维数组

```php

	$aaa = array('aa', 'bb', 'cc', 'dd', 'ee', 'ff', 'gg', 'hh', 'ii');
	for ($i = 0; $i < 3; $i++) {
		$bbb[] = array_slice($aaa, $i * 3, 3)
	}
	print_r($bbb);
	$arr = Array("0" = >Array("name" = >"gdfg"), "1" = >Array("name" = >"433"), "2" = >Array("name" = >"dfgff"));
	$last = end($arr);
	$end = $last["name"];
	foreach($arr as $k = >$val) {
		$str. = $val['name'];
		if ($val['name'] != $end) {
			$str. = "，"
		}
	}
	echo $str;输出结果：gdfg，433，dfgff

## 无限遍历数组函数

	function foreachKeyVals($data) {
		foreach($data as $key = >$values) {
			if (is_array($values)) {
				foreachKeyVals($values)
			} else {
				echo $values.""
			}
		}
		echo ""
	}

## 用递归的方法遍历多维数组


    递归遍历多维数组  
    
    $arr = array(11, 22, 99, array("a", "b", array("987yy", "39yy")));
    function bianli($a) {
    	foreach($a as $id) {
    		if (is_array($id)) {
    			bianli($id)
    		} else echo $id."
    "
    	}
    }
    bianli($arr);


## 第一次foreach遍历出第一维数组

	foreach($fruit as $v1) {
		foreach($v1 as $k2 = >$v2) {
			echo $k2."--".$v2.""
		}
		echo ""
	}
	$array = [[1, 2], [3, 4], ];
	foreach($array as list($a, $b, $c)) {
		echo "A: $a; B: $b; C: $c\n"
	}

```

> array_values($arr);获得数组的值

> array_keys($arr);获得数组的键名

> end($arr);将数组中的内部指针指向最后一个单元

> list($key,$value)=each($arr);获得数组当前元素的键名和值




## 无线遍历数组

```php

    $arr = array(array("1", "111", array("12", "122", "1222")), "2", array("3", "33", array("34", "344", "3444", array("344445", "3444455"))), "4");
    
    array_search_all($arr);
    function array_search_all($arr) {
    	foreach($arr as $value) {
    		if (is_array($value)) {
    			recurrence($value)
    		} else {
    			echo($value."")
    		}
    	}
    }
    function recurrence($arr) {
    	foreach($arr as $value) {
    		if (is_array($value)) {
    			recurrence($value)
    		} else {
    			echo($value."")
    		}
    	}
    }

## 每次遍历出来值组成以为数组

	$a = array(array(array(0,1),1,array(2,3)),array(3,4,5),array(6,7,8));
	function arrfun($arr, &$new_arr) {
		if (is_array($arr)) {
			foreach($arr as $value) {
				if (is_array($value)) {
					arrfun($value, $new_arr)
				} else {
					$new_arr[] = $value;
					echo $value
				}
			}
		} else {
			echo "不是数组!"
		}
	}
	
	$new_arr = array();
	
	arrfun($a,$new_arr);
	
	print_r($new_arr);



## 遍历三维数组

	$arr_temp5 = array();
	foreach($arr_temp2 as $value) {
		foreach($value as $v) {
			$arr_temp5[] = $v
		}
	}
	unset($arr_temp2, $value, $v);

## 一二维

	foreach($arr_age as $age) {
		if (is_array($age)) {
			foreach($age as $detail) {
				echo $detail;
			}
		} else {
			echo $age;
		}
	}

  ```