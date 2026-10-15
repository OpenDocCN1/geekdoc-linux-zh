
我要向本手册的过去作者们表示衷心感谢。他们的许多工作仍保留在此处。还要感谢那些耐心倾听我提问并更加耐心地给我答案的开发者和测试人员。没有他们的帮助，我无法完成这本手册。还要向文档团队的两位成员表示“BIG”感谢。我们的编辑 Paul Gallagher 对本手册的校对和编辑工作做得非常出色。他还撰写了本书的 GnoRPM 章节和《Red Hat Linux 官方入门指南》。文档团队的“无畏领袖”兼负责人 Edward Bailey 在让我保持最新信息并帮助我朝着正确的方向前进方面做得非常出色。他还被认为撰写了本《安装指南》中的新分区附录。没有他的领导和指导，这对我来说将是一项不可能完成的任务。你们二位合作起来很愉快，我真的无法表达足够的感谢。还要感谢过去《安装指南》的所有读者。没有他们的更正、建议甚至偶尔的赞扬，我就不知道自己是否走在正确的轨道上。你们的反馈已尽可能被纳入（在页数和截止日期允许的情况下）。请继续提供反馈。还要感谢 Cynthia Dale 更新了常见问题解答章节，以及 Jeff Goldin 为出版进行了校对。不幸的是，由于手册中空间不足，我们无法印刷它。但是，你可以在 `http://www.redhat.com/knowledgebase/index.html` 找到最新版本的 FAQ。最后，感谢 Red Hat Software 的支持团队。他们基于对数千名 Red Hat Linux 客户的丰富经验，对本手册提出了许多富有洞察力的建议。如果你发现自己阅读本《安装指南》更加轻松，其中很大一部分要归功于他们的努力。感谢 Red Hat Software 的每一个人对你们的帮助和支持。

Sandra A. Moore

# 1 Red Hat Linux 6.0 的新功能

本章描述了 Red Hat Linux 6.0 的新功能。

## 安装相关增强

以下是为了使 Red Hat Linux 安装过程更加简单而做出的许多更改的列表：

- New HTTP Installation Method
- “Out-of-the-Box” Processor Optimized Kernel Support
- New Boot Disks
- Improved Package Selection Screen
- New Authentication Configuration Screen
- Xconfigurator Now Part of Install

让我们更详细地了解一下每一个。

### New HTTP Installation Method

Red Hat Linux 6.0 安装程序已将 HTTP 添加到其可用的网络类安装列表中。与执行 FTP 安装的方式类似，你现在能够登录到一个网站并安装 Linux。有关网络类安装的更多信息，请参阅第 5 章。

### ‘Out-of-the-Box’ Processor Optimized Kernel Support

现在支持 Pentium Pro、Pentium II 和 Pentium III 处理器的优化内核以及 APM 启用的内核。此外，Red Hat Linux 6.0 安装现在具有 SMP 主板支持。安装过程将探测你的系统，如果检测到多于一个处理器，则会自动安装 SMP 启用的内核。

## The Installation Guide for Red Hat Linux 6.0

### New Boot Disks

Red Hat Linux 现在有两个启动盘。一个用于从本地媒体安装（CD-ROM 安装、硬盘安装），另一个用于基于网络的安装（NFS、FTP 或 HTTP）。此外，补充盘已被 PCMCIA 支持盘取代。所有安装方法现在只需要一张盘，除非你在安装过程中需要 PCMCIA 支持。如果需要，将提示你插入 PCMCIA 支持盘。

### Improved Package Selection Screen

单个软件包选择已得到改进，采用可折叠和可扩展的树形菜单，以便在安装过程中轻松选择软件包。

### New Authentication Configuration Screen

身份验证配置屏幕为你提供了启用三种不同类型密码的选项：

- Enable NIS — 允许你在一个 Network Information Service 域中以通用密码和组文件运行一组计算机。这里有两个选项可供选择：
  - NIS Domain — 此选项允许你指定系统将属于哪个域或计算机组。
  - NIS Server — 此选项会导致你的计算机使用特定的 NIS 服务器，而不是“广播”一条消息到局域网请求任何可用服务器托管你的系统。
