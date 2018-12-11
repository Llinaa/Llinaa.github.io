---
title: CSS Modules
date: 2018-12-11 17:29:20
tags:
---
### 什么是CSS Modules？
所有的class的名称和动画的名称默认属于本地作用域的CSS文件。
所以CSS Modules不是一个官方的规范，也不是浏览器的一种机制，它是一种构建步骤中对CSS类名选择器限定作用域的一种方式
构建通常需要webpack或者browserify的帮助）。通过构建工具的帮助，可以将class的名字或者选择器的名字作用域化。（类似命名空间化。）
不是将CSS改造成编程语言，只是加入了局部作用域和模块依赖，解决CSS中的全局作用域问题，确保样式服务于单个组件
### 1、局部作用域
CSS的规则都是全剧的，任何一个组件的样式规则，都对整个页面生效，产生布局作用域的唯一方法，就是使用就是使用一个独一无二的class的名字，不会与其他选择器重名。这就是 CSS Modules 的做法。
下面是一个React 组件
```
import React from 'react';
import style from './App.css';

export default () => {
  return (
    <h1 className={style.title}>
      Hello World
    </h1>
  );
};
```
CSS 文件，最终构建工具将类名style.title编译成一个哈希字符串，App.css也会同时被编译。这个类名就变成独一无二了
```
.title {
  color: red;
}
```
CSS Modules 提供各种插件（Webpack-css-loader、Browserify-css-modulesify等），支持不同的构建工具。例如Webpack 的css-loader插件
### 2、全局作用域
CSS Modules 允许使用:global(.className)的语法，声明一个全局规则。凡是这样声明的class，都不会被编译成哈希字符串。
```
.title {
  color: red;
}

:global(.title) {
  color: green;
}
```
```
import React from 'react';
import styles from './App.css';

export default () => {
  return (
    <h1 className="title">     //使用普通的class的写法，就会引用全局class
      Hello World
    </h1>
  );
};
```
### 3、定制哈希类名
css-loader默认的哈希算法是[hash:base64]，这会将.title编译成._3zyde4l1yATCOkgn-DBWEL这样的字符串。
webpack.config.js里面可以定制哈希字符串的格式。
```
module: {
  loaders: [
    // ...
    {
      test: /\.css$/,
      loader: "style-loader!css-loader?modules&localIdentName=[path][name]---[local]---[hash:base64:5]"
    },
  ]
}
```
### 4、Class 的组合
在 CSS Modules 中，一个选择器可以继承另一个选择器的规则，这称为"组合"（"composition"）。
```
.className {
  background-color: blue;
}

.title {
  composes: className;
  color: red;
}
```
### 5、输入其他模块，选择器也可以继承其他CSS文件里面的规则。
```
another.css
.className {
  background-color: blue;
}
App.css可以继承another.css里面的规则
.title {
  composes: className from './another.css';
  color: red;
}
```
### 6、输入变量
CSS Modules 支持使用变量，不过需要安装 PostCSS 和 postcss-modules-values
```
var values = require('postcss-modules-values');

module.exports = {
  entry: __dirname + '/index.js',
  output: {
    publicPath: '/',
    filename: './bundle.js'
  },
  module: {
    loaders: [
      {
        test: /\.jsx?$/,
        exclude: /node_modules/,
        loader: 'babel',
        query: {
          presets: ['es2015', 'stage-0', 'react']
        }
      },
      {
        test: /\.css$/,
        loader: "style-loader!css-loader?modules!postcss-loader"    //加入postcss-loader
      },
    ]
  },
  postcss: [
    values
  ]
};
```
```
colors.css
@value blue: #0c77f8;
@value red: #ff0000;
@value green: #aaf200;

App.css
@value colors: "./colors.css";
@value blue, red, green from colors;
.title {
  color: red;
  background-color: blue;
}
```
