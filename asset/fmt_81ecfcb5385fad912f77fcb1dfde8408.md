
当你安装新软件时，将看到支持的软件列表。这将包括 Office 应用以及某些添加/删除面板应用程序，如早期版本的 Photoshop。从安装软件面板，你可以选择从光盘或 exe 文件安装。对于光盘上的 Office，选择光盘、光驱器中的 Windows 光盘，然后点击下一步。Windows 安装程序将在 Linux 环境中启动，并运行就像你在使用 Windows 系统一样。如果安装需要重启，CrossOver 将模拟重启。安装完成后，你将在主菜单上看到 Windows 应用程序，从那里启动已安装的 Windows 软件。应用程序将在 Linux 窗口内运行，看起来就像在 Windows 中运行一样。对于不支持的应用程序，你可以尝试或不尝试 CrossOver。

通过 VMware，你可以在 Linux 下运行 Windows；你可以在 Linux 系统上运行 Windows 应用程序，包括 Office。有关更多信息，请查看 VMware 网站 `vmware.com`。

注意 尽管 Linux 允许用户直接挂载并访问 Windows 95、98 和 Me 使用的旧 DOS 或 FAT32 分区，但它可以使用 NTFS `ntfs-3g` 以及原始 NTFS 项目驱动程序挂载 NTFS 分区（Windows Vista、XP、2000 和 NT）。`ntfs-3g` 驱动程序支持写入 NTFS 分区，并默认安装在 Ubuntu 上。

## OpenOffice.org

OpenOffice.org 是一个完全集应用程序套件，作为一个开源项目开发并向所有人免费分发。它作为大多数 Linux 发行版的主要办公套件包含，可以通过 Office 菜单访问。它包含了文字处理、电子表格、演示文和绘图应用程序（参见表 13-2）。OpenOffice.org 存在于 Linux、Windows 和 Mac OS 版本。你可以从 `www.openoffice.org` 获取在线手册、常见问题解答（FAQs）以及当前版本等信息。

注意 OpenOffice.org 的开发是作为一个名为 `openoffice.org` 的开源项目进行的。其核心代码基于原始的 StarOffice。在 `openoffice.org` 项目中开发的代码将整合到 StarOffice 的未来版本中。

OpenOffice.org 是一个集成应用程序套件。你可以自由地打开 Writer、电子表格或演示文程序。此外，在大多数 OpenOffice.org 应用程序中，你可以点击“文件 | 新建”并在需要时选择不同的应用程序。Writer 处理器支持标准的文字处理功能，如剪切、粘贴、拼写检查和文本格式，以及段落样式。右键菜单让你能够轻松地格式化文本。向导（信函、网页、传真和议程）让你能够快速生成不同类型的文档。你可以在文档中嵌入对象，例如使用 Drawing 创建可以拖放到 Writer 文档中的功能。你可以在 OpenOffice 网站上各组件的相应页面找到有关每个组件的信息。

Calc 是一个专业级的电子表格。通过 Math，你可以创建可以嵌入到文本文档中的公式。通过 Impress 演示管理器，你可以为演示文稿创建图像——例如圆形、矩形、连接元素以及基于向量的插图。Impress 支持高级功能，如合并对象、分组对象和定义渐变。Drawing 是一个功能强大的绘图工具，包含了 3-D 建模工具。你可以创建简单或复杂的图像，包括在曲线上对齐的动画文本。OpenOffice.org 还包含一个打印机设置，你可以通过它选择打印机、字体、纸张大小和页面格式。

注意 StarOffice 是由 Sun Microsystems 开发并支持的完全集成且与 Microsoft Office 的办公应用程序套件，网址为 `www.sun.com/staroffice`。Sun 将 StarOffice 作为商业产品提供，但教育用途是免费。

| 应用程序 | 说明 |
| --- | --- |
| Base | 支持 MySQL、PostgreSQL 和 MaxDB 的基础数据库 |
| Calc | OpenOffice.org 电子表格 |
| Draw | OpenOffice.org 绘图应用程序 |
| Impress | OpenOffice.org 演示管理器 |
| Math | OpenOffice.org 数学公式编辑器器 |
| Writer | OpenOffice.org 文字处理器 |

