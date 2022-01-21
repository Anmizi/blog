---
title: 移动基础之flex布局
categories:
  - 前端
tags:
  - Html
index_img: 'https://gitee.com/Stubborner/images/raw/master/images/20210602160628.png'
abbrlink: 9c1d1cb1
date: 2021-06-02 09:32:40
---

## 基本概念

### 什么是flex布局

Flex是Flexible Box的缩写，意为’灵活的盒子‘，所以flex布局一般也叫弹性布局

### 什么是flex容器

采用flex布局的元素，称为flex容器

.box{display: flex | inline-flex} 

### 什么是flex项目(flex item)

flex容器的所有子元素自动成为容器成员，称为flex项目

项目默认沿主轴排列

![img](https://gitee.com/Stubborner/images/raw/master/images/bg2015071004.png)

## 容器属性

### display

- flex	容器为块级元素特性，占一行
- inline-flex   容器为行内块元素特性，宽度被flex项目撑开

### flex-direction

<span style="background:pink;color:#333;">flex-direction</span> 属性决定了主轴的方向(即项目的排列方向)

```css
.box{
	flex-direction: row | row-reverse | column | column-reverse;
}
```

它可能有4个值。

- `row`（默认值）：主轴为水平方向，起点在左端。
- `row-reverse`：主轴为水平方向，起点在右端。
- `column`：主轴为垂直方向，起点在上沿。
- `column-reverse`：主轴为垂直方向，起点在下沿。

### flex-wrap

默认情况下，项目都排列在一条线(又称“轴线”)上，<span style="background:pink;color:#333;">flex-wrap </span>属性定义，如果在一条轴线排列不下，如何换行。

```css
.box{
    flex-wrap: nowrap | wrap | wrap-reverse;
}
```

它有三个取值

- nowrap(默认)：不换行
- wrap：换行，第一行在上方
- wrap-reverse：换行，第一行在下方

*tips:*

当设置flex-wrap: nowrap时，如果flex项目是定宽的盒子且一行排列不下时，flex项目的宽度会被压缩

### flex-flow

**flex-flow** 属性是 **flex-direction** 属性和 **flex-wrap** 属性的简写形式，默认值为row nowrap

```css
.box{
	flex-flex: <flex-direction> | <flex-wrap>
}
```

### justify-content

<span style="background:pink;color:#333">justify-content</span> 属性定义了项目在主轴上的对齐方式

```css
.box{
    justify-content: flex-start | flex-end | center | space-between | space-around;
}
```

![img](https://gitee.com/Stubborner/images/raw/master/images/bg2015071010.png)

它可能取5个值，具体对齐方式与轴的方向有关。下面假设主轴为从左到右。

- `flex-start`（默认值）：左对齐
- `flex-end`：右对齐
- `center`： 居中
- `space-between`：两端对齐，项目之间的间隔都相等。
- `space-around`：每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。

### align-items

<span style="background:pink;color:#333">align-items</span> 属性定义项目在**交叉轴**上如何对齐

```css
.box{
    align-items: flex-start | flex-end | center | baseline | stretch;
}
```

![img](https://gitee.com/Stubborner/images/raw/master/images/bg2015071011.png)

它可能取5个值。具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下

- `flex-start`：交叉轴的起点对齐。
- `flex-end`：交叉轴的终点对齐。
- `center`：交叉轴的中点对齐。
- `baseline`: 项目的第一行文字的基线对齐。
- `stretch`（默认值）：如果项目未设置高度或设为auto，将占满整个容器的高度。

### align-content

align-content 属性定义了多根轴线(主轴线)的对齐方式，如果项目只有一跟轴线，该属性不起作用。

```css
.box{
    align-content: flex-start | flex-end | center | space-between | space-around;
}
```

![img](https://gitee.com/Stubborner/images/raw/master/images/bg2015071012.png)

该属性可能取6个值。

- `flex-start`：与交叉轴的起点对齐。
- `flex-end`：与交叉轴的终点对齐。
- `center`：与交叉轴的中点对齐。
- `space-between`：与交叉轴两端对齐，轴线之间的间隔平均分布。
- `space-around`：每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
- `stretch`（默认值）：轴线占满整个交叉轴。



## 项目属性

### order

order 属性定义项目的排列顺序，数值越小，排列越靠前

```css
.item{
    order: <integer>;
}
```

### flex-grow

<span style="background:pink;color:#333">flex-grow</span> 属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。

```css
.item{
	flex-grow: <number>;
}
```

如果所有项目的`flex-grow`属性都为1，则它们将等分剩余空间（如果有的话）。如果一个项目的`flex-grow`属性为2，其他项目都为1，则前者占据的剩余空间将比其他项多一倍。

### flex-shrink

<span style="background:pink;color:#333">flex-shrink</span>属性定义了项目的缩小比例，默认为1，即如果空间不足，该项目将缩小。

```css
.item {
  flex-shrink: <number>; /* default 1 */
}
```

如果所有项目的`flex-shrink`属性都为1，当空间不足时，都将等比例缩小。如果一个项目的`flex-shrink`属性为0，其他项目都为1，则空间不足时，前者不缩小。

负值对该属性无效



### flex-basis

<span style="background:pink;color:#333">flex-basis</span>属性定义了在分配多余空间之前，项目占据的主轴空间（main size）。浏览器根据这个属性，计算主轴是否有多余空间。它的默认值为`auto`，即项目的本来大小。

```css
.item {
  flex-basis: <length> | auto; /* default auto */
}
```

它可以设为跟`width`或`height`属性一样的值（比如350px），则项目将占据固定空间。

### flex属性

<span style="background:pink;color:#333">flex</span>属性是`flex-grow`, `flex-shrink` 和 `flex-basis`的简写，默认值为`0 1 auto`。后两个属性可选。

```css
.item {
  flex: none | [ <'flex-grow'> <'flex-shrink'>? || <'flex-basis'> ]
}
```

该属性有两个快捷值：`auto` (`1 1 auto`) 和 none (`0 0 auto`)。

建议优先使用这个属性，而不是单独写三个分离的属性，因为浏览器会推算相关值。

### align-self

<span style="background:pink;color:#333">align-self</span>属性允许单个项目有与其他项目不一样的对齐方式，可覆盖`align-items`属性。默认值为`auto`，表示继承父元素的`align-items`属性，如果没有父元素，则等同于`stretch`。

```css
.item {
  align-self: auto | flex-start | flex-end | center | baseline | stretch;
}
```

![img](https://gitee.com/Stubborner/images/raw/master/images/bg2015071016.png)

该属性可能取6个值，除了auto，其他都与align-items属性完全一致。

## 参考链接

[阮一峰Flex布局教程语法篇](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)