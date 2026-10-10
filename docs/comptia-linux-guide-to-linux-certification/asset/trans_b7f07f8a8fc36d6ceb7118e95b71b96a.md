
systemctl 命令。以下命令显示所有 Systemd 服务及其状态（dead 表示当前未运行）：

```
[root@server1 ~]# systemctl -a | grep service | less
abrt-ccpp.service       loaded active  exited    Install ABRT coredump
abrt-oops.service        loaded active  running   ABRT kernel log watcher
abrt-vmcore.service      loaded active  exited    Harvest vmcores for ABRT
abrd.service            loaded active  running   ABRT Automated Bug Repo
acpid.service            loaded active  running   ACPI Event Daemon
alsa-store.service       loaded inactive dead     Store Sound Card State
arp-ethers.service       loaded inactive dead     Load static arp entries
atd.service             loaded active  running   Job spooling tools
auditd.service            loaded active  running   Security Auditing
avahi-daemon.service      loaded active  running   Avahi mDNS/DNS-SD Stack
crond.service           loaded active  running   Command Scheduler
cups.service            loaded active  running   CUPS Printing Service
dbus-org.bluez.service  error inactive dead      dbus-org.bluez.service
dbus.service            loaded active  running   D-Bus System Message Bus
:
```

您可以通过使用 systemctl 命令的 status 参数来查看特定 Systemd 守护程序的详细信息。例如，`systemctl status crond.service` 将显示关于 cron 守护程序的详细信息。

若要配置某个 Systemd 守护程序在默认目标（例如，graphical.target）中启动，您可以使用 systemctl 命令的 enable 参数。例如，为了确保在系统初始化时启动 cron 守护程序，您可以运行 `systemctl enable crond.service` 命令。或者，`systemctl disable crond.service` 将防止在系统启动时启动 cron 守护程序。

systemctl 命令还可以用于在目标之间切换。您可以通过运行 `systemctl isolate multi-user.target` 或 `systemctl isolate runlevel3.target` 命令切换到 multi-user.target（类似于运行级别 3）。或者，您可以通过运行 `systemctl isolate graphical.target` 或 `systemctl isolate runlevel5.target` 命令切换到 graphical.target（类似于运行级别 5）。

## X Windows 系统

在本章中，到目前为止，我们一直专注于使用登录字符终端后获得的 BASH shell 命令行界面来执行任务。尽管大多数管理员更喜欢命令行界面，但 Linux 用户通常使用图形用户界面 (GUI) 来运行用户程序。因此，您需要了解组成 Linux GUI 的组件。特别是，您需要了解如何启动、停止和配置这些组件。

### Linux GUI 组件

Linux GUI 旨在无论计算机系统中安装的是什么视频适配卡和显示器，都能保持一致的功能。它由许多组件组成，每个组件都独立于视频硬件工作。

![](img/c27875544958897d817484d558c208c8_398_0.png)

**图 8-8** Linux GUI 组件

![](img/c27875544958897d817484d558c208c8_398_1.png)

图形程序可以通过使用 dbus 守护程序在任何 X Windows 环境中直接相互通信，或者通过 hald 守护程序与硬件设备通信。

Linux 安装通常包括图 8-8 中列出的所有 GUI 组件。在一起，这些 GUI 组件和相关程序在典型的 Linux 安装中使用超过 4GB 的存储空间。

**X Windows** Linux GUI 的核心组件是 **X Windows**，它提供了在终端屏幕上显示的窗口中绘制图形图像的能力。告诉 X Windows 如何绘制图形并显示结果的那些程序被称为 **X 客户端**。X 客户端不需要与 X Windows 运行在同一台计算机上；您可以通过更改第 7 章中讨论的 DISPLAY 环境变量，使用一台计算机上的 X Windows 将图形图像发送到完全位于另一台计算机上的 X 客户端。因此，X Windows 有时被称为 X Windows 的服务器组件，或简称为 **X 服务器**。

X Windows 由 Digital Equipment Corporation (DEC) 和麻省理工学院 (MIT) 于 1984 年联合开发。当时，它被命名为雅典娜项目（Project Athena），并在 1985 年作为 X Windows 发布，希望找到一个新名字来取代 X。不久之后，许多 UNIX 供应商都请求使用 X Windows；到 1988 年，MIT 发布了 X Windows 的 11 版本 2 版（X11R2）。自 1988 年以来，X Windows 由开放组织（The Open Group）维护，该组织在 1995 年发布了 X Windows 的 11 版本 6 版（X11R6）。自 2004 年以来，X Windows 由 **X.org 基金会**作为开源软件维护。

![](img/c27875544958897d817484d558c208c8_398_2.png)

若要了解有关 X Windows 的更多信息，请访问 X.org 基金会网站 www.x.org。

直到最近，X Windows 还由与 GPL 不同的许可证管理，这限制了 X Windows 及其源代码的使用。因此，开源开发者在 1990 年代创建了 X Windows 的开源版本。这个自由可用的 X Windows 版本在许多 Linux 发行版中使用，并被称为 XFree86，因为它最初是为 Intel x86 平台设计的。

