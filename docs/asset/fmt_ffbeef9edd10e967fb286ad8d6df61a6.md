
如果运气好的话，你不需要使用本章的第一部分。然而，尽管 Linux 的安装程序已经比以前好得多——更自动化、也更准确——但 X Window 偶尔仍会出现问题。大多数情况下，你可以通过重新运行发行版自带的 X Window 配置程序（即在安装期间运行的那个程序）来解决这些问题。但在某些情况下，可能仍需要尝试一种设计用于配置 X Window 的旧程序——或者在极端情况下，尝试手动配置它。

声卡在 Linux 中从未是首要任务，但支持情况正在越来越越来越。如果你的卡兼容这些支持的硬件中的一种，那么配置通常是相当简单的。

# 第 12 章：X Window 与声卡配置

## 重新配置 X Window

如果安装程序无法让 X Window 工作，或者你对它的性能不满意，你就需要重新配置 X Window。事实是，Linux 目前对图形适配器和显示器的组合支持还没有微软的产品那么好。不过，你通常可以让 X Window 在你的电脑上运行得与微软 Windows 一样好——甚至更好。

### 你需要重新配置吗？

输入：

```
startx
```

并按回车键。（注意：在 Caldera 中，输入：`kde`。如果 X Window 清晰出现，没有失真或波浪纹，颜色清晰且图标大小正确，那么你可能不需要重新配置了。为了省去麻烦，请直接跳到本章的第二部分：声卡配置。）

然而，请记住，这种需求最初可能并不明显。例如，你可能在 Windows 95/98 中运行的是 24 bpp，但在 Linux 中运行的是 16 bpp——这意味着色彩饱和度较低。你可能在过一段时间后才会注意到色彩饱和度降低，并想要重新配置。

在 X Window 中，有两个部分需要配置：服务器（server）和桌面（desktop）。配置桌面仅仅意味着配置 X Window 在运行时时的外观和行为。这将在第 3 部分介绍。配置服务器则决定了 X Window 是否能够正常工作，以及如色彩深度和分辨率等最基础的显示问题。

### 半自动重新配置 X Window 的选择

本书中涵盖的所有发行版都允许你重新运行它们自己的、通常是安装程序中的配置程序。这是最好的起点。这些程序通常是最新的，且最容易使用。要在命令行中运行原始配置程序（像既往一样注意大小写），并按回车键。

如果原始配置程序不起作用，所有四个发行版在需要手动编辑之前都有两个额外的配置程序可以尝试。你的选择总结在表 12-1 中。

书的第一部分提供了每个发行版自带安装程序的逐步操作说明。后面是两个额外程序的说明。

#### XF86Setup

`XF86Setup` 早于发行版自带的 X Window 配置程序，但它仍然非常有用——而且它通常会生成短得多的配置文件。它是图形化并支持鼠标的，因此相当容易使用。要运行它，首先收集你在第 1 章中获得的图形适配器和显示器的所有信息，然后输入：

```
XF86Setup
```

并按回车键。程序会询问你是否想要接受现有的 `XF86Config` 文件作为默认值。如果你只想进行微小的调整，那么选择 `y`（是）即可。否则，输入：

```
n
```

并按回车键，再次按回车键。这将带你进入程序的介绍界面。

#### xf86config

这同样早于发行版自带的配置程序，但它没有发行版程序或 `XF86Setup` 那么好用。不过，它有一个巨大的优势：由于它是基于文本的，即使你无法进入图形界面，可以使用它构建 `XF86Config` 文件。要运行它，首先收集你在第 1 章中获得的图形适配器和显示器的信息，然后输入：

```
xf86config
```

并按回车键。

| 表 12-1 | 发行版 | 安装程序 | 额外配置程序 | 额外配置程序 |
|---|---|---|---|---|
| Red Hat | `Xconfig` | `XF86Setup` | `xf86config` |
| Caldera | `lizardx` | `XF86Setup` | `xf86config` |
| TurboLinux | `turboboxcfg` | `XF86Setup` | `xf86config` |
| SuSE | `sax` | `XF86Setup` | `xf86config` |

## 第 2 部分：底层：命令行下的 Linux

### 手动配置 X Window

一个文件配置服务器：`XF86Config`。它通常位于 `/etc` 或 `/etc/X11`。图 12-1 是该文件的示例，针对 Toshiba Tecra 笔记本进行了优化。

![](img/2ca18b573042c4f829639d11e82e_171_0.png)

```
#### XF86Config 由 XF86Setup 自动生成
# Copyright: (1996) The XFree Project, Inc.
#### 关于此文件的信息请见 man XF86Config

Section "Files"
FontPath "/usr/X11R6/lib/X11/rgb"
FontPath "/usr/X11R6/lib/X11/fonts/local"
FontPath "/usr/X11R6/lib/X11/fonts/misc:unscaled"
FontPath "/usr/X11R6/lib/X11/fonts/75dpi:unscaled"
FontPath "/usr/X11R6/lib/X11/fonts/100dpi:unscaled"
FontPath "/usr/X11R6/lib/X11/fonts/dpi"
FontPath "/usr/X11R6/lib/X11/fonts/speed"
FontPath "/usr/X11R6/lib/X11/fonts/misc"
FontPath "/usr/X11R6/lib/X11/fonts/75dpi"
FontPath "/usr/X11R6/lib/X11/fonts/100dpi"
FontPath "unix:-"
Section

Section "ServerFlags"
Section

Section "Keyboard"
Protocol "Standard"
XkbRules "xfree86"
XkbModel "pc105"
XkbLayout "us"
XkbOptions "ctrl:"
Section

Section "Pointer"
Protocol "PS/2"
Device "/dev/mouse"
Section
```

### 图 12-1 XF86Config 文件示例（续）

| Section "Monitor" | "Primary Monitor" |
|---|---|
| Identifier | "Unknown" |
| VendorName | "Unknown" |
| HorizSync | +68 |
| VertRefresh | +87 |
| Mode line | "800x600" |
| +hync +vsync | |
| Modeline | "640x480" |
| -vsync -vsync | |
| EndSection |
| Section "Device" | "Primary Card" |
|---|---|
| Identifier | "Unknown" |
| VendorName | "None" |
| BoardName | "ct6550" |
| Chipset | |
| Option | "no_bitblt" |
| EndSection |
| Section "Screen" | "SVGA" |
|---|---|
| Driver | |
| Device | "Primary Card" |
| Monitor | "Primary Monitor" |
| DefaultDepth | 16 |
| SubSection "Display" | |
| Depth | 8 |
| Modes | "800x600" "640x480" |
| EndSection |
| SubSection "Display" | |
| Depth | 16 |
| Modes | "800x600" "640x480" |
| EndSection |
| SubSection "Display" | |
| Depth | 24 |
| Modes | "800x600" "640x480" |
| EndSection |

编辑这个文件虽然对大多数人来说并不是什么乐趣，但并不像看起来那么痛苦。该文件被分成了易于理解的部分。

通常的部分有：

- Files（字体文件路径）
- Keyboard（键盘配置）
- Pointer（指针配置）
- Monitor（显示器描述和规格）
- Device（定义你的图形适配器）
- Screen（指定要一起使用哪些图形适配器和哪些显示器，以及使用何种配置）

## 2：底层：命令行下的 Linux
