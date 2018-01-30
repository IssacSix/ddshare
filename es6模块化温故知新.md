[TOC]

## ES6 Module 

### 概述：

  （没啥知新的，主要就是温故，就是整体过一遍）

  对于js模块化这点内容，我个人觉得其实有点坑的，CommonJS + ES6自身的模块化机制，让很多新入门的同学傻傻分不清楚，关于前端模块化工具CommonJS跟AMD之前有整理过一篇文档，移步[我对前端模块化的认识与理解](https://github.com/IssacSix/ddshare/blob/master/%E5%89%8D%E7%AB%AF%E6%A8%A1%E5%9D%97%E5%8C%96.md) 希望不要误导大家。

  模块化是每种语言都有的功能，就连css都有@import，但是ES6之前没有原生的api支持，除非使用CommonJS 或者 AMD，成为客户端跟服务端的模块化解决方案。

  ES6延用的是CommonJS的规范，但是有别与CommonJS。

1. **尽量的静态化**
2. **代码块**
3. **动态绑定输出值**，CommonJS对输出值缓存，es6及时更新

  因为CommonJS"运行时加载"的特性，使得其运行后才能得到这个对象，注意是 **一个对象**，但ES6的设计思想是尽量的静态化，es6的模块不是一个对象，而是通过export 再 import之后的 **代码块**，使得在编译时就完成了加载。



### 命令

#### export

export可输出的类型 变量、函数、类

```
1.变量
var firstName = 'Ding';
var lastName = 'Issac';
export {firstName, lastName};

2.函数 或 类
export multiply = function (x, y) {
  return x * y;
}

3.输出默认变量或者方法
export default function () {
  console.log('foo');
}
```

默认default 命令注意点：

1. 一个模块只能有一个默认输出
2. import 可以不加大括号
3. 声明变量必须在export default 之前
4. export default 也可以输出类



#### import

1. import会执行所加载的模块
2. import命令具有提升效果，编译阶段会提升到整个模块的头部

```
1. import { lastName as surname } from './profile.js'
2. import customName from './export-default' // 引入默认类
```



#### 整体加载模块

```
1.逐一加载
import { area, circumference } from './circle'
console.log('圆面积：' + area(4))
console.log('圆周长：' + circumference(14))

2.整体加载
import * as circle from './circle';
blablabla 同上
```



#### 按需加载 import()

由于import 编译时加载，有一个[提案](https://github.com/tc39/proposal-dynamic-import)，建议引入`import()`函数，完成动态加载

举个🌰

```
const main = document.querySelector('main');

import(`./section-modules/${someVariable}.js`)
  .then(module => {
    module.loadPageInto(main);
  })
  .catch(err => {
    main.textContent = err.message;
  });
```

**动态加载**

区别于node require import 异步加载，require 同步

使用场合：

1. 按需加载

   ```
   button.addEventListener('click', event => {
     import('./dialogBox.js')
     .then(dialogBox => {
       dialogBox.open();
     })
     .catch(error => {
       /* Error handling */
     })
   });
   ```

   ​

2. 条件加载

   ```
   if (condition) {
     import('moduleA').then(...);
   } else {
     import('moduleB').then(...);
   }
   ```

   ​

3. 动态的模块路径

   ```
   import(f())
   .then(...);
   ```



**注意点：**

1. import() 模块加载成功后，作为一个对象，当作then方法中的参数。

2. import() 也可以用在async函数中

   ```
   async function main() {
     const myModule = await import('./myModule.js');
     const {export1, export2} = await import('./myModule.js');
     const [module1, module2, module3] =
       await Promise.all([
         import('./module1.js'),
         import('./module2.js'),
         import('./module3.js'),
       ]);
   }
   main();
   ```