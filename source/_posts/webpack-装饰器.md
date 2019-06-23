---
title: Webpack decorator 装饰器
date: 2019-06-23 22:48:17
tags: Webpack
---

# Webpack decorator 装饰器

安装依赖

```bash
yarn add --dev @babel/plugin-proposal-class-properties @babel/plugin-proposal-decorators @babel/plugin-syntax-decorators
```

配置`.babelrc`

```json
"plugins": [
    [
      "@babel/plugin-proposal-decorators",
      {
        "legacy": true
      }
    ],
    [
      "@babel/plugin-proposal-class-properties",
      {
        "loose": true
      }
    ]
  ]
```
