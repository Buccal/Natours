

## Converting Our CSS Code to Sass | Variables and Nesting
1. 颜色
注意：那些只使用了一次的属性值不要用变量

2. 嵌套
注意：相同前缀也是可以嵌套的，如.tools、.tools__btn、.tools__btn--white可以写成
```sass
.tools{
	&__btn{
		&--white{

		}
	}
}
```

## Implementing the 7-1 CSS Architecture with Sass
BEM原则和7-1模式
**7个包含部分css的文件夹**
base：最基本的产品定义product definitions
	`_base.scss`：存放非常低等级的基础
		初始化
		html和body的样式
	`animations.scss`：存放动画
	`typography.scss`：用于版面设计
	`utilities.scss`：for utilities
abstracts：不会输出到css中的代码
	变量
	mix-ins
	函数
components：每个组件单独存放在一个文件中（如按钮）
	可复用的
		完全独立
		可以在任何地方使用
	通过布局连接到一起组成了网站或app（building blocks）
layout：定义整体布局
	这种体系结构是为多页面项目设计的，因此这些布局元素应该适用于所有页面
	header：全局标题，可能在每个页面都有这个标题
	footer：全局页脚
	cetera：全局页眉
pages：具体页面的样式
	home.scss
themes：不同视觉的visual主题
vendors：第三方CSS
	bootstrap
	icon system
	animation framework
注意：下划线表示是部分scss，故这些文件夹里的文件都要加上_前缀
**一个主文件：导入部分css**
@import path-of-the-partial-sass（不用写_和.scss）
除了import声明不会有其他代码

## Review | Basic Principles of Responsive Design and Layout Types
**响应式设计的三个基本原则**
- 使用流动的网格和布局fluid grids and layouts
	使用百分比表示布局相关的长宽
- 灵活、响应式的图片flexible and responsive images
	图片不会随着窗口的改变自动伸缩
	使用百分比定义图片的尺寸
	为不同的宽度优化图片
- 媒体查询media queries
	为特定宽度（断点breakpoints）范围的设备提供不同的的样式

we make images flexible by defining their dimensions and percentages, rather than fixed units like pixels.

**三个主要的布局类型**
基于float的布局
	浏览器兼容
Flex盒布局
	laying out elements in a one dimensional row
CSS Grid
	creating the over layout of a page in a fully fleshed 2D grid, two dimensional grid.

## Building | a Custom Grid with Floats
build a simple float grid
构建一个简单的网格系统architect and build a simple grid system
- 属性选择器的工作原理
- 强大的伪类的工作原理
- calc函数的工作原理
- calc函数和sass简单的数学运算的区别

not伪类

calc()方法
	css：可以混合单位进行运算
	sass：不可以混合单位，因为一些单位是根据布局来计算的，而sass在渲染之前会先进行编译，故这个操作应该留在浏览器使用visual formatting model渲染css时。
参与计算的变量：#{$变量名}

为什么用inline-block不能一行放两个？


**网格是什么**
可以构建统一接口consistent interfaces的设计系统
gutter：列之间的统一间距consistent space


## Building | About

- how to think about components
- How and why to use utility classes
- how to use the background-clip property, especially with text
- how to transform multiple properties simultaneously/at the same time
- how to use the outline-offset property together with outline
- how to style elements that are not hovered while other elements are

1. think and break it down what we have to build in this section
一个section内，上面是一个h2，中间左边是两个h3+p，中间右边是三个img，最下面是个第二按钮
	img可以作为组件
	中间部分可用grid

	把外壳section的样式写在`_homepage.scss`里
		`_homepage.scss`包含的是在主页、且不会再在项目中的其他地方出现，至少不是类似的一个具体的样式
	h2、h3、p写在`_typography`，都是排版的一部分

**Emmet**
参见Tools/Sublime Text3/Packge.txt
Lorem


transform:
	translate/translateX/translateY/：平移
	scale：等比缩放，如1.1指110%
	rotate：旋转
	skew：歪斜，指2deg指2°

**utility classes工具类**
用元素将目标封装在其中，给元素添加样式


**HTML实体符号HTML Entity**
进入codingheroes.io/resources，打开HTML Entity Reference by CSS-Tricks，搜索arrows，第一列直接copy
	比起图标字体，这个更方便

**响应式图片设计**
always define the width of images in percentages if possible. This way, it will nicely scale with the view port.

compistion
1. 样式
2. 位置
3. 层叠
4. 悬浮框
5. 悬浮缩放

## Building | Features
- how to include and use an icon font
- Another way of creating the "skewed section" design
- How and when to use the direct child selector

1. 分析html结构
	四个div：图标、h3、p

2. 将样式分类
3. 分别实现
	下载图标字体linea.io
	先用icon font的css格式，下一章再用：
		使用矢量图标svg而非png图标，后者在页面伸缩时不能很好地自适应
		先指定font family，然后链接font文件夹中的各种字体文件以适应不同的浏览器，然后对每一个图标定义了一个类名
		i本来代表italic，但有人将其与icon混淆，现在i的本意已经不再使用，故普遍用来代表icon了。
	因为悬浮缩放效果，每个列里都再套一个feature-box块

