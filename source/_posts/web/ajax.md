---

title: 滚动加载-weui
date: 2016-12-12
categories: [web]
tags: [weui, 滚动加载]

---



## js代码

```bash

<script src="__TMPL__/public/js/fastclick.js"></script>

<script src="__TMPL__/public/js/jquery-weui.js"></script>

   <script>
	var loading = false;
	var url = 'http://192.168.2.29/thinkcmf/public/portal/video/js_tuandui_ajax';
	var ww = '';
	var pageStart = 2;
	$(document.body).infinite().on("infinite",
	function() {
		if (loading) return;
		loading = true;
		$.ajax({
			url: url,
			type: 'POST',
			dataType: 'json',
			data: {
				page: pageStart
			},
			success: function(datas) {
				if (datas == '1') {
					$(".weui-loadmore__tips").html("数据了");
					$(".weui-loading").hide()
				} else {
					var ww = create_html(datas)
				}
				setTimeout(function() {
					pageStart++;
					$("#WWW").append(ww);
					loading = false
				},
				1500)
			}
		})
	});
	function create_html(datas) {
		var len = datas.length;
		var _html = '';
		for (var i = 0; i < len; i++) {
			var item = '<div class="yuding_js"><div class="yuding_js_img" style="background: #313236"><a href="http://192.168.2.29/thinkcmf/public/portal/page/index/id/' + datas[i].id + '.html"><img style="margin-top: 20px;"  src="http://192.168.2.29/thinkcmf/public/upload/' + datas[i].more.thumbnail + '" alt="超级盟主"><i> 金牌讲师</i> </a></div><div class="yuding_neir"> <p style="margin: 0 0 .3em;"> <i class="yuding_neir_gf">官方认证</i>' + datas[i].post_title + '</p><p  style="margin: 0 0 .3em;"> ' + datas[i].post_excerpt + '</p><i  style="margin: 0 0 .3em;" class="yuding_neir_zc">支持全国</i><a  href="http://192.168.2.29/thinkcmf/public/portal/page/index/id/' + datas[i].id + '"> <p style="margin-top: 10px" class="yuding_neir_yd"> 金牌讲师预订</p> </a></div></div>';
			_html += item
		}
		return _html
	}



       
    </script>
```