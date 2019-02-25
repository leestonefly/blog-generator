---
title: JavaScript里的数据类型
date: 2019-02-12 11:11:55
tags: 学习笔记
categories: IT
---
> 学习资源：https://wangdoc.com/javascript

---
<!-- more -->
# 概述 

JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有六种。（ES6 又新增了第七种 Symbol 类型的值）

* 数值（number）：整数和小数（比如1和3.14）
* 字符串（string）：文本（比如Hello World）。
* 布尔值（boolean）：表示真伪的两个特殊值，即true（真）和false（假）
* undefined：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
* null：表示空值，即此处的值为空。
* 对象（object）：各种值组成的集合。

通常，数值、字符串、布尔值这三种类型，合称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。对象则称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于undefined和null，一般将它们看成两个特殊值。

对象是最复杂的数据类型，又可以分成三个子类型。

* 狭义的对象（object）
* 数组（array）
* 函数（function）
  
狭义的对象和数组是两种不同的数据组合方式，除非特别声明，本教程的“对象”都特指狭义的对象。

函数其实是处理数据的方法，JavaScript 把它当成一种数据类型，可以赋值给变量，这为编程带来了很大的灵活性，也为 JavaScript 的“函数式编程”奠定了基础。

---

# null, undefined 和 boolean
## null 和 undefined
当变量a分别被赋值为undefined和null，这两种写法的效果几乎等价。

>在if语句中，它们都会被自动转为false，相等运算符（==）甚至直接报告两者相等。

设计者为了避免在运算过程中`null`被自动转换成0而使一些错误难以发现，因此，又设计了一个undefined。undefined是一个表示"此处无定义"的原始值，转为数值时为NaN。

undefined例子如下：
```
// 变量声明了，但没有赋值
var i;
i // undefined

// 调用函数时，应该提供的参数没有提供，该参数等于 undefined
function f(x) {
  return x;
}
f() // undefined

// 对象没有赋值的属性
var  o = new Object();
o.p // undefined

// 函数没有返回值时，默认返回 undefined
function f() {}
f() // undefined
```
## Boolean
布尔值代表“真”和“假”两个状态。“真”用关键字true表示，“假”用关键字false表示。布尔值只有这两个值。

下列运算符会返回布尔值：

* 前置逻辑运算符： ! (Not)
* 相等运算符：===，!==，==，!=
* 比较运算符：>，>=，<，<=
* 
如果 JavaScript 预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为false，其他值都视为true。

* undefined
* null
* false
* 0
* NaN
* ""或''（空字符串）

> 空数组（[]）和空对象（{}）对应的布尔值，都是true
--- 
# 数值
## 整数和浮点数
JavaScript 内部，所有数字都是以64位浮点数形式储存，即使整数也是如此。所以，1与1.0是相同的，是同一个数。

由于浮点数不是精确的值，所以涉及小数的比较和运算要特别小心。
```
0.1 + 0.2 === 0.3
// false

0.3 / 0.1
// 2.9999999999999996

(0.3 - 0.2) === (0.2 - 0.1)
// false
```
## 数值精度
根据国际标准 IEEE 754，JavaScript 浮点数的64个二进制位，从最左边开始，是这样组成的。

* 第1位：符号位，0表示正数，1表示负数
* 第2位到第12位（共11位）：指数部分
* 第13位到第64位（共52位）：小数部分（即有效数字）
符号位决定了一个数的正负，指数部分决定了数值的大小，小数部分决定了数值的精度。

指数部分一共有11个二进制位，因此大小范围就是0到2047。IEEE 754 规定，如果指数部分的值在0到2047之间（不含两个端点），那么有效数字的第一位默认总是1，不保存在64位浮点数之中。也就是说，有效数字这时总是1.xx...xx的形式，其中xx..xx的部分保存在64位浮点数之中，最长可能为52位。因此，JavaScript 提供的有效数字最长为53个二进制位。

## 数值范围
根据标准，64位浮点数的指数部分的长度是11个二进制位，意味着指数部分的最大值是2047（2的11次方减1）。也就是说，64位浮点数的指数部分的值最大为2047，分出一半表示负数，则 JavaScript 能够表示的数值范围为2^1024到2^-1023（开区间），超出这个范围的数无法表示。

