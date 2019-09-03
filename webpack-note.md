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
- 输出（output）
- loader
- 插件（plugins）

<span id="entry">
### 入口（entry）
是指`webpack` 在打包项目的时候一个起点文件，可以引用多个入口起点。在进入口之后，会看那些模块、依赖和入口起点的关系，在打包。输出到 bundler

例子：

```javascript {.line-numbers}
module.exports = {
  entry: './file.js'
};
```
#未完待续....

[^1]: [webpack 中文网](https://www.webpackjs.com/concepts/)