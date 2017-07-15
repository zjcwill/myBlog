---
title: es6学习笔记
date: 2017-05-20 16:18:19
tags: es6 js
---
一些学习es6的心得
<!--more-->
### babel cli
把ES6代码转为可以使用的
`npm install --global babel-cli`
基本用法
```javascript
# 转码结果输出到标准输出
$ babel example.js

# 转码结果写入一个文件
# --out-file 或 -o 参数指定输出文件
$ babel example.js --out-file compiled.js
# 或者
$ babel example.js -o compiled.js

# 整个目录转码
# --out-dir 或 -d 参数指定输出目录
$ babel src --out-dir lib
# 或者
$ babel src -d lib

# -s 参数生成source map文件
$ babel src -d lib -s
```
***
### 闭包
1. 函数内部可以直接读取全局变量
```javascript
　var n=999;
　　function f1(){
　　　　alert(n);
　　}
　　f1(); // 999
```
2. 函数外部无法读取函数内部的局部变量
```javascript
　　function f1(){
　　　　var n=999;
　　}
　　alert(n); // error
```
3. 如果函数内部声明的时候没有使用var，实际上声明了一个全局变量
```javascript
　　function f1(){
　　　　n=999;
　　}
　　f1();
　　alert(n); // 999
```
4. 如何从外部读取函数的局部变量？

函数内部再定义一个函数
```javascript
    　　function f1(){
　　　　var n=999;
　　　　function f2(){
　　　　　　alert(n); // 999
　　　　}
　　}
 ```
 f1内部所有局部变量f2都是可见的
 Javascript语言特有的"链式作用域"结构（chain scope），子对象会一级一级地向上寻找所有父对象的变量。

 把函数作为返回值，即可在外部调用
 ```javascript
var result = function(){
    var n=999;
    function f2() {
        console.log(n);
    }
    return f2()
}

result();//999
```

__闭包就是能够读取其他函数内部变量的函数。__
或定义在一个函数内部的函数
5. 闭包会使函数中得变量被保存到内存中
6. 思考题
```js
　var name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
　　　　　　return function(){
　　　　　　　　return this.name;
　　　　　　};
　　　　}
　　};
　　alert(object.getNameFunc()());
//the windows
```
return function()上一级没有name，所以指向全局寻找

改良指向my object
```js
 name = "The Window";
　　var object = {
　　　　name : "My Object",
　　　　getNameFunc : function(){
            var that = this;
　　　　　　return function(){
　　　　　　　　return that.name;
　　　　　　};
　　　　}
　　};
　　alert(object.getNameFunc()());
```
***
### for循环
for循环外部是一个作用域，里是一个作用域
```js
for (let i = 0; i < 3; i++) {
  let i = 'abc';
  console.log(i);//abc abc abc
}
```
***
### let块级作用域
```js
function f1(){
    let n=5;
    if(true){
        let n=10;
    }
    console.log(n);
}
f1();//5
```
外层代码块不受内层代码块影响
内层作用域可以定义外层作用域的同名变量。
***
### 解构赋值
0. 数组
```js
//变量交换
{
    let a=1;
    let b=2;
    [a,b]=[b,a];
    console.log(a,b);//2,1
}
```
```js
//取多个返回值
{
    function f() {
        return['商品名','价格']
    }
    let a,b;
    [a,b]=f();
    console.log(a,b);//商品名 价格
}
```
```js
//选择性接收数据
{
    function f() {
        return[1,2,3,4,5,6]
    }
    let a,b;
    [a,,,b]=f();
    console.log(a,b);//1 4
}
```
```js
{
    function f() {
        return[1,2,3,4,5,6]
    }
    let a,b;
    [a,,,...b]=f();
    console.log(a,b);//1 [ 4, 5, 6 ]
}
```
1. 对象
```js
{
let {foo,bar}= {foo:'aa',bar:'66'};
//对象=对象 key value 匹配
console.log(foo);//aa
console.log(bar);//66
}
```
与对象结构赋值不同的是，变量必须与属性同名，才能取到正确的值。

json数据获取技巧
```js
{
    let data = {
        "resultcode": "200",
        "result": {
            "province": "辽宁",
            "city": "大连",
            "areacode": "0411",
            "zip": "116000",
            "company": "移动",
            "card": ""
        },
        "error_code": 0
    }
    let {result:{province:Rprovince,city:Rcity}}=data;
    console.log(Rprovince,Rcity);
}
```
2. 函数
```js
{
let array = [1,2];
function add([x,y]){
    return x+y;
}
console.log(add(array));//3
}
```
参数表面是一个数组，被传入那一刻解构成了x和y
3. 提取json
```js
{
    let jsonData = {
        id: 42,
        status: "OK",
        data: [867, 5309]
    };

    let { id, status, data: number } = jsonData;

    console.log(id, status, number);
}
```
***
### 字符串拓展
1. 检测字符串
- includes()：返回布尔值，表示是否找到了参数字符串。
- tartsWith()：返回布尔值，表示参数字符串是否在源字符串的头部。
- endsWith()：返回布尔值，表示参数字符串是否在源字符串的尾部。
2. 模板字符串
```js
$('#result').append(`
  There are <b>${basket.count}</b> items
   in your basket, <em>${basket.onSale}</em>
  are on sale!
`);
```
变量使用`${}`表示，可以传函数
***
### 函数
1. ES6 允许为函数的参数设置默认值，即直接写在参数定义的后面。
```js
function log(x, y = 'World') {
  console.log(x, y);
}
```
设置参数会在执行生成一个单独的作用域
2. rest 获取多余的参数
```js
function push(array, ...items) {
  items.forEach(function(item) {
    array.push(item);
    console.log(item);
  });
}
var a = [];
push(a, 1, 2, 3)
```
3. 箭头函数
如果箭头函数的代码块部分多于一条语句，就要使用大括号将它们括起来，并且使用return语句返回。
```js
var f = () => 5;
// 等同于
var f = function () { return 5 };

var sum = function(num1, num2) {
  return num1 + num2;
};
```
- 函数体内的`this`对象，就是定义时所在的对象，而不是使用时所在的对象
```js
function foo() {
  setTimeout(() => {
    console.log('id:', this.id);
  }, 100);
}
var id = 21;
foo.call({ id: 42 });
// id: 42
```
### .bind()绑定函数
bind() 最简单的用法是创建一个函数，使这个函数不论怎么调用都有同样的 this 值。
```js
this.x = 9; 
var module = {
  x: 81,
  getX: function() { return this.x; }
};

module.getX(); // 返回 81

var retrieveX = module.getX;
retrieveX(); // 返回 9, 在这种情况下，"this"指向全局作用域

// 创建一个新函数，将"this"绑定到module对象
// 新手可能会被全局的x变量和module里的属性x所迷惑
var boundGetX = retrieveX.bind(module);
boundGetX(); // 返回 81
```
***