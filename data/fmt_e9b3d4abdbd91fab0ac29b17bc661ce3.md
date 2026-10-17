
在所有运行 NIS 客户端程序的机器上安装 `ybind` 软件包（包含在 `y-tools` 软件包中）。如果你需要一个 NIS 服务器，你还需要在你的网络上的某台机器上安装 `yp` 软件包。

### ypserv (Version 1.3.6.1, 289K)

网络信息服务 (NIS) 是一个为网络上所有机器提供网络信息（登录名、备注、家目录、用户组信息）的系统。只要机器上运行着 NIS 客户端程序，且用户的密码记录在 NIS passwd 数据库中，NIS 允许用户登录到网络上的任何机器。NIS 曾被称为 Sun 黄页服务 (YP)。

此软件包提供了 NIS 服务器，该服务器需要在你的网络上运行。NIS 客户端不需要运行该服务器。

如果你的网络需要一个 NIS 服务器，请安装 `ypserv`。你还需要在任何 NIS 客户端上安装 `yp-tools` 和 `ybind` 软件包。

## D.6.3 内核

本节包含与 Red Hat Linux 基础的内核相关的软件包。

### kernel – (Version 2.2.5, 9,812K)

该软件包包含 Linux 内核 (`vmlinuz`)，它是 Red Hat Linux 操作系统的核心。内核处理操作系统的基本功能：内存分配、进程分配、设备输入输出。

### kernel-BOOT (Version 2.2.5, 5,881K)

此软件包包含一个精简版的 Linux 2.2.5 内核。该内核用于安装启动盘，不应用于安装服务器，因为由于尺寸限制，该内核中的许多功能都被关闭了。

### kernel-pcmcia-cs – (Version 2.2.5, 561K)

许多笔记本电脑（以及某些非笔记本电脑）支持使用 PCMC 卡进行扩展。PCMC 卡也称为“卡适配器”，是为现代系统提供 SCSI 支持的微型设备。PCMC 卡支持热插拔（即在不重启系统的情况下即可进行交换），且使用方便。`kernel-pcmcia` 软件包包含一组可加载的内核模块，它们实现了一个应用程序接口、一组针对特定卡的客户端驱动程序以及一个管理器守护进程，该守护进程可以根据需要加载和卸载来响应卡的插入和移除。该守护进程还支持交换，因此可以随时安全地插入和弹出卡。

如果你的系统使用 PCMC 卡，请安装 `kernel-pcmcia-cs` 软件包。

### kernel-smp - (Version 2.2.5, 9,494K)

此软件包包含 SMP 版本的 Linux 2.2.5 内核。它仅在具有两个或多个 CPU 的机器上需要，尽管在单 CPU 机器上也可以正常工作。

### modutils - (Version 2.1.121, 841K)

`modutils` 软件包包含了用于 2.0 内核下自动加载模块以及 2.0 和 2.2 内核下卸载模块的内核程序，以及其他模块管理程序。

加载和卸载的模块是设备驱动程序、文件系统以及其他内容。

## D.6.4 库

本节包含与 Red Hat Linux 下运行程序所需的库相关的软件包。

### XFree86-libs - (Version 3.3.3.1, 2,060K)

XFree86 包含了大多数 X 程序正常运行所需的共享库。这些共享库位于在单独的软件包中，以减少在没有运行 X 服务器的机器（即通过网络）上运行 X 应用程序所需的磁盘空间。

如果你在机器上安装 X Window 系统，你将需要安装 `XFree86-libs`。你还需要安装 `XFree86` 软件包、`XFree86-75dpi-fonts` 软件包或 `XFree86-100dpi-fonts` 软件包（取决于你的分辨率）、`Xconfigurator` 软件包以及 `X11R-contrib` 软件包。此外，如果你打算开发作为 X 客户端运行的应用程序，你还需要安装 `XFree86-dev`。

### Xaw3d - (Version 1.3, 292K)

Xaw3d 是针对 X Window 系统的 MIT Athena 组件集的扩展。Xaw3d 能够在极少或不更改源代码的情况下为应用程序添加三维视觉效果。

如果你正在使用包含 MIT Athena 组件的应用程序，并且想为这些应用程序创建 3D 效果，那么你应该安装 `Xaw3d`。

### audiofile - (Version 0.1.6, 183K)

处理各种音频文件格式的库。由声音进程使用。

### cracklib - (Version 2.7, 75K)

