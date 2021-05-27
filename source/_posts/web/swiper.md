---

title: swiper
date: 2016-12-06
categories: [web]
tags: [swiper]

---



## swiper



##  同一个页面面使用两个swiper轮播 ##

**html代码**
```html
<div class="swiper-container banner">
	<div class="swiper-wrapper">
		<div class="swiper-slide">
		</div>
		<div class="swiper-slide">
		</div>
		<div class="swiper-slide">
		</div>
	</div>
	<div class="swiper-pagination banner">
	</div>
</div>
<div class="swiper-container case ">
	<div style="height:51px;">
	</div>
	<div class="swiper-wrapper">
		<div class="swiper-slide">
		</div>
		<div class="swiper-slide">
		</div>
		<div class="swiper-slide">
		</div>
	</div>
	<div class="swiper-pagination case">
	</div>
</div>

```

**js代码：**

```js
$(function() {
	var mySwiper = $('.banner').swiper({
		mode: 'horizontal',
		loop: true,
		autoResize: true,
		pagination: '.banner .swiper-pagination',
		paginationClickable: true,
		autoplay: 3000,
	});
	var swiper = $('.case').swiper({
		pagination: '.case .swiper-pagination',
		slidesPerView: 4,
		slidesPerColumn: 2,
		paginationClickable: true,
		spaceBetween: 20
	});
})
```

```js
声明swiper变量时 加一个同级元素加以区别即

var mySwiper = $('.banner')

var swiper = $('.case')

然后就是更改pagination的默认值用以区别显示的页面控件

pagination:'.banner'

pagination: '.case',


这就是基本的修改方式，值得一提的是swiper在使用中不予bootstrap冲突

```


## 单个swiper的使用 ##
```js
<script src="https://cdn.bootcss.com/jquery-weui/1.2.0/js/swiper.min.js">
</script>
<script src="https://cdn.bootcss.com/jquery-weui/1.2.0/js/city-picker.min.js">
</script>
<div class="swiper-container" data-space-between='10' data-pagination='.swiper-pagination'
data-autoplay="1000">
<div class="swiper-wrapper">

	<div class="swiper-slide">
		<a href="#">
			<img width="100%" height="180px" src="#" alt="">
		</a>
	</div>
	
</div>
<div class="swiper-pagination">
</div>
</div>
<script>
$(".swiper-container").swiper({
	loop: true,
	autoplay: 3000
});
</script>

```

####  小程序swiper 自定义高度



```
<!-- components/swiperIdex/swiperIdex.wxml -->
<view class="index_swiper" style="height:{{Hei}};">
    <swiper autoplay indicator-dots circular style="height:{{Hei}}">
        <swiper-item wx:for="{{swiperList}}" wx:key="id" data-index="{{index}}" bindtap="handleNavigator">
            <image class="index_swiper_image" src="{{item.imagePath}}" mode="widthFix" bindload='imgHeight'></image>
        </swiper-item>
    </swiper>
    <view class="swiper_test">
        <i class="iconfont  iconicon_sosuo_xian-"></i>
        已有 {{times}} 人学习急救培训课程
    </view>
</view>


```



```
// components/swiperIdex/swiperIdex.js
Component({
    /**
     * 组件的属性列表
     */
    properties: {
        swiperList: Array,
        times:Number
    },
    /**
     * 组件的初始数据
     */
    data: {
        Hei: '',
        times:0,   },

    /**
     * 组件的方法列表
     */
    methods: {
        /**
         * swiper 高度自适应
         */
        imgHeight: function (e) {
            var winWid = wx.getSystemInfoSync().windowWidth;
            var imgh = e.detail.height;
            var imgw = e.detail.width;
            var swiperH = winWid * imgh / imgw + "px"
            this.setData({
                Hei: swiperH
            })
        },
        //轮播图跳转
        handleNavigator(e) {
            //1.获取轮播图的索引
            const {
                index
            } = e.currentTarget.dataset;
            //2.判断第几张轮播图对应跳转的页面
            if (index === 0) {
                //第一张轮播图跳转的页面
                let url = this.data.swiperList[0].url
                this.tiaozhuan(url.type, url.id,url.idType)
            } else if (index === 1) {
                //第二张轮播图跳转的页面
                let url = this.data.swiperList[1].url
                this.tiaozhuan(url.type, url.id,url.idType)
            } else if (index === 2) {
                let url = this.data.swiperList[2].url
                this.tiaozhuan(url.type, url.id,url.idType)
            } else if (index === 3) {
                let url = this.data.swiperList[3].url
                this.tiaozhuan(url.type, url.id,url.idType)
            } else {
                let url = this.data.swiperList[4].url
                this.tiaozhuan(url.type, url.id,url.idType)
            }
        },

        tiaozhuan(type, id,idType) {

         if(type == 1 ){
            // 类型 1公开课 2网络课 3团课
            if (idType == 1) {
                wx.navigateTo({
                    url: "/pages/class/public_clsss_details/public_clsss_details?id=" + id
                })
            } else if (idType == 2) {
                wx.navigateTo({
                    url: "/pages/class/network_clsss_details/network_clsss_details?id=" + id
                })
            } else if (idType == 3) {
                wx.navigateTo({
                    url: "/pages/class/league_clsss_details/league_clsss_details?id=" + id
                })
            }
        } else if (type == 2) {
            wx.navigateTo({
                url: "/pages/class/tutorpages/tutorpages?id=" + id
            })
        } else if (type == 3) {
            wx.navigateTo({
                url: "/pages/class/tutor_recruit/tutor_recruit"
            })
        }



        },
    },




})
```

