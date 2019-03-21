---
title: DOM API
date: 2019-02-25 08:55:21
tags: 学习笔记
categories: IT
---
> 学习资源：https://wangdoc.com/javascript

---

# Node节点
Node 分为 Document（html）、Element（元素）和 Text（文本），以及其他不重要的。

通过实验，发现DOM树的结构和JS的数据结构之间有非常类似的结构
{% asset_img window.png [结构图] %}
<!-- more -->
# Node 的接口
## 属性

childNodes,firstChild,innerText,lastChild,nextSibling,nodeName,nodeType,nodeValue,outerText,ownerDocument,parentElement,parentNode,previousSibling,textContent

妈的记不住。
如果记不住就背下以下单词：

* child / children / parent
* node
* first / last
* next / previous
* sibling / siblings
* type
* value / text / content
* inner / outer
* element
然后互相组合

## 方法
（如果一个属性是函数，那么这个属性就也叫做方法；换言之，方法是函数属性）

* appendChild()
* cloneNode()
* contains()
* hasChildNodes()
* insertBefore()
* isEqualNode()
* isSameNode()
* removeChild()
* replaceChild()
* normalize() // 常规化
搞清楚英文单词的意思就知道用法

如果发现知道英文后依然不明白用法，看 MDN 的例子即可，如 normalize

DOM APi 无外乎「增删改查」

# Document 接口
## 属性

* anchors
* body
* characterSet
* childElementCount
* children
* doctype
* documentElement
* domain
* fullscreen
* head
* hidden
* images
* links
* location
* onxxxxxxxxx
* origin
* plugins
* readyState
* referrer
* scripts
* scrollingElement
* styleSheets
* title
* visibilityState

## 方法：

* close()
* createDocumentFragment()
* createElement()
* createTextNode()
* execCommand()
* exitFullscreen()
* getElementById()
* getElementsByClassName()
* getElementsByName()
* getElementsByTagName()
* getSelection()
* hasFocus()
* open()
* querySelector()
* querySelectorAll()
* registerElement()
* write()
* writeln()

# Element 的接口

DOM API 反人类
获取元素
以前之后 document.getElementById, document.getElementsByTagName, document.getElementsByClassName

太反人类，于是有了 jQuery

后来 DOM API 终于抄袭 jQuery 提供了 document.querySelector 和 document.querySelectorAll

但是依然没有 jQuery 好用，因为「不一致」


# 避免使用全局变量
因为声明全局变量容易导致变量之间的覆盖问题。避免这个问题的方法如下：
1. 避免使用全局变量命名
2. 使用函数作用域包裹命名
3. 立即调用函数