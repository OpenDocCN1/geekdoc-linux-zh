

注意：可以从 Fedora 软件源中获取 LyX 编辑器；你可以通过输入 `yum install lyx` 来安装它。

如果你想在常规文本编辑器中编辑 LaTeX，你需要熟悉 LaTeX 命令。要获取完整的 LaTeX 命令列表，请输入 `info latex`，然后前往“LaTeX 文档中的命令”部分。

![](img/fb202c163797a743c3c6cf236316bc96_304_0.png)

## 使用 LyX LaTeX 编辑器

使用 `lyx` 命令启动 LyX LaTeX 编辑器。LyX 附带了大量支持文档。点击“帮助”可以选择教程、用户指南或其他信息。

对于你的第一份文档，我建议你选择 LyX 提供的一个模板。模板位于 `/usr/share/lyx/templates`。要打开模板，点击“文件” → “从模板新建”。此时会显示可用模板列表。例如，你可以使用它们创建信件、幻灯片和文章。

除了提供标准的编辑功能（如剪切、复制和粘贴）外，你还可以从“布局”菜单执行各种标记功能。至于数学功能，“数学”菜单允许你在文档中插入分数、平方根、指数、求和和积分函数。完成后，你可以：

-   将文件打印到 PostScript 打印机或输出 PostScript (.ps) 文件。（选择“文件” → “打印”，选择打印方法，然后点击“确定”。）
-   将文件导出为 LaTeX、DVI、PostScript 或 ASCII 文本。（选择“文件” → “导出”，并从文件格式列表中选择。LyX 直接将文件导出到你的主目录，而不让你选择保存位置。）

LyX 称自己为 WYSIWYM 编辑器——所见即所意。因此，你在编辑时在屏幕上看到的内容并不完全等同于打印文档的外观。例如，多次按下 Enter 键不会在行之间产生额外的空白。

由于 LyX 支持样式文件，它使你可以创建符合多种不同标准的文档。例如，LyX 支持使用 article 文本类为美国数学学会（AMS）期刊进行排版。其他受支持的文本类包括：

-   **article** — 单面打印，无章节的纸张。
-   **report** — 双面报告，通常比文章更长。
-   **book** — 与 report 相同，但包含额外的前置和后置内容。
-   **slides** — 用于制作透明胶片。
-   **letter** — 包含地址、签名和其他元素的环境。

## 打印 LaTeX 文件

无论你自己创建 LaTeX 文件、从 LyX LaTeX 编辑器导出，还是从互联网下载，都有几种实用程序可用于格式化、打印或显示输出。以下是一些选择：

-   要格式化 LaTeX 文件（filename.tex），请运行以下命令：
    ```
    $ latex filename.tex
    ```
-   要打印 DVI 文件（filename.dvi），将其发送到你的默认 PostScript 打印机，并输入以下内容：
    ```
    $ dvips filename.dvi
    ```
-   要在 X 窗口中显示 DVI 文件，请输入以下内容（安装 tetex-xdvi 软件包后）：
    ```
    $ xdvi filename.dvi
    ```

如果你更喜欢将 LaTeX 文件输出为 PDF 格式，可以尝试 dvipdf 命令。

## 转换文档

文档可能以许多不同的格式出现。只需在互联网上搜索一些 Linux FTP 站点，你会发现 PostScript、DVI、man、PDF、HTML 和 TeX 格式的文件。还有各种图形格式。Fedora 和 RHEL 附带了许多用于将文档和图形从一种格式转换为另一种格式的实用程序。以下是文档和图形转换实用程序的列表：

