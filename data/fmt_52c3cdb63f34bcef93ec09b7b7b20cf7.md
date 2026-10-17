
图 1-4：Ubuntu 8.10 中的默认 GNOME 桌面。

GNOME 开发者制作了大量与 GNOME 桌面集成的图形应用程序。这些应用程序显示在表 1-3 中。

### 表 1-3：GNOME 应用程序

| Application | Description |
|---|---|
| epiphany | Web browser |
| evince | Document viewer |
| gcalc-tool | Calculator |
| gedit | GNOME text editor |
| gnome-panel | Desktop panel for launching applications |
| gnome-nettool | Network diagnostics tool |
| gnome-terminal | Terminal emulator |
| nautilus | Graphical file manager |
| nautilus-cd-burner | CD-burning tool |
| sound juicer | Audio CD-ripping tool |
| tomboy | Note-taking software |
| totem | Multimedia player |

正如你所见，GNOME 桌面可用的应用程序相当多。其中一些应用程序默认包含在 Ubuntu 中，而其他则需要从 Ubuntu 仓库安装。除了所有这些应用程序之外，其他 Linux 应用程序还使用 GNOME 库来创建在 GNOME 桌面上运行的基于 Windows 的应用程序。

# KDE 桌面

K 桌面环境（KDE）于 1996 年首次发布，作为一个开源项目，旨在制作一个类似于 Microsoft Windows 环境的图形桌面。KDE 桌面包含了如果你是 Microsoft Windows 用户所熟悉的全部功能。图 1-5 显示了在 Kubuntu Linux 上运行的示例 KDE 桌面。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_45_0.png)

**图 1-5：** Kubuntu 8.10 中的默认 KDE 桌面。

就像在 Microsoft Windows 中一样，KDE 桌面允许你将应用程序和文件图标放置在桌面区域。与 Windows 不同的是，如果你单击一个应用程序图标，KDE 系统就会启动该应用程序。如果你单击一个文件图标，KDE 桌面会尝试确定要启动什么应用程序来处理该文件。

桌面底部的栏称为面板。面板由四个部分组成：

- **K 菜单：** 类似于 Windows 开始菜单；包含启动已安装应用程序的链接
- **程序快捷方式：** 从面板直接启动应用程序的快速链接
- **任务栏：** 显示桌面上当前正在运行的应用程序的图标
- **小程序：** 在面板中具有图标的小型应用程序，通常可以根据来自应用程序的信息而更改

所有面板功能都与你在 Microsoft Windows 中找到的功能相似。除了桌面功能之外，KDE 项目还制作了大量在 KDE 环境中运行的应用程序。这些应用程序显示在表 1-4 中。

### 表 1-4：KDE 应用程序

| Application | Description |
|---|---|
| amaroK | Audio file player |
| digiKam | Digital camera software |
| K3b | CD-burning software |
| Kaffeine | Video player |
| Kmail | Email client |
| Koffice | Office applications suite |
| Konqueror | File and web browser |
| Kontakt | Personal information manager |
| Kopete | Instant messaging client |

你可能会注意到 KDE 应用程序名称中使用大写 K 的趋势。这只是 KDE 项目生产的应用程序的部分列表。KDE 项目中还有许多其他应用程序。与 GNOME 环境类似，Kubuntu 默认不包含所有 KDE 项目软件，但你可以使用软件仓库轻松安装任何内容。

# 其他桌面

华丽的图形桌面环境的缺点是它需要相当多的系统资源才能正常运行。在 Linux 的早期，Linux 的标志和卖点之一是它能够在较旧、性能较低的 PC 上运行，而较新的 Microsoft 桌面产品无法在这些 PC 上运行。然而，随着 KDE 和 GNOME 桌面的流行，这一标志已经改变，运行 KDE 或 GNOME 桌面所需的内存几乎与最新的 Microsoft 桌面环境一样多（Ubuntu 的最低要求为 384 MB 内存）。

