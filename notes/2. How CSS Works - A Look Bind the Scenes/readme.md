# CSS的机制

## 1. 编写优秀页面的三大支柱及其准则
1. 响应式设计responsive design：跨平台和设备
	- 流体布局fluid layouts
	- 媒体查询media queries
	- 响应式图片responsive images
	- 正确单位correct units
	- 桌面端优先vs移动端优先desktop-first vs mobile-first
2. 编写可维护和可扩展的代码writing maintainable and scalable code
	- 简洁clean
	- 易读easy to understand
	- 支持未来扩展supports future growth
	- 可复用reusable
	- 如何管理文件how to organize files
	- 如何命名类how to name our classes
	- 如何构建html结构how to structure mark up in HTML
3. 实现web性能carrying about web performance
	- 更少的HTTP请求less HTTP requests
	- 更少的代码less code
	- 压缩代码compress code
	- 使用CSS预处理器Use a CSS preprocessor（eg.Sass）
	- 更少的图片less images
	- 压缩图片compress images

## 2. 当加载页面时浏览器是如何处理CSS的？
1. 浏览器加载HTML代码
2. 逐行解析HTML代码 → 构建文档对象模型DOM
3. 找到并加载HTML头部的样式表
4. 解析CSS样式表 → 构建CSS对象模型
	1. cascade解决冲突的声明
	2. 处理最终的CSS值
		eg. 百分比在不同设备上变为像素
5. 使用可视化格式模型呈现页面
	eg. 盒子模型、浮动和定位等

What happens to CSS when we load up a webpage?
1. Load HTML
2. Parse HTML → DOM(Document Object Model)
3. Load CSS(Cascading Style Sheets)
4. Parse CSS → CSSOM(CSS Object Model)
	1. Cascade resolves conflicting CSS declarations
	2. Process final CSS values
5. Render website → Render Tress: DOM & CSSOM
	Using the Visual Formatting Model to render the page

## 2. CSS是如何被解析的1 | 级联和权重

### 官方术语
```css
*{
	padding: 0;
	margin: 0;
}
```
- 选择器Slector：*
- 声明块Declaration block：{ ... }
	- 声明Declaration：padding: 0;
		- 属性Property：padding
		- 声明值Declared value：0

### 1. 解决冲突的CSS声明
#### 级联Cascade
**定义**
当多个规则应用于某个元素时，合并不同样式表并解决不同CSS规则和声明之间的冲突的过程

**类型（根据来源）**
- 作者声明（Author Declarations）：开发人员编写的CSS
- 用户声明（User Declarations）：用户的CSS
- 浏览器声明（Browser Declarations）：用户代理CSS，由浏览器默认设置

#### 如何解决冲突
1. 根据重要性的权重（importance）
	1. !important标记的用户声明
	2. !important标记的作者声明（尽量少用，把它当作最后手段（a last resource），代码更易维护）
	3. 正常的作者声明
	4. 正常的用户声明
	5. 默认的浏览器声明
2. 根据选择器权重（Specifity）
	1. 内联样式（尽量不用）
	2. id（1id > 1000class）
	3. 类、伪类和属性选择器（1class > 1000ele）
	4. 标签和伪元素选择器
	4. 通用选择器（(0, 0, 0, 0)）
	计算时从四个维度比较：weight = (inline, IDs, Classes, Elements) //只要靠前的某个数字更大就不用看后面了
3. 声明的顺序（Source Order）
	- 当具有相同权重时，后声明的会覆盖前者（尽量依靠权重而非顺序，避免因为调整CSS顺序二发生错误，代码更易维护）
	- 引入样式表时，后面的样式也会覆盖前面的（注意顺序）

## 3. 权重练习
refactor your code

优先级
即便两个样式指定的是不同状态的元素，也会根据优先级。
	若:link比:hover优先级高，即使鼠标悬浮在元素上，仍使用:link的样式


## 4. CSS是如何被解析的2 | 最终值的处理
how values are processed in a CSS parsing phase
most commonly used CSS units：percentages, ems, rems, vh, vw
		percentages and Relative Units will ultimately be converted to pixels
1. Declared Value：作者声明
2. Cascaded Value：作者声明根据级联筛选出的结果/浏览器声明-无作者声明
3. Specified Value：CSS属性的初始值（当前两项未声明时起作用，且未继承）/继承父元素的Computed Value
4. Computed Value：将相对值转换成绝对值，以便被继承（em/rem）
5. Used Value：基于布局最后计算的结果（percentage、vh/vw）
6. Actual value：考虑浏览器改变规定，一般有小数的会进行四舍五入的处理

### percentages
百分比不是单位，为了便于理解，当做单位来讲
- fonts：：父元素的computed font-size
- length(eg. height、padding、margin...)：父元素的computed width
- distance:?line-height计算的是当前元素的computed font-size，为哈？

### Relative Units
**em/rem**
- 基于字体
- 可以轻松创建响应式布局，只需修改字体大小，更具有灵活性

- em
  - fonts：父元素的computed font-size
  - length：当前元素的computed font-size
- rem：根元素的computed font-size
	IE9及以下不支持

**vh/vw**
基于视窗viewport
- vh：\d+% * window.innerHeight
- vw：\d+% * window.innerWidth

？？？

rendering phase 渲染期间/阶段

