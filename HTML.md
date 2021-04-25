### 1. **DOCTYPE**

`<!DOCTYPE>` 声明必须是HTML文档的第一行。

`<!DOCTYPE>` 声明包含在html标签里，对大小写不敏感，但它不是 HTML 标签；它的作用为了告诉浏览器该文件的类型。让浏览器解析器知道应该用哪个规范来解析文档。

因为 HTML 4.01 基于 SGML（标准通用标记语言），所以在 HTML 4.01 中，<!DOCTYPE> 声明需要引用 DTD（声明文件类型定义）。DTD 规定了标记语言的规则，这样浏览器才能正确地呈现内容。

HTML5 不基于 SGML，所以不需要引用 DTD。但是需要doctype来规范浏览器的行为。

SGML 即Standard Globalized Markup Language 是用来定义标准的标记语言，简单的说，就是定义文档的元语言。

#### HTML 4.01 与 HTML5 之间的差异

在 HTML 4.01 中有三种 <!DOCTYPE> 声明。在 HTML5 中只有一种：

```
<!DOCTYPE html>
```

#### 常用的 DOCTYPE 声明

##### HTML 5

```
<!DOCTYPE html>
```

##### HTML 4.01 Strict(严格的)

该 DTD 包含所有 HTML 元素和属性，但不包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。

```html
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
```

##### HTML 4.01 Transitional(过渡的)

