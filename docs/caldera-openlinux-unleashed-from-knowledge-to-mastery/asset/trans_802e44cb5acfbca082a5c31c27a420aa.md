
## 首先尝试一次性完美地输入那个。
请记住，你必须在 X 环境下的终端中执行此操作。如果在控制台终端中执行，它会提示找不到显示器。经过一段时间，当 xdv1 找到并加载支持文件后，实际上会显示该 dvi 图像。

选择此图像是因为它位于 Caldera 的安装 CD-ROM 上，而不是为了测试你手指的灵活性。

当你正确地完成所有步骤后，你会看到一个类似于图 28.9 的图像。

### 图 28.9
使用 xdv1 显示的图像。

![](img/df365d352a104b50fea29e59a052de4d_700_0.png)

从这个示例可以看出，xdv1 提供了许多选项。首先，你可以调整放大倍数，其次，你可以浏览 dvi 文件中的整页内容。此外，你还可以以 PostScript 格式查看图像。最后，你可以使用“文件”命令将单张图像保存到另一个文件中。

存在许多 dvi 格式实用程序。（其中大多数在后续章节中作为转换工具进行介绍，因为通常图像要么保持原样即可，此时 xdv1 将完全足够；要么你想将其转换为其他格式，这就属于转换操作。）

## gs (ghostscript)
GhostScript（简称 gs）是 Adobe Systems PostScript 和便携文档格式（PDF）语言在 Linux 上的实现。它可以读取 PostScript 文档和 PDF 格式文档，并几乎在任何显示或打印设备上显示它们。

GhostScript 拥有数百个选项，允许你选择显示用的纸张尺寸（从 2.6x3.7 cm 到 100x141 cm），文档或页面将正确调整大小，并具有与纸张尺寸匹配的正确纵横比。它允许你为每一页选择分辨率和特殊字体。

调用 gs 的常规方法是从桌面选择 K-gear, Graphics, PS Viewer，这将打开 ghostscript。

此时，如果你浏览到 /usr/share/ghostscript/5.10/examples/golfper.ps，应该会看到一个类似于图 28.10 的屏幕。

### 图 28.10
使用 ghostscript 显示图像。

![](img/df365d352a104b50fea29e59a052de4d_701_0.png)

在这个屏幕上，你有很多选项，但它们实际上只是以用户友好的方式实现了 gs 可用命令行选项中很小的一部分。

gv 是通用的 ghostscript 查看器，它提供了一套不同的选项和实用程序。它的一些选项让人联想到 Microsoft 的 PowerPoint 产品，而不仅仅是简单的查看器。

## XV
最后但同样重要，是 xv 查看器。你可以在 K-gear, Graphics, XV 中找到它。它可以对图形图像执行几乎任何操作，包括以下功能：

-   图像格式转换
-   屏幕捕获
-   抖动处理
-   色彩映射转换
-   色深转换（8/24 位）
-   模糊
-   边缘检测
-   浮雕效果
-   像素化
-   去噪点
-   裁剪

它可以加载和保存以下格式：

-   GIF
-   TIFF
-   JPEG
-   BMP
-   Sun Rasterfile
-   以及其他无法一一细述的格式

如果你需要在排版过程中进行任何图像转换或图像增强，这里一定有至少一个工具能满足你的具体需求。

## 用于排版的转换实用程序
数百个实用程序在 Caldera Linux 上运行。其中大多数随发行版 CD 提供，其余的则可以轻松通过网络获取。

我将简要介绍一些最实用的工具，这些通常是用于创建文档内容的工具。

### dvips
这些工具中第一个不得不提的是 **dvips**——它将 **dvi** 文档转换为 PostScript 文档的实用程序。它具有一些使其区别于其他 **TeX** PostScript 驱动程序的特性。

**dvips** 生成优秀的标准 PostScript，可以作为插图包含在其他文档中，或通过多种打印后台作业处理程序打印。生成的 PostScript 最小化了对打印机内存的使用，因此即使是非常复杂且包含许多字体的文档，也可以在内存很小的打印机上打印。

dvips 最有趣（也最重要）的功能之一是它能够创建虚拟字体。这种以自然且可移植的方式处理字体重映射的能力，为 TeX 排版器增加了一个全新的灵活性层次。

虽然它进行简单而快速的转换，并且这些转换可以输出到文件，但 dvips 更常用于将 dvi 文件打印到 PostScript 打印机。系统的一些选项，如“仅打印奇数页”、“多份折叠份数”或“打印裁剪标记”，使 dvips 在排版环境中不可或缺。它们会让你的文档看起来像是在专业的排版店完成的。

### dvilj
dvips 概念的一个变体是 dvilj 命令。它的工作方式与 dvips 命令完全相同，具有相同的选项集，但它创建的是适合 HP LaserJet 打印机而非 PostScript 打印机的输出。

