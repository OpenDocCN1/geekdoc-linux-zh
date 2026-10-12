

![](img/2045828cf45e5632bf056f9ca99d6755_292_0.png)

图 9.15 GNUME 的 Gnumeric 是一款功能强大的金融数据编辑器——此处正在处理前文使用的同一电子表格。OpenOffice.org 也提供电子表格应用，KoOffice 同样如此。

## 使用 KoOffice

K 桌面环境（KDE）并非 Fedora 的默认桌面环境。KDE 拥有自己的一套库、组件以及应用间通信（拖放）系统，这些与默认的 GNOME 桌面环境不兼容。这并不意味着如果你选择 GNOME 桌面（或反之），KDE 应用就无法使用。尽管 KDE 重复了许多 GNOME 提供软件的功能，但 KDE 应用通常以独特的方式解决熟悉的问题，可能正是你所寻找的。

KDE 办公套件 KoOffice 旨在提供与 KDE 桌面的紧密集成。集成使得一个应用中的对象可以通过拖放插入到其他应用中，并且所有应用都可以相互通信，因此对对象的更改会立即传递给其他应用。KDE 提供的应用集成是生产力的显著增强。（某些 GNOME 桌面应用之间也共享类似的通信机制。）如果你使用 KDE 桌面而不是默认的 GNOME 桌面，你可以享受这种集成的好处，以及 Konqueror Web 和文件浏览器。

KoOffice 的文字处理器是 KWord。KWord 是一个基于框架（frames）的文字处理器，意味着文档页面可以在包含文本、图形和对象的封闭区域中的框架内进行格式化。框架集（Framesets）可用于格式化包含多列、文本和图像（文本需要绕其流动）的页面文字，使 KWord 成为创建标准商务信函以外文档（如新闻通讯和宣传册）的极佳选择。

KWord 和 KoOffice 的其他组件仍在开发中，缺乏 OpenOffice.org 和 AbiWord 所有完善的功能，以及必要的 Microsoft 文件格式支持。如果 Microsoft 兼容性对你不重要，且你和你的同事使用的是 KDE 桌面环境而非 GNOME，KoOffice 值得考虑。KoOffice 的下一个版本将包含第 8 章中提到的 Kolab 群件应用；目前 GNOME 缺乏类似的群件功能。

你可以从 Office 菜单下的“更多办公应用”子菜单访问 KoOffice 组件。你也可以从 KOffice 外壳程序访问它们，该外壳程序可以通过命令行启动，如下所示：

```
$ koffice &
```

按下回车后，你会看到 KOffice 外壳程序的主窗口，如图 9.16 所示。左侧是代表你可用的所有 KOffice 应用的图标。单击其中一个会启动一个对话框，用于打开现有文件或开始在新文件中工作。

![](img/2045828cf45e5632bf056f9ca99d6755_293_0.png)

图 9.16 KDE 的 KOffice 提供工作区办公套件环境。此处显示的是打开文件对话框。

你可以单击主窗口左侧的图标来启动 KWord 文字处理客户端、KSpread 电子表格程序及其他组件。你也可以不使用 KOffice 工作区，直接从命令行启动单个客户端。

例如，要使用 KWord，输入以下内容：

```
$ kword &
```

然后 KWord 会要求你为当前会话选择文档。如图 9.17 所示，KWord 客户端提供高级编辑功能，包括桌面出版功能。

![](img/2045828cf45e5632bf056f9ca99d6755_294_0.png)

图 9.17 KOffice 的 KWord 文字处理组件是一个高级的基于框架的所见即所得编辑器，适合轻度桌面出版，支持多种格式，包括 WordPerfect。

KOffice 的 KSpread 客户端是一个功能完善的电子表格程序，提供图形功能。与 KWord 一样，KSpread 也可以从命令行启动。使用类似以下的命令后，你会被要求选择文档类型（新文档或旧文档）：

```
$ kspread &
```

KDE 在其 KOffice 及相关应用集合中包含其他生产力客户端。这些客户端包括通讯录、时间跟踪器、计算器、记事本和日程安排器。一个受欢迎的客户端是 KOrganizer，它提供任务、待办事项和预定日程的每日、每周、工作周和每月视图，并带有背景闹钟。

它还支持日志或日记功能，你可以与 Palm Pilot 同步信息。你可以从 KDE 桌面面板菜单或命令行启动此客户端，如下所示：

```
$ Korganizer &
```

典型的 KOrganizer 窗口如图 9.18 所示。

![](img/2045828cf45e5632bf056f9ca99d6755_295_0.png)

图 9.18 KDE 的 KOrganizer 客户端支持编辑任务和时间表，你可以将其与 PDA 同步。此处还显示了通讯录。

## Linux 商用办公套件

除了前文提到的 StarOffice，Fedora 还有几种可用的商用办公套件。这些商用套件均未随 Fedora 提供。值得一提的是 Hancock Office：使用与 KDE 桌面相同的 QT 组件集，Hancock Office 在 Microsoft 文件格式兼容性方面得分较高。该套件包括文字处理器、电子表格演示工具和图形应用。Corel 曾为其 WordPerfect Office 2000 制作了 Linux 版本，但在停止发布新的 Linux 产品之前。它仍然提供支持页面，但软件已不再可用，功能优秀但已过时的 Linux 版 WordPerfect 8 也是如此。

## 专为 Microsoft Windows 编写的生产力应用

Microsoft Windows 与 Linux 有着根本的不同，但你可以使用名为 Wine 的应用程序在 Linux 中安装和运行一些 Microsoft Windows 应用程序。Wine 使你能在基于 UNIX 的系统上运行 Microsoft Windows 和 DOS 程序。它包含一个程序加载器，可用于执行 Windows 二进制文件，以及实现 Windows 命令调用的 .dll 库，将这些调用转换为等效的 UNIX 和 X11 命令调用。由于 Wine 代码库的频繁更新，Wine 未随 Fedora Core 提供。从 http://www.winehq.org/ 下载当前版本的 Wine。要查看你喜爱的应用程序是否受 Wine 支持，你可以查看位于 http://appdb.winehq.org/ appbrowse.php 的 Wine 应用数据库。

此外，还有其他解决方案可以实现使用 Microsoft 生产力应用，主要是 CodeWeavers 的 CrossOver Office。如果你希望以简便的方式运行不仅限于 Microsoft Office，还包括 Apple iTunes 和其他软件，你确实应该访问 CodeWeavers。CrossOver Office 是你可以使用来让基于 Windows 的程序运行的最简单的程序之一。访问 www.codeweavers.com 下载最新软件的试用版。它需要注册，但别担心——CodeWeavers 的工作人员很棒，不会滥用你的详细信息。最大的好处是，在你决定是否购买之前，你有整整一个月的时间来试用。当然，你可能会在 30 天结束时意识到 Linux 已经做到了你想要的，你不希望回到 Windows。不要害怕；大胆尝试吧！

## 相关 Fedora 命令

以下命令让你能够访问 Fedora 中的生产力应用、工具和进程：

- oowriter—OpenOffice.org 的 Writer
- oocalc—OpenOffice.org 的 Calc
- oaimpress—OpenOffice.org 的 Impress
- koshell—KDE 的 KOffice 办公套件外壳程序
- kspread—KDE 的 Kspread 电子表格
- gimp—GIMP（GNU 图像处理程序包）
- gnumeric—GNOME 的电子表格编辑器
- planner—GNOME 的项目管理客户端
- abiword—GNOME 的图形文字处理器

