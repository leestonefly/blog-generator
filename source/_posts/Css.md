---
title: Css
date: 2018-12-28 10:54:56
tags: 作业
---

简单介绍了下Css内容

<!-- more -->
# CSS概述
## 引用CSS的4种方法
* 直接在html文件dom标签后面加入style=""属性
* 在html文件head标签加入`<style></style>`
* 在html文件head标签中利用`<link>`的`src`来引用css文件
* 在css文件中利用`@import " "`来引用css文件

<hr>

## 选择器

选择器是 CSS 规则的一部分且位于 CSS 声明块前。
选择器可以被分为以下几类：

* 简单选择器（Simple selectors）：通过元素类型、class 或 id 匹配一个或多个元素。
  
* 属性选择器（Attribute selectors）：通过 属性 / 属性值 匹配一个或多个元素。
  
* 伪类（Pseudo-classes）：匹配处于确定状态的一个或多个元素，比如被鼠标指针悬停的元素，或当前被选中或未选中的复选框，或元素是DOM树中一父节点的第一个子节点。

* 伪元素（Pseudo-elements）:匹配处于相关的确定位置的一个或多个元素，例如每个段落的第一个字，或者某个元素之前生成的内容。 

* 组合器（Combinators）：这里不仅仅是选择器本身，还有以有效的方式组合两个或更多的选择器用于非常特定的选择的方法。例如，你可以只选择divs的直系子节点的段落，或者直接跟在headings后面的段落。

* 多重选择器（Multiple selectors）：这些也不是单独的选择器；这个思路是将以逗号分隔开的多个选择器放在一个CSS规则下面， 以将一组声明应用于由这些选择器选择的所有元素。
  
>选择器可以让你自由的选择你所要更改的元素，灵活使用它，你可以实现很多特效，比如鼠标移动上去变色，点击下凹等

<hr>

## 模型框

模型框有3种类型，我们可以通过display属性来设定元素的框类型。display属性有很多的属性值。在本篇文章，我们将关注三个最常见的类型：block, inline, and inline-block。

* 块框（ block box）是定义为堆放在其他框上的框（例如：其内容会独占一行），而且可以设置它的宽高，之前所有对于框模型的应用适用于块框 （ block box）
{% asset_img box-model-alt-small.png block %}

* 行内框（ inline box）与块框是相反的，它随着文档的文字流动（例如：它将会和周围的文字和其他行内元素出现在同一行，而且它的内容会像一段中的文字一样随着文字部分的流动而打乱），对行内盒设置宽高无效，设置padding, margin 和 border都会更新周围文字的位置，但是对于周围的的块框（ block box）不会有影响。
  {% asset_img box-model-standard-small.png inline %}

* 行内块状框（inline-block box） 像是上述两种的集合：它不会重新另起一行但会像行内框（ inline box）一样随着周围文字而流动，而且他能够设置宽高，并且像块框一样保持了其块特性的完整性，它不会在段落行中断开。（在下面的示例中，行内块状框会放在第二行文本上，因为第一行没有足够的空间，并且不会突破两行。然而，如果没有足够的空间，行内框会在多条线上断裂，而它会失去一个框的形状。）
>注意：默认状态下display属性值，块级元素display: block ，行内元素display: inline

<hr>

## CSS 图形技巧
通过使用CSS模型框技巧，可以实现多种图形的绘制

{% asset_img images.jpg image %}

详情请看https://css-tricks.com/the-shapes-of-css/

<hr>

## text 与 box 
CSS俩个最基础的样式是`行内元素`text与`块级元素`box，早期我们通过这两种样式的混合使用,从而达成了网页最基础的显示方式。

* text默认是横向排列，主要标签有`<p>` `<span>`等 height和weight无效
* box默认是占满宽度纵向排列，主要标签有`<div>` 等 weight有效，但也不会令下一个box元素横向排列。
  
