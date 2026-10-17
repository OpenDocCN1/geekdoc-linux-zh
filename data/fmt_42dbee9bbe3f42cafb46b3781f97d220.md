
尽管是用 `ANSI C` 开发的，但其他语言提供了 `GNOME` 和 `GTK+` 库的包装器。大多数语言都有包装器，包括 `Ada`、`Scheme`、`Python`、`Perl`、`Dylan`、`Objective-C` 和 `C++`。

## 注意

`GNOME` 使用了 `GNOME`、`GTK+` 工具包、`GDK` 绘图包以及 `GNU` 库。有关这些库包含的函数、定义和结构的详细描述，强烈建议你使用 `GNOME` 开发者网站 (`developer.gnome.org`) 上提供的详尽文档。该文档包含了详细的教程、手册和参考资料，包括 `GNOME`、`GTK` 和 `GDK` API 的完整参考。

为在 `GNOME` 上运行编写的程序本质上是包含 `GNOME` 和 `GTK+` 函数的 `C` 程序。`GNOME` 和 `GTK+` 函数负责处理程序的 `GNOME` 桌面操作。在为 `GNOME` 编程时，你将使用包含许多库的极其丰富的函数和结构——这些函数和结构组成了 `GNOME` 应用的不同组件。

本模块只能提供这些库的概括介绍，以及你如何使用它们来创建 `GNOME` 程序。虽然 `GNOME` 不像 `Tk` 那么简单，但在 `GNOME` 中编程只需要使用少数函数即可创建简单的用户界面。你可以将 `GTK+` 视为底层操作，将 `GNOME` 函数 视为易于使用的高层操作。`GNOME` 函数通常整合了多个 `GTK+` 函数，使得 `GUI` 任务的编程变得相对简单。`GNOME` 程序本质上是一个带有 `GTK+` 函数以及 `GNOME` 函数的 `C` 程序。因为基础的 `GNOME` 操作由 `GTK+` 函数处理，因此本模块从基础 `GTK+` 编程开始，然后讨论 `GNOME` 程序。

`GNOME` 库提供了 `GNOME` 应用中最高级函数。在其下方是 `GTK+` 库。`GTK+` 是为 `GNU` 图像处理程序 (`GIMP`) 开发的工具包。

# Linux 编程入门指南

`GTK+` 由 `GIMP` 工具包 (`GTK`) 和 `GIMP` 绘图包 (`GDK`) 库组成。`GTK` 包含了管理小部件和界面任务的函数和结构。这些函数和结构可以在任何 `GNOME` 程序中直接访问。事实上，一个 `GNOME` 应用是一个带有 `GNOME` 库函数的 `GTK` 程序。`GTK` 函数和 `C++` 程序对象都被设计为用于 `C++` 风格的程序。`GDK` 包含了用于连接 `GTK` 到 `Xlib` 库的底层函数。`Xlib` 库持有执行实际 `X Window` 系统操作的函数。`GTK` 和 `GNOME` 也使用了由 `Glib` 库提供的标准 `C` 函数。表 9-1 列出了不同的 `GNOME` 组件。

## 1 分钟训练

- `GNOME` 使用的是什么种的小部件集？

- `GNOME` 代表什么？

| GNOME 组件 | 描述 |
|---|---|
| GNOME 库 | 包含高层 GNOME 函数 |
| GTK (GIMP Tool Kit) | 包含小部件和 GUI 函数 |
| GDK (GIMP Drawing Kit) | 为 Xlib 提供低层包装 |
| Xlib | 提供 X 窗口系统操作 |
| Glib | 包含 GNU C 库的标准函数 |

# 表 9-1 GNOME 组件

- `GTK+`

- `GNU` 网络对象模型环境

# 第 9 模块：GNOME

## GNOME 库

`GNOME` 库使得 `GNOME` 应用能够具有相同外观和感受的相同 `GUI` 界面。虽然一个 `GNOME` 应用是一个带有 `GNOME` 库函数的 `GTK` 程序，但 `GNOME` 库提供了几个复杂的高层小部件，以及许多 `GTK+` 库未包含的简单操作。表 9-2 列出了 `GNOME` 库。

`libgnome` 和 `libgnoui` 是任何 `GNOME` 应用需要的两个主要库。`libgnome` 是一组设计为独立于任何特定 `GUI` 工具包的函数。这些函数可以用于任何类型的程序，无论是只有命令行界面还是没有界面的程序。这些函数独立于任何特定的 `GUI` 工具包。`libgnoui` 库包含了提供 `GUI` 操作的函数。这些函数绑定到特定的 `GUI` 工具包，例如 `GTK`。可以创建一个绑定到不同 `GUI` 工具包的 `libgnome` 库。

