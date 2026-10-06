

# 第 13 章 + 文件操作 355

user@bible:-> strings filename

输出可能会提供一些实用的线索。应用程序 ghex2 或 khexedit 也很有用。这些是图形化编辑器——也就是说，它们允许你从字节层级查看并编辑二进制文件（你将看到它们以十六进制表示表示）。像 khexedit 这样的编辑器会在单独的窗格中显示这些字节的字符串表示，而文件的其余部分则显示文本字符。

使用十六进制编辑器修改二进制文件很容易让它们变得完全毫无用，无论是可执行文件还是数据文件。

`strings` 命令有时是快速查看 Microsoft Office 文件内部内容的快捷方法。`antiword` 也很有；它尝试从 Microsoft Word 文档中提取所有文本。`antiword` 支持几乎所有版本的 Microsoft Word .doc 格式，并且速度非常快。你可以结合 `grep` 使用它来检查特定文件是否包含特定单词。例如：

```
user@bible:-> antiword wordfile.doc | grep -i linux
```

检查该单词是否出现在 wordfile.doc 中。（-i 选项告诉 grep 忽略大小写。）

> `strings` 和 `antiword` 命令在第 10 章中都有详细讨论。

## 查看和打开不同的文件类型和格式

尝试列出读者在 Linux 上可能遇到的所有文件格式是不可能的且无用的。然而，在接下来的几秒钟，我们将指出一些最重要的文件类型和格式，并对如何查看或打开它们进行注释。

## PostScript

PostScript 是一种页面描述语言。它实际上不仅于此——事实上它是一种特殊的编程语言，但由 Adobe 用于描述图形元素和文本如何在页面上布局。PostScript 打印机将接受 PostScript 文件并直接打印。如果你有不同类型的打印机，打印系统会在传递给打印机之前对 PostScript 进行适当过滤，但 PostScript 被认为是 Linux 中打印的通用语言。产生打印输出的应用程序以 PostScript 的形式产生该输出。

# 356 第三部分 ◆ 在 SUSE Linux 中使用命令行

PostScript 文件是具有特定格式的纯文本文件。它总是如下开头：

```
%!PS-Adobe-3.0
%%Title: filename
```

虽然原始的 PostScript 一看之下很老旧，但学习如何编写简单的 PostScript 文件来创建带有几何形状和文本的页面并不困难，例如：

PostScript 文件通常称为 file.ps。封装的 PostScript 文件可能有扩展名 .eps。要查看它，你可以使用 gv、ggv 或 ghostview 中的任何一个程序。它们在后台都使用 ghostscript (gs) 将文件渲染为图形形式。

你可以直接从命令行打印 PostScript：

```
usersample:~/tmp lpr.file
```

由于其作为一种格式的重要性，有许多实用程序可以以各种方式处理 PostScript 文件：

- *ps2ascii* 尝试从 PostScript 文件中提取文本。
- *ps2pdf* 将 PostScript 文件转换为 PDF。
- `pscriptils` 软件包包含了各种用于分割和合并 PostScript 文件以及调整页面大小的实用程序。

任何允许你打印文件的应用程序都会产生 PostScript。某些应用程序还提供打印到 PDF 的选项。

> 注意：封装的 PostScript 文件 (.eps) 是一种特殊的 PostScript 文件，它包含了关于其物理尺寸（边界框）的信息，并被设计为包含在另一个文档内部。

## PDF

PDF 与 PostScript 相关，也是 Adobe 的一个完整文档的格式。打开 PDF 的应用程序必须是 Acrobat Reader、accroad，但也有 xpdf 和 gpdf。ghostview 应用程序也乐意打开 PDF 文件。然而，accroad 最能充分利用 PDF 的所有高级功能（超链接、文本搜索、字体等）。

再次，大量的实用程序可处理 PDF 文件，特别是 `pdfotext` 和 `pdf2ps`，它们尝试执行其名称所暗示的操作。

# 第 13 章 + 文件操作 357

![](img/e4e45c9f32e76fb35fabbd21a96f1a1e_401_0.png)

OpenOffice.org 现在具有即时的“导出为 PDF”功能以及相应的工具栏按钮。

