---
title: CSS 常见布局方式
excerpt: 本文较长，图片较多，主要是介绍 flex 布局和 grid 布局
categories:
- 技术文章
tags:
- css
---

## 前言
温馨提示：本文较长，图片较多，**不适合萌新看！**本来是想写一篇 CSS 布局方式的，但是奈何 CSS 布局方式种类太多并且实现方法太多，所以本文主要是介绍 flex 布局和 grid 布局，以及 CSS 常见的居中方式和两种经典的布局方式“圣杯布局”和“双飞翼布局”。想到哪写到哪，请各位见谅。

## 传统盒模型布局方式
我们的传统布局方式就是通过盒模型，使用 display 属性（文档流布局） + position 属性（定位布局） + float属性（浮动布局）。这个大家都比较熟悉，没有掌握的同学再去恶补一下基础

### 文档流布局
这是最基本的布局方式，就是按照文档的顺序一个一个显示出来，块元素独占一行，行内元素共享一行，这个相信大家都比较熟悉了，就不再赘述了

### 浮动布局
浮动方式布局就是使用 float 属性，使元素脱离文档流，浮动起来。这个大家也比较熟悉，就不再赘述了。

### 定位布局
我们也可以通过 position 属性来进行定位，这个大家也比较熟悉了，就不再赘述了。

## flex 布局
仅仅通过上述的三种布局方式还是有一些缺陷，比如我们不能只使用一个属性来实现垂直居中布局，所以就产生了第四种布局方式：flex 布局。

### 什么是 flex 布局
2009年，W3C 提出了一种新的方案----Flex 布局，可以简便、完整、响应式地实现各种页面布局。目前，它已经得到了所有浏览器的支持，这意味着，现在就能很安全地使用这项功能。
Flex 是 Flexible Box 的缩写，意为"弹性布局"，用来为盒状模型提供最大的灵活性。
flex 是一种新型的布局方式，使用该布局方式可以实现几乎所有你想要的效果。但是要注意其浏览器的兼容性，flex 只支持 ie 10+，所有还是要根据你的项目情况使用。

