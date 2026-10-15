
```
# rmv -h
safe file delete v1.0
rmv -d[delete]-e[empty] -h[elp] -l[ist] file-4
```

这会打印一条短消息，因为脚本在命令行上发现了字母 `h`，然后使用 `echo` 命令打印了该消息。要删除文件，必须使用 `-d` 或 `delete` 命令行选项：

```
# rmv -d graf.gif graf.pnm graf.tif
deleting:graf.gif graf.pnm graf.tif
rmv finished.
```

这通过将文件移动到你家目录下的 `.trash` 目录删除了四个文件。`d` 选项在命令行上执行，脚本随后打印了消息，将文件名回显到显示器，并将 `delete` 变量设置为 `true`。由于 `delete` 变量被改为 `true`，`if ...` 语句中找到 `rmv` 命令被执行。

你可以使用 `-l` 或 `list` 选项查看垃圾桶的内容，以验证文件已移动：

```
# rmv -l
your trash contains:
total 278
-rw-rw-r-- 1 ... graf.gif
-rw-rw-r-- 1 ... graf.pnm
-rw-rw-r-- 1 ... graf.tif
```

*(注：由于示例代码输出不完整，此处根据逻辑推断翻译并保持格式)*

# 使用 X Window 系统

## 设置窗口的外观

启动时要执行的任务，例如设置桌面的背景颜色，以及加载哪些模块

菜单定义，以便你可以自定义程序列表以匹配你的系统（默认菜单中定义的某些程序可能未安装在你的系统上）

你的鼠标按钮的默认操作或桌面上的菜单，或者你可以定义功能键实用程序

**图 7.1.** Linux 下用于 X11 的 fwm 窗口管理器提供了装饰性的窗口边框和控制。

![](img/91f0fe61bd3027cda34d2f54533df676_126_0.png)

如果你觉得 fwm2 窗口管理器很复杂，你可能还想尝试 AnotherLevel，它是对 fwm2 配置文件的高级定制版本。

# 配置 AnotherLevel

AnotherLevel 是 fwm2 窗口管理器的一个复杂变体，基于 Greg J. Badros 的 TheNextLevel 开发，而后者使用 fwm2 窗口管理器配置作为 Red Hat Linux 的默认 X11 桌面。你将发现一个近乎完全的菜单系统，并且可以自定义窗口外观的几乎任何方面，或者窗口管理器处理键盘和鼠标的方式。

图 7.2 显示了 AnotherLevel 窗口管理器。

![](img/91f0fe61bd3027cda34d2f54533df676_126_1.png)

# 图 7.2. fwm2AnotherLevel 窗口管理器带有一组你可以用于定制其窗口系统文件。

![](img/91f0fe61bd3027cda34d2f54533df676_127_0.png)

与 fvwm 不同，fwm2 的 AnotherLevel 有多个配置文件，位于 `/etc/X11/` 目录下。这些文件包括

- # Is A - /etc/X11/

- decors fwm2rc.forms fwm2rc.m4 fwm2rc.xlink

- fwm2rc.apps fwm2rc.functions fwm2rc.macros

- fwm2rc.decors fwm2rc.hostmenus fwm2rc.menus

- fwm2rc.defines fwm2rc.init fwm2rc.modules

- fwm2rc.defyles fwm2rc.keys fwm2rc.mouse scripts

如果你是 root 操作员，可以修改这些文件以定制此窗口管理器为所有用户的工作方式。这些文件包含许多你可以更改的不同定义，包括：

- 菜单栏和菜单项的颜色选项

- 启用声音的选项

- 菜单中使用图标或颜色的软件切换器和开关

- 自定义的鼠标和窗口操作，例如焦点（窗口是通过鼠标点击还是光标位置变为激活的）

- 虚拟桌面数量的定义

- 对 Windows 95 键盘的支持

- 可拆卸菜单的选项

# 使用 X Window 系统

为了自定义窗口管理器菜单中支持的应用程序，你需要使用 `wmconfig` 程序，它位于 `/usr/X1186/bin` 目录下。该程序根据 `/etc/X11/wmconfig` 目录下的定义文件构建窗口管理器配置文件。你可以使用此程序为多个窗口管理器构建配置文件。

