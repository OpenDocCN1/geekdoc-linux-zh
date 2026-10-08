
代码的输出如下：

## CSS 颜色属性 (RGB)

这里我们使用 RGB 颜色代码（`rgb(205, 92, 92)`）.

这里我们使用 RGB 颜色代码（`rgb(100, 149, 237)`）.

CSS 颜色属性 (RGB)。

## RGBA 颜色

在 CSS 中，RGBA 也是一种带有 Alpha 通道扩展的颜色显示格式。该颜色的结构如下所示：

`rgba` (红, 绿, 蓝, Alpha)

在此工作中，Alpha 用于表示颜色的透明度。在 CSS 透明度中，该区域用于设置颜色的亮度，其范围在 0.0 到 1.0 之间，其中0.0 代表完全透明，1.0 代表完全不透明。你将在提供的示例中获得更好的理解。

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
width:400px;
margin:0 auto;
text-align: center;
justify-content: center;
align-items: center;
}
.c1{
background-color: rgba(11, 156, 49, 0.2);
}
.c2 {
background-color: RGBA(11, 156, 49, 0.4);
}
.c3{
background-color: rgba(11, 156, 49, 0.6);
}
.c4 {
background-color: RGBA(11, 156, 49, 0.8);
}
.c5{
background-color: rgba(11, 156, 49, 1);
}
</style>
</head>
<body>
<div class="demo_container">
<h1> CSS 颜色属性 (RGBA)</h1>
<p class="c1">这里我们使用 RGBA 代码（rgba(11, 156, 49, 0.2)).</p><br>
<p class="c2">这里我们使用 RGBA 颜色代码（RGBA(11, 156, 49, 0.4)).</p><br>
<p class="c3">这里我们使用 RGBA 颜色代码（rgba(11, 156, 49, 0.6)).</p><br>
<p class="c4">这里我们使用 RGBA 颜色代码（RGBA(11, 156, 49, 0.8)).</p><br>
<p class="c5">这里我们使用 RGBA 颜色代码（rgba(11, 156, 49, 1)).</p><br>
</body>
</html>
```

代码的输出如下：

| CSS 颜色属性 (RGBA) |
| :--- |
| 这里我们使用 RGBA 代码（rgba(11, 156, 49, 0.2)). |
| 这里我们使用 RGBA 颜色代码（RGBA(11, 156, 49, 0.4)). |
| 这里我们使用 RGBA 颜色代码（rgba(11, 156, 49, 0.6)). |
| 这里我们使用 RGBA 颜色代码（RGBA(11, 156, 49, 0.8)). |
| 这里我们使用 RGBA 颜色代码（rgba(11, 156, 49, 1)). |

CSS 颜色属性 (RGBA)。

## HEX 颜色

CSS 颜色也可以通过十六进制值定义，这是表示颜色的方法。在 CSS 中，最常用的定义颜色方法是使用 "#"符号，如 #RGB。组合 0-9 和 A-F 的十六进制数字用于在 CSS 中表示颜色。以下是 HEX 颜色示例。

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
  width:400px;
margin:0 auto;
text-align: center;
justify-content: center;
align-items: center;
color:red
}
.c1{
color: #6495ed;
}
.c2 {
color:#b22222
}
</style>
</head>
<body>
<div class="demo_container">
<h1> CSS 颜色属性 (HEX)</h1>
<p class="c1">这里我们使用 HEX 代码（#6495ed）。</p><br>
<p class="c2"> 这里我们使用 HEX 代码（#b22222）。</p><br>
</body>
</html>
```

下方代码的输出：

## CSS 颜色属性 (HEX)

这里我们使用 HEX 代码（`#6495ed`）。

这里我们使用 HEX 代码（`#b22222`）。

CSS 颜色属性 (HEX)。

## 1. opacity 属性：`opacity` 属性指定元素的透明度。该属性的语法如下：

```
opacity: value | initial | inherit
```

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
  width: 400px;
  margin: 0 auto;
text-align: center;
  justify-content: center;
align-items: center;
}
.c1{
  opacity: 0.4;
}
img{
  background-image: url('/images-1.jpg');
  width: "300px"
  height: "300px"
  opacity: 0.5;
}
</style>
</head>
<body>
  <div class="demo_container">
    <h1> CSS 颜色透明度属性</h1>
    <h2 class="c1">这里我们使用透明度代码颜色。</h2><br>
    <img src="images-1.jpg" alt="image" width="200px" height="200px">
  </div>
</body>
</html>
```

2. 代码的输出如下：

## CSS 颜色透明度属性

这里我们使用透明度代码颜色。

![](img/87889aa057b33339873728c33e90f098_112_0.png)

CSS 颜色透明度属性。

## CSS 尺寸属性

### 1. height 属性：`height` CSS 属性指定元素内容区域的高度。内容区域不包括内边距、边框或外边距。
该属性的语法如下：

```
height: length | percentage | auto | initial | inherit
```

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
width:300px;
margin:0 auto;
text-align: center;
justify-content: center;
align-items: center;
}
.cl{
background-color: palevioletred;
height: 200px;
width:300px;
}
img{
background-image: url('/images-1.jpg');
width: 300px;
height: 300px;
}
</style>
</head>
<body>
<div class="demo_container">
<h1> CSS 尺寸属性 - 高度，宽度</h1>
<h2 class="cl">高度为 "200"，宽度为 "300"</h2><br>
<img src="images-1.jpg" alt="image" width="200px" height="200px">
</body>
</html>
```

