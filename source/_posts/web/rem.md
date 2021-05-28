---
title: rem
date: 2016-12-06
categories: [rem]
tags: [rem]


---

# PC端网页尺寸设计

屏幕分辨率有1024×768,1366×768,1280×800,1280×1024，1440×900,1600×900，1920×1080


rem和em很容易混淆，其实两个都是css的单位，并且也都是相对单位，现有的em，css3才引入的rem，在介绍rem之前，我们先来了解下em

em作为font-size的单位时，其代表父元素的字体大小，em作为其他属性单位时，代表自身字体大小——MDN

我在面试时经常问会一道和em有关的题，来看一下面试者对css细节的了解程度，如下，问s1、s2、s5、s6的font-size和line-height分别是多少px，先来想一想，结尾处有答案和解释

## js

```
var documentElement = document.documentElement;

function callback() {
    var clientWidth = documentElement.clientWidth;
    // 屏幕宽度大于780，不在放大
    clientWidth = clientWidth < 780 ? clientWidth : 780;
    documentElement.style.fontSize = clientWidth / 10 + 'px';
}

document.addEventListener('DOMContentLoaded', callback);
window.addEventListener('orientationchange' in window ? 'orientationchange' : 'resize', callback);

```
