---

title: PDFJS
date: 2019-11-06
categories: [web]
tags: [PDFJS, pdf.js]

---



##  Vue PDF文件预览vue-pdf

## PDFJS在线预览PDF



df.js是一款开源的pdf文档读取解析插件，据说在HTML5下诞生的，对于主流的浏览器基本都支持。

**使用pdfjs在线预览pdf可以有两个选择：**

1. 使用pdfjs已经写好的viewer.html页面
pdf.js主要包含两个库文件，一个pdf.js和一个pdf.worker.js，，一个负责API解析，一个负责核心解析

官网GitHub地址如下：https://github.com/mozilla/pdf.js

http://mozilla.github.io/pdf.js/

浏览pdf文档：http://xxxxxx/viewer.html?name=pdf地址

pdf.js nmp 搭建或者找个web目录放入，不跨域

 **viewer.js**

> var DEFAULT_URL = 'compressed.tracemonkey-pldi-09.pdf'  里面是PDF


 2. 我们只用修改viewer.js文件中的pdf路径参数即可：

> var DEFAULT_URL = '09.pdf';

如果pdf文件与viewer.html不在一层目录中，改成相对路径即可：

> var DEFAULT_URL = ' ../doc/ 09.pdf';

**下面我就介绍下，具体嵌入项目中是如何运用的！**



> 页面可以使用iframe标签来加载pdf


    <iframe src="x/pdfJs/generic/web/viewer.html" />?file=xxx" />" width="100%" height="800"></iframe>

![](https://www.linuxidc.com/upload/2015_06/150612094867576.png)



> 不知道大家有没有试过下面这段url请求:

    http://localhost:8080/akane/resources/plugin/pdfJs/generic/web/viewer.html?file=/akane/displayPDF.do?id=966c6f0e-3c06-4154-aafd-afdbee5bcb65

 我们在实际应用中，可能会根据不同的参数，来选择展示不同的pdf文件，此时就涉及到传参的问题了，仔细观察上面这段url地址会发现，在file请求参数中的值为一个url地址，而这个url地址又追加了自己的请求参数，这就导致一个url地址中出现2个"?"

导致浏览器不能正常解析这段url！

一种解决思路是：我们可以把file形参的值，先编码，然后再解码来解决这个问题！

此时，就可以请encodeURIComponent()函数出场了！因为其为js函数，所以需要在文档就绪函数中动态为iframe设置src的值，如下所示：

	<%@ page contentType="text/html;charset=GBK" language="java" %>
	<%@ taglib prefix="c" uri="http://java.sun.com/jsp/jstl/core" %>
	<script type="text/javascript">
	    $(function(){
	        $("#displayPdfIframe").attr("src",'<c:url value="/resources/plugin/pdfJs/generic/web/viewer.html" />?file=' + encodeURIComponent('<c:url value="/displayPDF.do?id=${id}"/>'));
	    });
	</script>
	<div class="ctrlDiv">
	    <div class="eleContainer elePaddingBtm">
	        <iframe id="displayPdfIframe" width="100%" height="100%"></iframe>
	    </div>
	</div> 

既然有编码，那么就一定要有解码来解析他，不过这个工作generic/web/viewer.js已经替我们做过了，如下所示：

![](https://www.linuxidc.com/upload/2015_06/150612094867577.png)