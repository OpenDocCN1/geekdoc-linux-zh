
# OpenOffice.org Writer 工具栏与功能

OpenOffice.org Writer 中的工具栏包含用于识别文件名的框，以及更改样式、字体类型和字号的选项。按钮允许你保存和打印文件、更改文本对齐方式，以及剪切、复制和粘贴文本。换句话说，Writer 几乎包含了你在高级文字处理器中期望看到的所有功能。此外，Writer 还包含一个方便的 PDF 按钮，可将文件直接输出为 PDF 格式。这对于交换文档或将数据发布到互联网上非常有用。

如果你是刚开始使用 OpenOffice.org Writer，以下是一些你可以尝试的功能：

- **向导（Wizards）** — 使用向导开始创建信函、传真、议程、演示文稿、Web 页面、文档转换器或欧元转换器。选择“文件 → 向导”，然后选择上述提到的文档类型之一。文档转换器向导允许你将 Microsoft 或 StarOffice 文档目录转换为 OpenDocument 格式。欧元转换器允许你将包含不同欧洲货币的文件转换为欧元。

- **文档样式和格式化** — 使用字符、段落、框架、页面和编号样式创建文档格式（选择“格式 → 样式和格式化”）。在“样式和格式化”窗口中，选择要更改的样式类型，在样式框中右键单击，然后选择“新建”来创建你自己的样式。

- **检查文档（Checking Documents）** — 尝试不同的功能来检查和纠正你的文档。Writer 包含拼写检查等功能（“工具 → 拼写和语法”）。你可以将内容显示为 Web 页面或打印版式，并查看字体和字符标记（“视图 → 非打印字符”）。

- **绘图和图片（Drawing and images）** — 使用绘图工具（“视图 → 工具栏 → 绘图”）在文档中创建绘图、流程图、标注或符号。在页面上插入背景颜色或图形（“格式 → 页面”，选择“背景”选项卡，并选择颜色或图形）。要插入图形，请从主菜单选择“插入 → 图片”，并从文件或扫描仪插入图像。

- **输出 PDF 或其他格式（Outputting PDF or other formats）** — Writer 提供了一个工具栏按钮，可将当前文档输出为 PDF 格式。PDF 是共享文档的优良格式，适用于希望他人阅读或打印文档但不一定提供原始源文件的情况。你还可以将 Writer 文档保存为其他有用格式，包括 HTML（用于将文档发布到 Web）或富文本格式（用于与不同的文字处理器共享文档）。

> 注意：请访问 `http://www.OpenOffice.org` 了解更多关于 OpenOffice.org 的信息。

## 其他文字处理器

从 Fedora 软件仓库中可以获得许多不同的文字处理器。诸如 AbiWord 和 KOffice（属于 KDE 桌面环境的一部分）等流行的轻量级文字处理器现在可以通过 Fedora 仓库中的单条 `yum` 命令轻松安装。至于商业产品，有 Sun Microsystems 的 StarOffice 和 TextMaker。

### StarOffice

Sun Microsystems, Inc. 的 StarOffice 办公套件（`http://www.sun.com/staroffice`）是一款在 Linux、UNIX 和 Windows 操作系统上运行的商业产品。StarOffice 包含文字处理、电子表格、演示图形、电子邮件、新闻、图表和图形应用程序。与 OpenOffice.org 类似，StarOffice 包含许多使其与 Microsoft Office 应用程序兼容的功能。特别是，它具有导入 Microsoft Word 和 Excel 文件的能力。

StarOffice 可能是 Linux 上最完整的集成办公套件。不过，如果你在跨平台环境中工作，也可以在 Sun Solaris 和 Microsoft Windows 操作系统上获取 StarOffice。StarOffice 包括：

- **StarOffice Writer** — 这是 StarOffice 的文字处理应用程序。它可以导入多种格式的文档，特别强调 Word 文档。

- **StarOffice Calc** — 这是随 StarOffice 附带的电子表格程序。你可以从 Microsoft Excel 和其他流行程序导入电子表格。

- **StarOffice Impress** — 此模块允许你创建演示文稿。

