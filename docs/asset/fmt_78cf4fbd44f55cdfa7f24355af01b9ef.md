
除了这些工具，许多图形应用程序（如 GIMP）允许你使用“另存为”功能将图像为多种不同的格式（BMP、JPEG、PNG、TIFF 等）。

# 创建 Doc 文档

文档项目通常需要生成多种格式的输出。例如，描述如何使用某个软件程序的示例可能需要输出为打印手册、HTML 页面和 PostScript 文件。Linux 社区最近采用创建所谓“结构化文档”的标准是 SGML、XML 和 DocBook。

# 理解 SGML 和 XML

标准通用型标记语言 (`SGML`) 的创建是为了提供一种标准的文本标记方法，以便其以各种格式输出。由于 `SGML` 标记是通过文本标签完成的，你可以使用任何纯文本编辑器创建 `SGML` 文档。文档由你的正文和标识文本中每种信息的标签组成。

与 `Groff` 和 `HTML` 等标记语言不同，`SGML` 的目的不是在创建文档时强制执行特定的外观。例如，你不会将某段文本设置为加粗或斜体，而是将其标识为地址、段落或名称。稍后，会将样式表应用到文档上，获取已标记的文本并分配列表和呈现形式。

由于 `SGML` 包含许多标签，为了简化基于 `SGML` 的文档，其他项目相继出现，以更好地关注 `SGML` 的使用方式。特别是可扩展标记语言 (`XML`) 的创建，是为了提供 `SGML` 一个易于管理的子集，专门为良好配合 Web 的发布而定制。

到目前为止，在 `SGML` 和 `XML` 中，我仅提到用于生成结构化文档的框架。特定的文档项目需要为要生成的文档类型创建并在某种程度上强制执行特定的标记定义。这些定义被称为数据类型定义 (`DTD`)。对于 Linux 本身和其他源项目的文档，`DocBook` 是首选的 `DTD`。

# 理解 DocBook

`DocBook` 是一种 `DTD`，非常适合生成各种格式的计算机软件文。。它最初由 OASIS 财团 (`www.oasis.org/docbook`) 创建，现在由许多不同的商业和开源工具支持。

> 交叉引用：你可以在 `www.docbook.org` 找到 `DocBook` 的官方文档。

`DocBook` 的重点在于标记内容，而不是指示特定的外观（即字体类型、大小、位置等）。它包含了用于自动化创建图像、插图列表和目录过程的标记。

`DocBook` 对 Linux 社区非常重要，因为许多开源项目使用它来生成 HTML、PDF、PostScript 等。例如，以下是使用 `DocBook` 创建文档的组织列表：

- Linux 文档项目 (`tldp.org/LDP/Author-Guide`)
- GNOME 文档 (`developer.gnome.org/projects/gdp/handler/gdp-handbook`)
- KDE 文档项目 (`kde.org/documentation`)
- FreeBSD 文档项目 (`freebsd.org/docproj`)

如果你想为任何上述项目做出贡献，请参考这些组织的网站。在所有情况下，它们都会发布编写指南或样式指南，说明支持编写工作的 `DocBook`。

# 创建 DocBook 文档

你可以使用任何文本编辑器创建文档，使用的标签外观与 `HTML` 标签相似（在小于大于符号之间有起始结束标签）。某些文字处理程序允许你创建 `DocBook`。例如，你可以从 `OpenOffice Writer` 导出为 `DocBook` 格式。

以下步骤包含一个使用纯文本编辑器创建并输出为 HTML 的 `DocBook` 示例。（你需要安装 DVD 上的 `docbook` 包才能执行以下步骤。）

1. 在你的主目录下创建一个工作目录并进入该目录。例如，你可以在终端窗口中输入以下内容：

```
$ mkdir $HOME/doftest
$ cd $HOME/doftest
```

2. 打开一个文本编辑器来存放你的 `DocBook` 文档。例如，你可以输入：

```
$ gedit cardoc.sgml
```

（可以在 `www.edit.org` 获取文本编辑器 `edit`，也可以处理 `DocBook` 使用的长标签名。）

3. 输入你希望出现在文档中的标签。大多数 `DocBook` 文档是 `<book>` 类型（大型多部分文档）或 `<article>` 类型（单章节文档）。要尝试一个 `DocBook` 文档，输入以下内容：

