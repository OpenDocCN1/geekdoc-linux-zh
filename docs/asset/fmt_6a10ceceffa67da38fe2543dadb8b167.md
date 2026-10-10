
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

您可以通过使用`systemctl`命令的`status`参数来查看特定`Systemd`守护程序的详细信息。例如，`systemctl status crond.service`将显示关于`cron`守护程序的详细信息。

若要配置某个`Systemd`守护程序在默认目标（例如，`graphical.target`）中启动，您可以使用`systemctl`命令的`enable`参数。例如，为了确保在系统初始化时启动`cron`守护程序，您可以运行`systemctl enable crond.service`命令。或者，`systemctl disable crond.service`将防止在系统启动时启动`cron`守护程序。

`systemctl`命令还可以用于在目标之间切换。您可以通过运行`systemctl isolate multi-user.target`或`systemctl isolate runlevel3.target`命令切换到`multi-user.target`（类似于运行级别 3）。或者，您可以通过运行`systemctl isolate graphical.target`或`systemctl isolate runlevel5.target`命令切换到`graphical.target`（类似于运行级别 5）。

## X Windows 系统

在本章中，到目前为止，我们一直专注于使用登录字符终端后获得的`BASH` shell 命令行界面来执行任务。尽管大多数管理员更喜欢命令行界面，但 Linux 用户通常使用图形用户界面 (`GUI`) 来运行用户程序。因此，您需要了解组成 Linux `GUI` 的组件。特别是，您需要了解如何启动、停止和配置这些组件。

### Linux GUI 组件

Linux `GUI` 旨在无论计算机系统中安装的是什么视频适配卡和显示器，都能保持一致的功能。它由许多组件组成，每个组件都独立于视频硬件工作。

![](img/c27875544958897d817484d558c208c8_398_0.png)

**图 8-8** Linux GUI 组件

![](img/c27875544958897d817484d558c208c8_398_1.png)

图形程序可以通过使用`dbus`守护程序在任何`X Windows`环境中直接相互通信，或者通过`hald`守护程序与硬件设备通信。

Linux 安装通常包括图 8-8 中列出的所有 `GUI` 组件。在一起，这些 `GUI` 组件和相关程序在典型的 Linux 安装中使用超过 4GB 的存储空间。

`X Windows` Linux `GUI` 的核心组件是 `X Windows`，它提供了在终端屏幕上显示的窗口中绘制图形图像的能力。告诉 `X Windows` 如何绘制图形并显示结果的那些程序被称为 `X 客户端`。`X` 客户端不需要与 `X Windows` 运行在同一台计算机上；您可以通过更改第 7 章中讨论的`DISPLAY`环境变量，使用一台计算机上的 `X Windows` 将图形图像发送到完全位于另一台计算机上的 `X` 客户端。因此，`X Windows` 有时被称为 `X Windows` 的服务器组件，或简称为 `X 服务器`。

`X Windows` 由 `Digital Equipment Corporation (DEC)` 和麻省理工学院 (`MIT`) 于 1984 年联合开发。当时，它被命名为雅典娜项目（`Project Athena`），并在 1985 年作为 `X Windows` 发布，希望找到一个新名字来取代 `X`。不久之后，许多 `UNIX` 供应商都请求使用 `X Windows`；到 1988 年，`MIT` 发布了 `X Windows` 的 11 版本 2 版（`X11R2`）。自 1988 年以来，`X Windows` 由开放组织（`The Open Group`）维护，该组织在 1995 年发布了 `X Windows` 的 11 版本 6 版（`X11R6`）。自 2004 年以来，`X Windows` 由 `X.org 基金会`作为开源软件维护。

![](img/c27875544958897d817484d558c208c8_398_2.png)

若要了解有关 `X Windows` 的更多信息，请访问 `X.org` 基金会网站`www.x.org`。

直到最近，`X Windows` 还由与 `GPL` 不同的许可证管理，这限制了 `X Windows` 及其源代码的使用。因此，开源开发者在 1990 年代创建了 `X Windows` 的开源版本。这个自由可用的 `X Windows` 版本在许多 Linux 发行版中使用，并被称为`XFree86`，因为它最初是为 `Intel x86` 平台设计的。

![](img/c27875544958897d817484d558c208c8_399_0.png)

若要了解有关 `XFree86` 的更多信息，请访问 `XFree86` 项目`www.xfree86.org`。

如今，Linux 发行版提供 `X Windows` 或 `XFree86` 实现的 `X Windows`，因为两者都是开源软件。`Fedora 20` 和 `Ubuntu 14.04` 使用 `X Windows` 而不是 `XFree86`。

### 窗口管理器和桌面环境

若要修改 `X Windows` 的外观和感觉，您可以使用窗口管理器。例如，在图形屏幕上绘制的窗口的尺寸和颜色，以及在图形屏幕上移动窗口的方法，都是窗口管理器的功能。

Linux 有许多不同的窗口管理器可供选择，包括表 8-4 中列出的那些。

