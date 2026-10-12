

![](img/774d40fd20903495c5cd00e2efad3f33_214_0.png)

**图 6.7** 你使用 switchdesk 来设置 X 会话的默认窗口管理器。

选择窗口管理器通常取决于个人偏好、实际需求和策略。在旧款 PC 上，你可能会更倾向于使用一些较老的窗口管理器——例如 **Tab 窗口管理器**（*twm*）或 **Motif 窗口管理器**（*mwm*）——因为它们对系统资源的需求更少（即需要更少的硬盘空间、CPU 性能和系统内存）。较新的桌面环境为了获得良好的性能，通常需要 64MB 甚至更多的内存。以下部分将介绍一些最流行的窗口管理器及其用途。

## Tab 窗口管理器（*twm*）

Tab 窗口管理器（*twm*）包含在 Xorg 中，有时也被称为 Tom's Window Manager。它是一个传统客户端，以较小的内存占用（少于 1MB）提供适度但必需的功能。它支持窗口装饰、菜单、图标和其他功能，但不支持虚拟桌面、会话管理以及其他功能（例如拖放）。

*twm* 窗口管理器在 Fedora 中用作备用或 *故障安全*（failsafe）窗口管理器，因为它所需的视频和系统内存少得多。它包含在 Xorg 软件分发版中，如果系统或你的默认窗口管理器设置丢失或不可用，在你登录或启动 X 时它将作为你的窗口管理器使用。*twm* 资源文件 *system.twmrc* 位于 */etc/X11/twm* 目录下。如果你将设置保存为家中目录中名为 *.twmrc* 的文件，就可以配置此文件以提供带有自定义应用程序菜单的默认桌面。此配置文件的格式记录在 *twm* 的手册页中。

图 6.8 展示了一个示例 *twm* 桌面，显示了 *xosview*、*xclock*、*xcalc* 和 *xterm* 客户端。可以使用 *xsetroot* 客户端更改默认桌面颜色。在 *twm* 中，你通过在主窗口（称为 *root* 显示器）的空白区域左键单击来访问桌面菜单。

![](img/774d40fd20903495c5cd00e2efad3f33_215_0.png)

**图 6.8** *twm* 包含在 Xorg 中，并提供基本的窗口和图标管理。

## Motif 窗口管理器（*mwm*）

*mwm*（Motif 窗口管理器）包含在 Fedora 中，以提供传统的 X 桌面。它是一个克隆窗口管理器，密切模仿了属于开放软件基金会 OSF/Motif 分发版的原始 *mwm* 窗口管理器。*mwm* 窗口管理器是名为 LessTif 的一组兼容 Motif 1.2 的编程库和开发文件的一部分。

*mwm* 甚至可以使用与 OSF/Motif 版本相同的配置文件。*mwm* 的默认资源文件位于 /etc/X11/ *system.mwmrc*。当该文件位于你的家中目录中且命名为 *.mwmrc* 时，你可以编辑此文件以提供自定义设置。

图 6.9 展示了一个示例 *mwm* 桌面。请注意，Motif 窗口管理器比 *twm* 窗口管理器提供更精致的窗口装饰（如边框和标题栏项目等控件）。

![](img/774d40fd20903495c5cd00e2efad3f33_216_0.png)

**图 6.9** Motif 窗口管理器为 Fedora 提供了一个简单的桌面。

## GNOME 和 KDE 桌面环境

X 的桌面环境提供一个或多个窗口管理器，以及符合基于通用软件库集的标准图形界面的客户端套件。当用于开发相关客户端时，这些库为客户端窗口、菜单、按钮和其他屏幕组件提供图形一致性，以及一些通用的键盘控件和客户端对话框。以下部分简要讨论了 Fedora Core 中包含的两个桌面环境：GNOME 和 KDE。

### GNOME：GNU 网络对象模型环境

