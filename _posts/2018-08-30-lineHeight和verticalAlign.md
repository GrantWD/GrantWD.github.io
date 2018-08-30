---
layout: post
title: 'line-height和vertical-align的应用'
subtitle: 'line-height和vertical-align的应用'
date: 2018-08-30
categories: 对齐
tags: CSS
---
## line-height
```line-height```可以设置带有长度单位或者一个无单位的值，默认是n```ormal```。没有单位的line-height是相对于```font-size```的大小的，但是问题是```font-size:50px```;的大小在使用不同的字体表现行为是不一样的，因此```line-height```在使用不同的字体也是不一样的	


#### font-family
1. 字体定义其```em-square```,每个字符将会绘制出自己的容器。这个正方形使用相对单位和生成一个1000单位，也可以是1024，2048等等
2. 根据其单位，字体的度量可以根据一些设置来决定(ascender,descender,capital height,x-height),这里有些值是em-square之外的值。
3. 在浏览器中，相对单位是用于缩放用来适应所需的font-size

#### line-height的问题
conten-area和line-box,line-box的高度是根据子元素的高度来计算的，但是并不是子元素的内内容区域(content-area)的高度。

内联元素有两个不同的高度内容区域(content-area)和虚拟高度区域(virtual-area)
1.内容区域的高度有字体来决定
2.虚拟区域高度是line-height,他的高度用来计算line-box的高度

#### vertcal-align:middle
由于基线的比例不同以及x-height比例，所以中间对齐是不可靠的，有时可以利用其它的值来确定对齐vertical-aling:top | bottom和line-box的顶部或者底部对齐
vertical-align-align:text-top|text-bottom和内容区的顶部或底部对齐