该 DTD 包含所有 HTML 元素和属性，包括展示性的和弃用的元素（比如 font）。不允许框架集（Framesets）。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" 
"http://www.w3.org/TR/html4/loose.dtd">
```

##### HTML 4.01 Frameset(框架集的)

该 DTD 等同于 HTML 4.01 Transitional，但允许框架集内容。

```
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" 
"http://www.w3.org/TR/html4/frameset.dtd">
```

### 2. 严格模式和混杂模式

严格模式（标准模式）：指浏览器按照W3C标准解析代码。

混杂模式（兼容模式，怪异模式）：是指浏览器用自己的方式解析代码。

#### 区分：与网页中的DTD相关

1. 如果XHTML、HTML 4.01文档包含形式完整的DOCTYPE，那么它以标准模式呈现。
2. 有过渡的、框架集的DTD而没有URL会导致页面以混杂模式呈现。
3. DOCTYPE不存在或形式不正确会以混杂模式呈现。
4. HTML5 没有 DTD ，因此也就没有严格模式与混杂模式的区别，HTML5 有相对宽松的语法，实现时，已经尽可能大的实现了向后兼容。

#### 意义

以前为了保障自己的网站在各个浏览器上显示正确，网页开发者们不得不根据各个浏览器自身的规范来排版以及确定JS的运行模式，因此大部分网站的实现并不符合W3C规范的标准。所以说如果只存在严格模式（也就是让各个浏览器只按照W3C标准解析代码），那么之前依据各个浏览器自身的规范来排版网站必然受到影响；如果只存在混杂模式，那么会回到当时浏览器大战时的混乱，每个浏览器都有自己的解析模式。

#### 区别

1. 混杂模式下盒子模型的宽高包括padding和border，而标准模式中盒子模型的宽高指的是content的高宽；
2. 混杂模式下可以设置行内元素的高度，而标准模式下不可以；
3. 混杂模式下设置图片padding会失效；
4. 混杂模式下Table中的字体属性不能继承上层的设置；
5. 混杂模式下white-space:pre会失效。
6. 标准模式下，一个元素的高度是由其包含的内容来决定的，如果父元素没有设置高度（假如设置了padding和border），子元素设置一个百分比的高度无效；
7. 标准模式下使用margin:0 auto;可以使元素水平居中，但是在混杂模式下会失效；混杂模式下需要设置text-align:center;来进行水平居中；

### 3. HTML5废除的元素

  1. 能用css代替的元素

     basefont、big、center、font、s、strike（已用del代替）、tt（已用code代替）、u。这些元素纯粹是为画面展示服务的，HTML5中提倡把画面展示性功能放在css中统一编辑。

  2. 不再使用frame框架

     frameset、frame、noframes。HTML5中不支持frame框架，只支持iframe框架，或者用服务器方创建的由多个页面组成的符合页面的形式，删除以上这三个标签。

  3. 只有部分浏览器支持的元素

     applet（已用object代替）、bgsound（已用audio代替）、blink、marquee等标签。


### 4. html5中可以省略结束标记的元素有

​		dd、dt、li、p、optgroup、option、rt、rp、thread、tfoot、tr、td、th

### 5. meta标签

设置网页中一些的元数据（浏览器与生俱来的数据），元数据是给浏览器或者爬虫程序去看的

| 属性              | 值                                                           | 描述                                              |
| :---------------- | :----------------------------------------------------------- | :------------------------------------------------ |
| charset( H5 新增) | character_set                                                | 定义文档的字符编码。                              |
| content           | text                                                         | 定义与 http-equiv 或 name 属性相关的元信息。      |
| http-equiv        | content-type<br />expires<br />refresh<br />set-cookie       | 把 content 属性关联到 HTTP 头部。                 |
| name              | author<br />description<br />keywords<br />generator<br />revised<br />others | 把 content 属性关联到一个名称。                   |
| scheme(H5 删除)   | format/URI                                                   | HTML5不支持。 定义用于翻译 content 属性值的格式。 |

#### name

name属性主要用于描述网页，对应属性是 content ，以便于搜索引擎机器人查找、分类。

语法：<meta name="参数" content="参数值" />

1. keywords（关键字）-  为搜索引擎提供的关键字列表。

   <meta name="keywords" content="程序员,程序猿,攻城狮"/>

2. description（简介）-  用来告诉搜索引擎，网站的主要内容。

   <meta name="description" content="meta标签是HTML中的一个重要标签，它位于HTML文档头部的<HEAD>标签和<TITL>标签之间。"/>

3. robots（机器人向导）- 用来告诉搜索引擎，哪些页面需要索引，哪些页面不需要索引。

   <meta name="robots" content="all/none/index/noindex/follow/nofollow"/>

   默认值是all。

   参数说明：

   all：文件将被检索，且页面上的链接可以被查询；

   none：文件将不被检索，且页面上的链接不可以被查询；

   noindex：文件将不被检索，但页面上的链接可以被查询；

   index：文件将被检索；

   follow：页面上的链接可以被查询；

   nofollow：文件将被检索，但页面上的链接不可以被查询；

4. author（作者）-  标注网页的作者。

   <meta name="author" content="TG,TG@qq.com"/>

5. copyright（版权）-  标注版权。

   <meta name="copyright" content="本网站版权归TG所有"/>

6. generator - 说明网站采用什么编辑器制作。

   <meta name="generator" content="你所用的编辑器"/>

7. revisit-after（重访）-  网站重访

   <meta name="revisit-after" content="7days"/>

#### http-equiv

`http-equiv`属性是添加http响应头部内容，对一些自定义的，或者需要额外添加的http响应头部内容，需要发送到浏览器中，我们就可以是使用这个属性。

语法：<meta http-equiv="参数"  content="参数值"/>

1. Expires（期限）-  指定网页在缓存中的过期时间，一旦网页过期，必须到服务器上重新传输。

   <meta http-equiv="expires" content="Wed, 26 Feb 1997 08:21:57 GMT"/>

   ==注意：==必须使用UTC的时间格式，或者直接设为0（数字表示多久后过期）

2. Pragma（cache模式）-  禁止浏览器从本地计算机的缓存中访问页面内容。

   <meta http-equiv="pragma" content="no-cache"/>

   ==注意：==网页不保存在缓存中，每次访问都刷新页面。这样设定，访问者将无法脱机浏览。

3. Refresh（刷新）-  自动刷新并指向新页面。

   <meta http-equiv="refresh" content="5; url=http://www.baidu.com/"/> 


   其中的5表示5秒后自动刷新并调整到URL新页面。

4. set-cookie（cookie设定）-  浏览器访问某个页面时会将它存在缓存中，下次再次访问时就可从缓存中读取，以提高速度。

   如果网页过期，那么存盘的cookie将被删除。

   <meta http-equiv="set-cookie"  content="cookievalue=xxx; expires=Wednesday, 21-Oct-98 16:14:21 GMT; path=/">

5. window-target（显示窗口的设定）-  强制页面在当前窗口以独立页面显示

   <meta http-equiv="window-target" content="_top"/>

   可以用来防止别人在框架里调用你的页面。

6. content-type（显示字符集的设定）-  设定页面使用的字符集

   <meta http-equiv="content-type" content="text/html;charset=utf-8"/>

7. content-Language（显示语言的设定）-  显示语言

   <meta http-equiv="content-language" content="zh-cn"/>

#### HTML5新增

##### name

1. viewport - 能优化移动端浏览器的显示（屏幕的缩放）

   <meta name="viewport" content="width=device-width, initial-scale=1.0, maximum-scale=1.0, user-scalable=no"/>

   参数值：

   width（viewport的宽度）： device-width | 数值 

   height（viewport 的高度 ）：device-height | 数值 

   user-scalable（是否允许缩放）： yes|no

   initial-scale （初始的缩放比例） ： <=10 &&  >0

   minimum-scale （允许缩放的最小比例） ：数值   

   maximum-scale （允许缩放的最大比例） ：数值

2. format-detection - 忽略电话号码和邮箱

   忽略页面中的数字识别为电话号码

   <meta name="format-detection" content="telephone=no">

   忽略页面中的邮箱格式识别为邮箱

   <meta name="format-detection" content="email=no"/>

   也可以写成：

   <meta name="format-detection" content="telphone=no, email=no"/>  

3. 浏览器内核控制 - 国内浏览器很多都是双内核（webkit和Trident），webkit内核高速浏览，IE内核兼容网页和旧版网站。而添加meta标签的网站可以控制浏览器选择何种内核渲染。（仅限360浏览器）

   <meta name="renderer" content="webkit|ie-comp|ie-stand">
   若页面需默认用极速核，增加标签：<meta name="renderer" content="webkit">
   若页面需默认用ie兼容内核，增加标签：<meta name="renderer" content="ie-comp">
   若页面需默认用ie标准内核，增加标签：<meta name="renderer" content="ie-stand">

4. WebApp全屏模式

   <meta name="apple-mobile-web-app-capable" content="yes" />

##### http-equiv

1. 优先使用 IE 最新版本和 Chrome

   <meta http-equiv="X-UA-Compatible" content="IE=edge, chrome=1" />  

   <!-- 关于X-UA-Compatible -->  

   <meta http-equiv="X-UA-Compatible" content="IE=6" ><!-- 使用IE6 -->  

   <meta http-equiv="X-UA-Compatible" content="IE=7" ><!-- 用于在IE8版本浏览器中使用IE7渲染来避免出错 -->  
   <meta http-equiv="X-UA-Compatible" content="IE=8" ><!-- 使用IE8 -->

2. 转码申明 - 用百度打开网页可能会对其进行转码（比如贴广告），避免转码可添加如下meta

   <meta http-equiv="Cache-Control" content="no-siteapp" />

##### charset

<meta charset="UTF-8">

meta标签的charset的信息参数如GB2312时，代表说明网站是采用的编码是简体中文；

meta标签的charset的信息参数如BIG5时，代表说明网站是采用的编码是繁体中文； 

meta标签的charset的信息参数如iso-2022-jp时，代表说明网站是采用的编码是日文；  

meta标签的charset的信息参数如ks_c_5601时，代表说明网站是采用的编码是韩文；  

meta标签的charset的信息参数如ISO-8859-1时，代表说明网站是采用的编码是英文；  

meta标签的charset的信息参数如UTF-8时，代表世界通用的语言编码。

#### SEO优化部分

```html
<!-- 页面标题<title>标签(head 头部必须) -->
<title>your title</title>
<!-- 页面关键词 keywords -->
<meta name="keywords" content="your keywords">
<!-- 页面描述内容 description -->
<meta name="description" content="your description">
<!-- 定义网页作者 author -->
<meta name="author" content="author,email address">
<!-- 定义网页搜索引擎索引方式，robotterms 是一组使用英文逗号「,」分割的值，通常有如下几种取值：none，noindex，nofollow，all，index和follow。 -->
<meta name="robots" content="index,follow">
```

### 6. src和href的区别

href：指向网络资源位置，建立当前文档中元素与资源之间的链接。浏览器会并行下载资源并且不会停止对当前页面的解析（渲染可能会暂停，因为浏览器需要样式规则来绘制和渲染页面）。这也是为什么建议使用link方式来加载css，而不是使用@import方式。常用的有link和a标签。

src：将资源嵌入到当前文档中元素定义的位置。在请求src资源时会将其指向的资源下载并应用到文档内，例如js脚本，img图片和frame等元素。当浏览器解析到该元素时，会暂停其他资源的下载和处理，直到将该资源加载、编译、执行完毕，类似于将所指向资源嵌入当前标签内。这也是为什么将js脚本放在底部而不是头部。

### 7. link和@import的区别

**1. 从属关系区别**
	`@import`是 CSS 提供的语法规则，只有导入样式表的作用；`link`是HTML提供的标签，不仅可以加载 CSS 文    	件，还可以定义 RSS、rel 连接属性等。	

**2. 加载顺序区别**
​	加载页面时，`link`标签引入的 CSS 被同时加载；`@import`引入的 CSS 将在页面加载完毕后被加载。

**3. 兼容性区别**
​	`@import`是 CSS2.1 才有的语法，故只可在 IE5+ 才能识别；`link`标签作为 HTML 元素，不存在兼容性问题。

**4. DOM可控性区别**
	可以通过 JS 操作 DOM ，插入`link`标签来改变样式；由于 DOM 方法是基于文档的，无法使用`@import` 的方	式插入样式。

**5. 权重区别**
​	`link`引入的样式权重大于`@import`引入的样式。

### 8. HTML5新特点

1. 语义化标签

   | **标签**  | 描述                              |
   | --------- | --------------------------------- |
   | <main>    | 用于指定文档的主体内容            |
   | <article> | 定义页面独立的内容区域。          |
   | <header>  | 定义了文档的头部区域              |
   | <nav>     | 定义导航链接的部分                |
   | <section> | 定义文档中的节（section、区段）   |
   | <aside>   | 定义页面的侧边栏内容。            |
   | <footer>  | 定义 section 或 document 的页脚。 |
   | <time>    | 定义日期或时间。                  |
   | <mark>    | 标记或突出显示文本                |

   对HTML语义化的理解

   ```
   用正确的标签做正确的事情。让页面的内容结构化，便于浏览器、搜索引擎解析;
   即使在没有样式CSS情况下也以一种文档格式显示，并且是容易阅读的;
   搜索引擎的爬虫也依赖于HTML标记来确定上下文和各个关键字的权重，利于SEO;
   使阅读源代码的人更容易将网站分块，便于阅读维护理解。
   ```
   
2. canvas绘图

3. draggable属性 可拖动 - draggable="true"

   拖动什么 - ondragstart 和 setData()

   ​	e.dataTransfer.setData() 方法设置被拖数据的数据类型和值

   ```js
   function drag(ev)
   {
   	ev.dataTransfer.setData("Text",ev.target.id);
   }
   ```

   放到何处 - ondragover

   ​	ondragover 事件规定在何处放置被拖动的数据。通过调用 ondragover 事件的 *event*.preventDefault() 方	法将数据/元素放置到其他元素中.

   ```js
   event.preventDefault()
   ```

   进行放置 - ondrop

   ​	当放置被拖数据时，会发生 drop 事件。

   ```js
   function drop(ev)
   {
     ev.preventDefault();
     var data=ev.dataTransfer.getData("Text");
     ev.target.appendChild(document.getElementById(data));
   }
   ```

   - 调用 preventDefault() 来避免浏览器对数据的默认处理（drop 事件的默认行为是以链接形式打开）
   - 通过 dataTransfer.getData("Text") 方法获得被拖的数据。该方法将返回在 setData() 方法中设置为相同类型的任何数据。
   - 把被拖元素追加到放置元素（目标元素）中

4. geolocationAPI 获取用户地理位置

   getCurrentPosition

5. audio/video 音频 视频元素

6. input类型增多，color、date、datetime、datetime-local、time、month、email、range、search、tel、url、week

7. 表单元素增强

   datalist 与input配合使用规定输入域的选项列表；

   keygen密钥;

   output定义不同类的输出。

8. Web存储，sessionStorge针对一个session进行数据存储，关闭浏览器窗口后清除，localStorage没有事件限制，不过它可能会因为本地时间修改失效。不过大量复杂数据结构一般用indexDB。

9. SSE server-sent-event 网页自动获取来自服务器的更新。用于接收服务器发送时间通知

10. WebSocket 在单个TCP连接上进行全双工通讯的协议。只需要握手一次，形成快速通道，传输数据。客户端和服务器可以直接通过TCP交换数据。获取连接之后，可以用send发送数据，用onmessage接收服务器返回的数据。

### 9. SEO

- 合理的`title`、`description`、`keywords`：

  搜索引擎对着三项的权重逐个减小，`title`值强调重点即可，不同页面`title`要有所不同；`description`把页面内容高度概括，长度合适，不同页面`description`有所不同；`keywords`列举出重要关键词即可

- 语义化的`HTML`代码，语义化代码让搜索引擎容易理解网页

- 非装饰性图片必须加`alt`

- 重要内容`HTML`代码放在最前：

  搜索引擎抓取`HTML`顺序是从上到下，有的搜索引擎对抓取长度有限制，保证重要内容一定会被抓取

- 重要内容不要用`js`输出：爬虫不会执行js获取内容

- 少用`iframe`：搜索引擎不会抓取`iframe`中的内容

### 10. cookie、session、localStorage、sessionStorage、token

#### cookie

因为HTTP协议是无状态的，即服务器不知道用户上一次做了什么，为了做到这点，Cookie和Session（session基于cookie）应运而生。Cookie 是服务器保存在浏览器的一小段文本信息，每个 Cookie 的大小一般不能超过4KB。浏览器每次向服务器发出请求，就会自动附上这段信息。服务器可以设置或读取Cookie中包含信息，借此维护用户跟服务器会话中的状态。

Cookie 主要用来分辨两个请求是否来自同一个浏览器，以及用来保存一些状态信息。它的常用场合有以下一些。

```
对话（session）管理：保存登录、购物车等需要记录的信息。
个性化：保存用户的偏好，比如网页的字体大小、背景色等等。
追踪：记录和分析用户行为。
```

缺点：

1. 容量很小（4KB）

2. 用户可以操作cookie，使功能受限，安全性较低

3. 有些状态不可能保存在客户端

4. 每次访问都要传送cookie给服务器，浪费宽带

5. cookie数据有路径（path）的概念，可以限制cookie只属于某个路径下。

   举例来说，用户访问网址www.example.com，服务器在浏览器写入一个 Cookie。这个 Cookie 就会包含www.example.com这个域名，以及根路径/。这意味着，这个 Cookie 对该域名的根路径和它的所有子路径都有效。如果路径设为/forums，那么这个 Cookie 只有在访问www.example.com/forums及其子路径时才有效。以后，浏览器一旦访问这个路径，浏览器就会附上这段 Cookie 发送给服务器。

浏览器的同源政策规定，两个网址只要域名相同和端口相同，就可以共享 Cookie。注意，这里不要求协议相同。也就是说，`http://example.com`设置的 Cookie，可以被`https://example.com`读取。

