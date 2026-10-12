

从零开始编写所有这些函数的代码，程序员只需参考部件即可。这使得编写 GUI 应用程序变得更加容易。与 Windows 和 Mac 程序员仅有一套部件可用不同，Unix 和 Linux 程序员拥有多套部件；不幸的是，这些部件之间互不兼容。KDE 桌面使用 QT 部件集，Netscape 使用 Motif 部件集，而 GNOME 应用程序使用 GTK 部件集。

GTK 是 GIMP Tool Kit 的缩写。GIMP（The GNU Image Manipulation Program，GNU 图像处理程序）是一款图形应用程序，与 Adobe Photoshop 非常相似。通过使用基于 GTK 的术语，我们可以省去几百字的打字，并有助于推进我们关于 GNOME Office 的讨论。你还会在这些章节中看到对 QT 和 Motif 以及其他部件集的类似引用。

以下是 Fedora 中可用的 GNOME Office 套件的一些主要组件：

- **AbiWord**——这款文字处理程序允许你撰写、格式化和组织文本文档，并且与 Microsoft Word 文件格式具有一定的兼容性。它使用插件（添加功能如语言翻译的程序）来增强其功能。
- **Gnumeric**——这款电子表格程序允许你在电子表格格式中操作数字。除了最晦涩难懂的 Microsoft Excel 函数外，它对其他函数都有支持，这意味着用户在与 Excel 用户交换电子表格时应该不会有太大麻烦。
- **The GIMP**——这款图形应用程序允许你创建通用图像。它可以导入和导出所有常见的图形文件格式。The GIMP 类似于 Adobe 的 Photoshop 应用程序，并在第 10 章“多媒体应用程序”中进行了描述。
- **Evolution**——Evolution 是一个电子邮件客户端，其界面类似于 Microsoft Outlook，提供电子邮件、日程安排和日历功能。它在第 8 章“互联网：浏览网页、撰写电子邮件和阅读新闻”中进行了描述。
- **Balsa**——这款轻量级电子邮件客户端类似于 Microsoft Outlook Express。它在第 8 章中进行了描述。

被称为 GNOME Office 的松散应用程序集合还包括一些额外应用程序，这些应用程序重复了 Fedora Core 已经提供的应用程序的功能。为了消除冗余，这些额外的 GNOME 应用程序并未包含在 Fedora 的默认安装中。它们都可以从 GNOME Office 网站 http://www.gnome.org/projects/ooo/ 获取，部分也包含在安装 CD 上。

Fedora 在其 Extras 中提供了 AbiWord 编辑器，如图 9.3 所示。AbiWord 可以导入 XML、Microsoft Word、RTF、UTF8、纯文本、WordPerfect、KWord 和少量其他格式。AbiWord 以其使用插件或集成的辅助应用程序来扩展其功能而著称。这些插件添加了语言翻译、HTML 编辑、同义词词典、Linux 命令 shell 和在线词典等功能和特性。如果你只需要一个轻量但强大的文字处理应用程序，你应该考察 AbiWord。

![](img/774d40fd20903495c5cd00e2efad3f33_277_0.png)

**图 9.3** AbiWord 是用于 Fedora、GNOME 和 X11 的文字处理程序。它可以处理一些 OpenOffice.org 无法处理的格式，但目前对 MS Word 格式的支持还做得不好。

AbiWord 应用程序图标位于“更多办公应用程序”菜单中，在“办公”菜单下（与本部分稍后讨论的 Gnumeric 和 KOffice 应用程序一起）作为“文字处理器”项目。只需单击图标即可启动应用程序，或者你可以从命令行启动它，如下所示：

```
$ abiword &
```

如果你熟悉 Microsoft Works，你会熟悉 AbiWord 的界面，因为其设计者以它作为模型。

