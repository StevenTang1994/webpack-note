# webpack

**写在最前面**

如果是想学`webpack`请移步[官方文档](https://www.webpackjs.com/concepts/)，本文章只是我**自己学习的笔记**

自己想学 `webpack` 也不是一天两天了，但是一直在拖，这次不能在拖了

## 为什么会出现 webpack

随着互联网的快速增长，简单的`H5`页面已经满足人们的需求，`web` 页面越来越复杂，模块化编程这个之前属于后端开发的概念（不只是模块化编程）也慢慢的前移。`web`存在多种支持`javaScript`模块化的工具，这些工具各有优势和限制。`webpack` 基于从这些系统获得的经验教训，并将模块的概念应用于项目中的任何文件。[^1]

## 概念
本质上，`webpack` 是一个现代 `javaScript` 应用程序的静态模块打包器(module bundler)。当 `webpack` 处理应用程序时，它会递归地构建一个依赖关系图(dependency graph)，其中包含应用程序需要的每个模块，然后将所有这些模块打包成一个或多个 bundle。[^1]

按照文档说的，开始前要先理解**四个核心概念**：
- [入口（entry）](#entry)
- [输出（output）](#output)
- [loader](#loader)
- [插件（plugins）](#plugins)

<span id="entry">

### 入口（entry）

是指`webpack` 在打包项目的时候一个起点文件，可以引用多个入口起点。在进入口之后，会看那些模块、依赖和入口起点的关系，在打包。输出到 bundler

例子：

```javascript {.line-numbers}
module.exports = {
  entry: './file.js'
};
```
<span id="output">

### 出口（output）

是指`webpack` 在打包之后输出在哪个文件目录下，叫什么名字，默认值为`./dist`

例子:
```javascript {.line-numbers}
const path = require('path');

module.exports = {
  entry: './path/to/my/entry/file.js',
  output: {
    path: path.resolve(__dirname, 'dist'),
    filename: 'my-first-webpack.bundle.js'
  }
};
```

<span id="loader">

### loader

可以处理非`javascript`的文件（webpack 自身只理解 JavaScript）,`loader`可以把文件处理成`webpack`能够处理的有效模块。

本质上，webpack loader 将所有类型的文件，转换为应用程序的依赖图（和最终的 bundle）可以直接引用的模块。

有两个属性 `test`、`use`
- test： 用于标识出应该被对应的 loader 进行转换的某个或某些文件。
- use： 表示进行转换时，应该使用哪个 loader。

例子：
```javascript {.line-numbers}
const path = require('path');

const config = {
  output: {
    filename: 'my-first-webpack.bundle.js'
  },
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  }
};

module.exports = config;
```
在`module`里面创建了`rules`属性，包含了两个必要的属性`test`、`use`

>上面的代码用通俗的语句来说就是：“嘿，webpack 编译器，当你碰到「在 require()/import 语句中被解析为 '.txt' 的路径」时，在你对它打包之前，先使用 raw-loader 转换一下。”

<span id="plugins">

### 插件(plugins)

loader可以应用各种类型的文件，但是插件的的功能更加的强大。如果你想要引入一个插件需要`require()`,在添加到`plugins `数组里面去

多数插件可以通过选项(option)自定义。你也可以在一个配置文件中因为不同目的而多次使用同一个插件，这时需要通过使用 new 操作符来创建它的一个实例。

例子: 
``` javascript {.line-numbers}
const HtmlWebpackPlugin = require('html-webpack-plugin'); // 通过 npm 安装
const webpack = require('webpack'); // 用于访问内置插件

const config = {
  module: {
    rules: [
      { test: /\.txt$/, use: 'raw-loader' }
    ]
  },
  plugins: [
    new HtmlWebpackPlugin({template: './src/index.html'})
  ]
};

module.exports = config;
```

### 模式
通过选择 `development` 或 `production` 之中的一个，来设置 `mode` 参数，你可以启用相应模式下的 `webpack` 内置的优化

例子:
```javascript {.line-numbers}
module.exports = {
  mode: 'production'
};
```

[^1]: [webpack 中文网](https://www.webpackjs.com/concepts/)