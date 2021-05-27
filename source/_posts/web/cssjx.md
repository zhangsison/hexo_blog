---

title: css建议
date: 2016-03-06
categories: [web]
tags: [css]

---



## margin 和 padding ##

这里主要用于两个属性：margin 和 padding，我们以 margin 为例，padding 与之相同。盒子有上下左右四个方向，每个方向都有个外边距：

```css

margin-top:1px;

margin-right:2px;

margin-bottom:3px;

margin-left:4px;

你可以简写成：

margin:1px 2px 3px 4px;

语法 margin:top right bottom left;

//四个方向的边距相同，等同于margin:1px 1px 1px 1px;

margin:1px;

//上下边距都为1px，左右边距均为2px，等同于margin:1px 2px 1px 2px;

margin:1px 2px;

//右边距和左边距相同，等同于margin:1px 2px 3px 2px;

margin:1px 2px 3px;

//注意，这里虽然上下边距都为1px，但是这里不能缩写。

margin:1px 2px 1px 3px;

##二、边框（border）

边框的属性如下：

border-width:1px;

border-style:solid;

border-color:#000;

可以缩写为一句：

border:1px solid #000;

语法 border:width style color;

##三、背景（Backgrounds）

背景的属性如下：

background-color:#f00;

background-image:url(background.gif);

background-repeat:no-repeat;

background-attachment:fixed;

background-position:0 0;

可以缩写为一句：

background:#f00 url(background.gif) no-repeat fixed 0 0;

语法是 background:color image repeat attachment position;

你可以省略其中一个或多个属性值，如果省略，该属性值将用浏览器默认值，默认值为：

color: transparent;

image: none;

repeat: repeat;

attachment: scroll;

position: 0% 0%;

## 四、字体（fonts）

字体的属性如下：

font-style:italic;

font-variant:small-caps;

font-weight:bold;

font-size:1em;

line-height:140%;

font-family:"Lucida Grande",sans-serif;

可以缩写为一句：

font:italic small-caps bold 1em/140%"Lucida Grande",sans-serif;

注意，如果你缩写字体定义，至少要定义 font-size 和 font-family 两个值。

## 五、列表（lists）

取消默认的圆点和序号可以这样写 list-style:none;

list的属性如下:

list-style-type:square;

list-style-position:inside;

list-style-image:url(image.gif);

可以缩写为一句：

list-style:square inside url(image.gif);

## 六、颜色（Color）

16进制的色彩值，如果每两位的值相同，可以缩写一半。例如：

Aqua: #00ffff —— #0ff

Black: #000000 —— #000

Blue: #0000ff —— #00f

Dark Grey: #666666 —— #666

Fuchsia:#ff00ff —— #f0f

Light Grey: #cccccc —— #ccc

Lime: #00ff00 —— #0f0

Orange: #ff6600 —— #f60

Red: #ff0000 —— #f00

White: #ffffff —— #fff

Yellow: #ffff00 —— #ff0

## 七、属性值为0

书写原则是，如果CSS属性值为0，那么你不必为其添加单位（如 px/em），你可能会这样写：

padding:10px 5px 0px 0px;

试试这样吧:

padding:10px 5px 0 0 ;

## 八、最后一个分号

最后一个属性值后面分号可以不写，如：

`#nav{

border-top:4px solid #333;

font-style: normal;

font-variant:normal;

font-weight: normal;

}
`
可以简写成:

`#nav{

border-top:4px solid #333;

font-style: normal;

font-variant:normal;

font-weight: normal

}
`
## 九、字体粗细（font-weight） ##

你可能会这样写:

h1{

font-weight:bold;

}

p{

font-weight:normal;

}

可以简写成:

h1{

font-weight:700;

}

p{

font-weight:400;

}

## 十、圆角半径（border-radius） ##

border-radius 是 css3 中新加入的属性，用来实现圆角边框。

-moz-border-radius-bottomleft:6px;

-moz-border-radius-topleft:6px;

-moz-border-radius-topright:6px;

-webkit-border-bottom-left-radius:6px;

-webkit-border-top-left-radius:6px;

-webkit-border-top-right-radius:6px;

border-bottom-left-radius:6px;

border-top-left-radius:6px;

border-top-right-radius:6px;

可以简写成:

-moz-border-radius:6px 6px 0;

-webkit-border-radius:6px 6px 0;

border-radius:6px 6px 0;

语法 border-radius:topleft topright bottomright bottomleft;

## 什么是rem ##

CSS3新增的一个相对单位rem（root em，根em）。rem是相对于根节点（或者是html节点）。如果根节点设置了font-size:10px;那么font-size:1.2rem;字体大小等于12px。

## 1. 计算页面的dpr ##

    if (!dpr && !scale) {
    var isAndroid = win.navigator.appVersion.match(/android/gi);
    var isIPhone = win.navigator.appVersion.match(/iphone/gi);
    var devicePixelRatio = win.devicePixelRatio;
    if (isIPhone) {
        // iOS下，3和3以上的屏，用3倍的方案，2用2倍方案，其余的用1倍方案
        if (devicePixelRatio >= 3 && (!dpr || dpr >= 3)) {                
            dpr = 3;
        } else if (devicePixelRatio >= 2 && (!dpr || dpr >= 2)){
            dpr = 2;
        } else {
            dpr = 1;
        }
    } else {
        // 其他设备下，仍旧使用1倍的方案
        dpr = 1;
    }
    scale = 1 / dpr;
    }


## 如何转换rem ##

对于使用webpack的来说，其实也是有一个postcss插件的px2rem，可以很轻松的配置相关属性，转换成相对于的rem单位。比如我们的.postcssrc 配置如下：


	module.exports = {
	  "plugins": {
	    "postcss-px2rem": {
	      baseDpr: 1,
	      remUnit: 37.5,
	      onePxComment: '1px',
	      forcePxComment: '!px',
	      keepComment: '!no',
	      forcePxProperty: ['font-size'] // font-size强制使用px单位
	    }
	  }
	}

## 1. 文本字号不建议使用rem ##

前面大家都见证了如何使用rem来完成H5适配。那么文本又将如何处理适配。是不是也通过rem来做自动适配。

显然，我们在iPhone3G和iPhone4的Retina屏下面，希望看到的文本字号是相同的。也就是说，我们不希望文本在Retina屏幕下变小，另外，我们希望在大屏手机上看到更多文本，以及，现在绝大多数的字体文件都自带一些点阵尺寸，通常是16px和24px，所以我们不希望出现13px和15px这样的奇葩尺寸。

如此一来，就决定了在制作H5的页面中，rem并不适合用到段落文本上。所以在Flexible整个适配方案中，考虑文本还是使用px作为单位。只不过使用[data-dpr]属性来区分不同dpr下的文本字号大小。

配置完成之后，在实际使用时，你只要像下面这样使用：

	.selector {
	width: 150px;
	height: 150px; 
	font-size: 12px; 
	border: 1px solid #ddd; 
	}

**px2rem处理之后将会变成**

	.selector {
	    width: 2rem;
	   height: 2rem;
	    border: 1px solid #ddd;
	}
	[data-dpr="1"] .selector {
	    font-size: 12px;
	}
	[data-dpr="2"] .selector {
	    font-size: 28px;
	}
	[data-dpr="3"] .selector {
	    font-size: 42px;
	}

因为不同的dpr，屏幕会缩成不同比例，所以这里的字号会根据dpr进行相应的放大。举个例子，如果data-dpr = 2 那么页面的viewport会被缩小，所以字号需要相应的乘以比例进行放大。

```
[px转成rem的插件地址]( https://github.com/flashlizi/cssrem)