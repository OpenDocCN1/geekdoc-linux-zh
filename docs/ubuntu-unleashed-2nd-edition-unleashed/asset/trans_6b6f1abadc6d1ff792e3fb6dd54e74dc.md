

按下 Enter 后，你会看到 KOffice shell 的主窗口，如图 9.16 所示。左侧是代表所有可用的 KOffice 应用程序的图标。点击其中一个会启动一个对话框，用于打开现有文件或开始在新文件中工作。

![](img/e464b828c497c99e41f61d4c55f1c0db_228_0.png)

图 9.16 KDE 的 KOffice 提供了一个工作区办公套件环境，允许快速访问套件的各个组件。

你可以点击主窗口左侧的图标来启动 KWord 文字处理客户端、KSpread 电子表格程序以及其他组件。你也可以不使用 KOffice 工作区，直接从命令行启动各个客户端。例如，要使用 KWord，输入以下内容：

```
$ kword &
```

然后 KWord 会要求你为本次会话选择一个文档。图 9.17 所示的 KWord 客户端提供了强大的编辑功能，包括桌面出版。

KOffice 的 KSpread 客户端是一个功能齐全的电子表格程序，提供图表功能。与 KWord 一样，KSpread 也可以从命令行启动。在使用如下命令后，你会被要求选择文档类型（新文档或已有文档）：

```
$ kspread &
```

![](img/e464b828c497c99e41f61d4c55f1c0db_229_0.png)

图 9.17 KOffice 的 KWord 文字处理组件是一个复杂的基于框架的所见即所得编辑器，适用于轻量级桌面出版，支持多种格式，包括 WordPerfect。

KDE 在其 KOffice 及相关应用程序的集合中还包含其他生产力客户端。这些客户端包括地址簿、时间跟踪器、计算器、记事本和日程安排器。

一个流行的客户端是 KOrganizer，它提供任务、待办事项列表和带背景闹钟的预约的日视图、周视图、工作周视图和月视图。它内部还支持日记或日记功能，并且你可以将信息与你的 Palm Pilot 同步。你可以从 KDE 桌面面板的菜单或从命令行启动此客户端，如下所示：

```
$ korganizer &
```

图 9.18 显示了一个典型的 KOrganizer 窗口。

## 适用于 Linux 的商业办公套件

除了前面提到的 StarOffice 外，还有多个商业办公套件可用于 Ubuntu。这些商业套件均未随 Ubuntu 提供。其中值得注意的是 Hancom Office。使用与 KDE 桌面相同的 QT 小部件集，Hancom Office 在 Microsoft 文件格式兼容性方面得分很高。该套件包括文字处理器、电子表格演示工具和图形应用程序。Corel 在停止发布任何新的 Linux 产品之前曾为 Linux 生产了其 WordPerfect Office 2000 的版本。它仍然提供支持页面，但软件已不再可用，优秀的——但被低调提及的——WordPerfect 8 for Linux 也不再提供。

![](img/e464b828c497c99e41f61d4c55f1c0db_230_0.png)

图 9.18 KDE 的 KOrganizer 客户端支持编辑可与你的 PDA 同步的任务和日程安排。此处还显示了地址簿。

## 为 Microsoft Windows 编写的生产力应用程序

Microsoft Windows 与 Linux 在根本上不同，但你可以使用名为 Wine 的应用程序在 Linux 中安装并运行一些 Microsoft Windows 应用程序。Wine 使你能够在基于 UNIX 的系统上使用 Microsoft Windows 和 DOS 程序。Wine 包含一个程序加载器，可用于执行 Windows 二进制文件，以及一个 .dll 库，该库实现了 Windows 命令调用，将其转换为等效的 UNIX 和 X11 命令调用。由于 Wine 代码库频繁更新，Wine 未包含在 Ubuntu 中。从 http://www.winehq.org/ 下载 Wine 的当前版本。

要查看你喜爱的应用程序是否得到 Wine 支持，你可以查看 Wine 应用程序数据库 http://appdb.winehq.org/appbrowse.php。

此外，还有其他解决方案可启用 Microsoft 生产力应用程序的使用，主要是 CodeWeavers CrossOver Office。如果你想要一种无痛的方式不仅运行 Microsoft Office，还运行 Apple iTunes 和其他软件，你真的应该访问 CodeWeavers。CrossOver Office 是你可以用它让基于 Windows 的程序运行的最简单的程序之一。查看 http://www.codeweavers.com 下载最新软件的试用版。它需要注册，但不用担心——CodeWeavers 的人很棒，不会滥用你的信息。最大的优点是你有整整一个月的时间试用后再决定是否购买。它要求注册，但不用担心——CodeWeavers 的人很棒，不会滥用你的信息。最大的优点是你有整整一个月的时间试用后再决定是否购买。它

