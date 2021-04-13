### 1. 数据类型

​	   **基本类型**：String、Number、Boolean、null、Undefined、Symbol、BigInt
​	   **引用数据类型**：Object、Array、Function
​	   **typeof返回的数据类型**：String、Number、Boolean、Symbol、undefined、bigint、object、function

### 2. 基本类型与对象类型的区别

原始类型存储的是值，对象类型存储的是地址。

### 3. typeof和instanceof的区别

typeof：对于基本类型数据来说，除了null，typeof都会显示正确的类型；对于对象来说，除了函数，typeof都会显示Object。

instanceof：用来判断对象，代码形式为obj1 instanceof obj2（obj1是否是obj2的实例），判断方法是根据对象的原型链依次向下查询，如果obj2的原型属性存在obj1的原型链上，（obj1 instanceof obj2）值为true。

### 4. 如何判断一个对象类型是数组

- 根据构造函数来判断 xxx instanceof Array
- 根据class属性判断 Object.prototype.toString.call(obj)==='[object Array]'
- 直接用isArray判断

### 5. 类型转换

在 JS 中类型转换只有三种情况，分别是：

- 转换为布尔值
- 转换为数字
- 转换为字符串

### 6. 转Boolean

在条件判断时，除了 `undefined`， `null`， `false`， `NaN`， `''`， `0`， `-0`，其他所有值都转为 `true`，包括所有对象。

### 7. toString() 和 valueOf()

valueOf()：返回变量本身的值

toString：将变量转换为String类型，数组调用toString()方法实际上是调用了join(',')，对象调用toString()方法返回[object Object]

### 8. 运算符的隐式转换

（1）运算符在运算的时候，如果两边的数据类型不一致，则会自动转成一致后运算。
		  a. 其他类型转string :  + 连接符
		  b. 其他类型转number : 
			  自增自减(++ --)
			  算术运算符( + - * / %)
			  关系运算符 :  > >= < <= == != `===` `!==`
		  c. 其他类型转boolean :  ! 逻辑非

（2）特殊情况
​		  === ： 全等运算符。 不存在类型转换， 先比较类型，然后比较值
​		  ==  :  比较运算符。 隐式转换规则是转成number，但是有前提条件

（3）x == y： 比较运算符分为五种情况
		  a. x和y 都为 null或undefined
			  *  不会类型转换，得到固定值true
	      b. x或y 为NaN 
			  *  不会类型转换，得到固定值false  (NaN与任何数据都不等，包含自身)
		  c. x和y 都为 string，boolean，number且类型不一致
			  *  会类型转换， 会把其他类型转成number后计算	
		    d. x或y 为引用类型 （一个是引用类型，一个是值类型）
			  *  前提 ： 引用类型会先调用valueOf(),然后调用toString(),再来计算  （最终变成字符串来比较）
			  *  valueOf() : 一般引用类型，返回自身（一般忽略）
			  *  toString() : 数组是join()字符串， 对象是固定字符串 '[object Object]'
		      e. x和y 都为引用类型。 则会比较两者地址，地址一样则为true，否则为false 

```typescript
1. null 和 undefined 在和数字、字符串、Boolean比较时
   1.1. 如果遇到 == 不会进行在转化,没有可比性(false)
   console.log(null == 0); // false
   console.log(null == 1); // false
   console.log(null == -1);// false
   1.2 如果遇到 > >= < <= 会隐式的转化为数字(null转化为 0 ,undefined 转化为 NaN),可以进行比较
	 console.log(null >= 0); // true
   console.log(null <= 0); // true
   console.log(null > -5); // true
   因为undefined转化为NaN 所以undefined的判断都是false
   console.log(undefined == 0); // false
   console.log(undefined >= 0); // false
   console.log(undefined <= 0); // false
```

### 9. 代码回收规则

​		  1、全局变量不会被回收。
​		  2、局部变量会被回收，也就是函数一旦运行完以后，函数内部的东西都会被销毁。
​		  3、只要被另外一个作用域所引用就不会被回收

### 10. js中字符串高效的连接方式

​		 1、在旧浏览器（**ie7-**）下用 join 会更高效。
​		 2、在现代浏览器，尽量用"+",更高效。
​		 3、当然，在少数现代浏览器里 “+” 不一定会比 join 快（如，**safari 5.0.5，opera 11.10**)
​		 4、本身是字符串数组的，直接 join 会更好。
​		 5、在"+"与concat之间，当然是优选使用"+"，方便又直观又高效。

### 11. 全局函数

简易记忆：6（编码相关）+  4（数字相关）+ 2（数据处理）+ 1（特殊）

-    编程相关
     escape()、unescape()、encodeURI()、decodeURI()、
     encodeURIComponent()、decodeURIComponent()
-    数字相关
     isFinite()、isNaN()、parseFloat()、parseInt()
-    数据处理
     Number()、String()
-    特殊
     eval()

### 12. 属性描述对象

```js
{
  value: 123,
  writable: false,
  enumerable: true,
  configurable: false,
  get: undefined,
  set: undefined
}
```

#### 数据描述符

- Configurable 表示能否通过delete删除属性或者重新定义属性，默认为true
- Enumerable 表示该属性是否可遍历（是否有枚举属性），默认为true
- Writable 表示能否修改属性的值，默认为true
- Value 包含这个属性的数据值，默认为undefined

```js
//使用字面量创建对象，前三个属性默认值为true，value为指定的值
var person={
    name:'xxxx'
}
```

#### 访问器描述符

- getter 函数：当访问该属性时，会调用此函数。执行时不传入任何参数，但是会传入 `this` 对象（由于继承关系，这里的`this`并不一定是定义该属性的对象）。该函数的返回值会被用作属性的值。默认为undefined。
- setter 函数：当属性值被修改时，会调用此函数。该方法接受一个参数（也就是被赋予的新值），会传入赋值时的 `this` 对象。默认为undefined。

