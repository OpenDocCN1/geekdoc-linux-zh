
由于 SGML 包含许多标记，为了简化 SGML，其他项目裁剪了 SGML 的使用方法。特别是可扩展标记语言 (XML) 的创建是为了提供一个专门为出版定制的、易管理的 SGML 子集。因此在 SGML 和 XML 中，我只提到了使用的框架。

## 理解 DocBook

DocBook 是一种非常适合生成多种格式软件文档的 DTD。它最初由 OASIS 会 (www.oasis-open.org/docbook) 创建，现在由许多不同的商业和开源工具支持。

> 交叉引用：您可以在 www.docbook.org 找到 DocBook 的官方文档。

DocBook 的重点是标记内容，而不是指示特定的外观（即字体大小、位置等）。它包含了自动创建索引、插图列表和目录的标记。Fedora 和 RHEL 中的工具允许将 DocBook 文档输出为 HTML、PDF、DVI、PostScript 和其他格式。

# 第 6 章：使用 Fedora 和 RHEL 进行发布 273

- [KDE 文档项目](www.kde.org/documentation)
- [FreeBSD 文档项目](www.freebsd.org/docproj)

如果您想为上述任何文档项目做出贡献，请参考每个机构的网站。在所有情况下，您发布的是作者指南或样式，用于描述他们为写作工作所支持的 DocBook 格式。

## 创建 DocBook 文档

您可以使用任何文本编辑器创建文档，并使用外观与 HTML 标签相似的标签（带有起始符号、小于号和大于符号）。某些文字处理程序允许您创建 DocBook 标记。例如，您可以将文档从 OpenOffice Writer 导出为 DocBook 格式。

以下步骤包含一个示例，使用 Fedora 和 RHEL 自带工具将纯文本输出为 HTML，并生成简单 DocBook 文档。（在执行以下步骤之前，您需要安装 DVD 上的 docbooks 软件包。）

- 1. 在您的家目录中创建一个工作目录并进入该目录。例如，您可以从终端窗口执行以下操作：

```
$ mkdir $HOME/doct
$ cd $HOME/doct
```

- 2. 打开文本编辑器来编写您的 DocBook 文档。例如，您可以输入：

```
$ gedit cardoc.sgml
```

（像 jedit 这样的文本编辑器可以在 www.jedit.org 获取，对于处理 DocBook 中使用的长名称也很有用。）

- 3. 输入标签和您希望在文档中显示的内容。大多数 DocBook 文档要么是 `<book>` 类型（大型、多部分文档），要么 `<article>` 类型（单章节文档）。要尝试 DocBook 文档，请输入以下内容：

```xml
<xml version="1.0">
<article>
<title>选择一辆新车</title>
<artheader>
<abstract>
在本文中你将学习如何对汽车进行定价、
谈判和购买。
</abstract>
</artheader>
<section>
<title>开始使用</title>
<para>
你将学到的第一件事是如何确定
你的买得起的范围。
</para></section>
<section><title>下一步</title><para>
在知道自己能买起什么之后，你就可以开始
搜索了。
</para></section>
</article>
```

您应该注意到此文档的几点。整个文档被包裹在文章标签 `<article></article>` 中。文章标题位于标签 `<title></title>` 标签中。章节标签 `<section> </section>` 表示带有标题和每个段落的文本章节。这些章节以后可以在目录目录（TOC）中被单独处理。

- 1. 保存文件并退出文本编辑器。

- 2. 接下来，您可以尝试将创建的文档转换为几种不同的格式。例如，要创建 HTML 输出，可以输入：

`$ db2html cardoc.sgml`

- 3. 为了查看创建的 HTML 文件，我输入了：

`$ firefox $HOME/doctest/cardoc/t2.html`

结果产生了一个名为 `cardoc` 的新目录。`cardoc` 目录下 `db2html` 的生成结果是：`stylesheets-images` 目录、`t2.html` 文件和 `x12.html` 文件。

图 61 显示了由 `db2html` 命令创建的输出示例。左侧显示每一页。点击页面顶部的 Next（下一个）链接。您看到的第二个页面在右侧。在转换为 HTML 期间，`db2html` 命令为每个页面添加了 Next/Previous（下一个/上一个）按钮。还将每个章节的标题放在第一页的目录以及浏览器标题栏中。

