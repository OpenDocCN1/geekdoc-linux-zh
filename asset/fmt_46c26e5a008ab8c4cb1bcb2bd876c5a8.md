
就本章而言，请不要过分关注用于创建 DocBook 文档所使用的编辑器类型。相反，我将重点介绍使用 DocBook 编写短文章的基础知识。因为由于无法演示你在文档中使用的每一个标签，我尝试侧重于附录 B《DocBook 元素参考》中列出的最全面的 DocBook 元素列表。

![](img/81f56bf497dbf7f7582072400d12cb42_41_0.png)

现在是时候创建 DocBook 文章了。我假设你正在创建一个没有附录、索引或其他附加文件的独立文档。对于更复杂的文档，请看第 4 章。通过启动你喜欢的编辑器或文字处理程序创建一个新文件。SGML 和 XML DocBook 标准之间的差异将在章节出现时注明。

记住，虽然你可以在文字处理程序中创建 DocBook 文件，但必须确保将文件保存为纯文本。如果你以 Microsoft Word 格式保存 DocBook 文件，将得到一个无法正确解析的文件。如果你习惯使用 Microsoft Word 写文档完全可以，但文件格式必须是纯文本。`vi`、`Emacs` 或 Windows 记事本等编辑器默认将文件保存为纯文本。

![](img/81f56bf497dbf7f7582072400d12cb42_41_1.png)

## 文章与其他类型的 DocBook 文档区别

文章与其他类型的 DocBook 文档区别不大，但某些元素是文章特有的。现在可能是指出这一点的好时机：如果你用 SGML 编写文章但计划在未来某个时候将其转换为 XML，你应该保持所有元素为小写以保持兼容性。

### 声明文章

如果你将使用 XML，将文件命名为 `Article.sgm` 或 `Article.xml` 并从声明文档类型开始：

```xml
<DOCTYPE article "-//OASIS//DTD DocBook V4.0//EN">
<article>
</article>
```

要声明 XML DocBook 文档，使用：

```xml
<?xml version="1.0"?>
<!DOCTYPE article "-//OASIS//DTD DocBook XML V4.0//EN">
"http://www.oasis.org/docbook/xml/4.0/docbook.dtd">
<article>
</article>
```

通过将文档声明为文章，解析器知道它正在处理什么类型的文档。声明还说明了使用的是哪个版本的 DocBook DTD（见图 2.1 和 2.2）。这一点很重要，因为如果解析器不知道内容，DocBook 各版本之间的变化可能会导致问题。`<article>` 元素标记文章的开始和结束。

虽然 DocBook 元素看起来与 HTML 标签相似，但记住 DocBook 解析器比普通的 Web 浏览器要求严格得多。你可以不声明 HTML 文档甚至跳过某些标签而无事，但 DocBook 并不那么宽容。小心包含所有必需元素并按正确的顺序使用它们。

请注意，你的文档目前只有一个章节。如果你添加一个 `Sect-2` 元素，它看起来像这样：

```
<sect1>
  <title>第一章节标题</title>
  <para>更多有趣且兴奋的文本...</para>
  <sect2>
    <title>第二个章节标题</title>
    <para>更多的文本！</para>
  </sect2>
</sect1>
```

`Sect-2`（或更低）元素必须嵌套在 `Sect1` 元素内部。元素之间是父子关系——一个元素依赖于另一个元素的存在。如果元素排列不当，文档将无法正确解析。

下一个元素是 `Para` 元素。`Para` 很好记，因为它代表 paragraph（段落）。你可能会发现，大多数 DocBook 元素都是合乎逻辑的，而且在编写了一份或两份 DocBook 文档后，你可能就不需要查阅最常用的元素了。

> 如果你想节省一些精力和精力，请务必检查随书附赠的光盘中的模板。它包含了最常见类型 DocBook 文档的模板，让你在上手 DocBook 时有一个快速开始。

![](img/81f56bf497dbf7f7582072400d12cb42_46_0.png)

最后，`Article` 元素结束了文章文档。这是一个虽然简陋但符合规范的 DocBook 文章。现在，我将集中介绍你为了编写典型文档可能可能需要的其他元素。