### 13. 继承

#### 原型链继承

 JavaScript使用原型链作为实现继承的主要方法，实现的本质是重写原型对象，代之以一个新类型的实例。下面代码中，原来存在于`SuperType`的实例对象的属性和方法，现在也存在于`SubType.prototype`中了

```js
function Super(){
    this.value = true;
}
Super.prototype.getValue = function(){
    return this.value
}
function Sub(){};
//Sub继承了Super
Sub.prototype = new Super();
Sub.prototype.constroctor = Sub;
var ins = new Sub();
console.log(ins.getValue());//true
```

我们没有使用`Sub`默认提供的原型，而是给它换了一个新原型；这个新原型就是`Super`的实例。于是，新原型不仅具有作为一个`Super`的实例所拥有的属性和方法，而且它还指向了`Super`的原型。最终结果就是这样的：

```
ins=>Sub的原型=>Super的原型
```

`getValue()`方法仍然还在`Sub.prototype`中，但`value`属性则位于`Sub.prototype`中。这是因为`value`是一个实例属性，而`getValue()`则是一个原型方法。既然`Sub.prototype`现在是`Super`的实例，那么`value`位于该实例中。

**缺点：**

1. 私有原型属性会被实例共享

   ```js
   function Super() {
   	this.colors = ['red', 'green', 'blue'];
   }
   Super.prototype.getValue = function () {
   	return this.colors
   }
   function Sub() { };
   //Sub继承了Super
   Sub.prototype = new Super();
   var ins1 = new Sub();
   ins1.colors.push('black');
   console.log(ins1.colors);//['red','green','blue','black'];
   var ins2 = new Sub();
   console.log(ins2.colors);//['red','green','blue','black'];
   ```

2. 在创建子类型的实例时，不能向父类型的构造函数传递参数

#### 借用构造函数继承

即**在子类构造函数的内部用apply()或call()方法调用父类构造函数**。

```js
function Super() {
    this.colors = ['red', 'green', 'blue'];
}
Super.prototype.getValue = function(){
    return this.colors;
}
function Sub(){
    //继承了Super
    Super.call(this);//相当于把构造函数Super中的this替换成了ins实例对象，这样在Super只有定义的私有属性会被继承下来，原型属性中定义的公共方法不会被继承下来
}
var ins = new Sub();
console.log(ins.colors);
```

相对于原型链来说，借用构造函数继承有一个很大的优势，即可以在子类构造函数中向父类构造函数传递参数

```js
function B(name){
    this.name = name;
}
function A(){
    //继承了B，同时还传递了参数
    B.call(this,'MJJ');
    //实例属性
    this.age = 28;
}
var p = new A();
alert(p.name);//'MJJ'
alert(p.age);//28
```

**缺点：**

如果仅仅是借用构造函数，那么将无法避免构造函数模式存在的问题——方法都在构造函数中定义，因此函数复用就无从谈起。而且，在父类的原型中定义的方法，对子类而言是不可见的。

#### 组合继承(重要)

是使用原型链实现对原型上的公共属性和方法的继承，而通过借用构造函数继承来实现对父类私有属性的继承。这样，即通过在父类原型上定义方法实现了函数复用，又能够保证每个实例都有父类的私有属性。

```js
function Super(name){
    this.name = name;
    this.colors = ['red','blue','green'];
}
Super.prototype.sayName = function(){
    console.log(this.name);
}
function Sub(name,age){
    Super.call(this,name);
    this.age = age;
}
// 继承方法
Sub.prototype = new Super();
Sub.prototype.constructor = Sub;
Sub.prototype.sayAge = function(){
    console.log(this.age);
}
var ins = new Sub('mjj',28);
ins.colors.push('black');
console.log(ins.colors);// ["red", "blue", "green", "black"]
ins.sayName();//'mjj'
ins.sayAge();//28

var ins2 = new Sub('alex',38);
console.log(ins2.colors);//["red", "blue", "green"]
ins2.sayName();//'alex'
ins2.sayAge();//38
```

`Sub`构造函数定义了两个属性：`name`和`age`。`Super`的原型定义了一个`sayName()`方法。在`Sub`构造函数中调用`Super`构造函数时传入了name参数，紧接着又定义它自己的属性age。然后，将`Super`的实例赋值给`Sub`的原型，然后又在该新原型上定义了方法`sayAge()`。

**缺点：**

无论在什么情况下，都会调用两次父类的构造函数：一次是在创建子类原型的时候，另一次是在子类构造函数内部。

#### 寄生组合式继承

通过借用构造函数来继承属性，通过原型链的混成形式来继承方法。不必为了指定子类型的原型而调用超类型的构造函数，我们所需要的无非就是超类型 原型的一个副本而已。

```js
function Super(name){
    this.name = name;
    this.colors = ['red','blue','green'];
}
Super.prototype.sayName = function(){
    console.log(this.name);
}
function Sub(name,age){
    //继承实例属性
    Super.call(this,name);
    this.age = age;
}
// 继承公有的方法
Sub.prototype = Object.create(Super.prototype);
Sub.prototype.constructor = Sub;
Sub.prototype.sayAge = function(){
    alert(this.age);
}
var ins = new Sub('mjj',28);
ins.colors.push('black');
console.log(ins.colors);// ["red", "blue", "green", "black"]
ins.sayName();//'mjj'
ins.sayAge();//28
var ins2 = new Sub('alex',38);
console.log(ins2.colors);//["red", "blue", "green"]
ins2.sayName();//'alex'
ins2.sayAge();//38
```

#### class继承

