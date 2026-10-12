
31: `fi`
32: `fi`
33: # 最后，尝试 `AnotherLevel`
34: # 这些文件是 `NextLevel` 留下的。
35: `rm -f $HOME/.Xrootenv.0`
36: `rm -f /tmp/fvwmrc>/dev/null`
37: # 第一件事 - 检查用户偏好
38: `if [ -f $HOME/.wm_style ]; then`
39: `WMSTYLE=$(cat $HOME/.wm_style)`
40: `case "$WMSTYLE" in`
41: `AfterStep | AfterStep)`
42: `exec /usr/X11/bin/RunWM -AfterStep`
43: `WindowMaker | Windowmaker | wmaker)`
44: `exec /usr/X11/bin/RunWM -WindowMaker`
45: `Fwm95 | fwm95)`
46: `exec /usr/X11/bin/RunWM -Fwm95`
47: `Mwm | Mwm | Lesstif`
48: `exec /usr/X11/bin/RunWM -Fwm`
49: `esac`
50: `fi`
51: # 哎！什么都没有安装。回退到 `fvwm` (`style`) 或
52: `/usr/X11/bin/RunWM -Fwm95 ||`
53: # 天哪，`fvwm` 和 `twm` 都不可用；回退到安全设置
54: `xclock -geometry 100x100 &`
55: `xterm -geometry 80x50 &`
56: `netscape -geometry 150 &`
57: `if [ -f /doc/HTML/index.html ]; then`
58: `else`
59: `exec fwm`
60: `exec twm` 让我们拆解 `Xclients` 文件的步骤：

- 第 4 到 13 行：设置偏好的桌面。正如在第 11 章“使用 KDE”中所讨论的，你可以使用第 4 行中的 `PREFERRED` 变量设置你偏好的桌面。如果 `PREFERRED` 未设置任何桌面，则根据 `/etc/sysconfig/desktop` 中针对 `GNOME`、`KDE` 和 `AnotherLevel` 选择的默认值。

- 第 14 到 18 行：确保 `PREFERRED` 桌面不是 `AnotherLevel`。

- 第 21 到 36 行：通过删除上次运行窗口可能留下的临时文件来执行清理工作。

- 第 38 到 54 行：检查 `AnotherLevel` 窗口管理器的样式，并以该样式启动 `AnotherLevel` 后退出脚本。

- 第 56 到 69 行：尝试用 `Fwm95` 样式启动 `AnotherLevel`。如果失败，则启动 `xclock`、`xterm` 和 `Netscape`，然后尝试启动存在的 `fwm`。如果不存在，则改为启动 `twm`。

## X Resources

如果你想在每次启动窗口时运行你自己的客户端，可以将全局 `Xclients` 文件复制到你家目录下的自己的 `Xclients` 文件中（第 14 章“处理文件”描述了文件复制），然后对其进行编辑。此过程的关键是在可能启动不同窗口管理器的部分之前添加要运行的程序命令。之所以这样做是因为，用于启动不同窗口管理器的 `exec` 关键字会导致脚本在窗口管理器启动后停止。

X resources 数据库为应用程序提供了偏好信息，用于控制颜色和字体等属性。大多数窗口应用程序都可以使用 X resources 来控制几乎所有由命令行标志控制的各个方面。通过 X resources 数据库，你可以指定比应用程序标准更合适的默认值。

## X Resources 如何工作

每当你启动 X 窗口时，不同的设置会被加载到 X resources 数据库中。默认设置来自列出的各种文件。大多数窗口应用程序可以使用 X resources 来控制几乎所有由命令行标志控制的各个方面。通过 X resources 数据库，你可以指定比应用程序标准设置更合适的默认值。

通常，默认设置位于 `.initrc` 文件。

## 通过 .defaults 设置 X Resources

设置 X resources 涉及到将条目加载到 X resources 数据库。这些条目的格式如下：

```
<ApplicationClass>|<ResourceName> : <value>
```

