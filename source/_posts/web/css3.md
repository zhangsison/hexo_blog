---

title: css3
date: 2016-02-06
categories: [web]
tags: [hexo, node]

---





## 背景图垂直、水平均居中



``` background-position: center center;
background-position: center center;
```

## 让背景图基于容器大小伸缩  ##

```
background-repeat: no-repeat;
```



## 当内容高度大于图片高度时，背景图像的位置相对于viewport固定  ##

background-attachment: fixed;


## 让背景图基于容器大小伸缩 ## 

background-size: cover;

## position: sticky ##

![](https://user-gold-cdn.xitu.io/2018/12/12/167a27466d618a59?imageslim)

新建一个sticky属性的元素。它的运行效果和fixed相同，但不会挡住任何元素。你最好看看[例子](https://codepen.io/CSSKing/pen/yyMGPJ) 只有Mozilla和Safari浏览器支持这一属性，但你也可以像下面那样使用它：

`.sticky {
  position: static;
  position: sticky;
  top: 0px;
}`


## 新的尺寸单位 ##

不久之前，一些新的用以描述不同元素大小的尺寸单位问世了，它们是：

> 
vw (viewport width) - 浏览器窗口宽度的1%。
> 
vh (viewport height) - 同上，只不过用来描述高度。
> 
vmin and vmax 设置介于vh和vw之间的最大最小值。

有趣的是，几乎所有的现代浏览器都能很好地支持它们，所以你可以放心地使用。
为什么我们需要这些新的单位？因为它们可以让不同的尺寸更容易被定义，你不要为父元素指定任何的百分比或者别的什么，请看例子：[地址>>>](https://codepen.io/CrocoDillon/pen/fBJxu)

> .some-text {
    font-size: 100vh;
    line-height: 100vh;
}


    IE9应该用vm而不是vmin。
    iOS7在使用vh的时候可能会有bug。
    vmax至今并未得到全面的支持。

## visibility: visible 显示隐藏 ##

把一个设置为visibility: visible的元素放在一个设置为visibility: hidden的元素里面，会发生什么？
```
.hidden {
  visibility: hidden;
}
.hidden .visible {
  visibility: visible;
}`
```
[查看效果](https://codepen.io/CSSKing/pen/lxBfk)

## 使用硬件加速 ##

有时候动画可能会导致用户的电脑卡顿，你可以在特定元素中使用硬件加速来避免这个问题：

> .block {
    transform: translateZ(0);
}

复制代码你并不会察觉有什么不同，但浏览器会为这个元素进行3D硬件加速，在will-change这个特殊属性未被全面支持之前，这个方法还是很有用的。

