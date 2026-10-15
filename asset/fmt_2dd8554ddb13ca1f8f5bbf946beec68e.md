
```html
<!DOCTYPE html>
<html
<head>
<style>
.demo_container{
  width:600px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
input {
  font-size: 1.5rem;
  margin: 10px;
  padding: 10px;
  width: 100%;
}
input:placeholder-shown {
  border: 5px solid red;
}
form {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
* {
  box-sizing: border-box;
}
body {
  padding: 1em;
}
input[type=checkbox] + label {
  color: #ccc;
  font-style: italic;
}
input[type=checkbox]:checked + label {
  color: #f00;
  font-style: normal;
}
</style>
</head>
<body>
<div class="demo_container">
<h1>伪类 (:checked)</h1>
<form>
<p>:checked 伪类在处于选中状态时选择元素。</p>
<input type="checkbox" id="title">
<label for="title">正在使用 CSS</label>
</form>
</div>
</body>
</html>
```

## 222 精通 CSS

## 伪类 (:checked)

`:checked` 伪类在处于选中状态时选择元素。

伪类（`:checked`）-

# 伪类 (:indeterminate)-

`:indeterminate` 选择器用于选择处于既未选中也未取消状态的表单元素。

示例：

```html
<!DOCTYPE html>
<html
<head>
<style>
.demo_container{
  width:600px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
form {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
* {
  box-sizing: border-box;
}
body {
  padding: 1em;
}
input:indeterminate + label {
  background: green;
  color: white;
  padding: 4px;
}
input:indeterminate {
  box-shadow: 0 0 1px 1px green;
}
</style>
</head>
<body>
<div class="demo_container">
<h2>CSS :indeterminate</h2>
<input type="checkbox" id="checkbox">
<label for="checkbox">这是一个不定的复选框。</label>
<br>
<input type="radio" id="radio" name="abc">
<label for="radio">这是一个不定的单选按钮。</label>

<script>
var doc = document.getElementsByTagName("input");

for (var i = 0; i < doc.length; i++) {
  doc[i].indeterminate = true;
}
</script>
</div>
</body>
</html>
```

代码的输出如下：

## CSS :indeterminate

伪类（`:indeterminate`）。

## CSS 类 (:valid 和 :invalid)

`:valid` 选择器根据元素设置验证表单元素。`:invalid` 伪类应用于内容不符合类型的表单字段。

示例：

```html
<!DOCTYPE html>
<html
<head>
<style>
.demo_container{
  width:600px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
form {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
* {
  box-sizing: border-box;
}
body {
  padding: 1em;
}
input {
  border-radius: 20px;
  width: 250px;
  background: #b4f7ab;
  border: 1px solid #06bca7;
  padding: 3px 10px;
  height:50px
}
input:invalid {
  background: #fc9cac;
  border: 1px solid #bc0624
}
</style>
</head>
<body>
<div class="demo_container">
<h2>CSS CSS :indeterminate 选择器</h2>
<label> 姓名：</label><input type="text" placeholder="输入文本 " <br>
<label> 数字：</label><input type="number" placeholder="输入数字" <br>
<label> 邮箱：</label><input type="email" placeholder="在此输入邮箱" <br>
<script>
var doc = document.getElementsByTagName("input");

for (var i = 0; i < doc.length; i++) {
  doc[i].indeterminate = true;
}
</script>
</div>
</body>
</html>
```

## 伪类 (:in-range 和 :out-range)

`:in-range` 选择值在代码指定范围内的元素，`:out-of-range` 选择值在代码范围外的元素。

示例：

```html
<!DOCTYPE html>
<html
<head>
<style>
.demo_container{
  width:600px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}
form {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}
input:in-range {
  border: 5px solid violetblue;
}
input:out-of-range {
  border: 5px solid magenta;
}
</style>
</head>
<body>
<div class="demo_container">
<h2>CSS (:in-range 和 :out-range) 选择器</h2>
<p>输入 5 到 20 之间的数字范围以查看输入字段上的样式</p>
<input type="number" min="5" max="20" placeholder="输入数字"><span> （ 范围代码将运行 ） </span><br><br>
<input type="number" min="5" max="20" placeholder="输入数字"><span>（超出范围代码将运行）</span>
</div>
</body>
</html>
```

` 标签内包含了完整的内容，我将对您提供的所有 Markdown  进行了翻译。

以下是完整的中文翻译：

## 伪类 (:required)

示例：

```html
<!DOCTYPE html>
<html><head>
<style>
.demo_container{
  width:600px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}