在 Windows 中，竖线（或管道字符 :) 通常用于表示“或”。因此，在上面的示例中，第一项使用 `<ApplicationClass>`，第二项使用 `<ResourceClass>`。这些值通常放在 `.defaults` 中。让我们来看看示例 `.defaults`：

```bash
*background: Black
*foreground: Wheat
*cursorColor: Orchid
*reverseVideo: false
*scrollbar: true
*reverseWrap: true
*font: fixed
*fullCursor: true
*scrollOutput: off
*scrollKey: on
*titleBar: false
clock*Geometry: 100x100+100
```

此 `.defaults` 文件为 Xterm 类和 `clock` 设置了 X resources。

## X resources 数据库

`clock`，你看到颜色和几何形状被设置了。这些资源所采用的值与提供命令行标志如 `-fg` 和 `-geometry` 的相同。

X resources 的来源是 `app-defaults` 文件。大多数 X 和 KDE 应用程序都有 `app-defaults` 文件。你可以查看这些文件以获取 `.defaults` 文件中的设置。在 Linux 7 中，这些文件位于 `/usr/X11R6/lib/X11/app-defaults/`。KDE 应用程序拥有特殊的 `app-defaults` 文件，位于 `/usr/share/kdisplay/app-defaults/`。

## 使用 xrdb 命令加载 X Resources

通常，`defaults` 在 X 启动时加载。然而，可以在 X 运行时通过 `xrdb` 命令将新值加载到数据库。这对于实验值组合特别有用。

如果你在一个名为 `experiment` 的文件中设置了实验性，可以使用命令将这些设置临时加载到数据库：

```
$ xrdb -merge experiment
```

一旦你对任何更改满意，可以将实验文件中的设置添加到 `.defaults` 中，以便引入未来的 Windows 会话。

## 展望

本章结束了对 Windows 的关注。现在你将进入一个对精通 Linux 至关重要的领域：命令行环境。

第 13 章“介绍 Linux 命令”和第 14 章“处理文件”描述了 Linux 命令的基础。它们讨论了基础命令以及如何处理驱动器上的文件和目录。在随后的章节中，你将学习 `shell`，它提供了一个强大的命令行工作环境，你将学习如何使用图形化 Red Hat 控制工具来简化 Linux 系统配置中一些晦涩的方面。

# 第四部分

# 掌握核心要素

- 第 13 章：介绍 Linux 命令
- 第 14 章：文件操作
- 第 15 章：使用 `LinuxConf` 和其他工具进行系统配置
- 第 16 章：理解 Shell
- 第 17 章：通用系统管理
- 第 18 章：外设的使用
- 第 19 章：Linux 多媒体
- 第 20 章：重新编译 Linux 内核

# 第 13 章

# 介绍 Linux 命令

- 什么是 Linux 命令？
- 执行 Linux 命令
- 常用 Linux 命令

## 292 第13 章 • 介绍 Linux 命令

在本章中，你将开始对 Unix 命令行环境的探索。命令行环境是 Linux 的核心和威力所在。你已经看到 X Windows 提供了快速方便访问图形化应用程序的途径，这让大多数用户能够立即开始工作。然而，缺失的是完全操作和处理 Linux 系统的能力。这种能力在你开始尝试命令时就会出现。

在这里，你将学习使用一些更常用的命令，例如 `ls`、`find` 和 `grep`。由于这些命令存在于大多数发行版中，Unix 用户应该立即知道这些命令以及类似命令可以做什么，以及在知识丰富的用户手中能提供什么力量。

> 对于本章，你需要使用 Linux 命令行。你可以通过两种方式获取命令行：系统启动时，登录到 Unix 虚拟控制台之一；或者从 X Windows 启动终端窗口，如 `xterm`、GNOME 终端或 KDE 的 `Console`。

## 什么是 Linux 命令？

在查看特定命令之前，你需要确切地理解“命令”一词的含义。