![](img/c27875544958897d817484d558c208c8_399_0.png)

若要了解有关 XFree86 的更多信息，请访问 XFree86 项目 www.xfree86.org。

如今，Linux 发行版提供 X Windows 或 XFree86 实现的 X Windows，因为两者都是开源软件。Fedora 20 和 Ubuntu 14.04 使用 X Windows 而不是 XFree86。

### 窗口管理器和桌面环境

若要修改 X Windows 的外观和感觉，您可以使用窗口管理器。例如，在图形屏幕上绘制的窗口的尺寸和颜色，以及在图形屏幕上移动窗口的方法，都是窗口管理器的功能。

Linux 有许多不同的窗口管理器可供选择，包括表 8-4 中列出的那些。

| 窗口管理器 | 描述 |
|---|---|
| Compiz Fusion | 一个高度可配置和可扩展的窗口管理器，基于 Compiz 和 Beryl 窗口管理器，利用现代视频卡上的 3D 加速来产生 3D 图形效果，包括 3D 窗口行为和桌面立方体工作区。 |
| enlightenment | 一个高度可配置的窗口管理器，允许具有不同设置的多桌面。它通常由 GNOME 桌面使用。 |
| fvwm | 一个基于 twm 的窗口管理器，使用更少的计算机内存，并为桌面提供 3-D 外观；其全称为“Fvwm 虚拟窗口管理器”。 |
| kwin | 用于 KDE 桌面的窗口管理器。 |
| lxde | 一个专门为性能较低的系统和旧式计算机（如上网本、移动设备）设计的窗口管理器；其全称为“轻量级 X 桌面环境”。 |
| metacity | GNOME 版本 1 和 2 桌面环境使用的默认窗口管理器。 |
| mutter | GNOME 版本 3 桌面环境使用的默认窗口管理器。 |
| mwm | 一个基本的窗口管理器，允许用户使用标准 X 实用工具进行配置；其全称为“Motif 窗口管理器”。 |
| sawfish | 一个通常用于 GNOME 桌面的窗口管理器。它允许用户通过工具或脚本配置大多数设置。 |
| twm | 最古老和最基础的窗口管理器之一；其全称为“Tab 窗口管理器”。 |
| wmaker | 一个提供拖放鼠标移动并模仿 Apple Computer, Inc. 制作的 NextSTEP 操作系统界面的窗口管理器；其全称为“Window Maker”。 |

表 8-4 常见窗口管理器

您可以单独使用窗口管理器，也可以将其与桌面环境结合使用。

桌面环境是一组标准 GUI 工具，设计为打包在一起，包括 Web 浏览器、文件管理器和绘图程序。桌面环境还提供了开发工具集，称为工具包（toolkits），可加速创建新软件的过程。正如本书前面所讨论的，Linux 上最常用的两个桌面环境是 K 桌面环境（KDE）和 GNU 对象模型环境（GNOME）。

KDE 是在 Linux 系统上使用的传统桌面环境。KDE 最初由 Matthias Ettrich 于 1996 年发布，使用 K 窗口管理器（kwin）和 C++ 编程语言的 Qt 工具包。

![](img/c27875544958897d817484d558c208c8_400_0.png)

若要了解有关 KDE 的更多信息，请访问 www.kde.org。

KDE 中包含的 Qt 工具包由挪威一家名为 Trolltech 的公司于 1990 年代创建。然而，由于当时大多数开源开发者更喜欢使用 C 编程语言而不是 C++ 进行开发，因此花费了一段时间才建立起用户基础。此外，Qt 直到 1998 年才作为开源软件发布，这是一个缺点，因为大多数开发者更喜欢可自由修改的源代码。

由于普遍对 Qt 工具包的不满，GNOME 桌面环境于 1997 年创建。最新版本的 GNOME 使用 mutter 窗口管理器和 C 编程语言的 GTK+ 工具包。GTK+ 工具包最初是为 GNU 图像处理程序（GIMP）开发的；与 GIMP 一样，它是开源的。GNOME 是大多数 Linux 发行版上的默认桌面环境。

![](img/c27875544958897d817484d558c208c8_400_1.png)

若要了解有关 GNOME 的更多信息，请访问 www.gnome.org。

代替使用 KDE 或 GNOME 桌面环境中的默认窗口管理器，您可以配置 KDE 或 GNOME 使用不同的窗口管理器。一个流行的选择是 Compiz Fusion，它需要具有基于硬件的 3D 加速支持的现代视频卡。安装 Compiz Fusion 后，您可以使用相关实用工具配置其功能和高级图形效果。Compiz Fusion 的基本功能允许用户通过在使用鼠标滚轮时按住 Ctrl+Alt 键来控制窗口透明度；它还允许用户通过在使用光标键时按住 Ctrl+Alt 键来在立方体效果中旋转四个桌面显示。

![](img/c27875544958897d817484d558c208c8_400_2.png)

若要了解有关 Compiz Fusion 的更多信息，包括其图形效果和附加插件，请访问 www.compiz.org。
