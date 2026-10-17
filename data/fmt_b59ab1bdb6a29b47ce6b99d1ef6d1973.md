
表 2.2 前景和背景

# 通过图形访问 CLI（继续）

图形环境提供了比虚拟控制台多多的 CLI 选项。许多图形化终端仿真器包可供选择。每个包都有其独特的功能和选项。流行的终端仿真器包列在表 2.3 中。

| 名称 | 网址 |
| --- | --- |
| Eterm | http://www.etern.org |
| Final Term | http://finalterm.org |
| GNOME Terminal | https://help.gnome.org/users/gnome-terminal |
| Guake | https://github.com/Guake/guake |
| Konsole | http://konsole.kde.org |
| LillyTerm | http://lillyterm.com.tw/index.html |
| LXTerminal | http://wiki.lxde.org/en/LXTerminal |
| mrxvt | https://code.google.com/p/mrxvt |
| ROXTerm | http://roxterm.sourceforge.net |
| rxvt | http://sourceforge.net/projects/rxvt |
| rxvt-unicode | http://software.schmorp.org/pkg/rxvt-unicode |
| Sakura | https://launchpad.net/sakura |
| st | http://st.suckless.org |
| Terminator | http://launchpad.net/terminator |
| Terminology | http://www.enlightenment.org/p.php?p=terminology |
| tilda | http://tilda.sourceforge.net/tildaabout.php |
| UXterm | http://manpages.ubuntu.com/manpages/guys/man1|uxterm.1.html |
| Wterm | http://sourceforge.net/projects/wterm |
| xterm | http://invisible-island.net/xterm |
| Xfce4 Terminal | http://docs.xfce.org/apps/terminal/start |
| Yakuake | http://extraarge.kde.org/apps/yakuake |

表 2.3 流行的终端仿真器包

虽然有很多图形化终端仿真器包可用，但本章的重点是三种常用的。它们通常默认安装在 Linux 发行版中，它们是 GNOME Terminal、Konsole Terminal 和 xterm。

# 使用 GNOME 终端模拟器

GNOME Terminal 是 GNOME 桌面环境的默认终端模拟器。许多发行版（如 RHEL、Fedora 和 CentOS）默认使用 GNOME 桌面环境，因此默认使用 GNOME Terminal。然而，其他桌面环境（如 Ubuntu Unity）也使用 GNOME 终端作为其默认终端模拟器包。它非常易于使用，对于 Linux 初学者来说，是一个非常好的终端模拟器。本章节将带你熟悉熟悉访问、配置和使用 GNOME 终端模拟器的各个部分。

## 访问 GNOME 终端

每个图形桌面环境都有不同的方法来访问 GNOME 终端模拟器。本节将介绍如何在 GNOME、Unity 和 KDE 桌面环境中访问 GNOME Terminal。

### 注意事项

如果你使用的桌面环境与表 2.3 中列出的不同，你必须浏览你环境中所提供的各种菜单，以找到 GNOME 终端模拟器。在菜单中，它通常命名为 Terminal（终端）。

在 GNOME 桌面环境中，访问 GNOME Terminal 非常简单。从窗口左上角的菜单系统中，点击“Applications（应用程序）”，然后从下拉菜单中选择“System Tools（系统工具）”，最后点击“Terminal（终端）”。用简写表示，路径如下：Applications⇒System Tools⇒Terminal。

参考图 2.1 可以查看 GNOME Terminal 的图片。它是在 CentOS 发行版的 GNOME 桌面环境中访问的。

在 Unity 桌面环境中，访问 GNOME 终端需要多一点精力。最简单的访问方法是 Dash⇒Search（搜索）并输入 Terminal。GNOME 终端会以名为 Terminal 的应用程序形式显示在 Dash 首页区域中。点击该图标即可打开 GNOME 终端模拟器。

提示

在某些 Linux 发行版的桌面环境中（如 Ubuntu 的 Unity），你可以使用快捷键组合 Ctrl+Alt+T 快速访问 GNOME 终端。

在 KDE 桌面环境中，Konsole 终端模拟器是默认模拟器。因此，你必须深入菜单才能访问 GNOME Terminal。从屏幕左下角标记为“Kickoff Application Launcher（启动 应用程序启动器）”的图标开始，然后点击 Applications⇒Utilities（工具）⇒Terminal。

在大多数桌面环境中，你可以为访问 GNOME Terminal 创建启动器。启动器是你在桌面上创建的一个图标，允许你启动选定的应用程序。这是一项很棒的功能，允许你在图形桌面中快速访问终端快捷模拟器。如果你不想使用快捷键，或者你所选的桌面环境中没有快捷键功能，这将特别有帮助。

例如，在 GNOME 桌面环境中，要创建一个启动器，请在桌面区域中间点击鼠标右键；会出现下拉菜单。从菜单中选择“Create Launcher...（创建启动器...）”，打开创建启动器应用程序窗口。在 Type（类型）字段中选择 Application（应用程序）。在 Name（名称）字段中为你的图标输入名称。在 Command（命令）字段中输入 `gnome-terminal`。点击确定保存你的新启动器。一个带有你为启动器命名的图标现在出现在桌面上。双击即可打开 GNOME 终端模拟器。

### 注意事项

当你在 Command 字段中输入 `gnome-terminal` 时，你输入的是启动 GNOME 终端模拟器的 shell 命令。你将在第 3 章中学习如何为命令（如 `gnome-terminal`）添加特殊选项，以提供特殊的配置选项，以及如何查看所有你可用的选项。

应用程序中的菜单和快捷键提供了若干配置选项，你可以在启动 GNOME 终端模拟器后应用这些选项。理解这些选项可以增强你的 GNOME Terminal CLI 体验。

## 菜单栏

GNOME Terminal 菜单栏包含所需的配置和自定义选项，让你的 GNOME Terminal 完全符合你的喜好。以下表格简要描述了菜单栏中的不同配置选项以及与这些选项相关的快捷键。

### 注意事项

在阅读这些 GNOME Terminal 菜单选项时，请记住你的 Linux 发行版的 GNOME Terminal 可能有略有不同的可用选项。这是因为某些 Linux 发行版使用了旧版本的 GNOME Terminal。

表 2.4 显示了文件（File）菜单。文件菜单包含以下项。

**表 2.4 文件菜单**

| 名称 | 快捷键 | 描述 |
|---|---|---|
| Open Terminal | None | 打开终端 |
| Open Tab | Shift+Ctrl+T | 打开标签页 |
| New Profile | Shift+Ctrl+N | 创建新配置文件 |
| Save Contents | None | 保存内容 |
| Close Tab | Shift+Ctrl+W | 关闭标签页 |
| Close Window | Shift+Ctrl+Q | 关闭窗口 |
| Reset | None | 重置终端会话 |