| 窗口管理器 | 描述 |

|---|---|

| `Compiz Fusion` | 一个高度可配置和可扩展的窗口管理器，基于`Compiz`和`Beryl`窗口管理器，利用现代视频卡上的 3D 加速来产生 3D 图形效果，包括 3D 窗口行为和桌面立方体工作区。 |

| `enlightenment` | 一个高度可配置的窗口管理器，允许具有不同设置的多桌面。它通常由`GNOME`桌面使用。 |

| `fvwm` | 一个基于`twm`的窗口管理器，使用更少的计算机内存，并为桌面提供 3-D 外观；其全称为“Fvwm 虚拟窗口管理器”。 |

| `kwin` | 用于`KDE`桌面的窗口管理器。 |

| `lxde` | 一个专门为性能较低的系统和旧式计算机（如上网本、移动设备）设计的窗口管理器；其全称为“轻量级 X 桌面环境”。 |

| `metacity` | `GNOME` 版本 1 和 2 桌面环境使用的默认窗口管理器。 |

| `mutter` | `GNOME` 版本 3 桌面环境使用的默认窗口管理器。 |

| `mwm` | 一个基本的窗口管理器，允许用户使用标准 `X` 实用工具进行配置；其全称为“Motif 窗口管理器”。 |

| `sawfish` | 一个通常用于`GNOME`桌面的窗口管理器。它允许用户通过工具或脚本配置大多数设置。 |

| `twm` | 最古老和最基础的窗口管理器之一；其全称为“Tab 窗口管理器”。 |

| `wmaker` | 一个提供拖放鼠标移动并模仿`Apple Computer, Inc.`制作的`NextSTEP`操作系统界面的窗口管理器；其全称为“Window Maker”。 |

表 8-4 常见窗口管理器

您可以单独使用窗口管理器，也可以将其与桌面环境结合使用。

桌面环境是一组标准 `GUI` 工具，设计为打包在一起，包括 Web 浏览器、文件管理器和绘图程序。桌面环境还提供了开发工具集，称为工具包（`toolkits`），可加速创建新软件的过程。正如本书前面所讨论的，Linux 上最常用的两个桌面环境是 K 桌面环境（`KDE`）和 `GNU` 对象模型环境（`GNOME`）。

`KDE` 是在 Linux 系统上使用的传统桌面环境。`KDE` 最初由 `Matthias Ettrich` 于 1996 年发布，使用 K 窗口管理器（`kwin`）和 `C++` 编程语言的`Qt`工具包。

![](img/c27875544958897d817484d558c208c8_400_0.png)

若要了解有关 `KDE` 的更多信息，请访问`www.kde.org`。

`KDE` 中包含的`Qt`工具包由挪威一家名为`Trolltech`的公司于 1990 年代创建。然而，由于当时大多数开源开发者更喜欢使用 `C` 编程语言而不是 `C++` 进行开发，因此花费了一段时间才建立起用户基础。此外，`Qt` 直到 1998 年才作为开源软件发布，这是一个缺点，因为大多数开发者更喜欢可自由修改的源代码。

由于普遍对`Qt`工具包的不满，`GNOME` 桌面环境于 1997 年创建。最新版本的 `GNOME` 使用`mutter`窗口管理器和 `C` 编程语言的`GTK+`工具包。`GTK+` 工具包最初是为`GNU` 图像处理程序（`GIMP`）开发的；与`GIMP`一样，它是开源的。`GNOME` 是大多数 Linux 发行版上的默认桌面环境。

![](img/c27875544958897d817484d558c208c8_400_1.png)

若要了解有关 `GNOME` 的更多信息，请访问`www.gnome.org`。

代替使用`KDE`或`GNOME`桌面环境中的默认窗口管理器，您可以配置`KDE`或`GNOME`使用不同的窗口管理器。一个流行的选择是`Compiz Fusion`，它需要具有基于硬件的 3D 加速支持的现代视频卡。安装`Compiz Fusion`后，您可以使用相关实用工具配置其功能和高级图形效果。`Compiz Fusion` 的基本功能允许用户通过在使用鼠标滚轮时按住`Ctrl+Alt`键来控制窗口透明度；它还允许用户通过在使用光标键时按住`Ctrl+Alt`键来在立方体效果中旋转四个桌面显示。

![](img/c27875544958897d817484d558c208c8_400_2.png)

若要了解有关 `Compiz Fusion` 的更多信息，包括其图形效果和附加插件，请访问`www.compiz.org`。

## 启动和停止 X Windows

正如本章前文所述，当`init`守护进程启动至运行级别 5 或`graphical.target`时，会启动一个名为`gdm`的程序，该程序会显示图形登录屏幕。如果在`gdm`中点击某个用户账户并选择设置图标，你就可以从已安装桌面环境或窗口管理器的列表中进行选择，如图 8-9 所示。

`GNOME` 显示管理器是 `X` 显示管理器（`xdm`）的一个变体，它为使用者显示基本的图形登录界面。此外，某些 Linux 发行版使用`KDE` 显示管理器（`kdm`）来为用户显示`KDE` 风格的图形登录界面。

