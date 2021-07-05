## Section Intro
making the Natours project responsive

- pretty advanced responsive design techniques
  media queries
  screen width resolutions
  different touch capabilities
  responsive images
- how to use feature queries to implement different features for browsers with different capabilities

## Mobile-First vs Desktop-First and Breakpoints
现代响应式设计的两个基本方面
决定网站或应用程序是移动优先还是桌面优先
为项目选择断点

最传统也最易学的方法：媒体查询+max-width/min-width

桌面优先策略
1. 为适应桌面编写css代码
2. 使用测试最大宽度（max-width）的媒体查询让设计适应更小屏幕

移动优先策略
1. 为适应手机编写css代码
  考虑到移动端的体验，将网站或应用的功能精简到绝对必须的程度，去掉所有不必要的东西以达到更小更快的目标
2. 使用测试最小宽度（min-width）的媒体查询将设计移动到更大的屏幕上
好处：
- 互联网流量的很大一部分已经来自移动
- 内容优先于纯粹的审美设计，即内容为王（content is king）
问题：
在桌面上可能会显得空洞和简单
如果网站并没有使用设备的资源和能力，有一个先进的系统也没什么意义
习惯于桌面网站的会不适应移动优先，过多限制

根据网站的目的以及用户的需求选择移动优先还是桌面优先
无论做出什么决定，移动优先和桌面优先都同等重要，不应该把其中一个当做解决方案进行设计，而将另一个抛诸脑后。


区别
桌面优先的max-width和移动优先的min-width

max-width的媒体查询的工作原理
0--------600--------900--------1200--------Infinity
```css
/*检查当前视窗宽度是否小于等于600px，若是，应用内部代码*/
@media all and (max-width: 600px) {
  //
}
/*≦900px*/
@media all and (max-width: 900px) {
  //
}

@media all and (max-width: 1200px) {
  //
}
```
媒体查询相当于在特定的视窗宽度时覆盖特定的CSS
都满足条件代码就都应用，冲突的规则按照后者覆盖前者，所以一般把媒体查询放在代码最后。

```css
/*≧600px*/
@media all and (min-width: 600px) {
  //
}
@media all and (min-width: 900px) {
  //
}

@media all and (min-width: 1200px) {
  //
}
```

选择breakpoints的三个方法
- 直接选择流行设备（iphone、ipad）的宽度作为断点：最常用、也最糟糕
  忽略了其他设备的用户
  这种策略不能更好地适应未来，苹果可能改变所有设备的分辨率（复用性、可维护性）
- 查看整个互联网上所有最常用的设备宽度，尝试以合理的方式将它们分组，然后从中选择断点：虽然仍不够理想，但比第一种方法好得多
  在相似的设备宽度之间设置断点
- 忽略所有的设备，只关注页面的内容和设计：最好的和最理想的方法
  从桌面/手机开始，减少/增加宽度，一旦页面设计出现问题，就插入一个新的断点，即将断点插入到任何看起来奇怪或不合适的地方
  更困难，也很少人用
  只要需要两个预定义的断点，才能在它们之间得到一大堆断点

第二种方法
工具：StatCounter获取最常用的屏幕尺寸

0--------600--------900--------1200--------1800--------Infinity
   手机      平板电脑  横向平板电脑  桌面电脑    大型桌面电脑


Anyway, in this diagram, I just plotted these most-used screen sizes, that you can see in the chart down there.
无论如何，在这个图表中，我刚刚绘制了这些最常用的屏幕尺寸，你们可以在下面的图表中看到。
So, from this, you can already see pretty good how we could group these screen sizes.
因此，从这里，你已经可以很好地看到我们是如何将这些屏幕尺寸分组的。
Right?
对吧？
So, usually, we'll need one breakpoint for phones, one for portrait tablets, one for landscape tablets and one for the desktop.
因此，通常情况下，我们需要一个手机断点，一个用于肖像平板电脑，一个用于横屏平板电脑，还有一个用于桌面电脑。
There can be more, or course, but these are the basics.
可以有更多，或当然，但这些都是基本的。
So, where do you think these breakpoints should be, based on this diagram?
那么，根据这个图，您认为这些断点应该在哪里呢？


## Let's Use the Power of Sass Mixins to Write Media Queries
- how to use a powerful Sass mixing to write all our media queries
- how to use the @content and @if Sass directives
- Taking advantage of Chrome DevTools for responsive design

传统方法：
1. 创建另一个CSS文件
2. 每个断点写一个大的媒体查询
3. 将代码复制到媒体查询中修改成相应的值
```
@media only screen and (max-width: xxx){
  // 复制代码修改值
}
```

更好的方法：
将媒体查询添加到要修改的选择器中

sass优化的方法：
把媒体查询写成mixin，建立一个媒体查询管理器
1. 减少写媒体查询的重复问题
2. 方便修改断点

@content 直接传入并应用整个代码块

