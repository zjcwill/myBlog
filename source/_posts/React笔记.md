---
title: React笔记
date: 2018-06-29 23:22:33
tags: react
---
记录一些React语法知识。
<!--more-->
# 2018年5、6月React笔记
## 纯函数组件使用`PropTypes`
```jsx
import React from 'react';
import PropTypes from 'prop-types';

function Title(props) {
return <h1>{ props.text }</h1>;
}
Title.propTypes = {
text: PropTypes.string
};
Title.defaultProps = {
text: 'Hello world'
};

export default Title;

```
## `props.children`
`props.children` 属性，它可以让我们访问父组件标签内的子元素。
```jsx
ReactDOM.render(<div>
<Title text="ni hao">Wooooooooooooo</Title>
</div>, document.getElementById('root'));
```
```jsx
function Title({text,children}) {
return <div>
<h1>{text}</h1>
{children}
</div>;
}
```
## `Refs`
通过`ref`获取不受控组件的值
```jsx
class Input extends React.Component {
constructor(props) {
super(props);
this.state = { value: 'hello' };
this._change = this._handleInputChange.bind(this);
}
_handleInputChange() {
this.setState({ value: this.input.value });
}
render() {
return (
<div>
<input type='text'
defaultValue={this.state.value}
onChange={this._change}
ref={input=>this.input = input}/>
</div>
);
}
}
```
`ref` 属性接收字符串或回调函数。上面的代码使用回调函数来将 DOM 元素保存在局部变量 `input`中。之后当`onChange` 事件触发时，我们将`input` 中的最新值保存到 App 组件的状态里。
## `Ref`
```jsx

class Tags extends Component {
shouldComponentUpdate(){
return false;
}
componentDidMount(){
console.log(this.refs.list)
}
render() {
return (
<ul ref='list'>
{
this.props.tags.map((tag,i)=><li key={i}>{tag}</li>)
}
</ul>
);
}
}
```
定义元素`ref='list'`，在`componentDidMount`生命周期通过`this.refs.list`获取`ul`真实dom，通过`shouldComponentUpdate`为`false`把dom更新从react接管到手动更新。

## dangerouslySetInnerHTML
`dangerouslySetInnerHTML` is React’s replacement for using `innerHTML` in the browser DOM. 
```js
function createMarkup() {
return {__html: 'First &middot; Second'};
}

function MyComponent() {
return <div dangerouslySetInnerHTML={createMarkup()} />;
}
```
## constructor(props)

官方解释

Class components should always call the base constructor with props.
```js
constructor(props) {
super(props);
this.state = {date: new Date()};
}


```
如果你用到了`constructor`就必须写`super()`,是用来初始化`this`的，可以绑定事件到this上;
如果你在`constructor`中要使用`this.props`,就必须给`super`加参数：`super(props)`；

（无论有没有`constructo`r，在`render`中`this.props`都是可以使用的，这是React自动附带的；）
## 创建refs
```js
class MyComponent extends React.Component {
constructor(props) {
super(props);
this.myRef = React.createRef();
}
render() {
return <div ref={this.myRef} />;
}
}
```