
开始标签和结束标签。图 53.1 展示了一个示例 HTML 页面。不必担心现在就完全理解它，因为本章将逐步构建这段代码。目前，你只需知道在结构中的每个元素周围都有开始标签和结束标签即可。（本章中使用的所有截图均来自于一台 Windows 95 或 Windows 3.11 机器，通过以太网访问我们编写 HTML 代码所在的 Linux 服务器。使用的浏览器是 NCSA 的 Mosaic。）

![](img/e8e6b47ac20475e23d48b4c476f5d891_904_0.png)

在开始时，关于标签有几个重要的知识点：它们不区分大小写（因此你不必担心大小写匹配问题），并且它们几乎总是成对出现的开始标签和结束标签。网页上最常见的错误是标签不匹配或未终止的标签。在许多情况下，网页看起来可能没有问题，但可能会出现严重的格式问题。快速扫描你的 HTML 代码有助于解决这类问题。

> **提示**
>
> 并非所有 HTML 标签都有开始标签和结束标签。少数是单端的，意味着它们通常只有开始标签。还有一些被称为容器，因为它们包含额外的信息。这些并不总是在两端都标记。

标签写在尖括号中。这些括号向浏览器发出信号，表示其中包含一条 HTML 指令。一个示例 HTML 代码元素如下所示：

```html
<start_tag_name> text text text <end_tag_name>
```

其中 `<start_tag_name>` 和 `<end_tag_name>` 分别是中间文本的开始标签和结束标签。标签的类型描述了文本将如何显示。例如，如果它们是标题标签，文本将显示得比普通正文大，并且可能会以加粗或突出显示的方式呈现。

如何编写 HTML 代码？有几种方法。最简单的是使用任何 ASCII 编辑器。确保不要将 HTML 文档保存为专有格式（如 Word 文档），因为 Web 浏览器无法理解除 ASCII 之外的任何格式。市面上有一些专门的 HTML 编辑器，具备标签下拉列表和预览屏幕功能。在处理非常大的网页时，这些编辑器可能很有用，但对于大多数人来说，一个简单的编辑器就足以开始了。

## 开始 HTML 文档

HTML 文档通常以一条标识该文档为 HTML 的指令开始。这是一个名为 `<HTML>` 的标签，浏览器用它来指示 HTML 指令的开始。以下是来自网页的一段示例代码：

```html
<HTML>
<HEAD>
<TITLE> This is my Web Page! Welcome! </TITLE>
</HEAD>
<BODY>
<H1> This is the first heading on my page. </H1>
This is a bunch of text that is written on my home page. I hope you like it.
</BODY>
</HTML>
```

可以看到，第一个和最后一个标签 `<HTML>` 和 `</HTML>` 标记了 HTML 代码的开始和结束。第二个标签中的斜杠表示结构元素的结束。这些标签应放在你编写的每个 HTML 文档的开头和结尾。`<HEAD>` 和 `</HEAD>` 标签标记文件的序言部分，通常用于显示在 Web 搜索工具下方的标题和关键词。在 `<HEAD>` 标签内只允许使用少数几个标签。`<TITLE>` 和 `</TITLE>` 提供文档的标题。`<BODY>` 和 `</BODY>` 标签标记文档主体的开始和结束。`<H1>` 和 `</H1>` 标签用于页面上的标题。

任何浏览器都可以读取此代码，如图 53.2 所示。可以看到，标题材料本身不会显示在页面上，只有正文标签之间的材料会显示。标题用于在浏览器顶部显示你当前登录的页面。这起到了标识符的作用。

上面显示的代码格式是逐行排列的，但这只是为了提高可读性。如果你想的话，可以将所有内容写在一长行中，因为 HTML 会忽略空白字符，除非另有说明。然而，为了调试和重新阅读的目的，保持代码整洁有序是有益的。

### 图 53.2

在 Internet Explorer 下显示的示例 HTML 代码。

![](img/e8e6b47ac20475e23d48b4c476f5d891_906_0.png)

