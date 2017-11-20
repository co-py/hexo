---
title: CSS3实现图片闪光划过效果
date: 2017-10-06 14:59:36
tags: CSS3
---

百度 'CSS3实现图片闪光划过效果',比较好的Blog是也讲清楚了实现原理，但都是通过添加一个标签来实现渐变，让他划过图片。
我觉得，使用css的伪类::before，实现更好。
不用添加无意义标签，代码更简洁。


### 先上代码 Copy到html文件看看效果

``` css
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>CSS3闪光特效</title>
    </head>
    <style>
     .project-item{
        width: 262px;
        height: 190px;
        overflow: hidden;
        margin: 0 auto;
        box-sizing: border-box;
        border-radius: 5px;
        position: relative;
        background-color: #70c3ff;
    }
     .project-item::before{
        content: '';
        position: absolute;
        top: 0;
        left: -262px;
        width: 100%;
        height: 100%;
        background-image: -moz-linear-gradient(0deg,rgba(255,255,255,0),rgba(255,255,255,0.5),rgba(255,255,255,0));
        background-image: -webkit-linear-gradient(0deg,rgba(255,255,255,0),rgba(255,255,255,0.5),rgba(255,255,255,0));
        transform: skewx(-25deg);
        -o-transform: skewx(-25deg);
        -moz-transform: skewx(-25deg);
        -webkit-transform: skewx(-25deg);
    }
     .project-item:hover::before{
        left: 262px;
        -moz-transition:0.3s ease;
        -o-transition:0.3s ease;
        -webkit-transition:0.3s ease;
        transition:0.3s ease;
    }
    </style>
    <body>
        <div class="project-item">
        </div>
    </body>
</html>
``` 





## 下面说下实现原理

### 给要应用闪光效果的东西，div img布拉布拉 添加样式
### 重要的两个如下

``` css
    overflow: hidden;
	position: relative;
``` 
overflow： 让闪光层只在这个元素有效，不要污染到其他元素
relative： 让闪光层相对他的定位


### 设置闪光层

``` css
    content: '';
    position: absolute;
    top: 0;
    left: -262px;
    width: 100%;
    height: 100%;
``` 
left : 闪光层的位移，负的宽度
absolute： 闪光层大小和父元素一样，绝对定位


### 设置hover效果

``` css
    .project-item:hover::before{
	// 效果
}
``` 
上面的意思是，.project-item类的元素添hover时候，它的before伪类要行进的效果


### so easy哈，这效果还不错，当然一般加上漂浮的效果更好，看看加上漂浮效果

``` css
<!DOCTYPE html>
<html>
    <head>
        <meta charset="utf-8">
        <title>CSS3闪光特效</title>
    </head>
    <style>
     .project-item{
        width: 262px;
        height: 190px;
        overflow: hidden;
        margin: 0 auto;
        box-sizing: border-box;
        border-radius: 5px;
        position: relative;
        background-color: #70c3ff;
    }
     .project-item::before{
        content: '';
        position: absolute;
        top: 0;
        left: -262px;
        width: 100%;
        height: 100%;
        background-image: -moz-linear-gradient(0deg,rgba(255,255,255,0),rgba(255,255,255,0.5),rgba(255,255,255,0));
        background-image: -webkit-linear-gradient(0deg,rgba(255,255,255,0),rgba(255,255,255,0.5),rgba(255,255,255,0));
        transform: skewx(-25deg);
        -o-transform: skewx(-25deg);
        -moz-transform: skewx(-25deg);
        -webkit-transform: skewx(-25deg);
    }
     .project-item:hover::before{
        left: 262px;
        -moz-transition:0.3s ease;
        -o-transition:0.3s ease;
        -webkit-transition:0.3s ease;
        transition:0.3s ease;
    }
    .cs-item:hover {
    transform: translateY(-6px);
    -webkit-transform: translateY(-6px);
    -moz-transform: translateY(-6px);
    box-shadow: 0 26px 40px -24px rgba(0, 36, 100, .5);
    -webkit-box-shadow: 0 26px 40px -24px rgba(0, 36, 100, .5);
    -moz-box-shadow: 0 26px 40px -24px rgba(0, 36, 100, .5);
    -moz-transition:0.5s ease;
    -o-transition:0.5s ease;
    -webkit-transition:0.5s ease;
    transition:0.5s ease;
	}
    </style>
    <body>
        <div class="project-item cs-item">
        </div>
    </body>
</html>
``` 