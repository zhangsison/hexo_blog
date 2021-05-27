---

title: Thinkphp
date: 2015-12-15
categories: [php]
tags: [Thinkphp]

---



## Thinkphp





| TP运算符    | SQL运算符       | 例子                                                         | 实际查询条件                        |
| ----------- | --------------- | ------------------------------------------------------------ | ----------------------------------- |
| eq          | =               | $where[‘id’] = array(‘eq’,100);                              | 等效于：$map[‘id’] = 100;           |
| neq         | !=              | $where[‘id’] = array(‘neq’,100);                             | id != 100                           |
| gt          | >               | $where[‘id’] = array(‘gt’,100);                              | id > 100                            |
| egt         | >=              | $where[‘id’] = array(‘egt’,100);                             | id >= 100                           |
| lt          | <               | $where[‘id’] = array(‘lt’,100);                              | id < 100                            |
| elt         | <=              | $where[‘id’] = array(‘elt’,100);                             | id <= 100                           |
| like        | like            | $where(‘username’) = array(‘like’,’%admin%’);                | username like ‘%admin%’             |
| between     | between and     | $where[‘id’] = array(‘between’,‘1,8’);                       | id BETWEEN 1 AND 8                  |
| not between | not between and | $where[‘id’] = array(‘not between’,‘1,8’);                   | id NOT BETWEEN 1 AND 8              |
| in          | in              | $where[‘id’] = array(‘in’,‘1,5,8’);                          | id in(1,5,8)                        |
| not in      | not in          | $where[‘id’] = array(‘not in’,‘1,5,8’);                      | id not in(1,5,8)                    |
| and（默认） | and             | $where[‘id’] = array(array(‘gt’,1),array(‘lt’,10));          | (id > 1) AND (id < 10)              |
| or          | or              | $where[‘id’] = array(array(‘gt’,3),array(‘lt’,10), ‘or’);    | (id > 3) OR (id < 10)               |
| xor（异或） | xor             | 两个输入中只有一个是true时，结果为true，否则为false，例子略。 | 1 xor 1 = 0                         |
| exp         | 综合表达式      | $where[‘id’] = array(‘exp’,‘in(1,3,8)’);                     | $where[‘id’] = array(‘in’,‘1,3,8’); |



对于两种去重方式： 

```php
$data = $test_data->Distinct(true)->field('descriprion')->order('description desc')->select();  //利用distinct方法去重
$data = $test_data->group('description')->order('description desc')->select();  //利用group方法去重
```

 利用distinct去重、简单易用，但只能对于单一字段去重，并且最终的结果也仅为去重的字段，实际应用价值不是特别大。 
 利用group去重，最终的显示结果为所有字段，且对单一字段进行了去重操作，效果不错，但最终显示结果除去去重字段外，按照第一个字段进行排序，可能还需要处理。