始于 1997 年的 GNOME 项目是程序员奇才 Miguel de Icaza 的创意之作。GNOME 提供了一整套软件库和客户端。GNOME 依赖于一个支持 GNOME 的窗口管理器。这意味着，为了提供带有 GNOME 元素的图形桌面，窗口管理器需要编写以识别并使用 GNOME。一些支持 GNOME 的合规窗口管理器包括 Havoc Pennington 的 *metacity*（默认 GNOME 窗口管理器）、Enlightenment、Window Maker、IceWM 和 *sawfish*。

Fedora 使用 GNOME 的易用户界面客户端套件来提供一致且用户友好的桌面。GNOME 是 Red Hat 商业 Linux 发行版和 Fedora 的重要特性，因为 Red Hat 积极支持其开发。GNOME 客户端位于 `/usr/bin` 目录下，GNOME 配置文件存储在 `/etc/gnome` 和 `/usr/share/gnome` 目录下，用户设置存储在家中目录下的 `.gnome` 中。

### Red Hat 的 Ximian GNOME

1999 年，Miguel de Icaza 和 Nat Friedman（最初的 GNOME 开发者）创建了一家名为 Ximian 的公司和产品。Ximian 是一个精致的 GNOME 环境，不仅提供了一整套更新版的 GNOME 客户端，还提供了提供集成邮件、日历、地址簿和即时通讯服务的组件软件。

2003 年 8 月，Ximian 被 Novell, Inc. 收购。Ximian GNOME 分发版（现更名为 Ximian Desktop 2）未包含在 Red Hat 的 Linux 发行版或 Fedora 中，但你可以通过 CD-ROM 安装它，或者如果你拥有宽带接入，可以在不到一小时内通过互联网安装它。有许多针对不同 Linux 发行版的版本可用（即使是基于非 Intel 平台的发行版）。

要开始，你可以访问 Novell 的 Ximian Desktop 网站 `http://www.novell.com/products/desktop/download.html`。首先使用 `wget` 快速下载一个图形安装程序，然后使用它来选择下载站点、选定的文件和基础 Ximian 分发版。下载和安装是一个自动过程，Ximian 会用其自己的 GNOME 分发版替换你默认的 GNOME 软件。安装后，你可以使用 Ximian 桌面上的更新图标快速安装更新和错误修复。

图 6.10 展示了一个代表性的 GNOME 桌面，运行着用于设置主题的 `gconf-tool-2` 客户端。

![](img/774d40fd20903495c5cd00e2efad3f33_217_0.png)

**图 6.10** Fedora 的 GNOME 桌面使用 `metacity` 窗口管理器，并提供 GNOME（和 KDE）主题选择。

你可以通过使用“首选项”菜单下的不同菜单项，以多种方式配置你的桌面。要查看首选项项目的全面图标视图，请从桌面面板的“首选项”菜单中点击“控制中心”菜单项。随后会启动一个名为 Nautilus 的图形外壳。Nautilus 最初由 Eazel 开发（该公司在 2001 年夏天前不久停止了业务）。Nautilus 外壳在 Fedora 桌面中用作文件浏览器和桌面实用工具。

图 6.11 显示了 Nautilus 主窗口，展示了首选项图标。然后你可以点击任何图标（如“背景”或“屏幕保护程序”）及其对话框，以更改桌面的外观、焦点行为、窗口行为、放置、声音和工作区设置。

![](img/774d40fd20903495c5cd00e2efad3f33_218_0.png)

**图 6.11** 你可以使用 Nautilus 图形外壳中可用的首选项设置来自定义 Fedora 桌面。

### KDE：K 桌面环境

KDE 包含在 Fedora 中，自 1996 年以来已可用于 Linux、Xorg 和 XFree86。KDE 是一个图形桌面环境，提供了庞大的客户端套件，包括名为 KOffice 的免费办公套件。KDE 客户端位于 /usr/bin 目录下，几乎所有客户端的名称都以 *k* 开头。

你家中目录下的 `.kde` 目录包含自定义设置和会话信息。你可以使用 KDE 的控制中心（如图 6.12 所示）来自定义桌面设置。你可以通过点击 KDE 桌面菜单（由位于桌面底部的面板托管，称为 *kicker*）中的“控制中心”菜单项，或者从命令行启动此客户端，如下所示：

```bash
$ kcontrol &
```

