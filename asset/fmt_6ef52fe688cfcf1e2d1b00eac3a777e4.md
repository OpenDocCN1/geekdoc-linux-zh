
b. `make mrproper`, `make menuconfig`, `make bzimage`, `make modules`, `make modules_install`

c. `make xconfig`, `make clean`, `make dep`, `make bzimage`, `make modules`, `make modules_install`

d. `make mrproper dep bzimage modules_install`

### 5

Linux 使用什么种分区格式？

a. Linux

b. BSD

c. Unixware

d. DOS

### 6

`make menuconfig` 选项是一个需要 X 视频支持的菜单驱动工具。

a. 正确

b. 错误

答案 b 是正确的。`make menoconfig` 工具是菜单驱动的，但不需要 X 支持。然而，`make xconfig` 命令确实需要这种 X 的支持。

## 问题 7

+ 谁创建了 Linux 内核？

- a. Linus Torvalds

- b. Richard Stallman

- c. Jon "maddog" Hall

- d. Bill Gates

答案 a 是正确的。答案 b 是错误的，因为 Richard Stallman 创建了大部分 GNU 工具。答案 c 是错误的，因为 Jon "maddog" Hall 是 Linux International 的主管。答案 d 是错误的，因为 Bill Gates 在 20 世纪 80 年代初与 Xenix 有关。

## 问题 8

+ 要停止 Linux 系统，你可以做什么？

- a. Ctrl+Alt+Delete

- b. `shutdown -h`

- c. `shutdown -r now`

- d. `init 0`

答案 d 是正确的。答案 a 和 c 是错误的，因为它们都会重启系统，而不是停止它。答案 b 是错误的，因为它不完整。

## 问题 9

运行级别 2 (`runlevel 2`) 和运行级别 3 (`runlevel 3`) 的主要区别是什么？

运行级别 2 和 3 都是多用户运行级别。两者最大的区别在于网络支持。运行级别 2 是没有网络的完整多用户模式，而运行级别 3 是带有网络的完整多用户模式。

## 问题 10

| 使用什么命令设置用户和组配额？ |

| a. `/usr/sbin/quota` |

| b. `/sbin/quotaon` |

| c. `/sbin/edquota` |

| d. `/sbin/usrquota` |

答案 c 是正确的。答案 a 和 d 是错误的，因为它们不是有效的命令。答案 b 是错误的，因为它只开启了配额但没有设置它们。

# 任务 1

重新编译你的内核。使用不同的内核配置工具，如 `make config`、`make menuconfig` 和 `make xconfig`，发现这些 make 选项之间的差异，并决定你喜欢哪种方法。

# 任务 2

设置两个新内核，一个是单体的，一个是模块化的。你注意到任何区别吗？

# 想了解更多吗？

![](img/7a3d74d02590d83bf562ed6969dbbaba_230_0.png)

Aleen Frisch. Essential System Administration, O'Reilly & Associates, Sebastopol, CA, 1995. ISBN:1-56592-127-5. 第 14 章讨论了 Unix 风格的启动过程，第 15 章讨论了编译 Linux 内核。

![](img/7a3d74d02590d83bf562ed6969dbbaba_230_1.png)

http://metalab.unc.edu/LDP/HOWTO/HOWTO-INDEX

Linux 文档项目为 Linux 的各个方面提供了极佳的资源，包括关于编译 Linux 内核的条目。

# X Window 系统

你需要理解的术语：

- 图形用户界面 (GUI)

- 客户端/服务器关系

- 根窗口 (Root window)

- 窗口管理器

- 桌面环境

- 远程主机

你需要掌握的技术：

- 理解 X 客户端/服务器关系

- 为特定硬件选择合适的 XFree86 (XF86) 服务器

- 配置 X 服务器

- 理解桌面环境

- 设置远程 X 访问

# 第 9 章

窗口系统是 Linux 运行时使用的 GUI。Linux 上使用的管理工具具有 GUI 界面，可以与 X Window 系统配合。大多数管理员在他们的红帽 Linux 机器上使用 X Window 系统。因此，当你准备 RHCE 300 考试时，理解 X Window 系统、X 服务器、X 客户端和远程 X 应用至关重要。

## X 概念