### dvipdfm
dvipdfm 是一个有趣的实用程序，可以将 dvi 格式转换为 Adobe Acrobat 格式的一种变体。它在自动生成超链接方面存在一些限制，但至少在基本层面上，它可以为你节省大量时间。可以从网络上免费在以下地址下载：

```
ftp://ftp.tex.ac.uk/tex-archive/dviware/dvipdfm.tar.gz
```

### dvitomp
dvitomp 是一个实用程序，可以将 dvi 格式转换为低级别的 MetaPost 命令，并保存在 MPX 文件中。虽然它通常由 makeMPX 例程调用，但你可以使用它通过命令行进行简单的紧急转换。

### dmp
dmp 将独立于设备的 troff (ditroff) 转换为低级别的 MetaPost 命令，并将它们保存在 .MPX 文件中。

如果你需要实现这一点，dmp 是一个有用的实用程序。只需注意，在它编写时，作者做出了若干假设（当时所有假设都是合理的），但现在这些假设不再有效，因此生成的许多输出都需要你手动调整，才能获得真正专业的文档。

### mpost
mpost 是一个有用的实用程序，它接受用 MetaPost 语言指定的一系列图片，并以 PostScript 格式输出它们。

### wp2latex
wp2latex 是一个很棒的小程序，可在以下地址获取：

http://warchieve.wustl.edu/mirrors/msdos/tex

这是一个由 Eindhoven 大学的 R. C. Houteep 用 Turbo Pascal 编写的 PC 程序，它可以将 WordPerfect 5 文件转换为 LaTeX 格式。然而，这是一个不完美的程序。它仅支持到 WordPerfect 5.0，这意味着它不具备以下功能：索引、目录、页边距、图形和公式编辑器。

虽然它是受版权保护的程序，但它是免费的，并附带 Pascal 源代码。

rtf2TeX 是一个将 Microsoft 富文本格式转换为 TeX 格式的程序。可以通过匿名 ftp 在以下地址获取：

ftp://astro.princeton.edu/pub/rtf2Tex.tar.Z

作者和维护者是 Robert Lupton。

一个有竞争力的（当谈到 Linux 和自由软件时，如果我们能使用这个词的话）实现在以下地址提供：

ftp://ftp.vmars.tuwien.ac.at/pub/misc

由 Erwin Wechtl 编写。

## WEB—清晰化编程
WEB 语言允许你一次编写代码并多次使用。你可以创建一个源文件，该文件既可编译又提供文档。以下实用程序将允许你既编译代码，又提供格式良好的文档，以尽可能详细的细节描述程序或系统。更好的是，一切都保存在一个地方，同时维护排版的文档和源代码。

关于清晰化编程和 WEB 语言的大量信息可在以下地址获取：

http://www.loria.fr/services/tex/english/litte.html

然而，一些亮点在于以下章节中。

Tangle（随 Caldera Linux 一起提供）从 WEB 源文件创建 Pascal 源文件。输出源文件可能不太美观（72 个字符被压缩在一行中），但它能编译，而且无论如何，你真正的源文件是 WEB 源文件。

### Weave
Weave（也随 Caldera Linux 一起提供）从 WEB 源文件创建 TeX 文档。它会处理诸如页面布局、缩进和标识符斜体等细节。它还会自动进行广泛的交叉引用。

## 用于排版的导出实用程序
许多实用程序将接收一个 LaTeX 格式文档并将其转换为另一种更实用的格式。这种转换最常见的需求是转换为 HTML 格式（Linux 旧使用的 SGML 格式不再受支持）。有一些实用程序可以协助你将文档放到网上，以下章节中提供了一些样本。

### LaTeX2HTML
这是一个程序，它将把你的 LaTeX 文档转换为适用于 Web 的 HTML。该程序最有用的信息页面位于：

http://cbl.leeds.ac.uk/nikos/teXhtml/doc/latex2html/latex2html.html

在这个站点，你可以找到世界各地的镜像站点链接、概述以及手册，还有一些非常具有参考价值的示例（总是最实用的）。

### LTX2X
LTX2X 是一个更通用的 LaTeX 到 HTML（以及其他选项）转换器。通过为目标语言/脚本类型设置表格（例如，针对 HTML），LTX2X 将为你完成转换。这是一个更高级到专家级的工具，但即使是初学者也可以使用一些预设的转换。

LTX2X 可在以下地址获取：

ftp://ftp.dante.de/tex-archive/support/ltx2x.tar.gz

### CWEB2HTML
这是一个程序，可在以下地址获取：

http://www.cdc.informatik.tu-darmstadt.de/~lippmann/cweb2html/