-   **dos2unix** — 将 DOS 文本文件转换为 UNIX（Linux）文本文件。你可能希望使用此命令的一个原因是，DOS 文本文件包含双字符回车符，而 Linux（UNIX）文本文件使用单字符换行符。
-   **fax2ps** — 将 TIFF 传真图像文件转换为压缩的 PostScript 格式。PostScript 输出针对通过低速线路发送至打印机进行了优化。对于包含大量黑色或连续色调的图像，此格式效率较低。（在这种情况下，*tiff2ps* 可能更有效。）
-   **fax2tiff** — 将传真数据（Group 3 或 Group 4）转换为 TIFF 格式。输出为低分辨率或中等分辨率的 TIFF 格式。
-   **gif2tiff** — 将 GIF (87) 文件转换为 TIFF 格式。
-   **man2html** — 将 man 页转换为 HTML 格式。
-   **pal2rgb** — 将 TIFF 图像（调色板颜色）转换为全彩 RGB 图像。
-   **pdf2dsc** — 将 PDF 文件转换为 PostScript 文档 DSC 文件。该 PostScript 文件符合 Adobe 文档结构约定（DSC）。输出使 PostScript 阅读器（如 Ghostview）能够逐页读取 PDF 文件。
-   **pdf2ps** — 将 PDF 文件转换为 PostScript 文件（level 2）。
-   **pb2pfa** — 将 Type 1 PostScript 字体（二进制 MS-DOS）转换为 ASCII 可读格式。
-   **pk2bm** — 将 TeX pkfont 字体文件转换为位图（ASCII 文件）。
-   **ppm2tiff** — 将 PPM 图像文件转换为 TIFF 格式。
-   **ps2ascii** — 将 PostScript 或 PDF 文件转换为 ASCII 文本。
-   **ps2epsi** — 将 PostScript 文件转换为封装式 PostScript（EPSI）。某些文字处理和图形程序可以读取 EPSI。输出质量通常较低。
-   **ps2pdf** — 将 PostScript 文件转换为便携式文档格式（PDF）。
-   **ps2pk** — 将 Type 1 PostScript 字体文件转换为 TeX pkfont。
-   **ras2tiff** — 将 Sun 光栅文件转换为 TIFF 格式。
-   **tiff2bw** — 将 RGB 或调色板颜色 TIFF 图像转换为灰度 TIFF 图像。
-   **tiff2ps** — 将 TIFF 图像转换为 PostScript。
-   **unix2dos** — 将 UNIX（Linux）文本文件转换为 DOS 文本文件。

除了这些工具外，许多图形应用程序（如 The GIMP）允许你使用“另存为”功能将图像保存为几种不同的格式（BMP、JPEG、PNG、TIFF 等）。

## 创建 DocBook 文档

文档项目通常需要生成以多种格式输出的文档。例如，描述如何使用某软件程序的相同文本可能需要输出为纸质手册、HTML 页面和 PostScript 文件。Linux 社区最近采用的用于创建所谓的结构化文档的标准是 SGML、XML 和 DocBook。

## 理解 SGML 和 XML

标准通用标记语言（SGML）旨在提供一种标准的文本标记方式，以便后来可以以多种格式输出。由于 SGML 标记是通过文本标签完成的，你可以使用任何纯文本编辑器创建 SGML 文档。文档由你的文档文本和标识文本中每种信息类型的标签组成。

与 Groff 和 HTML 等标记语言不同，SGML 标记并不旨在在创建文档时强制特定的外观。因此，例如，你不会将一段文本标记为 **粗体** 或 *斜体*，而是将其识别为地址、段落或名称。稍后，样式表将应用于文档，以获取带有标签的文本并分配外观和呈现。

由于 SGML 包含许多标签，为了简化基于 SGML 的文档生成，出现了其他项目以更好地聚焦 SGML 的使用方式。特别是，可扩展标记语言（XML）的创建是为了提供一个可管理的 SGML 子集，专门针对基于 Web 的出版进行定制。

在描述 SGML 和 XML 时，到目前为止我只提到了用于生成结构化文档的框架。具体的文档项目需要创建并在一定程度上强制实施其所需文档类型的特定标记定义。这些定义被称为数据类型定义（DTDs）。对于 Linux 本身和其他开源项目的文档，DocBook 已成为首选的 DTD。

### 理解 DocBook

DocBook 是一种非常适合以多种格式生成计算机软件文档的 DTD。它最初由 OASIS 联盟（www.oasis-open.org/docbook）创建，现在得到了许多不同的商业和开源工具的支持。

> **交叉引用：**你可以在 www.docbook.org 找到 DocBook 的官方文档。

DocBook 的重点在于标记内容，而不是指示特定的外观（即，字体类型、大小、位置等）。它包含允许你自动创建索引、图表列表和目录等过程的标记。Fedora 和 RHEL 中的工具使你能够将 DocBook 文档输出为 HTML、PDF、DVI、PostScript、RTF 和其他格式。

DocBook 对 Linux 社区很重要，因为许多开源项目正在使用 DocBook 来生成文档。例如，以下是使用 DocBook 创建描述其软件的文档的组织及相关网站列表：