以下是关于我们所使用的标签的一些更多评论。`<TITLE>` 标签总是位于头部标签（`<HEAD>` 和 `</HEAD>`）内部，用于描述页面的内容。你的页面应该只有一个标题。头部标签内不能有其他标签。为你的文档选择一个简短且描述性强的标题是有用的，这样看到它的人就会知道他们正在访问什么。

`<BODY>` 和 `</BODY>` 标签用于封闭网页的主要内容，通常只有一对这样的标签。所有文本和内容（链接、图形、表格等）都封闭在正文标签之间。

有几种层级的标题标签，每一种都是比上一级低一级的子标题。我们在上面代码中使用的标题是 `<H1>`，这是最高级别的标题。如果你想，可以用许多标题层级来组织你的文档。例如，你可以编写这段代码：

```html
<HTML>
<HEAD>
<TITLE> This is my Web Page! Welcome! </TITLE>
</HEAD>
<BODY>
<H1> This is an H1. </H1>
This is a bunch of text.
<H2> This is an H2 </H2>
This is more text.
<H3> This is an H3 </H3>
This is text about the H3 heading.
<H3> This is another H3 </H3>
Here's more text about the H3 heading.
<H2> This is yet another H2 </H2>
Text to do with H2 goes here.
</BODY>
</HTML>
```

此代码在浏览器中的显示如图 53.3 所示。可以看到，标题的层级略有不同，较高的标题（较小的数字）更具特色且更粗。这允许你将页面划分为逻辑类别，每个类别都有一个标题或副标题。你可以像写书一样使用这些标题：H1 可以包含 H2，H3 位于 H2 之下，等等。混合使用标题没有规则（例如，你可以只使用 H3），但常识通常决定了如何组织你的页面。

![](img/e8e6b47ac20475e23d48b4c476f5d891_907_0.png)

## 段落

那么段落呢？处理段落有几种方法，规则随每个 HTML 版本而改变。不过，最简单的方法是使用 `<P>` 和 `</P>` 标签来标记每个单独的段落。例如，这段代码使用了三对段落标签：

```html
<HTML>
<HEAD>
<TITLE> This is my Web Page! Welcome! </TITLE>
</HEAD>
<BODY>
<H1> This is an H1. </H1>
<P> This is the first paragraph. It is a really interesting paragraph and should be read several times because of its content. </P>
<P> Another paragraph. It's not quite as exciting as the first, but then it's hard to write really exciting paragraphs this late at night. </P>
<P> The closing paragraph has to be strong to make you feel good. On well, we can't always meet your expectations, can we? </P>
</BODY>
</HTML>
```

此代码在浏览器中的外观如图 53.4 所示。注意每个段落都是独立的，并且与下一个段落之间有一些空白。如果你省略了 `<P>` 和 `</P>` 标签会怎样？由于浏览器忽略包括换行符在内的空白字符，文本会像图 53.5 中所示那样连在一起。因此，你应该使用 `<p>` 和 `</p>` 标签来分隔页面上的段落。请记住，在 HTML 代码中段落之间放入大量空行并不重要。浏览器会忽略它们并将所有内容连在一起。

![](img/e8e6b47ac20475e23d48b4c476f5d891_908_0.png)

![](img/e8e6b47ac20475e23d48b4c476f5d891_908_1.png)

![](img/e8e6b47ac20475e23d48b4c476f5d891_908_2.png)

![](img/e8e6b47ac20475e23d48b4c476f5d891_908_3.png)

> **注意**
>
> 严格来说，你不需要 `</p>` 标签来指示段落的结束，因为另一个 `<p>` 会指示新段落的开始。`<p>` 标签是开放式标签的一个例子，这种标签不需要闭合。然而，闭合配对标签是良好的编程实践。

HTML 代码中的注释怎么办？你可能想给自己嵌入一些注释，关于谁编写了代码、它的功能、你何时完成的等。在 HTML 代码中编写注释的方式如下：

```html
<!-- This is a comment -->
```