```js
class Parent {
  constructor(value) {
    this.val = value
  }
  getValue() {
    console.log(this.val)
  }
}
class Child extends Parent {
  constructor(value) {
    super(value)
  }
}
let child = new Child(1)
child.getValue() // 1
child instanceof Parent // true
```

`class` 实现继承的核心在于使用 `extends` 表明继承自哪个父类，并且在子类构造函数中必须调用 `super`，因为这段代码可以看成 `Parent.call(this, value)`。

### 14. DOM创建元素

- 创建

  createElement('button') 创建元素结点

  createTextNode('CLICK ME') 创建文本结点

- 添加

  appendChild(element)

  insertBefore(insertdom, chosendom)

### 15. DOM获取元素的方式

#### 通过元素类型获取

1. document.getElementById(); //id名，在实际开发中较少使用，选择器中多用class id一般只用在顶级层存在 不能太过依赖id
2. document.getElementsByTagName(); //标签名
3. document.getElementsByClassName(); //类名
4. document.getElementsByName(); //name属性值，一般不用
5. document.querySelector(); //css选择符模式，返回与该模式匹配的第一个元素，结果为一个元素；如果没找到匹配的元素，则返回null
6. document.querySelectorAll(); //css选择符模式，返回与该模式匹配的所有元素，结果为一个类数组

#### 根据关系树来选择

1. parentNode//获取所选节点的父节点，最顶层的节点为#document
2. childNodes //获取所选节点的子节点们
3. firstChild //获取所选节点的第一个子节点
4. lastChild //获取所选节点的最后一个子节点
5. nextSibling //获取所选节点的后一个兄弟节点 列表中最后一个节点的nextSibling属性值为null
6. previousSibling //获取所选节点的前一兄弟节点 列表中第一个节点的previousSibling属性值为null

#### 根据元素节点树来选择

1. parentElement　//返回当前元素的父元素节点（IE9以下不兼容）
2. children // 返回当前元素的元素子节点
3. firstElementChild //返回的是第一个元素子节点（IE9以下不兼容）
4. lastElementChild //返回的是最后一个元素子节点（IE9以下不兼容）
5. nextElementSibling //返回的是后一个兄弟元素节点（IE9以下不兼容）
6. previousElementSibling //返回的是前一个兄弟元素节点（IE9以下不兼容）

### 16. 给元素添加事件

- 在HTML元素中绑定事件 onclick=show()
- 获取dom，dom.onclick
- addEventListener(click,show,1/0)

### 17. addEventListener三个参数

第一个参数是事件类型，第二个是事件发生的回调函数，第三个是个布尔值，默认是false，false是冒泡阶段执行，true是捕获阶段。

### 18. 节点属性中children和childNodes

- childNodes返回的是节点的子节点集合（NodeLists),包括元素节点、文本节点还有属性节点。
- children返回的只是节点的元素节点集合（HTMLCollection)

### 19. HTMLCollection和NodeList

共同点

- 都是类数组对象，都有length属性

- 都有共同的方法：item，可以通过item(index)获取返回结果的元素

- 都是实时变动的，document上面的更改会反映到相关的对象上

  注：querySeletorAll返回的NodeList是个浅拷贝的类数组对象，在节点数目上是非实时的，不过对节点属性进行修改，还是实时反映的。

区别

- NodeList可以包含任何节点类型，HTMLCollection只包含元素节点。elementNode就是HTML中的标签。
- HTMLCollection比NodeList多一个方法：nameitem()，除了可以用id，还可以用name来获取节点信息。

### 20. 事件冒泡与事件捕获

事件是先捕获，后冒泡

捕获阶段是外部元素先触发然后触发内部元素

冒泡阶段是内部元素先触发然后触发外部元素

### 21. 阻止事件冒泡、取消默认事件、阻止事件的默认行为

- #### 阻止事件冒泡：

  W3C: 

  stopPropagation()：可以阻止冒泡，但无法阻止同一事件的其他监听函数被调用

  stopImmediatePropagation()：可以阻止冒泡，也可以阻止同一事件的其他监听函数被调用

  IE: e.cancelBubble=true;

  写法 :

  window.event ? window.event.cancelBubble=true : e.stopPropagation()

- #### 取消默认行为：

  1. 在DOM0级事件处理程序中取消默认行为，使用returnValue、preventDefault()和return false都有效
  2. 在DOM2级事件处理程序中取消默认行为，使用return false无效
  3. 在IE事件处理程序中取消默认行为，使用preventDefault()无效

  W3C：preventDefault();

  IE: e.returnValue=false;

  写法 :

  window.event ? window.event.returnValue=false : e.preventDefault()

### 22. var、let、const

#### var

1. **存在提升（能在声明之前使用）**

   根本原因就是为了解决函数间互相调用的情况

```js
function test1() {
    test2()
}
function test2() {
    test1()
}
test1();
```

​		假如不存在提升这个情况，那么就实现不了上述的代码，因为不可能存在 `test1` 在 `test2` 前面然后 `test2` 		又在 `test1` 前面。

2. **函数提升优先于变量提升，函数提升会把整个函数挪到作用域顶部，变量提升只会把声明挪到作用域顶部**

3. **全局作用域下声明变量会导致变量挂载在 `window` 上**

#### let

1. **作用域是块级作用域**

2. **不存在变量声明提前 （在let之前使用，会报错 is not defined）**

3. **不可以重复定义 （var可以，不会报错，但是let 会说has already been declared)**

4. **存在暂时性死区**

   ```js
   var a = 1
   
   function test(){
     console.log(a)
     let a
   }
   test();//报错
   ```

   在一个块级作用域中，变量唯一存在，一旦声明了一个，就属于这个块级作用域，不受外部的影响

