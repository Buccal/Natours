## 1. Setup and First Steps

### Building the Header1
- the best way to perform a basic reset using the universal selector.
- how to set up project-wide font definitions.
- how to clip parts of elements using the new clip-path property

- reset
- background image

每个HTML标签都添加一个Class属性，在CSS中使用类名而非标签名


box-sizing：change the box model so that the borders and the paddings are no longer added to the total width or the total height that we specify for a box

>为什么字体不声明在通用选择器中？

linear-gradient() => linear-gradient( [ <angle> | to <side-or-corner> ]? , <color-stop-list> )
background-image: linear-gradient()/imageUrl, imageUrl; //放在前面的在上面
eg. linear-gradient(to bottom, rgba(255,255,0,0.5), rgba(0,0,255,0.5)),

clip-path: <clip-source>|<basic-shape>|<geometry-box>
- clip-source:指向svg图片的url
- basic-shape: <inset()> | <circle()> | <ellipse()> | <polygon()>
- geometry-box: <shape-box>（margin-box、border-box、padding-box、content-box）|fill-box|stroke-box|view-box

<polygon()> = polygon( <fill-rule>? , [ <length-percentage> <length-percentage> ]# )指定多边形的顶点坐标（左上开始顺时针）
eg. circle(40%)、ellipse(130px 140px at 10% 20%)、polygon(50% 0, 100% 50%, 50% 100%, 0 50%)

>常见形状实现：https://bennettfeely.com/clippy/

#### 后续会讲到的
CSS architecture

Inheritance（eg. font）


#### 总结
**新学的样式**
box-sizing
linear-gradient /'lɪnɪə/ /'greɪdɪənt/ 线性渐变；线性梯度；线性渐变填充
clip-path
polygon /'pɒlɪg(ə)n/n. 多边形

### Building the Header2
- the easiest way to center anything with the transform, top and left


- small logo
- primary heading
	如何将两个标题设为两行（改块元素）

为了SEO（Search Engine Optimization）或网络问题图片记得添加alt属性


#### 后续会讲到的
绝对定位和相对定位的区别、 文档流和浮动
