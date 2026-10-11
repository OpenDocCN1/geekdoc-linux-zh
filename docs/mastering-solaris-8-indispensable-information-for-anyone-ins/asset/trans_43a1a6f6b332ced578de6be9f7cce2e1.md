

虽然 twm 没有图标，且窗口相对简单，但它可以用于资源有限且并发用户较多的网络系统。您仍然可以在 Linux 上找到 twm。OpenLook 窗口管理器是另一个由 Sun Microsystems 和 AT&T 开发的早期尝试。OpenWindows 是 Sun 基于 OpenLook 工具包实现的 Open-Look，该工具包是 20 世纪 80 年代末和 90 年代初 Sun 的标准图形用户界面。

另一种行业努力出现在 20 世纪 80 年代，当时开放软件基金会（OSF）开发了 Motif 工具包，它是 OpenLook 的替代品。Motif 中的许多界面特性被微软 Windows 采用，反之亦然。尽管 Motif 很流行，但它从未在 Unix 上实现通用。更糟糕的是，每个供应商的 Motif 和 Motif 窗口管理器都略有不同。这给应用程序开发人员带来了问题。

到 1993 年，几家厂商联合起来组成了通用开放软件环境（COSE）计划，旨在创建一个行业标准图形用户界面和应用程序编程接口，即 API。该计划的原始成员包括 Hewlett-Packard、IBM、Novell 和 SunSoft；随后 Digital Equipment Corporation、富士通和日立也加入了进来。COSE 大量借鉴了过去的努力，主要是 Motif，以创建一个功能更丰富的图形环境，从而吸引 Windows 和 Macintosh 用户。COSE 的结果是通用桌面环境（CDE）版本 1 的开发，它运行在 Solaris 2.5 上。Solaris 8 运行 CDE 的版本 1.4。CDE 的各个版本在以下系统上运行，具有与 Solaris 上的 CDE 几乎完全相同的功能：

- IBM AIX
- Hewlett-Packard HP-UX
- Digital Unix

如今，大多数 Unix 用户使用的是 Solaris 和其他三家厂商的 Unix 环境。您也可以在 Linux 和 FreeBSD 上找到 CDE，使用由第三方厂商 TriTeal、X Inside 和 Work Group Solutions (WGS) 提供的软件。TriTeal 增强桌面（TED）是在 Linux 和 FreeBSD 上最广泛使用的 CDE，它为 CDE 标准提供了许多添加功能。

## 窗口管理器

您可以有许多不同的窗口管理器运行在 X Window 系统上。来自开放软件基金会（OSF）的 Motif 窗口管理器 (mwm) 可以运行在 X 上。Solaris 版本 2.5 及更高版本附带三种不同的 X 窗口管理器——OpenLook 窗口管理器 (olwm)、桌面窗口管理器 (dwm) 和虚拟标签窗口管理器 (vdtwm)——但您可以添加其他窗口管理器。桌面窗口管理器是 CDE 的一部分，基于 Motif，它负责工作区和许多命令。

作为 Sun 专有 OpenWindows 系统一部分的 OpenLook 窗口管理器，是最早运行在 X 上的窗口管理器之一。OpenWindows 在 Solaris 中受支持，您可以像登录 CDE 会话一样登录 OpenWindows 会话。虽然 CDE 基于更开放的标准，但 OpenWindows 因为它是专有的而正在失去人气。未来版本的 Solaris 将不再支持 OpenWindows。虚拟标签窗口管理器在 Solaris 上并不广泛使用。

还有许多其他在 Unix 上运行并可免费下载的窗口管理器。其中，Tom’s Window Manager (twm)、GNU Window Manager (gnwm)、OpenLook Virtual Window Manager (olvwm)、Virtual Window Manager (fvwm)、After-Step 和 xfce 比较受欢迎。AfterStep 是 NextStep 的克隆，而 xfce 是 CDE 的克隆。这些窗口管理器名称中的 *virtual* 指的是创建任意大小的工作区（超过监视器大小）以及多个工作区的能力。两个最新且迅速获得普及的窗口管理器是 GNOME 和 KDE。Sun 最近宣布将协助开发 GNOME，并将在未来某个时候将其作为默认界面包含在内。GNOME 也获得了 IBM 和 HP 的强力支持。

## CDE 桌面

CDE 是桌面管理器的一个例子。桌面管理器管理图标或图片在屏幕上表示对象的使用。它负责赋予您作为图标操纵文件和应用的能力。这是您执行删除、复制和移动等操作的子系统。您可以通过在文件图标上进行点击拖动操作创建符号链接，也可以通过双击打开可执行文件或二进制文件。桌面管理器与窗口管理器协同工作。

CDE 已成为标准桌面管理器，因为它为 Solaris 应用程序提供了通用的外观和感觉，让开发人员创建应用程序并让用户修改界面以支持多种语言，并且提供了一个应用程序间通信设施，允许远程或本地运行的应用程序协同工作。

