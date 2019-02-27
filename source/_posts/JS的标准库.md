---
title: JS的标准库
date: 2019-02-22 08:55:21
tags: 学习笔记
categories: IT
---
> 学习资源：https://wangdoc.com/javascript

---
<!-- more -->
# Array 

```javascript
var a = Array(3)
var b = Array(3,3)
var c = new Array(3)
var d = new Array(3,3)
```
## push()与pop()
push方法用于在数组的末端添加一个或多个元素，并返回添加新元素后的数组长度。注意，该方法会改变原数组

pop方法用于删除数组的最后一个元素，并返回该元素。注意，该方法会改变原数组

对空数组使用pop方法，不会报错，而是返回undefined。

```javascript
var arr = [];
arr.push(1, 2);
arr.push(3);
arr.pop(); // 3
arr // [1, 2]

[].pop() // undefined

```
## forEach 与 map

```javascript
var a =[1,2,3,4,5,6]
a.forEach(function(x,y){console.log(x,y)})

```
map 有返回值

## sort
sort方法对数组成员进行排序，默认是按照字典顺序排序。排序后，原数组将被改变。

sort方法不是按照大小排序，而是按照字典顺序。也就是说，数值会被先转成字符串，再按照字典顺序进行比较，所以101排在11的前面。

如果想让sort方法按照自定义方式排序，可以传入一个函数作为参数。

```javascript
[
  { name: "张三", age: 30 },
  { name: "李四", age: 24 },
  { name: "王五", age: 28  }
].sort(function (o1, o2) {
  return o1.age - o2.age;
})

// [
//   { name: "李四", age: 24 },
//   { name: "王五", age: 28  },
//   { name: "张三", age: 30 }
// ]
```
## join
join()方法以指定参数作为分隔符，将所有数组成员连接为一个字符串返回。如果不提供参数，默认用逗号分隔。

如果数组成员是undefined或null或空位，会被转成空字符串。

通过call方法，这个方法也可以用于字符串或类似数组的对象。
```javascript
Array.prototype.join.call('hello', '-')
// "h-e-l-l-o"

var obj = { 0: 'a', 1: 'b', length: 2 };
Array.prototype.join.call(obj, '-')
// 'a-b'
```

## concat

合并

## filter
过滤

## reduce 与reduceRight
reduce方法和reduceRight方法依次处理数组的每个成员，最终累计为一个值。
它们的差别是，reduce是从左到右处理（从第一个成员到最后一个成员），reduceRight则是从右到左（从最后一个成员到第一个成员），其他完全一样。


--- 

# Function

## name

## call()
f.call(undefined,1,2)

## this 和 argument