从现在起，您可以继续添加内容和不同类型的标签。如果您正在为特定项目编写文档（例如前面提到的 Linux 项目），您应该获取有关特定标签以及它们要求的其他样式信息。

# 第 6 章：使用 Fedora 和 RHEL 进行发布 275

![](img/6a8f767dda2519b458f97c2e7f586576_316_0.png)

## 选择一辆新车

摘要

在本文中，你将学习如何对汽车进行定价、谈判和购买。

- 目录
- 开始使用
- 下一步

## 开始使用

6-11：使用 `db2html` 命令将 DocBook 文件输出为 HTML。

## DocBook 文档

示例显示了如何创建一个简单的 DocBook 文档并将其转换为 HTML 输出。以下 Fedora 和 RHEL 工具可以将 DocBook 转换为其他格式：

- `docbook2dvi` — 将 DocBook 文件转换为设备无关格式。
- `docbook2html` — 将 DocBook 文件转换为 HTML 格式。
- `docbook2man` — 将 DocBook 文件转换为 man 页面格式。
- `docbook2pdf` — 将 DocBook 文件转换为便携文档格式 (PDF)。
- `docbook2rtf` — 将 DocBook 文件转换为富文本格式 (RTF)。
- `docbook2tex` — 将 DocBook 文件转换为 Tex 格式。
- `docbook2texi` — 将 DocBook 文件转换为 GNU Texinfo 格式。
- `docbook2txt` — 将 DocBook 文件转换为纯文本格式。

## 使用 Fedora 和 RHEL 打印文档

Red Hat Linux 中的打印由通用 UNIX 打印系统 (CUPS) 提供。LPRng 服务不再包含在 Fedora 或 RHEL 中，但仍然可以从 www.lprng.com/downloads.html 获取。不过，这两项服务都允许您使用本节描述的相同打印打印命令进行打印。

# 交叉引用：有关为 Fedora 和 RHEL 配置本地和远程打印机的信息，请参见第 17 章。

作为非管理员用户，您对打印机的配置没有太多的控制权。不过，您可以检查哪些打印机可用于打印，检查打印队列的状态（等待打印的文档），并删除您的任何已队列的打印作业。

## 打印到默认打印机

当您的系统管理员（或您）为计算机配置打印机时，其中一个打印机被定义为默认值。如果您不确定哪个打印机是默认的，请使用 `system-config-printer` 并寻找带有复选标记的打印机。

大多数文字处理器（如 StarOffice 和 OpenOffice.org）都允许您从可用选项中选择打印机。一些从命令行运行的复杂工具只使用默认打印机。例如，`dvips`（打印 PostScript 文件）和 `groff -l`（打印 troff/roff 文件）会自动将输出发送到默认打印机。

当您的系统管理员（或您）为计算机配置打印机时，其中一个打印机被定义为默认值。如果您不确定哪个打印机是默认的，请使用 `system-config-printer` 并寻找带有复选标记的打印机。

大多数文字处理器（如 StarOffice 和 OpenOffice.org）都允许您从可用选项中选择打印机。一些从命令行运行的复杂工具只使用默认打印机。例如，`dvips`（打印 PostScript 文件）和 `groff -l`（打印 troff/roff 文件）会自动将输出发送到默认打印机。

当您的系统管理员（或您）为计算机配置打印机时，其中一个打印机被定义为默认值。如果您不确定哪个打印机是默认的，请使用 `system-config-printer` 并寻找带有复选标记的打印机。

大多数文字处理器（如 StarOffice 和 OpenOffice.org）都允许您从可用选项中选择打印机。一些从命令行运行的复杂工具只使用默认打印机。例如，`dvips`（打印 PostScript 文件）和 `groff -l`（打印 troff/roff 文件）会自动将输出发送到默认打印机。

当您的系统管理员（或您）为计算机配置打印机时，其中一个打印机被定义为默认值。如果您不确定哪个打印机是默认的，请使用 `system-config-printer` 并寻找带有复选标记的打印机。
