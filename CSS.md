### 1. 动画相关的属性

​	   **transform（转换）**：改变元素形状、尺寸和位置
​	   **transition（过渡）**：元素从一种样式逐渐改变为另一种的效果
​	   **animation**：通过CSS3的@keyframes（关键帧）规则，可以创建动画 
​	   **rotate（deg）**：旋转给定的角度，正值为顺时针，负值为逆时针

### 2. CSS可继承属性

​	   **1、字体系列属性**
​			 font-family：字体系列
​			 font-weight：字体的粗细
​			 font-size：字体的大小
​			 font-style：字体的风格

​	   **2、文本系列属性**
​			 text-indent：文本缩进
​			 text-align：文本水平对齐
​			 line-height：行高
​			 word-spacing：单词之间的间距
​			 letter-spacing：中文或者字母之间的间距
​			 text-transform：控制文本大小写
​			 color：文本颜色

​	   **3、元素可见性**
​			 visibility：控制元素显示隐藏
​			 opacity: 控制元素的透明度

​	   **4、列表布局属性：**
​			 list-style：列表风格，包括list-style-type、list-style-image等

​	   **5、光标属性**
​			 cursor：光标显示为何种形态

### 3. 样式优先级顺序

![specifishity](C:\Users\small black\Desktop\specifishity.png)

​	   <u>!important > 行内样式 > id选择器 > 类选择器、伪类、属性选择器 > 标签选择器、伪元素选择器 > 通配符 > 继承</u>

### 4. CSS 百分比参照问题：

​	   1、参照父元素内容区域宽度的元素：padding  margin  width  text-indent
​	   2、参照父元素内容区域高度的元素：height
​	   3、参照父元素属性的元素：font-size line-height

​	  特殊：相对定位时，top(bottom) left(right)参照父元素内容区域的高度与宽度，而绝对定位时，参照最近的定				  位元素包含padding的高度与宽度。

### 5. 超出文本显示省略号

1. #### 单行超出部分显示省略号

   ```css
   .online {
     overflow: hidden; // 超出的文本隐藏
   	text-overflow: ellipsis; // 溢出用省略号显示
   	white-space: nowrap; // 溢出不换行
   }
   ```

2. #### 多行超出部分显示省略号

   ```css
   .multiple {
     overflow: hidden;
     text-overflow: ellipsis;
     display: -webkit-box; // 作为弹性伸缩盒子模型显示。
     -webkit-box-orient: vertical; // 设置伸缩盒子的子元素排列方式--从上到下垂直排列
     -webkit-line-clamp: 2; // 显示的行
    }
   ```

### 6. BFC

**概念**：BFC是块级格式化上下文，决定了元素如何对其内容进行定位，以及和其他元素的关系和相互作用。可以理解为它就是个**独立的容器，容器里面的布局与外面互不影响**。

**触发 BFC**：

1. `float`的值不为`none`。
2. `overflow`的值为`auto`, `scroll` 或 `hidden`。
3. `display`的值为`table-cell`，`table-caption`， `inline-block`，`flex`，`inline-flex`中的任何一个。
4. `position`的值不为 `relative` 和 `static`。

**特性：**
1、<u>同一个 BFC 下外边距会发生折叠</u>
2、<u>BFC 可以包含浮动的元素（清除浮动）</u>
3、<u>BFC 元素可以阻止被浮动元素覆盖</u>

### 7. 点击a标签的顺序

1. :link 向未被访问的链接添加样式。
2. :visited 向已被访问的链接添加样式。
3. :hover 当鼠标悬浮在元素上方时，向元素添加样式。
4. :focus 向拥有键盘输入焦点的元素添加样式。
5. :active 向被激活的元素添加样式。

### 8. 伪类和伪元素的区别

伪类和伪元素的根本区别在于：它们是否创造了**新**的元素，这个新创造的元素就叫 "伪元素" 。

伪类：是元素的某种状态，只有符合触发条件时才能看到，逻辑上存在但在文档树中却无须标识的“幽灵”分类。

