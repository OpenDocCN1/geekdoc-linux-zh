
## CSS 边框属性 - 左、下、右、上

Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime mollitia, molestiae quas vel sint commodo repudiandae consequuntur voluptatum laborum numquam blanditiis harum quisquam eum est sed odit fugiat iusto fuga praesentium optio, eaque rerum!

Provident similique accantium nemo autem. Veritatis obcaecati tenetur iure eum earum ut molestiae architecto voluptate aliquam nihil, eveneniet aliquid culpa officia aut!

Lorem ipsum dolor sit amet consectetur adipisicing elit. Maxime mollitia, molestiae quas vel sint commodo repudiandae consequuntur voluptatum laborum numquam blanditiis harum quisquam eum est sed odit fugiat iusto fuga praesentium optio, eaque rerum!

Provident similique accantium nemo autem. Veritatis obcaecati tenetur iure eum earum ut molestiae architecto voluptate aliquam nihil, eveneniet aliquid culpa officia aut!

CSS 边框属性 – 左、下、右、上。

- 3. **border-bottom-color 属性**：`border-bottom-color` 属性用于单独设置元素底部边框的颜色。然而，在其他情况下，像 `border color` 或 `border bottom` 这样的简写属性更方便使用且更优。该属性的语法如下：

```css
border-bottom-color: color | transparent | inherit
```

## CSS 属性 ■ 79

## 示例：

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
.text-1 {
  border-style: solid;
  border-bottom-color: #d83838;
}
.text-2{
  border-style: solid;
  border-left-color: #aec730;
}
text-3{
  border-style: solid;
  border-right-color: #e12424;
}
text-4{
  border-style: solid;
  border-top-color: #ffaa00;
}
</style>
</head>
<body>
<div class="demo_container">
<h1>CSS 底部边框属性 - 左、下、右、上</h1>
<p class="text-1">Lorem ipsum dolor sit amet adipisicing elit. Maxime mollitia, molestiae quas vel sint commodo repudiandae consequatur consequuntur voluptatum laborum nonquam blanditiis harum quisquam eius sed odit fugiat iusto fuga praesentium optio, aeque rerum!</p>
<p class="text-2">Provident similique accusamiam nemo autem. Veritatis obcaecati tenetur iure eum earum ut molestias architecto voluptate aliquam nihil, eveniet aliquid culpa officia aut!</p>
<p class="text-3">Lorem ipsum dolor sit amet consectetur adipiscing elit. Maxime mollitia, molestiae quas vel sint commodi repudiandae consequuntur voluptatum laborum numquam blanditiis harum quisquam eius sed odit fugiat iusto fuga praesentium optio, aeque rerum!</p>
<p class="text-4">Provident similique accusamiam nemo autem. Veritatis obcaecati tenetur iure eum earum ut molestias architecto voluptate aliquam nihil, eveniet aliquid culpa officia aut!</p>
</div>
</body>
</html>
```

- 4. **border-bottom-left-radius 属性**：`border-bottom-left-radius` 属性用于设置元素边框盒“左下”角的的圆角形状。

示例：

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
```
```css
.text-1 {
  border-style: solid;
  border-bottom-left-radius: 20px;
}
.text-2{
  border-style: solid;
  border-bottom-right-radius: 20px;
}
```
```css
</style>
</head>
<body>
<div class="demo_container">
  <h1>CSS 底部左下角属性 - 左、右</h1>
  <p class="text-1">Lorem sit amet consectetur adipiscing elit. Maxime mollitia, molestiae quas vel sint commodo numquam repudiandae consequuntur voluptam eius sed od fugiat iusto fuga quisquam eius blanditiis harum praesentium optio, eque rerum!</p>
  <p class="text-2">Provident similique accusamantium iure autem. Veritatis obcaecati tenetur iure earum ut molestias architecto voluptate aliquam nhil, eveniet aliquid culpa officia aut!</p>
</div>
</body>
</html>
```