# 标准标签

DocBook 元素多到数不完，但不用担心——我将专注于你近期可能需要的那些元素。记住，在 DocBook 中编写文档与在 WYSIWYG（所见即所得）文字处理器中编写文档是不同的。文档的物理格式由你用于解析 DocBook 文件的工具处理。你不需要担心使用不同大小的字体、粗体或斜体文本，或者

# 第 2 章：撰写技术文章

等等——这一切都由你选择的工具从你的 DocBook 文档生成输出时，“自动”地处理好了。

![](img/81f56bf497dbf7f7582072400d12cb42_47_0.png)

## 典型标记

接下来的章节将向你介绍一些典型的 DocBook 标记。

### Abstract 元素

`Abstract` 元素包含关于文章本身的信息，通常是关于文章内容的一或两个短段。

这个示例展示了 `Abstract` 元素的基本用法。`Title` 元素被复制了。

```
<abstract>
<title>基础摘要</title>
<para>文章摘要</para>
</abstract>
```

你可以在 Eric S. Raymond 写的《The Missing File》一书中找到其他有趣的表达：http://www.tuxedo.org/jargon

### Abbreviation 元素

为了表示文档中的缩写词，请使用 `Abbreviation` 元素。恰恰如此，“abbreviation”（缩写词）本身就是一个很长的词。想过为什么吗？这个示例展示了 `Abbreviation` 元素的标准用法。

```
<para>
你可以在圣克拉拉找到我们的新办公室，<abbreviation>Calif.</abbreviation>
</para>
```

### Acronym 元素

`Acronym` 元素用于表示文档文本使用的首字母词，例如 KDE、GNOME 和 FBI。根据样式表的不同，`acronym` 元素的内容显示可能与普通文本不同。代码显示了 `Acronym` 元素的标准用法。

```
<para>
当 <acronym>IRS</acronym> 或 <acronym>FBI</acronym> 出现在家门口时，没有人会喜欢这种事儿的。
</para>
```

### Acknowledgement 元素

`Acknowledgement` 元素表示文章正内的致谢。`Acknowledgement` 元素的内容可能与正文内容隔离开。注意，`Acknowledgement` 元素不能嵌套在 `Para` 元素中，只能如示例所示嵌套在 `Article` 元素中。

```
<article>
<acknowledgment>
<para>在开始文章之前，我想感谢所有帮助使其成为可能的人。非常感谢 Prima 和 Linux Magazine 的所有人。</para>
</acknowledgment>
</article>
```

### Attribution 元素

正如众所周知，将荣誉归于应得的人是非常重要的。`Attribution` 元素用于指示作为 `Blockquote`（块引用）元素或 `Epigraph`（题记）元素设置的引用的来源。在撰写学术论文时，该元素特别有用，因为可以设计样式表来自动以正确的引用格式格式化属性。这是一个 `Attribution` 的简单示例。

```
<blockquote>
<attribution>John Lennon</attribution>
生命就是当你正忙于制定其他计划时所发生的事情。
</blockquote>
```

> `Attribution` 元素的特殊之处在于，它不能包含在 `Para` 元素中。它只用在 `Blockquote` 或 `Epigraph` 元素内部，而这些元素不需要包含在 `Para` 元素中。

![](img/81f56bf497dbf7f7582072400d12cb42_48_0.png)

### Author 元素

正如本章前面介绍过的，`Author` 元素包含关于文章作者的信息。

### AuthorBlurb 元素

通常，当文章发表时，会有关于作者的简短介绍或其他信息。`AuthorBlurb` 元素包含此类信息，可以位于文档的任何地方。这里的示例显示它被嵌套在 `Article` 元素中，因为这看起来最合理。

```
<article>
<authorblurb>
<para>你可以在圣克拉拉找到我们的新办公室，<abbreviation>Calif.</abbreviation>
</para>
</authorblurb>
</article>
```

*(注：此处原文示例内容似乎存在逻辑混乱或重复，此处已按原文结构翻译)*
