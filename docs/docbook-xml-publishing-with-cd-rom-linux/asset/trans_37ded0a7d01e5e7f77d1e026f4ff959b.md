

# 书籍结构元素

我将大量讨论那些与其关注 DocBook 文档内容不如说关注其结构的元素。我已经触及了其中几个；Sect 元素和 Book 元素在本质上是结构性的。然而，我稍后将涵盖的 Sect 元素专门关注文档的结构。

# 使用导航元素

除了本章已经提到的原因外，为什么要考虑结构呢？嗯，DocBook 文档的格式源于样式表，样式表根据元素的结构或内容对文档的每个元素进行格式化。例如，包含在 Sect1 元素中的 Title（标题）元素的格式化方式可能与包含在 Sect2 或 Sect5 元素中的 Title 元素的格式化方式不同。

当文档被渲染以用于发布时，这些元素就变成了导航元素。在印刷版书籍中，标题作为章节标题出现在目录中；在 HTML 中，这些元素在字面意义上变成了导航元素。你可以点击它们并跳转到你描述的章节。注意结构非常重要，这样读者在此时就可以轻松导航你的文档，并找到他们寻找的信息。

# 使用章节

我已经提到过很多次，DocBook 非常关注文档的结构。没有哪个地方比专门用于文档章节层级的元素数量更能体现这一点了。DocBook 有七个，是的，七个与文档章节相关的元素。其中五个元素已经被简要提到过，即 Sect1 到 Sect5 元素。DocBook 还有一个没有特定层级的 SimpleSect 元素和 Section 元素。

以下是所有章节元素的列表，包括信息性元素：

- Sect1
- Sect1Info
- Sect2
- Sect2Info

# 第 4 章：使用 DocBook 准备书籍

- Sect3
- Sect3Info
- Sect4
- Sect4Info
- Sect5
- Sect5Info
- SimpleSect
- Section
- BridgeHead

Sect5 元素中使用的 SectInfo 包含关于其所在章节的元数据。例如，如果你想为包含在 sect1 元素中的 DocBook 文档部分内容包含元数据，请使用 sect1 元素。SectInfo 元素不能在其他其他章节中使用，并且它取代了旧版 DocBook 文档中的 DocInfo 元素。还需要提的是，SectInfo 元素仅包含其所包含的 sect1 的元数据，而不是文档中所有的 sect1 元素。

SimpleSect 元素是一个不包含子章节的章节元素，尽管它可能是另一个 sect 元素的子章节。例如，以下示例是有效的：

```
<sect1>
<title>Example Section</title>
<para>
这是一个包含 SimpleSect 元素的 Sect1 元素的示例。
</para>
<simplesect>
<title>SimpleSect Title</title>
<para>
SimpleSect 元素可以包含 Title（标题）元素和 Para（段落）元素，但不能包含另一个 Sect 元素。
</para>
</simplesect>
</sect1>
```

然而，如果在 SimpleSect 元素内部嵌套了另一个章节元素，它将是非有效的。关于 SimpleSect 元素的有效子元素的完整列表，请参考附录 B。

章节或其他文档可能包含多个 Sect2 元素，这些元素可能也包含多个 Sect3 元素，以此此类推。然而，DocBook 对维护 Sect 元素的层级有严格规定。你不能跳过 Sect 元素。例如，直接在 Sect1 元素中嵌套 Sect3 元素是非有效的。以下是 Sect 元素层级的有效示例，包括 SimpleSect 元素（见图 4.8）：

```
<chapter>
<section>
<para>
你可以在 Chapter 元素中包含 Section 元素，但不能包含任何 Sect1 到 Sect5 元素或 SimpleSect 元素。
</para>
<sect1>
<para>
这是一个 Sect1 元素。
</para>
<sect2>
<para>
这是一个 Sect2 元素。
</para>
<simplesect>
<para>
这是一个 SimpleSect 元素，它可以放在任何 Sect 元素之下，但不能放在 Section 元素之下。注意，你必须在下一个元素之前关闭 SimpleSect 元素。
</para>
</simplesect>
<sect3>
<para>
这是一个 Sect3 元素。
</para>
</sect3>
<sect3>
<para>
这是另一个 Sect3 元素，它也包含一个 Sect4 和 Sect5 元素。注意，我们在 Sect4 和 Sect5 元素关闭之后才关闭这个元素，但不要忘记关闭 Para 元素。
</para>
```

```
<sect4>
<para>
这是一个 Sect4 元素。
</para>
<sect5>
<para>
这是一个 Sect5 元素，图腾柱底部的元素。
</para>
</sect5>
</sect4>
</sect3>
</sect2>
</sect1>
</chapter>
```

在使用 Sect 元素时，你必须非常小心地正确嵌套。这意味着结束标签应该以反序出现，从 sect5（如果有的话）到 Sect1。

![](img/81f56bf497dbf7f7582072400)
**图 4.8** 大量的章节

在使用 Sect 元素时，你必须非常小心地正确嵌套。这意味着结束标签应该以反序出现，从 sect5（如果有）到 Sect1。

如果在 SimpleSect 元素内部嵌套了另一个章节元素，它将是非有效的。关于 SimpleSect 元素的有效子元素的完整列表，请参考附录 B。

如果在 SimpleSect 元素内部嵌套了另一个章节元素，它将是非有效的。关于 SimpleSect 元素的有效子元素的完整列表，请参考附录 B。

如果你有很多 Sect 元素，除非使用带有语法高亮的编辑器，否则很容易忘记正确嵌套。关于更多 Emacs 和 Vim，请参见第 8 章“使用 Emacs”和第 9 章“使用 Vim”。