首先，在你的主目录下创建一个名为 `.wmconfig` 的目录。将 `/etc/X11/wmconfig` 目录下的文件复制到你的 `.wmconfig` 目录，例如：

```
# mkdir .wmconfig
# cp /etc/X11/wmconfig/* .wmconfig
```

然后你可以通过创建、编辑或删除配置文件来添加、删除或更改菜单中的应用程序。有关这些文件格式的详细信息，请参阅 wmconfig 手页。当你完成应用程序和菜单的自定义后，可以使用 `wmconfig` 命令创建一个新的配置文件，例如：

```bash
# wmconfig --output=fwm2 --sysdir=home/dball/.wmconfig > fwm2rc
```

此命令将导致 `wmconfig` 程序解析 `.wmconfig` 目录下的配置文件，并将输出放在新的 `.fwm2rc` 文件中。

如果你喜欢将任务栏放在屏幕底部（请参见“屏幕空间”），并且不想在工作时让任务栏挡挡路，可以通过更改 `fwm2rc.modules` 文件中的设置让它自动隐藏。寻找处理任务栏的章节，例如：

```bash
############################################################
###### FwmTaskBar
###### FwmTaskBarAutoHide
```

在添加自动隐藏设置后，重启窗口管理器。当你不需要任务栏时，它会消失；当你的光标位于屏幕底部时，它会显示。

你也可以从 `fwm2rc.init` 文件中启动程序。虽然你可以通过将程序添加到 `.xinitrc` 来启动程序，但如果你希望“窗口具有特殊功能，例如可见的最小化、最大化或关闭按钮”，那么将它们添加到 `fwm2rc.init` 文件是非常重要的。寻找 `SetupFunction` 部分，然后按照所示添加你想在启动时运行的程序：

```bash
# # Setupfunction gets run at Init Restart

AddToFunc "SetupFunction"
+ "I" Exec xset -solid cyan4
+ "I" Exec rxvt -geometry 80x11+3-375 -bg white -fg black
+ "I" Exec rxvt -geometry 80x24+6 -2 -bg white -fg black
```

![](img/91f0fe61bd3027cda34d2f54533df676_128_0.png)

这些行不仅设置了桌面颜色，还在屏幕上的特定位置打开了两个终端窗口。窗口将具有你启用的任何特殊按钮或光标装饰。你还可以更改窗口对鼠标光标的反应。虽然你通常通过点击窗口或其标题栏使窗口激活，但你可以通过删除注释字符来更改此设置：

```bash
# If defined, the focus follows the pointer. Otherwise focus is set by
# clicking on a window. Undefined "ClickToFocus"
#define("FOCUS_FOLLOWS_POINTER")
```

当光标移动到它时，你可以通过在 `fwm2rc` 文件中取消注释字符来更改此设置，例如：

```bash
# Uncomment below Win95
#define("Keys")
```

在你删除注释字符并重启窗口管理器后，你可以使用 Windows 键弹出任务栏。如果你想了解更多信息，请查看 `/usr/doc` 目录。

# 配置 fwm 窗口管理器

fwm 或虚拟桌面管理器位于 `/usr/X11/` 目录，是 twm 的后代。fwm 程序由 Robert 提供了：

- 支持虚拟桌面

- 消耗内存

- 提供三维外观

- 引入支持声音、分页器、图标等等模块

你会在 fwm 窗口管理器的配置文件 `/etc/X11/system.fwmrc` 中找到它。如果你是 root 操作员，可以修改此文件为所有用户定制功能和程序。如果你想制作自己的 fwm 功能，可以将此文件复制为 `.fwmrc` 并保存到你的主目录下。

图 7.3 显示了 fwm 窗口管理器如何设置和自定义此窗口管理器，

如果你想获得更多关于如何设置和自定义窗口管理器的信息，请查看 fwm 手页以及每个模块的手页。

# 使用 X Window 系统

# 图 7.3. fwm 窗口管理器带有虚拟桌面、图标固定以及装饰性的窗口边框和控制。

![](img/91f0fe61bd3027cda34d2f54533df676_130_0.png)

版权 1998-1999. FWM 是华盛顿大学的一个框架。

![](img/91f0fe61bd3027cda34d2f54533df676_130_1.png)

# 配置 twm 窗口管理器

