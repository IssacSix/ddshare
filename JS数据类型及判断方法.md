## JS数据类型及判断方法

### 6种基本类型（值类型,按值访问）

1. null
2. undefined
3. string
4. boolean
5. number
6. symbol

### 一种特殊类型：object（引用类型）



###值类型与引用类型的区别

1. 值类型一旦确定就不可变
2. 值类型的比较是值的比较



### 判断数据类型

1. typeof

   ```
   typeof ''; // string 有效
   typeof 1; // number 有效
   typeof Symbol(); // symbol 有效
   typeof true; //boolean 有效
   typeof undefined; //undefined 有效
   typeof null; //object 无效
   typeof [] ; //object 无效
   typeof new Function(); // function 有效
   typeof new Date(); //object 无效
   typeof new RegExp(); //object 无效
   ```

   * 基本类型（null除外）正确返回类型
   * null、引用类型等返回的原型链最顶端的object
   * function 返回 function

2. instanceof（原型检测)

   ```
   [] instanceof Array; // true
   {} instanceof Object;// true
   new Date() instanceof Date;// true
    
   function Person(){};
   new Person() instanceof Person;
    
   [] instanceof Object; // true
   new Date() instanceof Object;// true
   new Person instanceof Object;// true
   ```
   从以上可以看出

   ```
   [] instanceof Array 即为 [].__proto__ === Array.prototype 间接指向 Object.prototype
   ```

   **so~ 用instanceof判断一个对象的类型，其实并不准确，更加适合判断两个对象是否属于实例关系**

3. constructor(构造函数检测)

   **当一个函数被定义时，JS引擎会为此函数添加 prototype 原型，然后再在 prototype上添加一个 constructor 属性，并其指向 F **

   ```
   const arr = []
   
   arr.constructor === Array // true
   ===
   arr.constructor === arr.__proto__.constructor === Array.prototype.constructor === Array
   ```

   **constructor是不稳定的，因为prototype可以被重写，那么constructor的指向就会被修改**

4. toString

   ```
   const arr = []
   Object.prototype.toString.call(arr)
   ```

5. Array.constructor
   ƒ Function() { [native code] }
   Array.prototype.constructor
   ƒ Array() { [native code] }

6. Array.constructor
   ƒ Function() { [native code] }
   Array.prototype.constructor
   ƒ Array() { [native code] }

7. Array.constructor
   ƒ Function() { [native code] }
   Array.prototype.constructor
   ƒ Array() { [native code] }

8. Array.constructor
   ƒ Function() { [native code] }
   Array.prototype.constructor
   ƒ Array() { [native code] }