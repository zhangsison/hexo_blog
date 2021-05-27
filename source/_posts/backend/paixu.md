---

title: 实现四种基本排序算法
date: 2015-12-16
categories: [php]
tags: [排序]

---





## 实现四种基本排序算法





## 冒泡

	$arr = array(1, 43, 54, 62, 21, 66, 32, 78, 36, 76, 39);
	function bubbleSort($arr) {
		$len = count($arr);
		for ($i = 1; $i < $len; $i++) {
			for ($k = 0; $k < $len - $i; $k++) {
				if ($arr[$k] > $arr[$k + 1]) {
					$tmp = $arr[$k + 1];
					$arr[$k + 1] = $arr[$k];
					$arr[$k] = $tmp
				}
			}
		}
		return $arr
	}

## 选择排序 

思路分析：在要排序的一组数中，选出最小的一个数与第一个位置的数交换。然后在剩下的数当中再找最小的与第二个位置的数交换，如此循环到倒数第二个数和最后一个数比较为止。


	function selectSort($arr) {
		$len = count($arr);
		for ($i = 0; $i < $len - 1; $i++) {
			$p = $i;
			for ($j = $i + 1; $j < $len; $j++) {
				if ($arr[$p] > $arr[$j]) {
					$p = $j
				}
			}
			if ($p != $i) {
				$tmp = $arr[$p];
				$arr[$p] = $arr[$i];
				$arr[$i] = $tmp
			}
		}
		return $arr
	}
## 插入排序

思路分析：在要排序的一组数中，假设前面的数已经是排好顺序的，现在要把第n个数插到前面的有序数中，使得这n个数也是排好顺序的。如此反复循环，直到全部排好顺序。



	function insertSort($arr) {
		$len = count($arr);
		for ($i = 1, $i < $len; $i++) {
			$tmp = $arr[$i];
			for ($j = $i - 1; $j >= 0; $j--) {
				if ($tmp < $arr[$j]) {
					$arr[$j + 1] = $arr[$j];
					$arr[$j] = $tmp
				} else {
					break
				}
			}
		}
		return $arr
	}

## 快速排序 ## 

思路分析：选择一个基准元素，通常选择第一个元素或者最后一个元素。通过一趟扫描，将待排序列分成两部分，一部分比基准元素小，一部分大于等于基准元素。此时基准元素在其排好序后的正确位置，然后再用同样的方法递归地排序划分的两部分。

	function quickSort($arr) {
		$length = count($arr);
		if ($length <= 1) {
			return $arr
		}
		$base_num = $arr[0];
		$left_array = array();
		$right_array = array();
		for ($i = 1; $i < $length; $i++) {
			if ($base_num > $arr[$i]) {
				$left_array[] = $arr[$i]
			} else {
				$right_array[] = $arr[$i]
			}
		}
		$left_array = quick_sort($left_array);
		$right_array = quick_sort($right_array);
		return array_merge($left_array, array($base_num), $right_array)
	}

## PHP内置的排序算法 ##



- sort()
升序排列数组。value/key关联不保留
- rsort()
按反向/降序排序数组。index/key关联不保留
- asort()
在保持索引关联的同时排序数组
- arsort()
对数组进行反向排序并维护索引关联
- ksort()
按关键字排序数组。它保持数据相关性的关键。这对于关联数组是有用的
- krsort()
按顺序对数组按键排序
- natsort()
使用自然顺序算法对数组进行排序，并保持value/key关联
- natcasesort()
使用不区分大小写的“自然顺序”算法对数组进行排序，并保持value/key关联。
- usort()
使用用户定义的比较函数按值对数组进行排序，并且不维护value/key关联。第二个参数是用于比较的可调用函数
- uksort()
使用用户定义的比较函数按键对数组进行排序，并且不维护value/key关联。第二个参数是用于比较的可调用函数
- uasort()
使用用户定义的比较函数按值对数组进行排序，并且维护value/key关联。第二个参数是用于比较的可调用函数