如果一个数大于等于2的1024次方，那么就会发生“正向溢出”，即 JavaScript 无法表示这么大的数，这时就会返回`Infinity`。

## 数值的进制与标识方法
JavaScript 的数值有多种表示方法，可以用字面形式直接表示，比如35（十进制）和0xFF（十六进制）。

科学计数法允许字母e或E的后面，跟着一个整数，表示这个数值的指数部分。

以下两种情况，JavaScript 会自动将数值转为科学计数法表示，其他情况都采用字面形式直接表示。
* （1）小数点前的数字多于21位。
* （2）小数点后的零多于5个。


## 特殊数值
* 正负数
* NaN不等于自己本身，不是数值
* Infinity 无穷
---
# 字符串
## 概述
字符串就是零个或多个排在一起的字符，放在单引号或双引号之中。

单引号字符串的内部，可以使用双引号。双引号字符串的内部，可以使用单引号。

如果要在单引号字符串的内部，使用单引号，就必须在内部的单引号前面加上反斜杠，用来转义。双引号字符串内部使用双引号，也是如此。

字符串默认只能写在一行内，分成多行将会报错。如果长字符串必须分成多行，可以在每一行的尾部使用反斜杠。
```
var longString = 'Long \
long \
long \
string';

longString
// "Long long long string"
```
## 转义
反斜杠（\）在字符串内有特殊含义，用来表示一些特殊字符，所以又称为转义符。

需要用反斜杠转义的特殊字符，主要有下面这些。

* \0 ：null（\u0000）
* \b ：后退键（\u0008）
* \f ：换页符（\u000C）
* \n ：换行符（\u000A）
* \r ：回车键（\u000D）
* \t ：制表符（\u0009）
* \v ：垂直制表符（\u000B）
* \' ：单引号（\u0027）
* \" ：双引号（\u0022）
* `\\` ：反斜杠（\u005C）
  
反斜杠还有三种特殊用法。

（1）\HHH

反斜杠后面紧跟三个八进制数（000到377），代表一个字符。HHH对应该字符的 Unicode 码点，比如\251表示版权符号。显然，这种方法只能输出256种字符。

（2）\xHH

\x后面紧跟两个十六进制数（00到FF），代表一个字符。HH对应该字符的 Unicode 码点，比如\xA9表示版权符号。这种方法也只能输出256种字符。

（3）\uXXXX

\u后面紧跟四个十六进制数（0000到FFFF），代表一个字符。XXXX对应该字符的 Unicode 码点，比如\u00A9表示版权符号。

## 字符集
JavaScript 使用 Unicode 字符集。JavaScript 引擎内部，所有字符都用 Unicode 表示。

JavaScript 不仅以 Unicode 储存字符，还允许直接在程序中使用 Unicode 码点表示字符，即将字符写成\uxxxx的形式，其中xxxx代表该字符的 Unicode 码点。比如，\u00A9代表版权符号。
```
var s = '\u00A9';
s // "©"
```
---
# 对象
对象（object）是 JavaScript 语言的核心概念，也是最重要的数据类型。

什么是对象？简单说，对象就是一组“键值对”（key-value）的集合，是一种无序的复合数据集合。
## 狭义的对象
### 例子
```
var obj = {
  foo: 'Hello',
  bar: 'World'
};
```
### 对象的引用
对象中的键名可以直接当成属性或者方法进行定义和使用，当使用的属性值还是一个对象，就构成了链式引用,如果取消某一个变量对于原对象的引用，不会影响到另一个变量。
```
var o1 = {};
var o2 = { bar: 'hello' };

o1.foo = o2;
o1.foo.bar // "hello"

var o1 = {};
var o2 = o1;

o1 = 1;
o2 // {}
```
### 属性的操作
读取对象的属性，有两种方法，一种是使用点运算符，还有一种是使用方括号运算符
```
var foo = 'bar';

var obj = {
  foo: 1,
  bar: 2
};

obj.foo  // 1
obj[foo]  // 2
```
上面代码中，引用对象obj的foo属性时，如果使用点运算符，foo就是字符串；如果使用方括号运算符，但是不使用引号，那么foo就是一个变量，指向字符串bar。

>方括号运算符内部还可以使用表达式。