- **StarOffice Draw** — 这是一个基于矢量的绘图程序。它包含创建 3D 对象和使用纹理的功能。

- **StarOffice Base** — 你可以使用 StarBase 管理数据，它是数据库的友好前端。它可以访问各种数据库接口。

StarOffice 中还有其他工具，使你可以创建商业图形、编辑光栅图像和编辑数学公式（StarOffice Math）。

你可以下载适用于 Linux 的 StarOffice 9.1，或从 StarOffice 网站 `http://www.sun.com/staroffice/` 购买盒装版。虽然 StarOffice 曾经可以免费下载，但当前家庭用户下载该软件的价格为 34.95 美元。

### AbiWord

`AbiWord` 文字处理器（`abiword` 命令）是 AbiSource 项目（`http://www.abisource.com`）开发的一款非常出色的免费文字处理器。如果你从零开始创建文档，AbiWord 包含创建高质量文档所需的许多基本功能。除了使用其自身的 AbiWord 格式（`.abw` 和 `.zabw`）处理文件外，AbiWord 还可以导入 Microsoft Word 和几种其他格式的文件。

使用 AbiWord，你可以选择文件包含的文档类型。你可以选择以以下格式保存文件：

- AbiWord、AbiWord 模板和 Gzipped AbiWord（`.abw`、`.awt`、`.zabw`）

- HTML/XHTML（`.html`）

- KWord（`.kwd`）

- 多部件 HTML（`.mht`）

- 富文本格式（`.rtf`）

- Microsoft Word（`.doc`）

- OpenDocument 格式，即 ODF，办公文档的标准

- PalmDoc（`.pdb`）

- 可移植文档格式（`.pdf`）

- Word Perfect（`.wp` 需要添加插件）

- 文本（`.txt`）

AbiWord 尚不能完全顺畅地导入所有这些文件类型。尽管 AbiWord 的最新版本支持 Word 样式，但有时表格、图形和其他功能无法完美转换。如果你想在 AbiWord 中处理 Word 文档，请将其作为 AbiWord 文件打开，纠正任何字体问题，并将文档保存为 AbiWord 格式。AbiWord 在过去几个版本中有了巨大改进，但如果你需要与使用 Word 的其他人交换文件，仍然可能会遇到问题。（若要保留 Word 格式文件，OpenOffice.org 和 StarOffice 表现要好得多，但也并非完美。）

如果你的硬件较慢，AbiWord 的性能比 OpenOffice.org Writer 更好。如果你在跨平台环境中工作，可以获取运行在 Windows、Mac OS X、QNX 和大多数 UNIX 衍生系统（Linux、BSD、Solaris 等）上的 AbiWord 版本。

最近新增的功能，如样式和项目符号，使 AbiWord 成为一个更有用的文字处理工具。虽然它无法与同类的商业产品竞争，但其开发人员仍在不断进行改进。

### 使用 KOffice

KOffice 软件包包含一套专为 KDE 桌面环境设计的办公生产力应用程序。安装 `koffice-suite` 软件包将引入使用 KOffice 所需的大多数软件。它包含文字处理器（KWord）、电子表格（KSpread）、演示文稿创建器（KPresenter）和图表绘制程序（KChart）。这些应用程序可以单独运行，也可以在 KOffice 工作区内运行。`koffice` 软件包位于随本书附带的 DVD 上。你可以从 KOffice 网站 `http://www.koffice.org` 了解更多相关信息。

使用命令 `yum install koffice-suite` 安装 KOffice 套件。

图 6-3 显示了 KWord 正在显示一个 Word 文档。

![](img/c78bdcb5b7842a0d73dcc98921f872a2_257_0.png)

你可以处理各种文档、电子表格和图像类型；目前支持的商业文档类型并不多。因此，你可能需要使用...

其他工具之前才能将它们读入 KWord。然而，KSpread 程序可以打开多种不同的电子表格样式，例如 Microsoft Excel 和 GNumeric 电子表格。Kivio 是一个有用的流程图工具。

> **注意：** 总体而言，OpenOffice.org 套件与在 Microsoft Office 中创建的文档相比，具有更高的兼容性，优于 KOffice 套件。

### TextMaker
