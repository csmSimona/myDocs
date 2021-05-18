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

### 4、iframe

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

### 5、Doctype作用?严格模式与混杂模式如何区分？它们有何意义?

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

### 6、click在ios上有300ms延迟，原因及如何解决？

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

### 7、判断span的width和height

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

### 8、html元素层级

- 在html中，帧元素（frameset）的优先级最高，表单元素比非表单元素的优先级要高。 

  表单元素包括：文本输入框，密码输入框，单选框，复选框，文本输入域，列表框等等； 

  非表单元素包括：连接（a），div,table,span等。 

- 所有的html元素又可以根据其显示分成两类：有窗口元素以及无窗口元素。有窗口元素总是显示在无窗口元素的前面。 

  有窗口元素包括：select元素，object元素，以及frames元素等等。 

  无窗口元素：大部分html元素都是无窗口元素。

### 9、DHTML

- DHTML是Dynamic HTML的简称，就是动态的HTML(标准通用标记语言下的一个应用)，是相对传统的静态的htm而言的一种制作网页的概念。

- DHTML只是HTML、CSS和客户端脚本的一种集成，即一个页面中包括html+css+javascript(或其它客户端脚本）。

- html+css+javascript(或其他脚本）的优点：html确定页面框架，css和脚本决定页面样式、动态内容和动态定位。

### 10、块级元素、行内元素与行块级元素

1.常见的块级元素（自动换行，可设置高宽)有：
div，h1-h6，p，pre，ul，ol，li，form，table等。

2.常见的行内元素（无法自动换行，无法设置宽高）有：
a，img，span，i（斜体），em（强调），sub（下标），sup（上标），label等。

3.常见的行块级元素（拥有内在尺寸，可设置宽高，不会自动换行）有：
button，input，textarea，select等。

### 11、position: relative 不会使div脱离文档流，只是相对常规流偏移

所谓的文档流，指的是元素排版布局过程中，元素会自动从左往右，从上往下的流式排列。脱离文档流即是元素打乱了这个排列，或是从排版中拿走。
position:absolute;和position:fixed;会直接将元素从排版中拿走从而脱离文档流之外，设置float对象也会“打乱这个排列”从而也被称为脱离文档流。

### 12、手动写动画最小时间间隔为16.7ms

显示器默认频率60hz，时间为1/60hz=16.7ms

### 13、HTML5中，area, base, br, col, command, embed, hr, img, input, keygen, link, meta, param, source, track, wbr等空标签可以不用自闭合（/>）了

### 14、白屏时间first paint和可交互时间dom ready的关系

先触发first paint，后触发dom ready

页面的性能指标详解：

白屏时间（first paint time）：用户从打开页面开始到页面开始有东西呈现为止

首屏时间：用户浏览器首屏内所有内容都呈现出来所花费的时间

用户可操作时间（dom interactive）：用户可以进行正常的点击、输入等操作，默认可以统计dom ready的时间，因为通常会在这时候绑定事件操作

总下载时间：页面所有资源都加载完成并呈现出来所花的时间，即页面onload的时间

### 15、浏览器兼容性问题

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

### 16、浏览器渲染页面的过程

- 根据 HTML 结构生成 DOM 树

- 根据 CSS 生成 CSSOM

- 将 DOM 和 CSSOM 整合形成 RenderTree

- 根据 RenderTree 开始渲染和展示

- 遇到`<script>`时，会执行并阻塞渲染

在构建CSSOM树时，会阻塞渲染，直至CSSOM树构建完成。并且构建CSSOM树是一个十分消耗性能的过程，所以应该尽量保证层级扁平，减少过度层叠，越是具体的CSS选择器，执行速度越慢。

当HTML解析到script标签时，会暂停构建DOM，完成后才会从暂停的地方重新开始。也就是说，如果你想首屏渲染的越快，就越不应该在首屏就加载js文件。并且CSS也会影响js的执行，只有当解析完样式表才会执行js，所以也可以认为这种情况下，css也会暂停构建DOM。

### 17、对语义化的理解

1、去掉或者丢失样式的时候能够让页面呈现出清晰的结构

2、有利于SEO：和搜索引擎建立良好沟通，有助于爬虫抓取更多的有效信息：爬虫依赖于标签来确定上下文和各个关键字的权重；

3、方便其他设备解析（如屏幕阅读器、盲人阅读器、移动设备）以意义的方式来渲染网页；

4，便于团队开发和维护，语义化更具可读性，遵循W3C标准的团队都遵循这个标准，可以减少差异化。

### 18、XHTML与HTML的区别

1.所有的标记都必须要有一个相应的结束标记

2.所有标签的元素和属性的名字都必须使用小写

3.所有的XML标记都必须合理嵌套

4.所有的属性必须用引号""括起来

5.把所有<和&特殊符号用编码表示

6.给所有属性赋一个值

7.不要在注释内容中使“--”

8.图片必须有说明文字

### 19、优雅降级和渐进增强

优雅降级：Web站点在所有新式浏览器中都能正常工作，如果用户使用的是老式浏览器，则代码会检查以确认它们是否能正常工作。由于IE独特的盒模型布局问题，针对不同版本的IE的hack实践过优雅降级了,为那些无法支持功能的浏览器增加候选方案，使之在旧式浏览器上以某种形式降级体验却不至于完全失效.

渐进增强：从被所有浏览器支持的基本功能开始，逐步地添加那些只有新式浏览器才支持的功能,向页面增加无害于基础浏览器的额外样式和功能的。当浏览器支持时，它们会自动地呈现出来并发挥作用。

### 20、clientHeight，scrollHeight，offsetHeight 以及scrollTop，offsetTop，clientTop

clientHeight：表示的是可视区域的高度，不包含border和滚动条

offsetHeight：表示可视区域的高度，包含了border和滚动条

scrollHeight：表示了所有区域的高度，包含了因为滚动被隐藏的部分。

clientTop：表示边框border的厚度，在未指定的情况下一般为0

scrollTop：滚动后被隐藏的高度，获取对象相对于由offsetParent属性指定的父坐标(css定位的元素或body元素)距离顶端的高度。

offsetTop：子元素的外边框到父元素的内边框的垂直距离 （没边框时自然就是content到content的距离）

### 21、重绘（repaint）和重排（reflow）

**1.简述重排的概念**

重排是DOM元素的几何属性变化，**DOM树的结构变化**（元素大小、定位等），渲染树需要重新计算。

**2.简述重绘的概念**

重绘是一个元素外观的改变所触发的浏览器行为，例如改变visibility、outline、背景色等属性。**浏览器会根据元素的新属性重新绘制，使元素呈现新的外观**。

**3.简述重绘和重排的关系**

重绘不会引起重排，但重排一定会引起重绘，一个元素的重排通常会带来一系列的反应，甚至触发整个文档的重排和重绘，性能代价是高昂的。

**4.什么情况下会触发重排？**

(1) 页面渲染初始化时；（这个无法避免）

(2) 浏览器窗口改变尺寸；

(3) 元素字体大小变化；

(4) 元素位置改变时；

(5) 元素内容改变时；

(6) 添加或删除可见的DOM 元素时。

**5.性能优化（减少重排）**

1. 减少DOM访问，将多次改变样式属性操作合并成一次操作

2. 如果需要批量操作DOM，可以先让元素脱离文档流，操作完后再带入文档流，这样只会触发一次重排（fragment元素的应用）

3. 将需要多次重排的元素，position属性设为absolute或fixed，这样此元素就脱离了文档流，它的变化不会影响到其他元素。例如有动画效果的元素就最好设置为绝对定位。

4. 由于display: none的元素不再渲染树中，对隐藏的元素操作不会引起其他元素的重排。如果要对一个元素进行复杂的操作时，可以先隐藏它，操作完成后再显示。这样只在隐藏和显示时触发两次重排。

5. 避免设置大量的style属性，因为通过设置style属性改变节点样式的话，每一次设置都会触发一次reflow，所以最好是使用class属性

6. 不要使用table布局，因为table布局中某个元素出发了重排，那么整个table的元素都会触发重排。

### 