你可以使用 Gnumeric 电子表格应用程序执行财务计算并对数据进行图形化，如图 9.4 所示。它可以导入逗号或制表符分隔的文件、文本或 Gnumeric XML 格式的文件，只能将文件保存为 XML 或文本格式。要从菜单启动 Gnumeric，请依次选择“办公”、“更多办公应用程序”，然后选择“Gnumeric 电子表格”。你也可以从命令行启动电子表格编辑器，如下所示：

```
$ gnumeric &
```

按下 Enter 键后，Gnumeric 主窗口会出现。你通过单击单元格然后在文本框中输入文字来在电子表格中输入数据。要创建图形，你单击并拖动以突出显示电子表格中的单元格以选中所需数据，然后单击 Gnumeric 工具栏中的图形向导图标。Gnumeric 的图形组件将启动，你将通过一系列对话框来创建图形。完成后，你可以单击并拖动电子表格的空白区域，图形就会出现。

![](img/774d40fd20903495c5cd00e2efad3f33_278_0.png)

**图 9.4** GNOME 的 Gnumeric 是一款功能强大的财务数据编辑器——此处用于跟踪 401K 退休账户。OpenOffice.org 也提供电子表格应用程序，KOffice 也是如此。

项目计划器（Project Planner）应用程序对于跟踪项目进度非常有用，很像其 Windows 对应产品 Microsoft Project。当主窗口显示时，你可以开始新项目或导入现有项目。该应用程序提供三种视图：资源、甘特图和任务。

> **注意**
> 一些生产力应用程序属于“群件”类别；这些包括共享日历、文件、笔记、电子邮件等。这些应用程序在第 8 章中详细涵盖。

## 使用 KOffice

被称为 KDE 的 K 桌面环境（K Desktop Environment）不是 Fedora 的默认桌面环境。KDE 带有自己的一套库、部件以及一个应用程序间通信系统（拖放），它与默认的 GNOME 桌面环境不兼容。这并不意味着如果你选择了 GNOME 桌面（或反之亦然），KDE 应用程序就不可用。虽然 KDE 重复了 GNOME 提供的许多功能，但 KDE 应用程序通常为解决熟悉的问题提供了独特的方法，可能正是你所寻找的。

KDE 办公套件 KOffice 旨在与 KDE 桌面紧密结合。集成使得一个应用程序中的对象可以通过拖放插入到其他应用程序中，并且所有应用程序都可以相互通信，因此对象中的更改会立即传达给其他应用程序。KDE 提供的应用程序集成是对生产力的重大增强。（一些 GNOME 桌面应用程序之间也共享类似的通信功能。）如果你使用 KDE 桌面而不是默认的 GNOME 桌面，你可以享受这种集成的好处，以及 Konqueror 网页和文件浏览器的便利。

KOffice 的文字处理器是 KWord。KWord 是一个基于框架的文字处理器，这意味着文档页面可以在持有文本、图形和对象的框架集中格式化。框架集可用于格式化页面上的文本，包括分栏文本和文本需要环绕的图像，这使得 KWord 成为创建标准商务信函以外文档（如新闻通讯和宣传册）的极佳选择。

KWord 和 KOffice 的其他组件仍在开发中，缺乏 OpenOffice.org 和 AbiWord 那样完善的特性，也缺乏必要的 Microsoft 文件格式支持。如果 Microsoft 兼容性对你不重要，你和你的同事使用 KDE 桌面环境而不是 GNOME，那么 KOffice 值得考虑。KOffice 的下一个版本将包括第 8 章提到的 Kolab 群件应用程序；目前 GNOME 缺乏类似的群件功能。

你可以从“办公”菜单下的“更多办公应用程序”子菜单访问 KOffice 组件。你也可以从 KOffice shell 访问它们，KOffice shell 可以从命令行启动，如下所示：

```
$ koshell &
```

按下 Enter 键后，你会看到 KOffice shell 的主窗口，如图 9.5 所示。左侧是代表所有可用 KOffice 应用程序的图标。单击其中一个会启动一个对话框，以打开现有文件或在新文件中开始工作。

你可以单击主窗口左侧的图标来启动 KWord 文字处理客户端、KSpread 电子表格程序以及其他组件。你还可以