CrackLib 测试密码以确定其是否符合某些安全导向的特征。你可以使用 CrackLib 防止用户选择易猜的密码。CrackLib 执行以下测试：

- 它从用户名和 gecos 条目创建单词，并检查这些单词与密码的匹配情况；
- 它检查简单的模式。

## D 系统环境

如果你计划使用 GIMP 或其他使用 GTK+ 的程序，你需要安装 `gtk+` 包。

### gtk+10 – (版本 1.0.6, 1,139K)

这些库最初是为 GIMP 编写的，现在也被其他几个程序使用。

此 RPM 是一组运行链接到 `gtk+` 1.0 系列和 `gl` 的应用程序所需的兼容性库。

### gtk-engines – (版本 0.5, 2,387K)

这些是各种 GTK+ 工具包主题的图形化引擎。包含的主题有：

- Notif
- Redmond95
- Pixmap
- Metal (类似 swing)

### imlib – (版本 1.9.4, 423K)

Imlib 是一个与显示深度无关的图像加载和渲染库。Imlib 旨在简化并加速加载图像以及获取 X Window 绘图的过程。Imlib 提供了许多简单的操作程序，可用于常用操作。

如果你为 X11 需要图像加载和渲染库，请安装 `imlib`。你可能还想安装 `imlib-cfeditor` 包，它将帮助你配置 `imlib`。

### imlib-cfeditor – (版本 1.9.4, 333K)

`imlib-cfeditor` 包包含 `imlib.config` 程序，你可以用它来配置 `imlib` 图像加载和渲染库。`Imlib.config` 可用于控制 `imlib` 如何使用颜色以及处理伽马校正等。

如果你正在安装多个程序，也应该安装 `imlib.cfeditor`。

### kdebinds – (版本 1.1, 5,771K)

用于 KDE 桌面面的库：KDE 库包括：`kdecore` (KDE 核心库), `kdeui` (用户界面), `kfm` (文件管理器), `khtml` (HTML 小部件), `kfile` (文件访问), `kspell` (拼写检查器), `jscript` (javascript), `kab` (地址簿), `kimgio` (图像管理器), `mediool` (声音、混合和动画)。

### kdesupport – (版本 1.1, 2,138K)

K 桌面面的支持库，但并非其一部分。

包含的库：`QtSpriteView`, `j` (javascript), `ubit`, `mlibib`, `red`：取决于 Red Hat 的版本，`dbmpeg` 和 `jpg` 库将被包含，或者需要 Red Hat 提供的版本。

此包还为 Red Hat Linux 提供了额外的 KDE 支持：一个名为 `"ukdesk"` 的脚本，用户运行它可以可以将 KDE 设置为默认桌面（在创建新用户时自动完成），以及用于激活 KDE X 显示管理器 `"kdm"` 以替换 `"xdm"` 的脚本。

### libPropList – (版本 0.8.3, 111K)

PL 的目的是紧密模拟 GNU/OPENSTEP 中使用的属性列表（它们由 SSString, NSData, NSArray 和 NDictionary 类组成）的行为并保持完全兼容。

### 软件包列表

ILib 允许使用配置或偏好文件的程序能够使这些配置/偏好与 GNUstep/-OPENSTEP 的用户默认处理机制兼容，而无需使用 Objective-C。

### libc - (版本 5.3.12, 5,259K)

旧的 Linux 系统（包括 2.0 到 4.2 之间的 Red Hat Linux 版本）基于 `libc` 版本 5。此 `lib` 包包含了基于 `libc` 版本 6 的其他库。安装这些库后，旧应用程序将能够在 `glibc` 系统上运行。

`lib` 包应该安装，以便运行需要 `lib` 版本 5 的应用程序。

### libelf - (版本 0.6,4,76K)

`libelf` 包包含一个访问 ELF 对象文件的库。`Libelf` 允许你访问 ELF 文件格式的不同部分。

如果你需要访问 ELF 对象文件，则应该安装 `libelf`。

### libhttp - (版本 1.0.2, 85K)

用于制作 HTTP 1.1 请求的库。

### libgr - (版本 2.0.13, 235K)

`libgr` 包包含处理图形文件格式的库：`.pbm`（便携位图）, `.pgm`（便携灰度图）, `.ppm`（便携映射）, `.ppm`（便携位图）等。

### libtop - (版本 1.0.1, 431K)