代码的输出如下：

## CSS 尺寸
属性 - 高度，宽度

![](img/87889aa057b33339873728c33e90f098_114_0.png)

![](img/87889aa057b33339873728c33e90f098_114_1.png)

CSS 尺寸属性 –高度，宽度。

### 2. max-height 和 max-width 属性：`max-height` 属性指定元素内容区域的最大高度。此最大高度不包括内边距、边框或外边距。
`max-width` 属性定义元素内容区域的最大宽度。此最大宽度不包括内边距、边框或外边距
该属性的语法如下：

```
max-height: length | percentage | none | initial | inherit
```

该属性的语法如下：

```
max-width: length | percentage | none | initial | inherit
```

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
  width:500px;
  height:500px;
  margin:0 auto;
  text-align: center;
  justify-content: center;
  align-items: center;
}
.cl{
  background-color: palevioletred;
  max-height: 300px;
  max-width: 300px;
}
img{
  background-image: url('/images-1.jpg');
  max-height: 200px;
  max-width: 300px;
}
</style>
</head>
<body>
<div class="demo_container">
<h1>CSS 尺寸属性 - 高度，宽度</h1>
<p class="cl">具有最大高度 "200" 和最大宽度 "300"</p><br>
<img src="images-1.jpg" alt="image" width="200px" height="200px">
</div>
</body>
</html>
```

代码的输出如下：

## CSS 尺寸属性 - 最大高度，最大宽度

![](img/87889aa057b33339873728c33e90f098_116_0.png)

CSS 尺寸属性 – max-height, max-width。

- 3. min-height 属性：元素内容区域的最小高度属性。此最小高度不包含内边距、边框或外边距。

该属性的语法给出：

```css
min-height: length | percentage | initial | inherit
```

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
width:800px;
height:500px;
margin:0 auto;
text-align: center;
justify-content: center;
align-items: center;
}
.cl{
background-color: palevioletred;
min-height: 200px;
min-width:200px;
}
img{
  background-image: url('/images-1.jpg');
  min-height: 200px;
  min-width:200px;
}
</style>
</head>
<body>
<div class="demo_container">
  <h1> CSS 尺寸属性 - 最小高度，最小宽度</h1>
  <p class="c1">具有最小高度 "200" 和 最小宽度 "300"</p>
  <img src="images-1.jpg" alt="image" width="200px" height="200px">
</div>
</body>
</html>
```

## CSS 生成内容属性

- 1. content 属性：content 属性-- CSS 属性用于与 ::before 和 :after 伪元素结合使用，以便在元素中生成内容。该属性的语法给出：

```css
content: normal | none | counter | string | url(url) | attr(attribute) | open-quote | close-quote | no-open-quote | no-close-quote | initial | inherit
```

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
width:800px;
height:500px;
margin:0 auto;
text-align: center;
justify-content: center;
align-items: center;
}
.before:::before{
  content: "Hi! ";
  display: inline;
  background-color: rgb(211, 81, 81);
}
.after:::after{
  content: "Bye! ";
  display: inline;
  background-color: rgb(224, 79, 79);
}
</style>
</head>
<body>
<div class="demo_container">
  <h1> CSS 内容属性</h1>
  <p class="before"> 文本将添加到你代码中的每个段落之前 </p>
  <p class="after"> 文本将添加到你代码中的每个段落之前 </p>
</div>
</body>
</html>
```

代码的输出如下：

## CSS 内容属性

**Hi** 文本将添加到你代码中的每个段落之前

文本将添加到你代码中的每个段落之前 **Bye**。

CSS 内容属性。

- 2. quotes 属性：quotes CSS 属性指定嵌入引用的引号。为此属性指定的引号字符将用于 content 属性的 open-quote（起始引号）和 close-quote（结束引号）值。

该属性的语法给出：

```css
quotes: [string string] one or more pairs | none | initial | inherit
```

## 示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
width:800px;
height:500px;
margin:0 auto;
text-align: center;
justify-content: center;
align-items: center;
}
q{
 quotes: '[' ']' '"' '"';
}
.q::before {
content: open-quote;
}
.q::after {
content: close-quote;
}
</style>
</head>
<body>
<div class="demo_container">
<h1> CSS 内容属性</h1>
<p class="before"><q> 文本将添加到你代码中的每个段落之前，带有 <q>嵌入引用</q></p>
<p class="after"> 文本将添加到你代码中的每个段落之前 <q>嵌入引用</q></p>
</div>
</body>
</html>
```

- 3. counter-reset 属性：counter-reset CSS 属性与 counter-increment 属性结合使用以创建计数器，并与 content 属性结合以显示生成的值。

该属性的语法如下：

```css
counter-reset: [ identifier integer ] more pairs | none | initial | inherit
```

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
width:800px;
height:500px;
margin:0 auto;
text-align: center;
justify-content: center;
align-items: center;
}
h1 {
  counter-reset: category;
}
::before {
  counter-increment: category;
  content: counter(category);
}
.after {
  counter-increment: category;
  content: counter(category);
}
li{
  list-style: none;
}
</style>
</head>
<body>
<div class="demo_container">
  <h1> 计数器重置</h1>
  <ul class="before">A</ul>
  <ul class="after">B</ul>
</div>
</body>
</html>
```
