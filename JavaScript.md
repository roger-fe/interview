## JavaScript

### 1. 内置对象Array

###### 	(1)  判断一个变量是否是数组

​	   Array.isArray(变量)
​	   如果对象是数组返回 true，否则返回 false。

######   (2）join()

​		join() 方法用于把数组中的所有元素转换一个字符串。
​		元素是通过指定的分隔符进行分隔的。	

```typescript
var fruits = ["Banana", "Orange", "Apple", "Mango"];
var energy = fruits.join();
//输出 Banana,Orange,Apple,Mango
```

######   (3）数组的栈方法和队列方法

​		push()  `可向数组的末尾添加一个或多个元素，并返回新的长度。`			
​		pop()    `用于删除数组的最后一个元素并返回删除的元素。`
​		unshift()   `可向数组的开头添加一个或更多元素，并返回新的长度。`
​		shift()  `用于把数组的第一个元素从其中删除，并返回第一个元素的值。`

######     (4)   数组排序-sort()

​		    `sort的默认形式是将数组中的每一个元素转换成字符串进行ACII码比较。`
​			升序：

```typescript
var points = [40,100,1,5,25,10];
points.sort(function(a,b){return a-b});
//输出   1,5,10,25,40,100
```

​			降序：

```typescript
var points = [40,100,1,5,25,10];
points.sort(function(a,b){return b-a});
//输出   100,40,25,10,5,1
```

###### (5）数组合并-concat()

​	   `concat() 方法用于连接两个或多个数组。`
​	   `该方法不会改变现有的数组，而仅仅会返回被连接数组的一个副本。`

```typescript
var colors = ['red','blue']
var newColors = colors.concat('green')
//输出newColors   ['red','blue','green']
----------------------------------------
var hege = ["Cecilie", "Lone"];
var stale = ["Emil", "Tobias", "Linus"];
var kai = ["Robin"];
var children = hege.concat(stale,kai)
//输出children  ['Cecilie','Lone,Emil','Tobias','Linus','Robin']
```

###### (6)  slice()

​	   `slice() 方法可从已有的数组中返回选定的元素。`
​	   `该方法不会改变原始数组。`

```typescript
var fruits = ["Banana", "Orange", "Lemon", "Apple", "Mango"];
var citrus = fruits.slice(1,3);
//输出citrus--["Orange", "Lemon"]
```

###### (7)  splice()	

​	   `splice() 方法用于添加或删除数组中的元素。`
​	   `这种方法会改变原始数组。`

```typescript
Array.splice(start:int,deleteCount:int,items...:any)
var fruits = ["Banana", "Orange", "Apple", "Mango"];
//删除
fruits.splice(2,1); //返回值是被删除的元素
//输出 fruits--["Banana", "Orange", "Mango"]
-------------------------------------------
  
//增加
fruits.splice(2,0,"Apple")
//输出 fruits--["Banana", "Orange", "Apple", "Mango"]
----------------------------------------------------

//替换
fruits.splice(2,1,"abc")
//输出 fruits--["Banana", "Orange", "abc", "Mango"]
```

###### (8)	indexOf()

​		`数组中某个指定的元素位置。`

```typescript
indexOf(searchvalue,start)
//start:可选的整数参数。规定在数组中开始检索的位置。如省略该参数，则将从字符串的首字符开始检索。
var names = ['rose','jack','michael','rose']
console.log(names.indexOf('rose')); // 0
console.log(names.indexOf('rose',1)); // 3
```

###### (9)	lastIndexOf()

​		`返回一个指定的元素在数组中最后出现的位置，从该字符串的后面向前查找`

```typescript
lastIndexOf(searchvalue,start)
//start:可选的整数参数。规定在字符串中开始检索的位置。如省略该参数，则将从字符串的最后一个字符处开始检索。
var names = ['rose','jack','michael','rose']
console.log(names.lastIndexOf('rose')); // 3
console.log(names.lastIndexOf('rose',1)); // 0
```

###### (10)	filter()

​		   `过滤数组中符合条件的所有元素`

```typescript
var numbers = [32, 33, 16, 40];
var filterResult = numbers.filter(function(item,index,array){
  /*
  	item:数组中的每一个元素
  	index:数组中每一个元素的索引
  	array:数组本身
  */
  return item>32;
});
console.log(filterResult);// [33,40]
```