窗口系统并不是一个新概念。事实上，在 Linux 创建之前，它已经在多个 Unix 系统上实现了！关于 X Window 系统来源的最好的解释之一可以在 LDP（Linux 文档项目，http://metalab.unc.edu/LDP）中由 Ray Bringle 维护的 X Window 系统 HOWTO 找到。该 HOW 解释 开发于麻省理工学院的计算机科学实验室，并于 1984 年首次发布。X 的起源基于斯坦福大学 Paul Asente 开发的 XWindowing 包。

HOWTO 继续解释道，在 1987 年 9 月，MIT 发布了我们今天熟悉并使用的 X11 第一版本。然而，作为 X11R2，开发和控制从 MIT 转移到了 1988 年 1 月成立的 X 联盟。

窗口系统目前由 X.org 开发和分发。宽松的许可允许免费和低成本实现的生存。Linux 使用的是 XFree86 版本的 X Window 系统。XF86 版本可以免费分发，是针对 Intel x86 平台上基于 Unix 的操作系统的 X 服务器集合。该工作源自 X386，此后许多新工作回馈了 X11R6 项目。

## X Window 系统组件

窗口系统由四个主要组件组成，它们相互交互：X 服务器、客户端、X 协议和 X 窗口管理器。我们将在本章后面讨论服务器、客户端和窗口管理器。

# X Window 系统

窗口系统是 Linux 运行时使用的 GUI。Linux 上使用的管理工具具有 GUI 界面，可以与 X Window 系统配合。大多数管理员在他们的红帽 Linux 机器上使用 X Window 系统。因此，当你准备 RHCE 300 考试时，理解 X Window 系统、X 服务器、X 客户端和远程 X 应用至关重要。

## X 概念

窗口系统并不是一个新概念。事实上，在 Linux 创建之前，它已经在多个 Unix 系统上实现了！关于 X Window 系统来源的最好的解释之一可以在 LDP（Linux 文档项目，http://metalab.unc.edu/LDP）中由 Ray Bringle 维护的 X Window 系统 HOWTO 找到。该 HOW 解释 开发于麻省理工学院的计算机科学实验室，并于 1984 年首次发布。X 的起源基于斯坦福大学 Paul Asente 开发的 XWindowing 包。

HOWTO 继续解释道，在 1987 年 9 月，MIT 发布了我们今天熟悉并使用的 X11 第一版本。然而，作为 X11R2，开发和控制从 MIT 转移到了 1988 年 1 月成立的 X 联盟。

窗口系统目前由 X.org 开发和分发。宽松的许可允许免费和低成本实现的生存。Linux 使用的是 XFree86 版本的 X Window 系统。XF86 版本可以免费分发，是针对 Intel x86 平台上基于 Unix 的操作系统的 X 服务器集合。该工作源自 X386，此后许多新工作回馈了 X11R6 项目。

## X Window 系统组件

窗口系统由四个主要组件组成，它们相互交互：X 服务器、客户端、X 协议和 X 窗口管理器。我们将在本章后面讨论服务器、客户端和窗口管理器。

## X Window System 205

![](img/7a3d74d02590d83bf562ed6969db9ba0_236_0.png)

图 9.1 Red 的 XConfigurator 程序。

在启动模式（kickstart mode）下，XConfigurator 会尝试自动探测所有所需信息。当你使用 PCI 显卡时，这非常有用，因为 XConfigurator 通常能正确探测它们。如果没有检测到显卡，系统会提示你手动选择显卡。

## XF86Setup

XF86Setup 程序是 XFree86 项目的图形用户界面工具。你通常使用 XF86Setup 来初始化 XF86 服务器或调整当前配置。在 shell 提示符下输入 `xf86setup` 即可调用该程序。运行时，XF86Setup 会向你展示出一个灰色、蓝色和青色的按钮风格界面，该界面运行在通用的 VGA16 服务器上。图 9.2 显示了 XF86Setup 的界面。

如图 9.2 所示，XF86Setup 提供了六个用于 X Window 系统配置的按钮。第一个按钮“Mouse”（鼠标）允许你配置鼠标设置。在该菜单中，你可以选择使用的鼠标协议类型（如 PS2、Microsoft、Logitech）以及其他鼠标选项，如鼠标设备（`/dev/ttyX` 或 `/dev/psanx`）和其他按钮设置。