当我们想让box类横向排列的时候，早期方法就是在box类兄弟元素使用`float：left`并在兄弟元素的末尾或者上一个父级元素利用拟元素::after 加入一个clearfix
```
.clearfix::after {
    content: '';
    display: block;
    clear: both;
}
```


--- 
# CSS 布局 
position、float、display这三个属性影响页面各个元素的整体布局

## float
float 是最简单的页面元素定位，他可以将元素进行浮动，类似于word排版中图片的浮动，他有4种可能的值：
* left — 将元素浮动到左侧。
* right — 将元素浮动到右侧。
* none — 默认值, 不浮动。
* inherit — 继承父元素的浮动属性。

> 浮动一般运用在兄弟元素中

<hr>

## position
position 是用于定位的，允许我们精准的将元素移动到一个位置

他有四种主要的定位方式：
* 静态定位(`Static`)是每个元素默认的属性——它表示“将元素放在文档布局流的默认位置——没有什么特殊的地方”。
  
* 相对定位(`Relative`)允许我们相对元素在正常的文档流中的位置移动它——包括将两个元素叠放在页面上。  这对于微调和精准设计(design pinpointing)非常有用。
  
* 绝对定位(`Absolute`)将元素完全从页面的正常布局流中移出，类似将它单独放在一个图层中.   我们可以将元素相对于页面的 <html> 元素边缘固定，或者相对于离元素最近的被定位的祖先元素(ancestor element)。  绝对定位在创建复杂布局效果时非常有用，例如通过标签显示和隐藏的内容面板或者通过按钮控制滑动到屏幕中的信息面板.
  
* 固定定位(`Fixed`)与绝对定位非常类似，除了它是将一个元素相对浏览器视口固定，而不是相对另外一个元素。 在创建类似页面滚动总是处于页面上方的导航菜单时非常有用。
<hr>

## display

我们一般常用的display 主要就是`inline` 、`block`、 `inline-block`、 `flex`等，
灵活应用我们就可以基本解决所有的常见排版问题，具体display的用法与分类如下：

1.  `<display-outside>`

    这些关键字指定了元素的外部显示类型，实际上就是其在流式布局中的角色。
```
display: block;
display: inline;
display: run-in;
```

2.  `<display-inside>`

    这些关键字指定了元素的内部显示类型，它们定义了元素内部内容的格式化上下文的类型（假设是不可替换的元素）。
 ```
display: flow;
display: flow-root;
display: table;
display: flex;
display: grid;
display: ruby;
```
3.  `<display-listitem>`
    将这个元素的外部显示类型变为 block 盒，并将内部显示类型变为多个 list-item inline 盒。
```
display: list-item;
display: list-item block;
display: list-item inline;
display: list-item flow;
display: list-item flow-root;
display: list-item block flow;
display: list-item block flow-root;
display: flow list-item block;
```
4.  `<display-internal>`
像 table 和 ruby 这样的布局模型有着复杂的内部结构，因此它们的孩子和后面的元素可能具有多个角色。这一类关键字就是用来定义这些“内部”显示类型，并且只有在这些特定的布局模型中才有意义。
```
display: table-row-group;
display: table-header-group;
display: table-footer-group;
display: table-row;
display: table-cell;
display: table-column-group;
display: table-column;
display: table-caption;
display: ruby-base;
display: ruby-text;
display: ruby-base-container;
display: ruby-text-container;
```
5.  `<display-box>`
这些值定义元素是否完全生成显示盒。
```
display: contents;
display: none;
```

6.  `<display-legacy>`
CSS 2 对于 display 属性使用单关键字语法, 对于相同布局模式的 block 级和 inline 级变体需要使用单独的关键字。
```
display: inline-block;
display: inline-table;
display: inline-flex;
display: inline-grid;
```
>这些属性看上去很多很复杂，但是我们常用的实际上只有flex，这个属性可以让我们基本实现所有的简单或者复杂的布局需求。
--- 