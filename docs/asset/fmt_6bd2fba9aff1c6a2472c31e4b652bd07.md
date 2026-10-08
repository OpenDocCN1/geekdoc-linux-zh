
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
  background: red;
}

/* 选择兄弟元素中的第三个元素 */
li:nth-child(3) {
  background: yellow;
}
</style>
</head>
<body>
<div class="demo_container">
  <h2>:last-child(n) 选择器匹配父元素的最后一个 n 个元素。 </h2>
  <ul>
    <li>第一个列表项</li>
    <li>第二个列表项</li>
    <li>第三个列表项</li>
    <li>第四个列表项</li>
    <li>第五个列表项</li>
  </ul>
</div>
</body>
</html>
```

代码的输出如下：

# `:last-child(n)` 选择器匹配父元素的最后一个 n 个元素。

- 第一个列表项
- 第二个列表项
- 第三个列表项
- 第四个列表项
- 第五个列表项

## 伪类 (`:first-child`)

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

/* 选择列表中的第二个 li 元素（注：原文注释写为第二个，但代码是first-child） */
li:first-child{
  background: red;
}
</style>
</head>
<body>
<div class="demo_container">
  <h2>:first-child 选择器匹配父元素的第一个 n 个元素。 </h2>
  <ul>
    <li>第一个列表项</li>
    <li>第二个列表项</li>
    <li>第三个列表项</li>
    <li>第四个列表项</li>
    <li>第五个列表项</li>
  </ul>
</div>
</body>
</html>
```

代码的输出如下：

## `:first-child` 选择器匹配父元素的第一个 n 个元素。

- 第一个列表项
- 第二个列表项
- 第三个列表项
- 第四个列表项
- 第五个列表项

## 伪类 (`:only-child`)

示例：

```html
<!DOCTYPE html>
<html>
<head>
<style>

demo_container{
  width:600px;
  margin:0 auto;
  justify-content: center;
  align-items: center;
}

/* 选择列表中的第二个 li 元素 */
li:only-child{
  background: red;
}
</style>
</head>
<body>
<div class="demo_container">
  <h2>:only-child 选择器选择父元素的唯一元素。 </h2>
  <h3>列表 1</h3>
  <ul>
    <li>第一个列表项</li>
    <li>第二个列表项</li>
    <li>第三个列表项</li>
    <li>第四个列表项</li>
    <li>第五个列表项</li>
  </ul>
  <h3>列表 2</h3>
  <ul>
    <li>第一个列表项</li>
  </ul>
</div>
</body>
</html>
```

代码的输出如下：

**:only-child 选择器选择父元素的唯一元素。**

## 列表 1

- 第一个列表项
- 第二个列表项
- 第三个列表项
- 第四个列表项
- 第五个列表项

## 列表 2

- 第一个列表项

```css
.demo_container{
  width:600px;
  margin:0;
  justify-content: center;
  align-items: center;
}
```

```css
/* Selects the second li in a list */
li:nth-of-type(odd) {
  width:200px;
  background: red;
}
```

```css
li:nth-of-type(even) {
  width:200px;
  background: green;
}
```

```html
</style>
</head>
<body>
<div class="demo_container">

## :only-child selectors selects an element, only child of its parent.

### List 1
<ul>
  <li>First list item</li>
  <li>Second list item</li>
  <li>Third list item</li>
  <li>Fourth list item</li>
  <li>Fifth list item</li>
</ul>

### List 2
<ul>
  <li>First list item</li>
</ul>
</div>
</body>
</html>

# PSEUDO-CLASSES (:nth-of-type(odd or even))

The `:nth-of-type(n)` selector matches every element, that is the nth child, of the same type, of its parent.

Example:

```html

<!DOCTYPE html>

<html>

<head>

<style>

.demo_container{

  width:600px;

  margin:0;

  justify-content: center;

  align-items: center;

}

/* Selects the second li in a list */

li:nth-of-type(odd) {

  width:200px;

  background: red;

}

:nth-of-type(even) {

  width:200px;

  background: green;

}

</style>

</head>

<body>

<div class="demo_container">

<h2>The (:nth-of-type(odd), nth-of-type(even)) selectors selects an element, only child of its parent.</h2>

### List 1

<ul>

  <li>First list item</li>

  <li>Second list item</li>

  <li>Third list item</li>

  <li>Fourth list item</li>

  <li>Fifth list item</li>

</ul>

### List 2

<ul>

<ul>

  <li>First list item</li>

</ul>

</div>

</body>

</html>

