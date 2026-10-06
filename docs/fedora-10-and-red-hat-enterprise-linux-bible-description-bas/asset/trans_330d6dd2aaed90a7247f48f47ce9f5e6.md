

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

从 Fedora 软件仓库中有许多不同的文字处理器。流行的轻量级文字处理器如 AbiWord 和 KOOffice（ KDE 的一部分）现在可以通过 yum 命令轻松安装。至于商业产品，有来自太阳的 StarOffice 和 TextMaker。

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