5. **全局作用域下声明变量存储在跟window同级的这个script的这个域中。**

#### const

1. **用来声明常量，不允许修改**
2. **只读属性，声明同时就要赋值**
3. **和let一样，都是块级作用域，不存在变量声明提前，不允许重复定义，存在暂时性死区，全局作用域下声明变量存储在跟window同级的这个script的这个域中。**

### 23. 事件循环机制

JavaScript是一个单线程、非阻塞、异步、解释性脚本语言

**宏任务：**script（整体代码）、setTimeout()、setInterval()、setImmediate()、postMessage、I/O、UI交互事件

**微任务：**process.nextTick()、promise的resolve和reject、MutationObserver(html5 新特性)

**运行机制**

进入整体代码（宏任务 -- 包裹的代码可以 理解为第一个宏任务），开始第一次循环，接着执行所有的微任务。然后再次从宏任务开始，找到其中一个任务队列的任务执行完毕， 再执行所有的微任务。

在事件循环中，每进行一次循环操作称为 tick，每一次 tick 的任务处理模型是比较复杂的，但关键步骤如下：

- `<script>`中的整段代码作为第一个宏任务开启第一次事件循环。
- 执行过程中如果遇到宏任务或微任务，就将它添加相应的任务队列中。
- 整体代码作为第一个宏任务执行结束，立即执行当前微任务队列中的所有微任务（依次执行）
- 第一轮事件循环结束，开始检查渲染，然后GUI线程接管渲染
- 渲染完毕后，再次从宏任务开始，进行下一次事件循环，重复执行上诉操作。

简单总结一下执行的顺序：

1. js执行从最先进入任务队列的宏任务开始，通常是整体<scirpt>代码
2. 宏任务队列事件全部执行完毕后，检查微任务队列是否有事件，有则执行，直到没有事件为止
3. 更新render（每一次事件循环，浏览器都可能会去更新渲染）
4. 重复以上步骤

**题目：**

```js
async function async1() {
    console.log('async1 start');
    await async2();
    console.log('async1 end');
}
async function async2() {
    console.log('async2');
}
console.log('script start');
setTimeout(function() {
    console.log('setTimeout');
}, 0)
async1();
new Promise(function(resolve) {
    console.log('promise1');
    resolve();
}).then(function() {
    console.log('promise2');
});
console.log('script end');
```

1. 执行整体`<script>`代码
2. 遇到setTimeout，现把 setTimeout 的代码放到宏任务队列中
3. 执行 async1()，输出 `async1 start`, 然后执行 async2(), 输出 `async2`，把 async2() 后面的代码 `console.log('async1 end')`放到微任务队列中
4. 接着往下执行，输出 `promise1`，把 .then()放到微任务队列中；注意Promise本身是同步的立即执行函数，.then是异步执行函数。
5. 接着往下执行， 输出 `script end`。同步代码（同时也是宏任务）执行完成，接下来开始执行刚才放到微任务中的代码
6. 依次执行微任务中的代码，依次输出 `async1 end`、 `promise2`, 微任务中的代码执行完成后，开始执行宏任务中的代码，输出 `setTimeout`

-------

```js
console.log('start');
setTimeout(() => {
    console.log('children2');
    Promise.resolve().then(() => {
        console.log('children3');
    })
}, 0);

new Promise(function(resolve, reject) {
    console.log('children4');
    setTimeout(function() {
        console.log('children5');
        resolve('children6')
    }, 0)
}).then((res) => {
    console.log('children7');
    setTimeout(() => {
        console.log(res);
    }, 0)
})
```

1. 执行`<script>`代码
2. 遇到setTimeout，先把 setTimeout 的代码放到宏任务队列①中
3. 接着往下执行，输出 `children4`, 遇到setTimeout，先把 setTimeout 的代码放到宏任务队列②中，此时.then并不会被放到微任务队列中，因为 resolve是放到 setTimeout中执行的
4. 代码执行完成之后，会查找微任务队列中的事件，发现并没有，于是开始执行宏任务①，即第一个 setTimeout， 输出 `children2`，此时，会把 `Promise.resolve().then`放到微任务队列中。
5. 宏任务①中的代码执行完成后，会查找微任务队列，于是输出 `children3`；然后开始执行宏任务②，即第二个 setTimeout，输出 `children5`，此时将.then放到微任务队列中。
6. 宏任务②中的代码执行完成后，会查找微任务队列，于是输出 `children7`，遇到 setTimeout，放到宏任务队列中。此时微任务执行完成，开始执行宏任务，输出 `children6`;

---

```js
const p = function() {
    return new Promise((resolve, reject) => {
        const p1 = new Promise((resolve, reject) => {
            setTimeout(() => {
                resolve(1)
            }, 0)
            resolve(2)
        })
        p1.then((res) => {
            console.log(res);
        })
        console.log(3);
        resolve(4);
    })
}

p().then((res) => {
    console.log(res);
})
console.log('end');
```

1. 执行代码，Promise本身是同步的立即执行函数，.then中的回调函数是异步执行函数。遇到setTimeout，先把其放入宏任务队列中，遇到`p1.then`会先放到微任务队列中，接着往下执行，输出 `3`
2. 遇到 `p().then` 会先放到微任务队列中，接着往下执行，输出 `end`
3. 同步代码块执行完成后，开始执行微任务队列中的任务，首先执行 `p1.then`，输出 `2`, 接着执行`p().then`, 输出 `4`
4. 微任务执行完成后，开始执行宏任务，setTimeout, `resolve(1)`，但是此时 `p1.then`已经执行完成，此时 `1`不会输出。

### 24. 链式调用

#### 实现a().b().c()

```js
function a(){
    return {
        b:function(){
            return {
                c:function(){
                    console.log('a');
                }
            }
        }
    }
}
a().b().c();
//a
```