CSS key words like "orange, oral, boulder" and a lot more are computed and replaced here in this step？

 You probably already used the vh unit before, right? That one was really useful to built nice hero sections with 100 percent of the view port's height so that's where we use them a lot.

## 5. CSS是如何被解析的3 | 继承

与文本有关的属性大多可以继承，可以继承父元素的Computed Value
	font-family、font-size、color,etc

是否有级联值？
	有：Specified Value = Cascaded Value
	否：该属性是否可继承？
		是：Specified Value = Computed Value of Parent Element
		再次注意继承的是Computed Value，而不是Declared Value
		否：Specified Value = Initial Value

inherit&initail关键字
- `property: inherit;`：强制继承特定属性
- `property: initail;`：将属性重置为初始值

## 6. 将px转化为rem | 一个高效的工作流
### 为什么以及如何转换？
不用写媒体查询和很多其他代码，只需简单修改就可以实现跨平台跨设备
设置根目录元素html的字体大小，其他所有的px都除以它得到rem值

### 一个简便的转换方式
1. 设置根目录元素html的字体大小为10px（便于计算：1rem=10px）
2. 将所有元素的px缩小十倍转换为rem
3. 考虑到适应用户设置的字体大小，而一般浏览器默认字体为16px，将根目录元素html的字体大小转换为10/16=62.5%

### 继承的应用
之前Natours中曾用通用选择器改变所有元素的box-sizing属性，鉴于该属性是不可继承的，可以使用inherit关键字强制继承
1. body样式中设置box-sizing属性
2. 通用选择器中将box-sizing的值改为inherit
另考虑到通用选择器不能选择伪元素，完善所有元素的选择：`*,*::after,*::before{}`

## 7. CSS是如何渲染网页的 | 可视化格式模型
- 视觉格式化模型(visual formatting model)的工作原理

### 视觉格式化模型(visual formatting model)
1. 本质：算法
2. 作用：计算整个页面的布局
	计算盒子
		盒子尺寸：盒子模型
		盒子类型：display属性
		定位方式：浮动和position属性
		堆叠上下文
		render tree的其他元素
		外部信息：当前窗口大小、图片尺寸等其他因素
	决定render tree中每个元素的盒子布局

### 盒子模型、盒子高宽的计算
content、padding、border、margin、fill area
图片和文本会占用content，但背景图像或背景色则会占用fill area(content + padding + border)
注意：
	1. 默认specified width = content，则fill area = specified width + padding + border
	2. 设置了box-sizing: borderbox;后，fill area = specified width

### 盒子类型、及其如何决定布局的？
块级盒子：`display:block/flex/list-item/table`
行内盒子：`display:inline`(没有宽高，只能设置水平内边距和外边距)
行内块盒子：`display:inline-block`（内部为块级盒子，外部仍表现为行内盒子）
the values flags for flags block layout list item and table also produce block-level boxes.

### 定位方式
- 正常流：默认、设置相对定位
- 浮动：左浮动、右浮动
- 绝对、固定定位：使用top, bottom, left and right相对相对定位的元素移动

后两者都会脱离正常流，但文本和行内元素会环绕浮动元素，而绝对定位对周围元素没有影响，甚至它们可以产生重叠

clear：指出不允许有浮动对象的边

```html
<div class="test">我将出现在屏幕右方</div>
<div class="test2">注意我出现的位置</div>
```

```css
.test {
	float: right;
	background: #eee;
}
.test2 {
	clear: right; /*不声明两个div就会排列在同一行*/
	background: #ddd;
}
```

### 层叠上下文
可能产生层叠上下文的方式：
- z-index属性
- 不为1的opacity属性
- transform属性
- filter属性
- ...
故，并不是仅仅设置z-index就万事大吉了。

## 8. CSS架构 | 组件和BEM
- how to think about layouts
- how to mark up our code in a professional way

代码目标：简洁、模块化、可复用、可扩展

1. Think：考虑布局
	组件驱动设计：将页面划分为模块化组件
		组件：构造接口的**独立**代码
		**跨项目**、可维护、可扩展
		类似Brad Frost的非常流行的atomic设计理念：页面最小的单位是原子，原子聚集在一起形成分子，分子聚集在一起形成生物体，在某些情况下，这些有机体可以看作是我们的组成部分。
2. Build：根据统一的命名系统使用HTML&CSS构建布局
	- 面向对象的CSS
	- S Max
	- BEM(Block Element Modifier 块元素修饰符)
		- Block：a standalone component that is meaningful on its own
		- Element：a part of a block and has no meaning on its own
		- Modifier：a flag that we can put on a block or an element in order to make it different from the regular blocks or elements
		不要嵌套元素名称，如.card>.card__side>.card__details而不是.card__side__details

```
block
block__element
block--modifier / block__element--modifier
```

3. Architect：构建一个合乎逻辑的CSS架构（多个css文件和文件夹目录）
- ITCSS
- S Max
- Hugo Giraudel's 7-1 Pattern
	- 7 folders: partial css
		- base：the basic product definitions
			`_base.scss`：for the real low level basics
				resets
				styles for the HML and body element selectors
		- components：one file for each component
		- layout：define the overall layout
		- pages：styles for specific pages
		- themes：different visual themes
		- abstracts：code that doesn't output any CSS, such as variables or mix-ins
		- vendors：third party CSS
	- one main file: import all of partial files into it
## 9. Natours项目中的接口BEM







































