[TOC]

## JS内存泄漏的原因及识别

### 概述：什么是内存泄漏

程序的运行需要内存，只要程序提出要求，操作系统运行时就必须要分配内存。对于持续运行的进程，必须及时释放没用的内存，否则内存占用越来越高，影响系统运行或者直接奔溃。

**对于没有再用到的内存，没有及时释放，就叫做内存泄漏**



### 什么是垃圾回收

内存可以手动清理，但是很多语言都提供内存自动管理，简化管理内存的代码，这就被称为 **垃圾回收机制**

#### 垃圾回收机制如何得知已不再需要的内存？

1. **引用计数法**

   这是一种最常用的方法。语言引擎有一张“引用表”，保存了内存中所有的值的引用次数，当某个值的引用次数为0，就表示这个值已经没有被用到，可以被释放了。



#### V8 垃圾回收机制



### 导致内存泄露的情况及处理

#### 情况1

某个值没有被用到，但是引用次数不为0

```
var arr = [1,2]
console.log('i am dingding')
```

 尽管 arr这个变量没有被用到，但是arr的引用次数为1，所以依然会占用内存，如何解除？

阮大大举了这么一个🌰

```
var arr = [1,2]
console.log('i am dingding')
arr = null
```

arr 被重置，解除了对[1,2]的引用，引用次数就变成了0，内存就可以被释放了。因此，并不是说有了垃圾回收机制，我们就轻松了。你还是需要关注内存占用，对那些很占空间的值，一旦不再用到，你就需要检查是否还存在对它们的引用。如果是的话，就必须手动解除引用。

**以上的伪代码，实际情况中，出现的可能性很小很小，为什么？** 不仅是阮大大举过这个例子，在《js高级程序设计》中有一个章节也出现过，但是对于前端小菜鸟来说，其实这个栗子实为不妥，原因：

1. all = null ？虽然理论上来说，可行，但是实际编程中不应该是通过这种操作手动清除，一般的编程规范也不会允许你这么去写。去坑的这几年，这种代码我是一行都没写过，因为我不知道要清除内存。。。
2. arr 是个全局变量？什么情况下我们真的需要定义一个变量在全局作用域下？往往是编程习惯的不妥
3. 一般内存泄漏的情况，大多是在闭包中，函数执行完，但是内部变量依然留在内存中，这就造成了内存泄漏！

#### 情况2:  意外的全局变量

```
function fun () {
  bar = "this is a hidden global variable" 
}
```

```
function fun () {
  this.bar = "potential accident global"
}
fun () // this 指向window 意外创建了一个全局变量
```

#### 处理：

js文件头部添加'use strict' 开启严格模式解析js，避免创建意外的全局变量



####情况3:  脱离DOM的引用





#### 情况4:  闭包会引起内存泄漏么







### 内存泄露的识别方法

1. chrome 浏览器

   ```
   1. 打开控制台
   2. 点击Memory
   3. 勾选Record allocation timeline
   ```

2. 命令行

   ​

### 避免内存泄漏的方法

大量引用类型的变量，都需要手动清除，是十分麻烦的，那么有咩有一种引用申明可以让垃圾回收机制不考虑该对象的引用，当其他对象都不再引用该对象，垃圾回收就可自动回收了，所以主要清楚主要的引用就方便很多了。

**有的！**

ES6考虑到了这点，推出两种新的数据结构 weakSet WeakMap,它们的对于值的引用就是不计入垃圾回收机制

#### WeakSet

1. WeakSet 是一个构造函数 通过new 创建

2. 成员类型只允许是 => 对象

   ```
   const a = [[1, 2], [3, 4]];
   const ws = new WeakSet(a);
   // WeakSet{[1, 2], [3, 4]}

   const b = [3, 4];
   const ws = new WeakSet(b);
   // Uncaught TypeError: Invalid value used in weak set(…)
   ```

   数组b的成员不为对象，所以报错

3. weakSet 方法

   * **WeakSet.prototype.add(value)**：向 WeakSet 实例添加一个新成员。
   * **WeakSet.prototype.delete(value)**：清除 WeakSet 实例的指定成员。
   * **WeakSet.prototype.has(value)**：返回一个布尔值，表示某个值是否在 WeakSet 实例之中。

#### WeakMap

类似WeakSet(感觉实际用处并不大，我真的懒得写了 : )



### 参考资料

1. [《阮大大 内存泄漏教程》](http://www.ruanyifeng.com/blog/2017/04/memory-leak.html?utm_source=tuicool&utm_medium=referral/*&^%$)
2. [《4类js内存泄漏》](https://jinlong.github.io/2016/05/01/4-Types-of-Memory-Leaks-in-JavaScript-and-How-to-Get-Rid-Of-Them/)

