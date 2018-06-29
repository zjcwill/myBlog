---
title: css基础知识总结
date: 2018-06-29 23:25:25
tags: css
---
记录一些自己容易忘的css知识汇总。
<!--more-->
# css基础知识总结
# 选择器
## `nth-type` `nth-child`
`nth-child(n)`选择器匹配属于其父元素的第N个子元素，**不论元素类型**。
`nth-type(n)` 选择器匹配属于父元素的**特定类型**的第N个子元素的每个元素。
## CSS 子元素选择器`>`
### 介绍
如果您不希望选择任意的后代元素，而是希望缩小范围，只选择某个元素的子元素，请使用子元素选择器。
### 例子
例如，如果您希望选择只作为 h1 元素子元素的 strong 元素，可以这样写：
```css
h1 > strong {color:red;}
```
这个规则会把第一个 h1 下面的两个 strong 元素变为红色，但是第二个 h1 中的 strong 不受影响：
```html
<h1>This is <strong>very</strong> <strong>very</strong> important.</h1>
<h1>This is <em>really <strong>very</strong></em> important.</h1>
```
## 动画
###  `animation-direction`
```css
div
{
animation-direction:alternate;
-webkit-animation-direction:alternate; /* Safari 和 Chrome */
}
```
animation-direction 属性定义是否应该轮流反向播放动画。

如果 animation-direction 值是 "alternate"，则动画会在奇数次数（1、3、5 等等）正常播放，而在偶数次数（2、4、6 等等）向后播放。
## 控制选择
### 禁用选择
使内容不可选择。
```css
.unselectable {
    user-select:none;
}
```
取值

key | value
---|---
none |文本不能被选择
text | 可以选择文本
all | 当所有内容作为一个整体时可以被选择。如果双击或者在上下文上点击子元素，那么被选择的部分将是以该子元素向上回溯的最高祖先元素。
element | 可以选择文本，但选择范围受元素边界的约束
## css变量var
CSS 变量是由CSS作者定义的实体，其中包含要在整个文档中重复使用的特定值。使用自定义属性来设置变量名，并使用特定的 `var()` 来访问。（比如  `color: var(--main-color);`）。
### 基本用法
声明一个**局部**变量
```css
element {
    --main-bg-color:brown;
}
```
使用一个**局部**变量
```css
element {
    background-color:var(--main-bg-color)
}

```
声明一个**全局**css变量
```css
:root {
    --global-color:#666;
    --pane-padding:5px 42px;
}
```
使用一个**全局**css变量
```css
.demo {
    color:var(--global-color);
}
```
### 例子
```css
:root {
  --main-bg-color: brown;
}

.one {
  color: white;
  background-color: var(--main-bg-color);
  margin: 10px;
  width: 50px;
  height: 50px;
  display: inline-block;
}

```
## transform-origin
`transform-origin` CSS属性让你更改==一个元素变形的原点==。
## :not()
`:not(selector) { CSS样式 }`
```html
<p>我是一个段落。</p>
<p class="fancy">我好看极了！</p>
<p>我不是一个段落。</p>
```
```css
p:not(.fancy) {
  color:red;
}
/* 类名不是fancy的p标签颜色为红色 */
```
### 例子：同级变淡
淡出悬停项目的同级。
```html
<div class="sibling-fade">
  <span>Item 1</span>
  <span>Item 2</span>
  <span>Item 3</span>
  <span>Item 4</span>
  <span>Item 5</span>
  <span>Item 6</span>
</div>
```
```css
span {
  padding: 0 1rem;
  transition: opacity 0.2s;
}
.sibling-fade:hover span:not(:hover) {
  opacity: 0.5;
}
```
说明

`.sibling-fade:hover span:not(:hover)` 指定当父项被徘徊时，选择当前没有被徘徊的任何span子项并将其不透明度更改为0.5 。
