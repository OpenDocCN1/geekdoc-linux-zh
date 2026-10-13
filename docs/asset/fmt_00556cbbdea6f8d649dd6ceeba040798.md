
# OpenOffice 套件概述

OpenCalc 是一款专业级电子表格。使用 OpenMath，您可以创建公式，然后将其嵌入到文本文档中。使用演示管理器（OpenImpress），您可以为演示文稿创建图像，例如圆形、矩形和连接元素（如箭头），以及基于矢量的插图。OpenImpress 支持高级功能，如对象变形、对象分组和定义渐变。OpenDraw 是一款复杂的绘图工具，包含 3D 建模工具。您可以创建简单或复杂的图像，包括沿曲线对齐的动画文本。OpenOffice 还包含一个打印机设置工具，可用于选择打印机、字体、纸张尺寸和页面格式。

注 StarOffice 是一款完全集成且兼容 Microsoft Office 的办公应用程序套件，由 Sun Microsystems 开发和支持。`www.sun.com/staroffice`. Sun 将 StarOffice 作为商业产品提供，不过教育用途免费。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_263_0.png)

## KOffice

KOffice 是 KDE（K 桌面环境）的一个集成办公套件，由多个办公应用程序组成，包括文字处理器、电子表格和图形应用程序。在 Red Hat 上，KOffice 只能从 KDE 桌面访问，具体位置在“更多办公应用程序”菜单中。所有应用程序都是为 KOM 组件模型编写的，该模型允许一个应用程序的组件在另一个应用程序中使用。这意味着您可以在 KWord 文档中嵌入来自 KSpread 的电子表格或来自 Kontour 的绘图。您可以在 KOffice 网站 `www.koffice.org` 上获取有关 KOffice 的更多信息。

### KOffice 应用程序

目前，KOffice 包括 KSpread、KPresenter、Kontour、Karbon14、KWord、KFormula、KChart、Kugar、Krita、Kivio 和 Kontact（见表 11-3）。KSpread 是电子表格，KPresenter 是演示应用程序，Kontour 是矢量绘图程序，Karbon14 是矢量图形程序，KWord 是类似 Publisher 的文字处理器，KFormula 是公式编辑器，KChart 生成图表和图形。Kugar 是报表生成器，Krita 是位图图像编辑器，Kivio 创建流程图，Kontact 是集成联系人应用程序，包括 Kmail、Korganizer、Kaddressbook 和 Knotes。

**表 11-3：KOffice 应用程序**

| 应用程序 | 描述 |
|---|---|
| KSpread | 电子表格 |
| KPresenter | 演示程序 |
| Kontour | 矢量绘图程序 |
| Karbon14 | 矢量图形程序 |
| KWord | 文字处理器（桌面出版） |
| KFormula | 数学公式编辑器 |
| KChart | 绘制图表和图形的工具 |
| Kugar | 报表生成器 |
| Krita | 绘画和图像处理程序 |
| Kivio | 流程图生成器和编辑器（类似 Vivio） |
| Kontact | 包含邮件、地址簿和组织工具的联系人应用程序 |

KSpread 是电子表格应用程序，包含大多数电子表格中常见的基本操作，其公式与 Excel 中使用的公式相似。您还可以使用 KChart、Krita、Kontour 或 KFormula 嵌入图表、图片或公式。

使用 KChart，您可以创建不同类型的图表，如条形图、饼图和折线图，以及创建图形。要生成图表，您可以使用 KSpread 中的数据输入数据。使用 KPresenter，您可以创建由文本和图形组成的演示文稿，使用不同的字体方向和颜色等属性进行建模。您可以添加诸如对话框、箭头和剪贴画等元素，以及嵌入任何 KOffice 组件。Kontour 是一款基于矢量的图形程序，很像 Adobe Illustrator、OpenDraw 和 Corel Draw。它支持标准图形操作，如旋转、缩放和对齐对象。

KWord 最好被描述为桌面出版软件，具有 Microsoft Publisher 和 FrameMaker 等出版应用程序中常见的许多功能。尽管它也是一个功能齐全的文字处理器，但 KWord 不是像 Word 或 WordPerfect 那样的基于页面的。相反，文本设置在框架中，这些框架像对象一样放置在页面上。框架就像绘图程序中的对象一样，可以移动、调整大小甚至重新定向。您可以将框架组织成框架集，使文本从一个流向另一个。可以对框架集应用格式设置，一次更改其所属所有框架的特征。您首次创建文档时默认设置的框架集与页面大小相同。这给您基于页面的文字处理器的效果，使您的工作就像使用标准文字处理器一样。当然，如果您愿意，可以更改框架的大小并添加新的框架。