@if (条件) {css样式}

媒体查询中一般不写px当做单位，而希望数值能随着用户设置的默认字体大小而改变，所以使用rem、em替代，又因为rem在某些浏览器中不能正常工作，所以直接使用em。

媒体查询的顺序
当多个媒体查询都符合条件时，按照顺序进行覆盖，桌面优先可以按照断点由大到小排序，手机优先反之

编写媒体查询的文件顺序
base → typography → layout → grid → header → footer → navigation → home → components

## Writing Media Queries - Base_Typography and Layout
修改typography、grid、header、navigation、footer

## Writing Media Queries - Layout_About and Features Sections
修改home、composition、feature-box

自身为相对定位，然后设置为左浮动？？？

20188
Let's put 10 here as well.
这里也写上10。


## Writing Media Queries - Tours_Stories and Booking Sections
card、story、form、home

Sizzy：在不同设备上测试

## An Overview of Responsive Images
响应式图片不仅是响应式设计的一个方面，更是网页性能的一个重要方面。

响应式图片是什么？
使用HTML或CSS中的不同技术将正确的图像提供给正确的屏幕尺寸和设备，这样用户就不必下载对于他们的设备来说太大的图像。

什么时候使用响应式图片？
1. 分辨率切换：为更小的屏幕提供分辨率更小的同一个图片
2. 屏幕像素密度切换：
  什么是屏幕像素密度？
    一英寸或一厘米内的像素数量。
  根据屏幕像素密度有哪些分类？
    1x屏幕（低分辨率屏幕）：经典的PC屏幕，使用一个物理像素来展示代码中的1px
    2x屏幕（高分辨率屏幕）：现代智能手机，带有视网膜显示屏的MacBook，使用两个物理像素来展示代码中的1px
  对图片清晰度有什么影响？
    在高分辨率屏幕上，使图像的分辨率是原始图像的两倍
3. 艺术指导/方向art direction
  在不同的分辨率下呈现不同的图像，可以是只保留重要细节的简化版，也可以是完全不同的图像

前两个针对同一图片不同分辨率，后一个直接换上不同的图片

Remember this diagram we talked about but in the beginning of the course where I told you how important performance is?
还记得我们在课程一开始讲过的，性能有多重要的这个图表吗？

## Responsive Images in HTML - Art Direction and Density Switching
在HTML中实现响应式图片
- how to use the srcset attribute on the image
- how to use source HTML elements together with density descriptors
- how and why to use the picture element for art direction with media queries in HTML

HTML中和CSS中的图片有什么区别？
HTML中的图片
  <img>标签
  <i>标签+图标字体类
CSS中的图片
  background-image

the philosophy behind density switching

**密度切换**
- 方法：使用srcset属性指定图片路径和使用密度描述符（1x, 2x）指定设备像素比（DPR, Device Ppixel Ratio），可添加多个，用逗号隔开
- 语法：`srcset: "图片路径 密度描述符, 图片路径 密度描述符";`
- 示例：
<img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x" alt="full logo" class="footer__logo">


**艺术指导/方向art direction**
- 方法：
  - picture标签：为图片指定多个源
  - source标签：没有闭合标签，可添加多个
  - srcset属性：指定图片路径和设备像素比，可添加多个，用逗号隔开
  - media属性：可以放置一个CSS媒体查询
  - src属性：不支持srcset的浏览器应用图片
  - img标签：不符合媒体查询的情况下应用的图片
- 示例：
<picture class="footer__logo">
  <source srcset="img/logo-green-small-1x.png 1x, img/logo-green-small-2x.png 2x"
    media="(max-width: 37.5rem)"
    src="img/logo-green-small-2x.png">
  <img srcset="img/logo-green-1x.png 1x, img/logo-green-2x.png 2x"
    alt="Full logo"
    class="footer__logo"
    src="img/logo-green-2x.jpg">
</picture>

Now these ones here, I'm not going to do them, okay?
这里的这些，我不会做的，好吗？


## Responsive Images in HTML - Density and Resolution Switching
- how to allow the browser to decide which is the best image to download, using the source set attribute with descriptors and the size attribute of the image element.
- how to test out the resolution of our screen using dev tools
  add device pixel ratio：不是总是有效

- 强制浏览器根据媒体查询使用特定的图片
- 允许浏览器根据当前的窗口和像素密度情况选择最好的图片

原理：
浏览器通过当前窗口宽度（view port width）、屏幕显示密度（display density）、图片本身宽度、代码定义的不同窗口宽度下的图片宽度信息来确定不同情况下使用哪个图片最合适。

