
虚拟机管理器将会出现。

3. **创建新客机** — 右键点击 localhost (qemu) 并点击“新建”。当“创建新虚拟系统”弹出框出现时，点击“下一步”。你会被要求制作虚拟系统。

4. **虚拟机** — 输入一个代表此虚拟机的名称并点击“下一步”。保持名称简单（一个单词、较短且无特殊字符），因为该名称用于在文件名和菜单中表示虚拟机。你会被要求虚拟化方法。

5. **虚拟化方法** — 选择“完全虚拟化”。你也可以选择创建一个使用不同 CPU 架构（i686, X86_64, ppc, sparc, mipsels）的客机。你会被要求安装媒体的位置。

6. **安装媒体** — 输入 ISO 镜像类型（你可以浏览查找）或插入有安装媒体的 CD 或 DVD（例如 Fedora DVD）。同时识别你正在安装的操作系统的类型（通用、Linux、UNIX、Windows 或其他）和变体（例如 Fedora、Windows、Sun Solaris）。你会被分配存储空间。

7. **分配存储空间** — 你可以通过识别名称和大小来识别磁盘分区或创建虚拟磁盘。在任何情况下，存储区域必须足够大以容纳已安装的客机操作系统。你会被要求网络连接。

8. **主机网络** — 识别虚拟或共享物理网络设备，为你的客机操作系统提供连接。接下来分配内存和 CPU。

9. **分配内存** — 从屏幕上的总内存中，选择虚拟机使用的数量和最大数量。建议至少使用 256MB。还应要启动的 CPU 数量（通常少于主机系统）。你会被要求检查你的安装信息。

10. **开始安装** — 如果所有信息正确，点击“完成”开始该过程。此时，你将按照所选操作系统的正常程序运行安装过程。一旦安装完成，你就可以从虚拟机管理器中启动和关闭新的虚拟环境。

### 总结

在为 Linux 和其他 UNIX 系统编写的应用程序、移植到 Linux 的应用程序以及在仿真中运行的应用程序之间，有数以千计的应用程序可供选择。随着 Fedora Core 和 Fedora Extras 在线存储库的合并，在 Fedora 和 RHEL 上运行的高质量软件数量指数级增长。为了简化安装和管理 Linux 应用程序的过程，使用了红帽软件包管理（RPM）格式。通过为 RPM 开发的工具（如 `yum` 命令），你可以轻松地安装、删除和查询 Linux 软件包。在 DOS、Windows 95/98/2000/NT/XP/Vista 和 Macintosh 上运行的应用程序类型在 Linux 中使用时提供了最高级别的兼容性。从远来看，像 Xen 和 KVM 这样的虚拟化软件允许多个操作系统作为客机在 Fedora 上运行。

## 第 6 章：使用 Fedora 和 RHEL 发布

本章内容

- Linux 中的桌面出版
- 尝试图形文本编辑器
- 使用 OpenOffice.org
- 使用 Groff 和 LaTeX 创建文档
- 创建 DocBook 文档
- 使用 Ghostscript 和 Acrobat 显示文档
- 使用 Libre 进行页面布局
- 图形处理
- 使用 SANE 驱动的扫描仪
- 在 Web 上发布

作为一个桌面系统，操作系统必须能够很好地执行至少一项任务：生成文档。Fedora 和 RHEL 包含了生成文档、处理图像和打印的工具。本章描述了 OpenOffice 和 KOffice 等 Linux 办公套件，用于创建演示文稿和表格。对于页面布局，Libre 是一个优秀的应用程序，可制作手册和小册。对于图像处理，我们涵盖了 GNU 图像处理程序（GIMP）。对于矢量图形，我们描述了 Inkscape 矢量图形编辑器。为了显示你创建的内容，有多种查看器可以显示 PDF 和 PostScript 格式的输出。对于 PDF，有 Evince 查看器和 Adobe Reader。显示 PostScript 文件，有 Ghostview。

## 第二部分：使用 Fedora 和 RHEL

如果你想在 Web 上发布，有工具可以编写基础 HTML 文档以及使用功能完整的内容系统制作网站。为 Linux 打包以管理你网站的软件包括 MediaWiki（维基）、WordPress（博客）、Drupal（内容管理）和 Gallery（照片）。

## Linux 中的桌面出版