###### (11)	map()

​		   `映射处理原数组中的每一个元素，并返回新的数组`

```typescript
var numbers = [2, 3, 4, 5];
var mapResult = numbers.map(function(item,index,array){
  /*
  	item:数组中的每一个元素
  	index:数组中每一个元素的索引
  	array:数组本身
  */
  return item*2;
});
console.log(mapResult);// [4,6,8,10]
```

###### (12)	forEach()

​		   `遍历数组的每个元素，无返回值`

```typescript
var numbers = [2, 3, 4, 5];
numbers.forEach(function(item,index,array){
  /*
  	item:数组中的每一个元素
  	index:数组中每一个元素的索引
  	array:数组本身
  */
  console.log(item);
});
//2
//3
//4
//5
```

### 2. 字符串

###### (1)	charAt()

​		`获取指定位置的字符`
​		`string.charAt(index)`

```typescript
var str = "HELLO WORLD";
var n = str.charAt(2)
//输出：L
```

###### (2)	charCodeAt()

​		`获取指定位置的字符对应的ASCII编码`
​		`string.charCodeAt(index)`

```typescript
var str = "HELLO WORLD";
var n = str.charCodeAt(0);
//输出：72
```

###### (3)	substring

​		`用于提取字符串中介于两个指定下标之间的字符。`
​		`string.substring(from,to);`

```typescript
var str="Hello world!";
console.log(str.substring(1,4));
//ell
```

###### (4)	substr

​		`可在字符串中抽取从 开始 下标开始的指定数目的字符。`
​		`string.substr(start,length);`

```typescript
var str="Hello world!";
console.log(str.substr(2,3));
//llo
```

### 3. Date

###### (1)	new Date()

​		`创建时间日期对象`
​		`new Date()  创建当前日期和时间`
​		`new Date(dateString) 将字符串日期转换为时间日期对象 `
​		`new Date(year, month, day, hours, minutes, seconds, milliseconds) 可传年月日时分秒参数`

```typescript
var now = new Date();
console.log(now);
//Wed Jul 22 2020 18:09:59 GMT+0800 (中国标准时间)
------------------------------------------------
var xms = new Date('December 25,2021 13:30:00');
console.log(xms);
//Sat Dec 25 2021 13:30:00 GMT+0800 (中国标准时间)
------------------------------------------------
var xms = new Date(2020,10,10);
console.log(xms);
//Tue Nov 10 2020 00:00:00 GMT+0800
```

###### (2)	getDate()

​		`获取当前月份的第几天(1-31)`

```typescript
//当前时间：2020.7.22
var day = new Date().getDate();
console.log(day);
//22
```

###### (3)	getMonth()

​		`获取当前时间的月份(0-11)`

```typescript
//当前时间：2020.7.22
var month = new Date().getMonth();
console.log(month);
//6
```

###### (4)	getFullYear()

​		`获取年份`

```typescript
//当前时间：2020.7.22
var year = new Date().getFullYear();
console.log(year);
//2020
```

###### (5)	getDay()

​		`获取一星期中的第几天(0-6), 0代表星期天, 6代表星期六`

```typescript
//当前时间：2020.7.22
var weekday = new Date().getDay();
console.log(weekday);
//3
```

###### (6)	getHours()，getMinutes()，getSeconds()

​		`获取当前时间的时分秒`

###### (7)	toDateString()

​		`可把 Date 对象的日期部分转换为字符串，并返回 星期几 月 日 年`

```typescript
//当前时间：2020.7.22
var time = new Date().toDateString();
console.log(time);
// Wed Jul 22 2020
```

###### (8)	toTimeString()

​		`可把 Date 对象的日期部分转换为字符串，并返回 时 分 秒 时区`

```typescript
//当前时间：2020.7.22 18:40:41
var time = new Date().toTimeString();
console.log(time);
// 18:40:41 GMT+0800 (中国标准时间)
```

###### (9)	toLocaleDateString()

​		`返回 年/月/日`

```typescript
//当前时间：2020.7.22 18:40:41
var time = new Date().toLocaleDateString();
console.log(time);
// 2020/7/22
```

###### (10)	toLocaleTimeString()

​			`返回 上午/中午/下午 时:分:秒`

```typescript
//当前时间：2020.7.22 18:40:41
var time = new Date().toLocaleTimeString();
console.log(time);
// 下午6:40:41
```

