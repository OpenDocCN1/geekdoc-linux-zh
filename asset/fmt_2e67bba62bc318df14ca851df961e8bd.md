
![](img/7a908c965299f9cdfda2a4ea3cd98bf4_206_0.png)

## The X Window

需要理解的术语：

- `startx`, `xdm`
- `.xinitrc`, `Xsession`
- `X11`, `XF86Config`
- `X Server`, `Display Manager`, `Widgets`
- `Window manager`, `applications`
- `SuperProbe`, `xf86config`, `XF86Setup`, `Xconfigurator`, `SaX`
- `GNOME`, `KDE`, `fvwm`, `Enlightenment`, `AfterStep`, `WindowMaker`, `Blackbox`
- `Virtual display`

需要掌握的技术：

- 描述 X Window 的启动方式
- 理解 X Server 配置文件的结构
- 描述 X Window 的五个主要组件
- 定位不同的 X11 配置文件和程序
- 使用各种 X Window 配置实用程序
- 描述多个窗口管理器的特点
- 管理 X Windows 内部的信息

在本章中，您将使用 X Window，它是 Linux 图形用户界面（GUI）。Linux X Window 系统几乎完全是模块化的。它基于多种不同类型的配置文件和实用程序运行。不同的窗口管理器为您的 GUI 桌面提供不同的“外观和感觉”。

## Starting the X Window

您可以从命令行界面启动 X Window，也可以将其设置为通过 `/etc/inittab` 配置文件自动启动。无论您使用 X Window 启动命令 `startx` 还是 `xdm`（X Display Manager），X Window 启动程序都会使用基于您硬件的配置文件。然后它会运行系统范围和用户特定的初始化文件。

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_207_0.png)

X Window 也被称为 `X11`。

### X Window Start Commands

启动 X Window 有两种基本方法。您可以在命令行界面登录并使用 `startx` 命令，或者在登录后运行 `xdm` 命令以启动 X 登录窗口。如果您有一个专门用于 `xdm` 的 init 级别，您可以设置 `/etc/inittab` 文件以确保 Linux 在该运行级别启动。

由于 `startx` 是一个 Linux 脚本，您可以使用文本编辑器查看其中的初始化文件。如果您已经设置了 `xdm`，其初始化文件将优先。

在任何一种情况下，`startx` 或 `xdm` 首先检查用户的 home 目录中的配置文件。如果没有可用文件，它然后检查系统范围的初始化文件，这些文件通常位于 `/etc/X11/xinit` 目录的子目录中。

*注意：根据您的发行版，您可能还可以使用 X 之类的命令来启动 X Window。*

### Configuration Files

关键配置文件是 `/etc/X11/XF86Config`，它设置您的鼠标、键盘、监视器和视频控制器。虽然 Linux 可以检测许多视频控制器和监视器的设置，但通过自定义此文件通常可以提高系统的性能。示例文件 `xf86config.eg` 包含自定义 `/etc/X11/XF86Config` 的指南，可分为八个主要部分：

- Files—包括颜色和字体的文件位置。
- `ServerFlags`—控制 X Window 对特殊命令的响应。例如，您可以使用 Ctrl+Alt+Backspace 退出 X Window。此部分中的 `DontZap` 命令会禁用此选项。
- `Keyboard`—设置键盘的参数。包括特殊键的设置以及键盘功能，例如 Num Lock 和 Auto Repeat。
- `Pointer`—设置指向设备，通常是鼠标。鼠标选项包括协议（Microsoft、PS/2、Logitech 等）、每秒位数（波特率）和三键仿真。
- `Monitor`—设置监视器允许的水平和垂直频率范围。设置过高可能会使监视器过载。也设置监视器的刷新率。
- `Device`—提供视频控制器的设置，包括允许的水平和垂直频率范围。
- `Screen`—提供允许的和默认的图形模式，指定监视器上显示的像素数量和尺寸。示例模式为 640×480、800×600 和 1024×768。
- `Xinput`—提供其他输入硬件的设置，例如带图形平板的笔、游戏适配器甚至触摸屏。

注意：在 Red Hat Linux 中，可能需要按两次此键组合。

上述列表只是可能选项的冰山一角。完整列表可在 `XF86Config` 文件的手册页中找到。