```xml
<xml version="1.0">
<article>
  <title>选择新车*</title>
  <author>
  <abstract>
    在本文中你将学习如何对汽车进行定价、还价和购买。
  </abstract>
```

## 入门

你将学习的第一点是如何确定你的预算范围。

## 下一步

在了解你能够负担的范围后，你就可以开始搜索了。

你应该注意关于此文档的几点。整个文档被包裹在 `<article></article>` 标签中。文章位于 `<title></title>` 标签中。`<section></section>` 标签表示具有标题和对应段落的文本章节。这些章节之后可以与目录（TOC）分开处理。

- 4. 保存文件并退出文本编辑器。
- 5. 接下来，你可以尝试将刚刚创建的文档转换为几种不同的格式。例如，要创建 HTML 输出，你可以使用：

```bash
$ db2html carddoc.sg
```

结果是一个名为 `carddoc` 的新目录。在 `cardoc` 目录下执行 `db2html` 的结果是：`stylesheet-images/t2.html` 文件和 `x12.html` 文件。

要查看创建的 HTML 文件，我输入了以下命令：

```bash
$ firefox $HOME/doctest/cardoc/t2.html
```

6-11 显示了由 `db2html` 命令生成的输出示例。左侧屏幕显示第一页。点击页面顶部的“Next”（下一页）链接。你在右侧看到的第二页。在转换为 HTML 的过程中，`db2html` 命令为每页添加了“Next/Previous”（上/上一页）按钮。它还将每个章节的标题放在第一页的目录以及浏览器的标题栏中。

从现在起，你可以继续添加内容和不同类型的标签。如果你正在为特定项目（如之前提到的 Linux 项目）编写文档，你应该获取所需的特定标签和其他样式问题的信息。

## 第 6 章：使用 Fedora 和 RHEL 27 进行发布

![](img/e48e37bc567c450fab455ad1b714d8c3_310_0.png)

图 6-11：使用 `db2html` 命令将 `DocBook` 文件输出为 HTML。

## 转换 DocBook 文档

上一个示例展示了如何创建一个简单的 `DocBook` 文档并将其转换为 HTML 输出。以下 Fedora 和 RHEL 工具可以将 `DocBook` 转换为其他格式：

- `docbook2dvi` - 将 `DocBook` 文件转换为设备无关格式（Device Independent）。
- `docbook2html` - 将 `DocBook` 文件转换为 HTML 格式。
- `docbook2man` - 将 `DocBook` 文件转换为 man 页面格式。
- `docbook2pdf` - 将 `DocBook` 文件转换为 PDF 文格式（PDF）。
- `docbook2rtf` - 将 `DocBook` 文件转换为富文本格式（RTF）。
- `docbook2tex` - 将 `DocBook` 文件转换为 TeX 格式。
- `docbook2texti` - 将 `DocBook` 文件转换为 GNU Texinfo 格式。
- `docbook2txt` - 将 `DocBook` 文件转换为纯文本格式。

## 使用 Fedora 和 RHEL 打印文档

Red Hat Linux 中的打印由通用 打印系统（`CUPS`）服务提供。`LPRng` 服务不再包含在 Fedora 或 RHEL 中，但仍然可以从 `www.lprng.com/downloads.html` 获取。不过，这两项服务都允许你使用本节描述的相同基本打印命令进行打印。

## 交叉引用：有关为 Fedora 和 RHEL 配置本地和远程打印机的信息，请参阅第 17 章。

作为非管理员用户，你对打印机的配置方式没有太大控制权。不过，你可以检查哪些打印机可以打印，检查打印队列的状态（等待打印的文档），并删除任何已队列的打印作业。

## 打印到默认打印机

当你的系统管理员（或你）为电脑配置打印机时，其中一个打印机被定义为默认打印机。如果你不确定哪一个是你的默认打印机，输入 `system-config-printer` 并查找带有勾选标记的打印机。

大多数图形化文字处理程序（如 `StarOffice` 和 `OpenOffice.org`）都允许你从中选择打印机。然而，一些从命令行运行的较复杂的 Linux 工具只使用默认打印机。例如，`dvips`（打印 PostScript 文件）和 `grep -l`（打印 traff/nroff 文件）会自动将输出发送到默认打印机。

作为普通用户，你可以使用 `PRINTER` 环境变量覆盖默认打印机。例如，如果你电脑上的默认打印机是 `lp0`，而你想经常打印到 `lp1`，可以通过如下设置 `PRINTER` 变量来更改默认打印机：
