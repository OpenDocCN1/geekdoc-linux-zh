
## Man 文档文件

你可以使用任何文本编辑器创建 Man 文档。你给文本文件命的名字就是文档或主题名称，并以节号作为扩展名。一个关于 `who` 的文档名称将是 `who.1`。在本文描述的示例中，文档是关于 `book` 的，节号为 I。它的名称是 `book.1`。

Man 文档组织成若干章节，顶部有一行运行标题。章节可以命名为任何名称。按照惯例，Linux 命令的 Man 文档被组织成几个章节，如 NAME、SYNOPSIS 和 DESCRIPTION。你可以根据需要拥有任意数量的章节，并给出你选择的名称。你创建的实际文档是一个带有适当宏的未格式化文本文件。一个 Man 文档至少需要两个宏：`TH` 和 `SH`。`TH` 提供显示在每页顶部的标题以及文档的章节号。你为每个章节标题使用 `SH` 宏。你可以根据需要添加更多宏，例如用于段落格式化的 `PP` 或用于缩进段落的 `IP`。Man 宏列于表 6 中。

### 表 6：创建在线文档的命令和宏

| 命令和选项 | 描述 |
| :--- | :--- |
| `man` | 手册文档可以搜索和显示在线文档。你可以创建自己的手册文档并指示它搜索这些文档。`man` 命令通过单词“man”后跟节号（如 `man1`）在章节目录中搜索文档。当你创建自己的手册时，请务必包含章节目录。 |
| `MANPATH` | Shell 特殊变量，存储命令自动搜索的路径名。你可以通过赋值添加新路径：<br>`MANPATH=$MANPATH:/HOME/man` |
| `Options` | 仅搜索指定章节用于手册文档：<br>`man -3 bookrec` |
| `-M directory-name` | 仅搜索指定目录用于手册文档：<br>`man -M HOME/man/bookrec` |

### 表 6：创建在线文档的命令和宏

| 命令和选项 | 描述 |
| :--- | :--- |
| `man command-name` | 搜索并显示在线文档。<br>`man who` |
| `MANPATH` | 仅搜索指定章节用于手册文档。<br>`MANPATH=$HOME/man` |
| `Options` | 仅搜索指定目录用于手册文档。<br>`man -M HOME/man/bookrec` |
| The Man Macros | 用于输入在线文档的运行标题。 |
| `.TH sec-name` | 用于输入章节标题。 |
| `.B word` | 用于加粗单词，如命令名。 |
| `.I word` | 用于斜体。 |
| `.PP` | 用于段落格式化。 |
| `.IP` | 用于缩进落。 |

developer.kde.org。此外，sourceforge.net 上开发着许多 Gnome 和 KDE 的开源项目。你可以在此处下载并检查你感兴趣的项目的源代码。你甚至可以在那里启动自己的项目。表 1 列出了若干 Gnome 和 KDE 的开发资源。

表 1：Gnome 和 KDE 开发资源
| 站点 | 描述 |
| :--- | :--- |
| developer.gnome.org | Gnome 开发网站，包括详细文档 |
| glade.gnome.org | Glade，GTK+ 用户界面构建器 |
| developer.kde.org | KDE 开发网站，包括详细文档 |
| www.kdevelop.org | 用于 KDE 的 KDevelop 集成开发环境 (IDE) |
| www.trolltech.com | QT 网站，包含 KDE 中使用的 QT 库以及 QT Designer 的文档 |
| www.sourceforge.org | 许多 Gnome 和 KDE 项目的开源开发网站 |

# Gnome 编程：Glade

Gnome 提供了一系列 Gnome GUI 工具库，开发者可以使用这些库来创建 Gnome 应用程序。如果程序使用了符合 Gnome 标准的按钮、菜单和窗口，则该程序可以符合 Gnome 标准。Gnome 应用程序使用了 Gnome、GTK 工具包、GTK 绘图包以及 GNU 库。有关这些库中包含的函数、定义和结构的详细说明，强烈建议使用 Gnome 网站（developer.gnome.org）上提供的详尽文档。“Documentation”部分包含了详细的教程、手册和参考资料，包括 Gnome、GTK 和 CDK API 的完整参考。

GTK+ 是 Gnome 应用程序所使用的控件集，其外观最初源于 Motif。控件集是桌面环境中可用的 GUI 对象集合。按钮、窗口和工具栏都属于控件。该控件集从零开始就为了性能和灵活性而设计。例如，按钮可以带有标签、图像或两者的任意组合。对象可以在运行时动态查询和修改。GTK+ 还包含一个主题引擎，允许用户更改使用这些控件的应用程序的外观和感受。同时，GTK+ 控件保持了轻量和高效。

