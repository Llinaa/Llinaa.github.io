---
title: 'JavaScript:[1,2,3].map(parseInt)问题解析'
categories:
- JS
tags:
- JS
date: 2018-08-15 16:24:36
---
###### 猜猜答案是什么呢
最近遇到[1,2,3].map(parseInt)，第一反应，觉得答案是[1,2,3]。深深的掉入陷阱，答案是[1,NaN,NaN]。。。
为什么会这样，下面逐一解释：
1、`parseInt(string, radix)`

parseInt(string, radix)是js的一个全局函数，解析一个字符串、并返回一个整数,string必需，radix可选（表示要解析的数字的基数。该值介于 2 ~ 36 之间。）

> 当radix为0时或者没有传入该参数时，parseInt()会根据string来判断数字的基数，
	当忽略参数 radix , JavaScript 默认数字的基数如下:
	如果 string 以 "0x" 开头，parseInt() 会把 string 的其余部分解析为十六进制的整数。
	如果 string 以 0 开头，parseInt() 会把 string 的其余部分解析为八进制或十六进制的整数。
	如果 string 以 1 ~ 9 的数字开头，parseInt() 将把它解析为十进制的整数。
```
var n = parseInt('123')      123
var m = parseInt('abc')      NaN
```

2、`Array.prototype.map`

map()方法返回一个新的数组，数组中的元素为原始数组元素调用函数处理后的值
	array.map(function(currentValue,index,arr), thisValue)
> function(currentValue,index,arr) 必需，函数，数组中的元素都会执行这个函数
	函数参数：currentValue，必需，当前元素的值，
			  index，可选，当前元素的索引值，
			  arr，可选，当前元素属于的数组对象
  thisValue 执行function时this指向的对象

问题解析：
	function 调用时，需要传入了三个参数，原本我们以为对parseInt的三次调用时这样：
```
parseInt('1')
parseInt('2')
parseInt('3')
```
但实际上却是这样：
```
parseInt('1',0,[1,2,3]);
parseInt('2',1,[1,2,3]);
parseInt('3',2,[1,2,3]);
```
JS函数一般会自动忽视多余的参数，parseInt仅仅需要两个参数，
第一次调用时，
`parseInt('1',0); 1`
第二次调用时，
`parseInt('2',1); NaN radix的范围是[2,26]`
第一次调用时，
`parseInt('3',2); NaN 2作为基数，那么字符串将被解析成字节数，仅包含0和1，‘3’不是一个有效数字，则被解析为NaN`

> 改进
```
[1,2,3].map((value)=> {
	return parseInt(value)
})
```