![](https://api2.mubu.com/v3/document_image/5b0e7fe5-25db-4722-bff5-a2328dd083a8-3807603.jpg)

### 使用 flex 布局
flex 的使用方法很简单，只需要将其 display 属性设置为 flex 就可以，也可以设置行内的 flex，记得 Webkit 内核的浏览器，必须加上 -webkit 前缀。注意，设为 Flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效。
```css
.ele{
    display: -webkit-flex;
    display: flex;
    display: inline-flex;
    display: -webkit-inline-flex;
}
```
在 flex 中，最核心的概念就是容器和轴，所有的属性都是围绕容器和轴设置的。其中，容器分为父容器和子容器。轴分为主轴和交叉轴（主轴默认为水平方向，方向向右，交叉轴为主轴顺时针旋转 90°）。
在使用 flex 的元素中，默认存在两根轴：水平的主轴（main axis）和垂直的交叉轴（cross axis）主轴开始的位置称为 main start，主轴结束的位置称为 main end。同理，交叉轴开始的位置称为 cross start，交叉轴结束的位置称为 cross end。在使用 flex 的子元素中，占据的主轴空间叫做 main size，占据的交叉轴空间叫做 cross size。

![](https://api2.mubu.com/v3/document_image/427bc57a-a5ea-49a8-9786-1d4ac565d4cb-3807603.jpg)

#### 父容器属性
父容器上有六个属性
- flex-direction：主轴的方向。
- flex-wrap：超出父容器子容器的排列样式。
- flex-flow：flex-direction 属性和 flex-wrap 属性的简写形式。
- justify-content：子容器在主轴的排列方向。
- align-items：子容器在交叉轴的排列方向。
- align-content：多根轴线的对齐方式。

**flex-direction 属性**
flex-direction 属性决定主轴的方向（主轴的方向不一定是水平的，这个属性就是设置主轴的方向，主轴默认是水平方向，从左至右，如果主轴方向设置完毕，那么交叉轴就不需要设置，交叉轴永远是主轴顺时针旋转 90°）。
```css
.ele {
    flex-direction: row;                // 默认值，主轴为水平方向，起点在左端。
    flex-direction: row-reverse;        // 主轴为水平方向，起点在右端。
    flex-direction: column;             // 主轴为垂直方向，起点在上。
    flex-direction: column-reverse;     // 主轴为垂直方向，起点在下。
}
```

![](https://api2.mubu.com/v3/document_image/308dfd45-2189-4aae-849f-0a3ef40af51c-3807603.jpg)

**flex-wrap 属性**
flex-wrap 属性决定子容器如果在一条轴线排不下时，如何换行。
```css
.ele {
    flex-wrap: nowrap;          // 默认，不换行
    flex-wrap: wrap;            // 换行，第一行在上方。
    flex-wrap: wrap-reverse     // 换行，第一行在下方。
}
```

![](https://api2.mubu.com/v3/document_image/8ba481ba-9bff-454f-a275-7e5433fbe4a1-3807603.jpg)

**justify-content 属性**
justify-content 属性定义了子容器在主轴上的对齐方式。
```css
.ele{
    justify-content: flex-start;      // 默认，左对齐
    justify-content: flex-end;        // 右对齐
    justify-content: center;          // 居中
    justify-content: space-between;   // 两端对齐，项目之间的间隔都相等。
    justify-content: space-around;    // 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与边框的间隔大一倍。
}
```

![](https://api2.mubu.com/v3/document_image/cfcf9946-64c5-47f9-bd2c-f47b8cc0c9b9-3807603.jpg)

**flex-flow 属性**
flex-flow 属性是 flex-direction 属性和 flex-wrap 属性的简写形式，默认值为 row nowrap。
```css
.ele {
    flex-flow: <flex-direction> || <flex-wrap>;
}
```

**align-items 属性**
align-items属性定义子容器在交叉轴上如何对齐。
具体的对齐方式与交叉轴的方向有关，下面假设交叉轴从上到下。
```css
.ele{
    align-items: flex-start;    // 交叉轴的起点对齐。
    align-items: flex-end;      // 交叉轴的终点对齐。
    align-items: center;        // 交叉轴的中点对齐。
    align-items: baseline;      // 项目的第一行文字的基线对齐。
    align-items: stretch;       // 默认，如果项目未设置高度或设为auto，将占满整个容器的高度。
}
```

![](https://api2.mubu.com/v3/document_image/25e2c016-6089-4a3c-826a-86109364b84b-3807603.jpg)

**align-content 属性**
align-content 属性定义了多根轴线的对齐方式。如果项目只有一根轴线，该属性不起作用。
```css
.ele{
    align-content: flex-start;   // 与交叉轴的起点对齐
    align-content; flex-end;     // 与交叉轴的终点对齐。
    align-content: center;       // 与交叉轴的中点对齐。
    align-content: space-between;// 与交叉轴两端对齐，轴线之间的间隔平均分布。
    align-content: space-around; // 每根轴线两侧的间隔都相等。所以，轴线之间的间隔比轴线与边框的间隔大一倍。
    align-content: stretch;     // 默认 轴线占满整个交叉轴。
}
```

![](https://api2.mubu.com/v3/document_image/aa255ff6-9084-45ec-9007-028601c7ea0c-3807603.jpg)

#### 子容器属性
子容器也有 6 个属性：
- order：子容器的排列顺序
- flex-grow：子容器剩余空间的拉伸比例
- flex-shrink：子容器超出空间的压缩比例
- flex-basis：子容器在不伸缩情况下的原始尺寸
- flex：子元素的 flex 属性是 flex-grow,flex-shrink 和  flex-basis 的简写
- align-self

**order 属性**
order 属性定义项目的排列顺序。数值越小，排列越靠前，默认为 0。
```css
.ele{
    order: num; 
}
```

![](https://api2.mubu.com/v3/document_image/594f5987-eda8-4215-92c6-9f4c58c42fbc-3807603.jpg)

**flex-grow 属性**
flex-grow 属性定义子容器的伸缩比例。按照该比例给子容器分配空间。
```css
.ele{
    flex-grow: <number>; /* default 0 */
}
```

![](https://api2.mubu.com/v3/document_image/9901c004-8d7a-49f1-9628-6b4871afeb2a-3807603.jpg)

**flex-shrink 属性**
flex-shrink 属性定义了子容器弹性收缩的比例。如图，超出的部分按 1:2 的比例从给子容器中减去。此属性要生效，父容器的 flex-wrap 属性要设置为 nowrap
```css
.ele{
    flex-shrink: <number>; /* default 0 */
}
```

![](https://api2.mubu.com/v3/document_image/268e00ee-0379-4fbc-ab1e-f45c2145d447-3807603.jpg)

**flex-basis 属性**
flex-basis 属性定义了子容器在不伸缩情况下的原始尺寸，主轴为横向时代表宽度，主轴为纵向时代表高度。
```css
.ele{
    flex-basis: <length> | auto; /* default auto */
}
```

![](https://api2.mubu.com/v3/document_image/8f776ce4-7ac6-4d14-ba7e-8784933f730a-3807603.jpg)

**flex 属性**
子元素的 flex 属性是 flex-grow,flex-shrink 和  flex-basis 的简写，默认值为 0 1 auto。后两个属性可选。
该属性有两个快捷值：auto (1 1 auto) 和 none (0 0 auto)。

**align-self 属性**
子容器的 align-self 属性允许单个项目有与其他项目不一样的对齐方式，可覆盖父容器 align-items 属性。默认值为 auto，表示继承父元素的 align-items属性，如果没有父元素，则等同于 stretch。
```css
.ele{
    align-self: auto;             // 继承父元素的 align-items 属性
    align-self: flex-start;       // 交叉轴的起点对齐。
    align-self: flex-end;         // 交叉轴的终点对齐。
    align-self: center;           // 交叉轴的中点对齐。
    align-self: baseline;         // 项目的第一行文字的基线对齐。
    align-self: stretch;          // 默认，如果项目未设置高度或设为auto，将占满整个容器的高度。
}
```

![](https://api2.mubu.com/v3/document_image/43299bb4-4531-4b24-8406-be60c444903d-3807603.jpg)

## grid 网格布局
flex 布局虽然强大，但是只能是一维布局，如果要进行二维布局，那么我们还需要使用 grid。
grid 布局又称为“网格布局”，可以实现二维布局方式，和之前的 表格table布局差不多，然而，这是使用 CSS 控制的，不是使用 HTML 控制的，同时还可以依赖于媒体查询根据不同的上下文得新定义布局。
网格布局还可以让我们摆脱现在布局中存在的文档流限制，换句话说，你的结构不需要根据设计稿从上往上布置了。这也意味着您可以自由地更改页面元素位置。这最适合你在不同的断点位置实现你最需要的布局，而不再需要为响应你的设计而担心HTML结构的问题。
和 table 布局不同的是，grid 布局不需要在 HTML 中使用特定的标签布局，所有的布局都是在 CSS 中完成的，你可以随意定义你的 grid 网格。
没有 HTML 结构的网格布局有助于使用流体、调整顺序等技术管理或更改布局。通过结合 CSS 的媒体查询属性，可以控制网格布局容器和他们的子元素，使用页面的布局根据不同的设备和可用空间调整元素的显示风格与定位，而不需要去改变文档结构的本质内容。
浏览器兼容性如下：

![](https://api2.mubu.com/v3/document_image/2e035db5-473b-49e8-bc43-dad277cd6d0a-3807603.jpg)

### grid 网格布局中的基本概念
#### 网格线(Grid Lines)
网格线组成了网格，他是网格的水平和垂直的分界线。一个网格线存在行或列的两侧。我们可以引用它的数目或者定义的网格线名称。

![](https://api2.mubu.com/v3/document_image/587445c5-23b1-4587-a2aa-63f3661a4801-3807603.jpg)

#### 网格轨道(Grid Track)
网格轨道是就是相邻两条网格线之间的空间，就好比表格中行或列。所在在网格中其分为grid column和grid row。每个网格轨道可以设置一个大小，用来控制宽度或高度。

![](https://api2.mubu.com/v3/document_image/176bf94f-ac78-46aa-9552-931a12a91619-3807603.jpg)

#### 网格单元格(Grid Cell)
网格单元格是指四条网格线之间的空间。所以它是最小的单位，就像表格中的单元格。

![](https://api2.mubu.com/v3/document_image/1aada5f5-1fdb-4c28-bda1-ecea7dbd1a25-3807603.jpg)

#### 网格区域(Grid Area)
网格区域是由任意四条网格线组成的空间，所以他可能包含一个或多个单元格。相当于表格中的合并单元格之后的区域。

![](https://api2.mubu.com/v3/document_image/88bebcca-aaf0-4266-9242-79e08559ea3c-3807603.jpg)

### 使用 grid 布局
使用 grid 布局很简单，通过display属性设置属性值为 grid 或 inline-grid 或者是 subgrid（该元素父元素为网格，继承父元素的行和列的大小） 就可以了。
网格容器中的所有子元素就会自动变成网格项目（grid item），然后设置列（grid-template-columns）和 行（grid-template-rows）的大小，设置 grid-template-columns 有多少个参数生成的 grid 列表就有多少个列。
注：当元素设置了网格布局，column、float、clear、vertical-align属性无效。
如果没有设置 grid-template-columns，那么默认只有一列，宽度为父元素的 100%，例如
比如我们设置如下的 HTML，
```html
<div class="grid-container">
    <div class="item item1">1</div>
    <div class="item item2">2</div>
    <div class="item item3">3</div>
    <div class="item item4">4</div>
    <div class="item item5">5</div>
    <div class="item item6">6</div>
</div>
```
在 CSS 中，我们不设置 grid-template-columns，只设置 grid-template-row
```css
.grid-container{
    display: grid;
    grid-template-rows: 50px 80px 100px;
    background: pink;
}
.item{
    border: 2px solid palegoldenrod;
    color: #fff;
    text-align: center;
    font-size: 20px;
}
```
显示如下

![](https://api2.mubu.com/v3/document_image/8f37b430-34cd-4c56-9607-b1dfb92b4346-3807603.jpg)

设置了 grid-template-columns 的话，设置了几个参数，就有几列（不超过 grid item 的个数），然后设置的 grid-template-row 参数就是每一列的高度（超出列数的高度无效）
比如：
```css
.grid-container{
    padding: 20px;
    display: grid;
    grid-template-rows: 50px 100px 60px 80px;
    grid-template-columns: 50px 40px 100px 80px;
    background: pink;
}
.item{
    border: 2px solid palegoldenrod;
    color: #fff;
}
```
虽然我们设置了四个 grid-template-rows，但是因为只有两行，所以只有前两个值生效。效果如下：

![](https://api2.mubu.com/v3/document_image/ac357612-35ff-4394-b974-d088a2deb8de-3807603.jpg)

当然，我们也可以像 flex 一样设置每一列的宽度：
```css
.grid-container{
    padding: 20px;
    display: grid;
    grid-template-rows: 50px 100px 60px;
    grid-template-columns: 1fr 1fr 2fr;
    background: pink;
}
```
注意到我们使用了一个新的单位：fr
css fr 单位是一个自适应单位，fr单位被用于在一系列长度值中分配剩余空间，如果多个已指定了多个部分，则剩下的空间根据各自的数字按比例分配。
tips：fr 是基于网格容器可用空间来计算的（flex 也是一样），所以我们可以和其他单位混合使用，如果需要的话
是不是找到了 flex 的感觉，这样设置效果如下：

![](https://api2.mubu.com/v3/document_image/daf51e70-e9b4-4322-a80a-3ad9127e14de-3807603.jpg)

### 行或列最小和最大尺寸
minmax() 函数来创建行或列的最小或最大尺寸，第一个参数定义网格轨道的最小值，第二个参数定义网格轨道的最大值。可以接受任何长度值，也接受 auto 值。auto 值允许网格轨道基于内容的尺寸拉伸或挤压。
```css
.grid-container{
    padding: 20px;
    display: grid;
    grid-template-rows: minmax(100px,200px) minmax(50px,200px);
    grid-template-columns: 1fr 1fr 2fr;
    background: pink;
    height: 300px;
}
```
我们将第一行的高度设置为 minmax(100px,200px)，第二行的高度设置为minmax(50px,200px)，容器总高度设置为 300px，这时每一列的高度要怎么算呢？
先判断总高度是小于第一列高度的最大值和第二列高度的最大值之和的，如果大于最大值之和，那么第一列和第二列的高度都为设置的最大值，如果是小于最小值之和的话，那么第一列和第二列的高度都为设置的最小值。
现在问题来了，我们这种情况是总高度是小于第一列高度的最大值和第二列高度的最大值之和的，这样就是先用 总高度 300px - 第一列最小高度 100px - 第二列最小高度 50px = 150px。第一列高度：第一列最小高度 100px + 150px/2 = 175px;第二列高度：第一列最小高度 50px + 150px/2 = 125px;
效果如下：

![](https://api2.mubu.com/v3/document_image/1c60234c-7538-4429-a348-ddb5ea9a722b-3807603.jpg)

### 重复行或者列
repeat() 属性可以创建重复的网格轨道。这个适用于创建相等尺寸的网格项目和多个网格项目。
repeat() 也接受两个参数：第一个参数定义网格轨道应该重复的次数，第二个参数定义每个轨道的尺寸。
```css
.grid-container{
    padding: 20px;
    display: grid;
    grid-template-columns: repeat(2,100px);
    grid-template-rows: repeat(3,100px);
    background: pink;
}
```
效果如下：

![](https://api2.mubu.com/v3/document_image/33b42917-e3a1-40f2-8216-a3b717437cbb-3807603.jpg)

### 间距
grid-column-gap：创建列与列之间的距离。
grid-row-gap：行与行之间的距离。
```css
.grid-container{
    padding: 20px;
    display: grid;
    grid-template-columns: repeat(2,100px);
    grid-template-rows: repeat(3,100px);
    grid-column-gap: 50px;
    grid-row-gap: 15px;
    background: pink;
}
```

![](https://api2.mubu.com/v3/document_image/e69ae1b5-fa2f-4bf4-a3b0-b88dcbc89c4d-3807603.jpg)

或者使用 grid-gap 是 grid-row-gap 和 grid-column-gap两个属性的缩写。

### 通过网格线定位 grid item
我们可以通过表格线行或者列来定位 grid item。比如：
```html
<div class="grid-container">
    <div class="item item1">1</div>
    <div class="item item2">2</div>
    <div class="item item3">3</div>
    <div class="item item4">4</div>
    <div class="item item5">5</div>
    <div class="item item6">6</div>
</div>
```
```css
.grid-container{
    padding: 20px;
    display: grid;
    grid-template-columns: repeat(2,100px);
    grid-template-rows: repeat(3,100px);
    grid-column-gap: 50px;
    grid-row-gap: 15px;
    background: pink;
}
.item{
    border: 2px solid palegoldenrod;
    color: #fff;
    text-align: center;
    font-size: 20px;
}
.item1{
    grid-row-start: 2;
    grid-row-end: 3;
    grid-column-start: 2;
    grid-column-end: 3;
    background: #fffa90;
    color: #000;
}
```
效果：

![](https://api2.mubu.com/v3/document_image/29121b2b-4eb2-4643-b4b0-fbdddf4dc445-3807603.jpg)

grid-row 是 grid-row-start 和 grid-row-end 的简写。grid-column 是 grid-column-start 和 grid-column-end 的简写。
如果只提供一个值，指定了 grid-row-start 和 grid-column-start 的值。
如果提供两个值，第一个值是 grid-row-start 或者 grid-column-start 的值，第二个值是 grid-row-end 或者 grid-column-end 的值，两者之间必须要用/隔开。
```css
.item1{
    grid-row: 2; 
    grid-column: 3 / 4;
}
```
这四个值可以用 grid-area 缩写，分别对应 grid-row-start、grid-column-start、grid-row-end、grid-column-end：
```css
.item1{
    grid-area: 2 / 2 / 3 / 3;
}
```

### 合并单元行与合并单元列
这个就和 excel 中的合并单元行/列是相同的（这个需要设置在 grid item 中）













![]()

```css

```
