
- `filename.dvi`：这是一个设备无关的输出文件，可以用于多种输出设备。
- `filename.log`：这是一个包含诊断信息的日志文件。
- `filename.aux`：这是一个 LaTeX 使用的辅助文件。

## 创建和格式化 LaTeX 文档

由于 LaTeX 是使用 TeX 最常见的方式，本节介绍了如何创建和格式化 LaTeX 文档。LaTeX 宏（通常称为命令）以以下两种形式之一出现在文档中：

- `\string[必需性参数]` — 首先是一个反斜杠（\），后面跟着一串字符。（将 string 替换为命令名称）。可选参数包含在大括号（\}）中，而必需性参数包含在方括号（\[ 中。
- `\?\option[必需性参数]` — 首先是一个反斜杠（\），后面跟着一个不是字母的单个字符。（将 \ 替换为命令字符）。可选参数包含在大括号（\}）中，而必需性参数包含在方括号（\[) 中。

每个命令都定义了某个要执行的操作。该操作可以控制页面布局、使用的字体、间距、段落布局或文档的各种其他操作。LaTeX 文档可以包含的最少格式化内容如下：

```
\documentclass{name}
\begin{document}

TEXT GOES HERE!
\end{document}
```

您应该将 `(name)` 替换为您正在创建的文档类名称。有效的文档类包括 `article`、`book`、`letter`、`report` 和 `slides`。文件的文本以及您的格式化命令位于 `begin` 和 `end` document 命令之间。

入门 LaTeX 的最佳方法是使用 LyX 编辑器。LyX 提供了一个用于创建 LaTeX 文档的图形用户界面（GUI）。它包含了许多可以使用的模板，而无需从头开始创建文档。图 6-8 显示了 LyX 编辑器的示例。

> 注意
> 随书附带的 CD-ROM中的 Red Hat Linux 并不带有 LyX 编辑器。您可以从 LyX FTP 网站 (`http://ftp.lyx.org/pub/lyx/bin`) 找到 LyX 的 RPM 软件包。除了需要安装几个 `texlive` 软件包来安装 LyX 之外，您还需要 `forms` 软件包（可以从 LyX.org FTP 网站获取）。

如果您想在普通的文本编辑器中编辑 LaTeX，将需要熟悉 LaTeX 命令。要查看完整列表，请查看 `info latex` 然后进入“Commands within a LaTeX document”部分。

![](img/0823b2119053dace3be4993846bb1ee1_263_0.png)

## 第6 章 ✦ 使用 Red Hat Linux 出版 231

![](img/0823b2119053dace3be4993846bb1ee1_264_0.png)

欢迎使用 LyX！

### 使用 LyX 时需要的几件事

1. LyX 带有极的文档——请务必使用它们！从 `Help->Introduction` 开始，它将为您提供关于文档非常简短的介绍。然后通过 `Help->Tutorial` 学习如何使用 LyX。
2. LyX 是我们所谓的“文档处理器”。从设计上，它与普通的文字处理器不同，这种不同使得编写文档变得更容易。它只是有一点不同，所以不要害怕。文档会让一切变得清晰。
3. LyX 的输出效果非常棒！现在选择 `File->View` 亲自查看吧。

图 6-8：使用 LyX 编辑器图形化查看 LaTeX 文档。

### 使用 LyX LaTeX 编辑器

您可以使用 `lyx` 命令启动 LyX 编辑器（可能位于 `/usr/bin/lyx`）。LyX 带有许多支持文档。点击 `Help` 选择 `Tutorial`、`User's Guide`、`Reference Manual`或其他信息。

要开始编写第一个文档，我建议选择 LyX 提供的模板之一。模板位于 `/usr/share/lyx/templates`。要打开模板，点击 `File->New template` 并选择 `Templates`。有适用于信件、技术论文和 Linux 文档的模板，仅举此。

除了排序标准的编辑功能（如剪切、复制和粘贴）外，您还可以从 `Layout` 菜单执行各种标记功能。您可以更改字符字体、段落对齐和间距，以及文档特征（如列、驱动程序和页面样式）。从 `Insert` 菜单，您可以导入封装的 PostScript (`EPS`) 图像、表格和不同类型的文件（ASCII 和 LyX 文件）。

