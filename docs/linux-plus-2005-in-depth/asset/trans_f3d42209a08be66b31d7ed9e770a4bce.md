

这就好比工具包让木匠能更快地完成项目一样。正如本书前面所讨论的，Linux 上最常用的两种桌面环境是 **K 桌面环境（KDE）** 和 **GNU 对象模型环境（GNOME）**。

KDE 是 Linux 系统上使用的传统桌面环境；它由 Matthias Ettrich 于 1996 年发起，使用 **K 窗口管理器** (kwin) 和用于 C++ 编程语言的 **Qt 工具包**。图 9-12 展示了一个典型的 KDE 桌面屏幕。

![](img/09bf13b782f71165e17bb3839040c96a_373_0.png)

### 图 9-12 KDE 桌面

![](img/09bf13b782f71165e17bb3839040c96a_373_1.png)

Qt 工具包由挪威一家名为 Trolltech 的公司创建，不幸的是，直到 1998 年它才作为开源软件发布。在 20 世纪 90 年代中期，大多数开源开发者更喜欢使用 C 编程语言而不是 C++ 进行开发。他们也不喜欢当时 Qt 工具包的源代码可以自由修改这一点。因此，**GNOME 桌面环境** 于 1997 年被创建。GNOME 通常使用 **Metacity 窗口管理器** 和用于 C 编程语言的 **GTK+ 工具包**。GTK+ 工具包最初是为 **GNU 图像处理程序（GIMP）** 开发的，和 GIMP 一样，它是开源的。GNOME 桌面是 Red Hat Fedora Linux 的默认桌面，如图 9-13 所示。

![](img/09bf13b782f71165e17bb3839040c96a_374_0.png)

> 注意
> 要了解有关 GNOME 桌面的更多信息，你可以访问互联网上的 http://www.gnome.org。

尽管不如 GNOME 和 KDE 常见，但 **Xfce 桌面环境**（图 9-14）是许多 Linux 系统上使用的另一种桌面环境。Xfce 附带了一小组易于使用的工具，并且比 KDE 或 GNOME 消耗更少的硬件资源。因此，Xfce 通常运行在硬件资源有限的 Linux 服务器上。

> 注意
> 要了解有关 Xfce 桌面的更多信息，你可以访问互联网上的 http://www.xfce.org。

尽管桌面环境对于如今的 Linux 用户来说很普遍，但你可以选择仅使用 **窗口管理器**。Linux 上有许多不同的窗口管理器，例如图 9-15 中所示的 **Tab 窗口管理器**。表 9-4 列出了一些其他常见的窗口管理器。

![](img/09bf13b782f71165e17bb3839040c96a_375_0.png)

### 图 9-14 *Xfce 桌面*

![](img/09bf13b782f71165e17bb3839040c96a_375_1.png)

### 图 9-15 *Tux 窗口管理器*

#### 表 9-4 常见的窗口管理器

| 窗口管理器 | 描述 |
| :--- | :--- |
| enlightenment | 一个高度可配置的窗口管理器，允许使用具有不同设置的多桌面。它通常被 GNOME 桌面使用。 |
| fvwm | 虚弱虚拟窗口管理器。它基于 Tab 窗口管理器，但旨在使用更少的计算机内存并赋予桌面 3D 外观。 |
| kwin | 用于 KDE 桌面的窗口管理器。 |
| metacity | 用于 Red Hat Fedora Core 2 中 GNOME 桌面的窗口管理器。它允许用户配置自定义主题，以修改桌面的外观和感觉。 |
| mwm | Motif 窗口管理器。它是一个基本的窗口管理器，允许用户使用标准 X 实用程序进行配置设置。 |
| sawfish | 一个常用于 GNOME 桌面的窗口管理器。它允许用户通过工具或脚本配置其大多数设置。 |
| twm | Tab 窗口管理器。它是古老且最基本的窗口管理器之一。 |
| wmaker | window maker 窗口管理器。它提供拖放鼠标移动功能，并模拟 Apple Computer, Inc. 制作的 NeXTSTEP 操作系统界面。 |

