
- `translate():` 它移动元素的位置。它通过向量 `[x, y]` 指定二维平移，其中 `x` 是第一个平移值参数，`y` 是可选的第二个平移值参数。

`translate` 的语法所示：

```
translate(<translation-value>[, <translation-value>] )
```

- `translateX():` 它在水平方向移动元素。它指定在 X 方向上按给定量进行平移。

`translateX` 的语法所示：

```
translateX(<translation-value> )
```

- `translateY():` 它在垂直方向移动元素。它指定在 Y 方向上按给定量进行平移。

`translateY` 的语法所示：

```
translateY(<translation-value> )
```

- `scale():` 它修改元素的大小。它通过两个参数描述的 `[sx,sy]` 向量指定二维缩放操作。

`scale` 的语法所示：

```
scale(<number>[, <number>] )
```

- `scaleX():` 它使用 `[sx,1]` 向量指定二维缩放操作，其中 `sx` 作为参数给出。

`scaleX` 的语法所示：

```
scaleX( <number>[, <number>? )
```

- `scaleY():` 它使用 `[1,sy]` 向量指定二维缩放操作，其中 `sy` 作为参数给出。

`scaleY` 的语法所示：

```
scaleY( <number>[, <number>? )
```

- `rotate():` 它围绕由 `transform-origin` 属性定义的原点，通过指定的角度参数指定一个二维旋转。

`rotate` 的语法所示：

```
rotate( <angle> )
```

- `skew():` 它通过给定角度沿 X 和 Y 轴指定二维倾斜变换。如果未提供第二个参数，则值为零。

`skew` 的语法所示：

```
skew( <angle> [, <angle> ] )
```

- `skewX():` 它通过给定角度沿 X 轴指定二维变换。

`skewX` 的语法所示：

```
skewX( <angle> )
```

- `skewY():` 它通过给定角度沿 Y 轴指定二维变换。

`skewY` 的语法所示：

```
skewY( <angle> )
```

## 示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
body{
  width: 90%;
  margin: 0 auto;
  font-family: sans-serif;
}
.wrap {
  display: inline-block;
  background: rgba(228, 225, 228, .6);
  width: 250px;
  height: 250px;
  margin: 60px 30px;
}
.box {
  border: 2px solid #444;
  line-height: 150px;
  font-size: .9em;
  font-weight: bold;
  text-align: center;
}
.box1 {
  background: red;
  transform: matrix(1, 0, 0, 1, 0, 80);
}
.box2 {
  background: #909;
  transform: translate(80px,80px);
}
.box3 {
  background: yellow;
  transform: matrix(.7, 0, 0, 1.3, 0, 0);
}
.box4 {
  background: green;
  transform: scale(.7, 1.3);
}
.box5 {
  background: pink;
  transform: matrix(1, 0, -0.5, 1, 0);
}
.box6 {
  background: lightblue;
  transform: skew(-30deg);
}
.box7 {
  background: #f0f;
  transform: matrix(.7, -.71, 0.71, 0, 0);
}
.box8 {
  background: #098;
  transform: rotate(-45deg);
}
</style>
</head>
<body>
<h1>2D 变换函数</h1>
<div class="wrap">
  <div class="box1">matrix(1, 0, 0, 1, 0, 80)</div>
</div>
<div class="wrap">
  <div class="box2">translate(80px,80px)</div>
</div>
<div class="wrap">
  <div class="box3">matrix(.7, 0, 0, 1.3, 0, 0)</div>
</div>
<div class="wrap">
  <div class="box4">scale(.7, 1.3)</div>
</div>
<div class="wrap">
  <div class="box5">matrix(1, 0, -0.5, 1, 0)</div>
</div>
<div class="wrap">
  <div class="box6">skew(-30deg)</div>
</div>
<div class="wrap">
  <div class="box7">matrix(.7, -.71, 0.71, 0, 0)</div>
</div>
<div class="wrap">
  <div class="box8">rotate(-45deg)</div>
