---
title: Javascripts运行原理解析
categories:
- JS
tags:
- JS
date: 2018-08-29 14:16:44
---

先介绍几个相关概念
* JS引擎
* JS Engine（JS引擎）
* Runtime（运行上下文）
* Call Stack (调用栈)
* Event Loop（事件循环）
* Callback (回调)

### JS引擎
JS引擎是对JS代码进行词法、语法分析，通过编译器将代码编译成可执行的机器代码(Java中的JVM 虚拟机一样)，Chrome和node均采用V8引擎
JS 引擎中也存在堆和栈
* 堆 存放对象
* 栈 存放方法和基础数据类型 、正在执行的任务
### Runtime（运行上下文）
JS在浏览器环境中运行时，BOM和DOM对象提供了很多相关外部接口（这些接口不是V8引擎提供的），供JS运行时调用，以及JS的事件循环(Event Loop)和事件队列(Callback Queue)，把这些称为RunTime。在Node.js中，可以把Node的各种库提供的API称为RunTime
![Alt text](/assets/img/event_loop2.jpg)
### Call Stack (调用栈)
* 全局执行环境
* 函数执行环境
* Eval 执行环境
当JS代码第一次被加载时，会创建一个全局执行环境（windows对象），当调用一个函数时，会创建一个函数执行环境
### Event Loop（事件循环）
Event Loop只做一件事情，负责监听Call Stack和Callback Queue。主线程空闲（调用栈空）时，当Call Stack里面的调用栈运行完变成空了，Event Loop就把Callback Queue里面的第一条事件(其实就是回调函数)放到调用栈中并执行它，后续不断循环执行这个操作。
![Alt text](/assets/img/event_loop.jpg)
