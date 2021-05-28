---

title: 让网站支持老版本IE6、7、8、9浏览器的3种解决方案
date: 2015-12-06
categories: [web]
tags: [IE]

---


# 让网站支持老版本IE6、7、8、9浏览器的3种解决方案


## htmlshiv.js

Remy的 HTML5shiv通过JavaScript 来创建HTML5元素(如 main, header, footer等).在某种程度上通过JavaScript 创建的元素是 styleable(可样式)的。我们可以花很多时间来思考其运行原理,但谁会在乎呢?这种策略在所有产品网站上仍然是必须使用的.



## selectivizr.js

Selectivizr.js 是一个不可思议的资源,用于填充不支持的CSS选择器和属性,包括重要的 last-child。在最近的重设计中,我嵌入了 selectivizr,并在更老的 IE 浏览器上也不会错过任何细节。下面是我的实现代码:

现代项目绝对必须的。只在老IE时才加载

## Conditional Comments

下面这样最土的情况你肯定看到过。但无论丑陋与否,事实上这段代码完全按预期的方式运行:

这个代码片段不需要或等待JavaScript,而且也不需要重量级的JavaScript库。你定义的styles类立即生效,还没有闪屏。

尽管 Internet Explorer 正在迎头赶上竞争对手,但事实上老的IE浏览器仍然比较流行,特别是在发展中国家。好消息是,这些资源在所有现代浏览器上运行良好,代价也并不高!


