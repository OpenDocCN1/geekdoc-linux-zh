
```post-script
[me@linuxbox ~]$ zcat /usr/share/man/man1/ls.1.gz | groff -mandoc | head
%%PS-Adobe-3.0
%%Creator: groff version 1.18.1
%%CreationDate: Thu Feb 5 13:44:37 2009
%%DocumentNeededResources: font Times-Roman
%% font Times-Bold
%% font Times-Italic
%%DocumentSuppliedResources: procset grops 1.18 1
%%Pages: 4
%%PageOrder: Ascend
```

我们在上一章中简要提到了 PostScript，下一章将再次提到。PostScript 是一种页面描述语言，用于向类似排版机之类的设备描述打印页的内容。如果我们将命令的输出存储到文件中（假设我们正在使用一个带有 `Desktop` 目录的图形桌面）：

```bash
me@linuxbox~ $ zcat /usr/share/man/man1/ls.1.gz | groff -mandoc =
~/Desktop/foo.ps
```

桌面上应该出现一个输出文件的图标。通过双击图标，页面查看器应该启动并显示其渲染后的文件：

![](img/bf35d3b896a7fc440213722090d1b1cf_345_0.png)

图 4：在 GNOME 中用页面查看器查看 PostScript 输出

我们看到的是第 1 页精美的排版！事实上，可以使用此命令将 Script 文件转换为 PDF（便携文档格式）文件：

```bash
me@linuxbox~ $ ps2pdf ~/Desktop/foo.ps ~/Desktop/1.pdf
```

`ps2pdf` 程序是 `ghostscript` 包的一部分，它安装在大多数支持打印的 Linux 系统上。

> 提示：Linux 系统通常包含许多用于文件格式转换的命令行。它们通常遵循 `format2format` 的命名约定。尝试使用命令 `ls /usr/bin/*[:alpha:]][[:alpha:]]*` 来识别它们。也尝试搜索名为 `formatto` 的程序。

在我们关于 `groff` 的最后一个练习中，我们将再次回到旧的 `dist.txt`。这次，我们将使用 `tbl` 程序对表格进行格式化，以排版我们的 Linux 发行版列表。为了实现这一点，我们将使用 `tbl` 脚本向文本流中添加内容。注意我们将得到以下结果：

```text
| Linux Distributions |
| Name                |
| Ubuntu              |
| Fedora              |
| SUSE               |
| Debian              |
| Arch               |
```

首先，我们将使用 `tbl` 脚本产生以下内容：

```text
| Linux Distributions |
|---------------------|
| Name                |
| Ubuntu              |
| Fedora              |
| SUSE               |
| Debian              |
| Arch               |
```

等等，让我们重新检查一下过程。为 `groff` 添加 `t` 选项会指示它用 `tbl` 预处理文本。同样，`-T` 选项用于输出 ASCII 而不是默认的输出媒介。如果我们指定 PostScript 输出并图形化查看结果，我们将得到满意的：

```bash
[me@linuxbox ~]$ sort -k 1,1 -k 2n dist.txt | sed -f distros-tbl
sed | groff -t ~/Desktop/foo.ps
```

| Linux Distributions |

|---------------------|

| Name                |

| Ubuntu              |

| Fedora              |

| SUSE               |

| Debian              |

| Arch               |

![](img//bf35d3b896a7fc440213722090d1b1cf_348_0.png)

图 5：查看完成的表格

### 总结

由于文本是 Unix 类系统的核心，因此存在许多处理和格式化文本的工具是合理的。正如我们所见，确实如此！像 `fnt` 和 `pr` 这样简单的格式化工具将在生成短文档的脚本中有许多用武，而 `groff` 及其伙伴可以用于编写书籍。我们可能永远不会使用命令行写技术论文（尽管很多人这样做！），但知道我们可以这样做是好的。

### 扩展阅读

- **groff User’s Guide** http://www.gnu.org/software/groff/manual/

- **Writing Papers with norff Using -me:** http://docs.freebsd.org/44doc/usd/19.memmacros/paper.pdf

- **Tbl – A Program To Format Tables:** http://plan9.bell-labs.com/10thEdMan/tbl.pdf

- 当然，尝试维基百科上的以下文章：

    - http://en.wikipedia.org/wiki/TeX

    - http://en.wikipedia.org/wiki/Donald_Knuth

    - http://en.wikipedia.org/wiki/Typesetting

## 22 – 打印

在花费了最后几个章节处理文本之后，是时候将这些文本打印到纸上了了。在本章中，我们将查看用于打印文件和控制打印机操作的命令行工具。我们不会涉及如何配置打印，因为这随发行版的不同而异，并且通常在安装期间自动设置。请注意，我们需要一个可以工作的打印机配置来完成本章的练习。

我们将讨论以下命令：

- *pr* – 将文本文件转换为打印格式

- *lpr* – 打印文件

- *a2ps* – 为在 PostScript 打印机上格式化文件

- *lpstat* – 显示打印机状态信息

- *lpq* – 显示打印队列状态

- *lprm* – 取消打印作业

## 打印的简史

为了完全理解 Unix 类操作系统中的打印功能，我们必须首先学习一些历史。Unix 类系统上的打印可以追溯到操作系统本身的初期。在那个时代，打印机及其使用方式与今天大不相同。

### 昏暗时代的打印

与计算机本身一样，PC 之前的打印机往往是庞大、昂贵且集中的。

980 年代的典型计算机运行在连接到远处计算机的终端上。打印机位于计算机附近，并在计算机操作员的监视下工作。

当打印机昂贵且集中的时候（这在 Unix 早期经常如此），许多用户共享一台打印机是常见做法。为了识别属于特定用户的打印作业，通常会在每个打印作业开始前打印一张显示用户名的横幅页（banner page）。然后，计算机人员会装载当天打印作业的推车，并将它们交付给个人用户。

### 基于字符的打印机

80代的打印技术在两个方面非常不同。首先，那个时期的打印机几乎都是针式打印机。针式打印机使用机械机构通过撞击纸张上的墨带来在页面上形成印迹。当时两种流行的技术是花字轮打印和点阵打印。

第二个也是更重要的特征是，早期打印机使用一组设备固有的固定字符集。例如，花字轮打印机只能打印实际模刻在花字轮瓣上的字符。这使得打印机非常像高速打字机。大多数打字机使用等宽字体（固定宽度）进行打印。这意味着每个字符的宽度相同。打印是在页面的固定位置进行的，一页的可打印区域包含固定数量的字符。大多数打印机每英寸打印十个字符（CPI），垂直每英寸六行（LPI）。使用这种方案，一张美制信纸宽 85 个字符，高 66 行。考虑到每边的微小页，80 个字符被认为是打印行的最大宽度。这解释了为什么终端显示（以及我们的终端模拟器）通常为 80 个字符宽。这通过等宽字体实现了打印输出的“所见即所得”（WYSIWYG）。

数据以包含打印字符的简单字节流发送到打字机。例如，为了打印“a”，会发送 ASCII 字符代码 97。此外，低号 ASCII 控制代码提供了移动打印机小架和分页的方法，使用回车、换行等代码。通过控制代码，可以实现某些有限的效果，例如粗体，让打印机打印一个字符、退格、再次打印该字符以在页面上获得深色的打印效果。如果我们使用 `nroff` 渲染帮助页并使用 `cat` 查看输出，实际上可以目眼观察到这一点：
