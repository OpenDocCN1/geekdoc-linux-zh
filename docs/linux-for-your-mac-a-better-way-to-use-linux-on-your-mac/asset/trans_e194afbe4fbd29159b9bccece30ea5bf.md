
表 8.1 **X 终端客户端**

| **名称** | **描述** |
|---|---|
| **aterm** | Afterstep X VT102 终端仿真器 |
| **cmdtool** | OpenWindows 终端 shell |
| **Eterm** | 用于 X 的 Enlightened 终端仿真器 |
| **gnome-terminal** | GNOME X 终端仿真器 |
| **konsole** | KDE 终端仿真器 |
| **kvt** | KDE 终端仿真器（基于 `rxvt`） |
| **nxterm** | 基于 `xterm` 的终端仿真器 |
| **rxvt** | 一种 X 终端仿真器 |
| **wterm** | Window Maker 终端仿真器 |
| **xfterm** | 用于启动终端以读取文件或目录的脚本 |
| **xterm** | XFree86 默认终端仿真器 |

在你的 X 会话中，你最有可能继续使用桌面环境提供的默认终端。然而，一些 Linux 发行版，例如 SuSE，也会在 Shell 菜单中提供整个系统的终端套件，通常是通过面板菜单访问的。你可以从命令行启动任何你喜欢的终端。

## 设置终端字体

当你使用符合 KDE 和 GNOME 标准的终端时，你会使用菜单和对话框来更改终端的字体、颜色方案或大小（尽管某些终端支持未记录的命令行选项）。其他终端则需要命令行选项或其他方法来修改或激活功能。

例如，通过按下 Ctrl 键和鼠标右键（按钮 3），你可以为 xterm 客户端选择新的字体大小。像这样启动终端：

```
$ xterm &
```

xterm 窗口将出现在你的桌面上。如果你按下 Ctrl 键，然后点击并按住鼠标右键，会出现一个弹出字体菜单，如图 8.2 所示。

滚动，然后在期望的字体大小上释放鼠标按钮。xterm 窗口随后会调整大小以使用新的字体大小。

![](img/1ea833f5a3e3c1547e3dd2891f52804a_195_0.png)

**图 8.2** *xterm 客户端的字体可以通过使用弹出菜单即时更改。*

使用命令行选项是强制终端使用特定字体和字体大小的另一种方法。这些命令行选项被称为 X Toolkit 选项，还允许你指定前景和背景颜色以及其他功能，例如窗口标题。例如，要启动带有淡紫色背景和红色文本的 `xterm`，像这样使用 `-bg` 和 `-fg` 选项：

```
$ xterm -fg red -bg Lavender &
```

你也可以指定不同的字体。例如，要启动具有非常大文本的 `xterm`，像这样使用 `-fn` 选项，后跟字体名称：

```
$ xterm -fn 10x20 &
```

按下回车键后，一个极大的终端窗口将出现在你的桌面上！

![](img/1ea833f5a3e3c1547e3dd2891f52804a_195_1.png)

> 颜色名称可以在 `rgb.txt` 文件中找到，可能位于 `/usr/X11R6/lib/X11` 目录下。你还可以在 `/usr/X11R6/lib/X11/fonts/misc` 目录下查找其他字体。

## 键盘问题

当你使用 X 时，你可以重新配置键盘或重新排列按键以适应你的需求。对于 Macintosh 用户来说，弄清楚该使用哪些按键可能会让人困惑，因为许多 X 客户端和应用可能会引用 Alt 键或 Meta 键。阅读你的 *Linux* 发行版的文档以确定当你使用 *Linux* 或 X11 时这些以及其他按键的默认映射方式是至关重要的。

例如，当使用 SuSE PCLinux 和 Apple USB 扩展键盘时，每个 Option 键都标记为 "Alt"。但是，当使用 emacs 编辑器时，按下 Cmd+x 键组合来使用 Meta 键。运行 Linux 的基于 Intel 的 PC 使用 Alt+x 组合。

### 自定义键盘

使用 xmodmap 客户端重新映射你的键盘。这个客户端可以通过命令行和一个名为主目录中的 `.Xmodmap` 文件来交换按键或加载新的键盘布局。`.Xmodmap` 中的条目被称为 *xmodmap 表达式*，用于重新定义按键或其他 X 输入事件，例如鼠标点击。系统范围的默认文件 xmodmap 可以在 `/etc/X11` 下找到，或者在 SuSE PCLinux 的情况下，位于 `/usr/X11R6/lib/X11` 目录下。