form {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

*{
  box-sizing: border-box;
}

body {
  padding: 1em;
}
input {
  border-radius: 20px;
  width:250px;
  border: 1px solid #06bca7;
  padding: 3px 10px;
  height:50px
}

input:required {
  background-color: pink;
}
</style>
</head>
```

```html
<body>
<div class="demo_container">
  <h2> CSS 选择器 (:required) </h2>
  <input type="number" placeholder="输入数字">
  <br><br>
  <input type="number" placeholder="输入数字（必填）" required>
</div>
</body>
</html>
```

## 伪类 (:optional)

示例：

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

form {
  display: flex;
  justify-content: center;
  align-items: center;
  flex-direction: column;
}

*{
  box-sizing: border-box;
}

body {
  padding: 1em;
}

input {
  border-radius: 20px;
  width:250px;
  border: 1px solid #06bca7;
  padding: 3px 10px;
  height:50px
}

input:required {
  background-color: lightcoral;
}

input:optional {
  background-color: lightgray;
}
</style>
</head>
<body>
<div class="demo_container">
<h2>CSS 选择器 (:optional)</h2>
<input type="number" placeholder="输入数字（可选）"><br><br>
<input type="number" placeholder="输入数字（必填）" required>
</div>
</body>
</html>
```

代码的输出如下：

## CSS 选择器 (:optional)

![](img/87889aa057b33339873728c33e90f098_249_0.png)

![](img/87889aa057b33339873728c33e90f098_249_1.png)

伪类 (:required, :optional)。

## 伪类 (:root)

`:root` 选择器匹配文档的根元素。

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
:root {
background: #ff0000;
font-size: 30px;
}
</style>
</head>
<body>
<div class="demo_container">
<h2> CSS 选择器 (:root) </h2>
<p> 它为整个文档设置了背景颜色，并将所有的 CSS 同样地应用于 HTML 中的所有元素 </p>
</div>
</body>
</html>
```

代码的输出如下：

```
CSS 选择器 (:root)
它为整个文档设置了背景颜色，并将所有的 CSS 同样地应用于 HTML 中的所有元素
```

伪类 (:root)。

## 伪类 (:empty)

它为空空的 `<p>` 元素指定背景颜色。

示例：

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
p:empty {
  width: 100px;
  height: 20px;
  background: #ff0000;
}
</style>
</head>
```

```html
<body>
<div class="demo_container">
  <h2> CSS 选择器 (:empty) </h2>
  1. <p></p>
  2. <p> 非空 </p>
  3. <p> (带有单个空格的标签也不能被视为空的 )</p>
</div>
</body>
</html>
```

代码的输出如下：

## CSS 选择器 (:empty)

- 1.

- 2. 非空

- 3. (带有单个空格的标签也不能被视为空的 )

![](img/87889aa057b33339873728c33e90f098_252_0.png)

伪类 (:empty)。

## 伪类 (:blank) *(注：原文此处为 :blank，通常指 :empty，此处保留原文翻译)*

示例：

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

p {
  min-height: 30px;
  width: 250px;
  background-color: lightblue;
}

p:blank { display: none; }
</style>
</head>
<body>
<div class="demo_container">
  <h2>CSS 选择器 (:blank)</h2>
  <div class="blanks">
    <p>段落不是空的或空白的。</p>
    <p>这不是空的，因为它有空格。它是空白的。</p>
    <p>段落不是空的或空白的。</p>
  </div>
</div>
</body>
</html>
```

代码的输出如下：

## CSS 选择器 (:blank)

| 段落不是空的或空白的。 |

| --- |

| 段落不是空的或空白的。 |

伪类 (:blank)。

## 伪类 (:nth-child)

示例：

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

/* 选择列表中的第二个 li 元素 */
li:nth-child(2) {
  background: green;
}

/* 选择兄弟元素中的第三个元素 */
li:nth-child(3) {
  background: yellow;
}
</style>
</head>
<body>
<div class="demo_container">
  <h2>:nth-child(n) 选择器匹配父元素的第 n 个元素。 </h2>
  <div>
    <p>这里有一些文本。</p>
  </div>
  <div>
    <p>这里有一些文本。</p>
    <ul>
      <li>第一个列表项</li>
      <li>第二个列表项</li>
      <li>第三个列表项</li>
      <li>第四个列表项</li>
      <li>第五个列表项</li>
    </ul>
  </div>
</div>
</body>
</html>
```

代码的输出如下：

## :nth-child(n) 选择器匹配父元素的第 n 个元素。

- 第一个列表项

- 第二个列表项

- 第三个列表项

- 第四个列表项

- 第五个列表项

## 伪类 (:last-child)

示例：
