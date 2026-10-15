
列表 8.39 展示了一个包含到为止所描述部分的 DocBook 源文件示例大纲。注意此列表的顶部有一个描述文档内容的注释，其后是文档标头（在本例中，它指定为书籍书籍文档）。紧接着，请注意列表末尾有一个 `<book>` 标签和一个相应的 `</book>` 标签。在 `<book>` 和 `</book>` 标签内部是书籍文档的组件，在本例中是章节，你接下来将学习这些内容。虽然该示例处理的是书籍文档，但如果你改为创建一个文章文档，则使用一组 `<article>` 和 `</article>` 标签来包裹文档内容。

## 章节和节组件

列表 8.39 在此示例书籍文档中有五个章节。每个章节被指定为一个独立的组件，封装在一组 `<chapter></chapter>` 标签对中。在每个章节组件内部，该章节的名称被指定为一组 `<title></title>` 标签对之间的任何其他组件。注意，对于文章类型文档，你将从“节”（使用 `<section>` 和 `</section>` 标签）开始拆分，而不是章节标签。

如果你希望将一个章节（在书籍类型文档中）拆分为更小的“节”，你可以在该章节组件中引入节组件。这涉及到在章节组件内指定 `<section>` 和 `</section>` 标签来包裹每个节。即使你的网络文档中没有使用“节”，如果你想将“引言”（Introduction）拆分为两个节，第一个命名为“术语”（Terminology），第二个命名为“问题陈述”（Problem Statement），你可以使用列表 8.40 所示的结构。列表 8.40 对节组件进行了缩进，有助于在视觉上将其与章节组件区分开，但缩进不是强制的。注意每个节都有自己的标题组件，包含该节的名称。

### 列表 8.40 分为若干节的章节

```
<chapter>

<title>Introduction</title>

<section>

<title>Terminology</title>

</section>

```
284 UNIX/Linux 简介
```
<section>

<title>Problem Statement</title>

</section>

</chapter>
```

如果你希望将一个节组件（无论是书籍类型还是文章类型文档）进一步拆分为更小的“子节”，你可以将节组件嵌套在另一个节组件内部。这种方法涉及在节组件内再次指定另一组 `<section>` 和 `<section>` 标签来包裹每个子节。

## 段落和文本

在每个章节或子节中，你拥有以一个或多个 `para`（对应 `<para>`）组件形式存在的文本。每个段落都封装在一组 `<para>` 和 `</para>` 标签对中。列表 8.41 展示了在“引言”章节中指定一个 `para` 组件的情况。如果你在章节的另一组 `<para>` 和 `</para>` 标签对中拥有第二个组件，你需要将其指定为另一个 `para`。

### 列表 8.41 指定文本段落

```
<chapter>

<title>Introduction</title>

<para>

This document contains an initial report of XYZ's<emphasis role="strikethrough">XYZ's</emphasis>

network performance and its impact on users. This work was initiated to investigate the following.

</para>

</chapter>
```

## 简单文本格式

DocBook 提供了一些基本的格式命令，允许你更改文本的外观。由于 DocBook 的目标是减轻开发者指定格式的负担，简单文本格式的种类可能看起来有限。简而言之，对于 HTML、PDF 或 PS 文档，你通常可以使用斜体、粗体、下标或上标文本来强调。要强调或斜体化文本，可以将文本封装在 `<emphasis>` 和 `</emphasis>` 标签中。

### 文本格式——创建和查看排版文档 285

列表 8.42 指定文本的强调或斜体格式

```
<emphasis>XYZ's</emphasis>
```

如果你想将名称格式化为粗体，可以使用 `<emphasis role="bold">`。列表 8.43 显示了如何

LISTING 8.43 指定文本的强调或斜体格式

```
<emphasis>XYZ's</emphasis>
```

如果你另一种方式想将名称格式化为粗体，可以使用 `<emphasis role="bold">`。列表 8.43 显示了如何

要强调或斜体化文本，可以将文本封装在 `<emphasis>` 和 `</emphasis>` 标签中。

## 标题和作者

现在你对标签有了一些了解，可以学习如何创建更多的文档组件。从每个文档需要的 `bookinfo` 组件开始，即标题和作者。

列表 8.44 展示了一个带有单个作者的 `bookinfo` 组件。标题“网络利用报告”（Network Utilization Report）指定在 `<title>` 和 `</title>` 标签中，就像你处理章节和节一样。

### 列表 8.44 标题和作者的指定

```
<bookinfo>

<title>Network Utilization Report</title>

<author>

<firstname>John</firstname>

<surname>Doe</surname>

</author>

</bookinfo>
```

作者封装在 `<author>` 和 `</author>` 标签中。此外，名称被指定为两个组件：名字和姓。名字封装在 `<firstname>` 和 `</firstname>` 标签中，姓

286 UNIX/Linux 简介

在 `<surname>` 和 `</surname>` 标签中。作者组件为了可读性进行了缩进，像之前一样，这种缩进不是必要的。为了可读性，名字和姓组件被指定在同一行。

如果你希望指定多个作者，需要在 `<authorgroup>` 和 `</authorgroup>` 标签中使用 `authorgroup` 组件。在 `authorgroup` 内部，你可以指定许多所需的 `author` 组件，每个封装在 `<author>` 和 `</author>` 标签中。列表 8.45 显示了一个带有两个作者的 `bookinfo` 组件示例。

### 列表 8.45 标题和多个作者的指定

```
<bookinfo>

  <title>Network Utilization Report</title>

  <authorgroup>

    <author>

      <firstname>John</firstname>

      <surname>Doe</surname>

    </author>

    <author>

      <firstname>Jane</firstname>

      <surname>Smith</surname>

    </author>

  </authorgroup>

</bookinfo>
```

## 项目

在 DocBook 中，你可以创建各种列表来列出或描述项目。下面展示了如何创建三种形式的列表：简单项目列表、描述性列表和编号列表。

### 项目列表

要创建项目列表（即带有项目符号的列表），可以使用一组 `<itemize>` 和 `</itemize>` 标签来封装该列表。列表中的每个项目都是自己的一组 `<item>` 和 `</item>` 标签。

### 列表 8.46 DocBook 中的项目列表

```
<para>

  This document contains an initial report of 

  <emphasis role="bold">XYZ's</emphasis>

  network performance and its impact on users. This work was initiated
```
