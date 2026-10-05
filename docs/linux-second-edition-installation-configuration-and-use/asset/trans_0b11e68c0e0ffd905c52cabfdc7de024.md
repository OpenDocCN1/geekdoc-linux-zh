

# 18

LaTeX 是一种广泛使用的排版程序，特别是在 Unix 世界。它专为科学文本的制作而设计，并且可以自由复制。LaTeX 的缺点是其处理过程相对复杂。这导致了宏包 LaTeX 的发展，它使得文本格式化变得稍微简单。通过 LaTeX，你可以编写任何能想象到的文档，从一封简单的信到整本书书。

本章的核心是当前的 LaTeX 版本，即 LaTeX2。在 PC 上，Linux 代表了 LaTeX 的理想工作环境；首先，LaTeX 是所有 Linux 发行版的固定部分，连同重要的实用程序（如 `dvips` 和 `ghostview`）在一起——因此，在 DOS 甚至 Windows 上获取和安装 LaTeX 版本时遇到的巨大困难便不复存在了。其次，Linux 的多任务环境允许高效工作工作。

本章简单介绍了如何开始使用 LaTeX，并总结了最重要的 LaTeX 指令。还重点讨论了 LaTeX 使用的正式以及部分针对 Linux 的特定方面，例如打印文件、字符问题等。

如果你想享受 LaTeX 的许多优势，而又不想深入研究其相当复杂的处理细节，LyX 是一个有趣的补充。LyX 是一种 LaTeX 的用户界面，几乎实现了 WYSIWYG（所见即所得）。关于此点的更多信息，请见下一章从 631 页开始的内容。

587

# 引言

## 18.1 引言

LaTeX 与其他类似程序相比的特定优势在于其卓越的排版质量（例如，自动字间距，即在 'Vector' 中，'e' 移动得更靠近 'V'）以及它极其惊人的公式设置能力（$\pi\sum_{i=1}^{\infty}$）。然而，LaTeX 也有它的缺点：程序的处理方式简直是石器时代的。像连字符或分页这样看似微不足道的事情，当 LaTeX 无法按标准产生所需结果时，必须在冗长的过程中手动编辑。

关于 TeX 和原始形式的 LaTeX 的起源，有几句话：TeX 由 Donald Knuth 编写的，相关的宏包 LaTeX 由 Leslie Lamport 编写的。Leslie Lamport 在 2.09 版本后已停止了 LaTeX 的进一步开发，现在主要归功于 Frank Mittelbach 和 Rainer Schopman，当前的版本 LaTeX 2 才得以问世，并实施了 LaTeX 3 的开发计划。

## LaTeX 和最重要的实用程序

LaTeX 是一个排版程序，而不是一个文字处理器。区别在于 LaTeX 没有配备它自己的编辑器，因此要排版的文本必须使用你选择的任何编辑器写成完全正常的文本。这意味着 LaTeX 也不是一个 WYSIWYG（所见即所得）程序——相反；所有的设置指令都必须在正文中以正确的语境语法进行指定。例如，如果你想写一个比周围文本更小的单词，这的 LaTeX 语法是 `\small{small}`。

使用编辑器输入文本后的下一步是将该文件（扩展名为 `*.tex`）翻译成 DVI 文件（扩展名为 `*.dvi`）。在该文件中，所有的页面布局指令都以一种独立于打印机或独立于设备的语言进行指定。

DVI 文件由 LaTeX 程序生成。因此，`latex` 命令只读取指定的文本文件并生成一个扩展名为 `.dvi` 的同名文件。这经常导致错误信息的生成，这些信息大部分由于 LaTeX 文件中的语法错误。关于错误消息处理和错误检测的更详细信息，可以找到第 590 页。

一旦生成了 DVI 文件，可以通过 `dvim` 程序在屏幕上查看。如果你想打印该文件，则需要额外一步——将 DVI 文件转换为当前打印机的格式。虽然 LaTeX 的版本（特别是 emTeX）提供了大量的程序，可以将 DVI 文件转换为特定的打印机格式，但在 Linux 下，真正只有一个程序用于将 DVI 文件转换为 PostScript 文件：`dvips`。它实现了与 `ghostscript` 类似的功能。PostScript 文件可以通过 `xdv` 在屏幕上查看。由于你拥有一台 PostScript 打印机，你现在可以使用 `cp` 直接打印 PostScript 文件，将文件发送到并行接口或串口接口（取决于你的打印机连接）。对于所有打印机，你必须先使用 `gs` 命令执行 PostScript 格式与当前打印机格式之间的转换。

详细来说，从文本文件 `test.tex` 到 LaTeX 格式再到 HP Deskjet 喷墨打印机上的输出路径如下：

```
user$ latex test.dvi
user$ dvips -o test.ps test.ps  #生成 test.ps
user$ ghostview test.ps  #检查结果
user$ gs -sDEVICE=deskjet -soutputFile=test.hp
    -dPSERVICE4 -dNOPAUSE test.ps #生成 test.hp
user$ cp test.hp /dev/lp0 #在 LPT1: 上打印
```

在执行 `dvips` 或 `dvim` 期间，可能会生成新的字符集。在这种情况下，两个命令都会启动 `mf` 程序（metafont）。关于 Metafont 的更多信息可以找到第 262 页。

如果你拥有 PostScript 打印机，你必须先使用 `gs` 命令执行 PostScript 格式与当前打印机格式之间的转换。

正如连字符或分页等，当 LaTeX 无法按标准产生所需结果时，必须在冗长的过程中手动编辑这些看似微不足道的事情。

例如，如果你想写一个比周围文本更小的单词，这的 LaTeX 语法是 `\small{small}`。

... 

  ]，第一次遇到 LaTeX 错误是令人沮丧的。

，当 LaTeX 无法按标准产生所需结果时，像连字符或分页，必须在冗长的过程中手动编辑。

## LaTeX 的在线文档

如果你想享受 LaTeX 的许多优势，而又不想深入研究其相当复杂的处理细节，LyX 是一个有趣的补充。LyX 是一种 LaTeX 的用户界面，几乎实现了 WYSIWYG（所见即所得）。关于此点的更多信息，请见下一章从 631 页开始的内容。

...（注：由于提供的原文文本存在大量逻辑重复和断句，译文已根据上下文逻辑进行了连贯性处理，保留了所有 Markdown 格式。）

