---
title: 小程序
date: 2019-12-06
categories: [web]
tags: [小程序]


---



# 小程序

Painter：微信小程序生成图片库，绘制一张可以发到朋友圈的图片

html2wxml：用于微信小程序的HTML和Markdown格式的富文本渲染组件，支持代码高亮



### 小程序video

在video组件上添加 bindtimeupdate 事件 播放进度变化时触发

视频全屏使用swiper组件

```
<video src="{{src1}}" object-fit="fill" controls="{{false}}" id="video"  loop="true" show-fullscreen-btn='false' autoplay='{{autoplay}}' show-play-btn='false' bindtimeupdate ='bindtimeupdate'></video>
```



### scene传多个参数

1、只传一个参数写法

```perl
scene=hid%3D34//34是参数值 %3D是=符号
```

2、传2个参数的情况

```perl
scene=hid%3D34%26pcid%3D1 //%26是&符号，hid和pcid是键名，34和1是键值
```



### 图片等比例

```
<image src="test.png" mode="widthFix"/>
```



### 小程序公众号文章

注意公众号文章链接里面有？会被截取掉后面的网址，这时候传送页面要使用（encodeURIComponent）和接收页面（decodeURIComponent）解码编译



### 动态标题

onLoad的时候动态设置标题

```
wx.setNavigationBarTitle({
  title: '新标题'
})
```



# 扫一扫

```
 var scene = decodeURIComponent(options.scene);
 
//获取等号前的
let queryarr = scene.split("=")[0];

//多个值转对象
  filterUrlParam : (urlSearch) => {
    let ret = {}
    let regParam = /([^&=]+)=([\w\W]*?)(&|$|#)/g
    if (urlSearch) {
      var strParam = urlSearch;
      var result
      while ((result = regParam.exec(strParam)) != null) {
        ret[result[1]] = result[2]
      }
    }
    return ret
  },
  
  //web端显示二进制流图片
  const url = 'data:image/png;base64,' + encodeURI(response.data.qrCode)

```





### 小程序 插入

```
const yi = {
"id": count,
"name": name,
"time": time
}
let list =jicilist.concat(yi)
```



# 小程序 appId

> ### wx.getAccountInfoSync()



### 小程序的更新机制

开发者可以通过 wx.getUpdateManager可以获知是否有新版本小程序、新版本是否下载好以及应用新版本的能力



# 小程序 实现横向滚动

``` html
<scroll-view scroll-x="true" style=" width: 100%;height: 100%;white-space: nowrap;">
 
       <view style='display: inline-block;' wx:for='{{viewPath}}' wx:key='{{item}}'>
 
            <image src='{{item}}' bindtap='bigimg'></image>
 
            <i class='iconfont icon-ai54' bindtap='delimg'></i>
 
        </view>
 
</scroll-view>
```

小程序 获取父级index

```js

<view class="social_is" wx:for="{{getCommunityThemeList}}" wx:key="key">
<view class="comment_box_li" wx:for="{{item.commentList}}" wx:key='key' wx:for-index="index2" wx:for-item="i"
wx:if="{{index2<5}}">
<i class="comment_name {{i.isSelf == 1 ? 'islike':''}}">{{i.userName}}：</i>
<view bindtap="{{i.isSelf == 0 ? 'userReply':'userDelete'}}" data-commentid="{{i.id}}" data-index="{{index}}">
{{i.content}}
</view>
</view>
</view>
```

