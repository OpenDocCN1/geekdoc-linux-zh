
图 31.3 显示了在 Mosaic 中显示的示例。

**图 31.3 在 Mosaic 中显示的文本格式。**

![](img/bffdba22b656a1846f7f38a3801d7f2.png)

假设你想显示某些文本，并希望换行和间距与输入一致。你可以使用 `<PRE>` 和 `</PRE>` 标签来定义预格式化文本。任何被这些包裹的文本都以等宽字体显示，所有的换行和空格都按照输入保留。

在某种程度上，你可以定义文本显示的方式。HTML 提供了让浏览器加粗、下划线或斜体显示文本的标签。这些标签被称为物理样式。加粗文本的标签是 `<b>`，下划线的标签是 `<u>`，斜体的标签是 `<i>`。HTML 还提供了用于格式化的逻辑标签。`<EM>` 和 `</EM>` 标签用于标记强调文本，通常以*斜体*显示。`<strong>` 和 `</strong>` 标签用于表示更强的强调，通常以**加粗**显示。

图 31.4 显示了不同格式可能外观。

**图 31.4 在 Netscape 中显示的格式示例**

![](img/bffdba22b656a1846f7f38a3801d7f2.png)

表 31.1 提供了一些常用的文本格式化 HTML 标签列表。

# 表 31.1 选定的 HTML 格式化标签

| 标签 | 操作 |
|---|---|
| `<b>...</b>` | 使文本加粗。 |
| `<BLOCKQUOTE>...</BLOCKQUOTE>` | 使用缩进格式化文本。 |
| `<FONT>...</FONT>` | 通过属性控制文本的各个方面——例如文本颜色（COLOR=rgb_value）和大小（SIZE=number）。 |
| `<i>...</i>` | 使文本变为*斜体*。 |
| `<PRE>...</PRE>` | 保持文本格式原样显示。 |
| `<STRIKE>...</STRIKE>` | 将文本格式化为~~删除线~~。 |
| `<u>...</u>` | 下划 |
| `<EM>...</EM>` | 逻辑样式；强调文本（通常显示为*斜体*）。 |
| `<KBD>...</KBD>` | 逻辑样式；将文本显示为键盘样式（通常以等宽字体显示）。 |
| `<strong>...</strong>` | 逻辑样式；强调文本（通常以**加粗**显示）。 |

# 杂文本

不属于其他标签类的格式化标签是 `<ADDRESS>` 和 `</ADDRESS>` 标签。这些标签用于标记文档中的地址、签名等。通常，这种格式位于文档末尾，紧跟在水平规则之后。`<ADDRESS>` 文本的精确格式由各个浏览器决定。

# 使用列表组织信息

有时你需要提供以某种方式逻辑分组的信息。例如，你可能有一组要显示的图形图像，或者你可能想显示一个编号的前 10 名列表。HTML 提供了多种格式化和显示信息列表的方法。在 HTML 中使用列表提供信息的强大方式，因为用户的浏览器会以一致的方式格式列表中的所有文本。你只需要决定信息如何组合在一起。

**显示无序列表** 无序列表使用项目符号或其他格式字符显示。无序列表中的每个文本条目可以是几行长。

使用两组标签来创建无序列表`<ul>` 和 `</ul>` 标签定义列表的开始和结束，`<li>` 标签用于标记每个列表项。列表 31.4 显示了简单无序列表的 HTML 源码。图 31.5 显示了 Mosaic 如何显示此列表。

## 列表 31.4 无序列表

```
<HTML>

<HEAD>

<TITLE>无序列表</TITLE>

</HEAD>

<body>

<ul>

<li>项目 1</li>

<li>项目 2</li>

<li>项目 3</li>

</ul>

</body>

</HTML>
```

## 列表 31.4 续

```html
<UL>
<li>This is list item 1.</li>
<li>This is list item 2.</li>
<li>This is list item 3.</li>
</UL>
<BODY>
</HTML>
```

