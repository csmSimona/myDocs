## HTML小记（持续更新）

### 1、HTML5中的新特性

1.图像 canvas

2.多媒体 video，audio

3.本地存储 localStorage、sessionStorage

4.语义化更好的内容元素 article、header、footer、nav、section

5.表单控件 date、time、canlendar、url、search

6.新的技术 webworker、websocket、Geolocation

移除的元素

1.纯表现的元素 u、big、center、strike、tt、font、basefont

2.框架集 frame、frameset、noframes 

### 2、什么是SVG? 

SVG 指可伸缩矢量图形 (Scalable Vector Graphics)

SVG 用来定义用于网络的基于矢量的图形

SVG 使用 XML 格式定义图形

SVG 图像在放大或改变尺寸的情况下其图形质量不会有所损失

SVG 是万维网联盟的标准

SVG 与诸如 DOM 和 XSL 之类的 W3C 标准是一个整体

SVG是HTML下的一个分支

### 3、说一下web Quality（无障碍）

能够被残障人士使用的网站才能称得上一个易用的（易访问的）网站。

残障人士指的是那些带有残疾或者身体不健康的用户。

使用alt属性：

`<img src="person.jpg"  alt="this is a person"/>`

- 有时候浏览器会无法显示图像。具体的原因有：

- 用户关闭了图像显示

- 浏览器是不支持图形显示的迷你浏览器

- 浏览器是语音浏览器（供盲人和弱视人群使用）

如果您使用了alt 属性，那么浏览器至少可以显示或读出有关图像的描述。

### 4、BOM属性对象方法

(突然发现这个应该放在JavaScript小记里面)

什么是BOM?  BOM（Browser Object Model）浏览器对象模型，是Javascript的重要组成部分。它提供了一系列对象用于与浏览器窗口进行交互，这些对象通常统称为BOM。 

有哪些常用的BOM属性呢？![](..\picture\bom.png)

**(1) location对象**

location.href-- 返回或设置当前文档的URL

location.search -- 返回URL中的查询字符串部分。例如 <http://www.dreamdu.com/dreamdu.php?id=5&name=dreamdu> 返回包括(?)后面的内容?id=5&name=dreamdu

location.hash -- 返回URL#后面的内容，如果没有#，返回空

location.host -- 返回URL中的域名部分，例如www.dreamdu.com

location.hostname -- 返回URL中的主域名部分，例如dreamdu.com

location.pathname -- 返回URL的域名后的部分。例如 <http://www.dreamdu.com/xhtml/> 返回/xhtml/

location.port -- 返回URL中的端口部分。例如 <http://www.dreamdu.com:8080/xhtml/> 返回8080

location.protocol -- 返回URL中的协议部分。例如 <http://www.dreamdu.com:8080/xhtml/> 返回(//)前面的内容

http:

location.assign -- 设置当前文档的URL

location.replace(url) -- 设置当前文档的URL，并且在history对象的地址列表中移除这个URL

location.reload() -- 重载当前页面

**(2) history对象**

history.go() -- 前进或后退指定的页面数 history.go(num);

history.back() -- 后退一页

history.forward() -- 前进一页

**(3) Navigator对象**

navigator.userAgent -- 返回用户代理头的字符串表示(就是包括浏览器版本信息等的字符串)

navigator.cookieEnabled -- 返回浏览器是否支持(启用)cookie

### 5、iframe

定义：iframe元素会创建包含另一个文档的内联框架

提示：可以将提示文字放在`<iframe></iframe>`之间，来提示某些不支持iframe的浏览器

优点

- 解决加载缓慢的第三方内容如图标和广告等的加载问题

- Security sandbox

- 并行加载脚本

缺点

- 会阻塞主页面的onload事件

- 搜索引擎无法解读这种页面，不利于SEO

- iframe和主页面共享连接池，而浏览器对相同区域有限制所以会影响性能。

- 没有语义

使用场景

- 与第三方域名下的页面共享cookie

- 上传图片，避免当前页刷新

- 左边固定右边自适应的布局

