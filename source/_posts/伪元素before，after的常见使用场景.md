---
title: 伪元素before，after的常见使用场景
date: 2017-10-12 16:43:52
tags: css3
---

伪元素（css3之前也叫伪类），就是假的元素，不是元素的元素，听起来拗口，其实说，它并不存在于DOM节点中，只是在CSS渲染层加入。在强调语义化的HTML5中，你尽量不要使用它展示一些有实际意义的内容。
那么问题来了（这句好熟悉-。-），它有什么实用场景呢？下面我介绍下我工作中使用到的地方

### 一、 清除浮动

这大概是伪元素使用最广泛的地方了，创建BFC（块级格式化上下文）来清除浮动
``` css
clearfix::after{
	content: ' ';
	display: table;
	clear: both;
}
```
OK，完成，但是工作中我们会使用比较复杂一点的写法
``` css
clearfix::before, /*加before是为了防止顶部空白的崩溃（两个盒子之间都有margin的值，会发生重叠）*/
clearfix::after{
	content: ' ';
	display: table;
}

clearfix::after{
	clear: both;
}
```

### 二、 扩大小按钮的可点击区域，以增强用户体验 

有没有这样的场景，UI界面有个小小的东西，可能是按钮，它的样式大小固定，同时也又有相应的事件，而手指的宽度决定了用户不能精确的点击到，就会发生用户多次点击却得不到相应情况。
在不改变样式的情况下，我们利用伪元素before扩大它的可点击区域
``` css
button {
	position: relative;
}

button::before{
	content： '';
	position: absolute;
	top: -10px;
	right: -10px;
	bottom: -10px;
	left: -10px;
}
```
### 三、 hover或者active的时候做出区别样式

比如导航栏，在hover如果只是改变颜色，会有些单调，现在大部分网页会加些衬线什么的，这样的东西不需要正真的元素，伪元素就粉墨登场了
``` css
nav-item:hover::after,
nav-item.active::after{
    content: " ";
    display: block;
    height: 4px;
    width: 100%;
    background-color: #f2b335;
}
```
### 四、 文字前面加图标

这里就不贴代码了，可以去[icomoon](https://icomoon.io/)下载相应的图标直接引用。