注意：三键仿真允许您在需要三个按钮的地方使用两个按钮鼠标。启用时，您可以通过同时按下左右按钮来模拟中间按钮。

### Initialization Files

有两个主要的初始化文件。`xinitrc` 文件与 `startx` 相关联，`Xsession` 文件与 `xdm` 相关联。`/etc/X11/xinit` 目录中的主要初始化文件是脚本，它们会让位于用户 home 目录中对应的文件。一旦做出选择，初始化文件就会调用其他脚本来分配资源，如内存、键盘设置、窗口管理器和 `XF86Config` 文件。

注意：如果您在 home 目录中有 X Window 初始化文件，它们可能被隐藏。您可以使用 `ls -a` 命令列出它们。隐藏文件如 `.xinitrc` 前面有一个句点。请记住，用户和系统范围的配置文件的实际位置会有所不同。

## X Window Architecture

如前所述，X Window 是模块化的。您可以从不同类别中混合搭配组件。无论您选择哪些组件，设置 X Window 架构都需要五组不同的组件：服务器、显示管理器、部件、窗口管理器和应用程序。

`X Server` 直接与视频硬件通信。显示管理器设置 X Window 环境并设置登录屏幕。您在 GUI 中看到的基本项目，例如菜单栏，是由部件构建的。实际的 GUI 是窗口管理器，所有 GUI 应用程序都应与任何窗口管理器配合使用。该系统可以通过网络以客户端-服务器方式设置。

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_209_0.png)

> 当您设置 X Window 时，Linux 首先启动 X Server，将您的计算机置于图形模式。然后它可以启动显示管理器以允许您登录。一旦登录，Linux 就会启动您选择的窗口管理器。

### Server

尽管名称如此，X Server 设置在客户端计算机上。它直接与您的视频控制器通信。在 Linux 在监视器上绘制图片之前，X Server 会将信息发送到您的视频硬件。无论输入来自应用程序还是鼠标，X Server 都会处理此数据并向您的视频控制器发送适当的输入/输出命令。

### Display Manager

您看到的显示管理器是一个图形登录屏幕。一些窗口管理器，例如 `KDE`（K Desktop Environment）和 `GNOME`（GNU Network Object Model Environment），有自己的显示管理器。其他如 `xdm`，则在 `/etc/inittab` 文件的特定级别配置。您看到的屏幕因 Linux 发行版而异。无论使用哪种显示管理器，成功登录都会激活窗口管理器。

### Building Blocks (Widgets)

在 Linux 中，部件是一个库程序。开发人员从部件构建窗口管理器的组件。这些组件包括菜单栏、滚动条、任务栏等。不同的窗口管理器可能由不同的部件库构建。

### 窗口管理器

窗口管理器决定 GUI 在显示器上的外观。有多种不同的窗口管理器可供选择，包括 `GNOME`、`KDE`、`Afterstep`、`Window Maker`、`fvwm`、`Blackbox` 和 `Enlightenment`。

两个最常见的默认窗口管理器是 `GNOME` 和 `KDE`。`GNOME` 窗口管理器基于 `GTK+` 小部件库构建。`KDE` 窗口管理器基于 `Qt` 小部件库构建。

### 应用程序

在大多数情况下，GUI 应用程序（如 Netscape Communicator 和 WordPerfect）与 X Window 架构一起工作，但并不属于其一部分。尽管如此，GUI 应用程序也会存储用户特定的配置文件。你的主目录中可能已经存在一些隐藏的应用程序配置文件。

`GNOME` 和 `KDE` 软件包包含诸如办公套件之类的应用程序。

## X Window 配置实用程序

编辑 `XF86Config` 文件对于除最熟练的管理员之外的所有人来说都可能是一个困难的过程。有许多优秀的工具可以帮助你配置此文件。尽管其中一些工具是图形化的，但它们不会像其他 Linux GUI 实用程序那样存在感知缺陷。换句话说，它们是可靠的。在大多数情况下，它们包含了大多数管理员配置系统所需的全部功能。

其中一些实用程序甚至可以帮助你安装或修改键盘和鼠标的设置。

![](img/7a908c965299f9cdfda2a4ea3cd98bf4_210_0.png)

> 在启动这些实用程序之前，请备份你的 X Server 配置文件，通常位于 `/etc/X11/XF86Config`。

## SuperProbe
