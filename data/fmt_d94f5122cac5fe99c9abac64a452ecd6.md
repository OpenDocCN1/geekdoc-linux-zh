
这些值告诉 `xpaint` 客户端绘制一个垂直工具箱。如果你想要水平工具箱，可以调整工具箱的大小，记录窗口管理器在调整操作期间显示的尺寸，并使用新设置更改其默认资源设置文件中工具箱的初始大小，例如：

- 顶层操作/工具箱操作
- `Xpaint.width`: 782
- `Xpaint.height`: 122

关于 X 资源的详情，请参阅 X 帮助页。关于不同客户端资源的详情，请参阅程序的帮助页或其他文档。

> 注意：确保你的更改符合所支持的屏幕尺寸，否则程序可能会在屏幕外启动，或者窗口太大而无法使用。始终使用感叹号 `!` 作为注释，如果你编辑默认的原始应用程序资源文件，请先将原始设置复制到注释行。

### 更改 X11 鼠标和光标模式

使用 X11 时，你可能更改鼠标的工作方式或切换鼠标键的顺序。如果你是左手用户，或者鼠标的响应与预期设置不符，这会特别方便。你还可以更改窗口管理器使用的光标类型。

为了更改根窗口光标，你需要知道有哪些可用的光标。你可以在 `/usr/X11/include/X11` 目录下的 `cursorsfont.h` 文件中找到光标列表，例如：

```
#define XC_exchange 50
#define XC_fleur 52
#define XC_gobbler 54
#define XC_gumbby 56
#define XC_hand1 58
#define XC_hand2 60
#define XC_heart 62
#define XC_icon 64
```

此外，该文件中还列出了许多类型的光标。了解这些不同类型的光标后，你可以使用 `xroot` 客户端（即根窗口实用程序）来设置根光标图像，例如：

```
# xsetroot -cursor_name hand1
```

这将根光标改为指向右手的手。如果你是左手用户，你可能想使用指向左手的 `hand2` 光标！

省时技巧

查看所有光标的一种简单方法是使用位于 `/usr/X11R/bin` 目录下的 `xfd`（即 X11 字体显示）客户端。配合 `-fn` 命令行选项使用，`xfd` 客户端将显示位于 `/usr/X11R/` 的光标字体的完整字符集。

`xwd` 程序易于使用。你可能需要在命令行中指定一个文件，因为如果你不这样做，该文件将发送到标准输出，并会刷屏你的终端窗口。

```
# xwd > mydump.xwd
```

输入此命令后，你的光标将变成一个十字准 (+)。如果你点击根桌面，`xwd` 客户端将转储（或捕获）你整个屏幕的图片。如果你点击一个窗口，`xwd` 客户端将捕捉该窗口的内容，即使它被隐藏或被另一个窗口遮挡。

如果你想捕捉运行中的客户端的一系列图片、展示游戏得分或创建快速幻灯片，这就会非常有用。该文件格式为 X11 窗口转储格式，但你会发现许多可以用来查看图像的客户端。其中一个是 `xwd` (X11 window dump) 客户端，用于查看你的截图：

```
# xwd -in mydump.xwd
```

你还可以使用位于 `/usr/X11R/bin` 目录下的 `xloadimage` 客户端为你的图像创建幻灯片。如果你创建了一系列屏幕转储，可以使用以下命令构建循环的截图幻灯片：

```
# xloadimage -fit 1.xwd 2.xwd 3.xwd -goto 1.xwd
```

使用此命令行，你可以通过按下键盘上的 N 字符反复翻页转储文件，或者按下 Q 字符退出。`xloadimage` 客户端具有许多功能，还可以将你的屏幕转储保存为不同的图形文件格式。更多信息请参见 `xloadimage` 手页。

| 几分钟 | 你的 CD-ROM 上还包含许多其他图形实用程序。参见第 16 小时关于绘图和绘制程序、图形转换工具和其他图像查看器（例如 `xv` 客户端，它不仅可以捕捉截图，还能编辑、转换、保存和打印图形）的概述。 |

### 自定义 X11 根窗口和使用屏

