---
title: Hello World
---
### 盒模型

margin/border/padding/content<br />
![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215178-5560c3fd-e4b2-499d-9532-351457a6e7c5.png#align=left&display=inline&height=186&linkTarget=_blank&originHeight=186&originWidth=244&size=0&width=244)

### 行内元素与块级元素

1. 块级元素

```html
div、ul、li、h1~h6、p
```

* 总是在新行上开始；
* 高度，行高以及外边距和内边距都可控制；
* 宽度缺省是它的容器的100%，除非设定一个宽度。
* 它可以容纳内联元素和其他块元素

1. 行内元素

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


![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215195-4fab7de2-1d99-4034-9d52-b2e05f914efa.png#align=left&display=inline&height=194&linkTarget=_blank&originHeight=194&originWidth=637&size=0&width=637)

1. float

> 浮动元素不在文档的普通流中，文档的普通流中的元素表现的就像浮动元素不存在一样。浮动的框可以左右移动（根据float属性值而定），直到它的外边缘碰到包含框或者另一个浮动元素的框的边缘。


![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215096-c94fcccc-d43b-410d-ae43-b436a4bca449.png#align=left&display=inline&height=383&linkTarget=_blank&originHeight=383&originWidth=527&size=0&width=527)<br />
![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215127-fc14ae33-9d69-4321-a24a-0b9a83dea220.png#align=left&display=inline&height=372&linkTarget=_blank&originHeight=372&originWidth=519&size=0&width=519)

1. position

![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215477-a994c36a-7869-466c-9331-604566e5ce0d.png#align=left&display=inline&height=245&linkTarget=_blank&originHeight=275&originWidth=839&size=0&width=746)

![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215604-4deece9d-faf5-45d2-b74c-dc8b4416ea33.png#align=left&display=inline&height=447&linkTarget=_blank&originHeight=447&originWidth=663&size=0&width=663)

![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215140-6c0605ee-f0de-4155-8ed7-a225c1616942.png#align=left&display=inline&height=399&linkTarget=_blank&originHeight=399&originWidth=668&size=0&width=668)

![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215441-d1fa26a5-3a23-4666-9576-fb60a860931b.png#align=left&display=inline&height=450&linkTarget=_blank&originHeight=450&originWidth=663&size=0&width=663)

### flex布局

[flex实例教程-阮一峰](http://www.ruanyifeng.com/blog/2015/07/flex-examples.html)<br />
`http://www.ruanyifeng.com/blog/2015/07/flex-examples.html`

1. 水平方向，左侧固定，右侧内容撑满<br />
![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215457-623a232c-c142-4ff2-aea1-b876618c8181.png#align=left&display=inline&height=342&linkTarget=_blank&originHeight=389&originWidth=826&size=0&width=726)

```html
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

1. 垂直方向，底部固定，中间内容撑满<br />
![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215688-bf7971f2-4005-44a2-8db9-0ada38e0856c.png#align=left&display=inline&height=362&linkTarget=_blank&originHeight=488&originWidth=979&size=0&width=726)

```html
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

1. 圣杯布局<br />
![](https://cdn.nlark.com/yuque/0/2019/png/128974/1550037215219-25326987-bdf7-4996-9e44-1c676ac2b6a1.png#align=left&display=inline&height=347&linkTarget=_blank&originHeight=445&originWidth=931&size=0&width=726)

```html
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

