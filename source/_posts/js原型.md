---
title: js原型
categories:
- JS
tags:
- JS
date: 2018-08-21 09:52:37
---

使用构造函数创建对象
```
function Animal (name) {
    this.name = name;
}
let dog = new Animal('xiaomi');
console.log("dog",dog.name);    xiaomi
console.log("Animal prototype",Animal.prototype)  
```
### prototype：
上述Animal是一个构造函数，每个函数都有一个prototype属性，该属性指向一个对象，这个对象就是调用该构造函数创建的对象实例的原型，即上述 dog的原型指向Animal.prototype.
原型是什么呢？每个对象实例（除null）在创建的时候就会与另外一个对象进行关联，这个对象就是该实例的原型，该实例对象对从原型对象上继承属性。
![Alt text](/assets/img/prototype.png)
那么person 与 Person.prototype 是怎样关联的呢？下来介绍第二个属性：
### \_proto\_ ：
每个对象实例都会有一个\_proto\_ 属性，这个属性指向该对象的原型
```
console.log("_proto_",dog.__proto__ === Animal.prototype)  //true  
```
![Alt text](/assets/img/prototype2.png)

### constructor 
每个原型对象都有一个constructor属性，指向构造函数
```
console.log("constructor",Animal.prototype.constructor === Animal) //true  
```
![Alt text](/assets/img/prototype3.png)

<!-- ### 实例与原型
当读取实例的属性时，如果找不到，就会查找原型对象中的属性，如果还查不到，会去原型的原则中查找，直到顶层为止 -->