如果你有一台彩色显示器，你可能想要更改根或桌面窗口的默认颜色或图案。你可以通过几个 X11 客户端快速方便地实现。我还将向你展示如何将图片放入背景中，以及如何在 X11 中设置和使用屏幕保护程序。

#### 使用 X 系统

##### 设置背景颜色

你可以使用位于 `/usr/X11R/bin` 目录下的 `xsetroot` 或根窗口工具来更改显示器的背景颜色。正如我之前提到的，你对颜色的选择取决于你的 X11 服务器的颜色深度。如果你正在使用 SVGA 服务器，你将 256 种颜色可选。例如，可以通过以下命令更改颜色：

```
# xsetroot -solid red
```

##### 设置背景图案

如果纯色对眼睛太刺，或者对于你的口味来说太单调，你还可以使用来自 `/usr/include/X11/bitmaps` 目录的近 90 种不同的位图图形文件来设置桌面图案。例如，为桌面设置红色的篮织图案：

```
# xsetroot -bitmap /usr/include/X11/bitmaps/wide_weave -bg red
```

此命令告诉 `xsetroot` 客户端从 X11 位图图形目录加载位图图形文件 `weave`，并用背景颜色显示该图案。

> 尝试不同的颜色和图案。当你找到喜欢的时，请在 `.xinitrc` 文件中使用 `xsetroot` 命令行，这样下次你运行 X11 会话时，背景就会被设置好。

省时利器

如果你运行的是单色显示器，那么颜色方面你就没戏了。但你可以使用不同的位图文件更改背景的图案和外观。尝试 `simple1`、`dimple3` 或 `flipped_gray` 位图文件。

### 在根显示上显示图片

许多用户喜欢在根窗口中显示一张喜欢的图片。如果你有一张扫描过的喜欢的照片或像这样的图形，你可以使用 `xsetroot` 客户端在桌面上显示你的图像，但图像必须是 X11 位图格式。

你可以使用已经讨论过的客户端——`xloadimage`。例如，你可以通过 `-supported` 命令行查看 `xloadimage` 客户端识别哪些图形文件：

```
# xloadimage -supported
```

| 类型 | 名称 | 是否可转储 | 描述 |
| :--- | :--- | :--- | :--- |
| niff | 是 | 原生图像文件格式 (NIFF) |  |
| sunraster | 否 | Sun Masterfile |  |
| gif | 否 | GIF 图像 |  |
| jpeg | 是 | JFIF 风格的 JPEG 图像 |  |
| fbm | 否 | FBM 图像 |  |
| cmuraster | 否 | CMU Raster |  |
| pbm | 是 | 便携位图 (PBM, PGM, PPM) |  |
| Faces | 否 | Faces 项目 |  |
| rle | 否 | Utah RLE 图像 |  |
| xwd | 否 | X Window Dump |  |
| vff | 否 | Sun 可视文件格式 |  |
| mcdidas | 否 | MCIDAS |  |
| vica | 否 | VICAR |  |
| pcx | 否 | PCX |  |
| gem | 否 | GEM |  |
| macpaint | 否 | MacPaint |  |
| xpm | 否 | XPM |  |
| xbm | 否 | XBM |  |

### 第 7 小时

#### 使用 X 系统

你可以使用位于 `/usr/X11R/bin` 目录下的 `xsetroot` 或根窗口工具来更改显示器的背景颜色。正如我之前提到的，你对颜色的选择取决于你的 X11 服务器的颜色深度。如果你正在使用 SVGA 服务器，你将 256 种颜色可选。例如，可以通过以下命令更改颜色：

```
# xsetroot -solid red
```

##### 设置背景图案

如果纯色对眼睛太刺，或者对于你的口味来说太单调，你还可以使用来自 `/usr/include/X11/bitmaps` 目录的近 90 种不同的位图图形文件来设置桌面图案。例如，为桌面设置红色的篮织图案：

```
# xsetroot -bitmap /usr/include/X11/bitmaps/wide_weave -bg red
```

此命令告诉 `xsetroot` 客户端从 X11 位图图形目录加载位图图形文件 `weave`，并用背景颜色显示该图案。

