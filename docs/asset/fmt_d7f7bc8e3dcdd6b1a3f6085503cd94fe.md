
```css
.box-3{
  transform-origin: 0 0;
  padding: 20px;
  width: 300px;
  height:300px;
  background-color: green;
  filter: opacity(70%);
  color: white;
  font-family: sans-serif;
}
.box-4{
  transform-origin: 0 0;
  padding: 20px;
  width: 300px;
height:300px;
background-color: green;
  filter: opacity(90%);
  color: white;
  font-family: sans-serif;
}
```
</style>
</head>
<body>
<div class="demo_container">
<h1>matrix3d() 函数可以结合 CSS 变换用于在三维空间内为元素设置样式。</h1>
<div class="row">
<div class="box-1">opacity(10%)</div>
<div class="box-2">opacity(40%)</div>
<div class="box-3">opacity(70%)</div>
<div class="box-4">opacity(90%)</div>
</div>
</div>
</body>
</html>
```

代码的输出下文：

![](img/87889aa057b33339873728c33e90f098_338_0.png)

CSS 函数-`opacity()`。

## `perspective()`

`perspective()` 函数定义了 z=0 平面与用户之间的距离，以赋予元素透视效果。`perspective()` 函数的工作原理是指定 z=0 平面的距离。参数也指定为长度值（例如 `1px`、`vw` 等）。长度越大，“3D效果”越不明显。

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style> {
  padding:0;
  margin:0;
  box-sizing: border-box;
}
.demo_container{
  padding:20px;
  width:900px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
img{
  width:100%;
  height:250px;
}
.row{
  display: flex;
}
.col{
  width:80%
}
.image-1 {
  transform: perspective(400px) rotateY(70deg);
  width:100px;
  height:100px
}
.image-2 {
  transform: perspective(200px) rotateY(60deg);
  width:100px;
  height:100px
}
.image-3 {
  transform: perspective(130px) rotateY(-60deg);
  width:100px;
  height:100px
}
p {
  line-height: 2;
  font-size:20px;
}
</style>
</head>
<body>
<div class="demo_container">
<h2>它定义了 z=0 平面与用户之间的距离，以赋予 3D 元素透视效果</h2>
<div class="row">
<div class="col">
<p>普通图像</p>
<img src="images/1.jpg" alt="image">
<p>perspective(400px) rotateY(70deg) 图像</p>
<img class="image-1" src="images/1.jpg" alt="image">
</div>
<div class="col">
<p>perspective(200px) rotateY(60deg) 图像</p>
<img class="image-2" src="images/1.jpg" alt="image">
<p>perspective(130px) rotateY(-60deg) 图像</p>
<img class="image-3" src="images/1.jpg" alt="image">
</div>
</div>
</div>
</body>
</html>
```

代码的输出下文所示：

它定义了 z=0 平面与用户之间的距离，以赋予 3D 元素透视效果

普通图像 `perspective(200px) rotateY(60deg)` 图像

![](img/87889aa057b33339873728c33e90f098_341_0.png)

`perspective(130px) rotateY(-60deg)` 图像

`perspective(400px) rotateY(70deg)` 图像

CSS 函数 (`perspective()`).

## `radial-gradient()`

`radial-gradient()` 函数允许使用 CSS 创建径向渐变。

CSS 渐变允许对元素应用多种背景颜色，从一种颜色混合到下一种颜色。

```html
<!DOCTYPE html>
<html>
<head>
<style>
* {
  padding:0;
  margin:0;
  box-sizing: border-box;
}
.demo_container{
  padding:20px;
  width:900px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
.row{
  display: flex;
}
.col{
  width:100%
}
.image-1{
  background: radial-gradient(to bottom right, red, yellow);
}
.image-2{
  background: radial-gradient(to bottom right, blue, cyan);
}
.image-3{
  background: radial-gradient(to bottom right, green, lime);
}
.image-4{
  background: radial-gradient(to bottom right, orange, pink);
}
p{
  line-height: 2;
  font-size:20px;
}
</style>
</head>
<body>
<div class="demo_container">
<h2>radial-gradient() 函数允许使用 CSS 创建径向渐变。</h2>
<div class="row">
<div class="col">
<div class="image-1"></div>
<div class="image-2"></div>
</div>
<div class="col">
<div class="image-3"></div>
<div class="image-4"></div>
</div>
</div>
</div>
</div>
</body>
</html>
```

代码的输出下文所示：

`radial-gradient()` 函数允许使用 CSS 创建径向渐变。

从一种颜色过渡到下一种颜色。这些这些渐变是线性渐变，其中颜色停止点在两个方向上无限重复。重复线性渐变的工作原理与（非重复）线性渐变的工作相同。语法：`repeating-linear-gradient()` 函数接受以下值：

- `angle`：它指定渐变方向的角度。例如，`45deg`。

以下关键字指定下方渐变线的指向：

- `to top`（向顶部）
- `to right`（向右）
- `to bottom`（向底部）
- `to left`（向左侧）

以下关键字指定下方渐变线的指向：

- `to top left`（向左上）
- `to top right`（向右上）
- `to bottom`（向底部）
- `to bottom left`（向左下）
- `color-stop`（颜色停止点）

