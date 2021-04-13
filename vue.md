# vue

###  1. 事件修饰符

```html
<!-- 阻止单击事件继续传播 -->
<a v-on:click.stop="doThis"></a>

<!-- 提交事件不再重载页面 -->
<form v-on:submit.prevent="onSubmit"></form>

<!-- 修饰符可以串联 -->
<a v-on:click.stop.prevent="doThat"></a>

<!-- 只有修饰符 -->
<form v-on:submit.prevent></form>

<!-- 添加事件监听器时使用事件捕获模式 -->
<!-- 即内部元素触发的事件先在此处理，然后才交由内部元素进行处理 -->
<div v-on:click.capture="doThis">...</div>

<!-- 只当在 event.target 是当前元素自身时触发处理函数 -->
<!-- 即事件不是从内部元素触发的 -->
<div v-on:click.self="doThat">...</div>
```

### 2. 按键修饰符

```HTML
<!-- 只有在 `key` 是 `Enter` 时调用 `vm.submit()` -->
<input v-on:keyup.enter="submit">
<input v-on:keyup.page-down="onPageDown">
```

在上述示例中，处理函数只会在 `$event.key` 等于 `PageDown` 时被调用。

- `.enter`
- `.tab`
- `.delete` (捕获“删除”和“退格”键)
- `.esc`
- `.space`
- `.up`
- `.down`
- `.left`
- `.right`

### 3. v-model

`v-model` 在内部为不同的输入元素使用不同的属性并抛出不同的事件：

- text 和 textarea 元素使用 `value` 属性和 `input` 事件；
- checkbox 和 radio 使用 `checked` 属性和 `change` 事件；
- select 字段将 `value` 作为 prop 并将 `change` 作为事件。

修饰符
    `.lazy`

​    在默认情况下，`v-model` 在每次 `input` 事件触发后将输入框的值与数据进行同步 (除了上述输入法组合    文字时)。你可以添加 `lazy` 修饰符，从而转变为使用 `change` 事件进行同步：

```
<!-- 在“change”时而非“input”时更新 -->
<input v-model.lazy="msg" >
```

​    ` .number`

​    如果想自动将用户的输入值转为数值类型，可以给 `v-model` 添加 `number` 修饰符：

```html
<input v-model.number="age" type="number">
```

​    `.trim`

​    如果要自动过滤用户输入的首尾空白字符，可以给 `v-model` 添加 `trim` 修饰符:

```html
<input v-model.trim="msg">
```