> 尝试不同的颜色和图案。当你找到喜欢的时，请在 `.xinitrc` 文件中使用 `xsetroot` 命令行，这样下次你运行 X11 会话时，背景就会被设置好。省时利器

如果你运行的是单色显示器，那么颜色方面你就没戏了。但你可以使用不同的位图文件更改背景的图案和外观。尝试 `simple1`、`dimple3` 或 `flipped_gray` 位图文件。

### 在根显示上显示图片

许多用户喜欢在根窗口中显示一张喜欢的图片。如果你有一张扫描过的喜欢的照片或像这样的图形，你可以使用 `xsetroot` 客户端在桌面上显示你的图像，但图像必须是 X11 位图格式。

你可以使用已经讨论过的客户端——`xloadimage`。例如，你可以通过 `-supported` 命令行查看 `xloadimage` 客户端识别哪些图形文件：

```
# xloadimage -supported
```

| 类型 | 名称 | 是否可转储 | 描述 |
| :--- | :--- | :--- | :--- |
| niff | 是 | 原生图像文件格式 (NIFF) |  |
| sunraster | 否 | Sun Masterfile |  |
| gif | 否 | GIF 图像 |  |
| jpeg | 是 | JFIF 风格的 JPEG 图像 |  |
| fbm | 否 | FBM 图像 |  |
| cmuraster | 否 | CMU Raster |  |
| pbm | 是 | 便携位图 (PBM, PGM, PPM) |  |
| Faces | 否 | Faces 项目 |  |
| rle | 否 | Utah RLE 图像 |  |
| xwd | 否 | X Window Dump |  |
| vff | 否 | Sun 可视文件格式 |  |
| mcdidas | 否 | MCIDAS |  |
| vica | 否 | VICAR |  |
| pcx | 否 | PCX |  |
| gem | 否 | GEM |  |
| macpaint | 否 | MacPaint |  |
| xpm | 否 | XPM |  |
| xbm | 否 | XBM |  |

### 屏保护设置与程序

`xscreensaver` 客户端带有近二十种屏保护程序，这些程序也可以作为独立程序运行。例如，你可以在窗口中运行分形绘制 `hopalong`：

```
# hopalong
```

将在窗口中运行屏保护程序，让你看到它的样子。关于适用于 `xscreensaver` 客户端的屏保护程序列表，请阅读 `/usr/X11R6/lib/X11/app-defaults` 目录下的 `XScreenSaver` 文件。你可以在该文件中找到其他设置，它是该客户端的 X11 资源文件。

`xscreensaver` 和 `xscreensaver-command` 客户端由 Jamie Zawinski 开发，位于 `/usr/X11R/bin` 目录。`xscreensaver` 客户端有 16 个命令行选项。虽然本小时没有涵盖所有选项，但使用此屏保护的基本方法是首先以后所示后台运行 `xscreensaver` 客户端：

```
# xscreensaver -timeout 5
```

此命令将屏保护设置为在键盘或鼠标活动五分钟后运行。你可以使用 `xscreensaver-command` 客户端控制此客户端，开启或关闭屏保护，立即激活它。虽然 `xscreensaver` 客户端有一个 `-lock` 选项可以保护你的显示器，但你需要重新编译程序来启用此功能。

### 探索 X11 程序

你可能还会对 `xlock` 客户端感兴趣。虽然它不是屏保程序，但 `xlock` 是一个复杂的终端锁定程序，具有近 50 个命令行选项和 50 多种内置显示模式。如果你想对显示进行密码保护，以防止在你离开时他人使用你的电脑，`xlock` 客户端将非常有帮助。

默认情况下，在你启动 `xlock` 程序后，你必须输入密码才能再次使用显示。但你也可以将其作为一个无需密码保护的简单屏保程序来显示各种动画，例如：

```bash
# xlock -duration 10 -nolock -mode random
```

此命令告诉 `xlock` 程序显示其随机选择的动画，每个动画将运行 10 秒。

![](img/91f0fe61bd3027cda34d2f54533df676_143_0.png)

> 如果你使用 `-inroot` 命令行选项，`xlock` 客户端还可以让你的桌面变成动画显示器。这不会保护你的系统，但你可能会发现这种视觉效果很刺激！

### 仅几分钟

