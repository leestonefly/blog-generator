---
title: Javascript语法
date: 2019-01-24 14:18:27
tags: 学习笔记
---
> 学习资源：http://javascript.ruanyifeng.com/


# 基本语法
## 语句
JavaScript 程序的执行单位为行（line），也就是一行一行地执行。一般情况下，每一行就是一个语句。
语句（statement）是为了完成某种任务而进行的操作，比如下面就是一行赋值语句。
```
    var a = 1 + 3;
```

`1 + 3`叫做表达式（expression），指一个为了得到返回值的计算式。语句和表达式的区别在于，前者主要为了进行某种操作，一般情况下不需要返回值；后者则是为了得到返回值，一定会返回一个值。凡是 JavaScript 语言中预期为值的地方，都可以使用表达式。比如，赋值语句的等号右边，预期是一个值，因此可以放置各种表达式。

语句以分号结尾，一个分号就表示一个语句结束。多个语句可以写在一行内。

## 变量
变量是对“值”的具名引用。变量就是为“值”起名，然后引用这个名字，就等同于引用这个值。变量的名字就是变量名。
> 注意，JavaScript 的变量名区分大小写，A和a是两个不同的变量。

### 变量提升
JavaScript 引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。

### 命名规则
* 第一个字符，可以是任意 Unicode 字母（包括英文字母和其他语言的字母），以及美元符号（$）和下划线（_）。
* 第二个字符及后面的字符，除了 Unicode 字母、美元符号和下划线，还可以用数字0-9。
  
> JavaScript有一些保留字，不能用作标识符：arguments、break、case、catch、class、const、continue、debugger、default、delete、do、else、enum、eval、export、extends、false、finally、for、function、if、implements、import、in、instanceof、interface、let、new、null、package、private、protected、public、return、static、super、switch、this、throw、true、try、typeof、var、void、while、with、yield。

## 注释
源码中被 JavaScript 引擎忽略的部分就叫做注释，它的作用是对代码进行解释。Javascript 提供两种注释的写法：一种是单行注释，用//起头；另一种是多行注释，放在/* 和 */之间。
此外，由于历史上 JavaScript 可以兼容 HTML 代码的注释，所以<!--和-->也被视为合法的单行注释。

<!-- more -->
# 数据类型

# 数值

# 字符串

# 对象

# 数组

# 函数

# 运算符

# 数据类型

# 数据类型转换

# 错误处理机制

# 编程风格



---

---

---