![](img/7a3d74d02590d83bf562ed6969db9ba0_236_1.png)

图 9.2 XF86Setup 界面。

# 第 9 章

XF86Setup 窗口中的第二个选项是“Keyboard”（键盘）。此菜单提供了选择键盘型号和语言的选项。此外，你还可以选择如 Shift/Lock 行为和 Control 键的位置。

XF86Setup 窗口中的第三个选项是“Card”（显卡）。此菜单允许你选择什么类型的 XF86 服务器。此外，还提供了选择特定芯片组、RamDac 选项、ClockChip 以及任何你希望自动添加到 XF86Config 文件中的选项。

XF86Setup 窗口中的第四个选项是“Monitor”（显示器）。此菜单允许你选择显示器类型以及水平和垂直同步率。它列出了自动设置水平和垂直同步率的常用显示器设置。如果你知道显示器的性能，或者你的显示器不在列表中，则必须在屏幕顶部手动指定水平和垂直同步率。图 9.3 显示了 XF86Setup 的显示器配置界面。

XF86Setup 窗口中的第五个选项是“Modeslection”（模式选择）。此菜单允许你配置显示分辨率和色彩深度。你可以从几种分辨率中选择（选项取决于你选择的服务器和显示器），范围从 320×200 到 1600×1200 以上。你还可以选择运行 XWindow 系统的色彩深度。某些选项包括 8bpp（每像素位）、16bpp、24bpp 和 32bpp。如果你尝试选择任何显卡或显示器不支持的选项，将收到错误并自动返回配置菜单。

XF86Setup 窗口上的最后一个按钮是“Other”（其他）。此菜单允许你选择可选的服务器设置。可用选项包括启用

![](img/7a3d74d02590d83bf562ed6969db9ba0_237_0.png)

图 9.3 XF86Setup 的显示器配置。

通过热键序列（Ctrl+Alt+Back Space）杀死 XF86 服务器，启用视频模式切换，并允许从其他主机进行更改。

## xf86config

`xf86config` 程序是一个基于文本的配置工具，用于配置 XF86Config 文件。要调用 xf86config，请在 root 提示符下输入 "`xf86config`"。

使用 `xf86config` 工具时，系统会提示你通过文本提示符方法配置鼠标、键盘和显示器设置。每个选项都会向你列出可选的编号列表供选择，或者让你回答是或否。`xf86config` 工具是配置 X Window 系统最少使用的。图 9.4 显示了 `xf86config` 工具界面的示例。

## X Client

X 客户端是向 X 服务器发送请求的软件。X 服务器的响应将显示在 X 客户端上。X 客户端可以是与 X 服务器在同一台机器上的软件，也可以是远程主机上的软件。我们将在本章稍后讨论远程 X 应用。

一种特殊的 X 客户端是桌面客户端。桌面客户端实际上控制标题栏、任务栏以及其他窗口处理。

标准的 X 桌面由许多服务和程序组成，取决于你使用的窗口管理器或环境。然而，有几个标准术语和应用程序通用的。在使用 X 客户端时，你应该注意以下术语及其区别：

![](img/7a3d74d02590d83bf562ed6969db9ba0_238_0.png)

图 9.4 xf86config 界面。

## 208 第 9 章

-   screen：你的桌面。“screen”和“desktop”这两个术语经常互换。从技术上讲，screen 是查看 X Window 系统的主要视频显示器。

-   root window（根窗口）：你屏幕的背景。根窗口不具备任何其他窗口的标准特征，但它有一些独特的应用程序。根窗口是你自定义背景图像等的地方。

-   window manager（窗口管理器）：X Window 系统与用户之间的主界面。窗口管理器提供窗口边框、菜单、图标、桌面、按钮和工具栏等功能，并允许你自定义所有内容。我们将在本章稍后讨论各种窗口管理器。

-   pointer（指针）：代表鼠标、轨迹球、滑点或其他设备位置的箭头或其他指示器，它对应于屏幕上的位置。指针的形状、颜色或大小经常会变化，以指示鼠标在屏幕的特定区域具有特定功能。