如果你有一台较旧的 PC，不要气馁。Linux 开发者们团结起来，将 Linux 带回其根源。他们创建了几个面向低内存的图形桌面应用程序，提供基本功能，可以在较旧的 PC 上完美运行。

尽管这些图形桌面没有大量围绕它们设计的应用程序，但它们仍然运行许多支持诸如文字处理、电子表格、数据库、绘图，当然还有多媒体应用程序等功能的基本图形应用程序。表 1-5 显示了一些可用于低功率 PC 和笔记本电脑的较小的 Linux 图形桌面环境。

### 表 1-5：其他 Linux 图形桌面

| Desktop | Description |
|---|---|
| xfce | 一个轻量级桌面，将组件单独打包，以便您可以挑选和选择想要实现的功能 |
| fluxbox | 一个精简的桌面，不包含面板——只有用于启动应用程序的弹出菜单 |
| fvwm | 支持一些高级桌面功能，例如虚拟桌面和面板，但在低内存环境中运行 |
| fvwm95 | 源自 fvwm，但设计成看起来像 Windows 95 桌面 |

这些图形桌面环境不如 KDE 和 GNOME 桌面那么花哨，但它们提供了基本图形功能。图 1-6 显示了在 Xubuntu 发行版中使用的 xfce 桌面是什么样子的。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_47_0.png)

**图 1-6：** 在 Xubuntu 8.10 发行版中看到的默认 xfce 桌面。

如果您使用的是较旧的 PC，请尝试使用其中一个桌面环境的 Linux 发行版，看看会发生什么。您可能会感到愉快的惊讶。

# Linux 发行版

现在您已经看到了构成完整 Linux 系统所需的四个主要组件，您可能会想知道如何将它们全部组合起来制作一个 Linux 系统。幸运的是，已经有人为我们完成了这项工作。

完整的 Linux 系统包称为发行版。有许多不同的 Linux 发行版可供选择，以满足几乎任何计算需求。大多数发行版都是为特定用户群体定制的，例如企业用户、多媒体爱好者、软件开发人员或普通家庭用户。每个定制发行版都包含支持专业功能的软件包，例如为多媒体爱好者提供的音频和视频编辑软件，或为软件开发人员提供的编译器和集成开发环境（IDEs）。

Linux 发行版通常分为三个类别：

- ♦ 全核心 Linux 发行版
- ♦ 专用发行版
- ♦ LiveCD 测试发行版

以下各节描述了这些不同的 Linux 发行版，并在每个类别中展示了一些 Linux 发行版的示例。

## 核心 Linux 发行版

核心 Linux 发行版包含一个内核、一个或多个图形桌面环境，以及几乎所有可用的 Linux 应用程序，均预编译用于该内核。它为完整的 Linux 安装提供一站式服务。表 1-6 显示了一些更受欢迎的核心 Linux 发行版。

### 表 1-6：核心 Linux 发行版

| Distribution | Description |
|---|---|
| Slackware | 最早的 Linux 发行版之一，深受 Linux 发烧友欢迎 |
| Red Hat | 一种商业业务发行版，主要用于 Internet 服务器 |
| Fedora | Red Hat 的分支，但设计用于家庭使用 |
| Gentoo | 专为高级 Linux 用户设计的发行版，仅包含 Linux 源代码 |
| Mandriva | 主要设计用于家庭使用（以前称为 Mandrake） |
| openSUSE | 针对企业和家庭使用的不同发行版（现由 Novell 所有） |
| Debian | 深受 Linux 专家和商业 Linux 产品欢迎 |

在 Linux 的早期，发行版以软盘集的形式发布。您必须下载一组文件，然后将它们复制到磁盘上。通常需要 20 多张磁盘才能制作完整的发行版！不用说，这是一次痛苦的经历。

如今，随着家用电脑普遍内置 CD 和 DVD 播放器，Linux 发行版以 CD 套装或单张 DVD 的形式发布。这使得安装 Linux 变得更加容易。
