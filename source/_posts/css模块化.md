---
layout: post
title: css module
date: 2019-05-18 10:17:30
tags: css
---
# css module

## 作用域

显式的局部作用域语法`:local(.className)`，等同于`.className`

全局作用域`:global(.className)`

```css
:local(.title) {
  color: red;
}

:global(.page) {
  background: #999;
}
```

## 组合

Class 的组合

```css
.className {
  background-color: blue;
}

.title {
  composes: className;
  color: red;
}
```

## 继承

继承其他文件里的规则
```css
.title {
  composes: className from './another.css';
  color: red;
}
```

## 变量
```css
@value red: #333;

:global(.h150) {
  height: 150px;
  background-color:  red;
}
```

## 多文件继承

```css
@value blue: #0c77f8;
@value red: #ff0000;
@value green: #aaf200;
```

```css
@value colors: "./colors.css";
@value blue, red, green from colors;

.title {
  color: red;
  background-color: blue;
}
```

## 外部如何覆盖局部样式

可以给组件关键节点加上 data-role 属性，然后通过属性选择器来覆盖样式。

```html
<div className={styles.root} data-role='dialog-root'>
```
```css
[data-role="dialog-root"] {
  // override style
}
```