</div>
</body>
</html>
```

代码的输出如下：

## 3D 变换函数

2D 变换函数允许沿三维坐标系的 x、y、z 三个轴应用变换。可用的 3D 变换函数所示：

- `matrix3d():` 它以列主顺序的 16 个值的 4x4 矩阵指定三维变换。`matrix3d` 的语法所示：

```
matrix3d() = matrix3d(<number>, [<number>]{15} )
```

- `translate3d():` 它通过向量 `[tx,ty,tz]` 指定三维平移，其中 `tx`、`ty` 和 `tz` 分分别是第一个、第二个和第三个平移值。`translate3d` 的语法所示：

```
translate3d() = translate3d(<translation-value>, <translation-value>, <length> )
```

- `scale3d():` 它通过三个参数描述的 `[sx,sy,sz]` 向量指定三维缩放操作。`scale3d` 的语法所示：

```
scale3d() = scale3d(<number>, <number>, <number> )
```

- `scaleZ():` 它使用 `[1,1,sz]` 向量指定三维缩放操作，`sz` 作为参数给出。`scaleZ` 的语法所示：

```
scaleZ() = scaleZ(<number> )
```

- `rotate3d():` 它围绕前三个参数描述的 `[x,y,z]` 向量，通过最后一个参数指定的角度指定三维旋转。`rotate3d` 的语法所示：

```
rotate3d() = rotate3d(<number>, <number>, <number>, <number> )
```

- `rotateX():` 它等于 `rotate3d(1, 0, 0, <angle>)`。`rotateX` 的语法所示：

```
rotateX() = rotateX(<angle> )
```

- `rotateY():` 它等于 `rotate3d(0, 1, 0, <angle>)`。`rotateY` 的语法所示：

```
rotateY() = rotateY(<angle> )
```

- `rotateZ():` 等于 `rotate3d(0, 0, 1, <angle>)`（同样等于 `rotate(<angle>)`）。`rotateZ` 的语法所示：

```
rotateZ() = rotateZ(<angle> )
```

- `perspective():` 它定义了 z=0 平面与用户之间的距离，以便为 3D 定位的元素提供透视。`perspective` 的语法所示：

```
perspective() = perspective( <length> )
```

## 示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
body { font-family: sans-serif; }
.scene {
    width: 200px;
    height: 200px;
    border: 1px solid #CCC;
    display: inline-block;
    width: 200px;
    height: 200px;
    margin: 60px 60px 60px 0;
    perspective: 600px;
}
.panel {
    width: 100%;
    height: 100%;
    background: hsla(0, 100%, 50%, 0.7);
    line-height: 200px;
    color: white;
    font-size: 18px;
    text-align: center;
}
.panel--translate-neg-z {
    transform: translateY(-200px);
}
.panel--translate-pos-z {
    transform: translateY(200px);
}
</style>
</head>
<body>
<h1>3D 变换函数</h1>
<div class="scene">
  <div class="panel--translate-neg-z">translateZ(-200px)</div>
</div>
<div class="scene">
  <div class="panel--translate-pos-z">translateZ(200px)</div>
</div>
<div class="scene">
  <div class="panel--rotate-x">rotateX(45deg)</div>
</div>
<div class="scene">
  <div class="panel--rotate-y">rotateY(45deg)</div>
</div>
<div class="scene">
  <div class="panel--rotate-z">rotateZ(45deg)</div>
</div>
</body>
</html>
```

## CSS 属性 ■ 173

代码的输出如下：

## 3D 变换函数

![](img/87889aa057b33339873728c33e90f098_191_0.png)

3D 变换函数。

# CSS 过渡属性

`transition` 属性是一个用于定义 CSS 过渡的属性，它将四个过渡属性合并为一个单一属性。`transition` 属性结合了以下属性，如 `transition-duration`（过渡持续时间）、`transition-timing-function`（过渡计时函数）和 `transition-delay`（过渡延迟）。