###### (11)	toLocaleString()

​			`返回 年/月/日 上午/中午/下午 时:分:秒`

```typescript
//当前时间：2020.7.22 18:40:41
var time = new Date().toLocaleString();
console.log(time);
// 2020/7/22 下午6:40:41
```

### 4. 将字符串转换为数值

###### (1)	parseInt()

​		`可解析一个字符串，并返回一个整数。`
​		`parseInt(string, radix)`
​		`radix可选。表示要解析的数字的基数。该值介于 2 ~ 36 之间。`

```typescript
parseInt("10")  //10
parseInt("10",16)  //16
```

###### (2)	parseFloat()

​			`该函数指定字符串中的首个字符是否是数字。如果是，则对字符串进行解析，直到到达数字的末端为止，然后以数字								返回该数字，而不是作为字符串`

```typescript
parseFloat(" 60 ") //60
parseFloat("40 years") //NaN
```

###### (3)	Number()

​		`Number() 函数把对象的值转换为数字。`
​		`如果对象的值无法转换为数字，那么 Number() 函数返回 NaN。`

```typescript
var test1= new String("999");  //999	
var test2= new String("999 888");		//NaN
```

### 5. 将数值转换为字符串

###### (1)	toString(radix)

​		`数字的字符串表示`
​		`radix:可选，规定表示数字的基数，是 2 ~ 36 之间的整数。`

```typescript
var num = 15;
var a = num.toString(); //15
var b = num.toString(2); //1111
```

###### (2)	''+number

###### (3)	''.concat(number)

###### (4)	toFixed(x)

​		`返回值 小数点后有固定的 x 位数字`
​		`x:必需。规定小数的位数，是 0 ~ 20 之间的值，包括 0 和 20,如省略，则用0代替`

```typescript
var num = 5.56789;
num.toFixed(2); //5.57
```

### 6. global对象的编码和解码方法

###### (1)	encodeURI(uri)

​		`把字符串作为 URI 进行编码`
​		`encodeURI(uri) 函数不会对 , / ? : @ & = + $ #进行转义 `

```typescript
var uri="my test.php?name=ståle&car=saab";
encodeURI(uri) //my%20test.php?name=st%C3%A5le&car=saab
```

###### (2)	encodeURIComponent(uri)

​		`功能与encodeURI(uri)类似`
​		`encodeURIComponent(uri) 函数会对 , / ? : @ & = + $ #进行转义 `

```typescript
var uri="http://w3cschool.cc/my test.php?name=ståle&car=saab";
encodeURIComponent(uri) //http%3A%2F%2Fw3cschool.cc%2Fmy%20test.php%3Fname%3Dst%C3%A5le%26car%3Dsaab
```

###### (3)	decodeURI(uri)

​		`将encodeURI(uri)的编码结果进行解码`

```typescript
var uri="my test.php?name=ståle&car=saab";
encodeURI(uri)  //my%20test.php?name=st%C3%A5le&car=saab
decodeURI(uri)  //my test.php?name=ståle&car=saab
```

###### (4)	decodeURIComponent(uri)

​		`将encodeURIComponent(uri)的编码结果进行解码`

```typescript
var uri="http://w3cschool.cc/my test.php?name=ståle&car=saab";
encodeURIComponent(uri) //http%3A%2F%2Fw3cschool.cc%2Fmy%20test.php%3Fname%3Dst%C3%A5le%26car%3Dsaab
decodeURIComponent(uri) //http://w3cschool.cc/my test.php?name=ståle&car=saab
```

### 7. Math数学对象

###### 	(1)	Math.max(*n1*,*n2*,*n3*,...,nX)

​			`返回最大值`

```typescript
Math.max(-5,10) //10
var arr = [1,2,32,23,45,21];
Math.max.apply(null,arr); //45
```

###### (2)	Math.min(*n1*,*n2*,*n3*,...,nX)

​		`返回最小值`

```typescript
Math.max(-5,10) //-5
var arr = [1,2,32,23,45,21];
Math.max.apply(null,arr); //1
```

###### (3)	Math.ceil(x)

​		`向上取整`

```typescript
Math.ceil(1.4) // 2
```

###### (4)	Math.floor(x)

​		`向下取整`

```typescript
Math.floor(1.6); // 1
```

###### (5)	Math.round(x)

​		`四舍五入`