## 函数
JavaScript 有五种声明函数的方法
* 具名函数
```angular2
 function f(x,y){
     return x+y
 }
 f.name // 'f'
```
* 匿名函数
```angularjs
 var f
 f = function(x,y){
     return x+y
 }
 f.name // 'f'
```
* 具名函数赋值
```angular2
 var f
 f = function f2(x,y){ return x+y }
 f.name // 'f2'
 console.log(f2) // undefined
```
* window.Function
```angularjs
 var f = new Function('x','y','return x+y')
 f.name // "anonymous"
```
* 箭头函数
```angularjs
 var f = (x,y) => {
     return x+y
 }
 var sum = (x,y) => x+y
 var n2 = n => n*n
```

>如果同一个函数被多次声明，后面的声明就会覆盖前面的声明。

>如果同时采用function命令和赋值语句声明同一个函数，最后总是采用赋值语句的定义。

## 数组
数组（array）是按次序排列的一组值。每个值的位置都有编号（从0开始），整个数组用方括号表示。

>任何类型的数据，都可以放入数组。


---
# 关于数据类型的常用API

## 如何判断一个值是什么类型
### 三种方法
JavaScript 有三种方法，可以确定一个值到底是什么类型。

* `typeof`运算符
* `instanceof`运算符
* `Object.prototype.toString`方法

`null`的类型是`object`，这是由于历史原因造成的。1995年的 JavaScript 语言第一版，只设计了五种数据类型（对象、整数、浮点数、字符串和布尔值），没考虑null，只把它当作object的一种特殊值。后来null独立出来，作为一种单独的数据类型，为了兼容以前的代码，typeof null返回object就没法改变了。

### 区分数组和对象
`typeof` 可以区分函数和对象，但是无法区分数组和对象，因为在JS中数组本质上是特殊的对象。`instanceof`可以区分数组和对象，使用方法如下
```
var o = {};
var a = [];

o instanceof Array // false
a instanceof Array // true
```
或者采用`Array.isArray()`方法
```
Array.isArray([])  // true
Array.isArray({})  // false
```
## 数值相关的全局方法
### parseInt()
`parseInt()`方法用于将字符串转为整数或者进行进制转换。
```
parseInt(1000000000000000000000.5) // 1
// 等同于
parseInt('1e+21') // 1

parseInt(0.0000008) // 8
// 等同于
parseInt('8e-7') // 8

parseInt('1000', 2) // 8
parseInt('1000', 6) // 216
parseInt('1000', 8) // 512

```
### parseFloat()
`parseFloat()`方法用于将字符串转为浮点数。
```
parseFloat(true)  // NaN
Number(true) // 1

parseFloat(null) // NaN
Number(null) // 0

parseFloat('') // NaN
Number('') // 0

parseFloat('123.45#') // 123.45
Number('123.45#') // NaN
```
### isNaN()
`isNaN()`方法可以用来判断一个值是否为`NaN`
>isNaN为true的值，有可能不是NaN，而是一个字符串。
### isFinite()
`isFinite()`方法返回一个布尔值，表示某个值是否为正常的数值。
>除了Infinity、-Infinity、NaN和undefined这几个值会返回false，isFinite对于其他的数值都会返回true。

## 编码相关的方法和属性
### length属性

* 字符串的length属性返回字符串的长度，该属性也是无法改变的。
* 函数的length属性返回函数预期传入的参数个数，即函数定义之中的参数个数。
* 数组的length属性，返回数组的成员数量。
  
### btoa()与 atob()
JavaScript 对 UTF-16 的支持是不完整的，由于历史原因，只支持两字节的字符，不支持四字节的字符。这是因为 JavaScript 第一版发布的时候，Unicode 的码点只编到U+FFFF，因此两字节足够表示了。后来，Unicode 纳入的字符越来越多，出现了四字节的编码。但是，JavaScript 的标准此时已经定型了，统一将字符长度限制在两字节，导致无法识别四字节的字符。上一节的那个四字节字符𝌆，浏览器会正确识别这是一个字符，但是 JavaScript 无法识别，会认为这是两个字符。

有时，文本里面包含一些不可打印的符号，比如 ASCII 码0到31的符号都无法打印出来，这时可以使用 Base64 编码，将它们转成可以打印的字符。另一个场景是，有时需要以文本格式传递二进制数据，那么也可以使用 Base64 编码。