无论你是写信、备忘录还是书籍，通常都从文字处理器开始。如果你的计算机性能不高，你可能会从简单的文本编辑器或如 AbiWord 的文字处理器开始。然而，大多数 Linux 用户从 OpenOffice Writer 开始。不过，如果你只需要编辑纯文本文档，可以从简单的文本编辑器开始。

## 使用文本编辑器和记事本

在跳转更多文字处理器之前，如果你想快速编写一些文本，这里有一些你可以尝试的应用程序：

- **GNOME 文本编辑器 (gedit)** — 从 GNOME 桌面，选择应用程序 -> 辅助 -> 文本编辑器。在打开的窗口中，你可以输入、复制、粘贴并使用箭头移动。除了创建文本文档，edit 还有拼写检查和搜索工具。高亮模式（选择视图 -> 高亮模式）会导致你编写的文本的不同部分（如 C 或 Java 代码，或 HTML 或 XML 标记）以不同的颜色显示。
- **KDE 文本编辑器 (kwrite)** — 从 KDE 桌面，KWrite 应用是默认的文本编辑器。KWrite 包含了许多文本编辑功能，还具有多语言输入的支持。
- **便签笔记 (tomboy)** — 不同的笔记应用 KNotes（用于 KDE）和 Tomboy（用于 GNOME）。Tomboy 在你的顶栏放置一个笔记本，你可以从中创建和管理笔记。创建一个包含 URL（点击在浏览器中打开）和其他笔记链接的新笔记。输入时会检查拼写。将笔记组织在笔记本中或进行关键字搜索以查找所需的笔记。

如果你想将文本从纯文本文件或便签移动到更正式的文档中，你可以将其复制或剪接到下一节描述的文字处理器之一。

## 使用文字处理器

OpenOffice.org 是一个作为 Fedora 和 RHEL 发行版一部分提供的强大的开源办公套件。基于 Sun Microsystems StarOffice 产品套件，OpenOffice 包含了文字处理器、电子表格、演示管理器和其他个人生产力工具。在许多情况下，OpenOffice.org 可以作为无缝替换

# 第 6 章：使用 Fedora 和 RHEL 进行发布

对于 Microsoft Office，其优势在于功能以及支持 Word、Excel、PowerPoint 等其他 Microsoft 格式的能力。

Linux 系统可用的其他文字处理应用程序还包括几个开源产品，如 AbiWord 和 KOffice。商业办公套件包括 StarOffice，它不仅包含一个文字处理器，还包含用于创建和处理电子表格以及其他面向办公的内容。

## 使用 OpenOffice.org

有些人称 OpenOffice.org 是对微软在桌面市场占据主导地位的重大威胁。如果你需要处理 Word 格式的文档，并且你正在使用 Linux 作为你的桌面电脑，那么 OpenOffice.org 是消除这一障碍的一大步。

> 注意：如果你愿意支付几美元，来自 Codewavers 的 CrossOffice 允许你从 Linux 桌面在系统中安装并运行不同版本的 Microsoft Office（97, 2000, XP, 2003）。更多信息请参阅第 5 章或访问 http://www.codewavers.com/products/cxoffice。

Fedora 和 RHEL 包含了整个 OpenOffice.org 桌面应用程序套件。此发行版本的 Fedora 包含了最新的 OpenOffice.org 版本 (3.0)。基于 StarOffice 的源代码，OpenOffice.org 包含以下办公效率应用程序：

- **OpenOffice.org Writer** — 一种绘图应用程序，可以处理 Microsoft Word、StarOffice 以及其他几种文件格式的文档。Writer 还具有全套功能，用于使用模板、处理字体、导航文档（包括图像和效果）以及生成目录。
- **OpenOffice.org Calc** — 一种电子表格应用程序，允许你整合来自 Microsoft Excel、StarOffice、Dbase 以及其他几种电子表格格式的数据。Calc 中的某些功能允许你创建图表、设置数据库范围（轻松地对电子表格区域的数据进行排序），并使用数据工具从不同视角对齐数据。
- **OpenOffice.org Draw** — 一种绘图应用程序，允许你创建、编辑和对齐对象；包含纹理和颜色；并处理对象层。它允许你将图像、矢量图形、AutoCAD 以及各种其他文件格式整合到你的绘图中。然后，你可以以 OpenOffice Drawing 或 StarOffice Draw 格式保存绘图。
- **OpenOffice.org Math** — 一个计算程序，允许你创建数学公式。
- **OpenOffice.org Impress** — 一种演示应用程序，包含多种幻灯片效果。使用 Impress，你可以创建并保存 Microsoft PowerPoint、Draw 和 Impress 格式的演示文。

