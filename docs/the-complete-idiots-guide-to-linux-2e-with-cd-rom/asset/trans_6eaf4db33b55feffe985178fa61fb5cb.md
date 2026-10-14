

## 完全傻瓜的 Linux 使用指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## UNIX 打印入门

在这本书中，我有点忽略了告诉你如何打印文件，部分原因是如果你使用的是 StarOffice、WordPerfect 或 Applix 等文字处理器，这些程序已经知道如何打印而无需经过这些麻烦（StarOffice 包含在这本书附带的 CD 上。）

如果你想从命令行进行 UNIX 文本处理（与在 GUI 中进行文字处理相对），有几件事你需要知道，这会影响你打印的文档的最终呈现。Linux 和 UNIX 下的打印与 Windows 或 Macintosh 下的打印截然不同。从命令行打印涉及三个步骤：

- 1. 使用文本编辑器创建文档，并在需要时添加格式命令。这些格式命令或宏将取决于你使用的格式化程序。然而，文本标记（UNIX 人喜欢称之为文本处理）的概念是相同的。
- 2. 将你的文档通过一个或多个过滤器运行（某些过滤器可能像我之前提到的 fmt 命令一样基础）；最终的过滤器通常会生成一个包含所有必要打印机控制代码以呈现文档的文件。有时，过滤器可以直接将此输出发送到打印机。
- 3. 使用名为 lpr 的程序将过滤后的文件发送到打印机。

如果你只需要打印一个纯文本文件，你必须做几件事。你使用的程序将取决于你拥有的打印机类型。通常，打印机分为两类：具有 PostScript 的和不具有 PostScript 的。

如果你的打印机具有 PostScript 支持，你可能会使用一个名为 enscript 的程序。如果没有，你将使用一个名为 pr 的程序。在表面上，这些程序是等效的——只是 enscript 利用了 PostScript 可用的功能，因此功能更多。这些程序在基本层面上允许你指定页边距、页眉和文本行的长度。

不花哨，但它们提供了生成一个相当朴素外观文档所需的基本格式化功能。

这里有一个例子。如果你想打印一个名为 intro.txt 的文本文件，你会将其发送给 pr：

```
pr intro.txt
```

将同一文件发送到 PostScript 打印机将是这样做的：

```
enscript intro.txt
```

pr 和 enscript 都可以将输出发送到打印机，并且默认情况下它们就是这样做的。抛开这一点，这些基本调用几乎不会产生你期望的输出。页边距是什么？行在哪里折叠？你明白了。你需要在 pr 或 enscript 上设置所有这些选项，否则你的文档将使用打印机的默认设置。你的默认值将类似于从纸张边缘起左侧和顶部页边距为 1/2"，行长度约为 72 个字符宽，以及 Courier（打字机）字体——很可能不是你想要的。那你该怎么办？

你需要做的第一件事是阅读 man 手册并弄清楚你想要的 pr 或 enscript 的默认设置。除此之外，你可能还必须使用另一个格式化命令，例如 fmt。当你弄清楚各种设置后，你只需反复使用它们。

我的典型 enscript 会话大致如下：

```
[alberto@digital alberto]$ fmt -w 65 intro.txt | enscript --margins=100:100:100:100 -h -B
[ 1 pages * 1 copy ] sent to printer
```

我使用 fmt 创建约 65 个字符宽的行，然后将输出通过管道传递给 enscript。我将页边距选项设置为 100 像素（72 像素 = 1"），并且使用 -h 选项，抑制横幅页的打印（该页说明谁打印了文件并浪费纸张）。-B 选项抑制通常显示文档标题、上次保存时间和页码的页眉行的打印。

我也可以使用 pr 产生类似的输出，如下所示：

```
fmt -w 65 intro.txt | pr -o 15
```

-o 选项指定左侧页边距的字符数；15 个字符约为 1.5"。

要访问内容，请点击章节和节标题。

## 完全傻瓜的 Linux 使用指南

（出版社：Macmillan Computer Publishing）
作者：Manuel Ricart
ISBN：078971826x
出版日期：12/22/98

搜索本书：

## UNIX 文本处理

要生成更精美的输出，例如粗体文本、不同字体等，你需要使用 UNIX 的格式化程序之一，例如 groff（传统 troff 格式化程序的 GNU 版本）。如果你查看 man 页的源代码，你会看到你在使用 groff 时使用的格式化代码。（要查看源代码，请对 /usr/man/man1/ 中的任何文档使用 zless。）这是一个你会看到的例子：

```
.TH man 1 "September 2, 1995"
.LO 1
.SH NAME
man \- format and display the on-line manual pages
.br
manpath \- determine user's search path for man pages
.SH SYNOPSIS
man [\-acd fhkKtwW] [\-m system] [\-p string] [\-C config_file] [\-M path] [\-P pager] [\-S section_list] [section] name ...
.SH DESCRIPTION
.B man
formats and displays the on-line manual pages. This version knows about the
.B MANPATH
and
.B (MAN) PAGER
environment variables, so you can have
your own set(s) of personal man pages and choose whatever program you like to display the formatted pages. If
.I section
is specified,
.B man
only looks in that section of the manual.
You may also specify the order to search the sections for entries
```

正如你从此源文本中看到的，groff（troff！）格式化的文件没有任何空行。格式化命令（宏）必须从左边缘开始。宏的名称通常以点（.）或撇号（'）开头。格式化一直持续到另一个宏覆盖它为止。

你使用的宏将取决于你设计的文档类型。前面列表中的宏是为格式化 UNIX 手册页而设计的。例如，Man 定义了诸如 .B 用于粗体和 .I 用于斜体以及更复杂的用于定义标题、描述等的宏。如果你曾经使用文本编辑器编写过 HTML 页面，从 UNIX 命令行格式化文本在概念上并没有那么不同，只是标记标签不同。标记标签会根据你使用的宏包而改变。例如，另一个名为 ms 的包提供了论文的格式化。

正如你可能已经猜到的，你实际上能做什么取决于你拥有的宏。除了前面提到的 man 宏之外，其他库如 ms、mm 和 me 用于格式化其他类型的文档（请参阅 UNIX 手册第 7 节中的 groff_ms、groff_mm、man 和 me；要进入那里，输入 man 7 keyword）。代码以及它们如何格式化文档因包而异。

当你的文本以这种（有些别扭）的方式格式化时，你可以使用 groff 命令生成文本、PostScript、HTML、LaserJet 打印机和其他格式的输出。然后你将生成的此文件发送给 lpr 命令以打印它。lpr 命令接受你提供的内容并将其排队到打印机。语法如下所示：

```
nroff -Tps -macropackage filename | lpr
```

将 macropackage 替换为宏的名称（man 用于手册页，ms、me、mm 等）和 filename 替换为你的文件名。

正如你所知，要生成一个简单格式化的文档，你需要知道很多东西。UNIX 文本处理并不止于 groff。其他更复杂的排版系统如 TeX 和 LaTeX 可以生成专业格式的文档。许多印刷的技术出版物都是使用 TeX 和 LaTeX 开发和印刷的。

那么为什么这么复杂？UNIX 命令行打印系统的意图是使用任何可以显示和正确打印到各种设备的文本编辑器生成文件。因此，你可以生成手册页，在纸上打印它们，生成 HTML 页面，并生成 pdf（Adobe Acrobat）文件，所有这些都来自同一个格式化的文件。如果你只是想使用文字处理或桌面出版，请坚持使用 GUI 文字处理器，例如 StarOffice 中包含的文字处理器。当你只需要一份漂亮的纸质文档时，它会为你节省时间。

