---

title: PDFJS
date: 2019-11-06
categories: [web]
tags: [PDFJS, pdf.js]

---



##  Vue PDF文件预览vue-pdf

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



# 在线预览PDF



首先将我们自己的文档上传至自己的服务器，然后呢URLEncode将服务器上要预览的文档链接转一下格式

--url在线编码
http://tool.chinaz.com/Tools/URLEncode.aspx


转完后，在http://view.officeapps.live.com/op/view.aspx?src=后面加上刚才自己转后的链接

--ppt
http://view.officeapps.live.com/op/view.aspx?src=http%3a%2f%2fvideo.ch9.ms%2fbuild%2f2011%2fslides%2fTOOL-532T_Sutter.pptx
--excel
http://view.officeapps.live.com/op/view.aspx?src=http%3A%2F%2Flearn.bankofamerica.com%2Fcontent%2Fexcel%2FWedding_Budget_Planner_Spreadsheet.xlsx
--word
http://view.officeapps.live.com/op/view.aspx?src=newteach.pbworks.com%2Ff%2Fele%2Bnewsletter.docx

1、 https://docs.google.com/viewer?url=（输入你的文档在服务器中的地址）

2、 https://view.officeapps.live.com/op/view.aspx?src=(输入你的文档在服务器中的地址)

3、 http://office.qingshanboke.com/Default.aspx?url=(输入你的文档在服务器中的地址)



第三方

http://usdoc.cn/



  1、百度智能云文档服务：https://cloud.baidu.com/product/doc.html

  2、腾讯在线文档：https://docs.qq.com/home/open

  3、IDOCV：[https://www.idocv.com/ ](https://www.idocv.com/ )

  4、XDOC：https://view.xdocin.com/