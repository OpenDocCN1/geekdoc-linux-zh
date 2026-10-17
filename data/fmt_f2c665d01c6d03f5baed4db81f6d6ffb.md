
| OPTIONS -a Run all options with it.<br>-b Run some options.<br>-c Run one or two options.<br>-v Print the version number with the command. |

| COMMENTS If you don't like the command, don't tell me. It will hurt my feelings. |

| ENVIRONMENT VARIABLES This environment variables are used by waycool: |

| DISPLAY This sets the Display variable. |

**图 6-2: man 页格式添加页眉并布局页面。**

## 创建信函或备忘录

备忘录宏（`-mm`）曾盛用于 UNIX 用户之间。尽管具有各种模板的现代文字处理器已让 `mm` 过时，但在情况下，`mm` 仍然可以快速在文本环境中创建排版风格的文档。

要使用 `mm` 宏格式化并打印文档，请使用以下命令行（假设你的默认打印机是 PostScript 打印机）：

```bash
groff -mm -Tps -l letter.mm
```

## 表 6-1: man 宏

（注：表格内容部分未提供原文，故未进行翻译）

# 198 第二部分 + 使用红帽 Linux

主题：合并技术规范

日期：1999年4月11日

发件人：Christopher Craft

## 摘要

本备忘录详细说明了计划合并的规范。

# 合并描述与指令

根据我们与 XYZ 公司的谈判，我们计划进行合并。本文包含：

- 进度和时间表。
- 财务报表。
- 资产分配。

请提出您的任何修改意见，然后在在本页底部的批准行处签字。

诚挚地，

Christopher Craft

批准人：

John W. Doe, XYZ 公司总裁

日期

批准人：

Sylvia Q. Public, XYZ 公司首席财务官

日期

抄送至：

公司全体人员。

## 添加方程、表格和图片

有几组 Groff 宏允许您向 Groff 文档中添加特殊内容。这些宏需要特殊的预处理器。您可以使用 `EQN` 宏添加数学方程。使用 `TBL`，您可以在 Groff 中格式化表格。通过 `PIC`，您可以创建简单的线条图。

要解释这些宏，您可以在运行 `groff` 命令之前，对文件分别运行单独命令 (`eqn`, `tbl`) 和 `pic` 命令，或者可以在 `groff` 命令命令行添加选项，通过任何命令自动对文件进行预处理（`-e` 用于 `eqn`，`-t` 用于 `tbl`，`-p` 用于 `pic`）。

以下是可以包含在 Groff 文档中的 `EQN`、`TBL` 和 `PIC` 标记示例。第一个示例显示了一个可以由 `eqn` 对 Groff 文档进行处理的方程：

```
.EQ
a ~ mark = ~ 30
.EN
.EQ
a sup 2 ~ + b sup 2-lineup = ~ 1000
.EN
.EQ
x sup 3 ~ + y sup 3 ~ + z sup 3-lineup = ~ 1400
.EN
```

如果这些内容出现在 `memoeqn.mm` 的备忘录中，该备忘录将通过 `eqn` 进行预处理，然后使用以下命令发送到打印机：

```
groff -Tps -l -mm -e memoeqn.mm
```

`.EQ` 和 `.EN` 宏之间的所有数据都被解释为方程。方程生成的输出结果将如图 6-5 所示。

要在 Groff 文档中创建表格，请使用 `tbl` 处理器的 `.TS` 和 `.TE` 宏。以下是用于生成简单表格的标记示例。

```
.TS
center, box, tab(:);
c c s
c | c | c
c 1 | 1 | 1.
Mergers and Acquisitions Team
Employee:Title:Location
Jones, James:Marketing Manager:New York City
Smith, Charles:Sales Manager:Los Angeles
Taylor, Sarah:R&D Manager:New York Office
Walters, Mike:Information Systems Manager:Salt Lake City Office
Zur, Mike:Distribution Manager:Portland Office
.TE
```

`.TS` 宏开始后，下一行表示表格应在页面上居中（`center`）并被线框包围，并将使用冒号将数据分隔到单元格中（`tab::`）。下一行显示标题应该在框内居中（`c`）并跨越接下来的两个单元格（`s`）。下一行指示每个单元格的标题应该居中（`c | c | c`），随后的数据单元格应该左对齐（`1 | | 1`）。