## Building | Tours
build a rotatingcard
- How to build an amazing, rotating card
- How to use perspective in CSS
- How to use backface-visibility properties
- Using background blend modes
- How and when to use the box-decoration-break property

**perspective**
firefox: -moz-perspective
值越小，透视效果越明显


**颜色参考**
codingheroes.io/resources

**免费图片**
unsplash
codingheroes.io/resources

**background blend modes**
介绍了元素和背景图片如何混合

card__heading-span
not an element of heading but a new element in the BEM system

## Building | Stories
- How to make text flow around shapes with shape-outside and float
- How to apply a filter to images
- How to create a background video covering an entire setion
- How to use the video HTML element
- How and when to use the object-fit property

同个元素有多个transform，目前只能写到一起

动画效果分析
- 图片缩小
- 图片模糊
- 文字从底部进入

**backface-visibility**


**filters**

**<video>**
不用<video>标签里的source属性，而是在<video>标签内嵌套一个<source>元素，指定<source>的src属性
autoplay
loop
muted

autoplay="autoplay" loop="loop" muted="muted"
或
autoplay loop muted




**免费视频网站**
coverr.co
会同时下载mp4和webm，兼容现代浏览器

**视频如何在保持长宽比的情况下占满整个盒子，类似background-size: cover;？**
1. 视频及其父元素都设置宽高百分百
2. 设置视频为object-fit:cover;

object-fit: fill; //不能保持长宽比
object-fit: contain; //和之前比没啥变化，只填充了父元素，不会裁剪

设置背景图片为cover后，左右图片溢出，看不到整个页面的padding了，所以设置overflow:hidden;

## Building | Booking
- How to implement "solid-color gradients"
- How to use the ::input-placeholder pseudo-element
- How and when to use the :focus, :invalid, placeholder-shown and :checked pseudo-classes
- How the general and adjacent sibling selectors work and why we need them
- Techniques to build custom radio buttons

按钮元素和瞄标签的区别
按钮元素没有:link和:visited



Now this focus is actually very important for people who use a webpage without a mouse, but only with a keyboard, and so when they move around with a keyboard on the webpage, they need to know which form elements are actually focused, and so for accessibility reasons, we should never just do input focus, and then set the outline to none and call it a day.
对于那些使用网页而不使用鼠标，只使用键盘的人来说，这个重点是非常重要的，所以当他们在网页上使用键盘移动时，他们需要知道哪些表单元素实际上是重点关注的，所以出于可访问性的原因，我们不应该仅仅使用输入重点，然后将大纲设置为无，然后收工。
So we should always make the form elements that are focused visible, alright?
因此，我们应该始终使聚焦的表单元素可见，对吗？

那你tm还设置none了？！！！


::-webkit-input-placeholder伪类
只能在Safari和Chrome上使用


## Building | Footer
- How to design a simple website footer


## Building | Navigation
- how checkbox hack works
- how to create custom animation timing functions using cubic bezier curves
- how to animate the solid-color gradients to create a nice hover effect
- how and why to use the transform-origin property

1. 先看一遍整体效果
2. 分析组成部分
按钮的三条线在点击后变成叉，就是由复选框实现的，如上自定义单选按钮，这里是隐藏复选框，设置label样式
当复选框选中，显示整个导航，这时可以使用:checked伪类实现
3. 写HTML
4. 写CSS

linear gradients 线性渐变，从一边到另一边
radial gradient 径向渐变，从元素中间到周围所有方向


background-position: 100%/top等

时间函数
	cubic-bezier()
工具：
	easings.net
	cubic-bezier.com



按钮变化：三条线变成一个叉
三条线是一个元素及其::before、::after，叉是元素消失，::before、::after旋转形成交叉。

transform-origin: right/left/center;// 描述了转换发生的地点，默认是元素中心

## Building | a Pure CSS Popup
- How to build a nice popup with only CSS
- How to use the :target pseudo-class
- How to create boxes with equal height using display: table-ceil
- How to create CSS text columns
- How to automatically hyphenate words using hyphens property

HTML entities
破折号 &ndash;
空格 &nbsp;
向右箭头 &rarr;
叉 &times;

Now in a real life scenario, it would probably not be a good idea to ask the client to first read the terms before booking，一般是注册的时候阅读……

how to fix the problem that images overlap the border radius with the image overlapping the border?
overflow: hidden;

So you have a word and then here there's not enough space for it, and so there's a hyphen and it continues on the next line.
你有一个单词，但是这里没有足够的空间，所以这里有一个连字符，它在下一行继续。
And actually if you select it, it selects both parts, so that's really nice as well.
实际上，如果你选择它，它会同时选择两个部分，这也很好。

**Column Layout**
column-count：一行平分成多少列
column-gap：列与列之间的间隔是多少
column-rule：列与列之间的分割线

**hyphens属性**
none，默认值
manual，手动指定希望连字符出现的位置，不实用
auto，自动根据文档指定语言（<html lang="en">）找到连字符出现的位置

以下三者的区别
display: none;
opacity: 0;
visibility: hidden;

**属性前缀**
-moz-// Mozilla
-ms-// Microsoft Edge
-webkit-//Chrome和Safari
工具：Autoprefixer




