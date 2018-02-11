## 我对Vue 虚拟Dom原理的理解

1. 字符串模版，正则匹配解析生成虚拟dom对象
2. 生成redener函数
3. 执行render返回Vnode
4. Vnode拼接字符串HTML解析渲染


### 真实Dom解析机制



### 虚拟DOM的弊端

1. 大小：代码包变大
2. 内存：虚拟DOM需要copy到内存中，这是更新速度跟内存之间的权衡
3. 适用场景：批量性修改，大量的DOM需要重新计算的情况，比如SPA



### 虚拟DOM设计思想

1. 提供一种方便的工具，开发效率的保证


2. 保证最小化的DOM操作，执行效率的保证




###mvvm随便扯扯

MVC等架构模式的框架，为了实现由数据变动，重新绘制视图的成本过高，会有哪些？

1. 为了记住某种状态，使用过多字段进行标记
2. 事件监听，回调处理DOM的代码随着业务的增加，越来越多，越来越复杂，越来越难维护
3. 操作DOM,重新渲染视图

MVC、MVP等架构模式与其他或者不应用模式有区别？其实，我个人觉得没有什么实质性的区别，只是通过了架构模式，规范了业务逻辑代码放置的位置，稍稍降低了复杂应用程序的维护成本，对于DOM来说，改操作还是操作，并没什么卵用...

**Q：能不能将试图跟状态进行绑定？**

**A：能！我们用MVVM**

感谢大佬们的智慧，让我们这些搬砖的可以轻点虐~



所谓的Virtual DOM 算法，一下步骤：

1. js对象构建object DOM tree，构建real DOM tree插入到文本中
2. 状态变更时，重新构建一棵new object DOM tree，对比新旧，记录差异
3. 差异应用到real DOM tree，update view

virtual DOM本质上就是在JS跟DOM之间增加一个缓存缓冲区，比如CPU跟磁盘之间加了一个内存。



#### 算法实现

1. js obejet DOM tree

   ```
   function Element (tagName, props, children) {
     this.tagName = tagName
     this.props = props
     this.children = children
   }

   export default function (tagName, props, children) {
     return new Element (tagName, props, children)
   }

   ```

   ​

2. object 通过render生成真正的DOM树

   ```
   Element.prototype.render = function () {
     let el = document.createElement(this.tagName)
     let _props = this.props
     _props.forEach ( (props) => {
       el.setAttribute(props.propName, props.propValue)
     })
     
     let _children = this.children || []
     _children.forEach ( (child) => {
       let childEl = child instanceof Element ? child.render() :  docoment.createTextNode(child)
       el.appendChild(childEl)
     })
     return el
   }
   ```

   ​

3. ​



























### 参考文档

1. [《全面理解虚拟DOM、实现虚拟DOM》](https://foio.github.io/virtual-dom/)































