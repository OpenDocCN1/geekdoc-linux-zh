
# 第12章：办公应用

## OpenOffice

OpenOffice 285

| 网站 | 说明 |
|---|---|
| www.openoffice.org | 基于 StarOffice 的 OpenOffice |
| www.koffice.org | KOffice |
| www.gnome.org | Gnome Office |
| www.ximian.com | Xianian |
| www.sun.com | StarOffice |
| www.codeavers.com | CrossOver Office |

表 12-1. Linux 办公软件

## 访问微软的可访问性

| 应用程序 | 描述 |
|---|---|
| OpenCalc | OpenOffice 电子表格程序 |
| OpenDraw | OpenOffice 绘图程序 |
| OpenWriter | OpenOffice 文字处理器 |
| OpenMath | OpenOffice 数学公式编辑器器 |
| OpenImpress | OpenOffice 演示文稿管理器 |

**表 12-2.** Gnome Open Office

OpenCalc 是一款专业的电子表格软件。通过 OpenMath，你可以创建公式，然后将其嵌入文本文档中。通过演示文稿管理器（OpenImpress），你可以为演示文创建图像，如圆形、矩形以及箭头等连接元素，以及基于的插图。OpenImpress 支持高级功能，如对象变形、对象分组和定义渐变。OpenDraw 是一款功能复杂的绘图工具，包含了 3D 建模工具。你可以创建简单或复杂的图像，包括在曲线上对齐的动画文本。OpenOffice 还包含一个打印机设置工具，通过它可以选择打印机、字体、纸张大小和页面格式。

![](img/0160c5015efa6b5e7fe8c8f2b89e33c1_315_0.png)

**图 12-1.** OpenOffice 的 OpenWriter 文字处理器

StarOffice 是一个完全集成且兼容 Microsoft Office 的办公应用程序套件，由 Sun Microsystems 公司开发并支持，网址为 www.sun.com/staroffice。Sun 提供 StarOffice 6.0 版本作为商业产品，但教育用途是免费的。

## KOffice

KOffice 是一个为 KDE（K 桌面环境）集成的集成办公套件，由多个办公应用程序组成，包括文字处理器、电子表格和图形应用程序。在红帽 8.0 上，KOffice 只能从 KDE 桌面面的“额外办公菜单”（Extras Office Menu）访问。所有应用程序都是为 KOM 组件模型编写的，该模型允许任何一个应用程序的组件在另一个应用程序中使用。这意味着你可以将来自 KSpread 的电子表格或来自 Contour 的绘图嵌入 KWord 文档中。你可以通过 KOffice 网站 www.koffice.org 获取更多关于 KOffice 的信息。

目前，KOffice 包含了 KSpread、KPresenter、Contour、Karbon、KWord、KFormula、KChart、Kivio 和 KPlato（见表 12-3）。KSpread 是电子表格程序，KPresenter 是演示程序，Contour 是矢量绘图程序，Karbon 是一个矢量图形程序，KWord 是一个类似 Publisher 的文字处理器，KFormula 是公式编辑器，而 KChart 生成图表和图解。Kugar 是报告生成器，Krita 是位图图像编辑器，Kivio 创建流程图，而 KPlato 处理项目管理。

| 应用程序 | 描述 |
| KSpread | 电子表格 |
| KPresenter | 演示程序 |
| Contour | 矢量绘图程序 |
| Karbon | 矢量图形程序 |
| KWord | 文字处理器（桌面出版系统） |
| KFormula | 数学公式编辑器 |
| KChart | 用于绘制图表和图解的工具 |
| Kugar | 报告生成器 |
| Krita | 图像处理程序 |
| Kivio | 流程图生成器和编辑器（类似于 Vivio） |
| KPlato | 项目管理 |

表 12-3. KOffice 应用程序

![](img/0160c5015efa6b5e7fe8c8f2b89e33c1_316_0.png)

嵌入组件支持实时更新。例如，如果你使用 KSpread 电子表格中的数据在 Kword 文档中生成图表，然后更改电子表格中选中的数据，KChart 会自动更新 Kword 文档中的图表。在这里，你正在创建一个复合文档——由多个组件组成的文档。这种能力由 KDE 的 KParts 模型实现。

在这方面，你可以认为一个应用程序也可以作为一个服务器工作，为其他应用程序提供其专长的服务。专门负责段落格式化或拼写检查等服务的文字处理器可以为所有 KOffice 应用程序提供这些服务。这样，其他应用程序就不需要在内部编写自己的格式化函数了。

