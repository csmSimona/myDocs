## CSS小记

[CSS实现多种常见布局](https://www.cnblogs.com/longlongdan/p/10532891.html)

部分参考[1.5 万字 CSS 基础拾遗（核心知识、常见需求）](https://juejin.cn/post/6941206439624966152)



### 1、@规则

- `@namespace`，告诉 CSS 引擎必须考虑XML命名空间。
- `@media`，如果满足媒体查询的条件则条件规则组里的规则生效。
- `@page`, 描述打印文档时布局的变化.
- `@font-face`，描述将下载的外部的字体。
- `@keyframes`，描述 CSS 动画的关键帧。
- `@document`，如果文档样式表满足给定条件则条件规则组里的规则生效。 (推延至 CSS Level 4 规范)
- `@charset`，用于定义样式表使用的字符集。默认是 `UTF-8`

- `@import`，用于告诉 CSS 引擎引入一个外部样式表。

- `@supports`，用于查询特定的 CSS 是否生效，可以结合 not、and 和 or 操作符进行后续的操作。

  ```css
  /* 如果支持自定义属性，则把 body 颜色设置为变量 varName 指定的颜色 */
  @supports (--foo: green) {
      body {
          color: var(--varName);
      }
  }
  ```

  

### 2、link和@import的区别

- link 导入的样式会在页面加载时同时加载，@import 导入的样式需等页面加载完成后再加载


- link 没有兼容性问题，而@import是css2里面的，所以IE5以上才能识别


- link 可以通过 JS 操作 DOM 动态引入样式表改变样式，而@import不可以


- link 是 HTML 标签，除了能导入 CSS 外，还能导入别的资源，比如图片、脚本和字体等；而 @import 是 CSS 的语法，只能用来导入 CSS；


- link方式样式的权重高于@import的




### 3、选择器

#### 基础选择器

- 标签选择器：`h1`
- 类选择器：`.checked`
- ID 选择器：`#picker`
- 通配选择器：`*`

#### 属性选择器

- `[attr]`：指定属性的元素；
- `[attr=val]`：属性等于指定值的元素；
- `[attr*=val]`：属性包含指定值的元素；
- `[attr^=val]`	：属性以指定值开头的元素；
- `[attr$=val]`：属性以指定值结尾的元素；
- `[attr~=val]`：属性包含指定值(完整单词)的元素(不推荐使用)；
- `[attr|=val]`：属性以指定值(完整单词)开头的元素(不推荐使用)；

#### 组合选择器

- 相邻兄弟选择器：`A + B`
- 普通兄弟选择器：`A ~ B`
- 子选择器：`A > B`
- 后代选择器：`A B`

#### 伪类

**条件伪类**

- `:lang()`：基于元素语言来匹配页面元素；
- `:dir()`：匹配特定文字书写方向的元素；
- `:has()`：匹配包含指定元素的元素；
- `:is()`：匹配指定选择器列表里的元素；
- `:not()`：用来匹配不符合一组选择器的元素；

**行为伪类**

- `:active`：鼠标激活的元素；
- `:hover`：	鼠标悬浮的元素；
- `::selection`：鼠标选中的元素；

**状态伪类**

- `:target`：当前锚点的元素；
- `:link`：未访问的链接元素；
- `:visited`：已访问的链接元素；
- `:focus`：输入聚焦的表单元素；
- `:required`：输入必填的表单元素；
- `:valid`：输入合法的表单元素；
- `:invalid`：输入非法的表单元素；
- `:in-range`：输入范围以内的表单元素；
- `:out-of-range`：输入范围以外的表单元素；
- `:checked`：选项选中的表单元素；
- `:optional`：选项可选的表单元素；
- `:enabled`：事件启用的表单元素；
- `:disabled`：事件禁用的表单元素；
- `:read-only`：只读的表单元素；
- `:read-write`：可读可写的表单元素；
- `:blank`：输入为空的表单元素；
- `:current()`：浏览中的元素；
- `:past()`：已浏览的元素；
- `:future()`：未浏览的元素；

**结构伪类**

- `:root`：文档的根元素；
- `:empty`：无子元素的元素；
- `:first-letter`：元素的首字母；
- `:first-line`：元素的首行；
- `:nth-child(n)`：元素中指定顺序索引的元素；
- `:nth-last-child(n)`：元素中指定逆序索引的元素；；
- `:first-child	`：元素中为首的元素；
- `:last-child`	：元素中为尾的元素；
- `:only-child`：父元素仅有该元素的元素；
- `:nth-of-type(n)	`：标签中指定顺序索引的标签；
- `:nth-last-of-type(n)`：标签中指定逆序索引的标签；
- `:first-of-type`	：标签中为首的标签；
- `:last-of-type`：标签中为尾标签；
- `:only-of-type`：父元素仅有该标签的标签；

#### 伪元素

- `::before`：在元素前插入内容；
- `::after`：在元素后插入内容；



### 3、& 的作用

```css
ul{
	margin-bottom: 20px;
	& > li{
		margin-bottom: 0;
	}
}
//相当于
ul {
	margin-bottom: 20px;
}
ul > li{
	margin-bottom: 0;
}
```

- “&”表示嵌套的上一级，是sass语法，代表上一级选择器
- “>”是特有的选择器，A>B 表示选择A元素的所有子B元素。
  与A B的区别在于，A B选择所有后代元素，而A>B只选择一代。



### 4、`a:link`,`a:visited`,`a:hover`,`a:active` 顺序

**L（link）V（visited）H（hover）A（active）**

1. link:连接平常的状态
2. visited:连接被访问过之后
3. hover:鼠标放到连接上的时候
4. active:连接被按下的时候



### 5、CSS优先级由高到低：

1.在属性后面使用!important会覆盖页面内任何位置定义的元素样式。

2.内联样式：作为style属性写在元素内的样式

3.ID选择器

4.类选择器、伪类选择器、属性选择器（后面的样式会覆盖前面的样式）

5.元素选择器、伪元素选择器

6.通配符选择器、后代选择器、兄弟选择器

7.浏览器自定义的样式



### 6、css可继承属性：

所有元素可继承：visibility和cursor。

内联元素可继承：letter-spacing、word-spacing、white-space、line-height、color、font、font-
family、font-size、font-style、font-variant、font-weight、text-decoration、text-transform、
direction。

终端块状元素可继承：text-indent和text-align。

列表元素可继承：list-style、list-style-type、list-style-position、list-style-image。



### 7、CSS盒模型

CSS中的盒子模型包括IE盒子模型和标准的W3C盒子模型。

这两种盒子模型最主要的区别就是width的包含范围：

- 标准盒模型的盒子总宽度：左右border+左右padding+width


- IE盒模型的盒子总宽度：width（即IE的内容宽度还包含了padding和border）


在CSS3中引入了box-sizing属性

`box-sizing: content-box;`  表示标准的盒子模型

`box-sizing: border-box;`  表示的是IE盒子模型



### 8、dispaly type

#### `display: inline`

- 内联元素，不会占满一行，宽度随着内容而变化；多个 inline 元素将按照从左到右的顺序在一行里排列显示，如果一行显示不下，则自动换行；
- 设置 width/height 将不会生效；
- 设置竖直方向上的 padding 和 margin 将不会生效；

#### `display: block`

- 块级元素，占满一行，默认继承父元素的宽度；多个块元素将从上到下进行排列；
- 设置 width/height 将会生效；
- 设置 padding 和 margin 将会生效；

#### `display: inline-block`

- 使元素以块级元素的形式呈现在行内。既具有宽度高度特性，又具有同行特性。不单独占满一行，可以看成是能够在一行里进行左右排列的块元素；
- 设置 width/height 将会生效；
- 设置 padding 和 margin 将会生效；



### 9、格式化上下文

格式上下文(formatting context)是个布局环境，不同的布局环境定有不同的布局规则，而处在什么布局环境里的元素（盒子），就得遵守什么环境的布局规则。

不同类型的盒子有不同格式化上下文，大概有这 4 类：

- BFC (Block Formatting Context) 块级格式化上下文；
- IFC (Inline Formatting Context) 行内格式化上下文；
- FFC (Flex Formatting Context) 弹性格式化上下文；
- GFC (Grid Formatting Context) 格栅格式化上下文；

#### BFC

**块格式化上下文**，它是一个独立的渲染区域，只有块级盒子参与，它规定了内部的块级盒子如何布局，并且与这个区域外部毫不相干。

具有BFC特性的元素可以看做是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的的一些特性。通俗一点来讲，可以把BFC理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。



**形成BFC的条件**

只要元素满足下面任一条件即可触发BFC特性：

- body 根元素
- 浮动元素：float 除 none 以外的值
- 绝对定位元素：position (absolute、fixed)
- display 为 inline-block、table-cell、table-caption，flex，inline-flex的元素
- overflow 除了 visible 以外的值 (hidden、auto、scroll)



**BFC常见作用**

1、阻止垂直margin合并

​	margin塌陷问题：在标准文档流中，块级标签之间竖直方向的margin会以大的为准，这就是margin的塌陷现象。如果让 2 个元素不在同一个 BFC 中即可阻止垂直 margin 合并。可以用`overflow：hidden`产生 BFC 来解决。

2、清除浮动

​	高度塌陷问题，在通常情况下父元素的高度会被子元素撑开，而在这里因为其子元素为浮动元素所以父元素发生了高度坍塌，上下边界重合，这时就可以用`overflow：hidden`产生 BFC 来清除浮动了。

3、阻止元素被浮动元素覆盖

​	由于左侧块级元素发生了浮动，所以和右侧未发生浮动的块级元素不在同一层内，所以会发生div遮挡问题。可以给右侧元素添加 `overflow: hidden`，触发BFC来解决遮挡问题。



### 10、浮动清除的方法

**方法一：使用带clear属性的空元素**

在浮动元素后使用一个空元素如`<div class="clear"></div>`，并在CSS中赋予`.clear{clear:both;}`属性即可清理浮动。亦可使用`<br class="clear" />`或`<hr class="clear" />`来进行清理。

**方法二：使用CSS的overflow属性**

给浮动元素的容器添加`overflow:hidden;`或`overflow:auto;`可以清除浮动，另外在 IE6 中还需要触发 hasLayout ，例如为父元素设置容器宽高或设置 `zoom:1`。

在添加overflow属性后，浮动元素又回到了容器层，把容器高度撑起，达到了清理浮动的效果。

**方法三：给浮动的元素的容器添加浮动**

给浮动元素的容器也添加上浮动属性即可清除内部浮动，但是这样会使其整体浮动，影响布局，不推荐使用。

**方法四：使用邻接元素处理**

什么都不做，给浮动元素后面的元素添加`clear: both`属性。

**方法五：使用CSS的:after伪元素**

给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动。

```css
.clearfix {
    zoom: 1;
}
.clearfix::after {
    content: "";
    display: block;
    clear: both;
}
```

### 

### 11、关于定位（position属性）

#### 1、absolute

- 生成绝对定位的元素，相对于static定位以外的第一个父元素进行定位。

- absolute绝对定位元素相对的元素是它最近的父元素进行定位，该父元素满足：position的值必须是：relative、absolute、fixed，若没有这样的父元素则相对于body进行定位。

- 元素的位置通过“left”，“top”，“right”以及“bottom”属性进行规定。

#### 2、fixed

生成绝对定位的元素，相对于浏览器窗口进行定位。

当元素祖先的 transform 属性非 none 时，容器由视口改为其父元素。

#### 3、relative

生成相对定位的元素，相对于其正常位置进行定位。不脱离文档流。

#### 4、static

默认值。没有定位，元素出现在正常的流中（忽略top，bottom，left，right或者z-index声明）。

#### 5、inherit

规定应该从父元素继承position属性的值。

#### 6、sticky

CSS3新属性，可以说是position: relative和position: fixed的合体。主要用在对scroll事件的监听上。

1.在目标区域在屏幕中可见时，它的行为就像position: relative;

2.页面滚动时

- 当父元素是body时

  a.滚动距离小于屏幕高度或宽度，它会固定在目标位置

  b.滚动距离大于屏幕高度或宽度，它的表现就像position:relative一样

- 当父元素不是body

  a.在父元素高度内滚动时它会固定在目标位置，就像fixed

  b.在父元素滚动为不可视时它的表现就像position:relative一样

使用条件：
1、父元素不能overflow:hidden或者overflow:auto属性。

2、必须指定top、bottom、left、right4个值之一，否则其行为与相对定位相同。并且top和bottom同时设置时，top生效的优先级高，left和right同时设置时，left的优先级高。

3、父元素的高度不能低于sticky元素的高度

4、sticky元素仅在其父元素内生效

例子：标题吸顶

```css
<ul class="sticky-list">
    <!-- n个list -->
        <li class="sticky-item">
            <div class="title">list1</div>
            <ul class="list">
                <!-- n个item -->
                <li class="item">1111</li>
            </ul>
        </li>
</ul>

<style>
    .title {
        position: -webkit-sticky;
        position: sticky;
        top: 0;
        background-color: #fff;
    }
    .item {
        display: block;
    }
</style>
```



### 12、px、em、rem的区别

- px：像素，在 CSS 中它是绝对的长度单位，也是最基础的单位，其他长度单位会自动被浏览器换算成 px。像素px是相对于显示器屏幕分辨率而言的。使用px可以准确的定位网页元素，但是，不同显示器网页的显示效果可能会有差异，比较难兼容。


- em：em就是根据基准来缩放字体的大小。em实质是一个**相对值**，而非具体的数值。em是**相对于父元素的属性而计算**的，假如父元素的font-size是16px，2em=2*16px=32px。


- rem：rem也是一个**相对值**，不过rem是**相对html根元素的font-size而计算**的。

  比如在做 H5 的时候，前端通常会让 UI 给 750px 宽的设计图，而在开发的时候可以基于 iPhone X 的尺寸 375px * 812px 来写页面，这样一来的话，就可以用下面的 JS 依据当前页面的视口宽度自动计算出根元素 html 的基准 font-size 是多少。

  ```js
  (function (doc, win) {
      var docEl = doc.documentElement,
          resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize',
          psdWidth = 750,  // 设计图宽度
          recalc = function () {
              var clientWidth = docEl.clientWidth;
              if ( !clientWidth ) return;
              if ( clientWidth >= 640 ) {
                  docEl.style.fontSize = 200 * ( 640 / psdWidth ) + 'px';
              } else {
                  docEl.style.fontSize = 200 * ( clientWidth / psdWidth ) + 'px';
              }
          };
  
      if ( !doc.addEventListener ) return;
      // 绑定事件的时候最好配合防抖函数
      win.addEventListener( resizeEvt, debounce(recalc, 1000), false );
      doc.addEventListener( 'DOMContentLoaded', recalc, false );
      
      function debounce(func, wait) {
          var timeout;
          return function () {
              var context = this;
              var args = arguments;
              clearTimeout(timeout)
              timeout = setTimeout(function(){
                  func.apply(context, args)
              }, wait);
          }
      }
  })(document, window);
  ```

- #### vw/vh

  vw 和 vh 分别是相对于屏幕视口宽度和高度而言的长度单位：

  - 1vw = 视口宽度均分成 100 份中 1 份的长度；
  - 1vh = 视口高度均分成 100 份中 1 份的长度；

  在 JS 中 100vw = window.innerWidth，100vh = window.innerHeight。

  视口（移动端你就可以当成屏幕就好啦）的宽为100vw，高为100vh。使用起来很简单，如果你需要一个宽高各为视口一半的div，只需要在css里面这样写:div {width: 50vw ;height: 50vh}

  相对视口的单位，除了 vw/vh 外，还有 vmin 和 vmax：

  - vmin：取 vw 和 vh 中值较小的；
  - vmax：取 vw 和 vh 中值较大的；



### 13、自定义属性

通过自定义属性引用变量

自定义属性也和普通属性一样具有级联性，申明在 :root 下的时候，在全文档范围内可用，而如果是在某个元素下申明自定义属性，则只能在它及它的子元素下才可以使用。

自定义属性必须通过 `--x` 的格式申明，比如：--theme-color: red; 使用自定义属性的时候，需要用 var 函数。比如：

```css
<!-- 定义自定义属性 -->
:root {
    --theme-color: red;
}

<!-- 使用变量 -->
h1 {
    color: var(--theme-color);
}
```

也可以在js中定义后在css中使用

```js
document.body.style.setProperty('--theme-color', this.themeColor)
```



















### 9、white-space 属性设置如何处理元素内的空白

| 值       | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| normal   | 默认。空白会被浏览器忽略。                                   |
| pre      | 空白会被浏览器保留。其行为方式类似 HTML 中的` <pre>` 标签。  |
| nowrap   | 文本不会换行，文本会在同一行上继续，直到遇到` <br>` 标签为止。 |
| pre-wrap | 保留空白符序列，但是正常地进行换行。                         |
| pre-line | 合并空白符序列，但是保留换行符。                             |
| inherit  | 规定应该从父元素继承 white-space 属性的值。                  |



### 44、实现单行、多行文本溢出显示省略号(…) 

单行文本

```css
overflow: hidden;
text-overflow: ellipsis;
white-space: nowrap;
```

多行文本

```css
-webkit-line-clamp: 2;          /* 用来限制在一个块元素显示的文本的行数,2表示最多显示2行。 为了实现该效果，它需要组合其他的WebKit属性 */
-webkit-box-orient: vertical;   /* 和1结合使用 ，设置或检索伸缩盒对象的子元素的排列方式 */
display: -webkit-box;           /* 和1结合使用，将对象作为弹性伸缩盒子模型显示 */
overflow: hidden;
text-overflow: ellipsis;
```







### 23、CSS3新增属性：

1、box-shadow(阴影效果)

2、border-color(为边框设置多种颜色）

3、border-image(图片边框）

4、text-shadow(文本阴影)

5、text-overflow(文本截断)

6、word-wrap(自动换行）

7、border-radius(圆角边框）

8、opacity(透明度）

9、box-sizing(控制盒模型的组成模式)

10、resize(元素缩放）

11、outline(外边框）

12、background-size(指定背景图片尺寸）

13、background-origin(指定背景图片从哪里开始显示)

14、background-clip(指定背景图片从什么位置开始裁剪）

15、background(为一个元素指定多个背景)

16、hsl(通过色调、饱和度、亮度来指定颜色颜色值)

17、hsla(在hsl的基础上增加透明度设置）

18、rgba(基于rgb设置颜色，a设置透明度）

### 18、calc属性

1、css3的一个新增的功能，用来指定元素的长度，你可以使用calc()给元素的border、margin、pading、font-size和width等属性动态的设置值。动态计算长度值，任何长度值都可以使用calc()函数计算，需要注意的是，运算符前后都需要保留一个空格，例如：width: calc(100% - 10px)；

2、calc()语法

```css
 .element {
   width：calc(expression);  
 }
```

3、calc()的运算法则

　　1）、使用 "+"、"-"、"*" 和 "/" 运算

　　2）、可以使用百分比、px、em、rem等单位运算

　　3）、可以混合使用各种单位进行运算

　　4）、表达式中有 "+" 和 "-" 时，其前后必须有空格。

　　5）、表达式中有 "*" 和 "/" 时，其前后可以没有空格，但建议保留





### 36、高斯模糊效果

css3  filter滤镜

`filter: blur(10px);`

因为有溢出的模糊效果，所以要在父元素加`overflow: hidden;`



### 13、当margin、padding的值是百分比时，是相对最近父级块级元素的width

[css height width padding margin 百分比取值的基准问题](https://blog.csdn.net/qq_35809245/article/details/54233662)





### 19、visibility=hidden, opacity=0，display:none的区别

`opacity = 0`：该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如click事件，那么点击该区域，也能触发点击事件的

`visibility = hidden`：该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件

`display: none`：把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉一样。





### 40、两个元素之间会有空隙，可在父元素设置font-size: 0;使两元素完全贴合

如果在父元素设置font-size: 0;的同时设置了文字内容超出隐藏，省略号会不见，这是不宜设font-size: 0;，可把两元素代码中间的换行删掉即可。

### 26、如何画一个三角形

三角形原理：边框的均分原理

```css
// 这是一个倒三角
div {
    width:0px;
    height:0px;
    border-top:10px solid red;
    border-right:10px solid transparent;
    border-bottom:10px solid transparent;
    border-left:10px solid transparent;
}
```



### 28、画一条0.5px的线

**1.采用meta viewport的方式**

```css
<meta name="viewport" content="width=device-width, initial-scale=0.5, minimum-scale=0.5, maximum-scale=0.5"/>
```

这样子就能缩放到原来的0.5倍，如果是1px那么就会变成0.5px

要记得viewport只针对于移动端，只在移动端上才能看到效果

**2.采用tansform: scale()的方式**

```css
transform: scaleY(0.5);
```









### 30、animation（动画）、transition（过渡）、transform（变形）、translate（移动）

来源：http://www.imooc.com/article/79030 

| 属性               | 含义                                                         |
| ------------------ | ------------------------------------------------------------ |
| animation（动画）  | 用于设置动画属性，他是一个简写的属性，包含6个属性            |
| transition（过渡） | 用于设置元素的样式过度，和animation有着类似的效果，但细节上有很大的不同 |
| transform（变形）  | 用于元素进行旋转、缩放、移动或倾斜，和设置样式的动画并没有什么关系，就相当于color一样用来设置元素的“外表” |
| translate（移动）  | translate只是transform的一个属性值，即移动。                 |

#### animation（动画）

语法：`animation: name duration timing-function delay iteration-count direction;`

1. name（需要绑定到选择器的 keyframe 名称）
2. duration（完成动画所花费的时间，以秒或毫秒计）
3. function（动画的速度曲线）
4. delay（动画开始之前的延迟）
5. count（动画应该播放的次数）
6. direction（是否应该轮流反向播放动画）

#### transition（过渡）

语法：`transition: property duration timing-function delay;`

1. property（设置过渡效果的 CSS 属性的名称）
2. duration（完成过渡效果需要多少秒或毫秒）
3. function（速度效果的速度曲线）
4. delay（过渡效果何时开始）

Animation和transition大部分属性是相同的，他们都是随时间改变元素的属性值

他们的**主要区别是transition需要触发一个事件才能改变属性，而animation不需要触发任何事件的情况下才会随时间改变属性值，并且transition为2帧，从from .... to，而animation可以一帧一帧的。**

#### transform（变形）

语法：`transform: none|transform-functions;`
functions提供多种方法，如：skewX(angle)沿着 X 轴的 2D 倾斜转换，translate3d(x,y,z)3D 转换，rotate(angle)2D 旋转，在参数中规定角度等等。

#### translate（移动）

`translate`其实是 `transform`的一种属性值，进去2D或者3D移动

1. translate(x,y) 2D平移，x/y分别是x坐标平移多少像素，y坐标平移多少像素
2. translate3d(x,y,z) 3D平移，和2D一样

### 



### 41、CSS3 动画

如需在 CSS3 中创建动画，需要运用 @keyframes 规则。

@keyframes 规则用于创建动画。在 @keyframes 中规定某项 CSS 样式，就能创建由当前样式逐渐改为新样式的动画效果。

```css
// 用关键词 "from" 和 "to"，等同于 0% 和 100%
@keyframes myfirst
{
	from {background: red;}
	to {background: yellow;}
}

// 可用百分比来规定变化发生的时间
@keyframes myfirst
{
    0%   {background: red;}
    25%  {background: yellow;}
    50%  {background: blue;}
    100% {background: green;}
}
```

在 @keyframes 中创建动画时，需把它捆绑到某个选择器，否则不会产生动画效果。

通过规定至少以下两项 CSS3 动画属性，即可将动画绑定到选择器：

- 规定动画的名称
- 规定动画的时长

```css
div
{
    animation: myfirst 5s;
    -moz-animation: myfirst 5s;	/* Firefox */
    -webkit-animation: myfirst 5s;	/* Safari 和 Chrome */
    -o-animation: myfirst 5s;	/* Opera */
}
```



### 43、CSS sprites

CSS Sprites其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的“background-image”，“background- repeat”，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。

这样可以减少很多图片请求的开销，因为请求耗时比较长；请求虽然可以并发，但是也有限制，一般浏览器都是6个。对于未来而言，就不需要这样做了，因为有了`http2`。







### 33、水平垂直居中的方法

(1) margin: auto法

父元素为relative，子元素定位为上下左右为0，margin：auto可以实现脱离文档流的居中.

```css
div {
    width: 400px;
    height: 400px;
    position: relative;
    border: 1px solid #465468;
}
p {
    position: absolute;
    margin: auto;
    top: 0;
    left: 0;
    right: 0;
    bottom: 0;
    width: 100px;
    height: 100px;
    background: red;
}
html:
<div>
	<p></p>
</div>
```

(2) margin负值法

先绝对定位到父元素距离顶部和左边50%的位置，然后再往左、上移动自身长宽的50%

```css
div {
    width: 500px;
    height: 400px;
    border: 2px solid #379;
    position: relative;
}
p {
    width: 100px;
    height: 100px;
    background-color: red;
    position: absolute;
    top: 50%;
    left: 50%;
    margin-top: -50px;    /* height的一半 */
    margin-left: -50px;   /* width的一半 */
}

/* 补充：其实这里也可以将marin-top和margin-left负值替换成 */
transform：translate(-50%, -50%)       /* 往左，上移动自身长宽的50% */
```

(3) table-cell（未脱离文档流的）

设置父元素的display:table-cell,并且vertical-align:middle，这样子元素可以实现垂直居中。

```css
div{
    width: 300px;
    height: 300px;
    border: 3px solid #555;
    display: table-cell;
    vertical-align: middle;     /* 垂直居中 */
    text-align: center;         /* 水平居中 */
}
p{
    display: inline-block; 
    width: 100px;
    height: 100px;
    background: red;
}
```

(4)利用flex

将父元素设置为`display: flex`，并且设置`align-items: center; justify-content: center;`

```css
div {
    width: 500px;
    height: 500px;
    border: 3px solid #546461;
    display: flex;
    align-items: center;              /* 在侧轴（纵轴）方向上居中 */
    justify-content: center;          /* 在主轴（横轴）方向上居中 */
}
p {
    width: 100px;
    height: 100px;
    background: red;
}
```



### 22、css布局

**圣杯布局**是指布局从上到下分为header、container、footer，然后container部分定为三栏布局。这种布局方式同样分为header、container、footer。圣杯布局的缺陷在于 center 是在 container 的padding中的，因此宽度小的时候会出现混乱。

**双飞翼布局**给center 部分包裹了一个 main 通过设置margin主动地把页面撑开。

**Flex布局**是由CSS3提供的一种方便的布局方式。

请看：

[Flex 布局教程：语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html?utm_source=tuicool)

[Flex 布局教程：实例篇](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)

**绝对定位布局**是给container 设置position: relative和overflow: hidden，因为绝对定位的元素的参照物为第一个postion不为static的祖先元素。 left 向左浮动，right 向右浮动。center 使用绝对定位，通过设置left和right并把两边撑开。 center 设置top: 0和bottom: 0使其高度撑开。

**表格布局**的好处是能使三栏的高度统一。

**网格布局**可能是最强大的布局方式了，使用起来极其方便，但目前而言，兼容性并不好。网格布局，可以将页面分割成多个区域，或者用来定义内部元素的大小，位置，图层关系。



### 35、三栏布局的实现

1、使用float+margin：

给div设置float：left，left的div添加属性margin-right：left和center的间隔px,right的div添加属性margin-left：left和center的宽度之和加上间隔

2、使用float+overflow：

给div设置float：left，再给right的div设置overflow:hidden。这样子两个盒子浮动，另一个盒子触发bfc达到自适应

3、使用position：

父级div设置position：relative，三个子级div设置position：absolute，这个要计算好盒子的宽度和间隔去设置位置，兼容性比较好，

4、使用table实现：

父级div设置display：table，设置border-spacing：10px//设置间距，取值随意,子级div设置display:table-cell，这种方法兼容性好，适用于高度宽度未知的情况，但是margin失效，设计间隔比较麻烦，

5、flex实现：

parent的div设置display：flex；left和center的div设置margin-right；然后right 的div设置flex：1；这样子right自适应，但是flex的兼容性不好

6、grid实现：

parent的div设置display：grid，设置grid-template-columns属性，固定第一列第二列宽度，第三列auto



### 21、css实现一个左侧固定20px，右侧响应式的布局

**1.将左侧div浮动，右侧div设置margin-left**

```css
/*方法1*/
.outer{overflow: hidden; border: 1px solid red;}
.sidebar{float: left;width:200px;height: 150px; background: #BCE8F1;}
.content{margin-left:200px;height:100px;background: #F0AD4E;}
```

**2.固定区采用绝对定位，自适应区设置margin**

```css
/*方法2*/
.outer2{position: relative;height:150px; border: 1px solid red;}
.sidebar2{position: absolute;left: 0;top:0;width:200px;height:100%;background: #BCE8F1;}
.content2{margin-left:200px;height:100px;background: #F0AD4E;} 
```

缺点:

- 使用了绝对定位，若是用在某个div中，需要更改父容器的position。
- 没有清除浮动的方法，若左侧盒子高于右侧盒子，就会超出父容器的高度。因此只能通过设置父容器的min-height来放置这种情况。

**3.标准浏览器的方法**  

```css
/*方法3*/
.outer3{display: table;width:100%; border: 1px solid red;}
.sidebar3{display:table-cell;width:200px;height:150px;background: #BCE8F1;}
.content3{display:table-cell;height:100px;background: #F0AD4E;}
```

**4.双float + calc()计算属性**

```css
/*方法4*/
.outer4{overflow: hidden; border: 1px solid red;}
.sidebar4{float:left;width:200px;height:150px;background: #BCE8F1;}
.content4{float:left;width:calc(100% - 200px);height:100px;background: #F0AD4E;}
```

**5.双inline-block + calc()计算属性**

```css
/*方法5*/
.outer5{box-sizing: content-box;font-size: 0; border: 1px solid red;}
.sidebar5,.content5{display: inline-block;vertical-align: top;box-sizing: border-box;width: 200px;height:150px; background: #BCE8F1;font-size: 14px;}
.outer5 .content5{width:calc(100% - 200px);height:100px;background: #F0AD4E;}
```

这种方法是通过width: calc(100% - 140px)来动态计算右侧盒子的宽度。需要知道右侧盒子距离左边的距离，以及左侧盒子具体的宽度(content+padding+border)，以此计算父容器宽度的100%需要减去的数值。同时，还需要知道右侧盒子的宽度是否包含border的宽度。
在这里，为了简单的计算右侧盒子准确的宽度，设置了子元素的box-sizing:border-box;以及父元素的box-sizing: content-box;。
同时，作为两个inline-block的盒子，必须设置vertical-align来使其顶端对齐。
另外，为了准确地应用计算出来的宽度，需要消除div之间的空格，需要通过设置父容器的font-size: 0;,或者用注释消除html中的空格等方法。

缺点:

- 需要知道左侧盒子的宽度，两个盒子的距离，还要设置各个元素的box-sizing
- 需要消除空格字符的影响
- 需要设置vertical-align: top满足顶端对齐。

**6.float + BFC方法**

```css
/*方法6*/
.outer6{overflow: auto; border: 1px solid red;}
.sidebar6{float: left;height:150px;background: #BCE8F1;}
.content6{overflow:auto;height:100px;background: #F0AD4E;}
```

这个方案同样是利用了左侧浮动，但是右侧盒子通过`overflow: auto;`形成了BFC，因此右侧盒子不会与浮动的元素重叠。

**7.flex**

```css
/*方法7*/
.outer7{display: flex; border: 1px solid red;}
.sidebar7{flex:0 0 200px;height:150px;background: #BCE8F1;}
.content7{flex: 1;height:100px;background: #F0AD4E;}
```

`flex`可以说是最好的方案了，代码少，使用简单。但存在兼容性，有朝一日，大家都改用现代浏览器，就可以使用了。

需要注意的是，`flex`容器的一个默认属性值:`align-items: stretch;`。这个属性导致了列等高的效果。
为了让两个盒子高度自动，需要设置: `align-items: flex-start;`

### 