至于数学函数，`Math` 菜单允许您向文档中插入分式、根号、指数、求和和积分函数。完成后，您可以：

- 将文件导出到 PostScript 打印机或输出 (`.ps`) 文件。（点击 `File->Print`，选择打印方法，然后点击 `OK`。）
- 将文件输出为 dvi 格式。（点击 `File->View.dvi.`）您的文档将出现在 `xdv` 窗口中，该窗口显示文档打印后的样子。
- 将文件导出为 LaTeX、DVI、PostScript 或 ASCII 文本。（点击 `File->Export` 并从格式列表中选择。）

`www.unlisted.com` 上的内容将其称为 WYSIWYM 编辑器——所见即所得（What You Say Is What You Mean）。因此，你在屏幕上看到的并不是打印文档的样子。例如，多次按回车不会在行之间出现额外的空格。同样，分页是在打印/格式化阶段完成的。

由于 LyX 支持样式文件，它允许您创建符合多种标准的文档。例如，LyX 支持使用 `article` 类为美国数学学会 (`AMS`) 杂志进行排版。其他支持的文本类包括：

- `article`—单面纸，无章节。
- `report`—双面报告，长度通常比 `article` 长。
- `book`—与 `report` 相同，但用于书籍。
- `letter`—信件。
- `slides`—幻灯片。

## 输出 LaTeX 文件

无论您是在 LyX 编辑器中创建 LaTeX 文件，还是从网上下载的，您都有多种方法将其输出。由于 LyX 支持，输出格式非常灵活。以下是常见的输出方式：

- 导出到 PostScript 打印机或输出 (`.ps`) 文件。（点击 `File->Print`，选择打印方法，然后点击 `OK`。）
- 输出文件到 dvi 格式。（点击 `File->View.dvi.`）您的文档将出现在 `xdv` 窗口中，该窗口显示文档打印后的样子。
- 将文件导出为 LaTeX、DVI、PostScript 或 ASCII 文本。（点击 `File->Export` 并从格式列表中选择。）

由于 LyX 支持样式文件，它允许您创建符合多种标准的文档。例如，LyX 支持使用 `article` 类为美国数学学会 (`AMS`) 杂志进行排版。其他支持的文本类包括：

- `article`—单面纸，无章节。
- `report`—双面报告，长度通常比 `article` 长。
- `book`—与 `report` 相同，但用于书籍。
- `letter`—信件。
- `slides`—幻灯片。

## 转换 LaTeX

无论您是在 LyX 编辑器中创建 LaTeX 文件，还是从网上下载的，您都有多种方法将其转换。由于 LyX 支持，输出格式非常灵活。以下是常见的转换方式：

- 导出到 PostScript 打印机或输出 (`.ps`) 文件。（点击 `File->Print`，选择打印方法，然后点击 `OK`。）
- 输出文件到 dvi 格式。（点击 `File->View.dvi.`）您的文档将出现在 `xdv` 窗口中，该窗口显示文档打印后的样子。
- 将文件导出为 LaTeX、DVI、PostScript 或 ASCII 文本。（点击 `File->Export` 并从格式列表中选择。）

## 234 第二部分 使用 Red Hat Linux

- `ps2pk` — 将 Type 1 类型 PostScript 字体转换为 TeX pk 字体。
- `pstotext` — 将 PostScript 文件转换为 ASCII 文本。`pstotext` 类似于 `ps2ascii`，但它在处理字体编码和间距调整方面比 `ps2ascii` 更好。此外，`pstotext` 不转换 PDF 文件。
- `ras2ttf` — 将 Sun 栅化文件转换为 TIFF 格式。
- `texi2html` — 将 Texinfo 文件转换为 HTML。
- `tiff2bw` — 将 RGB 或调色板（Palette）色彩 TIFF 图像转换为灰度 TIFF 图像。
- `tiff2ps` — 将 TIFF 图像转换为 PostScript。
- `unix2dos` — 将 UNIX（Linux）文本文件转换为 DOS 文本文件。

## 创建 DocBook 文档

文档项目通常需要生成输出为多种格式的文档。例如，描述如何使用某个软件程序的相同文本可能需要输出为打印手册、HTML 页面和 PostScript 文件。Linux 社区最近采用的创建所谓*结构化文档*的标准是 SGML、XML 和 DocBook。

## 理解 SGML 和 XML
