## 深入理解格式块上下文（BFC）

在问格式块上下文之前，我们回顾一个问题：

Q: 行与块的区别是什么？

A：主要是以下三个区别

1. 块独占一行（最明显的区别）
2. 可以容纳块或行为子元素
3. 行元素不能设置height、line-height、margin-top、margin-bottom



**开始进入主题**

Q: 什么是格式块上下文？

A: 块级盒模型发生的区域...

Q: 什么情况下会触发bfc？

A: 那情况就多了，个人常用元素罗列一下，不常用的不管了 ：）

* display: inline-block、flex、grid、table-cell等
* float
* position: absolute、fixed
* overflow



**触发BFC会有什么影响？**

在布局过程中，我们往往会使用float、flex、定位等来实现我们想要的布局，效果的实现伴随的副作用的出现，比如：

1. 浮动对夫、兄元素带来的麻烦（夫：高度，兄：图文环绕）
2. 合并外边距



Q：什么是合并外边距？

A：两个相邻盒子的外边距结合成一个单独的外边距的现象称为合并外边距，也叫折叠外边距

Q：怎么计算合并后的边距？

A：也是三种计算规则：

* 正正，边距取最大值
* 负负，边距取绝对值最大值
* 正负，边距取相加之和

Q：产生折叠的必要条件？

A：两个margin紧挨...

Q：如何算是两个盒子margin边距紧挨？

A：**敲黑板！**

* 必须是处于常规文档流的块级盒子，并且处在同一个BFC中
* 没有clearance，没有padding，border隔开
* 垂直方向上的外边距满足以下任意情况，即可召唤神龙
  * 元素的margin-top与其第一个常规文档流的子元素的margin-top
  * 元素的margin-bottom与其下一个常规文档流的兄弟元素的margin-top
  * height为auto的元素的margin-bottom与其最后一个常规文档流的子元素的margin-bottom
  * 高度为0并且最小高度也为0，不包含常规文档流的子元素，并且自身没有建立新的BFC的元素的margin-top和margin-bottom



**Generally speaking 解决如何外边距折叠的问题？**

1. clearance、给1px的padding或者margin
2. 父子关系：父元素触发BFC，使子元素处于非常规文档流中
3. 兄弟关系：按需求触发BFC
4. inline-block：无论父子还是兄弟，都不会产生折叠边距
5. 如何触发BFC ? 请爬楼，请爬楼...



### Over 日常随便写写...





