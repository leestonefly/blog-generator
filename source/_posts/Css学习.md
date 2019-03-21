---
title: Css学习
date: 2019-03-11 10:31:54
tags: 学习笔记
categories: IT
---
# CSS 学习的难点
CSS 一开始设计出来的时候并没有想到大家会这么依赖 CSS，所以设计的时候想得特别简单：你要什么功能我就加什么属性。

你要颜色，就有 color: red; background-color: red;
你要图文混排，就有 float: left
你要绝对定位，就有 position: absolute

虽然 CSS 有一些核心概念，还是我们主要接触的还是一些表面的「技巧」，比如如何布局、如何做出一个小效果。
即使你不了解核心概念，也能把效果搞（抄）出来。

原因很简单：写 CSS 不需要复杂的逻辑。
如果你看见别人用 CSS 写出了一个五角星，那么你只要抄到你的页面里，同样的样式，那么你也有一个五角星。

这就使得很多人不打算深入了解 CSS。

---
# 如果你不深入了解 CSS
如果你不深入了解 CSS，那么你会发现 CSS 不正交，因而有些反直觉。不正交主要表现在两点：

1. 各属性之间互相影响

* margin V.S. border
* 小圆点 V.S. display
* position: absolute V.S. display: inline

>display:flex,display:table 会阻断margin的相互覆盖；
>outline在显示中，如果子元素margin超过了父元素的大小，只会将子元素和父元素向下平移，父元素没有包裹子元素的margin；若父元素加入一个border，padding，display:###，overflow，父元素就会包裹子元素；
>display会影响`<li>`的小圆点；
>子元素有display:inline或inline-block，默认会出现在父元素内的左上角，但是在父元素上加入position:relative,子元素加上position:absolute后，子元素的display会变为bolck；



2. 各元素之间互相影响

* position: fixed V.S. transform
>transform会将fixed相对父级定位，不对窗口定位；
* float 影响 inline 元素
>文字会被float元素影响；
---
# CSS 学习的易点
1. 背套路即可应付日常工作
* 水平居中
>float和flex
* 垂直居中
>block 可以用auto；inline可以使用 t-a:center;table;

1. 巧用工具
* CSS 3 Generator