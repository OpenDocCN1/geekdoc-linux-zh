

## Red Hat Linux 6.0 入门指南

你在 GNOME Pager 右侧任务列表中最小化的应用程序。按下该应用程序的按钮，它就会返回到你的桌面。

![](img/46f4935125ba89e12897afbe9d77a097_543_0.png)

你可以在第 12 章中名为 GNOME Pager 的章节中阅读更多关于 GNOME Pager 的内容。

以下各节将更详细地介绍，描述系统的每个组件。

## 3 窗口管理器和 GNOME

### 关于窗口管理器

窗口管理器是控制 X 窗口环境中窗口的软件部分。任何窗口的放置、边框和装饰都由窗口管理器管理。这与许多其他操作系统非常不同，而且 GNOME 处理窗口管理器的方式也与其他桌面环境不同。

正如本指南前面所述，GNOME 不依赖于任何一个窗口管理器。这意味着当你决定切换窗口管理器时，你的桌面环境的主要部分不会发生变化。GNOME 与窗口管理器协同工作，为你提供最简单的工作环境。GNOME 不担心窗口的放置，而是从窗口管理器获取有关其放置的信息。GNOME Pager 仅适用于符合 GNOME 的窗口管理器，并且该管理器能够在桌面上拖放。

在本版 GNOME 用户指南发布时，Enlightenment 窗口管理器是唯一 100% 符合标准的窗口管理器。还有许多其他窗口管理器是部分符合标准或正在开发中以达到符合标准。

在本版 GNOME 用户指南发布时，部分到完全符合标准的窗口管理器有：

- Enlightenment - http://www.enlightenment.org
- Icewm - http://www.kiss.uni-lj.si/~k4fr0235/icewm/
- Window Maker - http://www.windowmaker.org
- FVWM - http://www.fvwm.org/

### 更改窗口管理器

你可以在任何时候通过在 GNOME 控制中心中使用窗口管理器小程序来更改正在使用的窗口管理器。你可以在第 10 章中名为 *Window Manager Capplet* 的章节中阅读更多关于此小程序的内容。

**重要提示：** 请记住，你选择的窗口管理器可能与 GNOME 不兼容，如果使用它，你可能无法享受到 GNOME 的某些功能。

## 4 Enlightenment 窗口管理器

### 简介

GNOME 是一个桌面环境，不依赖于任何一个窗口管理器来控制应用程序和其他功能之间的交互方式。GNOME 可以与各种窗口管理器协同工作。窗口管理器控制窗口边框、窗口装饰以及这些窗口的功能。目前大约有三到四个窗口管理器被认为是符合 GNOME 标准的。符合 GNOME 标准意味着不仅仅是能够与 GNOME 一起运行；它还意味着了解 GNOME 以及 GNOME 提供的功能。这包括会话管理、桌面设置，以及与 GNOME Pager 等应用程序的交互。

本版 Red Hat Linux 的默认窗口管理器是一个名为 Enlightenment 的窗口管理器。在 Enlightenment 中，有一个工具可以帮助你根据自己的规格配置窗口管理器。

### Enlightenment 配置工具

启动 Enlightenment 配置工具（E-conf）有两种方法。你可以打开 GNOME 控制中心并从桌面组中选择窗口管理器小程序。如果你当前使用的是 Enlightenment 作为窗口管理器，你可以通过按下运行 Enlightenment 配置工具按钮来运行 E-conf。

你也可以通过在桌面上点击鼠标中键（或如果你使用仿真，则同时按下左右鼠标键）并从弹出菜单中选择 Enlightenment 配置项来启动 E-conf。

E-conf 分为许多部分，控制 Enlightenment（E）内的各种效果和功能。你会找到这些部分的列表

