- SASS：CSS的一个扩展
- NPM系统：编译器

- 如何写SASS
- 如何使用NPM包和NPM脚本编译SASS

## 什么是SASS
**什么是SASS？**
SASS是当前最流行的CSS预处理器，添加了很多强大又优雅的代码的CSS扩展，主要修复了很多CSS的问题。
	- 难以管理，没有逻辑
	- 不能复用

其他CSS预处理器：Less、Stylus

**它的工作原理是什么？**
1. 在Sass文件中编写Sass
2. 编译器将写好的Sass文件转为CSS代码

**SASS有哪些特性**
- variables：可以使用变量自定义属性的值，便于复用
- nesting：可以将选择器嵌套，减少代码量
- operators：可以使用操作符进行数学运算
- partials and imports：可以将不同文件的css导入到一个单独的文件中
- mixins：可以编写可复用的CSS代码
- functions：类似mixin，但它产生的值可以以后使用
- extends：可以让不同的选择器继承同一些样式声明
- control directives：可以使用条件、循环编写复杂代码（基本不常用，这里不提，更适合writing CSS frameworks or something）

**两种语法**
- Sass：缩进敏感、不用任何花括号和分号，更复杂、更难学、更难转换为CSS
- SCSS：Sassy CSS，保留了原本CSS的语法样式

## SASS第一步 | 变量和嵌套

### 变量

$变量名: 值; //注释

选择器{属性:$变量名}

注意：值可以为颜色或数值，数值记得加单位

### 嵌套

选择器{
	选择器{
		&伪类选择器/伪元素选择器{}
	}
}

选择器 选择器伪类选择器/伪元素选择器{} //&代表没有空格

注意：伪类和伪元素选择器的:和::不能少
- 减少代码量
- 更好的组织性

嵌套是没有限制的

### 注释
- `//`
- `/**/`

### 清除浮动的方法
1. 创建一个clearfix的类，添加到要清除的元素上
2. 设置clearfix的伪元素after的样式为`content:"";`、`display:talbe;`、`clear:both;`。（display:block也可）

[清除浮动的方法和原理](https://zhuanlan.zhihu.com/p/137926413)

###codepen
1. 设置-CSS-CSS预处理器-CSSS-Close
2. 写代码-Save
3. 地址栏链接可以直接分享给其他人
4. CSS代码区-↓-View Compiled CSS

### 小问题
list-style作用域ul/ol，而非li！！

## SASS第一步 | Mixins 插件/扩展和函数

### mix-ins
代表一段可复用的代码的变量

@mixin 名字[($参数名)] {
	//样式代码
}

@include mixin名字;

注意：最常用

### functions

**内置函数**
darken(颜色值, 加深程度百分比);
lighten(颜色值, 浅化程度百分比);

**自定义函数**
@function 函数名($参数名){
	return 返回值;
}

函数名(参数) * 1单位;

注意：
1. 用处不大
2. 数值计算与单位：`运算结果*1单位`

### extends
1. 写一个包含一系列样式的占位符
2. 其他选择器扩展这个占位符

%扩展名 {
	//一系列代码
}

@extend %扩展名;

### mixin和extend的区别
a {@include m}
b {@include m}
结果是分别复制了m中的代码，copy代码
a {@extend %e}
b {@extend %e}
结果是a, b {e中的代码}共用，copy扩展名
	适用于选择器之间inherently and thematically related，如btn-main和btn-hot是相关的，所以从长远看不会导致维护性问题

### DRY
DRY原则: Don't Repeat Yourself.
重要的是编写的源代码，而不是最终编译的CSS代码

## 命令行的详细介绍
### 打开文件（夹）
**打开文件**
直接输入文件名，但文件名必须指定了默认打开方式

**打开文件夹**
cd desktop/test
cd ..
d: //不用加cd

### 列出目录下的文件
dir
dir /s /b | find /i "mp4"
/b只显示文件名（包含后缀
/s包含子文件夹
/i大小写不敏感
/d标记文件夹


### 创建文件（夹）
**创建文件**
type nul>文件
echo 文件内容>文件

**创建文件夹**
md/mkdir 文件夹
多个用空格隔开

### 移动复制文件（夹）
**移动复制文件**
move 文件（夹） 路径
copy 文件 路径

**移动复制文件夹**


### 删除文件（夹）
**删除文件**
del 文件

**删除文件夹**
rd 文件夹
	/S：除目录本身外，还将删除指定目录下的所有子目录和文件。用于删除目录树。
	/Q：安静模式，带 /S 删除目录树时不要求确认
rd css /S /Q

### 清除指令
cls

### 系统软件
mspaint			画图
notepad			记事本
snippingtool	截图工具
stikynot.		便利贴

## NPM包 | 本地安装SASS
1. 先安装node，使用`node -v`检测是否安装成功
2. 进入新项目目录，使用`npm init`创建package.json文件
3. 使用`npm install node-sass --save-dev`安装Node SASS

演示
4. 使用`npm install jquery --save`安装Jquery
5. 使用`npm uninstall Jquery --save`卸载Jquery
6. 删除node_modules文件夹，使用`npm install`安装依赖

## NPM脚本 | 本地编写和编译SASS
SASS有两种语法
- SASS：扩展名为.sass
- SCSS：SassyCSS，扩展名为.scss

### 如何使用Node SASS？
1. 改变ackage.json中的scripts内容，格式如下：
	"指令名": "node-sass 要编译的scss路径/输入文件 保存的css路径/输出文件 -w"
		-w后缀中w表示watch，会自动检测改动并自动执行命令
		后者会被简单覆盖
2. cmd中输入指令名

### 其他npm包
- 自动给css属性加上浏览器前缀
- 根据改动自动加载页面

## 最简单的方法 | 当文件改变自动重载页面
1. 执行命令`npm install live-server -g`安装live server
2. 在目录下执行命令`live-server`




