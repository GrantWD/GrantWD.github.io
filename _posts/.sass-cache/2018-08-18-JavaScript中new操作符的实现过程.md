---
layout: post
title: 'JavaScript中new操作符的实现过程'
subtitle: 'JavaScript基础知识'
date: 2018-08-18
categories: JavaScript
tags: 前端开发 JavaScript
---


## new操作符的实现过程


#### 问题描述
在IE6中元素设置了浮动flot,又设置了横向的margin,在IE6下显示的margin值会比正常设置的大一倍(比如设置了```margin-left=10px```,但是显示的是20px)只有特定的浮动行的第一个浮动元素会遭遇这个Bug。
![代码演示](/assets/img/201817001/20180817134506.png)![浏览器效果](/assets/img/201817001/20180817134625.png)
#### 解决方案 1
将浮动的元素设置为内联元素```display:inline```。
#### 解决方案 2
将使用hack方法，将第一个浮动元素的```_margin-left:5px```或在```_margin-right:5px```的值设置为一半(```_```下划线只有IE6识别,```*```只有IE6和7识别)。


## 2.IE6不识别高度小于10px的容器
#### 问题描述
浏览器认为容器可以放置的最小字体就是10px,因此只要是容器，那么就不会大于10px，小于10px的就默认是10px;(也就是说在IE6中是根据字体的大小确定了盒子的最小高度)
#### 解决方案1
浏览器根据最小字体来确定了容器的高度,那么将容器的```font-size:0```
### 解决方案2
给容器设置```overflow:hidden```

## 3.IE中```<a>```标签嵌套```<img>```标签时图片会产默认的边框
#### 问题描述
IE解析是为了区别有链接和没有链接的图片因此加上了边框，在实际的生成中我们经常是不需要这样的样式。
#### 解决方案
给图片设置```border:none```。

## 4.IE6 不能识别min-height属性
#### 问题描述：
由于css属性```min-height```的兼容问题，不能很好的被各个浏览器兼容,（当内容高度小于某个值得时候，容器高度就是最小的值，当超过这个值的时候，会自动的撑开这个，而不是出现滚动条。
#### 解决方案1
hack方案给IE设置高度，```min-height:100px```设置```_height:100px```或者```*height:100px;```
#### 解决方案2
```min-height:100px;height:auto!importent;height:100px```IE6不识别important。

## 5.透明度问题IE8不支持opcity属性
#### 解决方案
```opacity:0.5;filter:alpha(opacity=60)```;注意这里对应的数值是0-100

## 6.鼠标指针问题
#### 问题描述
在IE8以及一下的浏览器中不支持cursor:pointer属性
#### 解决方案
```cursor:pointer;cursor:hand;```

## 7.IE6中比分比bug
#### 问题描述
父元素设置宽度100%,子元素宽度为50%在IE6中两个50%大于100%。
#### 解决方案
给左边浮动的元素添加```clear:right```。

## 8.图片默认的间隙(3px)
#### 问题描述
图片默认底部是有3px的间隙， 产生原因：主要是因为图片的垂直对齐方式```vertical-align```引发的，默认值是```baseline```，默认为此值时图片下方就会多出3px
#### 解决方案1
将图片的```veritcal-align:bottom```。
#### 解决方案2
由于是```vertical-align```属性造成的那么使这个属性失效即可。设置```display:block```。

## 9.表单元素行高不一致问题
#### 解决方案1
给表单元素都添加上```vertical-align:middle```。
#### 解决方案2
给表单元素添加浮动属性```float```。