##### cookie的属性

**Expires、Max-Age：**

`Expires`属性指定一个具体的到期时间，到了指定时间以后，浏览器就不再保留这个 Cookie。它的值是 UTC 格式，可以使用`Date.prototype.toUTCString()`进行格式转换。

```
Set-Cookie: id=a3fWa; Expires=Wed, 21 Oct 2015 07:28:00 GMT;
```

如果不设置该属性，或者设为`null`，Cookie 只在当前会话（session）有效，浏览器窗口一旦关闭，当前 Session 结束，该 Cookie 就会被删除。另外，浏览器根据本地时间，决定 Cookie 是否过期，由于本地时间是不精确的，所以没有办法保证 Cookie 一定会在服务器指定的时间过期。

`Max-Age`属性指定从现在开始 Cookie 存在的秒数，比如`60 * 60 * 24 * 365`（即一年）。过了这个时间以后，浏览器就不再保留这个 Cookie。

如果同时指定了`Expires`和`Max-Age`，那么`Max-Age`的值将优先生效。

如果`Set-Cookie`字段没有指定`Expires`或`Max-Age`属性，那么这个 Cookie 就是 Session Cookie，即它只在本次对话存在，一旦用户关闭浏览器，浏览器就不会再保留这个 Cookie。

**Domain、Path、HostOnly：**

