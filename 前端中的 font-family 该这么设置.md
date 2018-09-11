[TOC]

##前端中的 font-family 该这么设置？

`font-family`允许您通过给定一个有先后顺序的，由字体名或者字体族名组成的列表来为选定的元素设置字体



### 解析原理

`font-family` 属性指定的是一个优先级从高到低的可选字体列表。 字体的选定**不是**在发现用户计算机上安装的列表中的第一个字体时停止。相反，对字体的选择是**逐字**进行的。也就是说即使某个字符周围都在某个字体中可以显示，但该字符在当前的字体文件中没有适合的图形，那么会继续尝试列表中靠后的字体



###有效族名

浏览器默认字体可直接解析中文字体名称

1. 引号包括的字符串
2. 字体族
3. 不带引号的一个或多个合法标识串（数字、标点开头非法）



###多种族名顺序定义策略

1. 英文族名优先

   绝大部分中文字体里都包含英文字母和数字，不进行英文字体声明是没有问题的，但是大多数中文字体中的英文和数字的部分都不是特别漂亮，所以建议也对英文字体进行声明。 由于英文字体中大多不包含中文，我们可以先进行英文字体的声明，这样不会影响到中文字体的选择，因此优先使用最优秀的英文字体，中文字体声明则紧随其次

2. 补充族名（最后兜底设置）

   * sans-serif
   * serif



### 疑点

1. 何时需要加上引号
   * 具体取值一种样式名 并且 包含空格，需要加上引号
   * 中文书写，保证兼容性，可以加上引号

### 浏览器默认字体

#### windows常见内置中文字体

1. 宋体
2. 黑体
3. 微软雅黑
4. 微软正黑
5. 楷体
6. 新宋
7. 仿宋

#### OS X常见内置中文字体

1. 苹方
2. 华文黑体
3. 华文楷体
4. 华文宋体
5. 华文中宋
6. 华文琥珀
7. ...

#### 开源字体

1. 思源黑体
2. 思源宋体
3. 文泉驿微米黑



###我们的几个工程的font-family又是如何设置的

####stp-page-client

```
font-family: Microsoft YaHei,Helvetica Neue Light Pro,tahoma,arial,Hiragino Sans GB,sans-serif;
```

####stp-page-wap

```
font-family: Helvetica Neue,Helvetica,Roboto,Segoe UI,Arial,sans-serif;
```

####stp-page-pc

```
font-family: "Microsoft Yahei";
```

#### 存在的问题

1. 顺序设置随意
2. 字体名、族名没有分清，引用比较随意
3. 由上面一条导致是否需要使用引号不明确，干脆全部去掉引号，这是不对的
4. 没有对特定的业务场景进行合理选择，比如 client中根本不需要考虑osx的字体渲染



### 参考设置

#### 小米

```
font-family: "Helvetica Neue", Helvetica, Arial, "Microsoft Yahei", "Hiragino Sans GB", "Heiti SC", "WenQuanYi Micro Hei", sans-serif
```

#### 淘宝

```
font-family: tahoma, arial, "Hiragino Sans GB", 宋体, sans-serif
```