KParts 是通过桌面通信协议 DCOP 实现的。这是一种非常简单、微小且快速的进程间通信（IPC）和远程过程调用（RPC）机制，基于 Windows 系统的 ICE 交换协议。KDE 应用程序现在使用 DCOP 库来管理它们之间的通信。DCOP 使 KOffice 应用程序的开发变得更加简单和稳定。

通过 KOffice，你创建一个文档而不是为不同的应用程序创建单独的文档。不同的应用程序变成了此文档的视图，将它们添加到 KOffice 中即可。Kword 设置了构建和文字处理组件，Contour 绘制绘图组件，而 KSpread 添加电子表格组件。你使用适当的应用程序来查看单一文档中的不同组件。这意味着你可以同时为文档的不同组件打开单独窗口。

KSpread 是电子表格应用程序，它包含了大多数电子表格中的基本操作，并带有与 Excel 相似的公式。你还可以使用 KChart、Krita、Contour 或 KFormula 嵌入图表、图片或公式。

通过 KChart，你可以创建不同类型的图表，如柱图、饼图和折线图，还可以创建图解。要生成图表，你可以使用 KSpread 中的数据输入数据。通过 KPresenter，你可以创建由文本和图形组成的演示文稿，使用气泡、箭头等元素以及颜色等属性。你还可以将此类元素作为剪贴，并嵌入任何 KOffice 组件。Contour 是一款矢量绘图程序，类似于 Illustrator 或 Core Draw。它支持旋转、缩放和对齐等图形操作。

| 应用 | 描述 |
|--- | --- |
| Gnumeric | 电子表格 |
| Gnome 个人信息管理器 | 日历/组织器和地址簿 |
| Gnumeric | 电子表格 |
| Guppi | 绘图和图表程序 |
| Sketch | 矢量绘图包 |
| Toutoux | 项目管理器 |
| OpenOffice | OpenOffice 办公套件 |

**表 12-4.** *Gnome 办公（续）*

用于嵌入组件的 CORBA 确保了整个 Gnome 界面中都具有拖放能力。所有这些程序都基于一组 Gnome 技术，包括 Bonobo、Gnome-Print 和 XML。Bonobo 是支持复合文档和可重用软件组件的 Gnome 架构。Gnome-Print 是 Gnome 打印架构，旨在支持图形应用程序并与任何打印资源协同工作。XML 被用作原生文件格式，支持 Gnome 之间数据的易于交换。

目前，Gnome 办公包含 AbiWord、Gnumeric、GIMP、Dia、Eye of Gnome、Gnome-PIM 和 Gnome-DB。AbiWord 是一个文字处理器，Gnumeric 是电子表格，GIMP 是 Gnome 图像编辑应用，Dia 是绘图工具，Eye of Gnome 是图像查看器，Gnome 个人信息管理器（Gnome-PIM）是一个个人信息管理器，而 Gnome-DB 提供数据库连接（见表 12-4）。

Gnumeric 是电子表格，一个替代商业电子表格的专业级程序。与 Gnome一样，Gnumeric 在 GNU 许可证下免费提供。你可以在任何支持 Gnome 的发行版中找到随 Gnome 一起安装它。它的开发目前由 Ximian 管理。你可以从 www.ximian.com 或 www.gnome.org/projects/gnumeric 下载当前版本。Gnumeric 具有标准的 GUI 电子表格功能，包括自动填充和单元格格式化，并提供了大量的格式。它支持拖放操作，允许你选择并移动复制到另一个位置。Gnumeric 还支持插件，使其能够轻松地扩展和自定义其功能。

AbiWord 是一个开源文字处理器，支持无限撤销操作和 Word 97 导入等功能。它是 AbiSource 项目（www.abisource.com）开发的一系列桌面应用程序的一部分。

GIMP 是 GNU 图像处理程序，支持照片修饰、图像合成和图像创作等操作（见第 13 章中关于图形的部分）。你可以从 www.gimp.org 获取更多信息。

Dia 是一个旨在创建图表的绘图程序。你可以选择不同类型的图表进行创建，例如数据库、电路对象、流程图和网络图。你可以轻松地创建元素以及带有不同类型端点（如箭头或菱形）的线条和圆弧。数据可以以 XML 格式保存，使其方便地传输到其他应用程序。

Eye of Gnome (EOG) 是一个图像查看器，也可以作为图像目录程序使用。它的设计目的是快速并提供高质量的图像显示。

Gnome 个人信息管理器 (Gnome-PIM) 是包含日历和地址簿的个人信息管理器。Gnome-PIM 包含在当前的 Gnome 分版中。你可以从 www.gnome.org/gnome-office 获取更新。