KFormula 是用于生成数学公式的公式编辑器。Kivio 是类似 Visio 的流程图应用程序。Kivio 具有使用可脚本化对象生成流程图的能力。给定一个网络，Kivio 可以为其生成流程图。使用 Java 头文件，它可以生成 Java 对象的流程图。Krita（前称 KImageShop）是一款图像编辑器，很像 Photoshop。

## KParts

嵌入式组件支持实时更新。例如，如果您使用 KChart 在 KWord 文档中根据 KSpread 电子表格中的数据生成图表，然后更改电子表格中选定的数据，KChart 会自动更新 KWord 文档中的图表。实际上，您正在创建一个复合文档——由多个应用程序组成。此功能由名为 KParts 的 KDE 组件模型实现。KParts 在分布式对象之间提供通信。从这个角度来看，您可以认为应用程序也作为服务器运行，为其他应用程序提供其专业化的服务。文字处理器，专门提供段落格式或拼写检查等服务，可以为所有 KOffice 应用程序提供这些服务。这样，其他应用程序就不必在其内部编写自己的文本格式功能。

KParts 使用 DCOP 实现，即桌面通信协议。这是一种非常简单、小巧且快速的进程间通信（IPC）/远程过程调用（RPC）机制，基于 X Window 系统的 ICE（客户端间交换）协议。KDE 应用程序现在使用 DCOP 库来管理它们之间的通信。DCOP 使 KOffice 应用程序的开发变得更加容易和稳定。

使用 KOffice，您创建一种文档，而不是为不同应用程序创建单独的文档。不同的应用程序成为该文档的视图，为其添加组件。KWord 设置出版和文字处理组件，Kontour 添加绘图组件，而 KSpread 添加电子表格组件。您使用适当的应用程序查看单个文档中的不同组件。这意味着您可以同时为文档的不同组件打开单独的窗口。

## GNOME 办公套件和 Ximian

GNOME 的办公应用程序已独立开发，例如电子表格 Gnumeric。 大多数可通过各种“更多”菜单访问，例如 AbiWord 和 Gnumeric 的“更多办公应用程序”，或 Galeon 的“更多 Internet 应用程序”。 然而，图表渲染工具 DIA 则包含在主办公菜单中。 GNOME Office 将 Gnumeric 和 AbiWord 等各种独立办公应用程序集成到生产力套件中。 Sun Microsystems 还将 OpenOffice 集成到 GNOME 中，使所有 OpenOffice 应用程序都成为 GNOME Office 的一部分。 您可以在 `www.gnome.org/gnome-office` 了解更多有关 GNOME Office 的信息。 在这里，您可以链接到当前版本的下载页面并查看屏幕截图。 当前列表显示在表 11-4 中。 所有程序都实现了用于嵌入组件的 CORBA 模型，确保在整个 GNOME 界面中具有拖放功能。 它们都基于一组 GNOME 技术，包括 Bonobo、Gnome-Print 和 XML。 Bonobo 是 GNOME 用于支持复合文档和可重用软件组件的架构。 Gnome-Print 是 GNOME 打印架构，旨在支持图形应用程序并轻松与任何打印资源配合使用。 XML 用作原生文件格式，以支持 GNOME 应用程序之间数据的轻松交换。

目前，GNOME Office 包括 AbiWord、Gnumeric、GIMP、Dia、Eye of GNOME、Evolution 和 GNOME-DB。 AbiWord 是文字处理器，Gnumeric 是电子表格，GIMP 是 GNOME 图像编辑应用程序，Dia 是图表制作器，Eye of GNOME 是图像查看器，Evolution 是集成的电子邮件和个人信息管理器，而 GNOME-DB 提供数据库连接（见表 11-4）。

表 11-4: GNOME 办公套件

| Application | Description |
|---|---|
| AbiWord | 跨平台文字处理器 |
| Balsa | 电子邮件客户端 |
| Gfax | 发送和接收传真 |
| Galeon | 网页浏览器 |
| Gnumeric | 电子表格 |
| Gnucash | 个人财务管理 |
| Dia | 图表和流程图编辑器 |
| Evolution | 电子邮件和日历 |
