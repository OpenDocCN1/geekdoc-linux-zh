

每个命令都定义了要采取的某些操作。该操作可以控制页面布局、所用字体、间距、段落布局，或对文档执行的各种其他操作。LaTeX 文档所能包含的最少格式化内容如下：

```
\documentclass{name}  
\begin{document}  
TEXT GOES HERE!  
\end{document}
```

您应将 {name} 替换为您要创建的文档类的名称。有效的文档类包括 article、book、letter、report 和 slides。文件的文本连同您的格式化命令，位于 \textit{begin} 和 \textit{end} 文档命令之间。

开始使用 LaTeX 的最佳方式是使用 LyX 编辑器。LyX 为创建 LaTeX 文档提供了 GUI。它还包含各种模板，您可以使用它们，而不必完全从头创建文档。图 6-10 展示了 LyX 编辑器的示例。

![](img/27a85d56d393921ced6412ae6e8336bf_248_0.png)

**图 6-10：** 使用 LyX 编辑器以图形方式创建 LaTeX 文档。

**注意：** LyX 编辑器不随 Red Hat Linux 提供。请从 LyX 站点 ftp://ftp.lyx.org/pub/lyx/bin 查找 LyX 的 RPM 包。寻找 Red Hat RPM。

如果您想在常规文本编辑器中编辑 LaTeX，则需要熟悉 LaTeX 命令。要获取 LaTeX 命令的完整列表，请输入 \texttt{info latex}，然后转到“Commands within a LaTeX document”（LaTeX 文档中的命令）一节。

## 使用 *LyX* *LaTeX* 编辑器

使用 `lyx` 命令启动 *LyX* *LaTeX* 编辑器。*LyX* 附带大量支持文档。单击 Help（帮助）以选择 Tutorial（教程）、User's Guide（用户指南）或其他信息。

要开始您的第一个文档，我建议您选择 *LyX* 提供的模板之一。模板位于 `/usr/share/lyx/templates`。要打开模板，请单击 File（文件）⇒ New from Template（从模板新建）。将出现可用模板列表。例如，您可以使用它们来创建信件、幻灯片和文章。

除了提供剪切、复制和粘贴等标准编辑功能外，您还可以从 Layout（布局）菜单执行各种标记功能。至于数学功能，Math（数学）菜单允许您将分数、平方根、指数、求和和积分函数插入文档。完成后，您可以：

- 将文件打印到 PostScript 打印机或输出 PostScript (`.ps`) 文件。（单击 File（文件）⇒ Print（打印），选择打印方法，然后单击 OK。）
- 将文件导出为 *LaTeX*、DVI、PostScript 或 ASCII 文本。（单击 File（文件）⇒ Export（导出），然后从文件格式列表中选择。）

*LyX* 称自己为 WYSIWYM 编辑器——What You Say Is What You Mean（所想即所得）。因此，您在编辑时屏幕上看到的内容并不完全是打印文档的样子。例如，多次按 Enter 键不会在行之间显示额外的空白。

因为 *LyX* 支持样式文件，所以它使您能够创建符合多种不同标准的文档。例如，*LyX* 支持使用 article 文本类为美国数学学会 (AMS) 期刊排版。其他支持的文本类包括：

- **article** - 无章节的单面论文。
- **report** - 双面报告，倾向于比文章长。
- **book** - 与 report 相同，但包含额外的前言和后记内容。
- **slides** - 用于制作透明胶片。
- **letter** - 包含地址、签名和其他元素的特殊环境。

### 打印 *LaTeX* 文件

无论您创建自己的 *LaTeX* 文件，从 *LyX* *LaTeX* 编辑器导出一个，还是从互联网下载一个，都有多种实用程序可用于格式化、打印或显示输出。以下是您的一些选择：

- 要格式化 *LaTeX* 文件 (`filename.tex`)，请运行以下命令：

```
$ latex filename.tex
```

- 要打印 .dvi 文件 (filename.dvi)，将其发送到默认的 PostScript 打印机，并输入以下内容：

```shell
$ dvips filename.dvi
```

- 要在 X 窗口中显示 .dvi 文件，请输入以下内容：

```shell
$ xdvi filename.dvi
```

- 要将 .dvi 文件打印到 PCL 打印机（如 HP LaserJet），请输入以下内容：

```shell
$ dvicopy filename.dvi
$ dvilj filename.dvi
```

- dvilj 命令不直接支持虚拟字体。dvicopy 命令转换字体，以便 PCL 打印机可以处理它们。

### 转换文档

