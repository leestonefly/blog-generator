---
title: jQuery是如何实现的
date: 2019-02-27 11:16:40
tags: 学习笔记
categories: IT
---
# 概述
jQuery是一套跨浏览器的JavaScript库，简化HTML与JavaScript之间的操作。

由`约翰·雷西格（John Resig）`在2006年1月的BarCamp NYC上发布第一个版本。
<!-- more -->
jQuery有下列特色：

* 使用多浏览器开源选择器引擎Sizzle（jQuery项目的派生产品）进行DOM元素选择
* 基于CSS选择器的DOM操作，使用元素的名称和属性（如id和class）作为选择DOM中节点的条件
* 事件
* 特效和动画
* Ajax
* Deferred和Promise对象来控制异步处理
* JSON解析
* 通过插件扩展
* 工具函数，如特征检测
* 现代浏览器中本地的兼容性方法，但对于旧版浏览器需要后备（fallback）方法，比如inArray()和each()
* 多浏览器（不要与跨浏览器混淆）支持
---
# jQuery 是如何实现的
## 封装函数

首先，我们封装两个功能函数
```javascript
function getSiblings(node) {
    let allChildren = node.parentNode.children;
    let array = {length: 0};
    for (let i = 0; i < allChildren.length; i++) {
        if (allChildren[i] !== node) {
            array[array.length] = allChildren[i];
            array.length += 1;
        }
    }
    return array;
}

function addClass(node, classes) {
    for (let key in classes) {
        let value = classes[key];
        let methodName = value ? 'add' : 'remove';
        node.classList[methodName](key);
    }
}

//调用方法

var dom = {};
dom.getSiblings(node);
dom.addClass(node,{a:true,b:false});
```

getSiblings函数用来获取当前函数的兄弟元素，并生成一个伪数组，addClass函数用来给节点添加一个类。

## 将封装函数放在Node原型中

```javascript
Node.prototype.getsiblings = function () {
    let allChildren = this.parentNode.children;
    let array = {length: 0};
    for (let i = 0; i < allChildren.length; i++) {
        if (allChildren[i] !== this) {
            array[array.length] = allChildren[i];
            array.length += 1;
        }
    }
    return array;
};

Node.prototype.addClass = function (classes) {
    classes.forEach((value) => this.classList.add(value))
};

//调用方法
var node = querySelector('div');
node.getsiblings();
node.addClass();

```
此时，我们就可以直接获取节点对象，利用节点调用编译函数。

## 使用新的接口
```javascript
// window.Node2

window.Node2 = function (nodeOrselector) {
    let node;
    if (typeof nodeOrselector === 'string') {
        node = document.querySelector(nodeOrselector);
    } else {
        node = nodeOrselector;
    }

    return {
        getSiblings: function () {
            let allChildren = node.parentNode.children;
            let array = {length: 0};
            for (let i = 0; i < allChildren.length; i++) {
                if (allChildren[i] !== node) {
                    array[array.length] = allChildren[i];
                    array.length += 1;
                }
            }
            return array;
        },
        addClass: function (classes) {
            classes.forEach((value) => node.classList.add(value))
        }
    }
};

//调用方式

var node =document.getElementById('xxx');
var node2 = Node2(node);
node2.getSiblings();
node2.addClass();

```

这种方法避免了对原型的污染

## 将Node2改为jQuery

```javascript

window.jQuery = function (nodeOrSelector) {
    let nodes;
    if (typeof nodeOrSelector === 'string') {
        let temp = document.querySelectorAll(nodeOrSelector);
        for (let i = 0; i < temp.length; i++) {
            nodes[i] = temp[i];
        }
        nodes.length = temp.length;
    } else if (nodeOrSelector instanceof Node) {
        nodes = {
            0: nodeOrSelector,
            length: 1
        }
    }
    nodes.getSiblings = function () {
        let allChildren = node.parentNode.children;
        let array = {length: 0};
        for (let i = 0; i < allChildren.length; i++) {
            if (allChildren[i] !== node) {
                array[array.length] = allChildren[i];
                array.length += 1;
            }
        }
        return array;
    };
    nodes.addClass = function (classes) {
        classes.forEach((value) => {
                for (let i = 0; i < nodes.length; i++) {
                    nodes[i].classList.add(value);
                }
            }
        )
    };
    nodes.getText = function () {
        let texts = [];
        for (let i = 0; i < nodes.length; i++) {
            texts.push(nodes[i].textContent)
        }
        return texts;
    };
    nodes.setText = function (text) {
        for (let i = 0; i < nodes.length; i++) {
            nodes[i].textContent = text;
        }
    };
    nodes.text = function (text) {
        if (text === undefined) {
            let texts = [];
            for (let i = 0; i < nodes.length; i++) {
                texts.push(nodes[i].textContent)
            }
            return texts;
        } else {
            for (let i = 0; i < nodes.length; i++) {
                nodes[i].textContent = text;
            }
        }

    };
    return nodes;
};


//再缩写一下
window.$ = jQuery;

// 调用方式

$('div').addClass('red');
$('div').setText('hi');
```
利用封装的方式，将原生的DOM方法转变成了更容易书写理解的形式。