**表 13-2** OpenOffice.org 应用程序

## 第 13 章：办公和数据库应用程序

OpenOffice.org 具有底层的组件模型，可以进行编程以开发自定义应用程序。请查看 OpenOffice.org API 项目获取更多详情（`http://api.openoffice.org`）。OpenOffice.org 软件开发包 (SDK) 支持使用 C++ 或 Java 编写的 OpenOffice.org 组件。统一网络对象 (UNO) 模型是 OpenOffice.org 的组件模型，提供了编程语言、其他模型和网络连接之间的交互。

另注在 GNOME 上可以使用桌面出版工具 Scribus，网址为 `www.scribus.net`。

## KOffice

KOffice 是为 K 桌面环境 (KDE) 的集成套件，由多个应用程序组成，包括文字处理器、电子表格和图形应用程序。你可以使用 Synaptic 软件包管理器下载它。所有应用程序都是为 K 组件模型编写的，允许任何一个应用程序的组件在另一个应用程序中使用。这意味着你可以在 KWord 文档中嵌入来自 KSpread 的电子表格或来自 Karbon14 的图表。你可以从 `http://office.org` KOffice 网站获取有关 KOffice 的更多信息。

提示 KOffice 应用程序具有导入和导出过滤器，允许它们从流行的应用程序（如 AbiWord、OpenOffice.org 应用程序、MS Word 甚至手持设备上的文档）导入或导出文件。这些过滤器的可靠性各异，你应该检查 KOffice Filters 网页以查看过滤器列表及其稳定性。

## KOffice 应用程序

目前，KOffice 包含 KSpread、KPresenter、KWord、Karbon14、KFormula、KChart、Kigar、Krita 和 Kivio（后者已作为一个独立项目分拆出去）。Contact 是一个集成应用程序，包括 KMail、KOrganizer、KAddressbook 和 Knotes。KSpread 是电子表格，KPresenter 是演示文稿应用程序，Karbon14 是矢量图形程序，KWord 是类似 Publisher 的文字处理器，KFormula 是公式编辑器，KChart 用于生成图表和图形。Kigar 是报告生成器，Krita 是位图图像编辑器，Kivio 创建流程图。KChart 提供与 KOffice 应用程序的数据集成，目前支持 PostgreSQL 和 MySQL。

电子表格应用程序 KSpread 包含了电子表格中的基本操作，其公式与 Excel 中使用的公式类似。你还可以使用 KChart、Karbon14 或 KFormula 嵌入图表、图片或公式。

通过 KChart，你可以创建不同类型的图表，如柱状图、饼图和折线图，还可以创建图形。要生成图表，你可以使用 KSpread 中的数据输入你的数据。通过 KPresenter，你可以创建由不同字体、方向和颜色等属性建模的文本和图形组成的演示文稿。你可以添加气泡、箭头和剪贴画等元素以及嵌入任何 KOffice 组件。Karbon14 是一个基于矢量的图形程序，类似于 Adobe Illustrator 和 OpenOffice.org Draw。它支持标准的图形操作，如旋转、缩放和对齐对象。

## 第五部分：应用程序

| 应用程序 | 说明 |
| --- | --- |
| Karbon14 | 矢量图形程序 |
| KChart | 用于绘制图表和图形的工具 |
| Keksi | 数据集成 |
| KFormula | 数学公式编辑器 |
| Kivio | 流程生成器和编辑器（类似于 Visio） |
| Kontakt（独立项目） | 包含邮件、地址簿和组织器的联系应用程序 |
| Contour | 矢量绘图程序 |
| KPlate | 项目管理与规划 |
| KPresenter | 演示程序 |
| Krita | 绘画和图像处理程序 |
| KSpread | 电子表格 |
| Kagar | 报告生成器 |
| KWord | 文字处理器（桌面出版） |

表 13-3 KOffice 应用程序