`Domain`属性指定浏览器发出 HTTP 请求时，哪些域名要附带这个 Cookie。如果没有指定该属性，浏览器会默认将其设为当前 URL 的一级域名，比如`www.example.com`会设为`example.com`，而且以后如果访问`example.com`的任何子域名，HTTP 请求也会带上这个 Cookie。如果服务器在`Set-Cookie`字段指定的域名，不属于当前域名，浏览器会拒绝这个 Cookie。

`Path`属性指定浏览器发出 HTTP 请求时，哪些路径要附带这个 Cookie。只要浏览器发现，`Path`属性是 HTTP 请求路径的开头一部分，就会在头信息里面带上这个 Cookie。比如，`PATH`属性是`/`，那么请求`/docs`路径也会包含该 Cookie。当然，前提是域名必须一致。

`host-only-flag`：在Cookie中不包含Domain属性，或者Domain属性为空，或者Domain属性不合法（不等于页面url中的Domain部分、也不是页面Domain的大域）时为true。此时，我们把这个Cookie称之为HostOnly Cookie；

如果host-only-flag为true，获取Cookie时，首先要检查Domain匹配性，只有当前域名与该Cookie的Domain属性完全相等才可以进入后续流程，其次才检查path、secure、httponly等属性的匹配性。host-only-flag为false时，符合域规则（domain-matches）的域名就可以获取到cookie。

