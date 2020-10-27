---
title: 负margin的使用
date: 2020-10-27 14:12:13
tags:
- 前端
- css
categories:
- 前端
- css相关
- 尺寸问题
---
![](/images/facade.jpg) <!-- more -->

## 负margin不占位
<div class="group group-1">
	<div class="left">
		<div class="box">margin-right: -15px;</div>
	</div>
	<div class="right"></div>
</div>
{% spoiler "CSS代码" %}
```css
.group-1 {
	font-size: 0;
}
.group-1 .left {
	display: inline-block;
	padding-top: 1px;
	width: 200px;
	height: 50px;
	background: #f99;
	vertical-align: bottom;
}
.group-1 .left .box {
	margin: 5px -10px 0 0;
	height: 25px;
	background: #3f3;
	font-size: 12px;
}
.group-1 .right {
	display: inline-block;
	width: 100px;
	height: 35px;
	background: #9ff;
}
```
{% endspoiler %}

## 负margin实现栅格系统
<div class="group group-2">
	<div>
		<div class="row">
			<div class="col">
				<div></div>
			</div>
			<div class="col">
				<div></div>
			</div>
			<div class="col">
				<div></div>
			</div>
			<div class="col">
				<div></div>
			</div>
		</div>
	</div>
</div>
{% spoiler "CSS代码" %}
```css
.group-2 > div {
	height: 60px;
	border: 1px dashed #ccc;
}
.group-2 .row {
	margin-left: -10px;
	margin-right: -10px;
}
.group-2 .row:after {
	content: '';
	display: block;
	clear: both;
}
.group-2 .col {
	float: left;
	padding: 0 10px;
	width: 25%;
	box-sizing: border-box;
}
.group-2 .col > div {
	height: 36px;
	background: #d3dce6;
	border-radius: 3px;
}
```
{% endspoiler %}

## 前后左右负margin谁显示上边
1. 左右 左 margin-right:-15px;
<div class="group group-3 t1">
	<div class="left"></div>
	<div class="right"></div>
</div>
结论：左侧盒子负margin-right后，右侧盒子向左边移动，并覆盖在左侧盒子上。
2. 左右 右 margin-left:-15px;
<div class="group group-3 t2">
	<div class="left"></div>
	<div class="right"></div>
</div>
结论：右侧盒子负margin-left后，右侧盒子向左边移动，并覆盖在左侧盒子上。
3. 上下 上 margin-bottom: -15px;
<div class="group group-3 t3">
	<div class="top"></div>
	<div class="bottom"></div>
</div>
结论：上方盒子负margin-bottom后，下方盒子向上移动，并覆盖在上方盒子上。
4. 上下 下 margin-top: -15px;
<div class="group group-3 t4">
	<div class="top"></div>
	<div class="bottom"></div>
</div>
结论：下方盒子负margin-right后，下方盒子向上移动，并覆盖在上方盒子上。
5. 左右 右 margin-right: -15px; 
<div class="group group-3 t5">
	<div class="left"></div>
	<div class="right"></div>
</div>
看起来没变化，但后面在有盒子的时候就会重叠到右盒子上，上下时同理，负margin的那一部分将不占位
6. 盒子里面有内容时，下面的盒子覆盖上面的盒子，但是上面盒子的内容会覆盖下面的盒子
<div class="group group-3 t6">
	<div class="top">
		<span></span>
	</div>
	<div class="bottom"></div>
</div>

## 选项卡去边框
<div class="group group-4">
	<div class="g-tabs">
		<span class="active">新闻</span>
		<span>财经</span>
		<span>科技</span>
	</div>
	<div class="g-content">随着国内疫情得到有效控制,三季度,全国多地的交通拥堵状况,也开始上升,据高德数据显示,三季度，全国有7.48%的城市,通勤高峰处于拥堵状态,有58.17%的城市</div>
