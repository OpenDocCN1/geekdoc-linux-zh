

```xml
<xml version="1.0">
<article>
  <title>选择新汽车</title>
  <artheader>
    <abstract>
      在这篇文章中，你将学习如何对汽车进行定价、
      谈判和购买。
    </abstract>
  </artheader>
  <section>
    <title>开始入门</title>
    <para>
      你将学习的第一点是如何确定
      你的负担能力。
    </para>
  </section>
  <section>
    <title>下一步</title>
    <para>
      在了解自己的负担能力之后，你就可以开始
      搜索。
    </para>
  </section>
</article>
```

你注意到了此文档的几点。整个文档被包裹在 article 标签 (`<article> </article>`) 中。标题位于 title 标签 (`<title></title>`) 中。section 标签 (`<section> </section>`) 表示带有标题和段落的章节。这些章节稍后可以在目录 (TOC) 中被单独处理。

- 4. 保存文件并退出文本编辑器。
- 5. 下一步，你可以尝试将创建的文档转换为不同的格式。例如，要创建 HTML 输出，你可以执行以下命令：

$ db2html cardoc.sgml

结果是一个名为 cardoc 的新目录。cardoc 目录下 db2html 的生成结果为：stylesheets-image、t2.html 和 x12.html。

- 6. 要查看你刚刚创建的 HTML 文件，我执行了以下操作：

$ firefox $HOME/doctype/cardoc/t2.html

6-6 显示了由 db2html 命令创建的输出。左侧屏幕显示第一页。点击页面顶部的“Next”（下一页）链接。你看到的第二页在右侧。在转换为 HTML 的过程中，db2html 命令会在每个页面添加 Next/Previous（上上一页）按钮。它还将每个章节的标题放在第一页的目录以及浏览器的标题栏中。

从现在起，你可以继续添加内容和不同类型的标签。如果你正在为特定项目（如之前提到的 Linux 项目）编写文档，你应该获取有关该特定标签以及其他要求的样式问题的信息。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_313_0.png)

图 6-6：使用 db2html 命令将 DocBook 文件输出为 HTML。

#  DocBook 文档

之前的示例显示了如何创建一个 DocBook 文档并将其转换为 HTML 输出。以下工具和 RHEL 工具可以将 DocBook 转换为其他格式：

- docbook2dvi - 将 DocBook 文件转换为设备无关格式。
- docbook2html - 将 DocBook 文件转换为 HTML 格式。
- docbook2man - 将 DocBook 文件转换为 man 页面。
- docbook2pdf - 将 DocBook 文件转换为便携文档格式 (PDF)。
- docbook2rtf - 将 DocBook 文件转换为富文本格式 (RTF)。
- docbook2tex - 将 DocBook 文件转换为 TeX 格式。
- docbook2xi - 将 DocBook 文件转换为 GNU TeXInfo 格式。
- docbook2txt - 将 DocBook 文件转换为纯文本格式。

# 使用 Adobe Acrobat Reader 显示 PDF 文件

如果每当你想更改文档内容或格式时都将 Groff 或 LaTeX 文档发送到打印机，那么非所见即所得的出版可能会非常费纸。为了节省纸张和时间，你可以使用一些打印预览程序在屏幕上显示文档及其在打印页面上显示的样子。以下章节描述了用于显示便携文档格式 (PDF) 文件的 Adobe Reader。

便携文档格式 (PDF) 提供了一种以打印形式存储文档的方法。通过 Adobe Acrobat Reader，你可以以非常友好的方式查看 PDF 文件。Adobe Acrobat 让你轻松地在 PDF 文件中移动。PDF 文件可能包含超链接、目录、图表和各种字体。

Adobe Acrobat Reader 的最新版本（版本 8）已从 Adobe.com 以 RPM 格式提供。此版本可以使用其他 PDF 阅读器不具备许多 PDF 功能，包括版本 1.4 中的一些新压缩功能。（当你正在为特定项目（如之前提到的 Linux 项目）编写文档时，你应该获取有关该特定标签以及其他要求的样式问题的信息。）

# 第6 章：使用 Fedora 和 RHEL 进行出版 267

