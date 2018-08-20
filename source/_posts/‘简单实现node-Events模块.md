---
title: 简单实现node Events模块
date: 2018-08-20 11:15:22
tags:
  - note
---

> 观察者模式定义对象间的一种一对多依赖关系，使得当每一个被依赖对象状态发生改变时，其相关依赖对象都得到通知并自动更新, node中的Events模块就是通过观察者模式来实现的：
```
var events = require('events');
var eventEventEmitter = new events.EventEmitter();
eventEventEmitter.on('hello',function(name){
	console.log('hello',name);
})
eventEventEmitter.emit('hello','linaa');
```
### 实现简单的Event模块的emit和on方法

```
function Events() {
	this.on = function(eventName,callBack) {
		if(!this.handles) {
			this.handles = {}
		}
		if(!this.handles[eventName]) {
			this.handles[eventName]=[];
		}
		this.handles[eventName].push(callBack)
	}

	this.emit = function(eventName,obj){
		if(this.handles[eventName]) {
			for(var i = 0;i<this.handles[eventName].length;i++){
				this.handles[eventName][i](obj);
			}
		}	
	}
}
```

###调用
```
var events=new Events();
 events.on('hello',function(name){
    console.log('Hello',name)
 });
 events.emit('hello','linaa');
```