</div>
{% spoiler "html与css代码" %}
```HTML
<div class="group group-4">
	<div class="g-tabs">
		<span class="active">新闻</span>
		<span>财经</span>
		<span>科技</span>
	</div>
	<div class="g-content">随着国内疫情得到有效控制,三季度,全国多地的交通拥堵状况,也开始上升,据高德数据显示,三季度，全国有7.48%的城市,通勤高峰处于拥堵状态,有58.17%的城市</div>
</div>
```
```CSS
.group-4 {
	height: 200px;
}
.group-4 .g-tabs {
	margin-bottom: -1px;
	border-left: 1px solid red; /*关键*/
}
.group-4 .g-tabs:after {
	content: '';
	display: block;
	clear: both;
}
.group-4 .g-tabs span {
	float: left;
	width: 80px;
	border-top: 1px solid red;
	border-right: 1px solid red;
	text-align: center;
	line-height: 36px;
}
.group-4 .g-tabs span.active {
	background: #fff;
}
.group-4 .g-content {
	padding: 10px;
	border: 1px solid red;
	box-sizing: border-box;
}
```
{% endspoiler %}


<style>
.group {
	position: relative;
	padding: 10px;
	width: 500px;
	max-width: 100%;
	height: 100px;
	border: 1px solid #999;
	box-sizing: border-box;
	overflow: auto;
}

/*1*/
.group-1 {
	font-size: 0;
}
.group-1 .left {
	display: inline-block;
	padding-top: 1px;
	width: 200px;
	height: 50px;
	background: #f99;
	vertical-align: bottom;
}
.group-1 .left .box {
	margin: 5px -10px 0 0;
	height: 25px;
	background: #3f3;
	font-size: 12px;
}
.group-1 .right {
	display: inline-block;
	width: 100px;
	height: 35px;
	background: #9ff;
}

/*two*/
.group-2 > div {
	height: 60px;
	border: 1px dashed #ccc;
}
.group-2 .row {
	margin-left: -10px;
	margin-right: -10px;
}
.group-2 .row:after {
	content: '';
	display: block;
	clear: both;
}
.group-2 .col {
	float: left;
	padding: 0 10px;
	width: 25%;
	box-sizing: border-box;
}
.group-2 .col > div {
	height: 36px;
	background: #d3dce6;
	border-radius: 3px;
}

/*three*/
.group-3 {
	font-size: 0;
}
.group-3 .left, .group-3 .right {
	display: inline-block;
}
.group-3 .left {
	width: 150px;
	height: 50px;
	background: #9f9;
}
.group-3 .right {
	width: 150px;
	height: 60px;
	background: rgba(100, 100, 255, 0.5);
}
.group-3 .top {
	width: 150px;
	height: 40px;
	background: #9f9;
}
.group-3 .bottom {
	width: 200px;
	height: 40px;
	background: rgba(100, 100, 255, 0.5);
}
.group-3.t1 .left {
	margin-right: -15px;
}
.group-3.t2 .right {
	margin-left: -15px;
}
.group-3.t3 .top {
	margin-bottom: -15px;
}
.group-3.t4 .bottom {
	margin-top: -15px;
}
.group-3.t5 .right {
	margin-right: -15px;
}
.group-3.t6 .top {
	border: 4px solid #f99;
	margin-bottom: -15px;
}
.group-3.t6 .top span {
	display: inline-block;
	width: 50px;
	height: 100%;
	background: red;
}
.group-3.t6 .bottom {
	border: 2px solid blue;
}

/*4*/
.group-4 {
	height: 200px;
}
.group-4 .g-tabs {
	margin-bottom: -1px;
	border-left: 1px solid red;
}
.group-4 .g-tabs:after {
	content: '';
	display: block;
	clear: both;
}
.group-4 .g-tabs span {
	float: left;
	width: 80px;
	border-top: 1px solid red;
	border-right: 1px solid red;
	text-align: center;
	line-height: 36px;
}
.group-4 .g-tabs span.active {
	background: #fff;
}
.group-4 .g-content {
	padding: 10px;
	border: 1px solid red;
	box-sizing: border-box;
}
</style>