在图形用户界面中，对象表示为图标，内容放置在称为窗口的容器中。图标有在右键单击时出现的弹出菜单，而窗口通常在菜单栏或标题栏上显示菜单。您可以将窗口的表示缩小为图标以节省空间，并在需要处理窗口内容时将图标还原为窗口。您看到的许多图标代表内容，而不是容器项。诸如程序（可执行或二进制文件）、数据文件和提供访问各种类型内容的符号链接等对象在图形用户界面中获得图标化处理。

> **注意** Solaris 使用三键鼠标。当您左键单击时，您使用的是鼠标按钮 1；当您右键单击时，您使用的是鼠标按钮 3。中间按钮，即鼠标按钮 2，用于复制和编辑功能。

## 登录

当您登录到 Solaris 提供的任何环境时，您使用的是登录管理器程序 `dtlogin`，这是一个基于名为 `xdm` 的 X Windows 程序。登录管理器是一个作为守护进程运行的服务器，直接登录到 X Windows，而不需要您运行 `xinit` 这样的程序或 `startx` 这样的 shell 脚本。登录管理器免除了您处理过去启动 X Windows 的方法的麻烦，那些方法包括在控制台上登录，设置或检查环境（通常还设置自定义配置），然后给出 X Windows 启动命令。现在，这些任务由 CDE 自动处理，并且可以建立默认用户配置，这对网络管理员帮助极大。

登录管理器读取位于 Xresources 文件 `(/usr/dtconfig/<lang>/Xresources)` 中的设置，该设置控制登录屏幕本身的外观。登录管理器可以本地或在远程 X 终端或工作站上启动多个图形界面和基于字符的环境实例。程序 `dtlogin`（位于 `/usr/dt/bin/dtlogin`）提示输入登录名和密码，验证用户身份，并运行一个会话（登录 shell 进程），该进程由 DT 会话管理器管理。登录管理器运行表 7.1 中显示的多个脚本。

**表 7.1：登录管理器配置文件**

| 文件名 | 描述 |
| :--- | :--- |
| /usr/dt/config/Xsetup | 启动显示设置的 Korn shell 脚本 |
| /usr/dt/config/Xstartup | 初始化某些系统功能的 Korn shell 脚本 |
| /usr/dt/bin/XSession | 启动桌面会话的 Korn shell 脚本 |
| /usr/dt/config/Xfail1safe | 允许您打开故障保护窗口的 Bourne shell 脚本 |
| /usr/dt/config/Xreset | 包含在会话结束时执行的命令列表的 Korn shell 脚本 |

由于 dtlogin 作为守护进程运行，因此不需要再次调用该程序。最好将登录管理器放入 dtconfig 脚本中，以便您可以指定其任何选项。选项包括 -d（禁用自动启动）、-e（启用自动启动）、-kill（终止 dtlogin）、-reset（重置 dtlogin）、-p（更新打印机操作）、-instd（启动 inet .conf /usr/ dt 守护进程）、-inetd.st（启动 inetd.conf /usr/ opwin 守护进程）。关于此重要系统功能的 man 页面提供了超过 26 页的文档，介绍其操作和选项。

> **提示** /usr/dt/config 目录包含存储登录管理器使用的设置的文件；其中许多文件定义了登录屏幕出现之前和您注销之后运行的脚本。当您升级系统时，这些文件会被覆盖。如果您希望保留登录行为，请将 /usr/dt/config 文件复制到 /etc/dt/config 文件夹。登录管理器优先使用 /etc/dt/config 文件夹中找到的文件和设置，而不是 /usr/dt/config 文件夹中的相同文件。如果您想要修改登录屏幕，请将 Xresources 文件复制到 /etc/dt/config/lang/Xresources 文件并编辑该文件。

当您处于登录屏幕时，您可以选择一种会话类型：

- 通用桌面环境（CDE）。
- Sun 的 OpenWindows，这是由 Sun 和 AT&T 开发的 OpenLook 窗口管理器的一部分。
- 故障保护会话。Solaris 运行单个版本的 X 终端 (xterm)，没有窗口管理器。此会话类型用于解决配置问题和安装新硬件。
- 命令行。

虽然 CDE 与 Unix Motif 界面有很多共同点，但它实际上并不是 Motif。Solaris 附带一些 Motif 库并支持一些 Motif 功能，但它不附带 Motif 窗口管理器 (mwm)。因此，如果您想使用 Motif，您需要安装它。然而，除非他们正在进行要求开发人员查看应用程序在 Motif 中外观的开发项目，否则很少有人实际上在 Solaris 上使用 Motif。

> **注意** 第 3 章“入门”介绍了作为登录例程一部分提供给您的选项。

实际运行 CDE 桌面的应用程序是会话管理器。会话管理器负责启动桌面并保存状态