> 注意
> 窗口管理器和桌面环境不是命令行界面的替代品。因此，几十个终端程序在窗口管理器或桌面环境内部提供命令行界面。这些终端程序通常使用 termcap 数据库 (/etc/termcap) 或 terminfo 数据库 (/usr/share/terminfo/*) 中的设置进行配置。GNOME 和 KDE 桌面中的默认终端包含执行管理和用户任务所需的所有功能；然而，其他终端（如之前 Tab 窗口管理器（图 9-15）中显示的 xterm 终端）可能需要在某些系统进行特殊配置才能正确显示文本。

## 启动和停止 X Windows

必须存在某种方法来启动 X Windows、窗口管理器以及桌面环境（如果使用）。回想本章前面提到的，运行级别 5 启动 GNOME 显示管理器 (gdm) 以显示图 9-16 中描绘的图形登录屏幕。

![](img/09bf13b782f71165e17bb3839040c96a_377_0.png)

### 图 9-16 *GNOME 显示管理器*

此登录屏幕允许用户在登录系统并启动 X Windows 之前，从会话菜单中选择使用的桌面环境或窗口管理器。

> 注意
> 你可以导航到 GNOME 或 KDE 桌面中的系统设置，登录屏幕，或编辑 /etc/X11/gdm/gdm.conf 文件来配置 **gdm** 的外观和行为。

**gdm** 是 **X 显示管理器 (xdm)** 的一个变体，它为用户显示基本的图形登录。此外，其他 Linux 发行版可能使用 **KDE 显示管理器 (kdm)** 来显示 KDE 风格的图形登录。

然而，如果你使用运行级别 3 而不是运行级别 5，你可以在字符终端中输入 **gdm** 来手动启动 **GNOME** 显示管理器，或者使用 `startx` 命令来启动 X Windows 以及在你的主目录中 `.Xclients` 文件指定的窗口管理器或桌面环境。如果该文件不存在，则默认启动 GNOME 桌面环境。如果该文件存在，它通常指向主目录中的 `.Xclients-default` 文件，如下面的输出所示：

```
[root@localhost root]# cat .Xclients
#!/bin/bash
# Created by Red Hat Desktop Switcher
if [ -e "$HOME/.Xclients-$HOSTNAME:$DISPLAY" ]; then
    exec $HOME/.Xclients-$HOSTNAME:$DISPLAY
else
    exec $HOME/.Xclients-default
fi
[root@localhost root]# cat .Xclients-default
# Created by Red Hat Desktop Switcher
exec gnome-session
[root@localhost root]# _
```

从上述输出中可以看出，`.Xclients-default` 文件包含一行，执行 `gnome-session` 命令，该命令进而启动 Metacity 窗口管理器和 GNOME 桌面，位于 X Windows 之上。类似地，要在 X Windows 上启动其他桌面或窗口管理器，你可以编辑 `.Xclients-default` 文件并将 `gnome-session` 一词更改为 `startkde`（启动 KDE 桌面）、`startxfce4`（启动 Xfce 桌面）或 `/usr/X11R6/bin/twm`（启动 Tab 窗口管理器）。

`.Xclients-default` 文件中使用设置也可以通过 GNOME 或 KDE 桌面环境中的图形 **桌面切换工具** 设置；只需导航到 Red Hat 按钮，首选项，更多首选项，桌面切换工具。此工具的一个示例如图 9-17 所示。

![](img/09bf13b782f71165e17bb3839040c96a_378_0.png)

## 配置 X Windows

X Windows 是 GUI 中计算机与视频硬件接口的组件。为了使 X Windows 执行其功能，它需要有关键盘、鼠标、显示器和视频适配卡的信息。一些 X Windows 配置实用程序要求你指定这些组件的具体硬件信息，而其他实用程序自动检测大部分甚至所有组件。因此，在配置 X Windows 之前，你应该收集所有这些设备的硬件信息。对于键盘和鼠标，你应该记录其类型和型号。对于视频适配卡，X Windows 可能需要以下信息：

- 视频适配卡的型号
- 视频适配卡上的 RAM 数量
- 视频适配卡上的 **芯片组**（可能与型号相同）

X Windows 可能还需要有关连接到视频适配卡的计算机显示器的以下信息：

- 支持的 **最大分辨率**
- 水平同步 (hsync) 范围
- 垂直同步 (vsync) 范围

如果你的系统使用 X Windows 的 X.org 实现，鼠标、键盘、显示器和视频适配卡的信息以文本格式存储在 `/etc/X11/xorg.conf` 文件中。如果你的系统使用 X Windows 的 XFree86 实现，此信息则存储在 `/etc/X11/XF86Config` 文件中。你可以手动编辑这些文件，或使用程序间接编辑它们。

![](img/09bf13b782f71165e17bb3839040c96a_379_0.png)

如果你计划手动编辑 X Windows 配置文件，请确保先阅读其相关手册或 info 页。对于 Red Hat Fedora Core 2，请确保阅读 xorg.conf 手册页。

因为 `/etc/X11/xorg.conf` 或 `/etc/X11/XF86Config` 文件中的一个错误可能会阻止 GUI 运行，所以使用配置程序编辑这些文件是个好习惯。

要在 Red Hat Fedora Linux 中配置鼠标，你可以使用 GUI 或终端环境中的 **mouseconfig** 或 **system-config-mouse** 命令。在终端环境中，这些命令显示一个类似于图 9-18 中描绘的屏幕。

