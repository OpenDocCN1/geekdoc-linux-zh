
代码的输出如下：

## 计数器重置

A
B

## FLEX 布局

`align-content` 属性描述了 flex 容器内行的对齐方式。当有剩余空间时，它决定了行如何分布。

- 1. `center`：在容器中居中对齐。
- 2. `flex-start`：在容器的起始处对齐。
- 3. `flex-end`：在容器的末尾对齐。
- 4. `stretch`：拉伸以填充容器空间（默认值）。
- 5. `space-around`：在行周围均匀分布剩余空间。
- 6. `space-between`：在行之间均匀分布剩余空间，两端对齐。
- 7. `initial`：设为默认值。
- 8. `inherit`：继承父元素的值。

该属性的语法给出：

```css
align-content: center | flex-start | flex-end | stretch | space-around | space-between | initial | inherit
```

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
  display: flex;
  flex-wrap: wrap;
  align-content: space-around;
  width: 500px;
  height: 500px;
  margin: 0 auto;
  background: lightgrey;
}
.item{
  width: 100px;
  height: 100px;
  background: tomato;
}
</style>
</head>
<body>
<div class="demo_container">
  <div class="item">1</div>
  <div class="item">2</div>
  <div class="item">3</div>
  <div class="item">4</div>
  <div class="item">5</div>
  <div class="item">6</div>
</div>
</body>
</html>
```

代码的输出如下：

## FLEX 布局

| 1 | 2 | 3 |
|---|---|---|
| 4 | 5 | 6 |

### CSS 字体属性

`font` 属性设置元素文本内容的样式、变体、粗细、行高和字体。它是为了在一个声明中设置单个字体属性，即 `font-style`、`font-variant`、`font-weight`、`font-size`、`line-height` 和 `font-family`。

该属性的语法给出：

```css
font: [ font-style font-variant font-weight font-size line-height font-family | caption | icon | menu | message-box | small-caption | status-bar | initial | inherit ]
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
.before{
  font: bold 2.5em "Times Roman", Times,
  serif;
}
.after{
  font: normal 1.2em Arial, Helvetica, sans-serif;
}
</style>
</head>
<body>
<div class="demo_container">
  <h1> CSS 字体属性</h1>
</div>
</body>
</html>
```

## CSS 属性 ■ 113

在这里你可以获得 `list-style-type` 的多种值。

## CSS MARGIN 属性

`margin` 属性设置元素四边的外边距。它是 `margin-top`（上边距）、`margin-right`（右边距）、`margin-bottom`（下边距）和 `margin-left`（左边距）属性的复合属性。

该属性的语法如下：

```
margin: [ 长度 | 百比 | auto ] 1 到 4 个值 | initial | inherit
```

### 示例

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
width:600px;
margin:0 auto;
text-align: center;
justify-content: center;
border:1px solid red;
align-items: center;
}
.text-1 {
border-style: solid;
margin: 25px;
}
.text-2{
border-style: solid;
margin: 20px 20px 20px 20px;
}
.text-3{
border-style: solid;
margin: 30px 30px;
}
.text-4{
border-style: solid;
margin: 30px 0px 30px 0px;
}
</style>
</head>
<body>
<div class="demo_container">
<h1>CSS margin 属性</h1>
<p class="text-1">Lorem ipsum sit amet consectetur adipisicing elit. Maxime mollitia, molestae quas vel sit commodi repudiandae consequuntur voluptatum laborum numquam blanditiis harum quisquam eum sed odit fugiat iusto fuga praesentium optio, eque rerum!</p> <br>
<p class="text-2">Provident similique accusantium nemo autem. Veritatis obcaecati tenitur iure earum ut molestias architecto voluptate aliquam nihil, eveneniet aliquid culpa officia aut!</p> <br>
<p class="text-3">Lorem ipsum dolor sit amet consectetur adipiscing elit. Maxime mollitia, molestae quas vel sit commodi repudiandae consequuntur voluptatum laborum numquam blanditiis harum quisquam eum sed odit fugiat iusto fuga praesentium optio, eque rerum!</p> <br>
<p class="text-4">Provident similique accuantium autem. Veritatis obcaecati tenitur iure earum ut molestias architecto voluptate aliquam nihil, eveneniet culpa officia aut!</p> <br>
</body>
</html>
```

这种表示法可以接受一个、二、三个或四个由空白符分隔的值。

- 1. 如果设置一个值，则 `margin` 应用于所有四边。
- 2. 如果设置两个值，则第一个值应用于顶部和底部，第二个值应用于右侧和左侧。
- 3. 如果设置三个值，则这些值分别应用于顶部、水平方向（即右侧和左侧）、底部。
- 4. 如果设置四个值，则按相同顺序应用于顶部、右侧、底部、左侧。

与其使用 `margin`，你应该使用其他各种 `margin-top`、`margin-right`、`margin-bottom` 和 `margin-left`。

### 示例

```html
<!DOCTYPE html>
<html>
<head>
<style>
.demo_container{
width:600px;
margin:0 auto;
text-align: center;
justify-content: center;
border: 2px solid black;
align-items: center;
}
.text-1 {
border:1px solid red ;
margin-top: 25px;
}
.text-2{
border:1px solid red ;
margin-right: 20px;
}
.text-3{
border:1px solid red ;
margin-bottom: 20px;
}
.text-4{
border:1px solid red ;
margin-left: 30px ;
}
</style>
</head>
<body>
<div class="demo_container">
<h1>CSS margin - 属性 (上边距, 右边距,下边距,左边距)</h1>
<p class="text-1">Lorem dolor sit amet consectetur adipiscing elit. Maxime mollitia, molestiae quas vel sint commudi repudiandae consequuntur voluptatum laborum numquam blanditiis harum quisquam eius sed odit fugiat iusto fuga praesentium optio, eaque rerum!</p><br>
<p class="text-2">Provident similique accusantium nemo autem. obcaecati tenetur iure eius harum ut molestias architecto voluptate aliquam nihil, eveneniet aliquid culpa officia aut!</p><br>
<p class="text-3">Lorem ipsum dolor sit amet consectetur adipiscing elit. Maxime mollitia, molestiae quas vel sint commudi repudiandae consequuntur voluptatum laborum numquam blanditiis harum quisquam eius sed odit fugiat iusto fuga praesentium optio, eaque rerum!</p><br>
<p class="text-4">Provident similique accusantium nemo autem. Veritatis tenetur iure eius harum ut molestias architecto voluptate aliquam nihil, eveneniet culpa officia aut!</p><br>
</body>
</html>
```

```html
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="utf-8">
<title>CSS3 column-count 属性示例</title>
<style>
 p {
  column-count: 2; /* 标准语法 */
}
</style>
```

## CSS3 column-count 属性