# 参考页面

对于某些书籍，你可能想在附录或书籍本身包含参考页面。Reference 元素最初设计用于处理手册（manpages），但经过了一些演变。如果你正在创建一个参考或类似的内容，你会发现 Reference 元素及其子元素非常好。

Sect5 元素中使用的 SectInfo 包含其所在章节的元数据。例如，如果你想为包含在 sect1 元素中的 DocBook 文档部分内容包含元数据，请使用 sect1 元素。SectInfo 元素不能在其他章节中使用，并且它取代了旧版 DocBook 文档中的 DocInfo 元素。还需要提的是，SectInfo 元素仅包含其所包含的 sect1 的元数据，而不是文档中所有的 sect1 元素。

SimpleSect 元素是一个不包含子章节的章节元素，尽管它可能是另一个 sect 子章节。例如，以下示例是有效的：

```
<sect1>
<title>Example Section</title>
<para>
这是一个包含 SimpleSect 元素的 Sect1 元素的示例。
</para>
<simplesect>
<title>SimpleSect Title</title>
<para>
SimpleSect 元素可以包含 Title（标题）元素和 Para（段落）元素，但不能包含另一个 Sect 元素。
</para>
</simplesect>
</sect1>
```

然而，如果在 SimpleSect 元素内部嵌套了另一个章节元素，它将是非有效的。关于 SimpleSect 元素的有效子元素的完整列表，请参考附录 B。

章节或其他文档可能包含多个 Sect2 元素，这些元素可能也包含多个 Sect3 元素，以此此类推。然而，DocBook 对维护 Sect 元素的层级有严格规定。你不能跳过 Sect 元素。例如，直接在 Sect1 元素中嵌套 Sect3 元素是非有效的。以下是 Sect 元素层级的有效示例，包括 SimpleSect 元素（见图 4.8）：

```
<chapter>
<section>
<para>
你可以在 Chapter 元素中包含 Section 元素，但不能包含任何 Sect1 到 Sect5 元素或 SimpleSect 元素。
</para>
<sect1>
<para>
这是一个 Sect1 元素。
</para>
<sect2>
<para>
这是一个 Sect2 元素。
</para>
<simplesect>
<para>
这是一个 SimpleSect 元素，它可以放在任何 Sect 元素之下，但不能放在 Section 元素之下。注意，你必须在下一个元素之前关闭 SimpleSect 元素。
</para>
</simplesect>
<sect3>
<para>
这是一个 Sect3 元素。
</para>
</sect3>
<sect3>
<para>
这是另一个 Sect3 元素，它也包含一个 Sect4 和 Sect5 元素。注意，我们在 Sect4 和 Sect5 元素关闭之后才关闭这个元素，但不要忘记关闭 Para 元素。
</para>
```

```
<sect4>
<para>
这是一个 Sect4 元素。
</para>
<sect5>
<para>
这是一个 Sect5 元素，图腾柱底部的元素。
</para>
</sect5>
</sect4>
</sect3>
</sect2>
</sect1>
</chapter>
```

![](img/81f56bf497dbf7f7582072400)
**图 4.8** 大量的章节

在使用 Sect 元素时，你必须非常小心地正确嵌套。这意味着结束标签应该以反序出现，从 sect5（如果有）到 Sect1。

如果你有很多 Sect 元素，除非使用带有语法高亮的编辑器，否则很容易忘记正确嵌套。关于更多 Emacs 和 Vim，请参见第 8 章“使用 Emacs”和第 9 章“使用 Vim”。

# 参考页面

对于某些书籍，你可能想在附录或书籍本身包含参考页面。Reference 元素最初设计用于处理手册（manpages），但经过了一些演变。如果你正在创建一个参考或类似的内容，你会发现 Reference 元素及其子元素非常好。

```
<!DOCTYPE type PUBLIC "-//OASIS//DTD DocBook V4.1//EN">
<reference>
  <title>Short Reference</title>
  <refentry>
    <title>Book</title>
    <sect1>
  <para>
TheDocBook element contains the elements that make up a book.
  </para>
    </sect1>
  </refentry>
  <refentry>
    <title>Chapter</title>
    <sect1>
    <para>
TheDocBook element contains the elements that make up a chapter.
  </para>
    </sect1>
  </refentry>
</reference>
```

![](img/81f56bf497dbf7f7582072400)
**图 4.9** xterm 中显示的男性

![](img/81f56bf497dbf7f7582072400)
**图 4.10** 参考输出

# 创建索引

索引化文档是一项大工程。在出版行业，有人专门靠索引文档来谋生。这是一门真正的科学，或者正如某些人所说，这是一门艺术。

> 即使你现在手中的这本书也经过了专业的索引。尽管 DocBook 包含了许多帮助自动化书籍制作和出版过程的工具，但没有什么能比真实人类做出编辑决策的能力。

- Index

你可以将 Index 元素包含在 Chapter、Article 或其他几个元素中。然而，如果你正在为整本书创建索引，最好的方法可能是将其作为独立文档开发，并像本章第一个示例所示将其包含。

以下示例展示了一个包含两个条目的简单索引，以提供 Index 元素的标记感觉。在示例示例中，索引是作为独立文档开发的，即使你通常会将一个两个条目的索引包含在另一个文档中。

```
<!DOCTYPE type PUBLIC "-//OASIS//DTD DocBook V4.1//EN">
<index>
<indexinfo>
<editor>
<firstname>P.K.</firstname>
<surname>Une</surname>
</editor>
</index>
```

