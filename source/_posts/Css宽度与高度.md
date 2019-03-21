---
title: Css宽度与高度
date: 2019-03-21 10:17:39
tags: 学习笔记
categories: IT
---
# 文档流

## div的宽高
div 默认display为block默认横向排列；span默认为inline默认撑开横向空格，纵向排列；

如果想更改div的高度和宽度，尽量不要直接设置固定长度；

可以采用inline-block 类型进行调试，字体会影响文档流的高度，更改字体大小（`line-height:`）可以改变div或span的高度

一个单词过长会溢出，可以使用word-break:break-all;进行强制换行。下列代码可以只显示两行，剩下的省略；
```css
display:-webkit-box；
-webkit-line-clamp:2;
-webkit-box-orient:vertical;
overflow:hidden;
```

div的宽度不是由内联文字所决定的，div的高度是由内部文档流中的元素的总和来决定的

文字的居中应合理使用padding
## margin 合并
如果父元素没有内容（padding/border）挡住margin，子元素的margin会与父元素的margin合并；
