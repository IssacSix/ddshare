[TOC]

## webpack回顾小结

### 概念

### 四个key points

#### entry

1. 单个入口写法

2. 对象语法

3. app + vendor

   ```
   const config = {
     entry: {
       app: './src/app.js',
       vendors: './src/vendors.js'
     }
   }
   ```

4. 多页面应用

   ```
   const config = {
     entry: {
       pageOne: './src/pageOne/index.js',
       pageTwo: './src/pageTwo/index.js',
       pageThree: './src/pageThree/index.js'
     }
   }
   ```

   使用 `CommonsChunkPlugin` 为每个页面间的应用程序共享代码创建 **bundle** ,多页应用能够复用入口起点之间的大量代码/模块。

#### output

1. 多个入口起点

   ```
   {
     entry: {
       app: './src/app.js',
       search: './src/search.js'
     },
     output: {
       filename: '[name].js',
       path: __dirname + '/dist'
     }
   }
   // 写入到硬盘：./dist/app.js, ./dist/search.js
   ```

2. ​

#### loader

模块与资源的转化器，本身是一个函数，接受源文件作为参数，返回转化的结果

1. 通过管道链式调用，上一个转化任意格式给下一个
2. 可同步可异步
3. 可接受参数，传递配置项给loader
4. 可访问配置

#### plugins

loader的功能补充

实现原理：

​	是一个具有apply属性的 JavaScript 对象。apply 属性会被 webpack compiler 调用，并且 compiler 对象可在**整个**编译生命周期访问。

```
function ConsoleLogOnBuildWebpackPlugin() {

};

ConsoleLogOnBuildWebpackPlugin.prototype.apply = function(compiler) {
  compiler.plugin('run', function(compiler, callback) {
    console.log("webpack 构建过程开始！！！");

    callback();
  });
};
```



###开发环境

1. webpack  - - progress - - colors

2. webpack  - - progress - - colors  - - watch

3. webpack-dev-server

   * ```
     # 安装
     $ npm install webpack-dev-server -g
     ```

   * ```
     # 运行
     $ webpack-dev-server --progress --colors
     ```



###故障处理

通过参数具体排查某个模块的错误

```
webpack --display-error-details
```



###CommonJS规范

建议也是比较习惯 使用commonJs规范定义模块