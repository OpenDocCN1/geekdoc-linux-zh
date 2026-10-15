
- KDE 使用来自挪威公司 Trolltech AS (http://www.troll.no/) 的 `Qt` 免费 GUI 工具包。`Qt` 是一个用于构建 GUI 的 C++ 类库；它提供了 KDE 应用程序中使用的菜单、按钮和滑块等控件。关于 `Qt` 许可证存在一些争议，因为其条款与 GNU 公许可证（GNU Public License）不同。然而，在 2000 年 9 月，Trolltech 宣布将根据 GNU 公许可证许可 `Qt 2.2` 版本。

## 270 第二部分：探索红帽 Linux

![](img/32dd492a14c1741062582e3caae7f04b_303_0.png)

**图 9-10：** 运行某些应用程序的 KDE Desktop

窗口菜单允许你执行各种操作，例如最大化或最小化窗口、更改大小以及切换到不同的桌面。当然，窗口边界也有其他按钮可以执行这些任务（例如窗口右上角的按钮）。

KDE 支持虚拟桌面。默认情况下，你可以点击标记为 One、Two、Three 和 Four 的按钮切换到特定的桌面。使用桌面来组织你的应用程序窗口。你不需要在单个桌面上堆满许多打开的窗口。当某个桌面变得拥挤时，只需切换到另一个桌面并打开应用程序即可。

KDE 面还包含一个图标为被 shell 覆盖的终端的按钮——图 9-9 是左起数第三个按钮。点击此按钮可以运行**控制台**（一个终端仿真程序）并获得终端窗口，如图 9-11 所示。

你可以在终端仿真窗口的 shell 提示符处输入 Linux 命令。第 7 章描述了 shell 和一些重要的 Linux 命令。

KDE 包含一个 KDE 控制中心，可以使用它来自定义 KDE 的各个方面，包括桌面背景、图标和字体。要启动 KDE 控制中心，选择 K Control Center；或者，从面板点击图标为电路板覆盖的显示器的按钮。KDE 控制中心的主窗口有两个部分。窗口左侧是树形菜单，你可以用该工具控制其中的项目。树形菜单按分类组织，例如外观与感觉（Look & Feel）、外设（Peripherals）、个性化（Personalization）等。点击项目以查看该项目的子分类。要更改项目，请通过树形菜单找到该项目；然后点击它。该项的配置随后将出现在窗口右侧的对话框中。例如，图 9-12 显示了自定义桌面背景的选项。

![](img/32dd492a14c1741062582e3caae7f04b_304_0.png)

图 9-11：在控制台终端仿真窗口中输入 Linux 命令

![](img/32dd492a14c1741062582e3caae7f04b_304_1.png)

图 9-12：使用 KDE 控制中心自定义桌面背景

## 第二部分：探索红帽 Linux

你可以选择你想要自定义背景的桌面。然后选择纯色背景或壁纸（用作背景的）。做出选择后，点击 OK 关闭对话框并应用更改。

要注销 KDE，选择 K -> Logout，并点击弹出对话框上的 Logout 按钮。

### 总结

无论是新手还是老手都能从图形化的点点用户界面中获益。本章向你展示了红帽 Linux 如何启动图形化登录界面，以便你可以留在图形环境中。本章还概述了 GNOME 和 KDE 图形用户界面，并解释了如何自定义 X 应用程序的外。下一章将向你介绍常见的 Linux 应用程序。

- *在 Linux 启动后，名为 `init` 的进程会启动所有其他进程。初始进程的精确集合取决于运行级别（run level），运行级别通常是 0 到 6 之间的数字。`/etc/initab` 文件指定了在每个运行级别启动的进程。`/etc/initab` 文件指定在运行级别 5 启动图形显示管理器。在红帽 Linux 中，GNOME 显示管理器（`gdm`）提供了图形化登录提示。红帽安装程序可以为你设置图形化登录。*

- *GNOME 和 KDE 是两种流行的 Linux GUI。红帽 Linux 同时带有 GNOME 和 KDE，但你的系统以 GNOME 作为默认 GUI 启动。你可以使用 `switchdesk` 工具将你的默认 GUI 更改为 KDE。*

- *GNOME 和 KDE 都与其他现代桌面环境相似，例如 Apple Macintosh 和 Microsoft Windows。因此，你可以轻松地学习使用 GNOME 和 KDE。它们都包含了控制中心，你可以通过控制中心自定义桌面的各个方面，包括外观。*

## 第 10 章

## Linux 应用程序与工具

### 本章内容

- 学习配套 CD-ROM 上的应用程序和工具
- 使用图形文本编辑器
- 使用办公工具，如 Gnumeric 电子表格、日历、计算器和拼写检查器
- 使用图形和成像应用程序
- 了解市售的办公应用程序

本书配套 CD-ROM 上的红帽 Linux 发行版包含了许多应用程序。GNOME 和 KDE 桌面带有许多应用程序，如日历、计算器、CD 播放器和游戏。红帽 Linux 还带有 GNU 软件包，其中包含了应用程序如 `GIMP`（用于处理图像）和 `Ghostview`（用于查看 PostScript 文件）。

更多 Linux 应用程序可以在互联网上或从各种 Linux 供应商处商业购买。本章简要描述了配套 CD-ROM 中包含的一些 Linux 应用程序。你还被介绍了几种未包含在配套 CD-ROM 中的 Linux 知名商业办公生产力应用程序。

## 配套 CD-ROM 上的应用程序

本书配套 CD-ROM 上的红帽 Linux 发行版包含了许多应用程序。GNOME 和 KDE 桌面带有许多应用程序，如日历、计算器、CD 播放器和游戏。红帽 Linux 还带有 GNU 软件包，包含了应用程序如 `GIMP`（用于处理图像）和 `Ghostview`（用于查看 PostScript 文件）。

表 10-1：CD-ROM 上的应用程序

| 类别 | CD-ROM 上的应用程序 |
| :--- | :--- |
| 编辑器 | GNU Emacs, JED, Joe, vim |
| 桌面 | GNOME, KDE |
| 办公工具 | AbiWord, 日历, Gnumeric, 计算器, 日历, 拼写检查器 |
| 工具 | bc, awk |
| 图形 | Gimp, Xfig, Gnuplot |
| Windows | (此处内容略) |
| 系统管理 | Nautilus, RPM |
| 互联网 | Pine, Net Communicator, Apache |
| 数据库 | PostgreSQL |
| 编程 | GCC, Python |
| 文本格式 | TeX |
| 游戏 | Chess, Mahjong, Sweeper, Snake |

表 10-1：CD-ROM 上的应用程序（续）

| 类别 | CD-ROM 上的应用程序 |
| :--- | :--- |
| 编辑器 | GNU Emacs, JED, Joe, vim, Binary Editor |
| 桌面 | GNOME, KDE |
| 办公工具 | AbiWord, 日历, Gnumeric, 计算器, 日历, 拼写检查器 |
| 工具 | bc, awk |
| 图形 | Gimp, Xfig, Gnuplot |
| Windows | (此处内容略) |
| 系统管理 | Nautilus, RPM |
| 互联网 | Pine, Net Communicator, Apache |
| 数据库 | PostgreSQL |
| 编程 | GCC, Python |
| 文本格式 | TeX |
| 游戏 | Chess, Mahjong, Sweeper, Snake |

## 第 10 章：Linux 应用程序与工具

你可以从 GNOME 或 KDE 桌面启动许多应用程序。每个桌面的主菜单提供了一系列供你选择的应用程序。

### 编辑器

配套 CD-ROM 上有以下文本编辑器：

- *GNU Emacs — 唯一的正版 Emacs*
- *JED — 一种类似 Emacs 的编辑器*
- *Joe — 一个命令类似于 WordStar 的文本编辑器*
- *Vim — 一种类似 vi 的编辑器*
- *GNOME 和 KDE 的 GUI 文本编辑器*
- *KDE Binary Editor — 用于二进制文件的图形编辑器*

### GNU Emacs

配套 CD-ROM 包含了 GNU Emacs 20.7 版本。GNU Emacs 是最著名的 GNU 产品之一，由自由软件基金会发行。该光盘包含了两个版本的 GNU Emacs：

- 完整版 GNU Emacs (`/usr/bin/emacs`)，它在 X 下运行并为编辑操作提供菜单。你必须安装 X 才能运行此版本。
- 一个版本 (`/usr/bin/emacs-nox`)，比完整版 GNU Emacs 小一些；提供相同的功能，但不支持 X。

你可以在 X 下的终端窗口输入 `emacs-nox` 来运行非 X 版本的 GNU Emacs。然而，非 X 版本主要供系统中没有安装 X 窗口系统的用户使用。

## JED

与其他几个免费提供的文本编辑器一样，该编辑器以其作者 John E. Davis 的命名命名。`JED` 是一个小巧但强大的类似于 GNU Emacs 的编辑器，它支持编辑模式并像 GNU Emacs 一样读取信息文件（info files）。`JED` 可以模拟其他文本编辑器，如 WordStar 和 VAX/VMS 系统的 EDT 编辑器。`JED` 的独特功能之一是你可以在 `JED` 中编辑二进制文件。

你可以在第二张配套 CD-ROM 的 `RedHat/RPMS` 目录下找到 `JED` 的 RPM 文件。

## Joe

配套 CD-ROM 包含了 2.9 版本的 Joe 编辑器。Joe 以其创建者 Joseph H. Allen 的命名。Joe 编辑器使用的命令与过去流行的 PC 文字处理器 WordStar 的命令相似。

你可以在第二张配套 CD-ROM 的 `RedHat/RPMS` 目录下找到 Joe 编辑器的 RPM 文件。

## Vim

`Vim` 是 Vi Improved（改进版 Vi）的缩写。正如其名所示，`Vim` 是标准 UNIX 文本编辑器 `vi` 的改进版本。配套 CD-ROM 包含了 5.8 版本的 Vim。除了标准的 vi 命令外，`Vim` 还包含许多新功能，包括多级撤销、命令行历史记录和文件名补全。

在 Red Hat Linux 中，当你运行 `vi` 编辑器时，你运行的就是 Vim。第 11 章将为你介绍如何使用 vi 编辑器。

## GUI 文本编辑器

两个 Linux 图形桌面——GNOME 和 KDE——都带有图形用户界面的 GUI 文本编辑器。

要尝试 GNOME 文本编辑器，请从 GNOME 桌面选择 Main Menu ➜ Applications ➜ edit。你可以通过点击工具栏上的“Open”按钮来打开文件。这将调出打开对话框。然后你可以更改目录并点击“OK”按钮选择要编辑的文件。

`edit` 编辑器会在窗口中加载文件。你可以打开多个文件并在编辑时在它们之间切换。图 10-1 显示了使用 gEdit 的典型编辑会话。

**图 10-1：** 使用 gedit 编辑多个文件

在这种情况下，编辑器有四个文件可以打开：`fstab`、`inittab`、`hosts` 和 **`modules.conf`**（全部来自 `/etc` 目录）。文件名显示在编辑器窗口工具栏下方的标签页上。你可以点击带有文件名的标签页在文件之间切换。

其余文本编辑步骤都是直观的。要输入新文本，点击定位光标并开始打字。你可以使用文本编辑区域上方工具栏上的按钮选择文本并复制或剪切。要将文本粘贴到文件的其他地方，定位光标并点击“Paste”按钮。

KDE 有三个文本编辑器：KDE 文本编辑器或 KATE、高级编辑器（Advanced Editor）和简单编辑器（Simple Editor）。所有这些编辑器都有相似的用户界面，但菜单有些不同。从 KDE 桌面，你可以通过选择 KDE ⇨ Text Editor 来启动 KEdit。要打开文本文件，从菜单中选择 File ⇨ Open。会弹出一个框。当你进入目标目录时，选择要打开的文件并点击“OK”按钮。KDE 文本编辑器随后打开文件并在窗口中显示其内容。

你可以以类似的方式使用 Advanced Editor 或 KATE 编辑文件。例如，要启动 Advanced Editor，选择 K ⇨ Advanced Editor。图 10-2 显示了 Red Hat Linux 系统上使用 Advanced Editor 编辑 `/etc/xinetd.conf` 文件。

KDE 编辑器也有一个工具栏，但按钮只显示图标。如果你不知道某个按钮的作用，将鼠标指针悬停在按钮上，就会出现带有帮助信息的弹出消息。

**图 10-2：** 使用高级编辑器编辑文件

## KDE 二进制编辑器

KDE Binary Editor 是一个用于二进制文件的十六进制编辑器。你可以使用 KDE Binary Editor 打开任何文件——文本或二进制——查看十六进制以及字符。要启动 KDE Binary Editor，在 KDE 桌面选择 Utilities -> Binary Editor（从 GNOME 桌面选择 Main Menu -> Utilities -> Binary Editor）。在 Binary Editor 窗口中选择 File -> Open。然后在 Binary Editor 中打开要编辑的文件 `/bin/bash`。例如，如图 10-3 所示，KDE Binary Editor 以分屏视图显示二进制文件的内容。左侧宽窗口显示每个字节的十六进制值（每个十六进制数字代表四位）。右侧窄窗口显示与字节对应的 ASCII 字符。如果字符不可打印，字节将显示为点（.）。

你可以从图 10-3 看到 Bash 的二进制文件包含 ELF 字符串。这意味着该文件是一个可执行文件（ELF 格式请见第 23 章）。此外注意文件包含一个共享库——`/lib/ld-linux.so`。你可能会发现通过 KDE 编辑器打开其他二进制文件很有趣。例如，如果你打开 GIF 图像，你会发现该文件以 GIF87a 开头。

| 8 位 | 127 | 有符号 32 位 | 179453647 | 十六进制 |
| :--- | :--- | :--- | :--- | :--- |
| 无符号 8 位 | 127 | 无符号 32 位 | 179453647 | 八进制 | 177 |
| 有符号 16 位 | 17791 | 32 位浮点数 | 1.30737E+04 | 二进制 | 0111111 |
| 无符号 16 位 | 17791 | 64 位浮点数 | 1.39613E-309 | | |

**图 10-3：** 在 KDE 二进制编辑器中编辑二进制文件

> 在使用二进制编辑器打开和查看可执行文件和库文件时，务必小心。记住，如果你不小心保存并保存了更改，可能会损坏二进制文件。

## 办公工具

本书的配套 CD-ROM 包含了一些办公工具，如日历、计算器和拼检查器。以下章节描述了这些办公工具中的几个：

- AbiWord——一个小型简单的文字处理器
- Gnumeric——一个电子表格程序
- 日历——ical 和 GNOME 日历
- 计算器——xcalc、GNOME 计算器和 KDE 计算器
- asell——拼检查器

## AbiWord

AbiWord 是一个简单的文字处理器。它是 AbiSource 项目（www.abisource.com/）开发的第一个开源桌面应用程序。要尝试 AbiWord，从 GNOME 面板选择 Main -> Programs -> Applications -> AbiWord。AbiWord 非常简单——它类似于 Microsoft Word 等文字处理器。例如，你可以在空白文档中输入文本、格式化文本并在完成后保存文本。图 10-4 显示了在 AbiWord 中准备的文档。

**图 10-4：** 在 AbiWord 中准备文档

# 第10 章：Linux 应用程序与实用程序

我不会解释如何使用 AbiWord，因为它非常简单。如果你需要，可以使用在线帮助。在 AbiWord 菜单中选择“帮助-> 目录”（Help->Contents）。这将启动 Mozilla，并以 HTML 文档的形式提供 AbiWord 的帮助（见图 10-5）。然后你可以点击链接查看特定的帮助信息。

图 10-5：Mozilla Web 浏览器中的 AbiWord 帮助信息

## Gnumeric 电子表格

GNOME 自带 Gnumeric —— 这是一个基于 X 的图形化电子表格程序。要尝试 Gnumeric，请从 GNOME 面板选择主菜单->程序->Gnumeric 电子表格。Gnumeric 程序会显示其主窗口，该窗口看起来与基于 Windows 的电子表格（如 Microsoft Excel）相似。（事实上，Gnumeric 能够读取和写入 Excel 95 格式的电子表格文件。）

像使用 Microsoft Excel 一样使用 Gnumeric。你可以在单元格中输入内容、使用公式并对单元格进行格式设置（例如指定类型和小数点后的位数）。图 10-6 显示了 Gnumeric 中一个典型的电子表格。

你可能想输入一个类似的电子表格。使用你通常在 Microsoft Excel 中使用的公式。例如，使用公式 `SUM(D2:D6)` 来加单元格 D2 到 D6 的内容。要将单元格 D2 设置为 A2 和 C2 内容的积，请使用 `=A2*C2`。要了解更多关于 Gnumeric 中可用函数的信息，请从菜单中选择“帮助-> Gnumeric 函数参考”。这将显示关于 Gnumeric 函数的信息，如图 10-7 所示。

图 10-6：Gnumeric 中一个典型的电子表格

图 10-7：在 Nautilus 中查看关于 Gnumeric 函数的信息

你可以浏览函数列表并点击某个函数以阅读更多关于它的信息。