# 第二部分：Fedora — RHEL

- *OpenOffice.Base* — 一个低端数据库，类似于微软的 Access 数据库。Base 也可以作为其他数据库的前端。

与其他使用 Microsoft 文档和数据格式创建的应用不同，OpenOffice.org（尽管并不完美）在打开和保存来自许多版本的 Microsoft Word (.doc) 和 Excel (.xls) 格式的文件方面表现得非常好，问题较少。OpenOffice.org 中出现的非常基础的样式和格式通常与它们在 Microsoft Word 中显示的方式没有明显区别。事实上，某些旧的 Word 文档在 OpenOffice.org Writer 中的运行效果实际上比在最新版本的 Microsoft Office 套件中更好。

> 注意：OpenOffice XML (OOXML) 格式是一本达 6000 页的巨著，代表了微软近期声称支持标准文档格式的努力。该格式是 Word 2007 的默认文档类型。然而，开源社区的一些人声称 OOXML 的特殊之处在于要求支持微软产品功能，而没有提供关于如何实现微软专有功能的指导，因此它作为标准是不可用的。换句话说，不要认为微软声称支持的标准就意味着你将来能够在任何平台上都完全使用微软文档。

要打开 OpenOffice.org Writer、Impress、Calc 等其他应用程序，请从“应用程序”菜单点击。然后选择你想要打开的 OpenOffice.org 应用程序。图 6-1 显示了一个使用 Microsoft Word 创建的文件的 OpenOffice.org Writer 示例。

![](img/63c86e1d25a0e2be7e9f6de6b6f02530_297_0.png)

# 第 6 章：使用 Fedora 和 RHEL 进行发布

OpenOffice.org 中的控件与你在 Word 2007 之前在 Word 中找到控件相似。因此，如果你对那些控件熟悉，你应该发现过渡到 OpenOffice.org Writer 是很容易的。事实上，你可能会发现它比使用 Microsoft Word 2007 更容易，因为许多人发现过渡到 Word 2007 是困难的。

OpenOffice.org Writer 中的工具栏包含用于识别文件名以及更改样式、字体和类型的框。按钮允许你保存和打印文件，更改文本对齐，以及剪切、复制和粘贴文本。换句话说，Writer 包含了你在高级文字处理器中预期的所有内容。此外，Writer 还包含一个实用的 PDF 按钮，可以将文件输出为 PDF 格式。这对于交换文档或在互联网上放置数据非常有用。

如果你刚开始使用 OpenOffice.org Writer，这里有几个你可以尝试的功能：

- 使用向导启动信函、传真、议程、演示文、网页、文档转换器或欧元转换器。选择 文件 (File) -> 向导 (Wizards) 并选择你提到的一种文档类型。文档转换向导允许将 Microsoft 或 StarOffice 目录转换为 OpenDocument 格式。欧元转换器允许将不同欧洲货币的文件转换为欧元。
- 文档样式和格式 — 使用字符、段落、框架、页面和编号样式创建你的文档格式（选择 格式 (Format) -> 样式和格式 (Styles and Formatting)）。
- 文档检查 — OpenOffice.org 中包含许多拼写和语法检查（Tools -> Spelling and Grammar）。
- 绘图和图像 — 使用绘图（View -> Drawing）创建矢量图形，插入图像（Insert -> Picture）。
- 输出 PDF — Writer 提供将文件输出为 PDF 格式的工具（Export as PDF）。这对于交换文档或在互联网上放置数据非常有用。

> 注意：有关 OpenOffice.org 的更多信息请访问 http://www.openoffice.org。

# 第二部分：Fedora RHEL

## 使用 Fedora RHEL

### 其他文字处理器

从 Fedora 软件仓库中有许多不同的文字处理器。流行的轻量级文字处理器如 AbiWord 和 KOOffice（ KDE 的一部分）现在可以通过 `yum` 命令轻松安装。至于商业产品，有来自太阳的 StarOffice 和 TextMaker。

## StarOffice

来自太阳的 StarOffice 办公套件（sun.com/staroffice）是运行在 Linux、UNIX 和 Windows 操作系统上的商业产品。StarOffice 包含了文字处理、电子表格、演示图形、电子邮件、新闻、图表和图形应用程序。OpenOffice.org StarOffice 包含了许多与 Microsoft 应用程序兼容的功能，特别是包含了导入 Microsoft Word 和 Excel 文件的能力。

