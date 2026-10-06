

# 第 6 章：使用 Fedora 和 RHEL 进行发布

使用 AbiWord，你可以选择文件包含的文档类型。你可以选择以以下格式保存文件：

- AbiWord、AbiWord 模板以及 压缩的 AbiWord (.abw, .awt, .zab)
- HTML/XHTML (.html)
- KWord (.kwd)
- 多部分 HTML (.mht)
- 富文本格式 (.rtf)
- Microsoft Word (.doc)
- OpenDocument 格式（或 ODF），这是一种新兴的办公文档标准。
- PalmDoc (.pdb)
- 便携式文档格式 (.pdf)
- UNIX nroff/man 格式 (.nroff)
- UTF8 (.utf8)
- Word 格式 (.wp) 需要额外的插件
- 文本 (.txt)

AbiWord 并不能非常完美地导入所有这些文件类型。虽然最新版本的 AbiWord 支持支持样式，但有时表格、图形和其他功能并无法完美转换。如果你想在 AbiWord 中处理 Word 文档，请将其作为 AbiWord 文档打开。虽然 AbiWord 在过去的几个版本中有所改进，但如果你需要与使用 Word 的他人交换文件，仍然可能会遇到问题。（为了保持 Word 格式，OpenOffice.org 和 StarOffice 的效果好得多，但并非完美。）

如果你的硬件配置较慢，AbiWord 的性能优于 OpenOffice.org Writer。如果你在跨平台环境中工作，可以获得适用于 Windows、Mac OS X、QNX 以及许多 UNIX 派生系统（Linux、BSD 等）的 AbiWord 版本。

最近添加的功能（如样式和项目）继续使 AbiWord 成为一个实用的文字处理工具。它与商业产品相比没有竞争力，但其开发者持续对其进行改进。

# 使用 KOffice

KOffice 软件包包含了一组为 KDE 桌面设计的办公效率应用程序。安装 `kofficesuite` 软件包将引入你使用 KOffice 需要的大部分软件。它包含一个文字处理器 (KWord)、电子表格 (KSpread)、演示文创建器 (KPresenter) 和图表绘制程序 (KChart)。这些应用程序可以单独运行，也可以在 KOffice 工作空间内运行。koffice 工作空间位于本书附带的 DVD 上。你可以通过 KOffice 网站 http://www.koffice.org 了解更多信息。

使用命令 `install koffice-suite` 安装 KOffice 套件。当你使用 KOffice 时，可以从左列选择不同的办公应用程序。在任何应用程序中打开多个文档。然后点击左列的“文档 (Documents)”来选择当前显示哪一个。

图 6-2 KWord 绘制 Word 文档。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_301_0.png)

图 6-2：你可以在 KWord 中处理 Word 文档。

你可以处理各种文档、电子表格和图像类型；但尚未支持许多商业文档类型。你可能需要使用其他工具导入文档以便将其导入 KWord。然而，KSpread 程序可以打开几种样式格式，例如 Microsoft Excel 和 Gnumeric 电子表格。Kivio 是一个实用的图表工具。

# TextMaker

TextMaker 是 Linux 上另一个流行的商业文字处理程序包（http://www.softmaker.com/english/tml_en.htm）。此文字处理器占用的内存比 OpenOffice Writer 少得多，但仍然包含许多强大的功能。使用 TextMaker 在不同操作系统之间交换文档非常容易，因为还有适用于 Windows、Pocket PCs、Handheld PCs、FreeBSD 和 Zaurus 的 TextMaker 版本。

# 使用传统的 Linux 发布工具

Linux 的第一个文档和图形工具大部分基于旧的基于文本的工具构建的。尽管年代久远，但许多旧的发布工具（如 Groff 和 LaTeX）仍被技术社区的人们使用。使用这些老派工具处理器，你可以在写作时忽略文档的外观。纯文本宏指示后处理器在写作完成后对文档进行排版布局以供打印。而使用文字处理器时（如 OpenOffice.org Word 和 StarOffice Writer），你可以在写作时对文本进行标记并设置文档的基本版式。

传统 Linux 发布工具的某些属性使其特别适用于某些特定类型的文档发布。Groff 和 LaTeX（基于 TeX）多年以来在 Fedora 和 RHEL 的技术人员中一直非常受欢迎。原因如下：

- 你可以操作纯文本文件。使用像 `sed` 和 `grep`这样的工具，你可以通过一个命令或脚本更改一个或几百个文档。
- 支持科学计数法。通过 `eqn`，你可以创建复杂的方程。LaTeX 和 TeX 适用于技术符号。某些数学出版物需要 LaTeX。
- 编辑速度可能更快，因为传统的 Linux 文档是用文本编辑器创建的。你通常可以获得比文字处理器更好的文本编辑器性能。

简单的页面布局与 Linux 文档工具配合良好。例如，一本带有少量图表和图片的技术书籍可以使用 Groff 或 TeX 文档工具轻松地制作和维护。信和备忘录使用这些工具也很容易。当然，Linux man 页是用基于文本的工具创建的。

此外，Linux 喜欢 PostScript。大多数 Linux 文档处理软件都包含 PostScript 的打印驱动程序。有很多工具可以将 PostScript 转换为其他格式。此外，网络上的某些文档以 PostScript (.ps) 格式发布。

传统 Linux 发布工具的缺点在于它们不直观。如果你习惯了带有 GUI 的文字处理器，可能会发现这些工具很难用。通常情况下，Groff 用于创建 man 页。如果你需要生成数学文档（例如为了发表技术期刊），LaTeX 则很有用。注意：多年来，AT&T 分发的文档是用 troff/nroff 创建的，这些是 man 页的宏。今天，Fedora 和 RHEL 包含了相同的 Groff 创建 man 页的工具。

# 在 Groff 或 LaTeX 中创建文档

你可以使用任何文本编辑器在 Groff 或 LaTeX 中创建文档。Fedora 和 RHEL 带有几种文本编辑器，或者你可以从互联网下载它们。

在 Groff 或 LaTeX 中创建文档的过程包括以下通用步骤：

1. 使用任何文本编辑器创建文档。文档将包含文本和标记。
2. 使用与你创建的文档样式匹配的格式命令对文档进行格式化（例如使用 groff 或 latex）。在此步骤中，你可能需要指示文档包含特殊内容，例如方程 (eqn)、表格 (tbl) 或线条图 (pic)。
3. 将文档发送到带有 GUI 的输出处理器。该设备可以是打印机或显示程序。

# 使用 Groff 进行文本处理

nroff 和 troff 格式命令是 UNIX 系统产生排版输出的第一个接口。它们不是编辑器；相反，它们是你发送给 troff 的命令，结果是格式化的：

- nroff 产生格式化的纯文本，并包含分页、缩进和文本对齐等功能。
- troff 产生排版文本，除了包含 nroff 可以实现的所有功能外，还具有产生不同字体和间距的能力。troff 命令还支持字间距。

groff 命令是产生 nroff/troff 文档的前端。由于 Linux man 页是用 Groff 格式化并输出的，这里的许多示例可以帮助你使用 Groff 创建打印 man 页。

人们很少使用 nroff/troff 标记。相反，有一些常用的宏包可以简化 nroff/troff 格式文档的创建：

- man 宏用于创建 Linux man 页。你可以使用 groff 命令的 -man 选项来格式化 man 页。
- mm 宏（备忘录宏）被用于生成备忘录、信件和技术白皮书。该宏包包含了创建目录、插图列表、引用以及其他有助于制作技术文档的功能。你可以使用 groff 的 -mm 选项来格式化 mm 文档。

