

![](img/8f9e74e2b343ff525bebfb720a3d8441_104_0.png)

**图 3.16** 当你准备切换到另一个环境时，使用登录窗口进行跳转。

self to switching permanently. Take the opportunity to try the new environment and make your mind up if you want to switch to it full time.

如果你已经决定永久切换，那么可以通过两种途径之一来实现。第一种方法是打开登录窗口（在 Gnome 下位于 系统、系统管理、登录窗口，也可在 KDE 下通过 Kicker 菜单、系统、登录窗口找到），然后从“默认会话”下拉列表中选择相关的窗口管理器，如图 3.16 所示。

或者你也可以在登录窗口中按 F10，点击“选择会话”，选择你想要的窗口管理器并选择“设为默认”。这样会将你的默认窗口管理器设置为你指定的选择。

无论你选择哪种方式，如果不喜欢新的环境，改回原设置都很简单。

![](img/8f9e74e2b343ff525bebfb720a3d8441_105_0.png)

图 3.17 KDE 提供了无限的定制选项；只需做好切换的准备！

![](img/8f9e74e2b343ff525bebfb720a3d8441_105_1.png)

图 3.18 XFce——轻量与简洁融为一体，打造出优秀的套件。

下一节将简要介绍除 Gnome 之外，在 Kubuntu 或 Xubuntu 中可用的另外两个主要窗口管理器。

## KDE——另一个环境

Ubuntu 的一大优点就是它提供的选择。当 Ubuntu 最初发布时，它偏爱 Gnome 桌面，但很快就决定创建一个名为 Kubuntu 的 KDE 替代版本。如果你安装 kubuntu-desktop 包（使用 apt-get 或 synaptic），你将可以使用 KDE 以及相关的 Kubuntu 应用程序。

KDE 与 Gnome 有所不同，因为它使用 QT 库而不是 GTK 库，因此窗口和其他元素看起来不同。Linus Torvalds 本人过去曾明确表示更喜欢 KDE，而且 KDE 还允许你以几乎可以想象的任何方式自定义工作环境。

标准的 KDE 桌面如图 3.17 所示。

## XFce

XFce 是另一种桌面环境，适用于内存或处理能力不高的计算机。它基于 Gnome 使用的相同 GTK 库，因此在外观和感觉上与 Gnome 桌面有相似之处。尽管如此，它捆绑了一系列 Xfce 专属应用程序，用以替代 Gnome 工具，如 nautilus。

有些人只是更喜欢 XFce 的简洁性，因此是否使用它由你决定。你可以通过安装 xubuntu-desktop 包（使用 apt-get 或 synaptic）来获得访问权限，示例桌面如图 3.18 所示。

## 参考

- http://www.x.org/—Curators of the X Window System.
- http://www.x.org/Downloads_mirror.html—Want to download the source to the latest revision of X? Start at this list of mirror sites.
- http://www.xfree86.org/—Home of The XFree86 Project, Inc., which provided a graphical interface for Linux for nearly 10 years.
- http://www.kde.org/—The place to get started when learning about KDE and the latest developments.
- http://www.gnome.org/—The launch point for more information about GNOME, links to new clients, and GNOME development projects.
- http://www.compiz.org/—The official page for the Compiz project, including Compiz Fusion, a set of plugins for the Compiz window manager.
- http://www.xfce.org/—The official home page for the XFce project.

## 第 4 章

## 命令行快速入门

## 本章内容

- 什么是命令行？
- 登录 Linux 并使用 Linux
- 进入命令行
- 使用文本编辑器
- 处理权限
- 以 root 身份工作
- 阅读文档
- 参考

命令行是使用 Ubuntu 乃至 Linux 可用的最强大的工具之一。掌握与其相关的命令以及如何将它们组合起来，将使你在 Ubuntu 上的生活变得轻松许多。

本章介绍你在命令行上保持高效所需了解的一些基本命令。你将了解如何进入命令行，以及如何使用用于在文件系统中导航的命令。本书后面有《命令行大师课》（第 30 章），将更深入地探讨该主题。本章学到的技能将在你需要使用命令行工作时给你信心。

## 什么是命令行？

在 Linux 用户身边待上一段时间，你很快就会听到他们以低声细语谈论命令行或终端。确实如此，因为命令行提供了一种独特而强大的方式与 Linux 交互。然而，在大多数情况下，你可能永远不需要访问命令行，因为 Ubuntu 提供了大量图形工具，可让你配置系统上的大多数内容。

但有时会出现问题，你可能没有图形界面的奢侈可供使用。在这些情况下，对命令行及其用途的基本理解可以成为真正的救命稻草。

