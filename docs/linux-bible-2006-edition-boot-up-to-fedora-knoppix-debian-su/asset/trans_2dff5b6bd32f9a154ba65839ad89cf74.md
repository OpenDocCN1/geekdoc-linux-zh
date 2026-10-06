

# 第 21 章 ✦ 文字与图像的运用 571

## 构建结构化文档

文档项目通常需要生成多种格式输出的文档。例如，描述如何使用某个软件程序的相同文本可能需要输出为打印手册、HTML 页面和 PostScript 文件。Linux 社区最近采纳的创建所谓“结构化文档”的标准是 SGML 和 XML。用于生成 Linux 文档的特定类型定义（DTD）被称为 DocBook。

## 理解 SGML 和 XML

标准泛化标记语言（SGML）的创建是为了为文本提供一种标准的标记方法，以便日后以多种格式输出。由于 SGML 标记是通过文本标签完成的，因此你可以使用纯文本编辑器创建 SGML 文档。文档由你的文档正文和识别文本中每种类型信息的标签组成。

与 Groff 和 TeX 等标记语言不同，SGML 标记的目的不是在创建文档时强制执行特定的视觉效果。例如，你不会将某段文本标记为加粗或*斜体*，而是将其识别为地址、段落或名称。随后，会将样式表应用于文档，以便为被标记的文本分配外观和呈现效果。HTML 是 SGML 标记的一个示例。

由于 SGML 包含许多标签，其他项目必须简化基于 SGML 的文档生成过程，并关注 SGML 的使用方法。特别是可扩展标记语言（XML）的创建是为了提供一个易于管理的 SGML 子集，专门用于适用于基于 Web 的出版。

因此，在对 SGML 和 XML 的描述中，我讨论了用于生成结构化文档的框架。特定的文档项目需要为它们需要生成的文档类型创建并在某种程度上强制执行特定的标记定义。这些定义被称为数据类型定义（DTD）。对于 Linux 以及开源项目的文档，DocBook 是首选的 DTD。

## 理解 DocBook

DocBook 是一种 DTD，非常适合以多种格式处理计算软件的文档。它最初由 OASIS 联盟（www.oasis.org）创建，现在由许多不同的商业和开源工具支持。

DocBook 的重点在于标记内容，而不是指示特定的视觉效果（即字体类型、大小、位置等）。它包含了某些标记，可以自动化创建索引、插图列表和目录等过程。

DocBook 对 Linux 社区非常重要，因为许多开源项目使用它来生成文档。例如，以下是使用 DocBook 创建描述其软件文档的组织列表：

- [Linux Documentation Project](https://www.tldp.org/LDP/LDP-Author-Guide)
- [GNOME Documentation Project](https://developer.gnome.org/projects/gdp/handbook/gdp-handbook)
- [KDE Documentation Project](https://www.kde.org/documentation)
- [FreeBSD Documentation Project](https://www.freebsd.org/docproj)

如果你想为这些文档项目之一做出贡献，请参考每个组织的网站。在所有情况下，请发布描述它们支持的 DocBook 标签的编写或样式指南。

## 创建 DocBook 文档

你可以在任何文本编辑器中创建文档，使用外观与 HTML 标签相似的标签（带有小于和大于符号的结束标签）。某些文字处理程序也允许你创建 DocBook 标记。

以下步骤展示了使用纯文本编辑器生成简单的 DocBook XML 文档，并输出到 Linux 系统中可用 HTML 工具的示例。

> 注意：DocBook DTD 同时提供 SGML 和 XML 两种形式。对于两者，XML 形式正在被积极维护。

- 1. 在你的主目录下创建一个目录并进入该目录。例如，你可以在终端窗口执行以下命令：

```bash
$ mkdir $HOME/doctypeest
$ cd $HOME/doctypeest
```

- 2. 创建一个文本编辑器来存放你的 DocBook 文档。例如，你可以输入：

```bash
$ edit cardoc.xml
```

（一个如 `edit` 的文本编辑器，你可以在 www.jedit.org 获取，对于处理 DocBook 中使用的长标签名也很有用。）

- 3. 输入你想在文档中显示的标签和文本。大多数 DocBook 文档是 `<book>` 类型或 `<article>` 类型。

- 4. 保存文件并退出。
- 5. 接下来，你可以将文档转换为其他格式。例如，要创建 HTML，请以下：

```xml
<?xml version="1.0"?>
<article>
<title>入门指南</title>
<abstract>
在这篇文章中，你将学习如何使用 DocBook 创建文档。
</abstract>
<section>
<title>下一步</title>
<p>你学的第一件事是如何输出文档。</p>
</section>
</article>
```