表格定义行的尾**必须**有一个句号。在这种情况下，它位于 `| 1 | 1.` 这一之后。如果没有该句号，`tbl` 将尝试将文本解释为表格定义的一部分，并将导致失败。

表格中的其余信息是数据。注意 `tab` 分隔符冒号字符（:`）。当表格完成后，您将尝试使用 `.TE` 宏。

如果表格文件名为 `memotbl.mm`，`tbl` 将预处理备忘录，然后使用以下命令发送到打印机：

```
groff -Tps -l -mm -t memotbl.mm
```

`.TS` 和 `.TE` 宏之间的内容被解释为表格。图 6-6 显示了上一个示例输出中该表格的示例。

# 合并收购团队

| 员工 | 职位 | 地点 |
|---|---|---|
| Jones, James | 市场经理 | 纽约 |
| Smith, Charles | 销售经理 | 洛杉矶 |
| Taylor, Sarah | 研发经理 | 纽约办公室 |
| Walters, Mike | 信息系统经理 | 盐湖城办公室 |
| Zur, Mike | 分销经理 | 波特兰办公室 |

图 6-6：通过使用 `tbl` 命令的 `.TS` 和 `.TE` 宏来设置文本对齐方式并分列。

`PIC` 宏（`.PS` 和 `.PE`）允许您在 Groff 中创建简单的图形和流程图。`PIC` 仅适用于创建简单的框、圆、椭圆、线、样线和某些文本。以下是可以包含在 Groff 文档中的一些 `PIC` 代码示例。

```
.PS
box invis "Start" "Here"; arrow
box "Step 1": arrow
circle "Step 2": arrow
elipse "Step 3": arrow
box "Step 4": arrow
box invis "End"
.PE
```

在 `PS` 之后，第一行表示一个包含“Start Here”字样的不可形框（`invis`），后面跟着箭头。该箭头连接到包含 *Step 1* 字样的下一个框。后续元素（通过箭头连接）是一个圆（Step 2）、一个椭圆（Step 3）、另一个框（Step 4）以及另一个不可形框。`.PE` 表示绘图结束。

如果这些行出现在名为 `mempic.mm` 的文档中，可以使用以下命令预处理 `pic` 并打印。图 6-7 显示了该图的示例：

```
groff -Tps -l -mm -p mempic.mm
```

**图 6-7**：使用 `pic` 命令的 `.PS` 和 `.PE` 宏创建简单的流程图。

# 使用 TeX 处理文本

`TeX` 解释来自 `latex` 文件的宏。默认情况下，`.tex` 和纯文本格式文件是在安装 LaTeX 时自动构建的。除了 `latex` 之外，还有其他可以使用 `TeX` 的宏格式文件：

- `ams`——美国数学学会将其作为官方排版系统。许多数学出版物使用该宏。
- `amlatex`——为 `latex` 添加 `ams` 功能。
- `explain`——包含索引、目录和交叉引用的宏。
- `latex`——可以配合 `amtex` 提供许多功能。
- `texinfo`——自由软件基金制作 Linux 手册使用的宏。

您可以使用任何文本编辑器创建 `TeX/LaTeX` 文件。创建宏后，您可以运行 `tex` 命令（或若干实用程序）来格式化文件。输入文件格式为 `filename`。输出三个不同的文件：

1. `filename.dvi`——设备无关的输出文件，可以转换为多种类型的输出设备（如 PostScript）。
2. `filename.log`——包含诊断信息的日志。
3. `filename.aux`——LaTeX 使用的辅助文件。

生成的 `dvi` 文件可以针对您使用的特定设备进行格式化。例如，可以使用 `dvips` 命令将结果输出到您的 PostScript 打印机。或者，可以使用 `undoubt` 命令在 X 窗口中预览 `dvi` 文件。

# 创建和格式化文档

由于 LaTeX 是使用 TeX 的常用方式，本节介绍了如何创建和格式化 LaTeX 文档。LaTeX 宏（称为命令）以两种方式之一出现在文档中：

> `\string(option)[required]` 首先是一个反斜杠（`\`），后面跟着一个字符串（替换为命令名称）。可选参数包含在大括号（`{}`）中，必需参数包含在方括号（`[]`）。

> `\?[option)[required]` 首先是一个反斜杠（`\`），后面跟着一个非字母的字符（替换为命令）。可选参数包含在大括号（`{}`）中，必需参数包含在方括号（`[]`）。

每个命令定义了要执行的操作。该操作可以控制页面布局、使用的字体、间距、段落布局以及对文档的各种操作。LaTeX 文档的最少格式化内容如下：

```latex
\documentclass{name}
\begin{document}
TEXT GOES HERE!
\end{document}
```

你应该将 `name` 替换为你正在创建的文档类别的名称。有效的文档类包括 `article`、`book`、`letter`、`report` 和 `slides`。文件的文本以及你的格式命令位于 `begin document` 和 `end document` 命令之间。

学习 LaTeX 的最佳方法是使用 `Lyx` 编辑器。`Lyx` 为创建 LaTeX 文档提供了一个图形化用户界面（GUI）。它还包含了多种模板，你可以使用这些模板而不是从头开始创建文档。图 6-8 显示了 `Lyx` 编辑器的示例。

![](img/24eb519de215a464182200824abe9318_232_0.png)

**图 6-8：** 使用 `Lyx` 编辑器创建 LaTeX 图形。

随附附 CD-ROM 的 Red Hat 发行版未自带 `Lyx` 编辑器。不过，你可以在 `ftp://contrib.redhat.com` 找到 `Lyx` 的 RPM 软件包。你可能还需要安装 `xforms` 软件包（你可以从 `http://bragg.phys.uwm.edu/xforms` 获取）。

