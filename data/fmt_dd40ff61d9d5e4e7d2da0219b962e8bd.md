
![](img/516568206e0e220ce5a120446a34b48d_164_0.png)

**图 9-7** 应用 body、h1、h2 和类选择器颜色。

## 文本对齐

在演示型 HTML 时代，文本是使用 `align` 属性和相应的对齐值进行对的。CSS 使用了相同的原理，但当然，它是在 HTML 外部通过 `text-align` 属性完成的。这些值是相同的，对于任何用过文字处理软件的人来说都是熟悉的：

- left—左对齐——也称为右侧不齐（ragged right），左对齐将文本左侧对齐，行在右侧断开。这是所有浏览器的默认行为，也是所有正文文本的首选。`text-align: left;`
- center—居中——这使文本居中。居中文本对于设置标题、说明和其他强调文本非常有用。阅读长段居中文本非常困难，因此不建议将其用于正文。`text-align: center;`
- right—右对齐——这让所有文本右对齐，留下左侧不齐的边缘。`text-align: right;`
- justify—两端对齐——对齐意味着左右边缘都对齐。这是通过计算可用行长度内的单词和间距来实现的。这在印刷报和杂志中很常见。但大多数人会避免它，因为间距看起来可能非常奇怪，因此更难以阅读。`text-align: justify;`

图 9-8 对比了应用各种对齐选项的段落。

| 后者是一个 | 后者是一个 | 后者是一个 | 后者是一个 |
| --- | --- | --- | --- |
| 异常大且 | 异常大且 | 异常大且 | 异常大且 |
| 美丽的动物， | 美丽的动物， | 美丽的动物， | 美丽的动物， |
| 全黑的，且 | 全黑的，且 | 全黑的，且 | 全黑的，且 |
| 聪明程度 | 聪明程度 | 聪明程度 | 聪明程度 |
| 令人惊讶。 | 令人惊讶。 | 令人惊讶。 | 令人惊讶。 |

图 9-8 居中、右对齐和两端对齐的文本。

## 文本装饰

你可以用 CSS “装饰”文本——即应用或移除特定的装饰值。这是通过 `text-decoration` 属性完成的，值如下：

- none—主要用于移除链接的默认下划线。第 10 章，“链接效果、列表和导航。”
- underline—下划线——在选定文本下方添加一条线。可用性专家倾向于避免带下划线的文本，因为它可能与链接文本混淆。
- overline—上划线——在选定文本上方添加一条线。
- blink—闪烁——是的，你没没错。这会导致文本闪烁，这是 Netscape 在早期引入（并使用到了令人痛苦程度）的功能。它在所有现代浏览器中都有效，但 Internet Explorer 除外。

示例 9-5 为装饰文本提供了内联 CSS 示例。

**示例 9-5** 用 CSS 装饰文本

```
<p style="text-decoration: underline;">这段文本有下划线</p>

<p style="text-decoration: overline;">这段文本有上划线</p>

<p style="text-decoration: line-through;">这段文本有删除线</p>

<p style="text-decoration: blink;">这段文本会闪烁</p>
```

图 9-9 显示了结果，除了闪烁之外。

![](img/516568206e0e220ce5a120446a34b48d_166_0.png)

**图 9-9** 用 CSS 装饰文本——尝试示例 CSS 以查看闪烁效果。

## 文本缩进

另一个非常有用的文本属性是 `text-indent`。它允许你使用 CSS 缩进文本，而不是在 HTML 中使用间隔图形或大量的不换行空格字符。

你可以使用任何固定长度值（在本章前面描述）。

```
p {text-indent: 45px;}
```

这会导致每个段落都有 45 像素的初始缩进（见图 9-10）。

![](img/516568206e0e220ce5a120446a34b48d_167_0.png)

**图 9-10** 使用 45 像素缩进段落。

你也可以使用百分比值，它将相对于元素的容器框（更多内容见第 12 章“定位、浮动和 Z-Index”）。

```
p {text-indent: 40%;}
```

这会导致深层缩进，你可以偶尔用它来实现特殊的视觉效果（见图 9-11）。

![](img/516568206e0e220ce5a120446a34b48d_168_0.png)

你可以使用负长度值来悬悬缩进（见图 9-12）。

![](img/516568206e0e220ce5a120446a34b48d_168_1.png)

图 9-12 通过设置边距并应用 `text-indent: -20px;` 实现文本悬缩进。

## 文本转换和变化

你可以通过两个不同的属性来设置文本的大小并改变字体。

要改变文本，使用 `text-transform` 属性，其值为 `capitalize`、`uppercase`、`lowercase` 或 `none`。

要改变文本，使用 `font-variant` 属性，其值为 `small-caps` 或 `normal`（默认值）。示例 9-6 显示了转换。

**示例 9-6** 用 CSS 转换文本

```html
<!DOCTYPE html> PUBLIC "-//W3C//DTD HTML 1.0 Transitional//EN""http://www.w3.org/TR/html4/strict.dtd">

<html xmlns="http://www.w3.org/1999/xhtml">

<head>

  <title>转换文本</title>

  <style>

    body {

      font-family: Arial, sans-serif;

      font-size: 14px;

      color: black;

    }

    h1 {

      text-transform: uppercase;

      font-weight: 700;

      color: red;

    }

    h2 {

      font-variant: small-caps;

      font-size: 18px;

    }

    p {

      text-transform: lowercase;

      font-size: 16px;

    }

  </style>

</head>

<body>

  <h1>转换文本</h1>

  <p>后者是一个异常大且美丽的动物，全黑的，且聪明程度令人惊讶。</p>

  <p>观察到我对家庭宠物的偏爱，她没有放过获取最可爱品种的机会。我们有鸟、金鱼、一只大狗、兔子、一只小猴子和猫。</p>

</body>

</html>
```

## 字母间距与单词间距

CSS 吸收的排版另一个方面是字母间距和单词间距，分别由 `letter-spacing` 和 `word-spacing` 属性处理。每个长度的值如下（参见示例 9-8）：

**示例 9-8** 字母间距与单词间距

```
<p style="letter-spacing: 10px;">I married early, and was happy to find in my wife a disposition uncongenial with my own.</p>

<p style="word-spacing: 0.5em;">Observing my partiality for domestic pets, those of the most agreeable kind. We had birds, gold fish, fine dog, rabbits, a small monkey, and a cat.</p>
```

第一段每个字母之间会有 10 像素的间距，第二段每个单词之间有 0.5 em 的间距（见图 9-15）。

![](img/516568206e0e220ce5a120446a34b48d_172_0.png)

**图 9-15** 字母间距与单词间距。

结果非常奇特。尽管你会在保守的文档中通常不会使用这些样式，但你可以开始看到使用此类样式如何提供许多细的设计选项。

## 修改首字母和首行文本

你可以使用伪元素选择器对文本的第一个字母（大字字母）和文本的第一行进行样式化。你还没有见过这些，这里看一下：

- `:first-line`
- `:first-letter`

这些会被应用于你想要应用样式的元素上（参见示例 9-9）。

示例 9-9 使用伪元素选择器设置样式

```
p:first-line {font-weight: bold; color: #333;}

p:first-letter {font-style: italic; color: #999;}
```