```typescript
Math.round(2.5); // 3
```

###### (6)	Math.random()

​		`返回介于 0（包含） ~ 1（不包含） 之间的一个随机数`

### 8. BOM

### 9. DOM

1. **`getBoundingClientRect()`**：方法返回元素的大小及其相对于视口的位置。

2. **`insertAdjacentHTML(position, text)`**： 方法将指定的文本解析为 [`Element`](https://developer.mozilla.org/zh-CN/docs/Web/API/Element) 元素，并将结果节点插入到DOM树中的指定位置。它不会重新解析它正在使用的元素，因此它不会破坏元素内的现有元素。这避免了额外的序列化步骤，使其比直接使用innerHTML操作更快。

   **参数**

   - position: 一个 [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)，表示插入内容相对于元素的位置，并且必须是以下字符串之一：
     - `'beforebegin'`：元素自身的前面。
     - `'afterend'`：元素自身的后面。
     - `'afterbegin'`：插入元素内部的第一个子节点之前。
     - `'beforeend'`：插入元素内部的最后一个子节点之后。
   - text: 是要被解析为HTML或XML元素，并插入到DOM树中的 [`DOMString`](https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString)。



### 10. 函数

###### (1)	call()，apply()

​		 `相同点：都可以用来改变函数的this指向问题，且第一个参数都是this的指向对象(如：{})`
​		 `不同点：call()的参数是直接放进去的，n个参数用逗号隔开，call({},argument[0],argument[1],...)`
​					   `apply()所有参数都是放在一个数组里面传进去，apply({},[argument[0],argument[1]...])`

​		<u>在非严格模式下，如果使用call()或者apply()方法第一个参数传入null或者undefined会被转换成window对象</u>

```typescript
1. 找出数组的最大元素 Math.max.apply(null,arr);
var arr = [1,2,3,4];
var arrMax = Math.max.apply(null,arr);

2. 将类数组转换为真正的数组 Array.prototype.slice.apply(arguments)
function add() {
  var arr = Array.prototype.slice.apply(arguments); //arr为一个真正的数组
}

3. 数组追加
var arr = []
Array.prototype.push.apply(arr,[1,2,3,4]);
console.log(arr);

4. 利用call和apply做继承
function Animal(name,age){
	this.name = name;
  this.age = age;
  this.sayAge = function() {
    console.log(this.age);
  }
}
function Cat(name,age) {
  Animal.call(this,name,age);
  //Animal.apply(this,arguments);
}
var c = new Cat("小黑",20);
```



###### (2)	bind()

​		 `将函数绑定到某个对象中，并且返回一个函数`

```typescript
函数柯里化(将函数的参数进行拆分)
function getConfig(colors,size,otherOptions) {
  console.log(colors,size,otherOptions);
}
var defaultConfig = getConfig.bind(null,'#ff6700', 1024*768);
defaultConfig("123");  // #ff6700 786432 123
defaultConfig("456");  // #ff6700 786432 456
```



### 11. 作用域（全局作用域和函数作用域）

（1）编译（分词、解析、代码生成）
		  编译器查找作用域是否已经有一个名称为a的变量存在于同一个作用域的集合中。如果是，编译器会忽略该		  声明，继续进行编译；否则它会要求作用域在当前作用域的集合中声明一个新的变量，并命名为a。
（2）执行
		  1、引擎运行时会首先查询作用域，在当前的作用域集合中是否存在一个叫作a的变量。如果是，引擎就会使			    用这个变量；如果否，引擎会继续查找该变量。
		  2、如果引擎最终找到了变量a，就会将2赋值给它。否则引擎会抛出一个异常

（3）查询（LHS、RHS）
（4）嵌套
（5）异常

### 12. [prototype、proto、constructor的关系](https://www.cnblogs.com/xiaohuochai/p/5721552.html)

### 13.  window对象

1. getComputedStyle(element, pseudoElement) 用于获取指定元素的 CSS 样式。

   **参数**

   - element: 必需，要获取样式的元素。
   - pseudoElement: 可选，伪类元素，当不查询伪类元素的时候可以忽略或者传入 null。

   **返回值**

   返回的对象是 CSSStyleDeclaration 类型的对象。

2. URLSearchParams 接口定义了一些实用的方法来处理 URL 的查询字符串。

   **返回**

   返回一个 `URLSearchParams `对象。