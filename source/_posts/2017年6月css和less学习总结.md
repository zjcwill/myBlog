---
title: 2017年6月css和less学习总结
date: 2017-06-28 20:30:21
tags: [前端,less,css]
---
近期实习关于样式调优的小记
<!--more-->
## box-shaodw
x,y,高斯
## transition-duration
过度时间 如.2s
##  background-origin 属性
background-origin 属性规定背景图片的定位区域。
背景图片可以放置于 content-box、padding-box 或 border-box 区域。
<image src="http://www.w3school.com.cn/i/background-origin.gif"></image>
## less
### 字符串插值
可用于同一目录调用不同文件
`@base-url: "http://assets.fnord.com";
background-image: url("@{base-url}/images/bg.png");`
### Import
引用less文件
`@import "lib.less";`
`@import "lib";`
### @定义变量
`@color:red`
### css设置图片
```less
.mainImg(@imgName)
 {
    width: 45px;
    height: 45px;
    background-size: cover;
    background-image:~"url(./assets/@{imgName}.png)";
    background-repeat: no-repeat;
}

```
### 定义传参的样式
```less
.box(@width, @height, @color) 
{
    width: @width;
    height: @height;
    background-color: @color;
}
```
### 命名空间
```less
#bundle {
  .button () {
    display: block;
    border: 1px solid black;
    background-color: grey;
    &:hover { background-color: white }
  }
  .tab { ... }
  .citation { ... }
}
```
```less
#header a {
  color: orange;
  #bundle > .button;
}
```
## css module
CSS Modules 默认是局部作用域的，想要声明一个全局规则，可用 :global 语法。
```css
.title {
  color: red;
}
:global(.title) {
  color: green;
}
```
```js
<App className={styles.title} /> // red
<App className="title" />        // green
```