[表单输入绑定](https://cn.vuejs.org/v2/guide/forms.html)

### 4.简写

​     v-bind -> :
​     v-on -> @

### 5. 计算属性

计算属性是基于它们的响应式依赖进行缓存的。只在相关响应式依赖发生改变时它们才会重新求值。

### 6. 侦听器watch

虽然计算属性在大多数情况下更合适，但有时也需要一个自定义的侦听器。这就是为什么 Vue 通过 `watch` 选项提供了一个更通用的方法，来响应数据的变化。当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。

watch用来监听数据的变化

用法：

```js
/*简单数据类型*/
dataname:function(newV,oldV){
  
}
/*复杂数据类型object,Array*/
dataname:{
  deep:'true',
  handler:function(newV,oldV){
    
  }
}
```

### 7. 组件通信

1. 父传子：
   
   通过props来进行通信
   
   1. 在父组件绑定子组件自定义的属性
   2. 在子组件中声明props接收在父组件挂载的属性
   3. 可以在子组件的template中任意使用
   
   ```js
   Vue.component('blog-post', {
     props: ['title'],
     template: '<h3>{{ title }}</h3>'
   })
   ```
   
   ```html
   <blog-post title="My journey with Vue"></blog-post>
   <blog-post title="Blogging with Vue"></blog-post>
   <blog-post title="Why Vue is so fun"></blog-post>
   ```
   
   通过this.$parent
   
   ```js
   Vue.component('son', {
   	data() {
   		return {
   			title: this.$parent.title
   		}
   	}
   })
   ```
   
   ```js
   Vue.component('parent', {
   	data() {
   		return {
   			title: 'parent'
   		}
   	},
   	template: `<div><son></son></div>`
   })
   ```
   
2. 子传父：
   1. 在父组件的子组件上绑定自定义事件
   2. 在子组件触发原生事件的回调函数中通过this.$emit(父组件自定义的事件名，在子组件抛出的值)触发在父组件自定事件

   ```vue
   <button v-on:click="$emit('enlarge-text', 0.1)">
     Enlarge text
   </button>
   ```

   ```vue
   <blog-post
     ...
     v-on:enlarge-text="postFontSize += $event"
   ></blog-post>
   ```

### 8. 平行组件通信

```typescript
const bus = new Vue();  //创建中央事件总线bus
Vue.component('B'{
	data(){
  	return {
      count:0
    }
	},
  template:`<div>{{count}}</div>`,
  created(){  //生命周期的created方法
    //绑定事件add，并且设置回调函数
    bus.$on('add',(n)=>{
      this.count+=n;
    })
  }
})

Vue.component('A'{
	data(){
  	return {
      
    }
	},
  template:`
		<div>
			<Button @click='handleClick'>加入购物车</Button>
		</div>`,
  methods:{
    //触发add事件
    handleClick(){
      bus.$emit('add',1);
    }
  }
})

```

### 9. 组件通信其他方式(provide和inject)

父组件 provide来提供变量，子组件中通过inject来注入变量，无论组件嵌套多深。

```typescript
//父组件
const App = {
  provide(){
    return {
      msg:'father message'
    }
  }
}
//子组件
vue.component('B',{
  inject:['msg']  //可用插值表达式使用：{{msg}}
})

/*
ps: this.$parent 可取到对应的父组件，this.$children  可取到对应的子组件
*/
```

### 10. 异步组件加载

```typescript
//在其需要的时候这个组件才会被加载出来，不需要的时候不会出现Test.Vue(js)
components: {
  Test:()=>import(./Test)
}
```

### 11. refs的使用

ref属性只有是在确定要操作DOM或者子组件的时候才设置

```typescript
//1. 如果给标签添加ref，获取的就是真实的DOM节点 (this.$refs.btn)
//2. 如果给子组件添加ref，获取的是当前子组件对象 (this.$refs.test)
{
  ...
  template:`
		<div>
			<Test ref='test'></Test>
			<button ref='btn'></button>
		</div>
	`
}
```

### 12. nextTick的应用

nextTick(()=>{}) 取到DOM更新之后的状态

```typescript
const vm = new Vue({
  el: '#example',
  data: {
    message: '123'
  }
})
vm.message = 'new message' // 更改数据
vm.$el.textContent === 'new message' // false
//组件内部的写法为：this.$nextTick
Vue.nextTick(()=> {
  vm.$el.textContent === 'new message' // true
})
```

### 13. 数据对象增加或删除的注意

```typescript
//对象的增加  不能直接this.user.name='jack'进行添加
{
	data:{
    user:{}
  },
  methods: {
    add():{
      //this.$set(this.user,'name','jack');
      this.user = Object.assign({},this.user,{  //此函数返回的也是对象数据，给对象添加多个属性
        name:'jack'
      })
    }
  }
}

```

### 14. vue脚手架

> 通过 `npm add vue `  可以添加一个vue项目的环境（node_modules和package-lock.json）
>
> 通过 `vue serve` 可以进行快速原型开发，自动启动App.vue文件
>
> 通过 `vue create 项目名` 指令生成vue-cli脚手架项目

##### Mock数据

创建vue.config.js文件，并在文件中写入：

```typescript
module.exports = {
  devServer: {
    before(app,serve){
      app.get('前端请求的url',(req,res) =>{
        res.json({
          result: 返回的数据;
        })
      })
    }
  }
}
```

下载 cnpm -i axios -S

重启服务 npm run serve

### 15. element-ui

#### 按需引入

> 在vue-cli中可以使用 vue add element 安装
>
> 安装之前注意提前提交当前内容到GitHub，因为脚手架会覆盖若干文件(App.vue文件会发生变化，按 ctrl+z撤回)

```bash
vue add element
```

接下来，如果你只希望引入部分组件，比如 Button 和 Select，那么需要在 element.js 中写入以下内容：

```typescript
import Vue from 'vue';
import { Button, Select } from 'element-ui';

 Vue.use(Button)
 Vue.use(Select)
 
```

### 16.  后台管理系统

vue-element-admin

### 17. vue-router

##### 安装：

`vue add router` 

##### 使用：

router.js

```typescript
import Vue from 'vue'
//1. 导入
import Router from '/vue-router'
import Home from './views/Home.vue'
import About from './views/About.vue'
//2. 模块化机制 使用Router
Vue.use(Router)
```

<!--上述操作是在生成vue项目的时候没有选中Vue Router-->

##### 监听路由复用的变化：

```typescript
watch:{
	$route:(new,old)=>{
		//路由组件复用的时候，$route对象的引用发生了变化，也就是给$route对象本身赋值，所以不用deep监听
	}
}
//或者
beforeRouteUpdate(new,old,next){
  
  next();//用此方法必须调用next，否则会阻塞路由复用
}
```

##### 导航守卫

当点击切换路由时：beforeRouterLeave-->beforeEach-->beforeEnter-->beforeRouteEnter-->beforeResolve-->afterEach-->beforeCreate-->created-->beforeMount-->mounted-->beforeRouteEnter的next的回调

当路由更新时：beforeRouteUpdate

**全局守卫：**beforeEach, beforeResolve, afterEach

**单个路由独享守卫：**beforeEnter

**组件内守卫：**beforeRouteEnter, beforeRouteUpdate, beforeRouteLeave

**完整的导航解析流程：**

1. 导航被触发。
2. 在失活的组件里调用离开守卫。
3. 调用全局的 `beforeEach` 守卫。
4. 在重用的组件里调用 `beforeRouteUpdate` 守卫 (2.2+)。
5. 在路由配置里调用 `beforeEnter`。
6. 解析异步路由组件。
7. 在被激活的组件里调用 `beforeRouteEnter`。(在组件内部不能访问this，因为该组件还没有被创建，只能通过next(this)来访问组件实例)
8. 调用全局的 `beforeResolve` 守卫 (2.5+)。
9. 导航被确认。
10. 调用全局的 `afterEach` 钩子。
11. 触发 DOM 更新。
12. 用创建好的实例调用 `beforeRouteEnter` 守卫中传给 `next` 的回调函数。

##### 权限认证

在定义路由的时候可以配置 `meta` 字段

```typescript
{
  //加入黑名单，需要权限控制
  meta:{
		requiresAuth: true
	}
}
//在main.js中
router.beforeEach((to,from,next)=>{
  //some() 方法用于检测数组中的元素是否满足指定条件,返回值为bool型
  if(to.matched.some(record=>record.meta.requiresAuth)){
    //用户未登录 需要跳转登录页面
    next({
      path:'/login',
      query:{
        redirect:to.fullPath
      }
    });

  }else{
    next();
  }
})
```

**模拟数据**（新建vue.config.js文件）

```typescript
module.exports = {
    devServer:{
        before:(app,serve)=>{
            app.get('/api/get',(req,res)=>{
                res.json({
                    title:'vue-router的数据获取',
                    body:'1.在导航完成之后获取数据'
                })
            })
        }
    }
}
```

下载axios: `cnpm i axios -S`

设置请求公共的url
axios.defaults.baseURL = 'http://localhost:3000'

### 18. Vuex原理

**解答问题：vuex的store是如何注入到组件中的？**

首先使用vuex,需要安装插件：

```
Vue.use(Vuex); // vue的插件机制,安装vuex插件
```

当use(Vuex)时候，会调用vuex中的install方法，装在vuex!
下面时install的核心源码：

```js
Vue.mixin({
        beforeCreate() {
            if (this.$options && this.$options.store) {
                //找到根组件 main 上面挂一个$store
                this.$store = this.$options.store
                // console.log(this.$store);

            } else {
                //非根组件指向其父组件的$store
                this.$store = this.$parent && this.$parent.$store
            }
        }
    })

```

可见，store注入 vue的实例组件的方式，是通过vue的 全局mixin机制，借助vue组件的生命周期 钩子 beforeCreate 完成的。即 每个vue组件实例化过程中，会在 beforeCreate 钩子前调用 vuexInit 方法。

**解答问题：vuex的state和getters是如何映射到各个组件实例中响应式更新状态呢？**

```
        this._s = new Vue({ 
            data: {
                // 只有data中的数据才是响应式
                state: options.state
            }
        })

```

```javascript
 //实现getters原理
        let getters = options.getters || {}
        // console.log(getters);
        // this.getters = getters; //不是直接挂载到 getters上 这样只会拿到整个 函数体
        this.getters = {};
        // console.log(Object.keys(getters))  // ["myAge","myName"]
        Object.keys(getters).forEach((getterName) => {
            // console.log(getterName)  // myAge
            // 将getterName 放到this.getters = {}中
            // console.log(this.state);
            Object.defineProperty(this.getters, getterName, {
                // 当你要获取getterName（myAge）会自动调用get方法
                // 箭头函数中没有this               
                get: () => {
                    return getters[getterName](this.state)
                }
            })
        })
```

**从上面源码，我们可以看出Vuex的state状态是响应式，是借助vue的data是响应式，将state存入vue实例组件的data中；Vuex的getters则是借助vue的计算属性computed实现数据实时监听。**

**mutations实现**

```js
let mutations = options.mutations || {}
// console.log(mutations);
this.mutations = {};
Object.keys(mutations).forEach(mutationName=>{
  // console.log(mutationName);

  this.mutations[mutationName] = (payload) =>{
    this.mutations[mutationName](this.state,payload)
  }
})
```

**actions实现**

```js
// actions的原理 
let actions = options.actions || {}
this.actions = {};
forEach(actions,(actionName,value)=>{
  this.actions[actionName] = (payload)=>{
    value(this,payload)
  }
})
```

**commit dispatch的实现**

```js
commit(type,payload){
    this.mutations[type](payload)
}
```
```js
// type是actions的类型  
dispatch=(type,payload)=>{
    this.actions[type](payload)
}
```
### 19. Vue-router原理

```js
let Vue;
class KVueRouter {
    constructor(options){
        this.$options=options;
        this.$routerMap={};//{"/":{component:...}}
        // url 响应式，当值变化时引用的地方都会刷新
        this.app = new Vue({
            data:{
                current:"/"
            }
        });
    }
    // 初始化
    init(){
        // 监听事件
        this.bindEvent();
        // 解析路由
        this.createRouteMap();
        // 声明组件
        this.initComponent();
    }
    bindEvent(){
        window.addEventListener('hashchange',this.onHashchange.bind(this));
    }
    onHashchange(){
        this.app.current = window.location.hash.slice(1) || "/";
    }
    createRouteMap(){
        this.$options.routes.forEach(route=>{
            this.$routerMap[route.path]=route;
        })
    }
    initComponent(){
        Vue.component('router-link',{
            props:{
                to:String,
            },
            render(h){
                return h('a',{attrs:{href:'#'+this.to}},[this.$slots.default])
            }
        });
        Vue.component('router-view',{
            render:(h)=>{
            //这里使用了data中的 this.app.current，根据vue相应式原理，当变this.app.current时
            //这里会监听并发生变化
                const Component = this.$routerMap[this.app.current].component;
                return h(Component)
            }
        });
    }
}
// 参数是vue构造函数，Vue.use(router)时,执行router的install方法并把Vue作为参数传入
KVueRouter.install = function(_vue){
    Vue = _vue;
    //全局混入
    Vue.mixin({
        beforeCreate(){//拿到router的示例，挂载到vue的原型上
            if (this.$options.router) {
                Vue.prototype.$router=this.$options.router;
                this.$options.router.init();
            }
        }
    })
}
export default KVueRouter;
```

### 20. nextTick的原理

```js
if (typeof Promise !== 'undefined' && isNative(Promise)) {
  const p = Promise.resolve()
  timerFunc = () => {
    p.then(flushCallbacks)
    if (isIOS) setTimeout(noop)
  }
  isUsingMicroTask = true
} else if (!isIE && typeof MutationObserver !== 'undefined' && (
  isNative(MutationObserver) ||
  MutationObserver.toString() === '[object MutationObserverConstructor]'
)) {
  let counter = 1
  const observer = new MutationObserver(flushCallbacks)
  const textNode = document.createTextNode(String(counter))
  observer.observe(textNode, {
    characterData: true
  })
  timerFunc = () => {
    counter = (counter + 1) % 2
    textNode.data = String(counter)
  }
  isUsingMicroTask = true
} else if (typeof setImmediate !== 'undefined' && isNative(setImmediate)) {
  timerFunc = () => {
    setImmediate(flushCallbacks)
  }
} else {
  timerFunc = () => {
    setTimeout(flushCallbacks, 0)
  }
}
```

步骤：

先判断Promise

在判断MutationObserver

在判断setImmediate

最后setTimeout

整体流程涉及到事件的循环（Event Loop）[暂不在这说]

每次event loop的最后，会有一个UI render，也就是更新DOM

只要让nextTick里的代码放在UI render步骤后面执行，就能访问到更新后的DOM了。

又涉及到微任务(microtask)和宏任务(macrotask)

microtask有：Promise、MutationObserver，以及nodejs中的process.nextTick

macrotask有：setTimeout, setInterval, setImmediate, I/O, UI rendering

每一次事件循环都包含一个microtask队列，在循环结束后会依次执行队列中的microtask并移除，然后再开始下一次事件循环。

vue的nextTick方法的实现原理：

vue用异步队列的方式来控制DOM更新和nextTick回调先后执行

microtask因为其高优先级特性，能确保队列中的微任务在一次事件循环前被执行完毕

因为浏览器和移动端兼容问题，vue不得不做了microtask向macrotask的兼容(降级)方案

### 21. 双向数据绑定实现原理

```html
<input id="input" type="text">
<span id="span"></span>
<script>
    //双向数据绑定
    let obj = {};
    let input = document.getElementById('input');
    let span = document.getElementById('span');

    //数据劫持
    Object.defineProperty(obj, 'text', {
        get() {
            console.log('获取数据');
        },
        set(newVal) {
            console.log('数据更新');
            input.value = newVal;
            span.textContent = newVal;
        }
    })

    //监听
    input.addEventListener('keyup', function (e) {
        obj.text = e.target.value;
    })
</script>
```

### 22. 生命周期

```js
beforeCreate() {
  console.log('组件创建之前'， this.$data) //拿不到组件的任何数据
}
created() {
  console.log('组件创建完成'， this.$data) //数据已初始化完毕，事件都已经声明了
}
beforeMount() {
  console.log('DOM挂载到渲染树之前');
}
mounted() {
  console.log('DOM已经挂载到渲染树');
}
beforeUpdated() {
  console.log('数据修改，DOM更新之前') // data修改时，DOM还没更新
}
updated() {
  console.log('DOM更新完毕') // DOM更新完毕
}
beforeDestroy() {
  console.log('组件销毁之前')
}
destroyed() {
  console.log('组件销毁完毕')
}
```

### 23. MVC、MVP与MVVM

#### MVC

三个单词的首字母缩写，它们是Model（模型）、View（视图）和Controller（控制）。

这个模式认为，程序不论简单或复杂，从结构上看，都可以分成三层。

- 最上面的一层，是直接面向最终用户的"视图层"（View）。它是提供给用户的操作界面，是程序的外壳。


- 最底下的一层，是核心的"数据层"（Model），也就是程序需要操作的数据或信息。


- 中间的一层，就是"控制层"（Controller），它负责根据用户从"视图层"输入的指令，选取"数据层"中的数据，然后对其进行相应的操作，产生最终结果。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015020105.png)