Gnome-DB 是一个库和应用程序包，允许访问不同的数据库系统。它提供指向 CORBA 的 API。通过此 API，Gnome 应用可以访问数据库。你可以在 www.gnome.org/gnome-db 了解 Gnome-DB。

Ximian 是一个 Gnome 项目，旨在为 Gnome 提供一个专业级的桌面，其中包含全系列的办公应用。你可以在 www.ximian.com 了解 Ximian。Ximian 目前提供了 Gnome 桌面的增强版本，并支持 Gnumeric 电子表格的开发。它的第一个办公应用是名为 Evolution 的联系人、日历和邮件客户端应用（见第 14 章）。你可以从 Ximian 网站下载 Evolution，但它需要 Ximian Gnome 桌面才能运行。他们的下一个项目是一个文字处理器。

> Corel WordPerfect 文字处理器的个人版现已在 Linux 上可用且免费。个人版是一个功能完全的文字处理器。你可以从 Corel 网站 linux.corel.com 下载 WordPerfect。WordPerfect 不仅仅是一个文字处理器。你可以用它创建图形、电子表格和图表，还可以编辑和发布 Web 页面。

![](img/0160c5015efa6b5e7fe8c8f2b89e33c1_320_0.png)

## 编辑器

传统上，大多数 Linux 发行版（包括红帽）都会安装基于光标的编辑器 Vim 和 Emacs。Vim 是 Unix 系统上使用的 Vi 编辑器的增强版本。这些编辑器使用简单的基于光标的操作来为你提供全屏格式。你可以从 shell 命令行启动这些编辑器，而无需任何 X Window 系统支持。在这种模式下，它们基于光标的操作没有菜单、滚动条或鼠标点击功能。然而，K Desktop 和 Gnome 支持具有所有这些功能的强大 GUI 文本编辑器。这些编辑器的运行方式与 Macintosh 和 Windows 系统上发现的编辑器非常相似。它们具有完整的鼠标支持、滚动条和菜单。你可能会发现它们比 Vi 和 Emacs 编辑器更易用。这些编辑器在各自的桌面环境中运行，要求你安装了 KDE 或 Gnome，尽管编辑器可以在任何一个桌面上运行。Vi 和 Emacs 拥有多年来完善的强大功能。特别是 Emacs，可以扩展为用于编写新应用程序的完整开发环境。

目前有多个版本的 Emacs 可供 Unix 和 Linux 系统使用。Linux 发行版通常包含的版本是 GNU Emacs 或 XEmacs。GNU Emacs 的当前版本为 20.x；它支持窗口系统，能够启用菜单、滚动条和基于鼠标的编辑操作等 GUI 功能。（有关 GNU Emacs 宏及其通讯的讨论，请参阅第 14 章。）请检查你所在发行版的更新 FTP 站点以获取新版本发布时的最新版本，并访问 GNU 网站 (www.gnu.org) 和 Emacs 网站 (www.emacs.org)。你可以在其网站 www.emacs.org 了解更多关于 Emacs 的信息。

Emacs 的强大之处和灵活性源于它管理缓冲区的能力。Emacs 被描述为一种面向缓冲区的编辑器。当你在任何编辑器中编辑文件时，文件都会被复制到工作缓冲区，并且编辑操作在缓冲区中进行。Emacs 可以同时管理多个缓冲区，允许你同时编辑几个文件。你可以编辑已删除或复制文本的缓冲区。你可以创建自己的缓冲区，向其中填充文本，稍后将其保存到文件中。Emacs 将缓冲区的概念扩展到涵盖任何任务。当你撰写邮件时，你打开一个邮件缓冲区；当你阅读新闻时，你打开一个新闻缓冲区。从一个任务切换到另一个只需切换到另一个缓冲区。

Emacs 编辑器的操作方式类似于标准的文字处理器。键盘上的键代表输入字符。命令通过特殊键实现，例如控制键 (`CTRL`) 和交替键 (`ALT`)。它没有像 Vi 或 Ed 那种特殊模式。你输入文本，并使用 `CTRL` 键执行编辑命令，例如移动光标或保存文本。这种结构使得 Emacs 编辑器易于使用。然而，Emacs 绝非简单——它是一个复杂灵活的编辑器，拥有数百条命令。Emacs 具有特殊功能，例如窗口。你可以同时显示两个文本窗口。你可以一次打开并处理多个文件，并在屏幕上为每个文件分配一个独立的窗口进行显示。你通过命令 `emacs` 启动 Emacs 编辑器。你可以输入想要编辑的文件名，如果文件不存在，则会创建它。在接下来的示例中，用户准备用 Emacs 编辑 `mydata` 文件：

```
emacs mydata
```