所谓 Base64 就是一种编码方法，可以将任意值转成 0～9、A～Z、a-z、+和/这64个字符组成的可打印字符。使用它的主要目的，不是为了加密，而是为了不出现特殊字符，简化程序的处理。

* btoa()：任意值转为 Base64 编码
* atob()：Base64 编码转为原来的值

## 对象的操作方法
点运算符和方括号运算符，不仅可以用来读取值，还可以用来赋值。
### Object.keys() 方法
`Object.keys()` 用来查看对象本身的所有属性，返回对象所有的键名。
### delete 运算符
`delete` 用来删除对象的属性.

* 如果删除一个不存在的属性，delete也不报错，会返回true;
* delete命令只能删除对象本身的属性，无法删除继承的属性
* 只有一种情况，delete命令会返回false，那就是该属性存在，且不得删除。

>```
>var obj = Object.defineProperty({}, 'p', {
>  value: 123,
>  configurable: false
>});
>
>obj.p // 123
>delete obj.p // false
>```
### in 运算符
`in`运算符用于检查对象是否包含某个属性（注意，检查的是键名，不是键值），如果包含就返回true，否则返回false。它的左边是一个字符串，表示属性名，右边是一个对象。
```
var obj = { p: 1 };
'p' in obj // true
'toString' in obj // true
```
### for...in
`for...in`循环用来遍历一个对象的全部属性。
* 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性。
* 它不仅遍历对象自身的属性，还遍历继承的属性。

## 函数特有的方法
### name 属性
函数的`name`属性返回函数的名字。
```
var f3 = function myName() {};
f3.name // 'myName'
```
f3.name返回函数表达式的名字。注意，真正的函数名还是f3，而myName这个名字只在函数体内部可用。

### .toString() 方法
函数的toString方法返回一个字符串，内容是函数的源码。
>此方法和.tostring 不相同

### arguments 对象
由于 JavaScript 允许函数有不定数目的参数，所以需要一种机制，可以在函数体内部读取所有参数。这就是arguments对象的由来。

严格模式下，arguments对象与函数参数不具有联动关系。也就是说，修改arguments对象不会影响到实际的函数参数。

虽然arguments很像数组，但它是一个对象。数组专有的方法（比如slice和forEach），不能在arguments对象上直接使用。

## 数组特有的方法
### forEach()
数组的forEach方法，也可以用来遍历数组，
```
var colors = ['red', 'green', 'blue'];
colors.forEach(function (color) {
  console.log(color);
});
// red
// green
// blue
```
### slice.call()
典型的“类似数组的对象”是函数的arguments对象，以及大多数 DOM 元素集，还有字符串。

数组的`slice`方法可以将“类似数组的对象”变成真正的数组。
```
var arr = Array.prototype.slice.call(arrayLike);
```
---
# 数据转换技巧

## 转换为字符串
* .tostring 方法
* String() 函数
* ''+ Any 表达式
## 转换为数字
* Number()  方法
* parseInt()  方法
* parseFloat()  方法
* `'1'-0 === 1`  表达式
* `+'1'=== 1` 或`+'-1' === -1` 表达式
## 转换为bool
* Boolean() 函数
* !!+ Any 表达式
  
# 内存图 
javaScript中的内存主要分为heap(堆内存)、stack(栈内存)

* number，string，null，undefined，boolean 这五类简单的数据类型主要使用的是stack(栈内存) 
* object 在stack(栈内存)中存储heap(堆内存)中的地址，在heap(堆内存)中存储对象内部的数据

>变量的方法与属性的实现，实际上就是对堆内存中的数据块进行的引用

## 内存图的5个例子
```
var a = '1'
var b = a
b = '2' 
a = ?    // 1
---
var a ={name : 'a'}
var b = a
b = {name : 'b'}
a.name = ?   // a
---
var a = {name : 'a'}
var b = a 
b.name = 'b'
a.name = ?   // b
---
var a = {name : 'a'}
var b = a
b = null
a = ?   // {name : 'a'}
---
var a = {n:1}
var b = a 
a.x = a = {n:2}

a.x = ?  // undefined
b.x = ?  // [object object]

```

## 深拷贝和浅拷贝
* 深拷贝：原始变量的内存，不随拷贝变量的更改而更改（包括堆内存和栈内存）
* 浅拷贝：原始变量的堆内存，随拷贝变量的改变而改变