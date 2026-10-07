

# Red Hat Linux 办公套件

开放数据库连接（ODBC）在 StarOffice 中提供，但在 OpenOffice.org 中则缺失，因为 OpenOffice.org 不包含数据库。然而，它提供了数据库前端。您可以在 http://www.unixodbc/doc/0MySql.pdf 获取的文档详细解释了如何配置 OpenOffice.org 以使用 Red Hat 提供的 MySQL 数据库，从而免费提供类似于 Microsoft Access 的功能。有关安装和配置 MySQL 的详尽情，，请参阅第 17 章。

OpenOffice.org Draw 用于创建可以包含在 OpenOffice.org 文档中的图形。它并不是为了作为更通用图形应用程序的替代品，但它具有足够的功能来满足大多数需求。

两个网站提供了关于 OpenOffice.org 功能的额外信息：

- http://dict.probits.com/download_dictionary.html—该网站提供了安装和连字符字典的说明和文件，这些字典未包含在 OpenOffice.org 中。
- http://sourceforge.net/projects/oextras/- 该网站提供了模板、宏和剪贴画，这些内容未由 OpenOffice.org 提供。

OpenOffice.org 是一个正在开发中的，但当前的版本是运行在 StarOffice 6.0 版本的 Sun 系统上的。您可以访问 OpenOffice.org 网站获取文档、解答常见问题并提供反馈。

# 使用 GNOME 办公

GNOME 项目并没有从零开始开发集成应用程序套件，而是汇集了来自不同开发者基于 GTK 的应用程序，以满足一般的办公需求（侧边栏）。由于 Sun 计划将 OpenOffice.org 与 GNOME 集成，某些 GNOME 办公组件的持续支持和开发可能会存在疑问。

### GTK 组件集

为了方便编写 GUI 应用程序，人们预先编写了一些小段代码来描述图形界面的某些图形函数；这些函数包括下拉列表、单选按钮、保存对话框、窗口按钮等。此类函数被称为组件（widgets），组件的集合被称为工具（tool）或组件集（widget set）。程序员不需要从零编写所有这些函数的代码，只需要引用这些组件即可。编写 GUI 应用程序变得简单（注：原文为 "This writing GUI applications is easy" 应为语法错误，此处意如此）。Windows 和 Mac 程序员仅有一套组件可以使用，而 Unix 和 Linux 程序员有许多套组件，遗憾的是，它们之间互不兼容。KDE 桌面使用 Qt 组件集，Netscape 使用 Motif 组件集，而 GNOME 应用使用 GTK 组件集。

GTK 是 G Tool 的缩写。GIMP（GNU 图像处理程序）是一个与 Adobe Illustrator 非常相似的图形应用程序。通过使用 GTK-based 术语，我们节省了数百个字的输入，并有助于我们对 GNOME 办公的讨论。在这些章节中，您可能还会看到对 QT 和 Motif 以及其他组件集的类似引用。

![](img/446debe023486a07fde575245cf7a3ff_854_0.png)

# 第 25 章 办公生产力应用程序

以下是 GNOME 办公套件的一些主要组件：

- AbiWord—此文字处理程序允许您编写、格式化和组织文本文档，并与 Microsoft Word 文件格式具有一定的兼容性。它使用插件（程序）来添加功能（如语言翻译）以增强其功能。
- Gnumeric—此电子表格程序允许您以电子表格格式操作数字。支持除极少数生门的 Microsoft Excel 函数以外的所有函数，意味着用户在与 Excel 用户交换电子表格时几乎不会遇到困难。
- The GIMP—此图形应用程序允许您创建通用的图像。它可以导入和导出常见的图形文件格式。GIMP 类似于 Adobe 的 Photoshop 应用，将在第 26 章“多媒体应用程序”中描述。
- Evolution—Evolution 是一个类似于 Microsoft Outlook 的邮件客户端，提供电子邮件、调度和日历功能。它在第 19 章“处理电子邮件”中描述。
- Balsa—此轻量级邮件客户端类似于 Microsoft Outlook Express。它在第 19 章中描述。

被称为 GNOME 办公的应用程序松散关联包含了几个额外的应用程序，这些程序重复了 Red Hat 已提供的应用程序的功能。为了消除冗余，那些 GNOME 应用未包含在 Red Hat 8.0 中。它们都可以从 GNOME 办公网站 http://www.gnome.org/gnome-office/ 获取。