- Enable Shadow Passwords — 提供一种非常安全的方法来保留你的密码。
- Enable MD5 Passwords — 允许密码长达 256 个字符，而非标准的八个。

### Xconfigurator 现在成为安装的一部分

`Xconfigurator` 现在在安装的最后阶段运行，在所有文件系统组件安装完成后。过去，如果 `Xconfigurator` 挂起，你很可能需要重新开始安装。现在可以在安装完成后启动 Red Hat Linux 并配置 X。此外，`Xconfigurator` 在安装期间会测试 X，以确保其为你的系统正确配置。`Xconfigurator` 还提供在安装完成后立即启动 X Window 系统的选项。

## 桌面和窗口管理器

Red Hat Linux 6.0 提供了更多图形用户界面的选择。

- 包含 Enlightenment 的 GNOME
- 包含 KDE

### 包含 Enlightenment 的 GNOME

GNOME 现在作为默认桌面管理器包含在 Red Hat Linux 6.0 中。GNOME 具有图形界面，使用户能够轻松使用和配置系统。GNOME 还支持拖放协议，有助于你使用非 GNOME 兼容的应用程序。Enlightenment 作为默认窗口管理器包含在内。Enlightenment 提供了一个具有出色图形界面的窗口管理器，并设计为允许用户以任何时尚的方式操作它。

### 包含 KDE

Red Hat Linux 6.0 还包含 KDE。KDE 是一个非常流行且功能强大的桌面环境，提供出色的图形界面、窗口管理器、文件管理器等。

## 杂项新功能

Red Hat Linux 6.0 的其他杂项功能包括：

- 增强的字体支持
- 增强的 Init 脚本
- Switchdesk 功能
- 包含最新的稳定 2.2 内核

### 增强的字体支持

TrueType 字体现在在 Red Hat Linux 6.0 中得到支持。动态字体加载现在得到支持，可用作本地机器上的字体服务器。

> 请注意：升级的用户在编辑字体路径之前将无法使用此功能。为此你必须编辑 `/etc/X11/XF86Config` 文件。向下滚动直到看到列出的字体路径。用 `FontPath "tcp/localhost:7100"` 全部替换它们。你还必须验证 `xfs`，X 字体服务器，是否正在运行。通过发出命令 `/sbin/chkconfig --add xfs`，你将确保它在系统启动时启动。

### 增强的 Initscripts

在启动和关闭系统时，Red Hat Linux 6.0 用户现在能够轻松查看服务是否失败，屏幕右侧会显示 OK、PASSED 或 FAILED。

### Switchdesk 功能

`Switchdesk`，正如其名所示，允许你轻松在不同的桌面环境之间切换，例如 GNOME、Another Level 或 KDE。只需运行 "`switchdesk`" 并选择你想要的界面即可。

### 包含最新的稳定 2.2 内核

Red Hat Linux 6.0 包含 Linux 内核 2.2 的最新稳定版本。

# 2 开始之前

虽然安装 Red Hat Linux 是一个直接的过程，但在开始安装前花一些时间可以使一切顺利得多。在本章中，我们将讨论在开始安装前应执行的操作。请注意：如果您当前运行的是版本 2.0 或更高版本的 Red Hat Linux 系统，您可以执行升级。浏览本章以回顾与安装相关的基本问题，并按顺序阅读以下章节，边读边执行。升级过程与安装过程完全相同；您将在启动安装程序并回答几个问题后被引导选择安装或升级。在安装 Red Hat Linux 之前，您应该做五件事：

- 1. 确保您拥有足够的文档，以便在安装后有效使用 Red Hat Linux 系统。
- 2. 确保您能够访问安装所需的 Red Hat Linux 组件。
- 3. 确保您了解计算机的硬件配置和网络信息。
- 4. 根据前两个任务，决定您将使用何种方法安装 Red Hat Linux。
- 5. 确定 Red Hat Linux 将驻留在硬盘驱动器上的位置。

让我们先确保您在安装 Red Hat Linux 后所需的文档。

## 获取文档