所有通信都是单向的。

1. View传指令到Controller，View层也有可能会有业务逻辑，可以直接操作Model。
2. Controller完成业务逻辑后，要求Model改变状态。
3. Model将新的数据发送到View，用户得到反馈。

#### MVP

MVP 模式将 Controller 改名为 Presenter，同时改变了通信方向。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015020109.png)

1. 各部分之间的通信，都是双向的。

2. View 与 Model 不发生联系（视图与模型完全分离），都通过 Presenter 传递。

3. View 非常薄，不部署任何业务逻辑，称为"被动视图"（Passive View），即没有任何主动性，而 Presenter非常厚，所有逻辑都部署在那里。

#### MVP与MVC的区别

1. 在MVP中View并不直接使用Model，它们之间的通信是通过Presenter (MVC中的Controller)来进行的，所有的交互都发生在Presenter内部，而在MVC中View会直接从Model中读取数据而不是通过 Controller。
2. 在MVC里，View是可以直接访问Model的。从而，View里会包含Model信息，不可避免的还要包括一些业务逻辑。 
3. 在MVC模型里，Model不依赖于View，但是View是依赖于Model的。
4. MVC 中的 View 的确可以访问 Model，但是我们不建议在 View 中依赖 Model，而是要求尽可能把所有业务逻辑都放在 Controller 中处理，而 View 只和 Controller 交互。