GTK+ 控件在《库通用公共许可证》(LGPL) 下是完全免费的。LGPL 允许开发者将控件集作为自由软件使用。该控件集还提供了一套丰富的语言绑定，包括 C++、Perl、Pascal、Objective-C、Guile 和 Ada。它完全支持国际化，允许基于 GTK+ 的应用程序与其他字符集配合（如亚洲语言）。它还与其他支持这些协议的其他控件集（如 Qt 和 Motif）进行拖放操作。

为 Gnome 编写的程序本质上是包含 Gnome 和 GTK+ 函数的 C 语言程序。Gnome 和 GTK+ 函数处理程序的 Gnome 桌面操作。在为 Gnome 编程时，你将使用位于许多库中极其大量的函数和结构——这些函数和结构构成了进入 Gnome 应用程序的不同组件。

本章可以提供这些库的概概述，以及你如何使用它们来创建 Gnome 程序。虽然 Gnome 不像 Tk 那样易于使用，但在 Gnome 中编程只需要使用少数函数即可创建简单的用户界面。你可以将 GTK+ 函数看作低级操作，将 Gnome 看作易于使用的高级操作。Gnome 函数通常整合了 GTK+ 函数，使得 GUI 任务的编程变得相对简单。一个 Gnome 程序本质上是一个带有 GTK+ 函数的 C 程序，本章将从讨论 GTK+ 编程开始然后然后 Gnome 程序。

Gnome 库提供了 Gnome 应用程序中使用的最高级函数。在其下方是 GTK 库。GTK+ 是为 GNU 图像处理程序（GIMP）开发的工具包（GTK+ 由 GIMP 工具包 (GTK) 和 GIMP 绘图包 (GDK) 库组成）。

GTK 包含了管理控件和用户界面任务的函数和结构。在任何 Gnome 程序中都可以访问这些函数和结构。事实上， Gnome 应用程序是一个带有 Gnome 库函数的 GTK 程序。GTK 函数和结构是 C++ 程序对象，都设计用于用于 C++ 风格的程序。

GDK 包含了用于连接 GTK 到 Xlib 库的低级函数。Xlib 库持有执行实际 X 系统操作的函数。GTK 和 Gnome 还使用了 Glib 库提供的标准 C 函数。表 2 列出了不同的 Gnome 组件。

表 2：Gnome 组件
| Gnome 组件 | 描述 |
| :--- | :--- |
| Gnome 库 | 包含高级 Gnome 函数 |
| GTK (GIMP Tool Kit) | 包含控件和 GUI 函数 |
| GDK (GIMP Drawing Kit) | 为 Xlib 提供低级封装 |
| Xlib | 提供 X 窗口操作 |
| Glib | 包含标准函数的 Gnu C 库 |

Gnome 应用程序还使用了 ORBit 和 Imlib（图像库）。Gnome 使用通用对象请求架构 (CORBA)，它允许软件组件相互连接，无论它们是用何种计算机语言实现的，或者运行在何种机器上。Gnome 的 CORBA 实现被称为 ORBit。通过 ORBit，程序可以定位并请求服务，即使该对象跨越网络。例如，编辑器可以向 ORBit 请求一个电子表格。Imlib 包含了处理各种格式图像的函数，允许在程序中显示、缩放、保存和加载图像。

# Gnome 库

Gnome 库使得 Gnome 应用程序能够具有相同的 GUI 界面。虽然 Gnome 应用程序是一个带有 Gnome 库函数的 GTK 程序，但 Gnome 库提供了若干 GTK+ 不包含的高级操作。表 3 列出了 Gnome 库。

| 库 | 描述 |
| :--- | :--- |
| libaudiofile | 读取多种音频格式（AIFF, AISC, WAV）。 |
| libimlib | 包含多种格式（JPEG, GIF, TIFF, PNG, XPM, PPM, BMP）。 |
| libgtk | 这是 GTK 工具包。Gnome 应用程序使用 libgtk 创建 GUI 元素（按钮、菜单、滚动条等）。 |
| libnome | 包含 Gnome 环境的程序，用于配置、帮助、管理 MIME 类型和会话。此库不依赖于任何 GUI 工具包。 |
| libnomeui | 扩展 GTK+ 以创建对话框和消息框、菜单栏、状态行等。它还包含了用于对话框、菜单项和按钮的图标，并提供了用于创建复杂界面（如地址簿、日历程序和电子表格）的 Gnome 画。这是一个依赖库。 |
| libnorba | 用于 ORBit CORBA 的库。 |
| libzvt | 包含终端控件的库。 |
| libart_lgpl | 包含用于 GnomeCanvas 的图形函数。 |