```

The output of the code is given below:

# The (:nth-of-type(odd), nth-of-type(even)) selectors selects an element, only child of its parent.

# List 1

- First list item
- Second list item
- Third list item
- Fourth list item
- Fifth list item

# List 2

- First list item

Pseudo-classes (:nth-of-type(odd or even)).

# PSEUDO-CLASSES (:first-of-type, nth-of-type, nth-last-of-type(3))

Example:

```html

<!DOCTYPE html>

<html>

<head>

<style>

demo_container{

  width:600px;

  margin:0;

  justify-content: center;

  align-items: center;

}

/* Selects the second li in a list */

li:first-of-type {

  width:200px;

  background: red;

}

li:nth-of-type(even) {

  width:200px;

  background: green;

}

li:nth-last-of-type(3) {

  width:200px;

  background: yellow;

}

```

```html

</style>

</head>

<body>

<div class="demo_container">

<h2>The (:first-of-type, nth-of-type, nth-last-of-type(3)) selectors selects an element, only child of its parent.</h2>

### List 1

<ul>

  <li>First list item</li>

  <li>Second list item</li>

  <li>Third list item</li>

  <li>Fourth list item</li>

  <li>Fifth list item</li>

</ul>

```

# 246 ■ Mastering CSS

```html

### List 2

<ul>

  <li>First list item</li>

</ul>

</div>

</body>

</html>

```

The output of the code is given below:

# The (:first-of-type, nth-of-type, last-of-type(3)) selectors selects an element, only child of its parent.

List 1

- First list item
- Second list item
- Third list item
- Fourth list item
- Fifth list item

List 2

- First list item

Pseudo-classes (:first-of-type, nth-of-type, nth-last-of-type(3)).

# COMBINATORS

COMBINATORS (E F)
It select style all h1 elements AND all h4 elements.

Example:

```html

<!DOCTYPE html>

<html>

<head>

<style>

.demo_container{

  width:600px;

  margin:0;

  justify-content: center;

  align-items: center;

}

h1{

  background-color: pink;

}

h4{

  background-color: lightblue;

}

```

```html

</style>

</head>

<body>

<div class="demo_container">

<h2>It select all h1 elements and all h4 elements.</h2>

### List 1

<ul>

  <li>First list item</li>

  <li>Second list item</li>

  <li>Third list item</li>

  <li>Fourth list item</li>

  <li>Fifth list item</li>

</ul>

### List 2

<ul>

  <li>First list item</li>

</ul>

</div>

</body>

</html>

```

It is also called a descendant selector ().

The output of the code is given below:

It select all h1 elements and all h4 elements.

List 1

- First list item
- Second list item
- Third list item
- Fourth list item
- Fifth list item

List 2

- First list item

This is H1 Heading

This is H4 Heading

Combinators selectors (E > F).

# COMBINATORS (E > F)
It is a child selector (>). It selects all elements that are the children of specified element.

Example:

```html

<!DOCTYPE html>

<html>

<head>

<style>

.demo_container{

  width:600px;

  margin:0;

  justify-content: center;

  align-items: center;

}

```

```css

ul > li {

  background-color: pink;

  border:2px solid darkgreen;

}

```

```html

</style>

</head>

<body>

<div class="demo_container">

<h2>It selects all elements that are the children of a specified element.</h2>

### List 1

<ul>

  <li>First list item</li>

  <li>Second list item</li>

  <li>Third list item</li>

  <li>Fourth list item</li>

  <li>Fifth list item</li>

</ul>

### List 2

<ul>

  <li>First list item</li>

</ul>

<h1>This is H1 Heading</h1>

<h4>This is H4 Heading</h4>

</div>

</body>

</html>

```

250 ■ Mastering CSS

The output of the code is given below:

It selects all elements that are the children of a specified element

List 1

- First list item
- Second list item
- Third list item
- Fourth list item
- Fifth list item

List 2

- First list item

This is H1 Heading

This is H4 Heading

Combinators selectors (E + F).

# COMBINATORS (E + F)
The adjacent sibling selector selects an element that is directly after another specific element. It is also called adjacent sibling selector (+).

Example:

```html

<!DOCTYPE html>

<html>

<head>

<style>

.demo_container{

  width:600px;

  margin:0;

  justify-content: center;

  align-items: center;

}

```

```css

h1 + h4 {

  background-color: pink;

  border:2px solid darkgreen;

}

```

```html

</style>

</head>

<body>

<div class="demo_container">

<h2>The + selector is used to select an element that is directly after another specific element.</h2>

### List 1

<ul>

  <li>First list item</li>

  <li>Second list item</li>

</ul>

### List 2

<ul>

  <li>First list item</li>

</ul>

<h1>This is H1 Heading</h1>
