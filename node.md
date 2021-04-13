### 1. module.exports和exports的区别

exports和module.exports其实是一个东西

```js
console.log(module.exports === exports);

//输出结果为：true
```

module.exports公开了它指向的对象。 exports公开了它指向的对象的属性。

### 2. export和export default的区别

1. export default仅有一个，export可以有多个

   ```js
   //model.js
   let e1='export 1';
   let e2='export 2';
   export {e2};
   export default e1;
   ```

   ```js
   import e1, {e2} from "./model";
   console.log(e1);
   console.log(e2);
   ```

2. 通过export方式导出，在导入时要加{ }，export default则不需要；export`如果要导出已经声明的表示符,必须使用`{}`,例如`export {e1}

3. export能直接导出变量表达式，export default不行。

4. 模块中通过`export` 导出的(属性或者方法)可以修改，但是通过`export default`导出的不可以修改

   ```js
   //model.js
   let e1='export 1';
   let e2='export 2';
   export {e2};
   export default e1;
   e1='export 1 modified';
   e2='export 2 modified';
   ```

   ```js
   //index.js
   import e1, {e2}from "./model";
   console.log(e1); // export 1
   console.log(e2); // export 2 modified
   ```

### 3. require和import的区别

1. `require`引入的是一个值的拷贝，`import`引入的是值的引用。

   ```js
   // lib.js
   var counter = 3;
   function incCounter() {
     counter++;
   }
   module.exports = {
     counter: counter,
     incCounter: incCounter,
   };
   
   // main.js
   var mod = require('./lib');
   
   console.log(mod.counter);  // 3
   mod.incCounter();
   console.log(mod.counter); // 3
   ```

   ES6 模块的运行机制与 CommonJS 不一样。JS 引擎对脚本静态分析的时候，遇到模块加载命令`import`，就会生成一个只读引用。等到脚本真正执行时，再根据这个只读引用，到被加载的那个模块里面去取值。

   ```js
   // lib.js
   export let counter = 3;
   export function incCounter() {
     counter++;
   }
   
   // main.js
   import { counter, incCounter } from './lib';
   console.log(counter); // 3
   incCounter();
   console.log(counter); // 4
   ```

2. `require`是运行时加载，`import`是编译时输出接口

3. `require()`是同步加载模块，`import`命令是异步加载，有一个独立的模块依赖的解析阶段。

### 4. required 的查找模块的顺序

根据参数的不同格式，`require`命令去不同路径寻找模块文件。

1. 如果参数字符串以“/”开头，则表示加载的是一个位于绝对路径的模块文件。比如，`require('/home/marco/foo.js')`将加载`/home/marco/foo.js`。

2. 如果参数字符串以“./”开头，则表示加载的是一个位于相对路径（跟当前执行脚本的位置相比）的模块文件。比如，`require('./circle')`将加载当前脚本同一目录的`circle.js`。

3. 如果参数字符串不以“./“或”/“开头，则表示加载的是一个默认提供的核心模块（位于Node的系统安装目录中），或者一个位于各级node_modules目录的已安装模块（全局安装或局部安装）。

举例来说，脚本`/home/user/projects/foo.js`执行了`require('bar.js')`命令，Node会依次搜索以下文件。

```
/usr/local/lib/node/bar.js
/home/user/projects/node_modules/bar.js
/home/user/node_modules/bar.js
/home/node_modules/bar.js
/node_modules/bar.js
```

4. 如果指定的模块文件没有发现，Node会尝试为文件名添加`.js`、`.json`、`.node`后，再去搜索。`.js`件会以文本格式的JavaScript脚本文件解析，`.json`文件会以JSON格式的文本文件解析，`.node`文件会以编译后的二进制文件解析。