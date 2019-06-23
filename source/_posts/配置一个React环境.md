---
title: webpack 配置一个React环境
date: 2019-06-23 22:41:43
tags: webpack
---

# Webpack 配置一个 React 环境

## 配置一个 React 环境

初始化 node 项目

```bash
yarn init -y
```

安装 webpack 相关依赖

```bash
yarn add webpack webpack-cli --dev
```

在`package.json`配置 webpack 生产环境打包脚本

```
"scripts": {
  "build": "webpack --mode production"
}
```

为了使浏览器支持诸如`Class`类 ES6 语法需要配置`Babel`，将 ES6 转成 ES5

1. babel preset env 编译 ES6 到 ES5
2. babel preset react 编译 JSX 语法糖

```bash
yarn add @babel/core babel-loader @babel/preset-env @babel/preset-react --dev
```

在根目录创建`.babelrc`配置

```json
{
  "presets": ["@babel/preset-env", "@babel/preset-react"]
}
```

在根目录创建`webpack.config.js`配置

```js
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader'
        }
      }
    ]
  }
};
```

对于 js 和 jsx 拓展名文件，通过 babel-loader，将 ES6 转换为 ES5

安装 React 相关依赖

```bash
yarn add react react-dom
```

安装配置 Webpack HTML 插件

```bash
yarn add html-webpack-plugin html-loader --dev
```

`webpack.config.js`配置

```js
const HtmlWebPackPlugin = require('html-webpack-plugin');
module.exports = {
  module: {
    rules: [
      {
        test: /\.(js|jsx)$/,
        exclude: /node_modules/,
        use: {
          loader: 'babel-loader'
        }
      },
      {
        test: /\.html$/,
        use: [
          {
            loader: 'html-loader'
          }
        ]
      }
    ]
  },
  plugins: [
    new HtmlWebPackPlugin({
      template: './src/index.html',
      filename: './index.html'
    })
  ]
};
```

在`src/index.html`路径，建立 html 文件

```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Document</title>
  </head>
  <body>
    <div id="app"></div>
  </body>
</html>
```

在`src/index.js`路径，建立 webpack 入口

```js
import React from 'react';
import ReactDOM from 'react-dom';

const App = () => <div>hello world</div>;
const Container = document.getElementById('app');
ReactDOM.render(<App />, Container);
```

执行打包

```bash
yarn run build
```

文件已在`dist`文件夹生成，预览打包文件

```js
npx run http-server dist/
```

配置开发环境热更新
安装依赖

```bash
yarn add webpack-dev-server --dev
```

配置`package.json`

```
"scripts": {
  "start": "webpack-dev-server --open --mode development",
  "build": "webpack --mode production"
}
```

启动

```
yarn start
```

done
