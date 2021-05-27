---

title: jquery
date: 2015-12-06
categories: [web]
tags: [jquery, jq]

---





## 选择器--他继承了css语法



$(css元素).css(样式)

#### jquery是添加行为

$(css元素>元素).css(样式)改变子节点

节点的判断

if（$("#i")length>0）{

$('$(i).css(red)')

}

$('#box,.pp,p').css(color,red)群组选择器

$('p *').css(color,red)通配符选择器

后代选择器 ul li a（）

子选择器div>p()

next选择器div+p()

nextall选择器div-p()

#### 过滤器

以冒号开头

$(li:frist)。css(color,red)第一

$(li:last).css(##)最后

$(ul li:frist)。css（）

$(li:even).css()偶数

$(li:odd).css()奇数

$(li:eq(2)).css()从零开始

：focus焦点

$('li').slice(2,7).css()从第几到第几

:filter 选择

$(s).html()也可替换html内容

$(sd).text()获取文本也可替换

$(input).val()获取表单内容也可替换

属性操作$().attr（）

$.each(box,function(){

(attr,value);

})

width()

var obx=$(

sahhd

)创建节点

$(div).append（）找到节点插入节点

$(div).after（）

$(div).prependto（）

$（）.wrap()添加DOM元素节点

$（）.clone()

$（）.remove()

$（）.empty()

$（）.replacewith()替换节点

表单过滤选择器

事件

绑定事件

复合事件

click点击事件

mouseout

mouseover移入移出的函数

dblclick（）双击事件

enter不会触发子节点

keydown()

keyup()

focusin()

blur()

复合事件

ready()当DOM结束时执行

hover（）；mouseenter，mouseleave的结合

bind()

#### 事件的冒泡行为

.stopPropgtion()  禁止冒泡

#### 模式用户操作

.trigger()

trigger多条数据用中括号

自定义事件

$(input).bind(my,function(）{

哈哈

}.trigger（my）)

triggerHandle（）

.preventDefault（）取消默认

命名空间

普通绑定bind（）

unbind()移除事件

$(input).bind(click.acb,functin(){

alent('sd')

})

$(input).bind(click.a,functin(){

alent('sd')

})$(input).bind(click.ac,functin(){

alent('sd')

})

$(input).unbind(click.acb);

on off和one

新方法的绑定on

#### 新方法的解绑off

$(input).on(click,function(){

alert('sad');

})

$(button)off(click);

one执行一次

#### 动画效果

显示show（）

隐藏hide（）

#### 列队动画 递归调用

$(.show).click(fuction(){

$(.test).first().show(fast,fuonction testshow(){

$(this).next().show(fast,testshow)

})

})

toggle隐藏显示切换

up down上卷下卷

out in 淡入淡出

to透明

animate滑动.delay（时间）

stop停止

arguments.callee不停的调用自己

animated查找

ajax

load（）方法载入载入html文本局部方法

get需要？号 post方式提交

全局

$.get()

$(input).click(function(){

$.get(test.php,url=ww,function(reponse,status,xhr){

$(#box).html(reponse)

})

})

$.post()

$.getjson()

$.ajax({

type:post

url:'test.php',

data:{

url:ds，

}

})

#### 表单序列化

.sreiralize()

ajaxstart()

ajaxshop()

success请求成功后执行

complete请求完成后执行

beforesend发送请求之前执行

error失败后执行

jqXHR就是$.ajax()返回的对象

$.each() 遍历数组

$.grep()

$.map()

$.merge()合并数组

$.unique（）删除

$.isarray()判断是否是数组

slideUp();以滑动动画隐藏

#### 插件

jquery-validation表单插件    

lazyload图片延迟加载

引入jq，lazyload