#### 实现 o.a().b().c()

```js
var temp={
    a:function(){console.log('a');return this;},
    b:function(){console.log('b');return this;},
    c:function(){console.log('c');return this;}
}
var o=new Object();
o.__proto__=temp;
o.a().b().c();
//a b c 
```

### 25. JSON.stringify

1. 布尔值、数字、字符串的包装对象在序列化过程中会自动转换成对应的原始值。
2. `undefined`、任意的函数以及 symbol 值，在序列化过程中会被忽略（出现在非数组对象的属性值中时）或者被转换成 `null`（出现在数组中时）。函数、undefined 被单独转换时，会返回 undefined，如`JSON.stringify(function(){})` or `JSON.stringify(undefined)`。
3. 对包含循环引用的对象（对象之间相互引用，形成无限循环）执行此方法，会抛出错误。
4. 所有以 symbol 为属性键的属性都会被完全忽略掉，即便 `replacer` 参数中强制指定包含了它们。
5. Date 日期调用了 toJSON() 将其转换为了 string 字符串（同Date.toISOString()），因此会被当做字符串处理。
6. NaN 和 Infinity 格式的数值及 null 都会被当做 null。

### 26. new操作符干了什么

```js
var Func=function(){
 
};
var func=new Func ();
```

new共经过了4个阶段

1. 创建空对象

   ```js
   var obj = {};
   ```

2. 设置原型链（当调用构造函数创建一个新实例后，该实例的内部将包含一个指针（内部属性），指向构造函数的原型对象）

   ```js
   obj.__proto__= Func.prototype;
   ```

3. 让Func中的this指向obj，并执行Func的函数体。（创建新的对象之后，将构造函数的作用域赋给新对象（因此this就指向了这个新对象））

   ```js
   var result = Func.call(obj);
   ```

4. 判断Func的返回值类型

   如果是值类型，返回obj。如果是引用类型，就返回这个引用类型的对象

   ```js
   if (typeof(result) == "object"){
     func = result;
   } else {
     func = obj;
   }
   ```
   

默认情况下函数返回值为undefined，即没有显示定义返回值的话，但构造函数例外，new构造函数在没有return的情况下默认返回新创建的对象。

但是，在有显示返回值的情况下，如果返回值为基本数据类型{string，number，null，undefined，Boolean}，返回值仍然是新创建的对象。

只有在显示返回一个非基本数据类型时，函数的返回值才为指定对象。在这种情况下，this所引用的值就会被丢弃了

### 27. 事件代理

由于事件会在**冒泡阶段**向上传播到父节点，因此可以把子节点的监听函数定义在父节点上，由父节点的监听函数统一处理多个子元素的事件。这种方法叫做事件的代理(delegation)，也叫事件委托。

事件代理应用事件目标的target或者srcElement属性完成

> target或者srcElement属性返回事件的实际目标节点

需求：一个ul中有5个li，移入时变蓝，移出时恢复

```html
<body>
  <ul id="box">
  <li>1</li>
  <li>2</li>
  <li>3</li>
  <li>4</li>
  <li>5</li>
  </ul>
  <script type="text/javascript">
    // 1.常规方法实现
    /* var lis = document.getElementsByTagName('li');
    for(var i = 0; i < lis.length; i ++){
    	lis[i].onmouseover = function (){
    		this.style.backgroundColor = 'blue';
    	}
    	lis[i].onmouseout = function (){
      	this.style.backgroundColor = '';
      }
    } */
    // 2.事件代理方式实现
    ul.onmouseover = function(e) {
      e = e || event;
      var target = e.target || e.srcElement;
    	target.style.backgroundColor = 'blue';
    }
    ul.onmouseout = function(e) {
      e = e || event;
      var target = e.target || e.srcElement;
    	target.style.backgroundColor = '';
    }
  </script>
</body>
```

需求：**给未来添加的元素添加事件**

```html
<body>
	<ul id="box">
    <li>1</li>
    <li>2</li>
    <li>3</li>
    <li>4</li>
    <li>5</li>
  </ul>
  <script type="text/javascript">
  // 模拟未来的某个事件添加了对应的数据
  	var ul = document.getElementById('box');
    setTimeout(function(){
      var item = document.createElement('li');
      item.innerHTML = '6';
      ul.appendChild(item);
    },100)
  /*
  //1.原生方式添加事件 不能触发未来添加元素的事件
  	var lis = document.getElementsByTagName('li');
    for(var i = 0; i < lis.length; i ++){
      lis[i].onmouseover = function (){
      	this.style.backgroundColor = 'blue';
    	}
  		lis[i].onmouseout = function (){
  			this.style.backgroundColor = 'red';
  		}
  	}
  */
  // 2.事件代理方式实现，可以触发未来添加元素的事件
  ul.onmouseover = function(e) {
    e = e || event;
    var target = e.target || e.srcElement;
    target.style.backgroundColor = 'blue';
  }
  </script>
</body>
```

### 28. 垃圾回收机制

程序的运行需要内存。只要程序提出要求，操作系统或者运行时（runtime）就必须供给内存。对于持续运行的服务进程（daemon），必须及时释放不再用到的内存。否则，内存占用越来越高，轻则影响系统性能，重则导致进程崩溃。不再用到的内存，没有及时释放，就叫做内存泄漏（memory leak）。

1. **标记清除**

   当变量进入环境时，这个变量标记为“进入环境”；而当变量离开环境时，则将其标记为“离开环境”。

   ```js
   function test(){
       var a = 10;    //被标记"进入环境"
       var b = "hello";    //被标记"进入环境"
   }
   test();    //执行完毕后之后，a和b又被标记"离开环境"，被回收
   ```

