# Css网格布局
网格布局是强大的`css`布局方案。它将容器划分成**“列”和“行”**，产生单元格，可以看作是**二维布局**。

## 一、基本概念

### 1.1 容器和项目

```html
<div class="grid">
  <div class="grid-item"><p>1</p></div>
  <div class="grid-item"><p>2</p></div>
  <div class="grid-item"><p>3</p></div>
</div>
```
网格布局只对容器的子元素起作用


### 1.2 行和列

### 1.3 单元格  行列交叉形成

### 1.4 网格线
n行有n+1条水平网格线，m列有n+1条垂直网格线。


## 二、容器属性

### 2.1 display
```css
div {
    display:grid;/*也可以设置为行内网格  inline-grid*/
}
```
注意：设置网格布局以后，容器子元素的`float`、`display：inline-block`、`display：table-cell`、`vertical-align`和 `column-*`等设置均失效。

### 2.2 grid-template-columns、  grid-template-rows
```css
.container{
    display:grid;
    grid-template-columns:100px 100px 100px;
    grid-template-rows:100px 100px 100px;
}
```
指定了一个列宽和行高都是100px，三行三列的网格。这里的绝对单位可以替换成百分比33.3%。

**（1）repeat()**
接受两个参数，第一个表示重复次数，第二个表示重复的值。
```css
.container {
  display: grid;
  grid-template-columns: repeat(3, 33.33%);
  grid-template-rows: repeat(3, 33.33%);
}
```
repeat()还可以这样写
```css
/*定义了9列*/
grid-template-columns: repeat(3, 100px 30px 60px);
```
**（2）auto-fill关键字**
有时单元格大小是固定的,但是容器大小不固定，auto-fill表示自动填充，尽可能填满
**（3）fr关键字**
为了方便表示比例关系，fr（fraction缩写，“片段”）。
```css
.container{
    display:grid;
    /* 表示后一列是前一列的两倍 */
    grid-template-columns:1fr 2fr;
}
```
**（4）minmax（）**
该函数产生一个长度范围，表示长度就在这个范围中
```css
grid-template-columns: 1fr 1fr minmax(100px, 1fr);
```
**（5）auto关键字**
auto表示自适应宽度，但是minwidth的权值更高
**（6）网格线的名称**
同一条网格线允许别名
```css
.container {
  display: grid;
  grid-template-columns: [c1] 100px [c2] 100px [c3 c-three] auto [c4];
  grid-template-rows: [r1] 100px [r2] 100px [r3] auto [r4];
}
```
**（7）布局实例**
设置左右两栏，宽度比（70%，30%）
```css
.wraper{
    display:grid;
    grid-template-columns:70% 30%;
}
```
传统12网格布局
```css
.wraper{
    display:grid;
    grid-template-columns:repeat(12,1fr);
}
```

### 2.3 grid-row-gap、  grid-column-gap、   grid-gap
`grid-row-gap`、`grid-column-gap`分别设置行与行，列与列之间的间距,
`grid-gap`是以上两个合并的简写模式,如果grid-gap省略了第二个值，浏览器认为第二个值等于第一个值。`grid-`在这三个属性中可省略。
```css
.container{
    grid-row-gap:30px;
    grid-column-gap:20px;
    /* 下面的表达与以上效果类似 */
    grid-gap:30px 20px;
}
```

### 2.4 grid-template-areas
网格布局允许指定“区域”（area）
```css
.container {
    display: grid;
    grid-template-columns: 100px 100px 100px;
    grid-template-rows: 100px 100px 100px;
    grid-template-areas:'a . c'
                        'd . f'
                        'g . i';
}
```
每个区域的起始网格线，会自动命名为区域名-start，终止网格线自动命名为区域名-end。
区域命名会影响到网格线，每个区域的起始网格线，会自动命名为区域名-start，终止网格线自动命名为区域名-end。

### 2.5 grid-auto-flow
默认按照子元素顺序，先行后列的放置子元素。
`grid-auto-flow:column`可改为先列后行。
该属性可设置为：`row`、`column`、`row dense`及`column dense`。
`row dense`及`column dense`两个值用于某些项目指定位置后，剩下项目如何放置，表示尽可能填满空格。

### 2.6 justify-items、 align-items、   place-items
`justify-items`属性设置单元格内容的水平位置（左中右），`align-items`属性设置单元格内容的垂直位置（上中下）。
```css
.container{
    justify-items:  start |  end  |  center  |  stretch;
    align-items:  start |  end  |  center  |  stretch;
}
```
这两个属性写法完全一致，可取下面的值：
+ start：对齐单元格的起始边缘。
+ end：对齐单元格的结束边缘。
+ center：单元格内部居中。
+ stretch：拉伸，占满单元格的整个宽度（默认值）。

