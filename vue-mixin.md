## vue-mixin

### 作用

**混入 **是一种分发vue组件可复用功能的一种方式



### 使用方法

1. 常规钩子函数（options）: 没有复用性

   ```
   export default {
   	methods: {
           test () {
             console.log('i am dingding in comp-mixin')
           }
       }
   }
   ```

   ​

2. 组件内定义mixin对象

   ```
   export default {
     mixins: [{
         methods: {
           test () {
             console.log('i am dingding in options')
           }
         }
     }]
   }
   ```

   ​

3. 全局定义

   ```
   // 导出mixin配置文件
   export default {
     methods: {
       test () {
         console.log('i am dingding in mixin')
       }
     }
   }

   // 导入mixin配置
   import MyMixin from '../xx.js'
   Vue.mixin(MyMixin)
   ```



###混合使用 权重策略

从后往前覆盖：全局mixin => 组件内mixin => options => options内部后者覆盖前者



###控制全局mixin在组件是否执行

利用组件定义options属性来标记

```

```