如果你想在普通的文本编辑器中编辑 LaTeX，你需要熟悉 LaTeX 命令。要获取 LaTeX 命令的完整列表，在输入以下内容后，进入“Commands within a LaTeX document”部分：

```
info latex
```

## 使用 Lyx LaTeX 编辑器

你可以使用 `lyx` 命令启动 `Lyx` LaTeX 编辑器（可能位于 `/usr/bin/lyx` 或 `/usr/local/bin/lyx`）。`Lyx` 附带了大量的辅助文档。点击“Help”（帮助）可以从教程、用户指南、参考手册或其他信息中进行选择。

为了开始编写你的第一个文档，我建议你使用 `Lyx` 提供的模板之一。模板位于 `/usr/share/lyx/templates`。要打开模板，点击 `File->New from template` 并选择 `Templates`。目前有用于信件、技术论文和 Linux 文档的模板可用，这仅是示例。

除了提供剪切、复制和粘贴等编辑功能外，你还可以从“Layout”（布局）菜单中执行各种标记功能。你可以更改字符字体、段落对齐方式和间距，以及文档特性（如列、驱动程序和页面样式）。从“Insert”（插入）菜单中，你可以导入封装的 PostScript（EPS）图片、表格和不同的文件类型（包括 ASCII 和 Lyx 文件）。

对于数学函数，“Math”菜单允许你向文档中插入分数、平方根、指数、求和和积分函数。当你完成时：

- 将文件打印到 PostScript 打印机或输出 PostScript（`.ps`）文件。（点击 `File->Print`，选择打印方法，然后点击 OK。）
- 将文件导出为 `dvi` 格式。（点击 `File->View.dvi`）。你的文档将出现在 `xdvi` 窗口中，该窗口显示了文档打印后的外观。

`Lyx` 自称为 WYSIWYM 编辑器——所见即所得（What You Say Is What You Mean）。因此，你在编辑时在屏幕上看到的与打印文档并不完全相同。例如，多次按 Enter 键行间不会出现额外的空白。同样，分页是在打印/格式化阶段完成的。

由于 `Lyx` 支持样式文件（style files），它允许你创建符合多种不同标准的文档。例如，`Lyx` 支持使用 `article` 为美国数学学会（AMS）期刊进行排版。其他文本类还包括：

- `article`—单面纸张，无章节。
- `report`—双面报告，通常比 `article` 长。
- `book`—与 `report` 相同，带有额外的前言和后记。
- `slides`—用于制作幻片。
- `letter`—包括用于地址、签名和其他信件元素的特殊环境。

## 打印 LaTeX 文件

无论你是自己创建的 LaTeX、从 `Lyx` LaTeX 编辑器导出的，还是从互联网下载的，都有多种实用程序可以格式化、打印或显示你的输出。以下是你的一些选择：