KWord 可以被描述为桌面出版软件，具有 MS Publisher 和 FrameMaker 等出版应用程序的功能。虽然它也是一个功能文字处理器，但 KWord 不像 Word 或 WordPerfect 那样基于页。相反，文本设置在帧中像对象一样移动、调整大小和改变方向。你可以将帧组织成帧集，使文本从一个流向另一个。

## KParts

嵌入组件支持实时更新。例如，如果你使用 KChart 利用 KSpread 中的数据在 KWord 文档中生成图表，然后更改电子表格中的选定数据，KChart 会自动更新 KWord 文档中的图表。事实上，你正在创建一个由多个应用程序组成的复合文档。这种能力通过名为 KParts 的 KDE 组件模型实现，该模型提供了分布式对象之间的通信。在这方面，你可以将一个应用程序视为服务器，为其他应用程序提供专门的服务。专门提供段落格式化或拼写检查服务的文字处理器可以为所有 KOffice 应用程序提供这些服务。这样，其他应用程序就不需要编写自己的文本格式化函数了。KParts 通过桌面通信协议 (DCOP) 实现。这是一种非常简单、快速且快速的进程间通信/远程过程调用 (IPC/RPC) 机制，基于 Windows 系统的客户端间交换（ICE）协议。KDE 应用程序现在使用 DCOP 库来管理它们之间的通信。

# 第 13 章：办公与数据库应用程序

## GNOME Office

GNOME Office 项目支持三款办公应用程序：AbiWord、Gnumeric 和 GNOME-DB。GNOME 的前成员仍提供某些办公任务的服务，例如 Novell 的 Evolution 电子邮件和联系人客户端。许多前成员目前仍是事实上的 GNOME 项目，其信息列在 `http://www.gnome.org/projects` 中。你可以从 `http://live.gnome.org/GnomeOffice` 的 GNOME 网站上获取更多信息。表 13-4 显示了常用的 GNOME Office 应用程序当前列表，包括一些不属于 GNOME Office 套件的程序。所有程序都实现了了用于嵌入组件的 CORBA 模型，确保在整个 GNOME 界面中都具有拖放功能。

Gnumeric 是一款专业级的 GNOME 电子表格软件，旨在取代商业电子表格软件。与 GNOME 一样，Gnumeric 在 GNU 公共许可下免费提供。Gnumeric 包含在 GNOME 发布中，你将在任何支持 GNOME 的发行版中找到它。你可以从 `www.gnome.org/projects` 下载当前版本。Gnumeric 支持标准的 GUI 电子表格功能，包括自动填充和单元格，并提供了大量的格式。它支持拖放操作，将单元格移动或复制到另一个单元格。Gnumeric 还支持插件，使其能够扩展和自定义功能。

AbiWord 是一款开源文字处理器，旨在成为一个全平台解决方案，可以在 Mac、Unix、Windows 以及 Linux 上运行。它是 AbiSource 项目（`http://abisource.com`）正在开发的一系列桌面生产力应用程序的一部分。

GNOME-DB 项目提供了一个 GNOME 数据访问 (GDA) 库，支持多种数据库，例如 PostgreSQL、MySQL、MS Access 和 unixODBC。它提供了一个数据库可以接入的 API。这些后端连接基于 CORBA。通过此 API，GNOME 应用程序可以访问数据库。你可以在 `www.gnome-db.org` 找到更多关于 GNOME-DB 的信息。

| 应用程序 | 描述 |
| :--- | :--- |
| **GNOME Office** | |
| AbiWord | 跨平台文字处理器 |
| GNOME-DB | 数据库连接性 |
| Gnumeric | 电子表格 |
| **其他 GNOME Office Apps** | |
| Balsa | 电子邮件客户端 (GNOME 项目) |
| Dia | 图表和流程图编辑器 (GNOME 项目) |
| Evolution | 集成电子邮件、日历和个人组织器 (Novell) |
| Gnu-Cash | 个人财务管理器 (GNOME 项目) |
| OpenOffice.org | OpenOffice.org 办公软件 |
| Planner | 项目管理器 (GNOME 项目) |

**表 13-4** 用于 GNOME 的 GNOME Office 及其他应用程序