## 示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
{
  padding:0;
  margin:0;
  box-sizing: border-box;
}
```
```css
.demo_container{
  padding:20px;
  width:900px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
.row{
  display: flex;
  flex-direction:row;
}
.col{
  height:100px;
  width:100%;
}
```

![](img/87889aa057b33339873728c33e90f098_346_0.png)
```css
.image-1 {
  background: repeating-linear-gradient(gold 15%, orange 30%);
  color: white;
  padding: 30px;
  height: 300px;
}
.image-2 {
  background: repeating-linear-gradient(to right, gold 16%, orange 30%);
  color: white;
  padding: 30px;
  height: 300px;
}
.image-3 {
  background: repeating-linear-gradient(to right, orange, gold 16%, orange 30%);
  color: white;
  padding: 30px;
  height: 300px;
}
.image-4 {
  background: repeating-linear-gradient(155deg, gold, gold 50px, orange 60px, orange 120px);
  color: white;
}
```
```css
padding: 30px;
height: 300px;
p{
  line-height: 2;
  font-size: 20px;
  margin-bottom:30px;
}
```
```html
</style></head>
<body>
<div class="demo_container">
  <h2>repeating-linear-gradient() 函数允许你创建一个在两个方向上无限循环、反复重复的线性渐变</h2>
  <div class="row">
    <div class="col">
      <p>默认角度，radial-gradient(yellow, red)</p>
      <div class="image-1"></div>
      <p>重复渐变角度，repe-linear-gradient (top right, orange, gold 15%, orange 30%)</p>
    </div>
    <div class="col">
      <div class="image-2"></div>
      <p>平滑过渡，repeating-linear-gradient (top right, orange, gold 15%, orange 30%)</p>
      <div class="image-3"></div>
      <p>创建条纹，repeating-linear-gradient (165deg, gold, gold 60px, orange 60px, orange 120px)</p>
      <div class="image-4"></div>
    </div>
  </div>
</div>
</body>
</html>
```

# 330 ■ 精通 CSS

代码的输出如下：

`repeating-linear-gradient()` 函数允许你创建一个在两个方向上无限循环、反复重复的线性渐变。

默认角度，`radial-gradient(yellow; red)`
平滑过渡，`repeating-linear-gradient(top right, orange, gold 15%, orange 30%)`

![](img/87889aa057b33339873728c33e90f098_348_0.png)

重复渐变角度，`repeating-linear-gradient(top right, orange, gold 15%, orange 30%)`
创建条纹，`repeating-linear-gradient(165deg, gold, gold 60px, orange 60px, orange 120px)`

![](img/87889aa057b33339873728c33e90f098_348_1.png)

CSS 函数 (`repeating-linear-gradient()`).

## `repeating-radial-gradient()`

CSS `repeating-radial-gradient()` 允许创建一个反复重复的径向渐变。CSS 渐变允许为元素应用多个背景颜色，这些颜色从单色过渡到下一种。重复径向渐变是颜色停止点无限重复的渐变。径向渐变具有圆形或椭圆形。在创建径向渐变时，指定渐变的中心以及大小和形状。

## CSS 函数 331

语法：此函数使用与 `radial-gradient()` 相同的语法，如下：

```css
radial-gradient(shape size position color-stop, color-stop)
```

`repeating-radial-gradient()` 函数接受以下值：

- `shape`：指定渐变的形状。可以是 `circle`（圆形）或 `ellipse`（椭圆形）。
- `size`：指定结束形状的大小。值为：
  - `closest side`（最近侧）
  - `farthest side`（最远侧）
  - `closest corner`（最近圆角）
  - `length`（长度）
- `position`：指定渐变的位置。值为：
  - `top`（顶部）
  - `right`（右侧）
  - `bottom`（底部）
  - `left`（左侧）
  - `center`（中心）

## 示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
*{
  padding:0;
  margin:0;
  box-sizing: border-box;
}
.demo_container{
  padding:20px;
  width:900px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
.row{
  display: flex;
  flex-wrap: wrap;
  flex-direction: row;
}
.col{
  width:50%;
}
p{
  height:50px;
}
.image-1 {
  background: repeating-radial-gradient(ellipse, green 20%, lime 40%);
  color: white;
  padding:30px;
  height:300px;
}
.image-2 {
  background: repeating-radial-gradient(circle, green 20%, lime 40%);
  color: white;
  padding:30px;
  height:300px;
}
.image-3 {
  background: repeating-radial-gradient(circle at top left, green 30%, lime 40%);
  color: white;
  padding:30px;
  height:300px;
}
.image-4 {
  background: repeating-radial-gradient(circle at top left, lightgreen 10%, green 45%, lime 60%);
  color: white;
  padding:30px;
  height:300px;
}
.image-5 {
  background: repeating-radial-gradient(circle at top left, lime, green 30%, lime 40%);
  color: white;
  padding:30px;
  height:300px;
}
.image-6 {
  background: repeating-radial-gradient(closest-side at 25px 35px, orange 25%, gold 40%);
  background-size:50px 50px;
  color: white;
```
