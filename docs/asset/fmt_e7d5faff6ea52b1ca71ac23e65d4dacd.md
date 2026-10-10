
对于基于 Windows 的个人电脑，两种流行的 X 服务器方案是来自 Starnet Communications 的 `X-Win32` 和 `X-Win32 Flash`。这两个系统都允许运行 Windows 操作系统（如 `Windows XP` 或 `Vista`）的计算机远程连接到运行 `UNIX/Linux` 的计算机。`X-Win32` 是加载到 PC 上的软件，而 `X-Win32 Flash` 则预装安装在插入 PC USB 端口的闪存驱动中。Windows PC 显示出带有窗口、菜单和其他特征的 X 窗口类型图形用户界面（GUI）。此外，远程连接通过 `SSH` 进行安全通信处理。你可以在 `www.starnet.com` 了解更多关于 `X-Win32` 和 `X-Win32 flash` 的信息。

另一个流行的 X 服务器是 Hummingbird Connectivity 提供的 `Exceed`。`Exceed` 旨在为 Windows 桌面用户提供对 `UNIX/Linux` 计算机的远程 GUI 访问。`Exceed` 还包含了使用 `NFS` 在系统之间共享资源的软件（参见第2章“探索 UNIX/Linux 文件系统和文件安全”）。访问 `connectivity.hummingbird.com/home/connectivity.html` 了解更多关于 `Exceed` 的信息。

![](img/0a988e998d76ede7c21a57edbc89e490_586_0.png)

# 使用窗口管理器

与 UNIX 操作系统本身一样，X 窗口系统是分层的并由组件构建。顶层是窗口管理器（`Window Manager`）。窗口管理器控制窗口如何出现以及用户如何控制它们。在许多方面，窗口管理器之于 X 窗口系统就像 shell 之于 UNIX/Linux：每个都为用户提供了一个与底层组件交互的界面。

已经开发了许多窗口管理器，大多数是免费提供的。Linux 支持超过 50 种不同的窗口管理器。表11-1 展示了 Linux 中常用的一些窗口管理器。

## 表11-1 常用窗口管理器

| 窗口管理器 | 描述 |
|---|---|
| AnotherLevel | 基于 `fwm` 窗口管理器，通常与某些红版 Linux 使用 |
| Blackbox | 一种为了速度编写的轻量或“极简主义”窗口管理器，旨在管理窗口（无图标或快捷方式） |
| CDE | 常用桌面环境，用于使用系统的各种大小计算机 |
| Enlightenment | 受欢迎的窗口管理器，有时称为 `E`；通常与 Fedora 和红版 Linux 使用 |
| FluxBox | 与 Blackbox 类似，并提供透明、窗口标签页和标题栏配置选项（完全兼容 KDE 并部分兼容 GNOME） |
| `fwm` | 虚拟窗口管理器，一个为 X 设计的全功能虚拟桌面和窗口系统 |
| `fwm95` | 具有 Windows 95 视觉效果和体验的 `fwm` 版本 |
| `gwm` | 通用窗口管理器（基于面向对象的语言 [WOOL]） |
| IceWM | 用 C++ 开发的窗口管理器，旨在追求速度并符合 GNOME 桌面标准 |
| `kwm` | KDE 使用的窗口管理器 |
| `olwm` | Open Look 窗口管理器，最初用于 Sun 计算机，但后来 Sun 切换到了 `mwm`、`CDE` 和 `GNOME` |
| Metacity | 由 Havel Pennington 为 Red Hat 开发的窗口管理器；用于 Red Hat 和 Fedora；与 GNOME 桌面集成 |
| `mwm` | Motif 窗口管理器，用于包括 Sun 计算机在内的某些商用 UNIX 系统 |
| Oroboros | 基于主题的窗口管理器 |
| sawfish | 与 LISP 编程语言兼容的窗口管理器，提供一个图标杂乱较少的桌面 |
| `twwm` | 标签窗口管理器或 Tom's Window 管理器 |
| Window Maker | 提供 GNUstep 桌面环境支持的窗口管理器 |

表11-1 所示的许多窗口管理器与下一节讨论的 X 窗口 `GNOME` 桌面兼容。这些窗口管理器包括 `Enlightenment`、`IceWM`、`fwm`、`fwm95`、`Metacity`、`Oboros`、`sawfish` 和 `Window Maker`。此外，还列出了三个“轻量级”窗口管理器：这些是为希望系统启动和运行更快、且通过启用较少选项来减少 GUI 资源的用户准备的。要了解更多这些和其他窗口管理器，请访问网站 `www.xwinman.org`。

# 使用桌面

当你在 UNIX/Linux 中使用 X 窗口系统和窗口管理器时，还会伴随着一个桌面。桌面提供了你使用的特定 GUI 外观、软件应用程序和其他资源。桌面与窗口管理器协同工作。

# 使用 GNOME

GNU 网络对象环境（`GNOME`，读作“guh-nome”）是 GNU 项目的一个产品，是一种配合窗口管理器使用的桌面环境。Fedora 和 Red Hat 默认安装它。GNU 项目是一个开发自由类 UNIX 操作系统的组织。Linux 内核用于许多发行版。该项目的网站为 `www.gnu.org`。你可以在 `www.gnu.org` 了解更多关于 `GNOME` 的信息。`GNOME` 被认为非常用户友好，在桌面上超过 `KDE`。除了其用户友好的方法外，`GNOME` 的受欢迎是因为有很多为它编写的应用，包括文件访问、办公软件和通用工具。

# 使用 KDE

`KDE` 是另一种流行的 `GNOME` 替代，也可以与 `GNOME` 一起安装。`KDE` 在国际上比 `GNOME` 更受欢迎，并提供了广泛的拖放功能。`KDE` 目前在美国的使用正在增加。与 Gnome 类似，`KDE` 旨在为 UNIX/Linux 用户提供类似于 Microsoft Windows 和 Mac OS 的图形化点击体验。两者都兼容 `X11` 以及各种窗口管理器——从而通过图标、窗口和其他图形特征导航 UNIX/Linux。

> 你可以通过 `KDE` 组织的网站 `www.kde.org` 了解 `KDE`。

![](img/0a988e998d76ede7c21a57edbc89e490_589_0.png)

# 启动窗口系统

如果你的系统没有自动启动 X 窗口系统，你可以从命令行使用 `startx` 命令启动它。

语法 `startx [-options]`

+ * 此命令启动 X 窗口系统。