图 31.5 在 Mosaic 中查看的无序列表。

![](img/bffdba228b656a1846f7f38a3801d7f2_655_0.png)

### 展示有序列表

有序列表以数字顺序呈现列表信息。每当识别出一个新列表时，列表项的编号就会加1。有序列表由 `<OL>` 和 `</OL>` 标签定义，无序列表使用的相同的 `<LI>` 标签也用于有序列表，以标记每个列表项。

列表 31.5 显示了一个简单有序列表的 HTML 源代码。图 31.6 显示了该列表在 Mosaic 中的显示方式。

## 列表 31.5 有序列表

```html
<HTML>
<HEAD>
<TITLE>An Ordered List</TITLE>
</HEAD>
<BODY>
<OL>
<li>This is list item 1.</li>
<li>This is list item 2.</li>
<li>This is list item 3.</li>
</OL>
</BODY>
</HTML>
```

### 使用定义列表

想象一下书中的术语表：你通常会有每个单词或术语单独一行，然后是一个给出定义的段落。HTML 定义列表（或术语列表）提供了一种在网页上实现这种效果的方法。定义列表由一个术语（可以是一个或一系列词）以及随后的定义组成。定义通常是解释性文本。

## 理解 HTML 语法

## 图 31.6

在 Mosaic 中查看的有序列表。

![](img/bffdba228b656a1846f7f38a3801d7f2_656_0.png)

尽管定义列表对于术语表特别有用，但你也可以用它们呈现任何需要标题和解释的信息。常见的用法是将术语项变为指向另一个文档的超链接，并将定义作为对链接文档的描述。（创建超链接将在本章稍后讨论，因此请记住定义列表的这一应用。）

定义列表需要 `<DL>` 和 `</DL>` 标签来标记列表的开始和结束。定义列表没有使用简单的列表项标签，而是使用双标签：`<DT>` 用于标记术语项，`<DD>` 用于标记定义。列表 31.6 显示了一个简单定义列表的 HTML 源代码。图 31.7 显示了该列表在 Mosaic 中的显示方式。

## 列表 31.6 简单的定义列表

```html
<HTML>
<HEAD>
<TITLE>A Simple Glossary List</TITLE>
</HEAD>
<BODY>
<DL>
<DT>Item 1</DT>
<DD>This is the definition field for list item 1.</DD>
<DT>Item 2</DT>
<DD>This is the definition field for list item 2.</DD>
<DT>Item 3</DT>
<DD>This is the definition field for list item 3.</DD>
</DL>
</BODY>
</HTML>
```

## 图 31.7

在 Mosaic 中查看的简单定义列表。

![](img/bffdba228b656a1846f7f38a3801d7f2_656_1.png)

## 组合列表

如你所见，HTML 中的各种列表为你提供了向用户展示信息的几种多种方法。事实上，HTML 允许你组合列表类型，以便对信息的呈现方式提供更强的控制。你可以轻松地将一种列表类型嵌套另一种列表类型内部。

假设你想在主页上创建一个区域，告诉用户你最喜欢的电影和音乐。你可以在无序列表内嵌套两个术语列表，以创建一个详细的大纲。列表 31.7 显示了一个使用嵌套列表的 HTML 源代码示例。

## 列表 31.7 通过嵌套不同的列表类型创建自定义列表

```html
<HTML>
<HEAD>
<TITLE>A Custom List</TITLE>
</HEAD>
<BODY>
This list shows some of my favorite musicians and movies.
It uses two definition lists nested in an unordered list.
It also uses some formatting tags.<P>
I hope you enjoy it.<HR>
<LI>Here are some of my favorite movies<P>
<DL>
<DT>Hopschotch</DT>
<DD>This is a wonderful film about an en-CIA agent traveling the world writing his memoirs</DD>
<DT>Highlander</DT>
<DD>An action adventure between a battle between immortals.
"There can be only one!"</DD>
</DL>
<P>
```
