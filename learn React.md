[TOC]

# Some notes about learning React

## About JSX

Q：什么是jsx？

A：js语法的一种扩展，似HTML 又不是HTML

Q：jsx有什么作用？

A：描述组件的结构

Q：原理？

A：jsx【babel编译 + react构造】=>	js 对象结构【react-dom】 =>  DOM元素  =>  插入页面



## About State

1. 只能通过setState() 方法的调用修改 state上的值
2. setState 接受对象或者函数作为参数
3. 更新队列中state值有缓存
4. **setState合并：** 多次的setState，实际上组件之后重新渲染一次，而不是多次，内部会对EventLoop中的同一个消息中的setState进行合并之后再重新渲染组件，因此并不会带来性能问题。



## About Props

1. 标签属性配置props

2. 可设置默认prop

   ```
   static defaultProps = {
     key: value
   }

   render() {
     return (
     	<h1>this.props.key</h1>
     )
   }
   ```

   ​

3. props 不可直接修改，但是可以通过修改state修改传入的参数

   ```
   class someComponent extends Component {
   	constructor () {}
     	someFun () {
       	this.props.key = _newValue
     	}
   }

   ReactDOM.render(
   	<someComponent key='value'/>
   )
   // 报错
   ```

   但是可以这么做，通过父组件主动重新渲染传入新的props，从而更改props

   ```
   class someComponent extends Component {
   	constructor () {}
     	someFun () {
       	this.props.key = _newValue
     	}
   }

   ReactDOM.render(
   	<someComponent key=this.state.key/>
   )
   ```



## State VS Props

state：是让组件自己控制自己的状态

props：是让外部对组件自己进行配置

**有状态组件：**包含state的组件叫，反之，称为：无状态组件

