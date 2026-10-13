
- 一组 C 函数，例如 `system` 和 `getenv`，应用程序可以使用它们来访问 shell 的特性
- 一组实用程序，如 `Perl` 和 `Tcp`，用于开发 shell 应用程序

# 第 1 章：Linux 概述

默认 shell 称为 `Bash`，代表 Bourne-Again Shell（再次 Bourne Shell）——这是对 Bourne shell 的引用，自 UNIX 早期以来它一直是标准的 UNIX shell。`Bash` 整合了 `IEEE 1003.2` 需要的许多特性并进行了扩展。在 Bourne shell 和 `IEEE 1003.2` 之间的任何差异中，为了更严格的 `IEEE 1003.2`，`Bash` 甚至有一个 `POSIX` 模式。

总而言之，`Linux` 是学习 UNIX 的良好平台，因为它提供了一个 UNIX 命令标准（`IEEE 1003.2` 标准，以及 `System V` 和 `BSD UNIX` 的最佳特性）。

`Linux` 对 `POSIX` 和其他常用 UNIX 系统调用（应用程序调用的函数）的支持使其成为极佳的软件开发系统。现代工作站软件的另一个要素 X 窗口系统也以 `X.Org X11` 的形式可用 `Linux` 中。

## Linux 标准基础 (LSB)

`Linux` 已经变得足够重要，以至于有一个针对 `Linux` 的标准称为 Linux 标准基础，简称 `LSB`，这是一组二进制标准，有助于减少不同发行版之间的差异并提高应用程序的可移植性。`LSB` 背后的理念是提供应用程序二进制接口 (`ABI`)，以便应用程序可以在任何符合 `LSB` 标准的 `Linux`（或其他 UNIX）系统上运行。`LSB` 规范引用了 `POSIX` 标准以及许多其他标准，如 `C` 和 `C++` 编程语言、`X` 窗口系统第11 版 (`X11RG`) 和文件系统层次结构 (`FHS`)。`LSB` 版本 1.2（通常称为 `LSB 1.2`）于 2002 年 6 月 28 日发布。`LSB 1.3` 于 2003 年 1 月推出，`LSB 2.0` 于 8 月 30 日发布。

`LSB` 规范分为部分——适用于所有架构的通用规范和针对每个架构的规范集。通用规范定义了所有符合 `LSB` 的系统必须满足的要求。特定架构规范为特定硬件的额外要求，例如 `x86`、`x64`、`SPARC` 和 `ARM`。符合 `LSB` 的系统必须满足通用规范和特定架构的要求。

### 第一部分：设置 Linux

#### 桌面

默认 shell 称为 `Bash`，代表 Bourne-Again Shell（再次 Bourne Shell）——这是对 Bourne shell 的引用，自 UNIX 早期以来它一直是标准的 UNIX shell。`Bash` 整合了 `IEEE 1003.2` 需要的许多特性并进行了扩展。在 Bourne shell 和 `IEEE 1003.2` 之间的任何差异中，为了更严格的 `IEEE 1003.2`，`Bash` 甚至有一个 `POSIX` 模式。

总而言之，`Linux` 是学习 UNIX 的良好平台，因为它提供了一个 UNIX 命令标准（`IEEE 1003.2` 标准，以及 `System V` 和 `BSD UNIX` 的最佳特性）。

`Linux` 对 `POSIX` 和其他常用 UNIX 系统调用（应用程序调用的函数）的支持使其成为极佳的软件开发系统。现代工作站软件的另一个要素 X 窗口系统也以 `X.Org X11` 的形式可用 `Linux` 中。

对于 GUI，`Linux` 包含了两个强大的图形桌面环境：`KDE` (`K Desktop Environment`) 和 `GNOME` (`GNU Network Object Model Environment`)。当你安装 `Linux` 时，你可以选择你想要的桌面，或者你可以安装两者并在它们之间切换。`GNOME` 和 `KDE` 提供了类似于 Microsoft Windows 和 Apple Mac OS 的桌面。`GNOME` 还带有 `Nautilus` 文件 shell，可以让你轻松地查找文件、运行应用程序并配置你的 `Linux` 系统。通过 `GNOME` 或 `KDE`，你可以开始使用你的 `Linux` 工作站而无需

来学习 UNIX 命令。然而，如果你以后需要使用 UNIX 命令，只需打开一个终端窗口并在 shell 提示符处输入命令即可。`Linux` 还带了许多在 X 之下运行的图形化应用程序。最值得注意的程序与图像显示和编辑有关。第一个是 `GIMP` —— GNU 图像操程序——一个功能与 Adobe Photoshop 媲美的程序；第二个程序是 `ImageMagick`。

X 窗口系统的另一个方面是，你可以在网络上运行应用程序，因为 X 使用了客户端/服务器架构。X 服务器运行在网络端，并控制桌面、键盘和鼠标。客户端请求被发送到 X 服务器，以接收用户输入和输出显示。你可能在网络上的某个服务器上运行应用程序，但在你的 `Linux` 桌面面上通过运行 X 的 GUI 与其交互。换句话说，X `Linux` 变成了通往网络上所有其他系统的网关。

`Motif` 是 UNIX 市场上的 GUI，但由于 Open Software 工具包是免费的，它并没有被捆装在 `Linux` 中。`Motif` 的外观和感觉与 Microsoft Windows 相似，并包含了 `Motif` 窗口管理器 (`MWM`) 和面向程序员的 `Motif` 工具包。你可以从 `www.motif.net/` 下载 `Linux` 版 OpenMotif。除了 Open Group 提供的 OpenMotif 外，`Motif` 的另一个选项是 `Lestif`，这是一个根据通用公共许可证（`GPL`）发布的 `Motif` 免费版本（访问 `www.lestif.org` 获取最新信息）。`Fedora Core` 带有 OpenMotif，如果你在安装过程中选择 X 软件开发包，它会自动安装。

如果你开发时需要 `Motif`，使用带有 OpenMotif 副本的 `Linux` 是搭建软件开发环境的极佳方法。如果你有业务需求，或者想在家里开发 X 和 `Motif`，那么 `Motif` 绝对是你的之选。

除了 `GNOME` 和 `KDE`，你可以在 `Linux` 中获得一些 GUI 应用。`GNOME` 带有 `GTK+`（GIMP 工具包），而 `KDE` 带有 `Qt` 工具包。如果你不想学习 `Motif`，可能希望为你的 GUI 应用使用 `Gtk` 或 `Qt`。

第 3 章将为你介绍如何设置 X 窗口系统。第 8 章介绍 `GNOME` 和 `KDE` 桌面。