1. 设置srcset属性
- 方法：类似密度转换，但使用宽度描述符说明图片宽度，浏览器无需下载图片即可获取图片宽度信息
- 语法：`srcset: "图片路径 宽度描述符, 图片路径 宽度描述符";`
- 示例：
<img srcset="img/nat-1.jpg 300w, img/nat-1-large.jpg 1000w">
300w代表宽度为300px
2. 设置sizes属性
- sizes属性：告诉浏览器在不同窗口宽度下图像的大致宽度
- 语法：`sizes: "媒体查询 指定宽度, 媒体查询 指定宽度, 默认宽度";`
<img sizes="(max-width: 56.25em) 20vw, (max-width: 37.5em) 30vw, 300px">
20vw = 指定宽度 / 56.25em = 指定宽度 / 900px
30vw = 指定宽度 / 37.5em = 指定宽度 / 600px
3. 设置src属性
防止用户使用不支持srcset、sizes这些新属性的旧浏览器

sublime如何查看图片分辨率/尺寸

屏幕分辨率 = 像素密度 / 窗口宽度

第一次能打开property，后面就不能打开了，图片应用规则也很奇怪

## Responsive Images in CSS
- how to implement responsive images in CSS by using media queries to target high resolution displays
- how to combine multiple conditions in media queries


media queries condition
- viewport width
  @media only screen and (max-width: 37.5em) {}
- device resolution
  @media only screen and (min-resolusion: 192dpi) and (min-width: 37.5em){}// 每英寸192个点，这是苹果视网膜屏幕的分辨率，一种高分辨率屏幕
  同同时考虑到设备宽度小于600px的一般是屏幕为2x的手机，`600*2=1200`，对1200px的图片来说绰绰有余
  Safari不支持，请改用-webkit-min-webkit-pixel-ratio: 2，等价于2x

- how to target higher resolution screens
- how to combine multiple conditions in a media query

## Testing for Browser Support with @supports
- how to use feature queries in CSS using the @supports rule
- backdrop-filter property


工具
caniuse.com：检查CSS属性的浏览器兼容性

graceful degradation：在现代浏览器上使用新CSS属性，在旧浏览器上显示相应的简化版本

backdrop-filter：对选定元素后面的内容应用一个过滤器，如背景模糊
  - blur(1rem)：模糊程度
  - brightness(200%)：亮度
  - invert()：反色
  - sepia()：色谱

@supports (condition1) or (condition2) {}
  eg. @supports (-webkit-backdrop-filter: blur(10px)) or (back-filter: blur(10px)) {}

backface-visibility：Safari不支持，需要加前缀-webkit-

clip-path：旧版本的firefox不支持

header:29 媒体查询里的clip-path不用@support吗？？？

story:38 border-radius: none;是个什么操作，另外，shape-outside为啥没有检测是否可用？

feature query?是什么东西？




So the clip path property will then be applied and only in that case we want the height of 95 as we had in the beginning.
因此，剪辑路径属性将被应用，只有在这种情况下，我们想要的高度为95，因为我们在开始。
And if it's not the case then let's just put like 85.
如果不是这样的话，我们就写成85。
And so that's better so the user knows that the page actually continues after this hero section.
所以这样更好，让用户知道页面实际上在这个英雄部分之后继续。
So let's take a look at that now.
现在让我们来看看这个。
And it actually already worked.
事实上它已经起作用了。
So you see that it's now smaller here and then down there, the webpage continues.
所以你可以看到这里变小了，那里变小了，网页继续说道。
And if you put this even smaller, like 80 view H then you would see, well it would be maybe a bit too much, but you get my point anyway, right?
如果你把这个放得更小，比如80视图h，你会看到，这可能有点过了，但是你明白我的意思，对吧？


And so yeah, that was the problem.
没错，这就是问题所在。
And so the overflow hidden here, what it does it basically it cuts out the part of the image which is overflowing which is bigger than this element.
所以隐藏在这里的溢出，它所做的基本上就是把图像中溢出的，比这个元素大的部分去掉。
Because you see this element has only this size.
因为您看到这个元素只有这个大小。

## Setting up a Simple Build Process with NPM Scripts
自动为属性添加前缀
压缩代码

build process
自动化当我们完成开发之后为投入生产（部署到服务器上）所重复做的一系列行为

1. 编译sass代码
2. concatenation：将css文件的内容与css和icon-font文件合并，这样页面只需包含一个css文件
    concat包
3. 自动添加前缀到我们的代码
4. 压缩整个代码

npmjs.com

## Wrapping up the Natours Project_ Final Considerations
- 使用伪元素::selection修改选择页面文本时的效果
- 把@media (condition) {}改成@media only screen and (condition) {}，表示媒体查询只应用到屏幕，如无需应用到打印
- 使用meta元素指定viewport的值
  若不指定浏览器可能会以网站最大进行缩放
- 在较小屏幕上默认为移动触摸设备对卡片做了优化，但对ipad、landscape模式，并不能对卡片进行悬浮，也就不能看到卡片背部，即不能通过屏幕宽度区分移动触控设备
  only screen and (hover: none)
  only screen and (hover: hover)
  chome devtools - add device type
- 导航点击没反应？图标缺失？
















