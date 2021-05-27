---

title: css 进度条
date: 2016-12-06
categories: [web]
tags: [hexo, node]

---


## CSS 滚动进度条效果 ##

<iframe height='365' scrolling='no' title='使用线性渐变实现滚动进度条' src='//codepen.io/Chokcoco/embed/KbBXQM/?height=265&theme-id=0&default-tab=html,result' frameborder='no' allowtransparency='true' allowfullscreen='true' style='width: 100%;'>See the Pen <a href='https://codepen.io/Chokcoco/pen/KbBXQM/'>使用线性渐变实现滚动进度条</aby Chokcoco (<a href='https://codepen.io/Chokcoco'>@Chokcoco</a>) on <a href='https://codepen.io'>CodePen</a>.
</iframe>



## CSS 闪光动画 ##
```css

    body{overflow:hidden;background:#000}
    .container{display:flex;justify-content:center;align-items:center;height:100vh;overflow:hidden;animation-delay:1s}
    .item-1{width:20px;height:20px;background:#f583a1;border-radius:50%;background-color:#eed968;margin:7px;display:flex;justify-content:center;align-items:center}
    @keyframes scale{0%{transform:scale(1)}
    50%,75%{transform:scale(2.5)}
    78%,100%{opacity:0}
    }
    .item-1:before{content:'';width:20px;height:20px;border-radius:50%;background-color:#eed968;opacity:0.7;animation:scale 1s infinite cubic-bezier(0,0,0.49,1.02);animation-delay:200ms;transition:0.5s all ease;transform:scale(1)}
    <div class="container">
      <div class="item-1"></div> 
    </div>
```
