

Linux 和 Mac OS X。X.Org 最初以 XFree86 的形式实现，当 XFree86 许可证中要加入某些限制时引发了争执，于是 X.Org 被分叉出来。基于在旧版许可证下授权的代码快照，X.Org 在此基础上推进了自己的实现。几乎同时，大多数 Linux 发行版都抛弃了 XFree86，转而将开发和工作重心转向 X.Org。

在本章中，你将学习如何使用 Gnome 以及 Ubuntu 中包含的 X 版本。我们将探讨 X 的基本原理，以及如何让 X 在可能影响它的升级后继续工作，例如新显卡或你刚买的那块新平板显示器。我们还将查看 Ubuntu 中包含的其他一些窗口管理器，包括 KDE 和 Xfce。

## Ubuntu 家族

当人们谈论 Ubuntu 时，他们通常指的是 2004 年发布的原始发行版，该版本使用 Gnome 窗口管理器。然而，Ubuntu 还有许多衍生版本，它们使用其他窗口管理器，并且你可以自由下载使用。例如，Kubuntu 使用 KDE 窗口管理器，而 Xubuntu 则使用 Xfce。尽管它们在视觉上差异很大，但这三者都依赖于相同的核心系统，而且你也可以通过使用其中一个 *-desktop 元包轻松地将该窗口管理器添加到现有系统中。这些包旨在安装与该 Ubuntu 版本关联的所有基础应用程序，因此安装 kubuntu-desktop 包将自动安装 Kubuntu 所需的所有软件，同时保留你现有的桌面环境。

## Gnome 桌面环境

X 的桌面环境提供一个或多个窗口管理器以及一套遵循基于通用软件库的标准图形界面的客户端。当用于开发相关客户端时，这些库为客户端窗口、菜单、按钮和其他屏幕组件提供图形一致性，同时提供一些通用的键盘控制和客户端对话框。以下各节讨论的是 Ubuntu 中包含的主要桌面环境：Gnome。

## Gnome：GNU Network Object Model Environment

Gnome 项目始于 1997 年，是程序员奇才 Miguel de Icaza 的创意。Gnome 提供了一整套软件库和客户端。Gnome 依赖于 Gnome 感知的窗口管理器。这意味着要提供包含 Gnome 元素的图形桌面，窗口管理器必须编写为能够识别并使用 Gnome。一些兼容的 Gnome 感知窗口管理器包括 Compiz（Ubuntu 中默认的 Gnome 窗口管理器）、Enlightenment、Metacity、Window Maker、IceWM 和 beryl。

Ubuntu 使用 Gnome 的用户友好型客户端套件来提供一致且用户友好的桌面。Gnome 客户端位于 /usr/bin 目录下，Gnome 配置文件存储在 /etc/gnome 和 /usr/share/gnome 目录下，用户设置存储在主目录下的 .gnome 和 .gnome2 中。

一个典型的 GNOME 桌面，运行用于设置事件操作的便携式媒体首选项工具，如图 3.1 所示。

![](img/8f9e74e2b343ff525bebfb720a3d8441_82_0.png)

图 3.1 Ubuntu 的 Gnome 桌面使用 Compiz 窗口管理器并提供多种 Gnome 主题选择。

你可以通过多种方式配置桌面，并通过主桌面菜单中的首选项菜单下的不同菜单项进行配置。众多的配置选项允许你定制系统外观和感觉的各个方面。在图 3.2 中，你可以看到可供使用的首选项选项的选集。

![](img/8f9e74e2b343ff525bebfb720a3d8441_82_1.png)

图 3.2 你可以通过系统、首选项菜单中提供的首选项设置来自定义 Ubuntu 桌面。

