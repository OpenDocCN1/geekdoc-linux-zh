
正如我提到的，所有状态的通用样式应该放在 `anchor` 元素中，以便利用继承特性。不需要在任何伪选择器中添加此声明，因为它们将继承该规则（参见图 10-5）。

![](img/516568206e0e220ce5a120446a34b48d_181_1.png)

**图 10-5** 看，妈妈——没有下划线！

你也可以混合使用规则。一些设计师喜欢下划线仅在悬停状态出现。要实现这一点，你只需要在 `:hover` 选择器中添加 `text-decoration: underline;` 声明，由于选择器的优先级（specificity），它会覆盖 `anchor` 中的继承值（有关优先级的更多细节，请参见第 7 章“使用 CSS”）。图 10-6 显示了链接在悬停状态激活之前没有下划线。

![](img/516568206e0e220ce5a120446a34b48d_181_2.png)

**图 10-6** 链接、已访问、悬停和激活状态，在悬停状态下带有下划线。

## 使用类选择器使用多种链接样式

CSS 提供的另一个优秀选项是允许文档中拥有多种样式的链接。当你页面上的某些区域需要不同的样式时，这特别有用。

```css
/* link styles for all descendant links of the example2 division */

#example2 (background-color: white; color: black);

#example2 a (color: lime);

#example2 alink (color: lime);

#example2 a:visited (color: red);

#example2 a:hover (color: aqua; text-decoration: underline);

#example2 a:active (color: fuchsia);
</style>
</head>
<body>
<div id="example1">
<p>I married early, and was happy to find in my wife a disposition not uncongenial with my own. Observing her partiality for domestic pets, she lost no opportunity of procuring those of the <a href="http://www.prenhall.com/#most">agreeable kind. We had birds, gold fish, a fine dog, rabbits, a small monkey, and a cat.</p>
</div>
<div id="example2">
<p>This letter was a <a href="http://www.prenhall.com/">remarkably</a>a> large and beautiful animal, entirely black, and sagacious. In speaking of his intelligence, my wife, who at heart was not a little tinted with superstition, made frequent allusion to the ancient popular notion, which regarded all black cats as witches in disguise. Not that she was ever serious upon this point - and I mention the matter at all for no reason than that it happens, just now, to be remembered.</p>
</div>
</body>
</html>
```

在这种情况下，两个 `div` 都有 `ID`。因为没有为 `example1` 定义链接样式，所以它们将采用默认值。但由于我专门为 `example2` 创建了链接样式，这些样式将应用于该 `div` 内部所有的后代链接（见图 10-8）。

I married early, and was happy to find in my wife a disposition not uncongenial with my own. Observing her partiality for domestic pets, she lost no opportunity of procuring those of the most agreeable kind. We had birds, gold fish, a fine dog, rabbits, a small monkey, and a cat.

This letter was a large and beautiful animal, entirely black, and sagacious to an astonishing degree. In speaking of his intelligence, my wife, who at heart was not a little tinted with superstition, made frequent allusion to the ancient popular notion, which regarded all black cats as witches in disguise. Not that she was ever serious upon this point - and I mention the matter at all for no reason than that it happens, just now, to be remembered.

**图 10-8** 使用后代选择器应用多个链接，通过避免类名泛滥（classitis）简化了 CSS 和标记语言。

链接效果、列表与导航 > 使用后代选择器样式化链接

## 样式化有序列表

关于列表，你将开始样式化有序列表。你将修改标记类型，然后用图像完全替换标记。我从一些文本和背景样式开始，配合一个无样式的有序列表，得到了图 10-9。

## 往派对的路线！

![](img/516568206e0e220ce5a120446a34b48d_185_0.png)

+ 1. 从百老汇和第五大道的转角，右转进入第五大路。
2. 沿着第五大路向北走约三英里，直到到达橡树路（Oak Road）路口。
3. 在橡树路右转。沿着橡树路一直走约五英里。
4. 你会在橡树路和藤蔓路（Vine）处看到一个路口，继续沿橡树路走两个街区。
5. 左转进入布姆街（Brome Street）。我们在右侧的第三家。

**图 10-9** 一个带有样式化有序列表的页面。

如果你想使用备用标记，可以使用 `list-style-type` 属性配合相应的值（支持其他语言的数字），但你可能想在有序列表中更换的标记分别是十进制-零（从零开始编号）以及对应的小写罗马数字或大写罗马数字。只需在你现有的样式表中添加你想要使用的值即可：

```css
ol {list-style-type: lower-roman;}
```

这将导致数字显示为小罗马数字（见图 10-10）。

## 往派对的路线！

![](img/516568206e0e220ce5a120446a34b48d_185_1.png)

i. 从百老汇和第五大道的转角，右转进入第五大路。
ii. 沿着第五大路向北走约三英里，直到到达橡树路路口。
iii. 在橡树路右转。沿着橡树路一直走约五英里。
iv. 你会在橡树路和藤蔓路处看到一个路口，继续沿橡树路走两个街区。
v. 左转进入布姆街。我们在右侧的第三家。

**图 10-10** 使用小写罗马数字样式化有序列表。

如果你想将数字替换为图像，可以为所需的每个数字创建图像并并每个列表项应用类以获得结果（见示例 10-6）。

## 示例 10-6 使用类应用于有序列表

```html
<!DOCTYPE html PUBLIC "//W3C//DTD HTML 1.0 Transitional//EN"
   "http://www.w3.org/TR/html1/html1-transitional.dtd">
<html xmlns="http://www.w3.org/1999/xhtml">
<head>
  <title>working with</title>
  <style type="text/css">
body { font: 14px Georgia, serif; color: black; background-image:
  url(balloons.gif); background-position: right; background-repeat: no-repeat;}
```