2. **引用计数**

   语言引擎有一张"引用表"，保存了内存里面所有的资源（通常是各种值）的引用次数。如果一个值的引用次数是`0`，就表示这个值不再用到了，因此可以将这块内存释放。

   如果一个值不再需要了，引用数却不为`0`，垃圾回收机制无法释放这块内存，从而导致内存泄漏。

   ```js
   const arr = [1, 2, 3, 4];
   console.log('hello world');
   ```

   上面代码中，数组`[1, 2, 3, 4]`是一个值，会占用内存。变量`arr`是仅有的对这个值的引用，因此引用次数为`1`。尽管后面的代码没有用到`arr`，它还是会持续占用内存。

   如果增加一行代码，解除`arr`对`[1, 2, 3, 4]`引用，这块内存就可以被垃圾回收机制释放了。

   ```js
   let arr = [1, 2, 3, 4];
   console.log('hello world');
   arr = null;
   ```

   上面代码中，`arr`重置为`null`，就解除了对`[1, 2, 3, 4]`的引用，引用次数变成了`0`，内存就可以释放出来了。

   解决方案：

   [WeakSet](http://es6.ruanyifeng.com/#docs/set-map#WeakSet) 和 [WeakMap](http://es6.ruanyifeng.com/#docs/set-map#WeakMap)。它们对于值的引用都是不计入垃圾回收机制的，所以名字里面才会有一个"Weak"，表示这是弱引用。

   ```js
   const wm = new WeakMap();
   
   const element = document.getElementById('example');
   
   wm.set(element, 'some information');
   wm.get(element) // "some information"
   ```

   上述代码DOM 节点对象的引用计数是`1`，而不是`2`。这时，一旦消除对该节点的引用，它占用的内存就会被垃圾回收机制释放。Weakmap 保存的这个键值对，也会自动消失。

#### 内存泄漏

虽然JavaScript会自动垃圾收集，但是如果我们的代码写法不当，会让变量一直处于“进入环境”的状态，无法被回收。下面列一下内存泄漏常见的几种情况：

1. ##### 意外的全局变量

   ```js
   function foo(arg) {
       bar = "this is a hidden global variable";
   }
   ```

   bar没被声明,会变成一个全局变量,在页面关闭之前不会被释放。

   另一种意外的全局变量可能由 `this` 创建:

   ```js
   function foo() {
       this.variable = "potential accidental global";
   }
   // foo 调用自己，this 指向了全局对象（window）
   foo();
   ```

   在 JavaScript 文件头部加上 'use strict'，可以避免上述情况错误发生。启用严格模式解析 JavaScript ，避免意外的全局变量。

2. ##### 被遗忘的计时器或回调函数

   定时器中有 dom 的引用，即使 dom 删除了，但是定时器还在，所以内存中还是有这个 dom。

   ```js
   // 定时器
   var serverData = loadData()
   setInterval(function () {
     var renderer = document.getElementById('renderer')
     if (renderer) {
       renderer.innerHTML = JSON.stringify(serverData)
     }
   }, 5000)
   
   // 观察者模式
   var btn = document.getElementById('btn')
   function onClick(element) {
     element.innerHTMl = "I'm innerHTML"
   }
   btn.addEventListener('click', onClick)
   ```

   这样的代码很常见，如果id为renderer的元素从DOM中移除，该定时器仍会存在，同时，因为回调函数中包含对serverData的引用，定时器外面的serverData也不会被释放。

   解决方法：

   - 手动删除定时器和 dom。
   - removeEventListener 移除事件监听

3. ##### 闭包引起的内存泄漏

   闭包可以读取函数内部的变量，然后让这些变量始终保存在内存中。如果在使用结束后没有将局部变量清除，就可能导致内存泄露。

   ```js
   function fn () {
     var a = "I'm a";
     return function () {
       console.log(a);
     };
   }
   ```

   解决：将事件处理函数定义在外部，解除闭包。

4. ##### 没有清理的 DOM 元素引用

   原因：虽然别的地方删除了，但是对象中还存在对 dom 的引用。

   ```js
   // 在对象中引用DOM
   var elements = {
     btn: document.getElementById('btn'),
   }
   function doSomeThing() {
     elements.btn.click()
   }
   
   function removeBtn() {
     // 将body中的btn移除, 也就是移除 DOM树中的btn
     document.body.removeChild(document.getElementById('btn'))
     // 但是此时全局变量elements还是保留了对btn的引用, btn还是存在于内存中,不能被GC回收
   }
   ```

   解决方法：手动删除，`elements.btn = null`。

### 29. 前端路由

1. #### 利用Hash实现前端路由

   ```
   http://www.xxx.com/#/login
   ```

   location.hash = '#/login'，而#后面 hash 值的变化，并不会导致浏览器向服务器发出请求，浏览器不发出请求，也就不会刷新页面。每次 hash 值的变化，还会触发`hashchange` 这个事件，通过这个事件我们就可以知道 hash 值发生了哪些变化。然后我们便可以监听`hashchange`来实现更新页面部分内容的操作：

   ```html
   <a href="#/">推 荐</a>
   <a href="#/bangdan">榜 单</a>
   <a href="#/gedan">歌 单</a>
   <div id="content" style="font-size: 30px;">
   </div>
   <script>
       function Router() {
           this.curUrl = '';
           this.routes = {};
           this.refresh = function () {
               this.curUrl = location.hash.slice(1) || '/';
               this.routes[this.curUrl]();
           };
           // 保存每个路由以及回调函数
           this.route = function (path, callback) {
               this.routes[path] = callback;
           }
           window.addEventListener('hashchange', this.refresh.bind(this));
           // 监听load事件，让页面一开始进入推荐页面
           window.addEventListener('load', this.refresh.bind(this));
       }
       const domDiv = document.querySelector('#content');
       const r = new Router();
       r.route('/', () => {
           domDiv.textContent = '推荐';
       })
       r.route('/bangdan', () => {
           domDiv.textContent = '榜单';
       })
       r.route('/gedan', () => {
           domDiv.textContent = '歌单';
       })
   </script>
   ```

2. #### 利用history实现前端路由

   HTML5标准发布。多了两个 API，`pushState` 和 `replaceState`，通过这两个 API 可以改变 url 地址且不会发送请求。

   popstate事件：每当同一个文档的浏览历史（即history对象）出现变化时，就会触发popstate事件。但是仅仅调用`pushState` 和 `replaceState`方法，并不会触发该事件，只有用户点击浏览器倒退按钮和前进按钮，或者使用JS调用back，forward，go方法时才会触发。

   ```html
   <span id="example">
     <a href="/name" title="name">name</a>
     <a href="/age" title="age">age</a>
   </span>
   <div class="main" id="main"></div>
   <script>
       var examplebox = document.getElementById('example')
       var mainbox = document.getElementById('main')
   
       examplebox.addEventListener('click', function (e) {
           // 阻止默认行为不然会跳转
           e.preventDefault()
           var elm = e.target
           var uri = elm.href
           var tlt = elm.title
           history.pushState({ path: uri, title: tlt }, null, uri)
           mainbox.innerHTML = 'current page is ' + tlt
       })
       window.addEventListener('popstate', function (e) {
           var state = e.state
           mainbox.innerHTML = 'current page is ' + state.title
       })
   </script>
   ```


### 30. 设计模式

4. #### 观察者模式

   1. 一个目标者对象 `Subject`，拥有方法：添加 / 删除 / 通知 `Observer`；
   2. 多个观察者对象 `Observer`，拥有方法：接收 `Subject` 状态变更通知并处理；
   3. 目标对象 `Subject` 状态变更时，通知所有 `Observer`。
   
   `Subject` 可以添加一系列 `Observer`， `Subject` 负责维护与这些 `Observer` 之间的联系，“你对我有兴趣，我更新就会通知你”。
   
   Subject - 被观察者，发布者;
   
   Observer - 观察者，订阅者；
   
   ```js
   // 目标者
   class Subject {
     constructor() {
       this.observers = []; // 观察者列表
     }
     // 添加订阅者
     add(observer) {
       this.observers.push(observer);
     }
     // 删除...
     remove(observer) {
       let idx = this.observers.findIndex(item => item === observer);
       idx > -1 && this.observers.splice(idx, 1);
     }
     // 通知
     notify() {
       for(let o of this.observers) {
         o.update();
       }
     }
   }
    
   // 观察者
   class Observer {
     constructor(name) {
       this.name = name;
     }
     // 目标对象更新时触发的回调，即收到更新通知后的回调
     update() {
       console.log(`目标者通知我更新了，我是：${this.name}`);
     }
   }
    
   // 实例化目标者
   let subject = new Subject();
    
   // 实例化两个观察者
   let obs1 = new Observer('前端');
   let obs2 = new Observer('后端');
    
   // 向目标者添加观察者
   subject.add(obs1);
   subject.add(obs2);
    
   subject.notify();
   ```
   
2. #### 发布订阅模式（Publisher && Subscriber）

   基于一个事件（主题）通道，希望接收通知的对象 Subscriber 通过自定义事件订阅主题，被激活事件的对象 Publisher 通过发布主题事件的方式通知各个订阅该主题的 Subscriber 对象。

   ```js
   // 控制中心
   let pubSub = {
     list: {},
     // 订阅
     subscribe: function(key, fn) {
       if (!this.list[key]) this.list[key] = [];
       // 订阅主题
       this.list[key].push(fn);
     },
     //取消订阅
     unsubscribe: function(key, fn) {
       let fnList = this.list[key];
    
       if (!fnList) return false;
    
       if (!fn) { // 不传入指定的方法，清空所用 key 下的订阅
         fnList.length = 0;
       } else {
         fnList.forEach((item, index) => {
           item === fn && fnList.splice(index, 1);
         });
       }
     },
     // 发布
     publish: function(key, ...args) {
       for (let fn of this.list[key]) {
         fn.call(this, ...args);
       }
     }
   }
   // 订阅
   pubSub.subscribe('onwork', time => {
     console.log(`上班了：${time}`);
   })
   pubSub.subscribe('offwork', time => {
     console.log(`下班了：${time}`);
   })
   pubSub.subscribe('launch', time => {
     console.log(`吃饭了：${time}`);
   })
    
   pubSub.subscribe('onwork', work => {
     console.log(`上班了：${work}`);
   })
   // 发布
   pubSub.publish('offwork', '18:00:00');
   pubSub.publish('launch', '12:00:00');
   // 取消订阅
   pubSub.unsubscribe('onwork');
   ```

观察者模式和发布订阅模式的区别

1. 观察者模式维护单一事件对应多个依赖该事件的对象关系；
2. 发布订阅维护多个事件（主题）及依赖各事件（主题）的对象之间的关系；
3. 观察者模式是目标对象直接触发通知（全部通知），观察对象被迫接收通知。发布订阅模式多了个中间层（事件中心），由其去管理通知广播（只通知订阅对应事件的对象）；
4. 观察者模式对象间依赖关系较强，发布订阅模式中对象之间实现真正的解耦。

### 31. call，apply，bind原理

#### call

成员访问，给CONTEXT设置一个属性，属性值一定是我们要执行的函数，接下来基于CONTEXT.XXX()成员访问执行方法，就可以把函数执行，并且改变里面的THIS。

```js
Function.prototype.myCall = function (context, ...rest) {
  // 如果传的是null或者undefined，context的值为window
  var context = context || window;
  context.fn = this;
  var result = context.fn(...rest);
  //销毁调用函数，以免作用域污染
  delete context.fn;
  return result;
}

// test
let obj = {
	name: 'jack'
}
function test(arg1, arg2, arg3) {
  console.log(this.name)   // jack
  console.log(arg1, arg2, arg3);  // 1 2 3
}
test.myCall(obj, 1, 2, 3);
```

#### apply

```js
Function.prototype.myApply = function (context, args) {
  var context = context || window;
  context.fn = this;
  let res;
  if (!args || args.length == 0){
    res = context.fn();
  } else  {
    res = context.fn(...args)
  }
  //销毁调用函数，以免作用域污染
  delete context.fn;
  return res;
}

// test
let obj = {
  name: 'jack'
}
function test(arg1, arg2, arg3) {
  console.log(this.name)   // jack
  console.log(arg1, arg2, arg3);  // 1 2 3
}
test.myApply(obj, [1,2,3]);
```

#### bind

```js
Function.prototype.bindNew = function (context, ...args) {
  return (...newArgs) => this.apply(context, [...args, ...newArgs]);
};

// test
const test = {
  name: "fy",
  showName: function (last: string) {
    console.log(this.name + " is " + last);
  },
};
test.showName("handsome"); // fy is handsome
test.showName.bind({ name: "Mr.fy" })("handsome");
test.showName.bindNew({ name: "Mr.fy" })("handsome");
```

#### instanceof

```js
function myInstanceOf(left, right) {
  let prototype = right.prototype;
  left = left.__proto__;
  while(left) {
    if (left == prototype) return true;
    left = left.__proto__;
  }
  return false;
}

console.log(myInstanceOf([], Array));  // true
```

#### 函数柯里化

```js
function sum(...args1) {
  let x = args1.reduce((tolal, next) => tolal + next)
  return function(...args2) {
    if (args2.length == 0) return x;
    let y = args2.reduce((tolal, next) => tolal + next)
    // 递归调用
    return sum(x+y)
  }
}

console.log(sum(1,2,2,5)(7)()) // 17
```

#### 数组扁平化

```js
var flatten = function(arr) {
  let res = [];
  for (let i = 0; i < arr.length; i++) {
    if (Array.isArray(arr[i])) {
      res = res.concat(flatten(arr[i]))
    } else {
      res.push(arr[i])
    }
  }
  return res;
}

console.log(flatten([1,[1,2,[2,4]],3,5]));  // [1, 1, 2, 2, 4, 3, 5]
```

### 32. 前中后序遍历

#### 前序遍历

利用栈来记录遍历的过程，实际上，递归就使用了调用栈，所以这里我们可以使用栈来模拟递归的过程

- 首先根入栈
- 将根节点出栈，将根节点值放入结果数组中
- 然后遍历左子树、右子树，因为栈是先入后出，所以，我们先右子树入栈，然后左子树入栈
- 继续出栈（左子树被出栈）…….

依次循环出栈遍历入栈，直到栈为空，遍历完成

```js
const preorderTraversal = (root) => {
    const list = [];
    const stack = [];
    
    // 当根节点不为空的时候，将根节点入栈
    if(root) stack.push(root)
    while(stack.length > 0) {
        const curNode = stack.pop()
        // 第一步的时候，先访问的是根节点
        list.push(curNode.val)
        
        // 我们先打印左子树，然后右子树
        // 所以先加入栈的是右子树，然后左子树
        if(curNode.right !== null) {
            stack.push(curNode.right)
        }
        if(curNode.left !== null) {
            stack.push(curNode.left)
        }
    }
    return list
}
```

#### 中序遍历

```js
const inorderTraversal = (root) => {
    let list = []
    let stack = []
    let node = root
    
    while(node || stack.length) {
    // 遍历左子树
      while(node) {
       	stack.push(node)
        node = node.left
      }
      
      node = stack.pop()
      list.push(node.val)
      node = node.right
    }
    return list
}
```

#### 后序遍历

**解题思路：** 后序遍历与前序遍历不同的是：

- 后序遍历是左右根
- 而前序遍历是根左右

如果我们把前序遍历的 `list.push(node.val)` 变更为 `list.unshift(node.val)` （遍历结果逆序），那么遍历顺序就由 **根左右** 变更为 **右左根**

然后我们仅需将 **右左根** 变更为 **左右根** 即可完成后序遍

```js
const postorderTraversal = (root) => {
  const list = [];
  const stack = [];

  // 当根节点不为空的时候，将根节点入栈
  if (root) {
    stack.push(root)
  }
  while (stack.length > 0) {
 	 	const node = stack.pop()
  	// 根左右=>右左根
  	list.unshift(node.val)

    // 先进栈左子树后右子树
    // 出栈的顺序就变更为先右后左
    // 右先头插法入list
    // 左再头插法入list
    // 实现右左根=>左右根
  	if (node.left !== null) {
  		stack.push(node.left)
  	}
    if (node.right !== null) {
      stack.push(node.right)
		}
	}
  return list
}
```

### 33. JS千分位

#### toLocaleString()

#### 正则实现

```js
function format (num) {  
    var reg=/\d{1,3}(?=(\d{3})+$)/g;   
    return (num + '').replace(reg, '$1,');  
}
```

解释

- 正则表达式 \d{1,3}(?=(\d{3})+$)  表示前面有1~3个数字，后面的至少由一组3个数字结尾
- ?=表示正向引用，可以作为匹配的条件，但匹配到的内容不获取，并且作为下一次查询的开始

运行过程

![img](https://images2017.cnblogs.com/blog/738658/201801/738658-20180115110625115-930619959.png)