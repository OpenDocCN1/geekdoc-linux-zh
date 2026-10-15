

## Qt 库

KDE 使用的 GUI 工具库是 Trolltech（www.trolltech.com）开发并支持的 Qt 库。Qt 被认为是 Unix/Linux 系统上可用的最佳 GUI 库之一。使用 Qt 的优势在于依赖于商业开发和支持的 GUI 库。此外，使用 Qt 库大大减少了 KDE 的开发时间。Trolltech 以开源软件的形式提供 Qt 库，可自由分发。然而存在某些限制：基于 Qt（KDE）的应用程序必须免费且开源，并且不得对 Qt 库进行修改。如果你使用 Qt 库开发应用程序并想出售它，那么你必须从 Troll Tech 购买许可证。换句话说，Qt 库对于免费和开源应用程序是免费的，但对于商业应用程序则不是。

## KDE 桌面

KDE 的目标之一是为用户提供一致的集成桌面，所有应用程序都使用 GUI 界面（见图 7-1）。为此，KDE 提供了自己的窗口管理器（KWM）、文件管理器（Konqueror）、程序管理器和桌面面板（Kicker）。

![](img/6c226e8ba1efd427dec3bf582418d33f_150_0.png)

图 7-1 KDE 桌面

你可以在 KDE 中运行任何其他符合 X Window System 的应用程序，例如 Mozilla，以及任何 GNOME 应用程序。反过来，你也可以在 GNOME 中运行任何 KDE 应用程序，包括 Konqueror 文件管理器。

## KDE 菜单

当你启动 KDE 时，KDE 面板会显示在屏幕底部。面板上放置有菜单和程序的图标，以及不同桌面屏幕的按钮。对于 Bluecurve 界面，KDE 面板被设计成看起来与 GNOME 面板完全相同。在 Red Hat 上，主菜单按钮显示一顶红色的 fedora，就像 GNOME 界面一样（通常这是一个齿轮上的 K 图像，顶部有一个小箭头表示它是菜单）。

这是 KDE 主菜单的按钮。单击此按钮可显示你运行的应用程序菜单（你也可以通过按 ALT-F1 打开主菜单）。从 KDE 菜单中，你可以访问不同类型应用程序的众多子菜单。菜单还包括某些关键项目，如注销，用于退出 KDE；锁定屏幕，用于锁定你的桌面；控制中心，用于配置你的 KDE 桌面；运行命令，用于从命令行运行程序；你的主目录，用于快速浏览你的主目录；以及帮助，启动 KDE 帮助工具。

随 KDE 安装的标准 KDE 应用程序可以通过此菜单访问。在 Bluecurve 上，主菜单的大多数条目与 GNOME 上的条目相同。条目已为两个界面标准化。你可以找到 Internet、系统设置、图形和办公等类别的条目。在 Red Hat 上，这些菜单列出了你可以使用 GNOME 和 KDE 应用程序。More 菜单中包含子菜单，其中条目可能在 KDE 和 GNOME 之间有所不同。例如，在 KDE 中，办公菜单中的 More Office Applications 子菜单显示 KOffice 的条目，如 KWord 或 KSpread。More Internet Applications 菜单包含众多 KDE Internet 应用程序，如 KMail 和 Konqueror Web 浏览器。大多数 KDE 系统工具位于 More System Tools 菜单中，包括 KDiskFree 和 KSystemGuard。这些 More 菜单不限于 KDE 应用程序，有时 KDE 应用程序包含在主菜单中。Red Hat 只是将更可能使用的应用程序放在主菜单中，而将不太可能使用的应用程序放在 More 菜单中。

> 提示 在 KDE 开始这里窗口中，首选项窗口包含的工具与 GNOME 首选项窗口不同，仅显示少数专用配置工具。最好使用主菜单的 Preferences 菜单或 KDE 控制中心来配置 KDE（主菜单上的控制中心）。

## 退出 KDE

要退出 KDE，你可以选择主菜单中的注销条目，或在桌面任何位置右键单击并从弹出菜单中选择注销条目。如果你退出时留下任何 KDE 或 X11 应用程序或窗口打开，它们在再次启动时会自动恢复。如果你只是想锁定桌面，你可以选择主菜单上的锁定屏幕条目，你的屏幕保护程序将出现。要访问锁定的桌面，单击屏幕会出现一个框提示你输入登录密码。输入密码后，你的桌面将重新出现。

