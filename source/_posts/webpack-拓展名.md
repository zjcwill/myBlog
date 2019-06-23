---
title: Webpack 配置import 省略文件拓展名称
date: 2019-06-23 22:47:33
tags: Webpack
---

# Webpack 配置 import 省略文件拓展名称

## `resolve.extensions`[](#resolve-extensions)

`[string]: ['.wasm', '.mjs', '.js', '.json']`

自动解析确定的扩展。默认值为：

**webpack.config.js**

```
module.exports = {
  //...
  resolve: {
    extensions: ['.wasm', '.mjs', '.js', '.json']
  }
};

```

能够使用户在引入模块时不带扩展：

```
import File from '../path/to/file';

```

> 使用此选项，会**覆盖默认数组**，这就意味着 webpack 将不再尝试使用默认扩展来解析模块。对于使用其扩展导入的模块，例如，`import SomeFile from "./somefile.ext"`，要想正确的解析，一个包含“\*”的字符串必须包含在数组中。
