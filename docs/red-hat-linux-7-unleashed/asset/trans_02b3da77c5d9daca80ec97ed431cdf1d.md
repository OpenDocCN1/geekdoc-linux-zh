

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_146_0.png)

> 图 5.1

> 你可以没有窗口管理器就运行 X11，但它值得吗？

Red Hat Linux 中包含的窗口管理器中，只有一个属于 XFree86 X11 发行版，其他都是 Red Hat 为你提供的。本章从介绍 X11 的 GNOME 软件库开始，然后重点介绍默认窗口管理器 sawfish，介绍 KDE，最后以 fvwm2 和 twm（XFree86 窗口管理器）作为结尾。

## GNOME X 环境

本节讨论 GNOME（GNU 网络对象模型环境，GNU Network Object Model Environment），这是由 Red Hat Software, Inc. 的程序员以及其他开发者开发和支持的。GNOME 受到了越来越多的关注，因为它是在 GNU GPL 下分发的；在 2000 年 8 月，IBM、Compaq、Hewlett-Packard、Sun Microsystems 以及其他公司开发者联合起来成立了 GNOME 基金会，旨在促进 GNOME 并将技术整合到 UNIX 和 Linux 的标准桌面环境中。

GNOME 是 Linux 图形 X 桌面未来的重要组成部分，原因有以下几点：

- 该软件是完全开源和中立于供应商的；商业软件可以建立在此软件之上，而无需购买软件许可证。
- 可以对其进行贡献、更改和修改，而不受中央源的控制，并且在对更改的制作和分发方面没有许可证限制。
- 该软件支持多种操作系统和外部编程语言。
- 该软件可与任何支持 GNOME 的 X11 窗口管理器配合使用，例如 sawfish 或 Enlightenment。

### 什么是 GNOME？

GNOME 是一组旨在支持 X11 桌面环境的软件库和 X11 客户端。GNOME 可以与任何支持 GNOME 的窗口管理器或任何支持其面板组件和客户端功能（如拖放桌面操作）的窗口管理器一起使用。GNOME 在启动窗口管理器之前初始化并运行。与 KDE 一样，GNOME 提供了一个丰富的用户环境，包括应用程序框架、文件管理器、面板、具有一致外观和感觉的应用程序套件以及会话管理，从而在 X11 会话之间恢复可用的桌面。

### GNOME 安装组件

GNOME 由许多软件组件组成，对于 Red Hat Linux，它通过一系列 RPM 文件分发。你可以使用 `gnorp` X11 客户端、`KDE's` *kpackage* 客户端或通过 `rpm` 命令安装 GNOME。此时 Red Hat Linux 中包含的大多数 GNOME 包如表 5.1 所示。你可能会发现 Red Hat Linux 中还包含额外的客户端，并且每天都有更多客户端在 `http://www.gnome.org` 上可用。

**表 5.1 GNOME 组件**

| RPM 文件 | 描述 |
| :--- | :--- |
| enlightenment-0.16.4-6 | E 窗口管理器 |
| g1ms-1.03-4 | GNOME 系统温度监控小工具 |
| gmc-4.5.51-8 | GNOME 午夜命令器 |
| gnome-applets-1.2.1-5 | GNOME 面板工具 |
| gnome-audio-1.0.0-12 | GNOME 声音 |
| gnome-audio-extra-1.0.0-12 | GNOME 额外声音 |
| gnome-core-1.2.1-33 | GNOME 核心客户端和库 |
| gnome-core-devel-1.2.1-33 | GNOME 开发库 |
| gnome-games-1.2.0-9 | GNOME 游戏 |
| gnome-games-devel-1.2.0-9 | GNOME 游戏开发库 |
| gnome-kerberos-0.2.1-1 | GNOME GUI Kerberos 工具 |
| gnome-libs-1.2.4-11 | GNOME 库 |
| gnome-libs-devel-1.2.4-11 | GNOME 开发库 |
| gnome-linuconf-0.33-7 | GNOME linuconf 的 GUI |
| gnome-lokit-0.41-5 | GNOME 防火墙配置客户端 |
| gnome-media-1.2.0-7 | GNOME 多媒体支持 |
| gnome-objc-1.0.2-9 | GNOME 的 Objective C 库 |
| gnome-objc-devel-1.0.2-9 | GNOME 的 Objective C 开发库和工具 |
| gnome-pim-1.2.0-5 | GNOME 个人信息管理客户端 (gnomecal, gnomecard) |
| gnome-pim-devel-1.2.0-5 | PIM 开发文件 |
| gnome-print-0.20-8 | GNOME 打印库和字体 |
| gnome-print-devel-0.20-8 | GNOME 打印开发库 |
| gnome-users-guide-1.2-2 | GNOME 用户指南 (HTML) |
| gnome-utils-1.2.0-7 | GNOME 实用工具 (如 gcalc) |
| gnotrpm-0.9.27 | GNOME RPM 客户端 |
| gnotepad+-1.3.1-3 | GNOME 记事本客户端 |
| gnumerjc-0.54-4 | GNOME 电子表格客户端 |
| gphoto-0.4.3-8 | GNOME 数码相机编辑器 |
| gtop-1.0.9-4 | 支持 GNOME 的系统监视器 |
| pynome-1.0.53-4 | Python 访问 GNOME 库 |
| pynome-applet-1.0.53-4 | 使用 Python 开发 GNOME 小工具 |
| pynome-capplet-1.0.53-4 | 使用 Python 开发 GNOME 控制面板小工具 |
| pynome-llibgfade-0.6.6-4 | GNOME libgfade Python 支持 |
| rep-gtk-gnome-0.13-3 | Lisp 解释器的 GNOME 库 |
| sawfish-0.30.3-10 | sawfish 窗口管理器 |
| sawfish-themer-0.30.3-10 | sawfish 主题构建器 |
| switchdesk-gnome-3.6-1 | GNOME 桌面切换器 |
| xmes-gnome-1.2.2-4 | xmes 的 GNOME 面板小工具 |

