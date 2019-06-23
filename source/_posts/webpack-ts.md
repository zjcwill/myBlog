---
title: webpack  配置 Typescript + React
date: 2019-06-23 22:49:48
tags: Webpack
---

# webpack Typescript + React

在已有的 react 项目中 安装 React 依赖

```js
yarn add --dev @types/react @types/react-dom
```

安装 ts 依赖

```js
yarn add -dev ts-loader typescript
```

建立 ts 配置文件`tsconfig.json`

```js
{
  "compilerOptions": {
    "outDir": "./dist/",
    "sourceMap": true,
    "noImplicitAny": true,
    "module": "commonjs",
    "target": "es5",
    "jsx": "react"
  },
  "include": ["./src/**/*"]
}
```

修改 webpack 配置

```js
{
    module: {
        rules: {
            {
                test: /\.(ts|tsx)?$/,
                use: {
                  loader: 'ts-loader'
                },
                exclude: /node_modules/
            },
        }
    },
    resolve: {
        extensions: ['.tsx', '.ts', '.js']
    },
}
```
