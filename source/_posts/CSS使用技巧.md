---
title: CSS使用技巧
date: 2019-01-02 20:38:29
tags: 学习笔记
categories: IT
---

本篇文章主要介绍CSS技巧如下：
* 左右布局
* 左中右布局
* 水平居中
* 垂直居中
<!-- more -->

---
#  左右布局
## float实现
float属性是css中关于布局的一个关键属性，其意为将该块状区域脱离父级标签的文档流，left属性值使该区域向父级标签区域的左侧边界放置，right属性值使该区域块向父级标签的右侧边界放置，如是利用该属性可以实现左右布局。 float属性属于布局属性，其中有着很多重要应用。

>float属性的三个特性为：
>1. 包裹性：可以按照区域块中子元素的实际宽度进行包裹；
>2. 破坏性：float区域块不会被父级区域块包裹，造成前端常见的高度塌陷问题，解决办法是清除浮动；
>3. 占位性（个人称呼），浮动区域块虽然是脱离了父级区域，但是它是要占用一定的正常流区域的，即如果不清除浮动，我们会看到它会占用它后面的同级元素（如果没有会占用它父级后面的同级元素，如果还是没有则向上追溯）的区域，影响同级元素，所以常见清浮动。
   
实现代码：
```
<style>
.clearfix::after {
	content: '';
	display: block;
	clear: both;
}

.wrap{
    float:left;
}

</style>
----------------------------------------------
<section class="section clearfix">
    <div class="wrap">
        <div class="col-4 c1">1</div>
        <div class="col-4 c2">2</div>
        <div class="col-4 c3">3</div>
        <div class="col-4 c4">4</div>
    </div>
    <div class="wrap">
        <div class="col-4 c5">5</div>
        <div class="col-4 c6">6</div>
    </div>
</section>

```
> 代码说明：
> 利用float可以实现`1234`和`56`横向排列

---
# 左中右布局
## float 实现
次布局依旧可以使用上节方法，不过需要调整每个元素中间的间隔,实现代码：
```
<style>
.clearfix::after {
	content: '';
	display: block;
	clear: both;
}

.wrap{
    float:left;
    margin-left：50px；
}

</style>
----------------------------------------------
<section class="section clearfix">
    <div class="wrap">
        <div class="col-4 c1">1</div>
        <div class="col-4 c2">2</div>
    </div>
    <div class="wrap">
        <div class="col-4 c3">3</div>
        <div class="col-4 c4">4</div>
    </div>
    <div class="wrap">
        <div class="col-4 c5">5</div>
        <div class="col-4 c6">6</div>
    </div>
</section>
```

---
# 水平居中
水平居中对于不同类型的元素使用的方法也不一样

## 行内元素
行内元素（主要是表现为文字，图片等行内元素），通过在父级元素设置 text-align:center 使子级行内元素居中。

## 定宽块级元素
浮动块级元素，随后定宽，中间的元素会居中。定宽块级元素设置：
```
 margin-left:auto;
 margin-right:auto;
```
## 不定宽块级元素

1. 加入 table 标签
   
>将元素用 table 标签包裹起来，包括 tbody、tr、td，但这种方法为了居中增加了无语义的标签。

```
<style>
table{
    margin:0 auto;
}
ul{
    list-style:none;
    margin:0;
    padding:0;
}
li{
    float:left;
    margin-right:8px;
}
</style>
----------------------------------------------
<div>
  <table>
    <tbody>
      <tr>
        <td>
           <ul>
              <li><a href="#">我是要</a></li>
              <li><a href="#">居中的</a></li>
              <li><a href="#">ul标签</a></li>
           </ul>
        </td>
      </tr>
    </tbody>
  </table>
</div>
```

2. 设置 display:inline 方法
   
> 设置为 inline 行内元素后沿用行内元素居中的方法，这种方法改变了元素的 display 样式

```

<style>
div{
    text-align:center;
}
ul{
    list-style:none;
    margin:0;
    padding:0;
    display:inline;
}
li{
    display:inline;
    margin-right:8px;
}
</style>
----------------------------------------------
<div>
    <ul>
       <li><a href="#">我是要</a></li>
       <li><a href="#">居中的</a></li>
       <li><a href="#">ul标签</a></li>
  </ul>
</div>
```

---
# 垂直居中
## 通过line-height实现
>设置子元素的line-height值等于父元素的height，这种方法适用于子元素为行内元素的情况。

```
<style>
#out{
    height:300px
}
#in{
    height:50%;
    line-height:300px
}
</style>
----------------------------------------------
<div id="out">
    <p id="in">CSS垂直</p>
</div>
```

---
# 重点：flex！！！
布局的传统解决方案，基于盒状模型，依赖 display 属性 + position属性 + float属性。它对于那些特殊布局非常不方便，比如，垂直居中就不容易实现。

2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。

## 基本概念
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为 Flex 布局。
{% asset_img bg2015071004.png flexitem %}
容器默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）。主轴的开始位置（与边框的交叉点）叫做main start，结束位置叫做main end；交叉轴的开始位置叫做cross start，结束位置叫做cross end。

项目默认沿主轴排列。单个项目占据的主轴空间叫做main size，占据的交叉轴空间叫做cross size。

## 容器的属性
* `flex-flow`属性是`flex-direction`属性和`flex-wrap`属性的简写形式，默认值为`row nowrap`
>此属性前半部分决定水平排列还是垂直列，后半部分决定是否换行

{% asset_img bg2015071005.png flex-flow %}

    row（默认值）：主轴为水平方向，起点在左端。
    row-reverse：主轴为水平方向，起点在右端。
    column：主轴为垂直方向，起点在上沿。
    column-reverse：主轴为垂直方向，起点在下沿

* `justify-content`属性定义了项目在主轴上的对齐方式。
>实现水平居中

{% asset_img bg2015071010.png flexitem %}

    flex-start（默认值）：左对齐
    flex-end：右对齐
    center： 居中
    space-between：两端对齐，项目之间的间隔都相等。
    space-around：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

* `align-items`属性定义项目在交叉轴上如何对齐。
>实现垂直居中

{% asset_img bg2015071011.png flexitem %}

    flex-start：交叉轴的起点对齐。
    flex-end：交叉轴的终点对齐。
    center：交叉轴的中点对齐。
    baseline: 项目的第一行文字的基线对齐。
    stretch（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

更多应用和详细写法请看阮一峰博客：http://www.ruanyifeng.com/blog/2015/07/flex-examples.html