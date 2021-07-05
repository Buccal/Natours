## CSS动画

how to create CSS animations using the @keyframes rule and the animation property.

1. 定义动画效果：@keyframes 动画名称{}
	- 指定每一刻的动画：0%-100%
		- opacity
		- transform
2. 指定和设置动画：
	- animation-name: 动画名称;
	- animation-duration: 动画持续时间;
	- animation-delay: 等待动画开始时间;
	- animation-iteration-count: 动画播放次数;
	- animation-timing-function: 动画变化率（eg. fast→slow）
	- animation: animation-name animation-duration animation-timing-function;
		animation: animation-name animation-duration ;
		animation: animation-name animation-duration animation-timing-function animation-delay;

animation-timing-function: linear | <cubic-bezier-timing-function> | <step-timing-function>
	<cubic-bezier-timing-function> = ease | ease-in | ease-out | ease-in-out | cubic-bezier(<number>, <number>, <number>, <number>)
	<step-timing-function> = step-start | step-end | steps(<integer>[, <step-position>]?)
		<step-position> = jump-start | jump-end | jump-none | jump-both | start | end

ease === cubic-bezier(0.25, 0.1, 0.25, 1.0) （默认）
ease-in === cubic-bezier(0.42, 0, 1.0, 1.0)
ease-out === cubic-bezier(0, 0, 0.58, 1.0)

动画有时候会有偏移，修复这个摇晃的感觉
-webkit-backface-visibility: hidden; // 兼容Safari
backface-visibility: hidden; //在元素transform的过程中隐藏背后的元素

transform: rotation(120deg); //旋转120°

动画不但可以在页面载入时播放，也可以在悬浮等情况下播放


