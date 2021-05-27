---
title: 小程序
date: 2019-12-06
categories: [web]
tags: [小程序]


---



# 小程序



### 图片等比例

```
<image src="test.png" mode="widthFix"/>
```



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