要格式化 LaTeX 文件（`filename.tex`），请运行以下命令。

```
latex filename.tex
```

要打印 `.dvi` 文件（`filename.dvi`），将其发送到你的默认 PostScript 打印机并输入：

```
dvips filename.dvi
```

要在 X 窗口中显示 `dvi` 文件，请输入以下内容：

```
xdvi filename.dvi
```

要将 `.dvi` 文件打印到 PCL 打印机（如 HP LaserJet），请输入以下内容：

```
dvicopy filename.dvi
dvilj filename.dvi
```

`dvilj` 命令直接不支持虚拟字体。`dvicopy` 命令转换字体，以便 PCL 打印机处理。

## 转换文档

文档可能以许多不同的格式提供。只需搜索互联网上的一些 Linux FTP 站点，就能找到 PostScript、DVI、man、PDF、HTML 和 TeX 格式。还有多种图形格式。

如果你将文档平台从一个文字处理应用程序切换到另一个，将文件从一种格式转换为另一种格式可能特别重要。Red Hat Linux 有许多工具可以将文档和图形从一种格式转换为另一种格式。要转换来自 Microsoft Word 等流行文字处理器的文档文件，请参见本章稍后关于 Linux 文字处理器的描述。

以下是文档和图形转换实用程序列表：

- `fax2ps`—将 TIFF 传真图像转换为压缩 PostScript 格式。PostScript 输出针对发送进行了优化。
- `fax2tiff`—将传真数据（Group 3）转换为 TIFF 格式。
- `g32bm`—将 Group 3 图像转换为便携位图。
- `gif2tiff`—将 GIF (87) 文件转换为 TIFF。
- `man2html`—将 man 页面转换为 HTML。
- `pal2rgb`—将 TIFF 图像（调色）转换为全色 RGB。
- `pbm2g3`—将便携位图转换为 Group 3。
- `pdf2dsc`—将 PDF 格式转换为 PostScript 文档 DSC。
- `pdf2ps`—将 PDF 格式转换为 Postscript（第 2 级）。
- `pdf2pfa`—将 Type 1 PostScript 字体（二进制-DOS 表示法）转换为 ASCII 可读格式。
- `pdf2pdf`—将 PostScript 文件转换为 PDF 格式。
- `pdf2pk`—将 Type 1 PostScript 字体转换为 TeX pkfont。
- `ppm2tiff`—将 PPM 图像转换为 TIFF。
- `ras2tif`—将 Sun 光栅文件转换为 TIFF 格式。
- `texi2html`—将 Texinfo 文件转换为 HTML。
- `pk2bm`—将 TeX pkfont 文件转换为位图。
- `ps2ascii`—将 PostScript 转换为 ASCII 文本。
- `ps2eps`—将 TIFF 图像转换为 PostScript。
- `tif2bw`—将 RGB 或调色板 TIFF 图像转换为灰度 TIFF 图像。
- `tif2ps`—将 TIFF 图像转换为 PostScript。

## 使用商业文字处理器

随着 Linux 系统数量的日益增长，越来越多的商业应用程序变得 Linux 可。在文字处理领域，已经有几种强大的产品可用，可以帮助非技术导向的用户过渡到 Red Hat Linux。本节描述了以下 Linux 商业文字处理器：

- Approx Words 提供文字处理和出版功能。Approx Graphics 是一个绘图、图表和图形编辑应用程序。Approx Spreadsheets 提供自定义。

## 第 6 章 在 Red Hat Linux 上发布 207

电子表格、数值分析、目标寻求、图表、图形和投影表。此外，Applixware 还包含创建演示文稿、管理电子邮件、编写 HTML、访问数据库以及构建自定义决策支持的功能。

- * StarOffice 办公套件包含文字处理、电子表格、演示文稿、电子邮件、新闻、图表和图形应用程序。它的设计是为了在 Linux 系统上运行，也可以在其他环境中运行。它可以导入和导出多种 Microsoft 文件格式。
- * WordPerfect — 曾经，WordPerfect 是 PC 上最流行的文字处理软件。尽管它被 Word 取代了（并从 WordPerfect 公司转到 Novel、Invention，再到 Corel 公司），但它仍然是一个强大的文字处理器。WordPerfect 版本 8 已经移植到 Linux。
