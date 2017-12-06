## JS的this大法

经常能看到关于this的博文，分享等，下面来谈谈前端小菜鸟眼中的this

关于this的概述，要说的这么一点：

1. this是javascript语言的一个关键字

2. 函数运行时，自动生成的一个内部对象，只能在函数内部使用

   ```
   function fun () {
     this.name = 'dingding'
   }
   ```

3. 随着函数使用的不同场合，this指向会发生变化，generally speaking，**this指向调用函数的那个对象**



### This 的六种情况使用

1. **纯函数调用**

   ```
   function test1 () {
     this.x = 1;
     alert(this.x)
   }

   test1() 	// 1
   ```

   ```
   var x = 1
   function test2 () {
     this.x = 0
     alert(x)
   }
   test2 (); 	// 0
   ```

   ​	很明显，这里test在全局作用域下被调用，this指向window，this.x 在函数中被篡改，window.x = 0 因此结果是0

2. **作为对象方法调用**

   ```
   var obj = {
     x: 1,
     f: function test3 (){
       alert(this.x)
     }
   }
   obj.f() 	// alert 1
   ```

   当函数作为某个对象的属性被调用,this指向该对象

3. **作为构造函数调用**

   ```
   var x = 2
   function test4 () {
     this.x = 0
   }
   var obj = new test4()
   obj.x 		// 0
   window.x 	// 2
   ```

   this指向的是构造函数new出来的obj这个新的对象，而不是指向window，因此出现以上结果

4. **call/apply调用**

   apply是函数对象的一个方法，作用就是改变函数的调用对象

   ```
   var x = 2
   var obj = {
     x: 1,
     f: function test3 (){
       alert(this.x)
     }
   }
   obj.f.apply() 		// alert 2
   obj.f.apply(obj) 	// alert 1
   ```

   apply 参数为空 默认的第一个参数（调用该函数的新对象）默认指向window

5. **bind调用**

   Function.prototype.bind

   举一个🌰

   ```
   this.x = 9
   var module = {
     x: 81,
     getX: function() {
       return this.x
     }
   }

   module.getX() 	// 81

   var windowGetX = module.getX
   windowGetX() 	// 9

   var boundGetX = module.getX.bind(module)()	// 81
   ```

   再来一个🌰

   ```
   var name="DingDing";
   function Person(name){
   	this.name=name;
   	this.sayName = function () {
   		setTimeout(function () {
   			console.log("my name is "+this.name);
   		},50)
   	}
   }

   var person=new Person("dingding");
   person.sayName() 	// my name is DingDing
   ```

   怎么才能输出 my name is dingding呢？

   ok 方案1: 利用call / apply 改变this 指向window

   ```
   person.sayName.call()
   or 
   person.sayName.apply()
   ```

   方案2：利用bind修改this指向

   ```
   var name="DingDing";
   function Person(name){
   	this.name=name;
   	this.sayName = function () {
   		setTimeout(function () {
   			console.log("my name is "+this.name);
   		}.bind(this),50)
   	}
   }

   var person=new Person("dingding");
   person.sayName() 	// my name is dingding
   ```

   setTimeout 默认由window修改成指向person 因此 person.name === 'dingding'

   方案3: 其实我们经常会用到，至少我经常用，就是这么干

   ```
   var name="DingDing";
   function Person(name){
   	this.name=name
   	var that = this
   	this.sayName = function () {
   		setTimeout(function () {
   			console.log("my name is " + that.name);
   		},50)
   	}
   }

   var person=new Person("dingding");
   person.sayName() 	// my name is dingding
   ```

   person中的this 已经由that代替，so~  setTimeout 中that.name === ’dingding‘  蓝鹅 this 依然指向 window，但是又有什么关系呢，我们又不用，是吧！

6. **箭头函数**

   说到箭头函数，那就比较厉害了！面试中，我也会问面试者，箭头函数中，遇到过什么坑？

   箭头函数最大的坑，就是**没有this!** this 固定化，始终指向外部对象。因此，不仅自身不能实例化，也不能用call,apply, bind来改变this指向～

   ```
   function Timer() {
   	this.seconds = 0;
   	setInterval( function() {this.seconds ++} , 1000);
   } 
   var timer = new Timer();
   setTimeout(function(){console.log(timer.seconds)}, 3000) // 0 
   ```

   setInterval( function () { console.log(this.seconds); this.seconds ++} , 1000)

   如果把this.seconds打印出来，你会看到 每隔一秒打印一个NaN，因为 setInterval 里的this跟Time内部的this 没有半毛钱关系，所以：

   this.seconds = undefined ++ = NaN

   如果我们使用箭头函数呢？会怎么样？

   ```
   function Timer() {
   	this.seconds = 0;
   	setInterval( () => this.seconds ++, 1000);
   } 
       
   var timer = new Timer();
   setTimeout( () => console.log(timer.seconds), 3000); 	// 3
   ```

   构造函数内部的setInterval 内的回调函数 this 始终指向实例化对象 即 timer



**Fine 关于this 总结的也就是这么几点，其实有时候经常用到的一些东西，真的未必你都能理解，如果真的都理解的，那么你写代码的效率提高的肯定不止一个level!**

