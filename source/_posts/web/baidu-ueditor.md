---

title: baidu-ueditor百度编辑器
date: 2018-08-08
categories:  [tool]
tags: [baidu]

---

# 百度编辑器

文档 http://fex.baidu.com/ueditor/


先打开ueditor.config.js这个文件。找到如下代码：

//,iframeCssUrl: URL + ‘/themes/iframe.css’ //给编辑器内部引入一个css文件

去掉前面的双斜杠。

接着找到/include/ueditor/themes路径下iframe.css

/可以在这里添加你自己的css/

img{max-width:100%;};

我们通过这段css就可以让图片自适应编辑器大小，从而解决出现横向滚动条的问题，当然除了设置图片，还可以

设置其他元素的样式