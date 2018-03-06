## Series Of Small Notes

1. void 0 获取undefined的准则，underscore中

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

2. ​