StarOffice 可能是 Linux 上最完整的办公套件。如果你在跨平台环境中，你也可以为 Solaris 和 Microsoft Windows 操作系统获取 StarOffice。StarOffice 包含：

- **StarOffice Writer** — 这是 StarOffice 的文字处理应用程序。你可以从各种格式导入文档，特别是 Word 文档。
- **StarOffice Calc** — 这是随 StarOffice 的程序。你可以从 Microsoft Excel 和其他程序导入电子表格。
- **StarOffice Impress** — 该模块允许你创建演示文。
- **StarOffice Draw** — 这是一个矢量绘图程序。它包含了创建 3D 对象和纹理的能力。
- **StarOffice Base** — 你可以使用 StarBase 管理数据，这是一个数据库数据库的前端。它可以访问各种数据库接口。

StarOffice 中还有其他工具允许你创建业务图形、光栅图像并编辑数学公式（StarOffice Math）。

你可以下载 Linux 版 StarOffice 8，或从 StarWeb 网站 http://www.sun.com/software/star/staroffice/ 购买套装。虽然 StarOffice 曾免费下载，但目前家庭用户下载该软件的价格为 69.99 美元。

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

`groff` 命令是产生 nroff/troff 文档的前端。由于 Linux man 页是用 Groff 格式化并输出的，这里的许多示例可以帮助你使用 Groff 创建打印 man 页。

人们很少使用 nroff/troff 标记。相反，有一些常用的宏包可以简化 nroff/troff 格式文档的创建：

- man 宏用于创建 Linux man 页。你可以使用 `groff` 命令的 `-man` 选项来格式化 man 页。
- mm 宏（备忘录宏）被用于生成备忘录、信件和技术白皮书。该宏包包含了创建目录、插图列表、引用以及其他有助于制作技术文档的功能。你可以使用 `groff` 的 `-mm` 选项来格式化 mm 文档。

## 第 6 章：在 Fedora 和 RHEL 上发布

- `me` 宏在 Berkeley UNIX 系统上用于生成备忘录和技术论文。使用 `-me` `groff` 选项格式化 me 文档。

Groff 宏包存储在 `/usr/share/groff*/tnac`。`man` 宏从 `.tmac` 文件调用，`mm` 宏来自 `.tmac`，`me` 宏来自 `.etmac`。每个宏包的命名约定为 `xxx.tmac`，其中 `xxx` 替换为一个或多个代表宏包的字母。在每情况下，你都可以在后缀文件的开头添加 `an` 来理解它。

> > 提示：与其指定特定的宏包，你可以使用 `-mandoc` 来选择宏包。

当你运行 groff 格式化命令时，可以在命令行上指定你正在使用的宏包。你还可以指定文档通过以下任何一个命令来运行，这些命令会对特定格式的文本进行预处理：

- `eqn` 该处理器格式化在 groff 中生成方程的宏。
- `pic` 该处理器格式化在 groff 中创建简单线条图的宏。
- `tbl` 该处理器格式化在 groff 中生成表格的宏。
- `ps` 为 PostScript 打印机或 PostScript 查看器产生 PostScript 输出。
- `lj4` 为 HP LaserJet 打印机或其他兼容 PCL5 的打印机产生输出。
- `ascii` 可以在终端窗口查看的纯文本输出。
- `dvi` 生成 Tex dvi 输出，输出到后文描述的各种设备。
- `X75` 为 X11 75 点/英寸查看器产生输出。
- `X100` 为 X11 100 点/英寸查看器产生输出。
- `latin1` 使用 ISO Latin-1 字符集产生类打字机输出。

格式化后的 Groff 文档输出到特定设备。该设备可以是打印机、窗口或纯文本。Groff 支持的输出格式有：

## 使用 Groff 格式化和打印文档

你可以尝试使用 Fedora 或 RHEL 系统上的任何页面（例如 `/usr/share/man/*` 中的页面）来格式化现有的 Groff 文档。这些页面是经过压缩的，因此你可以将它们复制到临时目录并解压，以便由 Groff 输出。

这些命令将 `chown` man 页面复制到 `/tmp` 目录并解压。然后 Groff 将 man 页面格式化为纯文本，以便你可以在屏幕上打印。
