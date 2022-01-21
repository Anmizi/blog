---
title: CSS 中的浮动和清除浮动
categories:
  - 前端
tags:
  - CSS
abbrlink: bbeacaa3
date: 2020-06-23 18:08:43
index_img: https://gitee.com/Stubborner/images/raw/master/images/5d33d5dc1531213134.png
---
## 浮动是什么

浮动核心就一句话：**浮动元素会脱离文档流并向左/向右浮动，直到碰到父元素或者另一个浮动元素**。请默念3次！
<!-- more -->
## 浮动的特征

1. 脱离文档流
   - 脱离文档，也就是说浮动不会影响普通元素的布局
2. 浮动可以内联排列
   - 浮动会向左/向右浮动，直到碰到另一个浮动元素为止，这是浮动可以内联排列的特征。也就是说，浮动可以设置宽高，并且能够一行多个，是介于`block`和`inline`之间的存在

3. 浮动会导致父元素高度坍塌
   - 浮动会脱离文档流，这个问题对整个页面布局有很大的影响。
   - 浮动元素脱离文档流，并不占据文档流的位置，自然父元素也就不能被撑开，所以没有了高度。
   
## 用clear清除浮动
clear属性不允许被清除浮动的元素的左边/右边挨着浮动元素，底层原理是在被清除浮动的元素上边或者下边添加足够的清除空间。这句话，请默念5次！
要注意了，我们是通过在别的元素上清除浮动来实现撑开高度的， 而不是在浮动元素上。

###  使用带clear属性的空元素

```html
<style>
    main{
        border: 4px solid pink;
        width: 1000px;
        margin: 0 auto;
    }
    div{
        height: 100px;
        width: 100px;
        background-color: red;
        border: 4px solid green;
        float: left;
    }
    //利用带clear属性的空元素清除浮动
    /* .clear{
        content: "";
        clear: both;
    } */
</style>
<body>
    <main>
        <div></div>
        <div></div>
        <div></div>
        <p class="clear"></p>
    </main>
</body>
```

### 使用CSS的:after伪元素

结合`:after`伪元素（注意这不是伪类，而是伪元素，代表一个元素之后最近的元素）和 IEhack ，可以完美兼容当前主流的各大浏览器，这里的 IEhack 指的是触发 hasLayout。

需要注意的是为了IE6和IE7浏览器，要给main标签添加一条zoom:1;触发haslayout。(IE已经被微软抛弃了,妙呀)

```html
<style>
    main{
        border: 4px solid pink;
        width: 1000px;
        margin: 0 auto;
    }
    div{
        height: 100px;
        width: 100px;
        background-color: red;
        border: 4px solid green;
        float: left;
    }
    /* 添加一个:after伪元素实现元素末尾添加一个看不见的块元素（Block element）清理浮动 */
    main:after{
        content: "";
        display: block;
        height: 0;
        clear: both;
        visibility: hidden;
    }
    main{
        /* 触发haslayout */
        zoom: 1;
    }
</style>
<body>
    <main>
        <div></div>
        <div></div>
        <div></div>
    </main>
</body>
</html>
```


## BFC清除浮动

BFC全称是块状格式化上下文，它是按照块级盒子布局的。我们了解他的特征、触发方式、常见使用场景这些就够了。
BFC的主要特征

- BFC就是页面上的一个独立的容器，容器内的子元素不会影响到外面的元素，外面的元素也不- -会影响到容器内的子元素。
- 盒子垂直方向的距离由margin决定，属于同一个BFC的相邻盒子的上下margin会发生折叠；分别触发两个元素的BFC，就可以解决垂直边距折叠的问题
- BFC可以包含浮动；通常用来解决浮动父元素高度坍塌的问题。
其中，BFC清除浮动就是用的“包含浮动”这条特性。

### BFC的触发方式

我们可以给父元素添加以下属性来触发BFC：

1. `float` 为 `left` | `right`
2. `overflow` 为 `hidden` | `auto` | `scorll`
3. `display` 为 `table-cell` | `table-caption` | `inline-block` | `flex` | `inline-flex`
4. `position` 为 `absolute` | `fixed`



清除浮动的方式有很多，我们只要根据不同的使用场景使用即可

<u>文章参考来源:</u>

[^1] [ <u>CSS清除浮动方法总结</u> ](https://juejin.im/post/582d98d5da2f600063e28f27)

[^2] [<u>CSS 中的浮动和清除浮动，梳理一下！</u>](https://juejin.im/entry/580479b85bbb50005b7c5083)