| 库 | 描述 |
|---|---|
| libgtk | 这是 GTK 工具包库。GNOME 应用完全使用 libgtk 编写所有 GUI 元素（按钮、菜单、滚动条等）。 |
| libgnome_imlib | 包含用于加载多种文件格式（JPEG, GIF, TIFF, PNG, XPM, PPM, PGM, PBM 和 BMP）的函数。 |
| libgnome | 包含用于 GNOME 桌面环境的实用程序，例如配置、帮助、管理 MIME 类型和管理会话的程序。此库独立于任何 GUI 工具包。 |
| libgnoui | 包含对 GTK+ 小部件集的工具包扩展，用于创建对话框和消息框、菜单栏、工具栏、状态行等。它还包含了用于对话框、菜单条目和按钮的图标；并提供了 GNOME 画布，以便于创建复杂的界面，如地址簿、日历应用程序和电子表格。 |
| liborba | 一个使用 ORBIT CORBA 的库。 |
| libvt | 包含终端的库。 |
| libart | 包含用于 GNOME 的图形函数。 |

# Linux 编程入门指南

`libgnome` 提供了许多与 `GNOME` 桌面环境相关的实用程序。提供的功能包括应用程序存储持久化数据的支持、对元数据的支持（附加到文件对象，例如显示文件的图标）以及将帮助文档加载到 `GNOME` 浏览器的支持。还提供了一个接口让 `GNOME` 应用与会话管理器通信。最后，还有配置 `GNOME` 和文件管理器处理不同类型的程序。其中一些函数列在表 9-3。

`libgnoui` 库包含了为你的应用程序创建 `GNOME` 用户界面所需的函数和结构，这些函数绑定到 `GTK` 工具包。该库是 `GTK+` 小部件集的扩展，程序员可以轻松创建对话框和消息框，以及菜单栏、工具栏和状态行。提供了大量的内置图标供程序员在对话框、菜单条目中使用，由于所有 `GNOME` 应用都使用 `libgnome` 创建这些常用的 `GUI` 元素，视觉一致性在许多方面（相对于 `GNOME` 画布）得到了保证。

# GNOME 函数分类

| | 描述 |
|--- | --- |
| gnome-config | 提供配置值的简单访问 |
| gnome-defs | 包含用于 C++ 链接的 GNOME 定义 |
| gnome-exec | 允许 GNOME 应用执行程序 |
| gnome-help | 包含显示帮助的程序 |
| gnome-history | 最近使用的文档 |
| gnome-i18n | 提供本地化和国际化支持 |
| gnome-mime-info | 包含获取绑定到 MIME 的程序 |
| gnome-paper | 包含纸张尺寸和打印单位转换 |
| gnome-popt | 命令行参数解析器 |
| gnome-regex | 包含正则表达式缓存的实现 |
| gnome-sound | 为 GNOME 应用提供的音频播放程序 |
| gnome-triggers | 包含用于应用程序事件的分级信号机制 |
| gnome-url | 允许根据 URL 启动查看器 |
| gnome-lib | 初始化 libgnome 库 |

表 9-3 GNOME 库 (libgnome)

# 第 9 模块：GNOME 315

为创建地址录、日历应用程序和电子表格提供了一个框架。在此库中可以找到的各种函数如表 9-4 所示。

`GUI` 应用程序大量使用图像来创建友好舒适的用户界面。传统上，将所有常见的图形文件格式加载到 `X11` 应用程序是非常困难的。`libdk_imlib` 通过提供方便且强大的工具来加载多种文件格式（`JPEG`, `GIF`, `TIFF`, `PNG`, `XPM`, `PPM`, `PGM`, `PBM` 和 `BMP`）解决了这个问题。这些文件被转换为内部的 `24` 位 `RGB` 表示，并存在相应的实用函数来执行缩放，以及将从 `24` 位 `RGB` 渲染到各种其他颜色深度（如果需要，可以使用抖动处理）。`libdk_imlib` 在内部缓存输入图像，以提高反复使用图像的应用程序的性能。

# 用户接口函数分类

| 描述 | |
| :--- | :--- |
| gnome-app-helper | 启用简化菜单和工具栏的创建 |
| gnome-app-util | 包含操作 GnomeApp 容器小部件的实用函数 |
| gnome-canvas-util | 包含辅助画布函数 |
| gnome-dialog-util | 为制作对话框提供便利函数 |
| gnome-dns | 提供非阻塞名称解析接口 |
| gnome-geometry | 包含窗口几何结构实用函数 |
| gnome-icon-text | 包含用于图标说明的文本换行函数 |
| gnome-init | 初始化 GNOME 库 |
| gnome-mdi-session | 包含提供 GnomeMDI 状态保存和恢复的程序 |
| gnome-popup-help | 包含 GtkWidgets 的弹出帮助系统 |
| gnome-popup-menu | 包含将弹出菜单附加到小部件的程序 |