代码的输出如下：

## CSS 底部边框属性 - 左、下、右、上

| 文本内容 |
| :--- |
| Lorem ipsum dolor sit amet consectetur adipiscing elit. Maxime mollitia, molestiae quas vel sint commodi repudiandaeandae consequuntur voluptatum laborum numquam land-tiis harum quisquam eius sed odit fugiat iusto fuga praesentium optio, eque rerum! |
| Provident similike accuantium nemo autem. Veritatis obcaecati tenetur iure eius earum ut molestias architecto voluptate aliquam nihil, eveniet aliquid culpa officia aut! |
| Lorem ipsum dolor sit amet consectetur adipiscing elit. Maxime mollitia, molestiae quas vel sint commodi repudiandaeandae consequuntur voluptatum laborum numquam land-tiis harum quisquam eius sed odit fugiat iusto fuga praesentium optio, eque rerum! |
| Provident similike accuantiam nemo autem. Veritatis obcaecati tenetur iure eius earum ut molestias architecto voluptate aliquam nihil, eveniet aliquid culpa officia aut! |

- 5. **border-bottom-color 属性**：`border-bottom-color` 属性用于单独设置元素底部边框的颜色。然而，在其他情况下，像 `border color` 或 `border bottom` 这样的简写属性更方便使用且更优。该属性的语法如下：

```css
border-bottom-color: color | transparent | inherit
```

## 86 精通 CSS

## 6. border-image 属性：`border-image` CSS 属性指定了如何使用图像来代替边界样式。这是一个用于一次性设置 `border-image-source`、`border-image-width`、`border-image-slice`、`border-image-outset` 和 `border-image-repeat` 属性的属性。该属性的语法如下：

```
border-image: [ source slice width outset repeat ] | initial | inherit
```

示例：

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
.box {
  width: 300px;
  height: 150px;
  border: 15px solid transparent;
  border-image: url("/images-1.jpg") 30 30 round;
}
</style>
</head>
<body>
<div class="demo_container">
  <h1> CSS border-image 属性</h1>
  <div class="box"></div>
</div>
</body>
</html>
```

代码的输出如下：

## CSS border-image 属性

![](img/87889aa057b33339873728c33e90f098_105_0.png)

CSS border-image 属性。

## CSS 颜色属性

CSS 颜色功能设置文本元素内容的颜色。所有现代网络浏览器都支持不同的颜色以保持色彩丰富的显示。在 CSS 中，颜色可以用多种方式表示，甚至可以使用诸如 "color: blue" 这样的颜色单词。然而，这种方法仅支持颜色名称。因此，在 CSS 中使用了其他更高级的方法来显示颜色，如 RGB、HSL、HEX 等。

示例：

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
color: black;
}
.c2 {
color:green
}
</style>
</head>
<body>
<div class="demo_container">
  <h1>CSS 颜色属性</h1>
  <p class="c1">这里我们使用简单的颜色代码（黑色）。</p><br>
  <p class="c2">这里我们使用简单的颜色代码（绿色）。</p><br>
</body>
</html>
```

代码的输出如下：

## CSS 颜色属性

这里我们使用简单的颜色代码（黑色）。

这里我们使用简单的颜色代码（绿色）。

CSS 颜色属性 (color)。

## RGB 颜色

RGB 是三种颜色（红、绿、蓝）的组合，用于所有计算机程序中显示颜色。正如我们所知，这些是基础色，通过组合它们，我们可以找到色谱中出现的任何颜色。

示例：

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
color: rgb(205, 92, 92);
}
.c2 {
color:rgb(100, 149, 237);
}
</style>
</head>
<body>
<div class="demo_container">
<h1>CSS 颜色属性 (RGB)</h1>
<p class="c1">这里我们使用 RGB 代码（rgb(205, 92, 92)).</p><br>
<p class="c2">这里我们使用 RGB 颜色代码（rgb(100, 149, 237)).</p><br>
</body>
</html>
```