## 第五部分：应用程序

Dia 是一种绘图程序，用于创建图表（GNOME 项目），例如数据库对象、流程图和网络图。你可以轻松创建元素，以及带有不同类型端点的线和弧（作为箭头或菱形）。数据可以以 XML 格式保存，方便地传输到其他应用程序。

GnuCash (`http://gnucash.org`) 是一款用于管理账户、股票和支出的个人财务应用程序（GNOME 项目）。它包含了通过 OpenHBC 接口支持家庭银行。OpenHBC 是开源家庭银行计算机接口（`http://openhbcisource.net`）。

## 文档查看（PostScript、PDF 和 DVI）

虽然在应用程序菜单的图形子菜单下查找，但 PostScript、PDF 和数字视觉界面 (DVI) 查看器更多地用于办公应用程序（见表 13-5）。Evince 和 Ghost 都显示 PostScript (.ps) 和 PDF (.pdf) 文件。Ghostview 的 X Window 系统以前端是由 KPDF 提供的，Xpdf 是 PDF 查看器。KPDF 包含了许多标准的 Adobe Reader 特功能，如缩放、双页显示和全屏模式。或者，你可以下载 Linux 版 Acrobat Reader 来生成 PDF 文档。你可以使用 Scribus 桌面出版系统（`www.scribus.net`），编辑 PDF 文档可以使用 pdfedit。

Linux 还拥有一种名为 TeX 的专业级排版工具，通常用于编写复杂的数学公式。TeX 生成的 DVI 文档可以由 DVI 查看器显示，Linux 下有多种此类查看器。由 TeX 文档应用程序生成的 DVI 文件可以通过 KDVI 查看，它是 KVShell 的一个插件。KVShell 可以显示和打印它拥有插件的任何类型的文档。

| 查看器 | 描述 |
| :--- | :--- |
| Acrobat Reader | Adobe PDF 和 PostScript 显示应用程序 |
| Evince | PostScript 和 PDF 文件的文档查看器 |
| Gnome-gv | Gnome Ghostscript |
| KDVI | 显示 DVI 文件的 KDE 工具（KVShell 的插件） |
| KGhostView | 显示 PostScript 和 PDF 文件的 KDE 接口 |
| KPDF | 显示 PDF 文件的 KDE 工具 |
| pdfedit | 编辑 PDF 文档 |
| Scribus | 生成 PDF 文档的桌面出版系统 |
| xpdf | 仅显示 PDF 文件的 X Window 系统 |

**表 13-5** PostScript、PDF 和 DVI 查看

## PDA 访问

对于许多 PDA，你可以使用 pilot 工具来使用你的手持设备，在它和系统之间传输信息。`pilot-link` 包包含了你可以用于访问 PDA 的工具。请查看 `www.pilot-link.org` 获取详细文档和有用链接。工具名称以 `pilot-` 开头——例如，`pilot-addresses` 从地址簿中读取地址。其他名称以 `read` 开头的工具允许你将 PDA 数据转换为其他应用程序格式；`read-expenses` 将支出数据输出为标准文本。最实用的工具之一是 `pilot-xfer`，用于备份 PDA。

与其使用命令行命令，不如使用 JPilot、KPilot 和 GNOMEpilot 访问你的 PDA。要在 GNOME 上使用 PDA，你可以使用 gnomepilot 插件（在偏好设置中）。Conduits 允许自动执行若干同步操作，包括电子邮件和安装文件。查看帮助按钮获取详细手册。

JPilot 提供了一个 GUI，让你执行同步书籍和编写备忘录等基本任务。KPilot 在安装了 kpilot 包后启用。当你启动 kpilot 时，它将让你与 PDA 同步或执行备份。然后你可以执行查看地址、安装文件等操作。对于文本和 Palm 格式的转换，你可以使用 PalmDoc。该工具会将文本文件转换为 Palm 文件。

> 用于 PDA 的设备名称为 `idev`，由 udev 管理。如果你需要手动为手持设备指定端口，你需要修改 udev 规则，而不是直接更改 udev 文件。

## 编辑器