| **属性**                                                     | **描述**                                 |
| ------------------------------------------------------------ | ---------------------------------------- |
| [:link](https://www.w3school.com.cn/cssref/pr_pseudo_link.asp) | 向未被访问的链接添加样式。               |
| [:visited](https://www.w3school.com.cn/cssref/pr_pseudo_visited.asp) | 向已被访问的链接添加样式。               |
| [:hover](https://www.w3school.com.cn/cssref/pr_pseudo_hover.asp) | 当鼠标悬浮在元素上方时，向元素添加样式。 |
| [:active](https://www.w3school.com.cn/cssref/pr_pseudo_active.asp) | 向被激活的元素添加样式。                 |
| [:focus](https://www.w3school.com.cn/cssref/pr_pseudo_focus.asp) | 向拥有键盘输入焦点的元素添加样式。       |
| [:first-child](https://www.w3school.com.cn/cssref/pr_pseudo_first-child.asp) | 向元素的第一个子元素添加样式。           |
| [:last-child](https://www.runoob.com/cssref/sel-last-child.html) | 向元素的最后一个子元素添加样式。         |

伪元素：是新的元素，是虚拟的元素，不存在DOM文档中，这个新元素(伪元素)是某个元素的子元素，这个子元素虽然逻辑上存在，但却并不实际存在于文档树中。

| **属性**                                                     | **描述**                         |
| ------------------------------------------------------------ | -------------------------------- |
| [:first-letter](https://www.w3school.com.cn/cssref/pr_pseudo_first-letter.asp) | 向文本的第一个字母添加特殊样式。 |
| [:first-line](https://www.w3school.com.cn/cssref/pr_pseudo_first-line.asp) | 向文本的首行添加特殊样式。       |
| [:before](https://www.w3school.com.cn/cssref/pr_pseudo_before.asp) | 在元素之前添加内容。             |
| [:after](https://www.w3school.com.cn/cssref/pr_pseudo_after.asp) | 在元素之后添加内容。             |

因为伪类是类似于添加类所以可以是多个，而伪元素在一个选择器中只能出现一次，并且只能出现在末尾 

### 9. 行内元素和块级元素

行内元素：

- [b](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/b), [i](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/i), [small](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/small), [em](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/em), [strong](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/strong)
- [abbr](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/abbr), [cite](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/cite), [code](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/code), [dfn](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/dfn), [var](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/var)
- [a](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/a), [bdo](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/bdo), [br](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/br), [img](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/img), [object](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/object), [q](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/q), [script](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/script), [span](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/span), [sub](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/sub), [sup](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/sup)
- [button](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/button), [input](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/Input), [label](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/label), [select](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/select), [textarea](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/textarea)

块级元素：

- [address](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/address), [article](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/article), [aside](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Element/aside), footer, header, section
- audio, video, canvas
- blockquote, hr, output, pre
- div, p, ol, ul, li, dl, dd, form, h1~h6, hgroup, table, tfoot
- filedset, figcaption, figure

> https://developer.mozilla.org/zh-CN/docs/Web/HTML/Block-level_elements

空元素：br hr img input link meta

#### 区别

- 行内元素会在一行水平方向排列，块级元素独占一行，自动填满父级元素
- 块级元素可以嵌套行内元素和块级元素，行内只能嵌套文本和其他行内元素
  - p只接受语句型元素
  - h1-h6、dt、dl、dd块不推荐嵌套块级元素
  - a的子元素是以它的父元素允许的子元素为准，但不包括交互型元素。
- 盒模型属性上，行内元素设置width，height无效，设置pading和margin垂直方向上无效

#### 为什么img是inline还可以设置宽高？

img是**可替换元素**，这类元素的展现效果不是由CSS来控制的。他们是一种外部对象，外观的渲染独立于CSS。内容不受当前文档的样式影响，CSS可以影响可替换元素的位置，但是不会影响到可替换元素自身的内容。（比如iframe，可能有自己的样式表，不会继承父文档的样式）可替换元素有内置宽高，性质同设置了inline-block一样。

### 10. 外边距重叠

多个相邻(兄弟或父子) 普通流的块级元素在垂直方向的margin会重叠

- 两个相邻的外边距都为正数，折叠结果是较大的值
- 两个相邻的外边距为负数，折叠结果是绝对值较大的值
- 两个相邻外边距为一正一负，折叠结果是他们的和

### 11. 层叠上下文、层叠水平、层叠顺序

#### 什么是“层叠上下文”

如果一个元素含有层叠上下文，(也就是说它是层叠上下文元素)，我们可以理解为这个元素在`Z轴`上就“高人一等”，最终表现就是它离屏幕观察者更近。

> **具象的比喻**：你可以把层叠上下文元素理解为**该元素当了官**，而其他非层叠上下文元素则可以理解为普通群众。凡是“当了官的元素”就比普通元素等级要高，也就是说元素在`Z轴`上更靠上，更靠近观察者。

层叠上下文也基本上是有一些特定的CSS属性创建的，一般有3种方法：

1. `HTML`中的根元素`<html></html>`本身就具有层叠上下文，称为“根层叠上下文”。
2. 普通元素设置`position`属性为**非**`static`值并设置`z-index`属性为具体数值，产生层叠上下文。
3. CSS3中的新属性也可以产生层叠上下文。
   - 父元素的display属性值为`flex|inline-flex`，子元素`z-index`属性值不为`auto`的时候，子元素为层叠上下文元素；
   - 元素的 `opacity` 属性值不是 `1`；
   - 元素的 `transform` 属性值不是 `none`；
   - 元素 `mix-blend-mode` 属性值不是 `normal`；
   - 元素的 `filter` 属性值不是 `none`；
   - 元素的 `isolation` 属性值是 `isolate`；
   -  `will-change` 指定的属性值为上面任意一个；
   - 元素的 `-webkit-overflow-scrolling` 属性值设置为`touch`。

#### 什么是“层叠水平”

决定了同一个层叠上下文中元素在z轴上的显示顺序。所有的元素都有层叠水平，包括层叠上下文元素，层叠上下文元素的层叠水平可以理解为官员的职级，1品2品，县长省长之类。普通元素的层叠水平优先由层叠上下文决定，因此，层叠水平的比较只有在当前层叠上下文元素中才有意义。

#### 什么是“层叠顺序”

“**层叠顺序**”(stacking order)表示元素发生层叠时按照特定的顺序规则在`Z轴`上垂直显示。由此可见，前面所说的“层叠上下文”和“层叠水平”是一种概念，而这里的“层叠顺序”是一种规则。

![层叠顺序](https://image.zhangxinxu.com/image/blog/201601/2016-01-07_223349.png)

1. 左上角"层叠上下文`background/border`"指的是层叠上下文元素的背景和边框。
2. `inline/inline-block`元素的层叠顺序要高于`block`(块级)/`float`(浮动)元素。
3. 单纯考虑层叠顺序，`z-index: auto`和`z-index: 0`在同一层级，但这两个属性值本身是有根本区别的。

为什么`inline/inline-block`元素的层叠顺序要高于`block`(块级)/`float`(浮动)元素？

因为`border`/`background`一般为装饰属性，而浮动和块状元素一般用作布局，而内联元素都是内容。而网页设计之初最重要的就是文字内容，所以在发生层叠时会优先显示文字内容，保证其不被覆盖。

#### 层叠准则

1. **谁大谁上：**当具有明显的层叠水平标示的时候，如识别的z-index值，在同一个层叠上下文中，层叠水平值大的那一个覆盖小的那一个。通俗讲就是官大的压死官小的。
2. **后来居上：**当元素的层叠水平一致、层叠顺序相同的时候，在DOM流中处于后面的元素会覆盖前面的元素。

> 参考：https://blog.csdn.net/llll789789/article/details/97562099，https://www.zhangxinxu.com/wordpress/2016/01/understand-css-stacking-context-order-z-index/

### 12. 元素隐藏的方法

`display: none` 

1. 不占据空间，资源会加载，DOM可以访问
2. 会产生回流
3. 该节点和子孙节点都会隐藏

`visibility: hidden` 

1. 占据空间，资源会加载，DOM可以访问，但不能点击
2. 只会产生重绘
3. 该节点的子孙节点可以设置 `visibility:visible` 显示

`opacity：0 ` 

1. 占据空间，资源会加载，DOM可以访问，可以点击。
2. 该节点是在合成层的话，是不会发生重绘的。

### 13. Rem, em和px的区别

px是绝对长度单位。

em是相对长度单位，继承父级元素的字体大小，所有字体都是相对于父元素大小的

rem也是相对长度单位，但它是相对于根元素（html),不会像em造成混乱。

### 14. img和background-image的区别

- 解析机制：img属于html标签，background-img属于css。img先解析
- SEO：img标签有一个alt 属性可以指定图像的替代文本，有利于SEO，并且在图片加载失败时有利于阅读
- 语义化角度：img语义更加明确

### 15. rgba()和opacity的区别

- opacity 作用于元素及元素中所有的内容（包括文字、图片） 有继承性

- rgba() 只用于元素的颜色及背景色

### 16. outline和border的区别

outline 

1. outline 是针对链接、表单控件元素设计。
2. outline 的效果将随元素的 focus 而自动出现，相应的由 blur 而自动消失。这些都是浏览器的默认行为，无需JavaScript配合CSS来控制。
3. outline不占据空间，不会像border那样影响元素的尺寸或者位置。

border

1. border 可应用于几乎所有有形的html元素

### 17. 清除浮动

1. BFC

   给父容器加上overflow:hidden，加上之后，形成BFC，需要计算超出的大小来隐藏，所以父容器会撑开放入子元素，同时计算浮动的子元素。

   缺点：但是一旦子元素大小超过父容器大小就会显示异常。

2. 使用带有clear属性的空元素

   在浮动元素后面添加一个不浮动的空元素，父容器必须考虑浮动子元素的位置，子元素出现在浮动元素后面，所以显示出来就正常了。

   同时要给空元素加上:  `style="clear:both"`

   缺点：需要添加额外的html标签，这违背了语义网的原则

3. 使用伪元素::after

   它父容器尾部自动创建一个子元素，原理和空元素一样，可以把它设置为height：0不显示，clear：both display:block，保证空白字符不浮动区块。

   ```css
   .clearifx::after{
       content:'';
       height:0;
       clear:both;
       display:block;
   }
   ```

### 18. 水平垂直居中

#### 水平居中

1. 利用块级元素撑满父元素的特点，如果宽度已定，子元素使用margin: 0 auto 就可以平分水平方向上的空间
2. 利用行内块居中的特点，父元素设置为text-align: center，子元素的display必须为inline或inline-block
3. 元素设置： `position: absolute`; `left: 50%`; `transform: translateX(-50%)`;，父元素设置position: relative; 
4. 元素设置： `position: absolute`;`left: 0`;`right: 0`;`margin: 0 auto`，父元素设置position: relative; 
5. flex布局，父元素设置 display: flex; justify-content: center;

#### 垂直居中

1. 父元素高度确定的单行文本，设置line-height：高度

2. 父元素设置display: table-cell; vertical-align: middle;，并且父元素必须设置宽高，子元素就会垂直居中

3. 元素设置： `position: absolute`; `top: 50%`; `transform: translateY(-50%)`;，在非static的定位父元素垂直居中

4. 元素设置： `position: absolute`;`top: 0`;`bottom: 0`;`margin: auto 0`，父元素设置position: relative; 

5. flex布局，父元素设置 display: flex; align-items: center;

6. 父元素设置伪元素

   ```css
   parent:after {
     content: '';
     height: 100%;
     vertical-align: middle;
     width: 0;
     display: inline-block;
   }
   child {
     display: inline-block;
     vertical-align: middle;
   }
   ```

#### 水平垂直居中

1. 利用父相子绝+margin

   ```css
   parent{
       position:relative;
   }
   ```

   

   ```css
   child{
     	width: wpx;
     	height: hpx;
       position:absolute;
       top:50%;
       left:50%;
       margin-top:(-h/2)px;
       margin-left:(-w/2)px;
   }
   ```

   ```css
   child{
       position:absolute;
       top:0;
       left:0;
       right:0;
       bottom:0;
       margin:auto;
   }
   ```

   ```css
   child{
     	width: wpx;
     	height: hpx;
       position:absolute;
       top:calc(50%-h/2px);
       left:calc(50%-w/2px);
   }
   ```

   ```css
   child{
       position:absolute;
       top:50%;
       left:50%;
       transform:translate(-50%,-50%);
   }
   ```

2. flex布局

   ```css
   parent{
   	display: flex;
   	justify-content: center;
   	align-items: center;
   }
   ```

3. 文本水平垂直居中

   ```css
   parent{
     height: hpx;
   	text-align: center;
     line-height: hpx;
   }
   child {
     display: inline-block
   }
   ```

4. 利用table-cell和text-align

   ```css
   parent {
     width: wpx;
     height: hpx;
     display: table-cell;
     vertical-align: middle;
     text-align: center;
   }
   child {
     display: inline-block;
   }
   ```


### 19. 两栏布局

#### float

两个div，第1个div设置 `float: left; width: wpx;`， 第2个div设置`margin-left: wpx;`

```css
div1 {
  width: wpx;
  float: left;
}
div2 {
  margin-left: wpx;
}
```

#### 绝对定位

三个div，一个父div，两个子div，父div设置 `position: relative`，第1个子div设置 `position: absolute;width: wpx;`，第2个子div设置 `margin-left: wpx; width: 100%`；

```css
parent {
	positon: relative;
}
son1 {
  postion: absolute;
  width: wpx;
}
son2 {
  margin-left: wpx;
}
```

#### table布局

三个div，父div设置 `display: table;`，第1个子div设置`width: wpx;`  (需要时可以设置margin-left)，第2个子div设置 `display: table-cell; width: 100%;`（不可以设置margin）

```css
parent {
  display: table;
}
son1 {
  width: 100px;
 /* margin-right: 20px; */
}
son2 {
  display: table-cell;
  width: 100%;
}
```

#### flex布局

三个div，父div设置 `display: flex;`，第1个子div可以设置`width: wpx;`，第2个div设置 `flex: 1;`，若两个子div都设置了 `flex: 1;`，那么两个子div会平分父div的空间

```css
parent {
  display: flex;
}
son1 {
  width: 100px;
 /* flex: 1 */
}
son2 {
  flex: 1
}
```

### 20. 三栏布局

#### 左右中

##### 浮动布局

四个div，第1个div设置`float: left; width: lwpx`，第2个div设置`float: right;width: rwpx`，第3个div设置`margin: 0 rw 0 lwpx;`。

```css
#left {
  width: 100px;
  float: left;
}

#right {
  float: right;
  width: 100px;
}

#middle {
  margin: 0 100px;
}
```

```html
<div id="parent">
  <div id="left">左</div>
  <div id="right">右</div>
  <div id="middle">中</div>
</div>
```

##### 绝对定位

四个div，父div设置 `position:relative`，第1个div设置`position: absolute; width: lwpx`，第2个div设置`position: absolute; width: rwpx; right: 0;`，第3个div设置`margin: 0 rw 0 lwpx;`。

```css
#parent {
  position: relative;
}

#left {
  position: absolute;
  width: 100px;
}

#right {
  position: absolute;
  width: 100px;
  right: 0;
}

#middle {
  margin: 0 150px;
}
```

```html
<div id="parent">
    <div id="left">左</div>
    <div id="right">右</div>
    <div id="middle">中</div>
</div>
```

##### BFC特点：不被浮动元素覆盖

四个div，第1个div设置`float: left; width: lwpx`，第2个div设置`float: right;width: rwpx`，第3个div设置`overflow: hidden`。用此方法第3个div设置的margin值还是以父元素参考对象，所以可以用两边浮动元素设置margin值

```css
#left {
  float: left;
  width: 100px;
  /* margin-right: 10px; */
}

#right {
  float: right;
  width: 100px;
  /* margin-left: 10px; */
}

#middle {
  overflow: hidden;
}
```

```html
<div id="parent">
  <div id="left">左</div>
  <div id="right">右</div>
  <div id="middle">中</div>
</div>
```

#### 左中右

##### table布局

四个div，父div设置 `display: table;`，第1个div设置` width: lwpx`，第2个div设置`display: table-cell; width: 100%;`，第3个div设置` width: rwpx; `。margin只能在所有两个div设置。

```css
#parent {
  display: table;
}

#left {
  width: 100px;
  /* margin-right: 10px;*/
}

#middle {
  width: 100%;
  display: table-cell;
}

#right {
  width: 100px;
  /* margin-left: 10px; */
}
```

```html
<div id="parent">
  <div id="left">左</div>
  <div id="middle">中</div>
  <div id="right">右</div>
</div>
```

##### flex布局

四个div，父div设置 `display: flex;`，第1个div设置` flex-basic: lwpx`，第2个div设置` flex-basic: rwpx `，第3个div设置`flex: 1`。如果三个子div都设置了`flex: 1`，那么就会平分父div的空间。

```css
#parent {
  display: flex;
}

#left {
  flex-basic: 100px;
}

#middle {
  /* margin: 0 20px; */
  flex: 1;
}

#right {
  flex-basic: 100px;
}
```

```html
<div id="parent">
  <div id="left">左</div>
  <div id="middle">中</div>
  <div id="right">右</div>
</div>
```

##### grid布局

父div设置`display: grid; grid-template-columns: 150px auto 150px;`

```css
#parent {
  display: grid;
  grid-template-columns: 150px auto 150px;
}

#middle {
  /* margin: 0 50px; */
}
```

```html
 <div id="parent">
     <div id="left">左</div>
     <div id="middle">中</div>
     <div id="right">右</div>
</div>
```

#### 中左右

##### 前言：margin负值情况下

- margin-top 和 margin-left 会影响自身向指定方向偏移

- margin-right 和 margin-bottom 会影响相邻元素向指定方向偏移
- 后边的元素也可以通过负边距实现覆盖前边元素。

##### 圣杯布局

- 左中右三个元素分别左浮动。
- 设置父元素的左右 padding 为左右两个元素留出空间，以展示中间元素内容。
- 中间元素占据第一位置优先渲染，设置该元素 width 为 100%（此时宽度是父元素content的宽度，减去了左右padding）
- 左元素设置左边距为-100%（100%=同上100%值）以使得左元素上升一行并且处于最左位置，右元素设置左边距为自身宽度的负值使得右元素上升一行处于最右位置。
- 设置左右元素为相对定位，左元素的 left 和右元素的 right 为内边距的宽度的负值。

```css
#parent {
    overflow: hidden; /* 清除浮动 */
    background-color: antiquewhite;
    padding: 0 110px; /* 预留左右两边的位置，实际上是控制中间div的宽度 */
}

#middle {
    float: left;
    width: 100%;
    height: 200px;
}

#left {
    float: left;
    width: 100px;
    height: 200px;
    margin-left: -100%;
    position: relative;
    left: -110px;
}

#right {
    float: left;
    width: 100px;
    height: 200px;
    margin-left: -100px;
    position: relative;
    left: 110px
}
```

```html
<div id="parent">
    <div id="middle">中</div>
    <div id="left">左</div>
    <div id="right">右</div>
</div>
```

##### 双飞翼布局

- 左中右三个元素分别左浮动。
- 中间元素占据第一位置优先渲染，设置该元素 width 为 100%
- 左元素设置左边距为-100%以使得左元素上升一行并且处于最左位置，右元素设置左边距为自身宽度的负值使得右元素上升一行处于最右位置。
- 设置中间元素的子元素左右边距为左右元素留空位，以展示中间元素内容。

```css
#parent {
    overflow: hidden; /* 清除浮动 */
    background-color: antiquewhite;
}

#outMiddle {
    float: left;
    width: 100%;
}

#middle {
    height: 200px;
    border: 1px solid black;
    margin: 0 110px;
}

#left {
    float: left;
    width: 100px;
    height: 200px;
    border: 1px solid red;
    margin-left: -100%;
}

#right {
    float: left;
    width: 100px;
    height: 200px;
    margin-left: -100px;
}
```

```html
<div id="parent">
    <div id="outMiddle">
      <div id="middle">中</div>
  	</div>
    <div id="left">左</div>
    <div id="right">右</div>
</div>
```



##### 圣杯布局与双飞翼布局的区别

圣杯布局跟双飞翼布局的实现上，在前部分是一样的。同样都是左右栏定宽，中间栏自适应。采用浮动和负边距使左右栏与中间栏并排。不同之处大部分在于中间元素的的展示方式上。

圣杯布局采用父元素设置边距的方法，左右元素设置相对定位辅助。而双飞翼布局在中间采用嵌套子元素方法，通过设置子元素外边距来展示。

对比看来，双飞翼比圣杯多了一个嵌套元素，但是少了左右元素的定位。

