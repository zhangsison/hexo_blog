---

title: ecshop
date: 2015-10-06
categories: [php]
tags: [ecshop]

---


# ecshop


foreach 必须和/foreach 成对使用，且必须指定from 和item 属性

没有from表单

ini.php核心文件

lib_artcle.php文章操作文件

lib_common.php分类函数

sms  短信类

smtp 邮件类

ecshop中有2个地方使用了json,一个是cls_json.php文件，一个是transport.js文件。

eq相等，

ne、neq不相等，

gt大于，

lt小于，

gte、ge大于等于，

lte、le 小于等于，

not非， mod求模。

is [not] div by是否能被某数整除，

is [not] even是否为偶数，

$a is [not] even by $b即($a / $b) % 2 == 0，

is [not] odd是否为奇，

$a is not odd by $b即($a / $b) % 2 != 0 示例：

equal/ not equal/ greater than/ less than/ less than or equal/ great than or equal/后面的就不用说了

Smarty 中的 if 语句和 php 中的 if 语句一样灵活易用，并增加了几个特性以适宜模板引擎. if 必须于 /if 成对出现. 可以使用 else 和 elseif 子句. 可以使用以下条件修饰词：eq、ne、neq、gt、lt、lte、le、gte、ge、is even、is odd、is not even、is not odd、not、mod、div by、even by、odd by、==、!=、>、<、<=、>=. 使用这些修饰词时必须和变量或常量用空格格开

---------------------------

update_user_info    更新用户SESSION,COOKIE及登录时间、登录次数。

smarty里面有能够调用循环次数的方法

没记错的话是这样写的 {$smarty.foreach.foreachname.iteration}

这个是从1开始的

这个时候要定义下循环的名字

{foreach from="" name="foreachname"}

所以你要实现的东西可以这样写

{foreach from=$categories item=cat name=test}

{$cat.name}

{/foreach}

应该可以顺利实现你想要的效果.

可以判断当前条数与2求余是否给li加样式

{foreach from = $a item = val name=val}

{$val}

{/foreach}

样式的设置就不多说了



1. 供应商新增商品

2. 供应商修改商品（此步骤含商品下架,要更新ecs_goods on_sale_time字段）

3. 管理员新增商品

4. 管理员商品上架 (要更新ecs_goods on_sale_time字段）

5. 管理员商品下架 (要更新ecs_goods on_sale_time字段）

6. 管理员编辑商品

7. 管理员回收商品

8. 管理员还原商品

	
	
	
	
	```php
	1. function getTop5_fanli($type) {
	   	$ret = array();
	   	if ($type == "D") {
	   		$sql_d = "select b.mobile_phone,a.total_fanli from(select vip_id,sum(deduct_amt) as total_fanli from hsz_deduct_log where deduct_mode <>101 "." and vip_id>0 and to_days(create_date) = to_days(now()) "." group by vip_id  order by sum(deduct_amt) desc limit 0,5)a left join ecs_users b on a.vip_id=b.user_id ";
	   		$ret_d = $GLOBALS['db'] - >getAll($sql_d);
	   		foreach($ret_d as $key = >$value) {
	   			$ret[$key]['mobile_phone'] = substr($value['mobile_phone'], 0, 3)."****".substr($value['mobile_phone'], 7, 3);
	   			$ret[$key]['total_fanli'] = $value['total_fanli']
	   		}
	   	}
	   	if ($type == "W") {
	   		$sql_w = "select b.mobile_phone,a.total_fanli from(select vip_id,sum(deduct_amt) as total_fanli from hsz_deduct_log where deduct_mode <>101 and vip_id>0 and date_sub(curdate(),interval 7 day)
	           $ret_w=$GLOBALS['db']->getAll($sql_w);
	           foreach($ret_w as $key=>$value)
	           {
	         $ret[$key]['mobile_phone']=substr($value['mobile_phone'],0,3)." * ***".substr($value['mobile_phone'],7,3);
	
	   
	           $ret[$key]['total_fanli']=$value['total_fanli'];
	       }
	   }
	   if($type=="M "){
	       $sql_m="select b.mobile_phone,
	   	a.total_fanli from(select vip_id, sum(deduct_amt) as total_fanli from hsz_deduct_log where deduct_mode < >101 "
	       ."and vip_id > 0 and date_sub(curdate(), interval 30 day)." ecs_users b on a.vip_id=b.user_id"; $ret_m = $GLOBALS['db'] - >getAll($sql_m); foreach($ret_m as $key = >$value) {
   		$ret[$key]['mobile_phone'] = substr($value['mobile_phone'], 0, 3)."****".substr($value['mobile_phone'], 7, 3);
	   		$ret[$key]['total_fanli'] = $value['total_fanli']
	   	}
	   }
	   return $ret
	
	   }
	
	   function get_top_cat_id($cat_id) {
	   	$arr_cat = array();
	   	$parent_id = get_parent_id($cat_id);
	   	while ($parent_id > 0) {
	   		$parent_id = get_parent_id($parent_id);
	   		array_unshift($arr_cat, $parent_id)
	   	}
	   	return $arr_cat[1]
	   }
	   function get_parent_id($cat_id) {
	   	$sql = "select parent_id from ecs_category where cat_id = '".$cat_id."' limit 1";
	   	$ret = $GLOBALS['db'] - >getOne($sql);
	   	return intval($ret)
	   }
	   get_top_cat_id($cat_id)
	
	​
	```
	
	
	
	
