---
title: JavaScript语法
date: 2019-01-24 14:18:27
tags: 学习笔记
categories: IT
---

> 学习资源：http://javascript.ruanyifeng.com/

---
<!-- more -->
# 语句
JavaScript 程序的执行单位为行（line），也就是一行一行地执行。一般情况下，每一行就是一个语句。
语句（statement）是为了完成某种任务而进行的操作，比如下面就是一行赋值语句。
```
    var a = 1 + 3;
```

`1 + 3`叫做表达式（expression），指一个为了得到返回值的计算式。语句和表达式的区别在于，前者主要为了进行某种操作，一般情况下不需要返回值；后者则是为了得到返回值，一定会返回一个值。凡是 JavaScript 语言中预期为值的地方，都可以使用表达式。比如，赋值语句的等号右边，预期是一个值，因此可以放置各种表达式。

语句以分号结尾，一个分号就表示一个语句结束。多个语句可以写在一行内。
--- 

# 变量
变量是对“值”的具名引用。变量就是为“值”起名，然后引用这个名字，就等同于引用这个值。变量的名字就是变量名。
> 注意，JavaScript 的变量名区分大小写，A和a是两个不同的变量。

## 变量提升
JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。

## 标识符

标识符（identifier）指的是用来识别各种值的合法名称。最常见的标识符就是变量名，以及后面要提到的函数名

* 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（$）和下划线（_）。
* 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字0-9。
  
> JavaScript有一些保留字，不能用作标识符：arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield。

---

# 注释
源码中被 JavaScript 引擎忽略的部分就叫做注释，它的作用是对代码进行解释。

Javascript 提供两种注释的写法：
* 一种是单行注释，用//起头；
* 另一种是多行注释，放在/* 和 */之间。

此外，由于历史上 JavaScript 可以兼容 HTML 代码的注释，所以`<!--`和`-->`也被视为合法的单行注释。

需要注意的是，–>只有在行首，才会被当成单行注释，否则会当作正常的运算。
```
function countdown(n) {
  while (n --> 0) console.log(n);
}
countdown(3)
// 2
// 1
// 0
```
---

# 区块

JavaScript 使用大括号，将多个相关的语句组合在一起，称为“区块”（block）。

对于var命令来说，JavaScript 的区块不构成单独的作用域（scope）。函数内的区块才能形成单独的作用域。

在 JavaScript 语言中，单独使用区块并不常见，区块往往用来构成其他更复杂的语法结构，比如for、if、while、function等。
---

# 条件语句

## if...else

`if`代码块后面，还可以跟一个`else`代码块，表示不满足条件时，所要执行的代码。
```
if (m === 3) {
  // 满足条件时，执行的语句
} else {
  // 不满足条件时，执行的语句
}
```
## switch

多个`if...else`连在一起使用的时候，可以转为使用更方便的`switch`结构。
```
switch (fruit) {
  case "banana":
    // ...
    break;
  case "apple":
    // ...
    break;
  default:
    // ...
}
```
## 三元运算符 ?

三元运算符（即该运算符需要三个运算子）`?:`，也可以用于逻辑判断
```
(条件) ? 表达式1 : 表达式2
```
上面代码中，如果“条件”为true，则返回“表达式1”的值，否则返回“表达式2”的值。
---

# 循环语句

## while

`While`语句包括一个循环条件和一段代码块，只要条件为真，就不断循环执行代码块。

## for

`for`语句是循环命令的另一种形式，可以指定循环的起点、终点和终止条件。
```
for (初始化表达式; 条件; 递增表达式) {
  语句
}
```

## do...while

`do…while`循环与`while`循环类似，唯一的区别就是先运行一次循环体，然后判断循环条件.

不管条件是否为真，`do…while`循环至少运行一次，这是这种结构最大的特点。另外，`while`语句后面的分号注意不要省略。

## break 语句和 continue 语句

`break`语句和`continue`语句都具有跳转作用，可以让代码不按既有的顺序执行。

`break` 是直接终止循环，`continue` 是 跳过本次循环后面的代码，进入下一个循环。

## 标签（label）
JavaScript 语言允许，语句的前面有标签（label），相当于定位符，用于跳转到程序的任意位置，标签的例子如下。
```
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) break top;
      console.log('i=' + i + ', j=' + j);
    }
  }
// i=0, j=0
// i=0, j=1
// i=0, j=2
// i=1, j=0
```
上面代码为一个双重循环区块，`break`命令后面加上了`top`标签（注意，top不用加引号），满足条件时，直接跳出双层循环。如果`break`语句后面不使用标签，则只能跳出内层循环，进入下一次的外层循环。
```
top:
  for (var i = 0; i < 3; i++){
    for (var j = 0; j < 3; j++){
      if (i === 1 && j === 1) continue top;
      console.log('i=' + i + ', j=' + j);
    }
  }
// i=0, j=0
// i=0, j=1
// i=0, j=2
// i=1, j=0
// i=2, j=0
// i=2, j=1
// i=2, j=2
```
上面代码中，`continue`命令后面有一个标签名，满足条件时，会跳过当前循环，直接进入下一轮外层循环。如果`continue`语句后面不使用标签，则只能进入下一轮的内层循环。
---