Red Hat 提供了如图25.3 所示的 AbiWord 编辑器。AbiWord 可以导入 XML、Microsoft Word、RTF、UTF-8、文本文件以及少数其他格式，但它还无法保存为 Microsoft Word 格式。AbiWord 的特点是使用插件来扩展其能力。这些插件增加了语言翻译、HTML 编辑、同义词典、Linux 命令行 shell 和在线字典等功能和特性。如果您需要一个轻量但强大的文字处理应用程序，应该检查一下。

AbiWord 应用图标位于“额外”（Extras）菜单下的“办公”（Office）菜单中（与 Gnumeric 和我们将在本节稍后讨论的 KOOffice 应用在列）。只需点击图标即可启动应用程序。或者，您也可以从命令行启动它，例如：

```
$ Abiword &
```

如果您熟悉 Microsoft Word，AbiWord 的界面会让您感到熟悉，因为它的设计者使用了 Word 作为模型。

![](img/446debe023486a07fde575245cf7a3ff_856_0.png)

图 25.3 AbiWord 是一个用于 Red Hat Linux、GNOME 和 X11 的文字处理程序。

您可以使用 Gnumeric 进行财务计算和数据绘图，如图25.4 所示。要启动 Gnumeric，选择“额外”、“办公”、“Gnumeric”。您也可以从命令行启动电子表格编辑器，如下：

```
$ gnumeric &
```

按下回车键后，出现 Gnumeric 主窗口。您通过点击单元格并在文本框中输入文本来输入数据。要创建图表，您点击并拖过电子表格单元格以高亮所需数据，然后点击 Gnumeric 工具栏中的“图表向导”（Graph Wizard）。它的绘图组件将启动，并将引导您通过一系列对话框创建图表。完成后，您可以点击并拖动电子表格的空白区域，图表就会出现。

MrProject 应用（见图25.5）用于跟踪项目进度，类似于其 win32 对应程序 Microsoft Project。尽管它正式上是 GNOME 办公应用的一部分，但 Red Hat 将 MrProject 作为 Red Hat 套件的一部分包含在主办公菜单中。您点击图标即可启动应用程序。当主窗口显示时，您可以启动新项目或导入现有项目。您可以在 http://mrproject.codefactory.se/user-guide.php 获取用户指南。

![](img/446debe023486a07fde575245cf7a3ff_857_0.png)

图 25.4 GNOME - Gnumeric 是一个强大的财务数据编辑器。

![](img/446debe023486a07fde575245cf7a3ff_857_1.png)

图 25.5 一个实用的 GNOME 应用，MrProject 是 Red Hat 应用程序的一部分。

# Red Hat Linux 办公套件

# 注意

Horde Project 是一个基于 PHP 的应用程序框架，提供 IMAP 访问、联系人管理器、日历管理器、错误跟踪器、标题查看器、CVS 仓库查看器、笔记本管理器、列表管理器、密码管理器、邮件管理器、日历以及演示演示。Horde Project 尚未完成，但已在企业中使用。提供一些应用程序的在线演示。您可以在 http://www.horde.org/ 查看 Horde Project。

# 使用 KOffice

KDE 办公套件 KOffice 的开发是为了与 KDE 桌面深度集成。集成允许将一个应用程序中的对象插入其他应用程序中，并且所有应用程序都可以相互通信，因此对象的更改会立即传递到其他应用程序。如果您使用 KDE 桌面，可以享受这种集成的好处，以及 Konqueror Web 和文件浏览器。

KOffice 的文字处理器是 KWord。KWord 是一个基于框架的文字处理器，这意味着文档页面可以使用框架进行格式化，框架内包含文本、图形和对象。框架可以用于格式化包含流文本和图像的页面，使得 KWord 成为创建标准商务信之外文档的绝佳选择。

KWord 和 KOffice 的其他组件仍在开发中，缺乏 OpenOffice.org 和 AbiWord 那种完善的功能，以及必要的 Microsoft 文件格式支持。如果 Microsoft 兼容性对您不重要且您使用的是 KDE 桌面而不是 GNOME，KOffice 值得考虑。

您可以通过“额外”菜单下的“办公”子菜单访问 KOffice 组件。您也可以从 KOffice shell 访问，它可以从命令行启动，如下：

```
$ koshell &
```

按下回车键后，看到如图25.6 所示的 KOffice 主窗口。

您可以点击主窗口左侧的图标启动 KWord 文字处理客户端、KSpread 电子表格程序和其他组件。您也可以从命令行启动单个客户端，而无需使用 KOffice 工作空间。例如，要使用 KWord，输入以下：

```
$ kword &
```