![](img/c27875544958897d817484d558c208c8_401_0.png)

在`Fedora 20`上，`GNOME` 显示管理器启动的默认桌面环境是`GNOME`。然而，当你以特定用户身份登录并通过“会话”菜单选择`KDE`后，除非你做出其他选择，否则`GNOME` 显示管理器将继续使用`KDE`作为该用户账户的默认桌面环境。

`GNOME` 显示管理器是登录并访问系统中可用桌面环境的最简单方式。但是，如果你使用运行级别 1（或`rescue.target`）或运行级别 2 到 4（`multiuser.target`），`GNOME` 显示管理器默认不会启动。在这种情况下，你可以在字符终端中输入`startx`来启动`X Windows` 以及默认窗口管理器或桌面环境（例如`Fedora 20`中的`GNOME`）。

![](img/c27875544958897d817484d558c208c8_401_1.png)

图 8-9 在 `Fedora 20` 的 `GNOME` 显示管理器中选择会话

## 配置 X Windows

`X Windows` 是 `GUI` 中负责与计算机视频硬件交互的组件。为了执行其功能，`X Windows` 需要关于键盘、鼠标、显示器和显卡的信息。默认情况下，`X Windows` 尝试自动检测这些信息。如果自动检测失败，你可能需要手动指定正确的硬件信息。

如果你使用`XFree86`，`X Windows` 将其所有配置存储在文件`/etc/X11/XF86Config`中。你可以手动编辑此文件，也可以使用如`xf86config`等配置程序。如果你使用`X.org`，`X Windows` 将其配置存储在文件`/etc/X11/xorg.conf`中。同样，你可以手动编辑此文件，或使用配置程序进行编辑。

![](img/c27875544958897d817484d558c208c8_402_0.png)

在修改`XF86Config`或`xorg.conf`文件之前，请先阅读相关手册页的内容。

![](img/c27875544958897d817484d558c208c8_402_1.png)

你也可以在某些 Linux 发行版上使用`xdpyinfo`命令来显示`X Windows` 配置。

在`Fedora 20`中，`Xorg` 设置是自动检测的，而不是手动配置的。虽然`Fedora 20` 默认没有`/etc/X11/xorg.conf`文件，但如果存在该文件，它会被使用。相反，用户自定义的设置存储在`/etc/X11/xorg.conf.d`目录下的文件中，而诸如显示分辨率等常用设置可以通过`GNOME` 桌面环境中的“显示”实用工具进行修改。为此，只需在`GNOME` 中导航到“活动”、“显示应用”、“设置”，点击“显示”，然后选择你的显示器以查看可用设置，如图 8-10 所示。

![](img/c27875544958897d817484d558c208c8_402_2.png)

**图 8-10** 选择显示分辨率

![](img/c27875544958897d817484d558c208c8_403_0.png)

![](img/c27875544958897d817484d558c208c8_403_1.png)

键盘布局在`Fedora 20` 安装过程中自动检测。但是，如果你更改了键盘且`X Windows` 无法检测其布局，你可以在桌面环境内的终端提示符处或命令行终端中手动运行`system-config-keyboard`命令来启动键盘选择工具。参见图 8-11。

配置`X Windows`后，你可以使用桌面环境中的`xvidtune`实用工具来微调垂直刷新率（`vsync`）和水平刷新率（`hsync`）设置。只需在桌面环境中打开一个命令行终端并输入`xvidtune`来启动该工具，如图 8-12 所示。

虽然当今大多数显示器支持广泛的`hsync`和`vsync`值，但将任一值设置得过高可能会损坏显示器。另一方面，选择过低的`hsync`或`vsync`值对必须观看显示器的人类有害，因为这可能导致头痛。

![](img/c27875544958897d817484d558c208c8_403_2.png)

## 章节总结

- 启动加载程序通常由系统`BIOS`从`MBR/GPT`或硬盘活动分区的第一扇区加载。在 Linux 系统中最常用的启动加载程序是`LILO`、`GRUB`和`GRUB2`。

- 启动加载程序加载 Linux 内核后，系统初始化过程会继续加载守护进程，使系统达到可用状态。

- 有两种常见的系统初始化过程：`UNIX SysV` 和`Systemd`。现代`UNIX SysV` 实现使用`upstart`系统初始化过程。

- `UNIX SysV` 使用七个运行级别，根据内存中加载的守护进程的数量和类型来分类 Linux 系统。`Systemd` 使用五个标准目标，对应于七个`UNIX SysV` 运行级别。

- `init`守护进程负责在运行级别和目标之间切换时，以及在系统启动和关闭时加载和卸载守护进程。

- 守护进程通常通过`rc`脚本在系统初始化期间执行。`/etc/init.d`目录包含大多数`UNIX SysV` rc 脚本，`/usr/lib/systemd/`系统目录包含大多数`Systemd` rc 脚本。
