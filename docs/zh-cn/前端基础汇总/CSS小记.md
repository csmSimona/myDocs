## CSS小记（持续更新）

[CSS实现多种常见布局](https://www.cnblogs.com/longlongdan/p/10532891.html)

[1.5 万字 CSS 基础拾遗（核心知识、常见需求）](https://juejin.cn/post/6941206439624966152)

### 1、text-decoration属性

| 值           | 描述                                            |
| ------------ | ----------------------------------------------- |
| none         | 默认。定义标准的文本。无划线                    |
| underline    | 下划线                                          |
| overline     | 上划线                                          |
| line-through | 中划线                                          |
| blink        | 定义闪烁的文本。（只有FireFox支持）             |
| inherit      | 规定应该从父元素继承 text-decoration 属性的值。 |

### 2、CSS代码书写顺序

1. position flex布局等写在前面
2. 宽高
3. 字体颜色

### 3、& >

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

另外：

- 没有<的用法。
- A+B表示HTML中紧随A的B元素。
- nth-child是个伪类的用法，如p:nth-child(2)就表示在p的父元素中选择位居第二位的p

### 4、inline-block 详解

一句话就是在CSS中通过display:inline-block对一个对象指定inline-block属性，可以将对象呈递为内联对象，但是对象的内容作为块对象呈递。

在CSS中，块级对象元素会单独占一行显示，多个block元素会各自新起一行，并且可以设置width,height属性；而内联对象元素前后不会产生换行，一系列inline元素都在一行内显示，直到该行排满，对inline元素设置width,height属性无效。

我们有个时候既希望元素**具有宽度高度特性，又具有同行特性**，这个时候我们可以使用inline-block。

### 5、dispaly:inline inline-block block 三者区别

（4、5有点重复）

- inline：使用此属性后，元素会被显示为内联元素，元素则不会换行。
  - inline元素设置width，height属性无效。
  - inline元素的padding和margin可以设置，但是水平方向的padding-right，padding-left，margin-right，margin-left都产生了效果，而垂直方向的padding-top，padding-bottom，margin-bottom，margin-top是没有效果的。
- block：使用此属性后，元素会被现实为块级元素，元素会进行换行。可以设置width,height属性。
- inline-block：是使元素以块级元素的形式呈现在行内。**既具有宽度高度特性，又具有同行特性**

### 6、什么时候用margin？什么时候用padding？

#### 使用margin值的情况

- 需要在border外侧添加空白时。

- 空白处不需要背景（色）时。

- 上下相连的两个盒子之间的空白，需要相互抵消时。如15px + 20px的margin，将得到20px的空白。(margin折叠）。

- 需要使用负值对页面布局时(**margin值可以取负，padding不行**)。

#### 使用padding时的情况

- 需要在border内测添加空白时。

- 空白处需要背景（色）时。

- 上下相连的两个盒子之间的空白，希望等于两者之和时。如15px + 20px的padding，将得到35px的空白。

**margin是用来隔开元素与元素的间距；padding是用来隔开元素与内容的间隔。margin用于布局分开元素使元素与元素互不相干；padding用于元素与内容之间的间隔，让内容（文字）与（包裹）元素之间有一段“呼吸距离”。**

### 7、box-sizing: border-box;

`border-box` 告诉浏览器去理解你设置的边框和内边距的值是包含在width内的。

也就是说，如果你将一个元素的width设为100px,那么这100px会包含其它的border和padding，内容区的实际宽度会是width减去border + padding的计算值。大多数情况下这使得我们更容易的去设定一个元素的宽高。

| 值          | 描述                                                         |
| :---------- | :----------------------------------------------------------- |
| content-box | 宽度就是实际内容的宽度                                       |
| border-box  | 宽度包含border和padding，分别减去边框和内边距才能得到实际内容（content）的宽度和高度。 |
| inherit     | 规定应从父元素继承 box-sizing 属性的值。                     |

### 8、border-radius: 50%  一个圆

### 9、white-space 属性设置如何处理元素内的空白

| 值       | 描述                                                         |
| -------- | ------------------------------------------------------------ |
| normal   | 默认。空白会被浏览器忽略。                                   |
| pre      | 空白会被浏览器保留。其行为方式类似 HTML 中的` <pre>` 标签。  |
| nowrap   | 文本不会换行，文本会在同一行上继续，直到遇到` <br>` 标签为止。 |
| pre-wrap | 保留空白符序列，但是正常地进行换行。                         |
| pre-line | 合并空白符序列，但是保留换行符。                             |
| inherit  | 规定应该从父元素继承 white-space 属性的值。                  |

### 10、font-size/fontSize 

在js里面添加的属性名使用驼峰法，在css里面是用连接线

### 11、css优先级由高到低：

1.在属性后面使用!important会覆盖页面内任何位置定义的元素样式。

2.作为style属性写在元素内的样式

3.id选择器

4.类选择器=伪类选择器=属性选择器（后面的样式会覆盖前面的样式）

5.标签选择器

6.通配符选择器

7.浏览器自定义的样式

### 12、link和@import的区别

1.页面被加载时，link会同时被加载，而@import引用的CSS会等到页面被加载完再加载，所以会出现一开始没有css样式，闪烁一下出现样式后的页面（网速慢的情况下)。

2.link属于html标签，没有兼容性，而@import是css2里面的，所以IE5以上才能识别

3.当使用javascript控制dom去改变样式的时候，只能使用link标签，因为@import不是dom可以控制的

4.link除了能加载css外还能定义RSS，定义rel连接属性，@import只能加载css

5.link方式样式的权重高于@import的

### 13、当margin、padding的值是百分比时，是相对最近父级块级元素的width

[css height width padding margin 百分比取值的基准问题](https://blog.csdn.net/qq_35809245/article/details/54233662)

### 14、css可继承属性：

所有元素可继承：visibility和cursor。

内联元素可继承：letter-spacing、word-spacing、white-space、line-height、color、font、font-
family、font-size、font-style、font-variant、font-weight、text-decoration、text-transform、
direction。

终端块状元素可继承：text-indent和text-align。

列表元素可继承：list-style、list-style-type、list-style-position、list-style-image。

### 15、margin auto是自动根据剩余的长度居中对齐，并不是0

### 16、background-color设置的背景颜色会填充元素的content、padding、border区域

### 17、如果 position:absolute | fixed; 或 float的值不为none，display的值就会被设置为block

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

### 19、visibility=hidden, opacity=0，display:none的区别

`opacity = 0`：该元素隐藏起来了，但不会改变页面布局，并且，如果该元素已经绑定一些事件，如click事件，那么点击该区域，也能触发点击事件的

`visibility = hidden`：该元素隐藏起来了，但不会改变页面布局，但是不会触发该元素已经绑定的事件

`display: none`：把元素隐藏起来，并且会改变页面布局，可以理解成在页面中把该元素删除掉一样。

### 20、伪类选择器与伪元素

**伪类**

伪类选择器分为两种。

（1）**静态伪类**：只能用于**超链接**的样式。如下：

- `:link` 超链接点击之前
- `:visited` 链接被访问过之后

PS：以上两种样式，只能用于超链接。

（2）**动态伪类**：针对**所有标签**都适用的样式。如下：

- `:hover` “悬停”：鼠标放到标签上的时候
- `:active` “激活”： 鼠标点击标签，但是不松手时。
- `:focus` 是某个标签获得焦点时的样式（比如某个输入框获得焦点）

由于css的优先级问题，下面四个伪类需要按顺序书写，否则会出现问题

**L（link）V（visited）H（hover）A（active）**

love and hate（爱与恨）

**伪元素**

基于元素的抽象，它跟伪类的区别就是它依赖于元素，其自身可作为一个抽象的元素来使用，行内元素，伪元素使用时要用两个冒号，但为兼容IE只写一个冒号。

1. `:before`   元素之前
2. `:after`  元素之后
3. `:first-letter`  文本的首字母
4. `:first-line`  文本的首行

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

### 24、a:link,a:visited,a:hover,a:active 顺序

1. link:连接平常的状态
2. visited:连接被访问过之后
3. hover:鼠标放到连接上的时候
4. active:连接被按下的时候

正确顺序：“爱恨原则”（LoVe/HAte），即四种伪类的首字母:LVHA。再重复一遍正确的顺序：a:link、a:visited、a:hover、a:active .

### 25、关于定位（position属性）

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

  b.滚动距离大于屏幕高度或宽度，它的表现就像position:relative和1一样

- 当父元素不是body

  a.在父元素高度内滚动时它会固定在目标位置，就像fixed

  b.在父元素滚动为不可视时它的表现就像position:relative和1一样

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

### 27、说一下css盒模型

CSS中的盒子模型包括IE盒子模型和标准的W3C盒子模型。

这两种盒子模型最主要的区别就是width的包含范围：

标准盒子模型的盒子总宽度：左右border+左右padding+width

IE盒子模型的盒子总宽度：width（即IE的内容宽度还包含了padding和border）

在CSS3中引入了box-sizing属性

box-sizing:content-box;  表示标准的盒子模型

box-sizing:border-box;  表示的是IE盒子模型

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

### 31、什么是BFC？

块级格式化上下文 (Block Formatting Context) 。

具有BFC特性的元素可以看做是隔离了的独立容器，容器里面的元素不会在布局上影响到外面的元素，并且BFC具有普通容器所没有的的一些特性。通俗一点来讲，可以把BFC理解为一个封闭的大箱子，箱子内部的元素无论如何翻江倒海，都不会影响到外部。

**形成BFC的条件**
只要元素满足下面任一条件即可触发BFC特性：

- body 根元素
- 浮动元素：float 除 none 以外的值
- 绝对定位元素：position (absolute、fixed)
- display 为 inline-block、table-cell、table-caption，flex，inline-flex的元素
- 除了 visible 以外的值 (hidden、auto、scroll)

**BFC常见作用**

用于清除浮动，防止margin重叠等

1、阻止外边距折叠

​	margin塌陷问题：在标准文档流中，块级标签之间竖直方向的margin会以大的为准，这就是margin的塌陷现象。可以用overflow：hidden产生bfc来解决。

2、包含浮动元素

​	高度塌陷问题，在通常情况下父元素的高度会被子元素撑开，而在这里因为其子元素为浮动元素所以父元素发生了高度坍塌，上下边界重合，这时就可以用BFC来清除浮动了。

3、阻止元素被浮动元素覆盖

​	由于左侧块级元素发生了浮动，所以和右侧未发生浮动的块级元素不在同一层内，所以会发生div遮挡问题。可以给右侧元素添加 overflow: hidden，触发BFC来解决遮挡问题。

### 32、重绘（repaint）和重排（reflow）

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

### 34、浮动清除的方法

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

结合:after 伪元素（注意这不是伪类，而是伪元素，代表一个元素之后最近的元素）和 IEhack ，可以完美兼容当前主流的各大浏览器，这里的 IEhack 指的是触发 hasLayout。

给浮动元素的容器添加一个clearfix的class，然后给这个class添加一个:after伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动。

```css
.clearfix {
    display: inline-block;
    &:after {
        display: block;
        content: '';
        height: 0;
        line-height: 0;
        clear: both;
        visibility: hidden;
    }
}
```

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

### 36、高斯模糊效果

css3  filter滤镜

`filter: blur(10px);`

因为有溢出的模糊效果，所以要在父元素加`overflow: hidden;`

### 37、chrome最小显示12px，手机上最小显示10px

### 38、line-height: 1;等于 line-height: 100%;根据该元素本身的字体大小设置行高

### 39、px、em、rem的区别

px：**像素**。相对长度单位。像素px是相对于显示器屏幕分辨率而言的。使用px可以准确的定位网页元素，但是，不同显示器网页的显示效果可能会有差异，比较难兼容。

em：em就是根据基准来缩放字体的大小。em实质是一个**相对值**，而非具体的数值。em是**相对于父元素的属性而计算**的，假如父元素的font-size是16px，2em=2*16px=32px。

rem：rem也是一个**相对值**，不过rem是**相对html根元素的font-size而计算**的。

### 40、两个元素之间会有空隙，可在父元素设置font-size: 0;使两元素完全贴合

如果在父元素设置font-size: 0;的同时设置了文字内容超出隐藏，省略号会不见，这是不宜设font-size: 0;，可把两元素代码中间的换行删掉即可。

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

### 42、`<ins>`：定义文档的其余部分之外的插入文本。

可与 `<del>` 标签一起使用，来描述对文档的更新和修正。

```html
<p>这件商品现在是 <del>100元</del> <ins>50元</ins> 一件。</p>
```

效果：![ins](..\picture\ins.png)

### 43、CSS sprites

CSS Sprites其实就是把网页中一些背景图片整合到一张图片文件中，再利用CSS的“background-image”，“background- repeat”，“background-position”的组合进行背景定位，background-position可以用数字能精确的定位出背景图片的位置。

这样可以减少很多图片请求的开销，因为请求耗时比较长；请求虽然可以并发，但是也有限制，一般浏览器都是6个。对于未来而言，就不需要这样做了，因为有了`http2`。

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