举个例子，host-only-flag为true时，Domain属性为example.com的Cookie只有在example.com才有可能获取到；host-only-flag为false时，Domain属性为example.com的Cookie，在example.com、www.example.com、sub.example.com等等都可能获取到。

**Secure、HttpOnly、sameSite：**

`Secure`属性指定浏览器只有在 HTTPS 协议下，才能将这个 Cookie 发送到服务器。另一方面，如果当前协议是 HTTP，浏览器会自动忽略服务器发来的`Secure`属性。该属性只是一个开关，不需要指定值。如果通信是 HTTPS 协议，该开关自动打开。

`HttpOnly`属性指定该 Cookie 无法通过 JavaScript 脚本拿到，主要是`Document.cookie`属性、`XMLHttpRequest`对象和 Request API 都拿不到该属性。这样就防止了该 Cookie 被脚本读到，只有浏览器发出 HTTP 请求时，才会带上该 Cookie。

`sameSite`属性用来限制第三方Cookie，从而减少安全风险。它可以设置三个值

- Strict：最为严格，完全禁止第三方 Cookie，跨站点时，任何情况下都不会发送 Cookie。换言之，只有当前网页的 URL 与请求目标一致，才会带上 Cookie。
- Lax：稍稍放宽，大多数情况也是不发送第三方 Cookie，但是导航到目标网址的 Get 请求除外。
- None：Chrome 计划将`Lax`变为默认设置。这时，网站可以选择显式关闭`SameSite`属性，将其设为`None`。不过，前提是必须同时设置`Secure`属性（Cookie 只能通过 HTTPS 协议发送），否则无效。