#### MMVM

MVVM 模式将 Presenter 改名为 ViewModel，基本上与 MVP 模式完全一致。

![img](http://www.ruanyifeng.com/blogimg/asset/2015/bg2015020110.png)

### MVVM与MVP区别：

它采用双向绑定(data-binding): View的 变动，自动反映在View Model，反之亦然。这样开发者就不用处理接收事件和View更新的工作，框架已经帮你做好了。

### 24. diff算法

#### 虚拟DOM

用JS模拟DOM结构

```
{
	tag: '',
	props: {},
	children: []
}
```

- 用 JavaScript 对象结构表示 DOM 树的结构，然后用这个树构建一个真正的 DOM 树，插到文档当中；
- 当状态变更的时候，重新构造一棵新的对象树，然后用新的树和旧的树进行比较，记录两棵树差异；
- 把记录的差异应用到步骤 1 所构建的真正的 DOM 树上，视图就更新了。

Virtual DOM 本质上就是在 JS 和 DOM 之间做了一个缓存。可以类比 CPU 和硬盘，既然硬盘这么慢，我们就在它们之间加个缓存：既然 DOM 这么慢，我们就在它们 JS 和 DOM 之间加个缓存。CPU（JS）只操作内存（Virtual DOM），最后的时候再把变更写入硬盘（DOM）。

#### **比较两棵虚拟 DOM 树的差异**

两个树的完全的 diff 算法是一个时间复杂度为 O(n^3) 的问题。但是在前端当中，你很少会跨越层级地移动 DOM 元素。

所以 Virtual DOM 只会对同一个层级的元素进行对比：

1. 两个相同的组件产生类似的DOM结构，不同的组件产生不同的DOM结构。

2. 同一层级的一组节点，他们可以通过唯一的id进行区分。

![preview](https://segmentfault.com/img/bVbgaug?w=912&h=471/view)

上面的 div 只会和同一层级的 div 对比，第二层级的只会跟第二层级对比。这样算法复杂度就可以达到 O(n)。

深度优先遍历，记录差异

在实际的代码中，会对新旧两棵树进行一个深度优先的遍历，这样每个节点都会有一个唯一的标记（key绑定的作用）：

![clipboard.png](https://segmentfault.com/img/bVbgaun?w=1018&h=513)

在深度优先遍历的时候，每遍历到一个节点就把该节点和新的的树进行对比。如果有差异的话就记录到一个对象里面。

Virtual DOM 算法主要是实现上面步骤的三个函数：element，diff，patch。然后就可以实际的进行使用：

```js
// 1. 构建虚拟 DOM
var tree = el('div', {'id': 'container'}, [
    el('h1', {style: 'color: blue'}, ['simple virtal dom']),
    el('p', ['Hello, virtual-dom']),
    el('ul', [el('li')])
])
// 2. 通过虚拟 DOM 构建真正的 DOM
var root = tree.render()
document.body.appendChild(root)
// 3. 生成新的虚拟 DOM
var newTree = el('div', {'id': 'container'}, [
    el('h1', {style: 'color: red'}, ['simple virtal dom']),
    el('p', ['Hello, virtual-dom']),
    el('ul', [el('li'), el('li')])
])
// 4. 比较两棵虚拟 DOM 树的不同
var patches = diff(tree, newTree)
// 5. 在真正的 DOM 元素上应用变更
patch(root, patches)
```

注意：diff算法是一边比较新旧vdom，一边改变真实dom节点

### 25. key的作用

- 在列表渲染时使用key属性

  key的作用主要是为了高效的更新虚拟DOM。

  ![img](https://upload-images.jianshu.io/upload_images/13201627-c3e12cdb02d59c24.png?imageMogr2/auto-orient/strip|imageView2/2/w/477/format/webp)

  我们希望可以在B和C之间加一个F，Diff算法默认执行起来是这样的：

  ![img](https://upload-images.jianshu.io/upload_images/13201627-9d6226c6268a341b.png?imageMogr2/auto-orient/strip|imageView2/2/w/572/format/webp)

  即把C更新成F，D更新成C，E更新成D，最后再插入E，没有效率

  所以我们需要使用key来给每个节点做一个唯一标识，Diff算法就可以正确的识别此节点，找到正确的位置区插入新的节点。

  ![img](https://upload-images.jianshu.io/upload_images/13201627-d0b3a1577860fda9.png?imageMogr2/auto-orient/strip|imageView2/2/w/452/format/webp)

  

- 使用key属性强制替换元素

  强制替换元素，从而可以触发组件的生命周期钩子或者触发过渡。因为当`key`改变时，Vue认为一个新的元素产生了，从而会新插入一个元素来替换掉原有的元素。

  ```vue
  <transition>
    <span :key="text">{{text}}</span>
  </transition>
  ```

  这里如果`text`发生改变，整个`<span>`元素会发生更新，因为当`text`改变时，这个元素的`key`属性就发生了改变，在渲染更新时，Vue会认为这里新产生了一个元素，而老的元素由于`key`不存在了，所以会被删除，从而触发了过渡。

  假如没有key属性：

  ```vue
  <transition>
    <span>{{text}}</span>
  </transition>
  ```

  那么当text改变时，Vue会复用元素，只改变<span>元素的内容，而不会有新的元素被添加进来，也不会有旧的元素被删除。

  同理，key属性被用在组件上时，当key改变时会引起新组件的创建和原有组件的删除，此时组件的生命周期钩子就会被触发。