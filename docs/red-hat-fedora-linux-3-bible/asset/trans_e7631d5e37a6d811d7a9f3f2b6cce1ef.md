

# 打印 LaTeX 文件

由于 LyX 支持样式文件，因此它允许你创建符合多种不同标准的文档。例如，LyX 支持使用 article 文本类为美国数学会（AMS）期刊进行排版。其他受支持的文本类包括：

- **article** — 单面文档，无章节。
- **report** — 双面报告，通常比文章更长。
- **book** — 与 report 相同，但包含额外的前置和后置内容。
- **slides** — 用于制作透明胶片。
- **letter** — 包含用于地址、签名及其他元素的特殊环境。

无论是你自己创建 LaTeX 文件，从 LyX LaTeX 编辑器导出，还是从互联网下载，都有许多实用工具可用于格式化、打印或显示输出。以下是你的一些选择：

- 要格式化 LaTeX 文件（`filename.tex`），请运行以下命令：
  ```text
  $ latex filename.tex
  ```
- 要打印 DVI 文件（`filename.dvi`），请将其发送到你的默认 PostScript 打印机，并输入以下内容：
  ```text
  $ dvips filename.dvi
  ```
- 要在 X 窗口中显示 DVI 文件，请输入以下内容：
  ```text
  $ xdvi filename.dvi
  ```
- 要将 DVI 文件打印到 PCL 打印机（例如 HP LaserJet），请输入以下内容：
  ```text
  $ dvicopy filename.dvi
  $ dvilj filename.dvi
  ```
- `dvilj` 命令不直接支持虚拟字体。`dvicopy` 命令会转换字体，以便 PCL 打印机可以处理它们。

# 转换文档

文档可以通过多种不同的格式到达你手中。仅搜索互联网上的一些 Linux FTP 站点，你就会找到 PostScript、DVI、man、PDF、HTML 和 TeX 格式的文件。还有各种图形格式。Fedora 附带了许多用于将文档和图形从一种格式转换为另一种格式的工具。以下是文档和图形转换工具列表：

- **dos2unix** — 将 DOS 文本文件转换为 UNIX（Linux）文本文件。
- **fax2ps** — 将 TIFF 传真图像文件转换为压缩的 PostScript 格式。PostScript 输出针对通过低速线路发送至打印机进行了优化。对于包含大量黑色或连续色调的图像，这种格式效率较低。（在这种情况下，tiff2ps 可能更有效。）
- **fax2tiff** — 将传真数据（Group 3 或 Group 4）转换为 TIFF 格式。输出为低分辨率或中分辨率 TIFF 格式。
- **g32pbm** — 将 Group 3 传真文件（difax 或 raw 格式）转换为便携式位图。
- **gif2tiff** — 将 GIF（87）文件转换为 TIFF 格式。
- **man2html** — 将 man 手册页转换为 HTML 格式。
- **pal2rgb** — 将 TIFF 图像（调色板颜色）转换为全彩 RGB 图像。
- **pbm2g3** — 将便携式位图图像转换为传真文件（Group 3）。
- **pdf2dsc** — 将 PDF 文件转换为 PostScript 文档 dsc 文件。该 PostScript 文件符合 Adobe 文档结构约定（DSC）。输出允许 PostScript 阅读器（如 Ghostview）逐页读取 PDF 文件。
- **pdf2ps** — 将 PDF 文件转换为 PostScript 文件（level 2）。
- **pfb2fa** — 将 Type 1 PostScript 字体（二进制 MS-DOS）转换为 ASCII 可读格式。
- **pk2bm** — 将 TeX pkfont 字体文件转换为位图（ASCII 文件）。
- **ppm2tiff** — 将 PPM 图像文件转换为 TIFF 格式。
- **ps2ascii** — 将 PostScript 或 PDF 文件转换为 ASCII 文本。
- **ps2epsj** — 将 PostScript 文件转换为封装 PostScript（EPSI）。某些文字处理和图形程序可以读取 EPSI。输出通常质量较低。
- **ps2pdf** — 将 PostScript 文件转换为可移植文档格式（PDF）。
- **ps2pk** — 将 Type 1 PostScript 字体转换为 TeX pkfont。
- **pstotext** — 将 PostScript 文件转换为 ASCII 文本。pstotext 类似于 ps2ascii，但在处理字体编码和字距调整方面比 ps2ascii 更好。pstotext 不转换 PDF。
- **ras2tiff** — 将 Sun 光栅文件转换为 TIFF 格式。
- **texi2html** — 将 Texinfo 文件转换为 HTML。
- **tiff2bw** — 将 RGB 或调色板颜色的 TIFF 图像转换为灰度 TIFF 图像。
- **tiff2ps** — 将 TIFF 图像转换为 PostScript。
- **unix2dos** — 将 UNIX（Linux）文本文件转换为 DOS 文本文件。