## DVI

DVI 文件是一种设备无关的文件，通常具有文件扩展名 .dri。DVI 格式几乎只作为 TeX 和 LaTeX 排版程序的输出出现。这通常不被视为生成 PostScript 的中间阶段；程序 `dvips` 能够将 DVI 文件转换为 PostScript。然而，你可以使用 xdv 或 kdvi 直接查看 DVI 文件。（在生成必要的字体时，你可能需要等待异常长的时间。）

## TeX 和 LaTeX 文件

在一些源代码文档中，你有时会遇到 .tex 文件，它们通常是 LaTeX 文件。TeX 是由 Donald Knuth 开发的基于标记的排版系统，而 LaTeX 是 Tex 的一组广泛使用的宏。如果你需要从一个不存在的 LaTeX 文件创建可打印输出，`latex` 命令处理 `file.tex` 会创建一个 dvi 文件（见前一节）。这可以通过 `dvips` 文件将 `file.dvi` 转换为 PostScript。

LaTeX 是制作非常精美的打印输出的极佳方法，特别是对于数学排版，但它有一条学习曲线。

## HTML

HTML 是一种无需介绍的文件格式。对于在 Linux 上编辑 HTML，首选工具（在我们看来）是带有其一种一种 HTML 模式的 emacs。另一个具有良好 HTML 编辑能力的编辑器是 free（一个折叠文本的编辑器），它让你能够轻松地“折叠”标签的内容，以便你可以看到代码的大规模结构。

此外还有 quanta HTML 编辑器和 Mozilla composer，以及 OpenOffice.org 中的 HTML 导出。

`tidy` 工具根据其 DOctype 声明检查 HTML 的有效性。

如果你需要从网页或本地 HTML 文件中提取文本，可以考虑的一种方法是使用带有 -dump 选项的 lynx 浏览器：

```
usable:-> lynx -dump http://lwn.net/ ~ ln
```

## 图形格式

SUSE 中的图形查看器和编辑器可以处理大量的图形格式。几乎你遇到的任何图形文件都可以由 GIMP 处理，如果你需要编辑，它是你的首选

# 358 第三部分 在 SUSE Linux 中使用命令行

GIMP 一个偶尔实用的功能是它可以将 PostScript 文件转换为图形格式，更通地说，它可以在各种格式之间转换

## 音频和多媒体格式

在音频方面，可以使用许多应用程序播放 .mp3、.ogg 和 .wav 文件，特别是 xm，并且 MIDI 文件由多个应用程序处理。

电影文件的情况并不简单。

应用程序 caffeine、noat 和 xine 都可以播放电影。caffeine 应用程序是 xine 的 KDE 前端。问题是大多数电影格式需要受专利保护的解码器。你可能获取这些解码器并将其添加到 xine。

RealPlayer 应用程序包含在 SUSE Professional 中。它播放 .rm 和 ram 文件，这些是网络网站上声音和视频片段的常见格式。

还有为 SUSE 构建的第三方软件包，非常强大的 mplayer 多媒体应用程序可以播放 .avi、.wmv、.mov (QuickTime)、MPEG 以及其他格式。每个都能处理大多数格式。通过为各种解码器添加插件，mplayer 软件包可以使用 Windows 动态链接库 (DLLs) 用于额外的解码器。在实践中，将 mplayer 软件包与各种解码器结合使用，是在 SUSE Linux 上获得最广泛视频格式支持的最佳方法。

mplayer 项目的主页位于 www.mplayer.hu/。SUSE 提供了两个致力于 SUSE Linux 上多媒体信息的邮件列表（一个德语，一个英语）。要订阅这些（以及其他）SUSE 邮件列表，请参阅  www.suse.com/us/support/online_help/mailinglists/

## CSV 文件

CSV（逗号分隔）是一种常见的数据交换格式，特别是作为 Windows 上运行的各种商业应用程序的导出格式。

CSV 文件由列表组成。每行通过分隔符（通常是逗号）划分为字段，每个字段通常被引号包围。

> "名","姓","街道地址","城市" "Peter","Rabbit","1, The Burrows","Peterborough"