twm 或标签窗口管理器位于 `/usr/X11R/bin` 目录，是 X 系统的原始窗口管理器之一。twm 程序由 Tom LaStrange 和其他作者开发，提供了最基本的窗口操作，例如标题、图标、根窗口菜单以及其他自定义鼠标或键盘命令。图 7.4 显示了 twm 窗口管理器。

# 图 7.4. twm 或标签窗口管理器提供了带有程序列表、图标和窗口控制的基本 X11 显示。

![](img/91f0fe61bd3027cda34d2f54533df676_130_2.png)

你可以在 `/etc/X11/twm` 目录下找到 twm 窗口管理器的配置文件 `system.tmrc`。如果你是 root 操作员，可以自定义此文件以为所有用户支持你的系统功能。如果你想创建自定义的 twm 特性，可以将此文件复制并命名为 `.tmrc` 保存到你的家目录下。

## X11 终端程序

X11 终端客户端为你提供了一个可以通过命令行访问 shell 的控制台。虽然你不需要一直使用终端程序，但在 X11 会话期间，你可能至少会打开一个终端窗口，以便启动其他程序。同时打开多个窗口是学习新命令的方便方法，因为你可以在一个窗口中显示帮助页，同时在另一个窗口中尝试运行该程序。你还可以使用多个终端来复制和粘贴信息。

这里向你介绍两种你会在 X11 中想要使用的终端程序：`xterm`（或者一个支持色彩版本的 `nxterm`）以及 `rxvt` 终端。你将学习如何使用这些程序以及它们的一些命令行选项。

## 修改 nxterm 终端设置

nxterm 客户端（或终端模拟器）是 `xterm` 客户端支持色彩的版本。由于这些客户端除了颜色外基本相同，我将在终端窗口的语境下讨论这些特性。

nxterm 终端模拟器会显示一个带有命令行的打开窗口。你可以运行程序、进行文字处理，或执行几乎你平时在没有运行 X11 时会执行的任何功能。与大多数 X11 终端模拟器一样，nxterm 客户端具有一个运行 shell 的可缩放窗口。窗口左角的按钮允许你移动、调整大小、最小化或最大化窗口，还可以关闭或杀死窗口以及从窗口启动的任何运行程序。

右上角的按钮也允许最大化或最小化窗口。如果你最小化了一个窗口，图标可能会出现在桌面上，或者放在图标任务栏中，这取决于你当前使用的窗口管理器。通过将鼠标指针移动到窗口的任何角并按住左鼠标键，你可以调整窗口大小。

你可以通过各种命令行选项告诉 nxterm 初始如何以及在何处显示窗口。其中某些选项（X11 Toolkit 选项）将在本小时稍晚后的“学习 X11 基础操作”章节中讨论。你在其他终端模拟器中无法发现的一个特性是：nxterm 可以使用 Ctrl 键和鼠标按键动态更改特性。

![](img/91f0fe61bd3027cda34d2f54533df676_131_0.png)

## 使用 X 窗口系统

例如，如果你想终端使用更大或更小的字体，只需将光标移动到终端窗口内，按住 Ctrl 键并点击右键。会弹出一个名为 VT Fonts 的菜单，其中有一个尺寸列表，你可以从中选择更小的尺寸。

![](img/91f0fe61bd3027cda34d2f54533df676_132_0.png)

nxterm VT Fonts 的一个非常棒的特性是 Selection 选项。它的工作原理如下：首先，运行 nxterm 客户端，然后从命令行启动客户端。nxterm 客户端显示许多变种字体，你可以看到不同字号或方向对所选字体的影响。如果你为显示器找到了一个极易读的字体，点击 nxterm 窗口顶部的 Select 按钮，将指针移动到 nxterm 窗口，按住 Ctrl 键，点击右键，并选择 VT Fonts 菜单项中的 Selection。完成！你的窗口现在将使用你通过 xterm 客户端选择的字体。这对于为终端寻找最佳字体非常有用。

你终端窗口的许多功能取决于你选择的窗口管理器。虽然几乎所有的终端都支持滚动，但并不是所有的模拟器都有绘制精美的滚动条。你可以按住 Ctrl 键并点击鼠标中键来控制是否启用滚动以及滚动条是否可见（对于双键鼠标用户，请确保已启用三键模拟，并同时按下两个鼠标键）。你会发现通过这个方便的菜单设施可以动态更改许多其他特性。