`Gnome` 和 `libnomeui` 是任何 Gnome 应用程序的主要库。Gnome 是一组设计不依赖于特定 GUI 工具包的函数。这些函数可以任何类型的程序，无论是带有命令行界面还是没有界面。这些函数不依赖于特定的 GUI 工具包。`libnome` 库包含了提供 GUI 界面操作的函数。这些操作绑定到特定的 GUI，例如 GTK。可以创建一个绑定到所需 GUI 工具包的 `libnome` 库。

`libnome` 库提供了许多与 Gnome 桌面环境相关的实用程序。提供的功能包括用于应用程序存储持久化数据的配置文件支持、元数据支持（附加到文件对象的数据，如特定文件类型显示的图标）以及将帮助文档加载到 Gnome 帮助浏览器的支持。还提供了一个接口，使 Gnome 应用程序与 Gnome 会话管理器通信。最后，还有用于配置不同 MIME

由 Gnome 和 Gnome 文件管理器处理。表 4 列出了其中一些功能。

| Gnome 库函数类别 | 描述 |
|---|---|
| gnome-config | 提供对配置值的简单访问。 |
| gnome-defs | 包含用于 C++ 连接的 Gnome 定义。 |
| gnome-exec | 允许从 Gnome 应用执行程序。 |
| gnome-help | 包含显示帮助的例程。 |
| gnome-history | 跟踪最近使用的文档。 |
| gnome-i18n | 提供本地化和国际化支持。 |
| gnome-mime-info | 获取 MIME 类型信息的例程。 |
| gnome-paper | 包含纸张尺寸和单位转换。 |
| gnome-popt | 命令行参数解析器。 |
| gnome-regex | 包含正则表达式缓存实现。 |
| gnome-sound | 包括 Gnome 应用的声音例程。 |
| gnome-triggers | 包含应用程序事件的层级搜索机制。 |
| gnome-url | 允许根据 URL 启动文档查看器。 |
| gnome_lib | 初始化 gnome 库。 |

libgnome 库包含了为应用程序创建 Gnome 用户界面所需的函数和结构，这些结构与 GTK+ 控件集绑定， Gnome 可以轻松地创建对话框和消息框，以及菜单栏、工具栏和状态行。为程序员提供了大量的库存图标，供其在对话框、菜单项和按钮中使用，由于所有 Gnome 应用都使用 `libgnome` 创建这些常用的 GUI 元素，因此视觉一致性得到了保证。在许多方面与 Tk 画布类似，Gnome 画布为创建地址框、日历应用程序和电子表格提供了框架。

GUI 应用需要大量使用图像来创建友好舒适的用户界面。传统上，将所有常用的图形格式加载到 X11 应用中非常困难。libgtk 库通过提供强大的函数来加载多种文件格式（JPEG, GIF, TIFF, PNG, XP, PPM, PGM, PBM 和 BMP）解决了这个问题。文件被转换为内部 24 位 RGB 表示，并存在实用函数来缩放以及将 RGB 渲染为各种颜色深度（如果需要，带有抖动）。输入图像由 libgtk 内部缓存，以提高重复使用图像的应用程序性能。

`libgtk` 是 GTK 工具包库。这是一个专业级的控件集，在许多方面优于其他控件集。Gnome 应用完全使用 `gtk` 编写所有 GUI 元素（按钮、菜单、滚动条等）。`libgnorba` 库为 CORBA 操作提供支持，例如获取对象的引用和请求对象的新实例。Libzvt 是包含终端控件的简单库。Libart_lgpl 拥有可以与 GnomeCanvas 控件使用的图形函数。

# GTK+

GTK+ 包含了一系列用于各种类型控件的函数，例如菜单、按钮和窗口。它还支持将 GUI 函数（如鼠标点击）与对象（如按钮）关联起来。请访问 www.gtk.org 和 developer.gnome.org 网站查看 GTK API 的在线文档。该文档包含了所有 GTK 函数的完整列表，以及一个关于 GTK 编程的详细教程。强烈建议你利用这些文档——由于尺寸限制，本书只能介绍介绍并列出常用的 GTK 函数和结构，还请检查 GTK 头文件以获取不同函数和返回值的详细声明。

任何 GTK 程序都包含基础的函数和组件。你首先需要至少包含 `gtk.h` 头文件。根据你使用的控件和函数，可能需要其他 GTK 头文件。然后，你需要定义指向要定义和使用的窗口的指针。接着，使用 `gtk_init` 函数初始化 GTK 库。完成后，你可以使用 GTK 函数定义你的控件，并将它们的地址分配给之前定义的指针。然后，你可以使用 GTK 函数为控件指定动作和属性，例如显示它们。例如，一个关闭框（delete_event）连接到窗口和 `gtk_main_quit` 函数，这样用户点击窗口的框时，程序就会结束。最后，你使用 `gtk_main` 函数运行控件。

以下 `base.c` 程序定义了一个简单的 GTK 程序，显示一个：

```c
```
