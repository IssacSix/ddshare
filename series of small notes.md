[TOC]

## Series Of Small Notes

### void 0 

void 0获取undefined的准则，underscore中

```
_.isUndefined = (obj) {
  return obj === void 0
}
```

Q: void 0 获取undefined原因？

A: 在js中undefined不是保留关键字，低版本ie可以被篡改

```
let undefined = 10
alert(undefined) // 10
```

A：ES5中全局对象read-only 局部作用域还是可以被重写。综上，还是void 0 来获取undefined稳健



### 屏幕分辨率可视内容宽高等API

详细API list

```
function getScreenInfo() { 
    var s = ""; 
    s = " 网页可见区域宽：" document.body.clientWidth; 
    s = " 网页可见区域高：" document.body.clientHeight; 
    s = " 网页可见区域宽：" document.body.offsetWidth " (包括边线和滚动条的宽)"; 
    s = " 网页可见区域高：" document.body.offsetHeight " (包括边线的宽)"; 
    s = " 网页正文全文宽：" document.body.scrollWidth; 
    s = " 网页正文全文高：" document.body.scrollHeight; 
    s = " 网页被卷去的高(ff)：" document.body.scrollTop; 
    s = " 网页被卷去的高(ie)：" document.documentElement.scrollTop; 
    s = " 网页被卷去的左：" document.body.scrollLeft; 
    s = " 网页正文部分上：" window.screenTop; 
    s = " 网页正文部分左：" window.screenLeft; 
    s = " 屏幕分辨率的高：" window.screen.height; 
    s = " 屏幕分辨率的宽：" window.screen.width; 
    s = " 屏幕可用工作区高度：" window.screen.availHeight; 
    s = " 屏幕可用工作区宽度：" window.screen.availWidth;
    s = " 你的屏幕设置是 " window.screen.colorDepth " 位彩色"; 
    s = " 你的屏幕设置 " window.screen.deviceXDPI " 像素/英寸"; 
} 
```



### console 小技巧

1. 打印多个值

   ```
   console.log(`name:${ding}`, `age:${age}`)
   ```

2. assert(boolean, 'error log text')

   ```
   console.assert(list.childNodes.length < 500, "Node count is > 500")
   ```

3. error(),  warn()

4. 查看数据结构

   ```
   console.table([{a:1, b:2, c:3}, {a:"foo", b:false, c:undefined}]);
   console.table([[1,2,3], [2,3,4]]);
   ```

5. 字符串裁剪格式化

   - %s - 字符串格式
   - %i 或 %d - 整型格式
   - %f - 浮点格式
   - %o - DOM节点
   - %O - JavaScript 对象
   - %c - 对输出的字符串使用css样式，样式由第二个参数指定

   ```
   console.log('name is %s, and her age is %d, time is %f', 'dingding', 25, Date.now())
   VM5188:1 name is dingding, and her age is 25, time is 1524021307249
   ```

6. Dom对象转化为js对象：console.dir()

7. 耗时监控：console.time('need count time') / consle.timeEnd('need count time')