nxterm 或 xterm 模拟器还有许多功能，包括显示 Tektron 图形的能力。但如果你不需要所有这些特性，或者需要更多内存来运行程序，你可能想要使用接下来要讨论的 rxvt 终端模拟器。

## 使用内存高效的 rxvt 终端

rxvt 客户端（或终端模拟器）是一个支持色彩的 X11 控制窗口，与 nxterm 或 xterm 客户端相比，它的特性更可能更实用：

- 更小，因此使用更少的内存或交换空间

- 支持色彩的终端模拟器

- 支持 X Toolkit 命令行选项

- 没有 Tektronix 4014 仿真，这对于独立的 Linux X11 工作站并不是真正需要的

![](img/91f0fe61bd3027cda34d2f54533df676_132_1.png)

在 X 下运行通常从非图形环境运行的程序，例如：

```
rxvt -e
```

rxvt 客户端（或终端模拟器）是一个支持色彩的 X11 控制窗口，具有更多可能更实用的特性。如果你想创建自定义的 twm 特性，可以将此文件复制并命名为 `.tmrc` 保存到你的家目录下。右上角的按钮也允许最大化或最小化窗口。如果你最小化了一个窗口，图标可能会出现在桌面上，或者放在图标任务栏中，这取决于你当前使用的窗口管理器。通过将鼠标指针移动到窗口的任何角并按住左鼠标键，你可以调整窗口大小。你可以通过各种命令行选项告诉 nxterm 初始如何以及在何处显示窗口。其中某些选项（X11 Toolkit 选项）将在本小时稍晚后的“学习 X11 基础操作”章节中讨论。你在其他终端模拟器中无法发现的一个特性是：nxterm 可以使用 Ctrl 键和鼠标按键动态更改特性。

nxterm 终端模拟器显示一个带有命令行的打开窗口。你可以运行程序、进行文字处理，或执行你平时在没有运行 X11 时会执行的任何功能。与大多数 X11 终端模拟器一样，nxterm 客户端具有一个运行 shell 的可缩放窗口。窗口左角的按钮允许你移动、调整大小、最小化或最大化窗口，还可以关闭或杀死窗口以及从窗口启动的任何运行程序。

## 设置 X11 客户端资源

其他颜色选项包括用于窗口框颜色的 `-bd`，以及 `-rv` 和 `+rv` 反转模式显示，这些对于单色显示非常有用。

X 窗口系统还通过使用客户端资源支持进一步的客户端配置。这些资源本质上是文本文件，包含了关于客户端外观或运行各个方面的设置。你也可能在客户端程序启动时使用 `-xr` 命令行选项指定资源字符串，来设置程序的不同资源，但大多数程序只会使用资源文件。

为了更改资源设置，你需要知道 X11 客户端使用了哪些资源。你可以通过阅读程序的帮助页，或者在 `/usr/X11/lib/X11` 目录下的 `app-defaults` 目录中查找与客户端同名的文件（但并非总是如此）来获取这些信息：

```
# # ls -a /usr/X11/lib/X11/app-defaults
Beforelight RVt* XGetfile Xpc
Bitmap Seyon Xidle XScreenSaver Xpper
Bitmap-color Seyon-color Load Xsp Xpper-color
Chooser Vickers Xlock Xsysinfo Xman
Editres Xanner Xlogo-color XTerm Xman
Editres-color X3278 Xlogo Xterm-color Xmessage
Fig Xc Mailbox Xditview
Fig-color Xcalic-color XDM Xditview-chhtrt Xvidtune
GV GXditview XClock Mixer Xedit xview
NXTerm XConsole Ghostpoint XPaint Fpm
```

你可以有很多带有应用程序默认设置的文件，但 X11 的超过 200 个程序并非全部都安装了设置。每个文件都包含针对特定 X11 客户端的资源字符串。这些资源字符串不仅提供了决定程序如何显示的信息，还包含了菜单、按钮或程序其他部分的内容和处理方式。

资源字符串的格式在 X 帮助页中有定义，但许多 X11 客户端程序会为特定客户端列出不同的资源及其示例。如果你查看 xpoint 绘图程序 man 工具箱的资源设置，你会看到以下值：

- 顶层操作/工具栏菜单

- Xpoint.width: 232

- Xpoint.height: 350

## 使用 X 窗口系统