这一小时没有足够的空间讨论你 CD-ROM 上所有的 X11 客户端。你将在本书的其余部分找到不同客户端的讨论，但本节展示了一些实用的程序，它们将为你提供有关系统的更多信息，以及如何使用它们的一些技巧。

### 使用 x11fonts 列出 X11 字体

如果你想列出系统中 X11 识别的所有字体列表，可以使用 `x11fonts` 客户端。如果你使用通配符或模式匹配名称调用客户端，你可能需要多或少地使用分页器（在第 4 小时“阅读和导航命令”中讨论过）。这对于寻找系统上的特定字体非常方便，例如：

```bash
# x11fonts -fn *italic*
lucidans-bolditalic-10
lucidans-bolditalic-10
lucidans-bolditalic-12
lucidans-bolditalic-14
lucidans-bolditalic-16
lucidans-bolditalic-18
lucidans-bolditalic-20
lucidans-bolditalic-24
```

![](img/91f0fe61bd3027cda34d2f54533df676_143_1.png)

## 使用窗口 系统

`lucidansans-bolditalic-8`

`lucidansans-bolditalic-8`

`lucidansans-italic-10`

`lucidansans-italic-10`

`lucidansans-italic-12`

`lucidansans-italic-12`

`lucidansans-italic-14`

`lucidansans-italic-14`

`lucidansans-italic-18`

`lucidansans-italic-18`

`lucidansans-italic-24`

`lucidansans-italic-24`

`lucidansans-italic-8`

`lucidansans-italic-8`

如你所示，这列出了你的 X11 服务器安装或识别的所有斜体字体。你可以使用 `xfonts` 客户端来排查字体是否被识别，或者在启动客户端时寻找一个名称作为 X Toolkit 选项。

### 使用 xwininfo 客户端获取窗口信息

你可以使用 `xwininfo` 客户端（或窗口信息实用程序）获取有关窗口的有用信息。当你使用此命令时，可以点击另一个窗口以获取详细信息列表，例如：

```bash
# xwininfo
xwininfo: Please select the window about you would like information by by clicking the mouse in that window.
```

点击所需的窗口后，你将看到一个信息列表，如下：

```
xwininfo: Window id: 0xc0002 "rxvt"

Absolute upper-left X: 8
Absolute upper-left Y: 397
Relative upper-left X: 0
Relative upper-left Y: 0
Width: 574
Height: 158
Depth: 8
Visual Class: PseudoColor
Border width: 0
Class: InputOutput
Colormap: 0x21 (Installed)
Bit Gravity State: ForgetGravity
Window Gravity State: NorthWestGravity
Backing Store State: NotUseful
Save State: no
Map State: IsViewable
Override Redirect State: no
Corners: +397 -218+397 -218-45 +8-45
-geometry 0x11+3-40
```

![](img/91f0fe61bd3027cda34d2f54533df676_144_0.png)

## 第 7 小时

这些信息可能有用，例如，如果你想在下次运行程序时获取窗口几何设置的规格，或者如果你想通过编辑资源文件来更改窗口的默认行为。

### 使用 xmmessage 客户端制作便签日历

由 Chris Peterson 和 Stephen Gilda 开发的 `xmmessage` 客户端是在工作时创建快速笔记作为提醒的方便方法。这个看起来非常简单的客户端非常易使用。例如，如果你想对一个电话号码做个快速笔记：

```bash
# xmmessage "George called at 10:15; call him back at 555-1212"
```

此命令行将显示带有你的消息内容的 `xmmessage` 客户端窗口。虽然这是一个简单的例子，但你还可以使用 `xmmessage` 客户端显示程序搜索结果，或者在你的个人日程中使用它在你工作时自动发送提醒（详情请参阅第 18 小时“个人生产力工具”或第 24 小时“调度”）。

如果你需要在屏幕上复制一份当前日历，或者如果你在启动 X 会话时在桌面上有一个日历，你也可以将 `xmmessage` 作为日历显示程序。你找不到简单的 X11 版本的 `cal` 日历程序，但有一个你可以使用的：

```bash
# cal | xmmessage -file ".-" &
```

这将在正框中显示 `cal` 日历程序的输出。
