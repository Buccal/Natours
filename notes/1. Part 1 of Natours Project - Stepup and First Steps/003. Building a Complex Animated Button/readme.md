## 创建一个复杂的按钮动画

- 什么是伪元素和伪类？
- 为什么在伪元素之后使用::？
- 如何使用transition属性实现一个有创意的悬浮动画？

页面上的按钮大都大同小异，只有颜色样式有所区别，所以以颜色作为类名区分

注意
1. transform的坐标系是x轴→，y轴↓
2. 按下按钮会经过:link→:hover→:active→:visited，所以translateY的值变化为0→-3→-1→0

box-shadow: 在x轴上的偏移 阴影高度 阴影模糊blur程度 颜色

::after伪元素会在所选择的元素后面创造一个虚拟的元素
- content、display属性是必须指定的，不管它的值是什么，否则这个伪元素将不起作用
- 这个伪元素会被当作所选择元素的子元素

z-index：层叠顺序

scale：比例尺

outline：没发现了，为什么？？？？？

两种动画
- transition：想要动画的属性(all) 动画持续时间，放在初始状态的元素样式中
	transition: transition-property transition-duration;
- @keyframes： specify the steps of the animations with the @keyframes rule.

问题：当动画延迟时，一开始元素会放在动画结束位置，而不是不可见
解决方案：animation-fill-mode: backwards; 

## 后续
因为样式文件越来越复杂，后面会讲到css的结构问题
