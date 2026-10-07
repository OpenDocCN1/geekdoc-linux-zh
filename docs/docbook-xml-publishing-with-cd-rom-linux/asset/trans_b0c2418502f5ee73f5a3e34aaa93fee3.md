
# 理解 DocBook 标记

![](img/81f56bf497dbf7f7582072400d12cb42_38_0.png)

# User Friendly Media 样式指南

Joe Brockmeier

Copyright © 2000 by User Friendly Media

目录
10 User Friendly Media 样式指南简介

图 1.4 在 Netscape 中查看的转换为 HTML 的 DocBook 文档

> 是的，没错。DocBook 可以用来创建计算机能够创建的几乎任何类型的输出。只要你有正确的应用程序，几乎一切都是可能的。DocBook 的设计不仅仅是为了处理打印输出。这甚至是即使是普通的文字处理程序或排版程序也能够完成的壮举！

用于 DocBook 的免费样式表是公开且免费提供的。值得注意的是，Norman Walsh 提供了可供 Jade 和 OpenJade 引擎使用的样式表。。Jade 和 OpenJade 程序可以读取 DocBook 文档，对其进行解析，获取数据并与样式表进行比较，然后产生某种类型的输出（见图 1.5）。

第 6 章详细描述了样式表以及 Jade 和 OpenJade 引擎的使用。第 10 章涵盖了自定义现有样式表以及创建你自己的样式表。与自定义 DocBook DTD 本身不同，自定义样式表是被明确鼓励的，而且在你掌握之后做起来非常简单。

![](img/81f56bf497dbf7f7582072400d12cb42_38_1.png)

# 第 1 章：入门

![](img/81f56bf497dbf7f7582072400d12cb42_39_0.png)

图 1.5 从 DocBook 文件到出版

## 总结

本章用非常通俗的语言解释了 DocBook 的基础。在书的其余部分，我将利用这些构建模块并展示如何创建 DocBook 文档以及从它们生成输出。虽然本章中的某些概念看起来很复杂，但如果你与 DocBook 工作一小会儿，它们就会变得更容易理解。

你可能还会发现，不需要记忆这里的大部分信息。通常，你只需要 DocBook 的一小部分元素和功能就可以创建实用的文档。DocBook 拥有海量的元素来涵盖各种需求，但每个人可能只使用其中的极小一部分。

背景介绍足够。让我们开始使用 DocBook 吧！

# 第 2 章：编写技术文章

- 文章元素
- 标准标签
- 准备出版

在第 1 章“入门”中，我涵盖了 DocBook 的一些基础知识。现在，我将带你逐步完成使用 DocBook 创建一篇技术文章的过程。虽然 DocBook 主要用于文档编写，但没有理由不使用它来编写任何类型的文章、短故事、大学论文或文本。本章是指导你创建自己的文章类文档的指南。通过 DocBook，你可以创建一个主文档，该文档可以转换为多种适用于打印、在线或电子共享的格式。一个 DocBook 文件可以转换为纯文本、PDF、HTML、PostScript、DVI 或 RTF。

就本章而言，请不要过分关注用于创建 DocBook 文档所使用的编辑器类型。相反，我将重点介绍使用 DocBook 编写短文章的基础知识。因为由于无法演示你在文档中使用的每一个标签，我尝试侧重于附录 B《DocBook 元素参考》中列出的最全面的 DocBook 元素列表。

![](img/81f56bf497dbf7f7582072400d12cb42_41_0.png)

现在是时候创建 DocBook 文章了。我假设你正在创建一个没有附录、索引或其他附加文件的独立文档。对于更复杂的文档，请看第 4 章。通过启动你喜欢的编辑器或文字处理程序创建一个新文件。SGML 和 XML DocBook 标准之间的差异将在章节出现时注明。

记住，虽然你可以在文字处理程序中创建 DocBook 文件，但必须确保将文件保存为纯文本。如果你以 Microsoft Word 格式保存 DocBook 文件，将得到一个无法正确解析的文件。如果你习惯使用 Microsoft Word 写文档完全可以，但文件格式必须是纯文本。vi、Emacs 或 Windows 记事本等编辑器默认将文件保存为纯文本。

![](img/81f56bf497dbf7f7582072400d12cb42_41_1.png)

# 文章与其他类型的 DocBook 文档区别不大，但某些元素是文章特有的。现在可能是指出这一点的好时机：如果你用 SGML 编写文章但计划在未来某个时候将其转换为 XML，你应该保持所有元素为小写以保持兼容性。

## 声明文章

如果你将使用 XML，将文件命名为 Article.sgm 或 Article.xml 并从声明文档类型开始：

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

通过将文档声明为文章，解析器知道它正在处理什么类型的文档。声明还说明了使用的是哪个版本的 DocBook DTD（见图 2.1 和 2.2）。这一点很重要，因为如果解析器不知道内容，DocBook 各版本之间的变化可能会导致问题。<article> 元素标记文章的开始和结束。

虽然 DocBook 元素看起来与 HTML 标签相似，但记住 DocBook 解析器比普通的 Web 浏览器要求严格得多。你可以不声明 HTML 文档甚至跳过某些标签而无事，但 DocBook 并不那么宽容。小心包含所有必需元素并按正确的顺序使用它们。