你可以使用 xev 客户端或 X 事件客户端检查当前的按键定义。像这样从终端窗口的命令行启动 xev：

```
$ xev
```

按下回车键后，其窗口将出现，如图 8.3 所示。要找到 Mac 键盘 Cmd 键的值，按下该键。按键按下和释放的值将显示在你的终端中。然后你可以使用带有 -pk 选项的 xmodmap 交叉检查此值，像这样：

```
$ xmodmap -pk
61    0xff1b (Escape)
62    0xff1e3 (Control_L)
63    0xff59 (Alt_L)
```

![](img/1ea833f5a3e3c1547e3dd2891f52804a_196_0.png)

64    0xffe1 (Shift_L)
65    0xffe5 (Caps_Lock)
66    0xff7e (Mode_switch)    0xfff20 (Multi_key)
67    0xfff51 (Left)
68    0xfff53 (Right)
69    0xfff54 (Down)
70    0xfff52 (Up)

虽然这里没有显示所有输出，但是返回的值（来自 Apple USB 扩展键盘）对应于 Ctrl 和 Caps Lock 键（值为 62 和 65）。要交换这些按键，你可以在你的 .Xmodmap 文件中输入以下内容：

```
remove Lock = Caps_Lock
remove Control = Control_L
keysym Control_L = Caps_Lock
keysym Caps_Lock = Control_L
add Lock = Caps_Lock
add Control = Control_L
```

然后你可以像这样使用 xmodmap 客户端使更改生效：

```
$ xmodmap .Xmodmap
```

按下回车键后，按键将被交换！

> 另一个方便的客户端是 xkeycaps，它显示你键盘的图形。这个客户端有一个包含超过 100 种键盘的数据库，可用于生成 xmodmap 表达式文件以重新映射整个键盘。

## 指针问题

本节不是关于配置鼠标以用于 Linux，而是关于更改你的指针的视觉表示，以及更改在你的 X 会话期间你的鼠标按钮如何工作。这里提供的信息，特别是关于按钮重新配置的内容，可以为你或你系统中的用户让生活稍微容易一点和有趣一点。

尽管 X 会话期间使用的传统指向设备是三键鼠标，但许多 Apple 计算机只带有单按钮 ADB（Apple Desktop Bus）或 USB（通用串行总线）鼠标或触摸板。各种技巧用于在控制台和 X 中将其他按键（如 F11 和 F12）或按键组合（如 Fn+Ctrl 和 Fn+Option）重新映射到中间和右侧鼠标按钮。例如，如果你有一个单按钮 USB 鼠标，你可以使用以下脚本将中间和右侧鼠标按钮映射到键盘的 F11 和 F12 键：

```sh
#!/bin/sh
echo "1" > /proc/sys/dev/mac_hid/mouse_button_emulation
echo "87" > /proc/sys/dev/mac_hid/mouse_button2_keycode
echo "88" > /proc/sys/dev/mac_hid/mouse_button3_keycode
```

传统的鼠标按钮标记为 1、2 和 3。左侧鼠标按钮（按钮 1）通常用于按下按钮、点击菜单项、选择对象和关闭框。中间按钮（按钮 2）用于在客户端之间粘贴数据，或者在按住时用于滚动滚动条。右侧按钮（按钮 3）用于根显示中的属性菜单或其他信息。

为了演示文本复制和粘贴，首先在某个终端窗口中高亮显示文本，然后在另一个 X 终端窗口中点击中间鼠标按钮。你可以使用这种技术从浏览器复制 URL，将命令粘贴到终端窗口，或在编辑会话之间移动文本。

### 更改指针

X 指针是当你移动显示或桌面的根窗口时的光标表示。它在活动窗口内通常变为“I”或文本编辑光标。如果你是 Mac OS 用户，你很可能熟悉各种指针，例如标准箭头和动画手表。

更改你的 X 会话的根显示指针既有趣又简单。X 指针的名称对应于在 `/usr/X11R6/include/X11` 目录下找到的文件 `cursorfont.h` 中的定义。要更改你的指针，使用带有 `-cursor_name` 选项的 `xsetroot` 客户端，后跟光标名称，像这样：

```sh
# xsetroot -cursor_name gumbi
```

按下回车键后，你的指针将成为一个老朋友。要重置你的光标，使用默认指针的名称，像这样：

```sh
# xsetroot -cursor_name X_cursor
```

使用带有 `-fn` 选项的 `xfd` 客户端，后跟名称，允许你查看可用的光标，像这样：

```sh
# xfd -fn cursor
```

按下回车键后，你将看到对话框中的光标，如图 8.4 所示。