文档可能以许多不同的格式呈现给您。只需搜索互联网上的一些 Linux FTP 站点，您就会发现 PostScript、DVI、man、PDF、HTML 和 TeX 格式的文件。还有各种图形格式。Red Hat Linux 自带大量实用程序，用于将文档和图形从一种格式转换为另一种格式。以下是文档和图形转换实用程序的列表：

- **dos2unix** — 将 DOS 文本文件转换为 UNIX (Linux) 文本文件。
- **fax2ps** — 将 TIFF 传真图像文件转换为压缩的 PostScript 格式。PostScript 输出经过优化，可发送到低速线路上的打印机。对于包含大量黑色或连续色调的图像，此格式效率较低。（在这些情况下，tiff2ps 可能更有效。）
- **fax2tiff** — 将传真数据（第 3 组或第 4 组）转换为 TIFF 格式。输出为低分辨率或中分辨率 TIFF 格式。
- **g32pbm** — 将第 3 组传真文件（digifax 或 raw 格式）转换为可移植位图。
- **gif2tiff** — 将 GIF (87) 文件转换为 TIFF 格式。
- **man2html** — 将手册页转换为 HTML 格式。
- **pal2rgb** — 将 TIFF 图像（调色板颜色）转换为全彩 RGB 图像。
- **pbm2g3** — 将可移植位图图像转换为传真文件（第 3 组）。
- **pdf2dsc** — 将 PDF 文件转换为 PostScript 文档 dsc 文件。PostScript 文件符合 Adobe 文档结构约定 (DSC)。输出使 PostScript 阅读器（如 Ghostview）能够逐页读取 PDF 文件。
- **pdf2ps** — 将 PDF 文件转换为 PostScript 文件（第 2 级）。
- **pfb2pfa** — 将 Type 1 PostScript 字体（二进制 MS-DOS）转换为 ASCII 可读格式。
- **pk2bm** — 将 TeX pkfont 字体文件转换为位图（ASCII 文件）。
- **ppm2tiff** — 将 PPM 图像文件转换为 TIFF 格式。
- **ps2ascii** — 将 PostScript 或 PDF 文件转换为 ASCII 文本。
- **ps2epsi** — 将 PostScript 文件转换为封装 PostScript (EPSI)。某些文字处理和图形程序可以读取 EPSI。输出质量通常较低。
- **ps2pdf** — 将 PostScript 文件转换为便携式文档格式 (PDF)。
- **ps2pk** — 将 Type 1 PostScript 字体转换为 TeX pkfont。
- **pstopext** — 将 PostScript 文件转换为 ASCII 文本。pstopext 类似于 ps2ascii，但比 ps2ascii 更好地处理字体编码和字距调整。pstopext 不转换 PDF。
- **ras2tiff** — 将 Sun 光栅文件转换为 TIFF 格式。
- **texi2html** — 将 Texinfo 文件转换为 HTML。
- **tiff2bw** — 将 RGB 或调色板颜色 TIFF 图像转换为灰度 TIFF 图像。
- **tiff2ps** — 将 TIFF 图像转换为 PostScript。
- **unix2dos** — 将 UNIX (Linux) 文本文件转换为 DOS 文本文件。

除了这些工具，许多图形应用程序（如 The GIMP）也允许您使用“另存为”功能将图像保存为多种不同格式（BMP、JPEG、PNG、TIFF 等）。

## 创建 DocBook 文档

文档项目通常需要生成以多种格式输出的文档。例如，描述如何使用软件程序的相同文本可能需要输出为印刷手册、HTML 页面和 PostScript 文件。Linux 社区最近最广泛采用的用于创建所谓结构化文档的标准是 SGML、XML 和 DocBook。

### 理解 SGML 和 XML

标准通用标记语言 (SGML) 的创建是为了提供一种标准的文本标记方式，以便稍后能以多种格式输出。因为 SGML 标记是用文本标签完成的，所以您可以使用任何纯文本编辑器创建 SGML 文档。文档由文档的文本和标识文本中每种信息类型的标签组成。

与 Groff 和 HTML 等标记语言不同，SGML 标记在创建文档时并不旨在强制执行特定的外观。因此，例如，您不会将一段文本标记为粗体或斜体，而是将其标识为地址、段落或名称。稍后，将样式表应用于文档，以获取标记的文本并赋予其外观和呈现方式。

因为 SGML 包含许多标签，为了简化基于 SGML 生成文档，其他项目应运而生，以更好地聚焦 SGML 的使用方式。特别是

