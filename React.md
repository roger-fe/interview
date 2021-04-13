# React

### 1. react的基本使用

```html
<script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
<script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
<script src="https://unpkg.com/babel-standalone@6/babel.min.js"></script>
```

```html
<script type="text/babel">
  // 1.创建虚拟DOM元素对象
  const vDom = <h1>Hello React!</h1>
  // 2.将虚拟DOM渲染到页面真实DOM容器中
  React.Dom.render(vDom,document.getElmentById('test'))
</script>

```

### 2. jsx练习

```js
const names=['jQuery','zepto','angular','react','vue']
console.log({names}) //react会自动遍历数据
//map函数可对数组的每一个元素进行操作，并且返回一个操作完的数组
names.map((name) => <li>{name}</li>)
```

### 3. react组件的基本定义和使用

```js
//1.定义组件
//方式1：工厂函数组件(简单组件：没有状态的组件)
function MyComponent1(){
  return <h2>工厂函数组件(简单)</h2>
}
//方式2：ES6类组件(复杂组件)
class MyComponent2 extends React.Component{
  render(){
    return <h2>ES6类组件(复杂组件)</h2> 
  }
}
//2.渲染标签
React.Dom.render(<MyComponent1/>,document.getElmentById('example1'))
React.Dom.render(<MyComponent2/>,document.getElmentById('example2'))
```

### 4. 组件属性之state

```js
construtor (props){
  super(props)
  //初始化state
  this.state = {
    isLikeMe:false
  }
  // 将新增方法中的this强制绑定为组件对象，用.bind()
 /* bind()方法主要就是将函数绑定到某个对象，bind()会创建一个函数，函数体内的this对象的值会被绑定		到传入bind()中的第一个参数的值，例如：f.bind(obj)，实际上可以理解为obj.f()，这时f函数体内的		this自然指向的是obj；*/
  this.handleClick = this.handleClick.bind(this)
}
//对于组件内部来说，新增方法：内部的this默认不是组件对象，而是undefined
handleClick(){
  //得到状态
  const isLikeMe = !this.state.isLikeMe
  //更新状态
  this.setState({isLikeMe});
}

render (){
  //读取状态
  const {isLikeMe} = this.state
  return <h2 onClick={this.handleClick}>{isLikeMe?"你喜欢我":"我喜欢你"}</h2>
}
```

### 5. 组件属性之props

```js
/*定义好组件后可以指定属性默认值*/
组件名字.defaultProps = {
  key:value
}
// 指定属性值的类型和必要性(引入prop-types.js)
组件名.propTypes = {
  key1:PropTypes.string.isRequired, //指定属性是字符类型且是必要的
  key2:PropTypes.number //指定属性是数值类型
}
/*
...(扩展运算符)的作用
1.打包(将多个数据打成一个包(可能是对象也可能是数组))
  例：function fn(...as){},fn(1,2,3)
2.解包(将一个数组或对象的数据逐个拿出来)
  例：const arr1 = [1,2,3] const arr2 = [6,...arr1,9]
*/

```

### 6. 组件组合使用

​	 组件化编写功能的流程

```js
/*
	1. 拆分组件
	2. 实现静态组件(只有静态页面，没有动态数据和交互)
	3. 实现动态组件
		1). 实现初始化数据动态显示
		2). 实现交互功能
*/
```

### 7. onChange事件

​     原生DOM的onChange只有在 `<input> `标签失去焦点的时候才触发，
​     而react的onChange当 `<input>` 输入时即可触发。

### 8. 生命周期流程

1.  第一次初始化渲染显示：ReactDom.render()
   constructor(): 创建对象初始化state
   componentWillMount()：将要插入容器DOM回调
   render()：用于插入虚拟DOM回调
   componentDidMount()：已经插入容器DOM回调
2. 每次更新state：this.setState()
   componentWillUpdate()：将要更新虚拟DOM回调
   render()：更新(重新渲染)
   componentDidUpdate()：已经更新虚拟DOM回调
3. 移除组件：ReactDOM.unmountComponentAtNode(containerDom)
   componentWillUnmount()：组件将要被移除回调

PS：setInterval()的回调函数是window，所以this指的是window

### 9. [fetch文档](https://github.github.io/fetch/)和[axios文档](https://github.com/axios/axios)

### 10. 组件间通信

 方式一：通过props传递

1. 共同的数据放在父组件上，特有的数据放在自己组件内部(state)
2. 通过props可以传递一般数据和函数数据，只能一层一层传递
3. 一般数据 --> 父组件传递数据给子组件 --> 子组件读取数据
4. 函数数据 --> 子组件传递数据给父组件 --> 子组件调用函数

方式二：使用消息订阅(subscribe)-发布(publish)机制

1. 工具库：PubSubJs
2. 下载：npm install pubsub-js --save
3. 使用：
   import PubSub from 'pubsub-js' //引入
   PubSub.subscribe('delete',function(msg,data){}) //订阅
   PubSub.publish('delete',data) //发布消息

### 11. redux

1. redux是一个独立专门用于做状态管理的JS库(不是react插件库)
2. 可以用在vue等项目中，基本与react配合使用
3. 作用：集中式管理react应用中多个组件共享的状态

### 