`place-items`是合写形式。
`place-items: <align-items> <justify-items>;`
如果省略第二个值，则浏览器认为与第一个值相等。

### 2.7 justify-content 属性，align-content 属性，place-content 属性
`justify-content`属性是整个内容区域在容器里面的水平位置（左中右）
`align-content`属性是整个内容区域的垂直位置（上中下）。
```css
.container {
  justify-content: start | end | center | stretch | space-around | space-between | space-evenly;
  align-content: start | end | center | stretch | space-around | space-between | space-evenly;  
}
```
+ start - 对齐容器的起始边框。
+ end - 对齐容器的结束边框。
+ center - 容器内部居中。
+ stretch - 项目大小没有指定时，拉伸占据整个网格容器。
+ space-around - 每个项目两侧的间隔相等。所以，项目之间的间隔比项目与容器边框的间隔大一倍。
+ space-between - 项目与项目的间隔相等，项目与容器边框之间没有间隔。
+ space-evenly - 项目与项目的间隔相等，项目与容器边框之间也是同样长度的间隔。

`place-content`是合写形式。
`place-content: <align-content> <justify-content>;`
如果省略第二个值，则浏览器认为与第一个值相等。

### 2.8 grid-auto-columns 属性，grid-auto-rows 属性

```css
.container {
  display: grid;
  grid-template-columns: 100px 100px 100px;
  grid-template-rows: 100px 100px 100px;
  grid-auto-rows: 50px; 
}
```
上面代码指定新增的行高统一为50px（原始的行高为100px）。

### 2.9 grid-template 属性，grid 属性
grid-template属性是grid-template-columns、grid-template-rows和grid-template-areas这三个属性的合并简写形式。

grid属性是grid-template-rows、grid-template-columns、grid-template-areas、 grid-auto-rows、grid-auto-columns、grid-auto-flow这六个属性的合并简写形式。

还是别合写了。。。

## 三、子项属性
### 3.1 grid-column-start 属性，grid-column-end 属性，grid-row-start 属性，grid-row-end 属性

+ grid-column-start属性：左边框所在的垂直网格线
+ grid-column-end属性：右边框所在的垂直网格线
+ grid-row-start属性：上边框所在的水平网格线
+ grid-row-end属性：下边框所在的水平网格线

```css
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 2;
  grid-row-end: 4;
}
.item-1 {
  grid-column-start: header-start;
  grid-column-end: header-end;
}
```
一者是根据网格线，另一个是根据网格线名字。
这四个属性的值还可以使用span关键字，表示"跨越"，即左右边框（上下边框）之间跨越多少个网格。
使用这四个属性，如果产生了项目的重叠，则使用z-index属性指定项目的重叠顺序。


### 3.2 grid-column、   grid-row

```css
.item-1 {
  grid-column: 1 / 3;
  grid-row: 1 / 2;
}
/* 等同于 */
.item-1 {
  grid-column-start: 1;
  grid-column-end: 3;
  grid-row-start: 1;
  grid-row-end: 2;
}
/* 也可以使用span关键字 */
.item-1 {
  background: #b03532;
  grid-column: 1 / 3;
  grid-row: 1 / 3;
}
/* 等同于 */
.item-1 {
  background: #b03532;
  grid-column: 1 / span 2;
  grid-row: 1 / span 2;
}
/* 斜杠以及后面的部分可以省略，默认跨越一个网格。 */
.item-1 {
  grid-column: 1;
  grid-row: 1;
}
```
### 3.3 grid-area 属性
把指定子项放在哪一个区域
```css
.item-1 {
  grid-area: e;
}
```
`grid-area`属性还可用作`grid-row-start`、`grid-column-start`、`grid-row-end`、`grid-column-end`的合并简写形式，直接指定项目的位置。

```css
.item {
  grid-area: <row-start> / <column-start> / <row-end> / <column-end>;
}
```

### 3.4 justify-self 属性，align-self 属性，place-self 属性
`justify-self`属性设置单元格内容的水平位置（左中右），跟`justify-items`属性的用法完全一致，但只作用于单个项目。

`align-self`属性设置单元格内容的垂直位置（上中下），跟`align-items`属性的用法完全一致，也是只作用于单个项目。
+ start：对齐单元格的起始边缘。
+ end：对齐单元格的结束边缘。
+ center：单元格内部居中。
+ stretch：拉伸，占满单元格的整个宽度（默认值）。

`place-self`属性是`align-self`属性和`justify-self`属性的合并简写形式。
`place-self: <align-self> <justify-self>;`