当你安装 Red Hat Linux 时，大多数特定的 GNOME X11 客户端都安装在 /usr/bin 目录下。系统范围内的配置和支持文件将安装在 /usr/share/gnome 目录下，或者你也可以在 /usr/share 下找到其他 GNOME 客户端目录（例如用于 gedit、gnibbles 或 gnotepad+ 的目录）。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_149_0.png)

## 配置 X11 以使用 GNOME 或其他显示管理器

X11 客户端和软件库的 GNOME 发行版不包含窗口管理器。GNOME 库和客户端（如面板应用程序）设计用于与你最喜欢的 X11 窗口管理器配合使用。

如果你安装 Red Hat Linux，配置 XFree86 X11 服务器以配合你计算机的显卡工作，并选择直接启动到 X，那么默认情况下你将使用带有 GNOME 库的 **sawfish** 窗口管理器。你的登录将通过 GNOME 显示管理器 gdm 进行（如图 5.2 所示）。但是，Red Hat Linux 还附带其他显示管理器，例如 K 显示管理器 (kdm) 和 X 显示管理器 (xdm)。

![](img/6bd28cbdb5cafd4e9d424d0c660b83ee_149_1.png)

启动时默认启动的显示管理器由 /etc/X11 目录下名为 prefdm 的 shell 脚本决定。当你检查 prefdm 文件时，shell 脚本逻辑根据 /etc/sysconfig 目录下名为 desktop 的文件内容来确定默认显示管理器。所使用的显示管理器类型通过将关键字 GNOME、KDE 或 AnotherLevel1（其他窗口管理器）转换为 shell 环境变量来确定，这将分别启动 gdm、kdm 或 xdm。

prefdm 脚本的相关部分如下所示：

```bash
preferred=
if [ -f /etc/sysconfig/desktop ]; then
source /etc/sysconfig/desktop >/dev/null 2>&1
if [ "$DESKTOP" = GNOME ]; then
preferred=gdm
elif [ "$DESKTOP" = KDE -o "$DESKTOP" = KDE1 ]; then
preferred=/usr/bin/kdm
elif [ "$DESKTOP" = KDE2 ]; then
preferred=/usr/lib/kde2/bin/kdm
elif [ "$DESKTOP" = AnotherLevel1 ]; then
preferred=/usr/X11R6/bin/xdm
fi
fi
```

你的 Red Hat 系统初始化表 /etc/inittab 中针对运行级别 5 的条目显示如下：

```text
x5:respawn:/etc/X11/prefdm -nodaemon
```

如你所见，prefdm 首先查找 /etc/sysconfig 目录下名为 desktop 的文件。要设置默认显示管理器，请在 /etc/sysconfig 下创建 desktop 文件，然后输入 GNOME、KDE 或 AnotherLevel 等关键字。

gdm 显示管理器启动的默认会话（或窗口管理器类型）定义在 /etc/X11/gdm/Sessions 目录中。如果你检查 Sessions 目录，你会看到以下内容：

```text
Default  Failsafe  Gnome  KDE  default
```

这些文件是简短的 shell 脚本，显示在 gdm 对话框框中的 Sessions 下拉菜单中。脚本使用位于 /etc/X11/xdm 目录下的 Xsession 命令来启动特定的 X 会话。例如，Gnome 会话脚本包含

```bash
#!/bin/bash
/etc/X11/xdm/Xsession gnome
```

如果你检查 Xsession 脚本，你会发现这一段：

```bash
case $1 in
1)
case $2 in
failsafe)
exec xterm -geometry 80x24 -0
;;
gnome)
exec gnome-session
;;
kde|kde1)
exec /usr/share/apps/switchdesk/Xclients.kde
;;
kde2)
exec /usr/share/apps/switchdesk/Xclients.kde2
;;
anotherlevel)
# we assume that switchdesk is installed.
exec /usr/share/apps/switchdesk/Xclients.anotherlevel
;;
esac
esac
```

这显示了通过显示管理器选择后用于启动你的 X 会话的不同命令。注意，Failsafe 会话仅启动 xterm 客户端。

### 注意

> 有关 shell 脚本和 shell 编程的更多信息，请参见第 25 章，“Shell 脚本编程”。

如果你不使用显示管理器登录 Red Hat Linux，例如，你想在 X 会话中使用 GNOME，你的 .xinitrc 应包含以下条目：

```bash
exec gnome-session
```

然后使用 startx 命令启动你的 X 会话：

```bash
# startx
```

该会话将启动主要的 GNOME 组件，如面板（一个用于访问根菜单、配置桌面或启动 X11 客户端的任务栏客户端），以及桌面、键盘和鼠标控制软件。最后，sawfish 窗口管理器被启动。图 5.3 显示了运行多个客户端时你的 X11 桌面的可能样子。