----

#### session

Session代表服务器与浏览器的一次会话过程，Session是一种服务器端的机制，Session 对象用来存储特定用户会话所需的信息。Session由服务端生成，保存在服务器的内存、缓存、硬盘或数据库中。

##### 原理

session是基于cookie的，用户登录后服务器会为登录用户创建一个 session，**并把sessionid 保存在用户浏览器的 cookie 中**。当用户登录成功后，cookie 会随着后边的每个请求一起发送。这样，服务器通过 cookie 中的 sessionid 找到相对应的 session 数据，来验证用户身份，从而在响应中返回相应的状态。

##### session持久化

用于解决重启服务器后session就消失的问题。在数据库中存储session，而不是存储在内存中。

##### cookie和session的区别

1. 存放位置不同：
   Cookie保存在客户端，Session保存在服务端。
2. 存取方式的不同：
   Cookie中保存的是字符串，Session保存的是对象
3. 安全性（隐私策略）的不同 ：
   Cookie存储在浏览器中，对客户端是可见的，客户端的一些程序可能会窥探、复制以至修正Cookie中的内容。而Session存储在服务器上，对客户端是透明的，不存在敏感信息泄露的风险。 假如选用Cookie，比较好的方法是，敏感的信息如账号密码等尽量不要写到Cookie中。最好是像Google、Baidu那样将Cookie信息加密，提交到服务器后再进行解密。而假如选择Session就省事多了，反正是放在服务器上，Session里任何隐私都能够有效的保护。