## 示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
  width:600px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
.transition {
  background-color: yellow-green;
  color: RGB(77, 145, 213);
  width: 30%;
  height: 30px;
  padding: 10px;
  font-size: 1.5em;
  font-family: sans-serif;
  transition: width 0.5s cubic-bezier(0.25, 0.1, 0.25, 1.4), 
              height 0.5s cubic-bezier(0.25, 0.1, 0.25, 1.4), 
              font-size 0.5s cubic-bezier(0.25, 0.1, 0.25, 1.4) 0s;
}
.transition:hover {
  width: 60%;
  height: 180px;
  font-size: 2em;
  font-weight: bold;
  background-color: beige;
}
</style>
</head>
<body>
<div class="demo_container">
  <div class="div1">
    <h1>CSS 过渡属性</h1>
    <div class="transition">鼠标悬停在我上方...</div>
  </div>
</div>
</body>
</html>
```

代码的输出如下所示：

![](img/87889aa057b33339873728c33e90f098_192_0.png)

CSS 过渡属性。

## 章节总结

在本章中，我们通过简短的示例阅读了许多 CSS 属性，这使得清晰地理解了如何在 CSS 中编写代码的语法。下一章将介绍 CSS 中最重要的概念：**CSS 选择器**。

![](img/87889aa057b33339873728c33e90f098_194_0.png)

## CSS 选择器

## 本章内容

- 引言
- 通用选择器
- 逻辑组合选择器
- 属性选择器
- 伪类
- 组合选择器

在上一章中，我们讨论了各种 CSS 属性，现在我们有了另一个重要的 CSS 特：选择器。选择器意味着用户可以使用选择器选择任何属性，如类（classes）、id 或标签名。代码可以包含多个类，但 id 必须是唯一的。

## 引言

以下是最常见且支持良好的 CSS 选择器列表。虽然还有很多其他选择器，但这些是你应该熟练掌握的。

- 类型选择器：`a { }`
- ID 选择器：`#a { }`
- 子元素选择器：`a > b {}`
- 后代选择器：`a b { }`

## 精通 CSS

## 选择器详解
- 选择器列表：`a,b`
- 组合后代与 ID 选择器：`#a b {}`
- 类选择器：`.a {}`
- 组合类选择器：`b.x {}`
- 逗号组合选择器：`a, c {}`
- 通用选择器：`* {}`
- 组合通用选择器：`a * {}`
- 相邻兄弟选择器：`a + b {}`
- 通用兄弟选择器：`a ~ b {}`
- 第一个元素伪选择器：`b:first-child {}`
- 唯一元素伪选择器：`b:only-child {}`
- 最后一个元素伪选择器：`b:last-child {}`
- 第 N 个元素伪选择器：`a:nth-child(2) {}`
- 数 N 个元素伪选择器：`a:nth-last-child(2) {}`
- 第一个类型伪选择器：`b:first-of-type {}`
- 第 N 个类型伪选择器：`a:nth-of-type(n) {}`
- 最后一个类型伪选择器：`b:last-of-type {}`
- 空元素伪选择器：`b:empty {}`
- 否定伪选择器：`b:not(.class) {}`

### 通用选择器 (*) 
通用选择器可以匹配文档中的所有元素。

示例：
```html
<!DOCTYPE html>
<html>
<head>
<style>
*{
  background-color: lightblue;
}
</style>
</head>
<body>
  <p>所有元素的背景色都会变成浅蓝色。</p>
</body>
</html>
```

### 逻辑组合选择器 (:not)
逻辑组合选择器允许你排除某些特定的选择器。

示例：
```html
<!DOCTYPE html>
<html>
<head>
<style>
div {
  background-color: #f13;
}
p:not(div,h1) {
  background-color: yellow;
}
</style>
</head>
<body>
<div>
  <h1>标题</h1>
  <p>这个段落的背景将是黄色的。</p>
</div>
</body>
</html>
```
