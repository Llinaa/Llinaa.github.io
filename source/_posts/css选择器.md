---
title: css选择器
date: 2020-05-23 16:47:15
categories: 
- CSS
tags:
- CSS
---

######  1、通配选择器
等同于列出了文档中所有元素的一个分组选择器
```css
* {color: red;}  
```
######  2、类选择器
要应用样式而不考虑具体修改的元素
```css
.warnging {color: red;}  
```
######  3、ID选择器
<font color=red>
与类选择器区别：</br>
1、类选择器可应用到多元素上，而id选择器仅可使用一次（实际中，浏览器并不会检查html中id的唯一性）</br>
2、类选择器可以结合使用，而id选择器不能</br>
3、当你想确定应当向一个给定元素应用那些样式，id能包含更多含义</br>
</font>

```css
#warnging {color: red;}  
```
######  4、属性选择器

-  简单属性选择：选择有某个属性的元素，而不论值是什么
```css
h1[class] {color: red;}  
```
-  根据具体属性值选择
```css
a[title='test'] {color: red;}  
h1[class='urgent warning'] {color: red;}
```
-  根据部分属性值选择
```css 
h1[class～='warning'] {color: red;} 包含warnging
h1[class^='warning'] {color: red;} 以warnging开头
h1[class$='warning'] {color: red;} 以含warnging结尾
h1[class*='warning'] {color: red;} 包含warnging 字串
```
-  特定属性选择
```css 
*[lang|="en"] {color: red;}
```
######  5、后代选择器
从右向左读取
-  选择子元素
```css
h1 > strong {color: red;}  
```
-  选择相邻兄弟元素（父元素相同）
```css
h1 + p {color: red;} 
```
######  6、伪类选器

  <font color=red>
    锚类型分为：已访问的和未访问的，这些类型称为伪类，使用这个伪类的选择器称为伪类选择器。
  </font>

-  链接伪类

    <font color=red>
    在HTML、XHTML1.0、1.1中，超链接是有href属性的所有a元素；</br>
    在XML语言中，超链接则可以是任何元素，只要它作为另一个资源的链接；
    </font>
    
    </br>

    <font color=blue>
    CSS2.1中定义了 :link、 :visited两个静态伪类(第一次显示后，一般不会再改变文档样式)</br>
    :focus、:hover、:active 三个动态伪类，可用于任何元素 </br>
    顺序：lvfha
    </font>

    ```css
    a:link{color: red;}  
    a:visited{color: blue;} 
    ```

-  选择第一个子元素
```css
p:first-child {color: red;} 
```

###### 7、伪元素选器

  <font color=red>
    伪元素能够在文档中插入假想的元素，进而得到某种效果，CSS2.1中定义了4个伪元素
  </font>

    ```css
    p:first-letter{color: red;}  
    p:first-line{color: blue;}
    h1:before {
    content: "}}";
    color: salmon;
    } 
    ```

######  8、结构和层叠

   当多条规则应用于同一元素时，浏览器则会去计算优先级，值是<font color=red>从左向右</font>比较

-  优先级
    1. ID：0100
    2. 类、属性选择、伪类：0010
    3. 元素、伪元素：0001
    4. 结合符号和通配选择器对特殊性没有任何贡献，换句话说，其优先级为0000
    5. 内联，其优先级为100（注意是3个），与ID选择器相同，所以ID选择器很容易覆盖内联样式
    
-  继承
 
    继承沿着文档树向下传播到后代元素，并且继承值没有任何优先级
    <font color=red>不可继承：</font>边框，盒子模型，背景属性
    <font color=red>可继承： </font>字体，文本样式属性
   
   - 所有元素可继承：`visibility`（元素是否显示，即使hidden也占空间）和`cursor`（鼠标样式）。
   - 内联元素可继承：
   `letter-spacing`、`word-spacing`、`white-space`、`line-height`、
   `color`、`font`、
   `font-family`、`font-size`、`font-style`、`font-variant`（小型大写字母）、`font-weight`、
   `text-decoration`、`text-transform`、`direction`（文字方向）。
   - 块状元素可继承：`text-indent`（首行缩进）和`text-align`。
   - 列表元素可继承：
    `list-style`、`list-style-type`、`list-style-position`、`list-style-image`。
   - 表格元素可继承：`border-collapse`。
   
-  层叠

  <font color=red>
     当优先级相等时，使用层叠规则，如下：
  </font>
  
  1. 按权重和来源，从大到小
    -  读者的important声明
    -  创作人员的important声明
    -  创作人员的正常声明
    -  读者的正常声明
    -  用户代理声明（浏览器默认样式）
  2. 按优先级大小
  3. 按顺序排序：越后出现权重越大，如果样式表中有导入的样式表，一般认为导入样式表的声明在前，主样式表声明在后