4. 有效期上的不同：
   只需要设置Cookie的过期时间属性为一个很大很大的数字，Cookie就可以在浏览器保存很长时间。由于Session依赖于名为SESSIONID的Cookie，而Cookie SESSIONID的过期时间默认为–1，只需关闭了浏览器（一次会话结束），该Session就会失效。
5. 对服务器造成的压力不同 ：
   Cookie保管在客户端，不占用服务器资源。假如并发阅读的用户十分多，Cookie是很好的选择。Session是保管在服务器端的，每个用户都会产生一个Session。假如并发访问的用户十分多，会产生十分多的Session，耗费大量的内存。
6. 跨域支持上的不同 ：
   Cookie支持跨域名访问，例如将domain属性设置为“.baidu.com”，则以“.baidu.com”为后缀的一切域名均能够访问该Cookie。跨域名Cookie如今被普遍用在网络中。而Session则不会支持跨域名访问。Session仅在他所在的域名内有效。

---

### token

上面说到的Session和Cookie机制来保持会话，会存在一个问题：客户端浏览器只要保存自己的SessionID即可，而服务器却要保存所有用户的Session信息，这对于服务器来说开销较大，而且不利用服务器的扩展。它与 session 方式最大的不同是用户状态不存储在服务器端，而是存储在 token 中并保存在客户端的cookie、sessionStorage、localStorage，再次请求时**不一定默认携带**，需要给请求头中添加Authorization认证字段并携带token信息，服务器端就可以通过token确认用户登录状态。

##### 优点：

1. token可以抵抗csrf（跨域请求伪造），更安全，使用cookie在post请求的同时会自动添加到请求头上，token则不会自动添加到请求头中，

2. 攻击者也无法访问用户的token，无法形成攻击。
3. 每一次请求都需要携带 token，需要把 token 放到 HTTP 的 Authorization头信息字段中
4. 基于 token 的用户认证是一种服务端无状态的认证方式，服务端不用存放 token 数据。用解析 token 的计算时间换取session 的存储空间，从而减轻服务器的压力。

---

#### Web Storage

Web Storage存储机制是对HTML4中cookie存储机制的一个改善。由于cookie存储机制有很多缺点，HTML5不再使用它，转而使用改良后的Web Storage存储机制。Web Storage其实就是一个本地数据库，使用它可以在客户端本地建立一个数据库，原本必须保存在服务器端数据库中的内容现在可以直接保存在客户端本地了，这大大减轻了服务器端的负担，同时也加快了访问数据的速度。Web Storage存储数据大小一般都是：5MB

Web Storage又分为两种：

#### localStorage

将数据保存在客户端本地的硬件设备(通常指硬盘，也可以是其他硬件设备)中，即使浏览器被关闭了，该数据仍然存在，下次打开浏览器访问网站时仍然可以继续使用。

localStorage：常用于长期登录（+判断用户是否已登录），适合长期保存在本地的数据

#### sessionStorage

保存的数据用于浏览器的一次会话（session），当会话结束（通常是窗口关闭），数据被清空。

sessionStorage：敏感账号一次性登录