-   window（窗口）：任何应用程序存放并由窗口管理器管理的框架。活动窗口（你当前在桌面上使用的窗口）通常通过位于顶层、获取焦点或与屏幕上的非活动窗口相比高亮显示来指示。

-   terminal emulator（终端模拟器）：一个仅包含文本、基本上模拟控制台的窗口。终端模拟器的一个示例是 `xterm`。

## Window Managers（窗口管理器）

许多窗口管理器——如 AfterStep、Enlightenment、fwm 和 Window Manager——供你的 X 客户端使用。你不将窗口管理器与桌面环境混淆，例如 GNU 网络对象模型（GNOME）和 K Desktop 环境（KDE）。我们将在本章稍后讨论桌面环境。

## AfterStep

图 9.5 所示的 AfterStep 最初设计为看起来和感觉像 Apple 购买公司之前在 NeXT 机器上使用的 NeStep 界面。

## X Window System 209

![](img/7a3d74d02590d83bf562ed6969db9ba0_240_0.png)

图 9.5 AfterStep 桌面。

## Enlightenment

与 AfterStep 或其他少数窗口管理器不同，图 9.6 所示的 Enlightenment 并不是模仿现有的窗口管理器或其他操作系统环境。它是一个开发频繁的高度图形化窗口管理器。

> 注意：不建议内存或磁盘空间较低的用户使用此窗口管理器。

## fvwm

图 9.7 所示的 fwm 窗口管理器是 Linux 可用的最老的窗口管理器之一。与 Enlightenment 等较新的管理器相比，它非常小，需要的内存和 CPU 资源更少。你可以配置 fwm 窗口管理器使其看起来像 Motif 甚至是 Windows 95。

## Window Maker

图 9.8 所示的 Window Maker 是另一个模仿 NeStep 的窗口管理器。Window Maker 设计为 GNUStep 提供额外的集成支持。Window Maker 运行快速、易于使用，并在许多 Linux 用户中很流行。

## 210 第 9 章

![](img/7a3d74d02590d83bf562ed6969db9ba0_241_0.png)

图 9.6 Enlightenment 和 GNOME。

![](img/7a3d74d02590d83bf562ed6969db9ba0_241_1.png)

图 9.7 fvwm.

# X Window 系统

![](img/7a3d74d02590d83bf562ed6969db9ba0_242_0.png)

**图 9.8** Window Maker。

# X Server 工具、技巧与窍门

有多种工具、技巧和窍门可以帮助你管理和配置窗口管理器选项。例如，你可以设置你的 Red Hat Linux 6.0 安装，使其默认自动启动到你喜喜欢的窗口管理器。要实现这一点（假设你没有在安装期间选择窗口管理器），你需要编辑 `/etc/initab` 文件。若要自动启动到你的窗口管理器，你必须将 `/etc/initab` 文件设置为启动到运行级别 5（runlevel 5）。你可以在文件前面的几个选项之一中进行设置，字符串如下：

```
id:X:initdefault:
```

其中 X 是启动时的默认运行级别。要自动启动到运行级别 5，该配置字符串应为：

```
id:5:initdefault:
```

如果你在运行级别 3（控制台模式）下运行，你有两种运行 X Window 系统的方法。你可以通过 `init5` 命令启动到运行级别 5，或者直接使用 `startx` 启动 X Window 系统。通常，`startx` 是从控制台启动 X Window 系统的首选方法。

用于指定用户显示管理器（gdm、kdm 或 xdm）的 shell 脚本是 `Xsession`。位于 `/etc/X11/xdm/` 的默认 `Xsession` 脚本

# 第 9 章

如果用户在其主目录下没有 `.xsession` 文件或 `.Xclients` 文件，则使用它。`.xsession` 和 `.Xclients` 文件用于为用户指定特定的显示环境或窗口管理器，通常当用户希望设置与默认系统设置不同时使用。执行窗口管理器的脚本是 `xinitrc`。如果用户主目录下有一个 `xinitrc`，则使用其个人启动脚本。否则，使用默认的 `/etc/X11/xinit/xinitrc`。

![](img/7a3d74d02590d83bf562ed6969db9ba0_243_0.png)