- 资源加载

### 6、Doctype作用?严格模式与混杂模式如何区分？它们有何意义?

转载：[Doctype作用？严格模式与混杂模式如何区分？它们有何差异？](https://www.cnblogs.com/wuqiutong/p/5986191.html)

Doctype声明于文档最前面，告诉浏览器以何种方式来渲染页面，这里有两种模式，严格模式和混杂模式。

**严格模式：**又称标准模式，是指浏览器按照 W3C 标准解析代码。严格模式的排版和JS运作模式是以该浏览器支持的最高标准运行。

**混杂模式：**又称怪异模式或兼容模式，是指浏览器用自己的方式解析代码。向后兼容，模拟老式浏览器，防止浏览器无法兼容页面。

**严格模式与混杂模式的语句解析不同点有哪些？**

1）盒模型的高宽包含内边距padding和边框border

![img](http://img.blog.csdn.net/20130912194842984?watermark/2/text/aHR0cDovL2Jsb2cuY3Nkbi5uZXQvZnJlc2hsb3Zlcg==/font/5a6L5L2T/fontsize/400/fill/I0JBQkFCMA==/dissolve/70/gravity/SouthEast)

 

​    在W3C标准中，如果设置一个元素的宽度和高度，指的是元素内容的宽度和高度，而在IE5.5及以下的浏览器及其他版本的Quirks模式下，IE的宽度和高度还包含了padding和border。

2）可以设置行内元素的高宽

​    在Standards模式下，给span等行内元素设置wdith和height都不会生效，而在quirks模式下，则会生效。

3）可设置百分比的高度

​        在standards模式下，一个元素的高度是由其包含的内容来决定的，如果父元素没有设置高度，子元素设置一个百分比的高度是无效的。

​        当你让一个元素的高度设定为百分比高度时，是相对于父元素的高度根据百分比来计算高度。当没有给父元素设置高度（height）时或设置的高度值百分比不生效时，浏览器会根据其子元素来确定父元素的高度，所以当无法根据获取父元素的高度，也就无法计算自己高度。 换句话说，父元素的高度只是一个缺省值：height: auto;。当你要求浏览器根据这样一个缺省值来计算百分比高度时，只能得到undefined的结果，也就是一个null值，浏览器不会对这个值有任何的反应。

4）用margin:0 auto设置水平居中在IE下会失效

​        使用margin:0 auto在standards模式下可以使元素水平居中，但在quirks模式下却会失效,quirk模式下的解决办法，用text-align属性:

   body{text-align:center};#content{text-align:left}

5）quirk模式下设置图片的padding会失效

6）quirk模式下table中的字体属性不能继承上层的设置

7）quirk模式下white-space:pre（保留空白）会失效

### 7、click在ios上有300ms延迟，原因及如何解决？

转载自[移动端click事件延迟300ms到底是怎么回事，该如何解决？](https://www.cnblogs.com/zhaodahai/p/6831165.html)

这要追溯至 2007 年初。苹果公司在发布首款 iPhone 前夕，遇到一个问题：当时的网站都是为大屏幕设备所设计的。于是苹果的工程师们做了一些约定，应对 iPhone 这种小屏幕浏览桌面端站点的问题。

这当中最出名的，当属双击缩放(double tap to zoom)，这也是会有上述 300 毫秒延迟的主要原因。双击缩放，顾名思义，即用手指在屏幕上快速点击两次，iOS 自带的 Safari 浏览器会将网页缩放至原始比例。

那么这和 300 毫秒延迟有什么联系呢？

假定这么一个场景。用户在 iOS Safari 里边点击了一个链接。由于用户可以进行双击缩放或者双击滚动的操作，当用户一次点击屏幕之后，浏览器并不能立刻判断用户是确实要打开这个链接，还是想要进行双击操作。因此，iOS Safari 就等待 300 毫秒，以判断用户是否再次点击了屏幕。

鉴于iPhone的成功，其他移动浏览器都复制了 iPhone Safari 浏览器的多数约定，包括双击缩放，几乎现在所有的移动端浏览器都有这个功能。之前人们刚刚接触移动端的页面，在欣喜的时候往往不会care这个300ms的延时问题，可是如今touch端界面如雨后春笋，用户对体验的要求也更高，这300ms带来的卡顿慢慢变得让人难以接受。 

(1)粗暴型，禁用缩放

`<meta name="viewport" content="width=device-width, user-scalable=no">`


(2)利用FastClick，其原理是：

检测到touched事件后，立刻出发模拟click事件，并且把浏览器300毫秒之后真正触发的事件给阻断掉

### 8、前端性能优化

**1、采用 lazyLoad**

俗称懒加载，可以控制网页上的内容在一开始无需加载，不需要发请求，等到用户操作真正需要的时候立即加载出内容。这样就控制了网页资源一次性请求数量。

**2、控制资源文件加载优先级**

浏览器在加载HTML内容时，是将HTML内容从上至下依次解析，解析到link或者script标签就会加载href或者src对应链接内容，为了第一时间展示页面给用户，就需要将CSS提前加载，不要受 JS 加载影响。

一般情况下都是CSS在头部，JS在底部。

**3、利用浏览器缓存**

浏览器缓存是将网络资源存储在本地，等待下次请求该资源时，如果资源已经存在就不需要到服务器重新请求该资源，直接在本地读取该资源。

**4、减少重排（Reflow）**

基本原理：重排是DOM的变化影响到了元素的几何属性（宽和高），浏览器会重新计算元素的几何属性，会使渲染树中受到影响的部分失效，浏览器会验证 DOM 树上的所有其它结点的visibility属性，这也是Reflow低效的原因。如果Reflow的过于频繁，CPU使用率就会急剧上升。

减少Reflow，如果需要在DOM操作时添加样式，尽量使用 增加class属性，而不是通过style操作样式。

**5、减少 DOM 操作**

[JS对DOM的操作优化法则](https://www.cnblogs.com/nightstarsky/p/5853978.html)

1.批量读写
当我们需要获取某一属性，这一属性需要计算才能得到，并且队列中存在尚未提交的DOM修改操作，则此时，DOM修改操作的队列将会被提交。
为了提高效率，减少更新render tree的次数，可以先统一读取属性，然后统一修改DOM，这样，就可以减少更新render tree的次数。

2.虚拟结点
当我们需要对DOM做出大量修改时，可以先创建一个虚拟结点，将所有修改附加在该节点，最后将该虚拟节点一次性提交给在render tree上存在的结点，则相当于只提交了一次修改操作。

3.查找元素的优化
因为ID是唯一的，也有原始的方法，因此使用ID查找元素是最快的，其次的是根据类和类型查找元素，通过属性查找元素是最慢的，因此应该尽可能的通过ID或者类来查找元素，避免通过类来查找元素。

**6、图标使用 IconFont 替换**

**7、DNS预解析**

DNS解析也是需要时间的，可以通过与解析的方式来预先获得域名所对应的IP

`<link rel="dns-prefetch" href="//yuchengkai.cn">`

**8、图片加载优化**

- 不用图片。很多时候会使用到很多修饰类图片，其实这类修饰图片完全可以用CSS去代替

- 一般图片都用CDN加载，可以计算出适配屏幕的宽度，然后去请求相应裁剪好的图片

  > CDN图片加速服务是指CDN网络和客户源文件服务器形成良好的互动，即将源站的图片、flash动画、css / js、及各种文件类型的图片缓存于CDN中心网络中，这些文件的特点在于更新的频率较低，用缓存技术将文件cache在CDN的边缘节点上，即可满足终端用户就近访问的需求。文件可以通过定期和不定期的方式在CDN节点上进行更新：定期更新时CDN中心网络主动更新源站数据，再通过智能解析系统将内容进行优化分配到各CDN网络节点；不定期更新可以通过CDN客服管理系统进行主动推送完成。
  >
  > CDN图片加速服务是当前CDN服务的基本应用，也是使用最为广泛的服务。例如在线商城，图片站，图库，地图导航，新闻资讯，行业门户等，为了提高图片在客户端的加载速度，都会使用CDN图片加速服务。

- 小图使用base64格式

- CSS Sprites，将多个图标文件整合到一张图片中（雪碧图/精灵图）

- 选择正确的图片格式：
  - 对于能够显示WebP格式的浏览器尽量使用WebP格式。因为WebP格式具有更好的图象数据压缩算法，能带来更小的图片体积，而且拥有肉眼识别无差异的图象质量，缺点就是兼容性并不好
  
  - 小图使用PNG，其实对于大部分图标这类图片，完全可以用SVG代替

  - 照片使用JPEG

**9、使用Webpack优化项目**

- 对于Webpack4，打包项目使用production模式，这样会自动开启代码压缩

- 使用ES6模块来开启tree shaking，这个技术可以移除没有使用的代码

- 优化照片，对于小图可以使用base64的方式写入文件中

- 按照路由拆分代码，实现按需加载

- 给打包出来的文件名添加哈希，实现浏览器缓存文件

### 9、事件对象

**DOM中的事件对象**：(符合W3C标准）

preventDefault()：取消事件默认行为

stoplmmediatePropagation()：取消事件冒泡同时阻止当前节点上的事件处理程序被调用。

stopPropagation()：取消事件冒泡对当前节点无影响。

**IE中的事件对象**：

returnValue()：取消事件默认行为

cancelBubble()：取消事件冒泡

### 10、DHTML

- DHTML是Dynamic HTML的简称，就是动态的HTML(标准通用标记语言下的一个应用)，是相对传统的静态的htm而言的一种制作网页的概念。

- DHTML只是HTML、CSS和客户端脚本的一种集成，即一个页面中包括html+css+javascript(或其它客户端脚本）。

- html+css+javascript(或其他脚本）的优点：html确定页面框架，css和脚本决定页面样式、动态内容和动态定位。

### 11、Node节点

这是一张优秀的思维导图：[JavaScript Node节点类型](https://www.processon.com/view/5cc00e24e4b085d010837583#map)

#### 节点属性

1、nodeType：节点类型

- **Node.ELEMENT_NODE(1)；（元素节点）**

- **Node.ATTRIBUTE_NODE(2)；（属性节点）**

- **Node.TEXT_NODE(3)；（文本节点）**

- Node.CDATA_SECTION_NODE(4)；

- Node.ENTITY_REFERENCE_NODE(5)；

- Node.ENTITY_NODE(6)；

- Node.PROCESSING_INSTRUCTION_NODE(7)；

- **Node.COMMENT_NODE(8)；（注释节点）**

- **Node.DOCUMENT_NODE(9)；（document节点）**

- Node.DOCUMENT_TYPE_NODE(10)；

- Node.DOCUMENT_FRAGMENT_NODE(11)；

- Node.NOTATION_NODE(12)

2、nodeName：节点名称。元素节点为标签名，文本节点为#text

3、nodeValue：节点值。元素节点为null，文本节点为文本内容

#### 节点关系

1、childNodes：当前节点的子节点的节点列表

2、parentNode：当前节点的父节点

3、firstChild：父节点的第一节点。相当于childNodes[0]或childNodes.item[0]

4、lastChild：父节点的最后一个节点

5、nextSibling：当前节点的后一个节点

6、previousSibling：当前节点的前一个节点

7、hasChildNodes：节点包含一或多个子节点的情况下返回true

8、ownerDocument：指向表示整个文档的文档节点

#### 节点操作

1、createElement()：创建元素节点

2、createAttribute()：创建属性节点

3、appendChild()：向节点的子节点列表的结尾添加新的子节点

4、cloneNode()：复制节点

5、insertBefore(newNode，target)：在指定的子节点前插入新的子节点

6、replaceChild(newNode，target)：用新节点替换一个子节点

7、removeChild()：删除（并返回）当前节点的指定子节点

8、normalize()：将空文本节点删除或将相邻的文本节点合并一个文本节点

9、getAttribute()：返回指定属性值

10、setAttribute()：把指定属性设置或修改为指定的值

11、querySelectorAll()：返回文档中匹配指定css选择器的所有元素，返回NodeList对象（集合）

### 12、mouseover和mouseenter两个事件的区别

mouseover(鼠标覆盖)：不论鼠标指针穿过被选元素或其子元素，都会触发 mouseover 事件。

mouseenter(鼠标进入)：只有在鼠标指针穿过被选元素时，才会触发 mouseenter 事件。

二者的本质区别在于,mouseenter不会冒泡,简单的说,它不会被它本身的子元素的状态影响到.但是mouseover就会被它的子元素影响到,在触发子元素的时候,mouseover会冒泡触发它的父元素.(想要阻止mouseover的冒泡事件就用mouseenter)

### 13、块级元素、行内元素与行块级元素

1.常见的块级元素（自动换行，可设置高宽)有：
div，h1-h6，p，pre，ul，ol，li，form，table等。

2.常见的行内元素（无法自动换行，无法设置宽高）有：
a，img，span，i（斜体），em（强调），sub（下标），sup（上标），label等。

3.常见的行块级元素（拥有内在尺寸，可设置宽高，不会自动换行）有：
button，input，textarea，select等。

### 14、position: relative 不会使div脱离文档流，只是相对常规流偏移

所谓的文档流，指的是元素排版布局过程中，元素会自动从左往右，从上往下的流式排列。脱离文档流即是元素打乱了这个排列，或是从排版中拿走。
position:absolute;和position:fixed;会直接将元素从排版中拿走从而脱离文档流之外，设置float对象也会“打乱这个排列”从而也被称为脱离文档流。

### 15、手动写动画最小时间间隔为16.7ms

显示器默认频率60hz，时间为1/60hz=16.7ms

### 16、HTML5中，area, base, br, col, command, embed, hr, img, input, keygen, link, meta, param, source, track, wbr等空标签可以不用自闭合（/>）了

### 17、html元素层级

- 在html中，帧元素（frameset）的优先级最高，表单元素比非表单元素的优先级要高。 

  表单元素包括：文本输入框，密码输入框，单选框，复选框，文本输入域，列表框等等； 

  非表单元素包括：连接（a），div,table,span等。 

- 所有的html元素又可以根据其显示分成两类：有窗口元素以及无窗口元素。有窗口元素总是显示在无窗口元素的前面。 

  有窗口元素包括：select元素，object元素，以及frames元素等等。 

  无窗口元素：大部分html元素都是无窗口元素。

### 18、白屏时间first paint和可交互时间dom ready的关系

先触发first paint，后触发dom ready

页面的性能指标详解：

白屏时间（first paint time）：用户从打开页面开始到页面开始有东西呈现为止

首屏时间：用户浏览器首屏内所有内容都呈现出来所花费的时间

用户可操作时间（dom interactive）：用户可以进行正常的点击、输入等操作，默认可以统计dom ready的时间，因为通常会在这时候绑定事件操作

总下载时间：页面所有资源都加载完成并呈现出来所花的时间，即页面onload的时间

### 19、判断span的width和height

```html
<div style="width: 400px; height: 200px;">
	<span style="float: left; width: auto; height: 100%">
        <i style="position:absolute; float: left; width: 100px; height: 50px;">hello</i>
    </span>
</div>
```

span不是块级元素，是不支持行高的，但是style中有了个`float: left;`就使得span变成了块级元素支持宽高，`height: 100%;`即为，200，宽度由内容撑开。

但是内容中的i是绝对定位，脱离了文档流，所以不占父级空间，所以span的width = 0

所以，width = 0px，height = 200px

### 20、事件触发三个阶段

- 事件捕获阶段：事件从最不精确的对象(document对象)开始触发，然后到最精确
- 处于目标阶段
- 事件冒泡阶段：事件按照从最特定的事件目标到最不特定的事件目标(document对象)的顺序触发。不是所有事件都能冒泡。以下事件不冒泡：blur、focus、load、unload（关闭页面）

事件触发一般来说会按照上面的顺序进行，但是也有特例，如果给一个目标节点同时注册冒泡和捕获事件，事件触发会按照注册的顺序执行。

```js
// 以下会先打印冒泡然后是捕获
node.addEventListener('click', (event) => {
    console.log('冒泡');
}, false);
node.addEventListener('click', (event) => {
    console.log('捕获');
}, true);
```

通常我们使用addEventListener注册事件，该函数的第三个参数可以是布尔值，也可以是对象。对于布尔值useCapture参数来说，该参数默认值为false。useCapture决定了注册的事件是捕获事件（false）还是冒泡事件（true）。

一般来说，我们只希望事件只触发在目标上，这时候可以使用stopPropagation来阻止事件的进一步传播。通常我们认为stopPropagation是用来阻止事件冒泡的，其实该函数也可以阻止捕获事件。stopImmediatePropagation同样也能实现阻止事件，但是还能阻止该事件目标执行别的注册事件。

### 21、浏览器兼容性问题

参考：[前端常见的浏览器兼容性问题及解决方案](https://blog.csdn.net/wanmeiyinyue315/article/details/79654984)

1、不同浏览器的标签默认的外补丁( margin )和内补丁(padding)不同
解决方案： css 里增加通配符 * { margin: 0; padding: 0; }

2、IE6双边距问题；在 IE6中设置了float , 同时又设置margin , 就会出现边距问题
解决方案：设置display:inline;

3、当标签的高度设置小于10px，在IE6、IE7中会超出自己设置的高度
解决方案：超出高度的标签设置overflow:hidden,或者设置line-height的值小于你的设置高度

4、图片默认有间距
解决方案：使用float 为img 布局

5、IE9一下浏览器不能使用opacity
解决方案：
opacity: 0.5;

filter: alpha(opacity = 50);

filter: progid:DXImageTransform.Microsoft.Alpha(style = 0, opacity = 50);（ie提供的css渲染）

6、边距重叠问题；当相邻两个元素都设置了margin 边距时，margin 将取最大值，舍弃最小值；
解决方案：为了不让边重叠，可以给子元素增加一个父级元素，并设置父级元素为overflow:hidden；

7、cursor:hand 显示手型在safari 上不支持
解决方案：统一使用 cursor:pointer

8、两个块级元素，父元素设置了overflow:auto；子元素设置了position:relative ;且高度大于父元素，在IE6、IE7会被隐藏而不是溢出；
解决方案：父级元素设置position:relative

### 22、浏览器渲染页面的过程

1、根据HTML结构生成DOM树

2、根据CSS生成CSSOM树

3、将DOM和CSSOM整合形成RenderTree（渲染树）

4、根据渲染树来布局，计算每个节点的位置

5、调用GPU绘制，合成图层，显示在屏幕上

在构建CSSOM树时，会阻塞渲染，直至CSSOM树构建完成。并且构建CSSOM树是一个十分消耗性能的过程，所以应该尽量保证层级扁平，减少过度层叠，越是具体的CSS选择器，执行速度越慢。

当HTML解析到script标签时，会暂停构建DOM，完成后才会从暂停的地方重新开始。也就是说，如果你想首屏渲染的越快，就越不应该在首屏就加载js文件。并且CSS也会影响js的执行，只有当解析完样式表才会执行js，所以也可以认为这种情况下，css也会暂停构建DOM。

### 23、对语义化的理解

1、去掉或者丢失样式的时候能够让页面呈现出清晰的结构

2、有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；

3、方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；

4，便于团队开发和维护，语义化更具可读性，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

### 24、XHTML与HTML的区别

1.所有的标记都必须要有一个相应的结束标记

2.所有标签的元素和属性的名字都必须使用小写

3.所有的XML标记都必须合理嵌套

4.所有的属性必须用引号""括起来

5.把所有<和&特殊符号用编码表示

6.给所有属性赋一个值

7.不要在注释内容中使“--”

8.图片必须有说明文字