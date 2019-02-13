---
title: css布局
---
### 盒模型
margin/border/padding/content
![盒模型结构图](https://upload-images.jianshu.io/upload_images/8245634-fd92d0a88b04cce8.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### 行内元素与块级元素
1. 块级元素
```
div、ul、li、h1~h6、p
```
* 总是在新行上开始；
* 高度，行高以及外边距和内边距都可控制；
* 宽度缺省是它的容器的100%，除非设定一个宽度。
* 它可以容纳内联元素和其他块元素
2. 行内元素
```
span、a、img、表单元素(input、select)等
```
* 和其他元素都在一行上；
* 高，行高及外边距和内边距不可改变；
* 宽度就是它的文字或图片的宽度，不可改变
* 内联元素只能容纳文本或者其他内联元素

**对行内元素，需要注意如下：**
* 设置宽度width 无效。
* 设置高度height 无效，可以通过line-height来设置。
* 设置margin 只有左右margin有效，上下无效。
* 设置padding 只有左右padding有效，上下则无效。注意元素范围是增大了，但是对元素周围的内容是没影响的。

### 布局与定位：display、float、position
1. display
> 通过display属性对行内元素和块级元素进行切换

![常见display属性](https://upload-images.jianshu.io/upload_images/8245634-a6b93e5d8e1094e4.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

2. float
> 浮动元素不在文档的普通流中，文档的普通流中的元素表现的就像浮动元素不存在一样。浮动的框可以左右移动（根据float属性值而定），直到它的外边缘碰到包含框或者另一个浮动元素的框的边缘。

![](https://upload-images.jianshu.io/upload_images/8245634-202b9fef587f89d1.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)
![](https://upload-images.jianshu.io/upload_images/8245634-825924dec0b2f41a.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)


3. position

![image.png](https://upload-images.jianshu.io/upload_images/8245634-181e7d808f3cdfa9.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![相对定位，根据自身位置定位](https://upload-images.jianshu.io/upload_images/8245634-42aac828cd98aec6.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![绝对定位，根据父元素定位，脱离文档流](https://upload-images.jianshu.io/upload_images/8245634-e77db900ac52a6c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

![固定定位，根据浏览器窗口定位](https://upload-images.jianshu.io/upload_images/8245634-cf9581e13da5159d.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

### flex布局
[flex实例教程-阮一峰](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)
```http://www.ruanyifeng.com/blog/2015/07/flex-examples.html```

1. 水平方向，左侧固定，右侧内容撑满
![image.png](https://upload-images.jianshu.io/upload_images/8245634-f3e8ff0fb93395f7.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<div class="InputAddOn">
  <span class="InputAddOn-item">...</span>
  <input class="InputAddOn-field">
  <button class="InputAddOn-item">...</button>
</div>

.InputAddOn {
  display: flex;
}
.InputAddOn-field {
  flex: 1;
}
```

2. 垂直方向，底部固定，中间内容撑满
![image.png](https://upload-images.jianshu.io/upload_images/8245634-3c0db1d3333516c0.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<body class="Site">
  <header>...</header>
  <main class="Site-content">...</main>
  <footer>...</footer>
</body>

.Site {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}
.Site-content {
  flex: 1;
}
```

3. 圣杯布局
![image.png](https://upload-images.jianshu.io/upload_images/8245634-e9e27d6869748f23.png?imageMogr2/auto-orient/strip%7CimageView2/2/w/1240)

```
<body class="HolyGrail">
  <header>...</header>
  <div class="HolyGrail-body">
    <main class="HolyGrail-content">...</main>
    <nav class="HolyGrail-nav">...</nav>
    <aside class="HolyGrail-ads">...</aside>
  </div>
  <footer>...</footer>
</body>

.HolyGrail {
  display: flex;
  min-height: 100vh;
  flex-direction: column;
}
header,
footer {
  flex: 1;
}
.HolyGrail-body {
  display: flex;
  flex: 1;
}
.HolyGrail-content {
  flex: 1;
}
.HolyGrail-nav, .HolyGrail-ads {
  /* 两个边栏的宽度设为12em */
  flex: 0 0 12em;
}
.HolyGrail-nav {
  /* 导航放到最左边 */
  order: -1;
}
```

### 案例分析