除了这些工具外，许多图形应用程序（如 The GIMP）允许你使用“另存为”功能将图像保存为几种不同的格式（BMP、JPEG、PNG、TIFF 等）。

# 创建 DocBook 文档

文档项目通常需要生成以多种格式输出的文档。例如，描述如何使用软件程序的相同文本可能需要输出为印刷手册、HTML 页面和 PostScript 文件。Linux 社区最近采用的用于创建所谓的*结构化文档*的标准是 SGML、XML 和 DocBook。

## 理解 SGML 和 XML

标准通用标记语言（SGML）的创建是为了提供一种标准方式来标记文本，以便稍后以多种格式输出。由于 SGML 标记是使用文本标签进行的，因此你可以使用任何纯文本编辑器创建 SGML 文档。文档由文档的文本和标识文本中每种信息类型的标签组成。

与 Groff 和 HTML 等标记语言不同，SGML 标记并不意在强制你在创建文档时采用特定的外观。因此，例如，与其将某段文本标记为*粗体*或*斜体*，你应将其标识为地址、段落或名称。稍后，样式表将应用于文档，以提取带有标签的文本并分配外观和展示方式。

由于 SGML 包含许多标签，为了简化基于 SGML 的文档生成，其他项目应运而生，以更集中地关注 SGML 的使用方式。特别是，可扩展标记语言（XML）的创建旨在提供一个可管理的 SGML 子集，该子集专门针对网络发布进行定制，以使其运行良好。

到目前为止，在描述 SGML 和 XML 时，我仅提到了用于生成结构化文档的框架。具体的文档项目需要创建并（在一定程度上）强制执行其需要生成的文档类型的具体标记定义。这些定义被称为数据类型定义（DTDs）。对于 Linux 本身和其他开源项目的文档，DocBook 已成为首选的 DTD。

## 理解 DocBook

DocBook 是一个非常适合以多种格式生成计算机软件文档的 DTD。它最初由 OASIS 联盟（www.oasis-open.org）创建，现在受到许多不同的商业和开源工具的支持。

DocBook 的重点在于标记内容，而不是指示特定的外观（即字体类型、大小、位置等）。它包含标记，允许你自动化创建索引、图表列表和目录等过程。Fedora 中的工具允许你将 DocBook 文档输出为 HTML、PDF、DVI、PostScript、RTF 和其他格式。

DocBook 对 Linux 社区很重要，因为许多开源项目正在使用 DocBook 来制作文档。例如，以下是一个使用 DocBook 创建描述其软件的文档的组织及相关网站列表：

- Linux 文档项目（www.tldp.org/LDP/LDP-Author-Guide）
- GNOME 文档（developer.gnome.org/projects/gdp/handbook/gdp-handbook）
- KDE 文档项目（www.kde.org/documentation）
- FreeBSD 文档项目（www.freebsd.org/docproj）

如果你想为上述任何文档项目做出贡献，请参考每个组织的网站。在所有情况下，它们都会发布作者指南或风格指南，描述其写作工作所支持的 DocBook 标签。

# 创建 DocBook 文档

你可以在任何文本编辑器中创建文档，使用外观类似于 HTML 标签的标签（开始和结束标签出现在小于号和大于号之间）。还有文字处理程序允许你创建 DocBook 标记。

以下程序包含一个使用纯文本编辑器生成并输出为 HTML 的简单 DocBook 文档示例，使用了随 Fedora 附带工具。

1. 在你的主目录中创建一个目录用于工作并进入该目录。例如，你可以从终端窗口输入以下内容：
   ```text
   $ mkdir $HOME/doctest
   $ cd $HOME/doctest
   ```
2. 打开一个文本编辑器来容纳你的 DocBook 文档。例如，你可以输入：
   ```text
   $ gedit cardoc.sgml
   ```
   （jedit 等文本编辑器，你可以从 www.jedit.org 获取，对于处理 docbook 中使用的长标签名称也很有用。）
3. 输入你希望出现在文档中的标签和文本。大多数 DocBook 文档要么是 <book> 类型（大型、多章节文档），要么是 <article> 类型（单章节文档）。为了尝试 DocBook 文档，输入以下内容：

   ```xml
   <xml version='1.0'>
   <article>
   <title>Choosing a new car</title>
   <header>
   <abstract>
   In this article, you will learn how to price,
   negotiate for, and purchase an automobile..
   </abstract>
   </header>
   <section>
   <title>Getting Started</title>
   <para>
   ```

