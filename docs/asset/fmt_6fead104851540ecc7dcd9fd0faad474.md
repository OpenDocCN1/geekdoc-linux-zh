
多年来，各种程序一直尝试自动化复杂的 XF86Config 文件创建。然而，到目前为止，这些程序对我们来说都惨遭失败了——直到最近的版本以及一个名为 `xf86config` 的程序出现。第一次，`xf86config` 似乎能够创建一个可运行的 XF86Config 文件，而且我们甚至没有任何特殊的硬件。

在运行 `xf86config` 之前，请仔细阅读以下每个章节，这些章节描述了 `xf86config` 程序将填充的 XF86Config 文件的各个部分。通过深入了解 XF86Config 文件，你使用 `xf86config` 的成功率将会大大。

因此，我们将讨论这六个部分，然后介绍如何使用 `xf86config`。

## 在配置文件中设置路径

`Files` 部分是 XF86Config 文件中最容易设置的部分。这是因为几乎每个人的路径都是相同的。在 `Files` 部分中，你需要告诉 X RGB（红-绿-蓝）颜色数据库文件所在的位置以及字体所在的位置。由于它们都应该位于标准位置，你只需在 XF86Config 文件中使用以下部分即可（事实上，示例版本已经是这样配置的）：

```
Section "Files"
RgbPath      "/usr/X11R6/lib/X11/rgb"
FontPath      "/usr/X11R6/lib/X11/fonts/misc/"
FontPath      "/usr/X11R6/lib/X11/fonts/Type1/"
FontPath      "/usr/X11R6/lib/X11/fonts/Speedo/"
FontPath      "/usr/X11R6/lib/X11/fonts/75dpi/"
FontPath      "/usr/X11R6/lib/X11/fonts/100dpi/"
EndSection
```

这个 `Files` 部分告诉 XFree86 你的 RGB 数据库位于 `/usr/X11R6/lib/X11/`，字体位于 `/usr/X11R6/lib/X11/fonts/`。这些都是两者的标准位置。需要注意的一点是，你可能没有加载所有的字体目录（尽管我们建议你这样做）。因此，你应该检查 `/usr/X11R6/lib/X11/fonts/`：

```
$ ls /usr/X11R6/lib/X11/fonts/
100dpi/ 75dpi/ PEX/ Speedo/ Type/ misc/
```

在我们的系统中，我们拥有列出的所有目录以及一个用于 PEX 字体的 PEX 目录（你现在可以忽略它；更多关于 PEX——X 的 3D 扩展的信息请参见附录 B）。如果你没有相应的字体目录，你应该删除 XF86Config 文件中的任何条目。例如，如果你没有加载 100 DPI 字体（100dpi），那么你的 `Files` 部分看起来应该像这样：

### Section "Files":

- RgbPath `/usr/X11R6/lib/X11/rgb`

- FontPath `/usr/X11R6/lib/X11/fonts/misc/*`

- FontPath `/usr/X11R6/lib/X11/fonts/Type/*`

- FontPath `/usr/X11R6/lib/X11/fonts/Speedo/*`

- FontPath `/usr/X11R6/lib/X11/fonts/75dpi/*`

- EndSection

我们删除了 100dpi 字体的条目。

在运行 `xf86config` 时，你应该表示你不打算使用 X 字体服务器，即使你想使用。如果在你启动 X 之前字体服务器没有运行，你的系统可能会锁死。我们发现分开问题要容易得多。首先，让 X 运行起来。然后配置 X 字体服务器（提供缩放字体）。你可能需要回来编辑 XF86Config 文件，但这很麻烦。

### 配置 ServerFlags

在 `Files` 部分之后是 `ServerFlags` 部分。事实上，我们很少需要使用它。

### 表 3.7 Server 标志

| 选项 | 含义 |
| :--- | :--- |
| NoTrap | 当信号到达时产生核心转储 |
| DontZap | 禁用切换 |
| DontZoom | 禁用图形 |

切换到虚拟终端的魔法键序列是 Alt-Fn，其中 Fn 是你键盘上的功能键之一，例如 F1。但要注意：在 X 中，切换到虚拟终端的魔法键序列不是 Alt-Fn，而是 Ctrl-Alt-Fn。产生差异是因为大多数窗口管理器捕获了 Alt-Fn。

```
Section "ServerFlags"
NoTrap
DontZap
DontZoom
EndSection
```

### 表 3.8 键盘选项

| 选项 | 用法 |
| :--- | :--- |
| Protocol | 标准 |
| AutoRepeat rate | 设置自动重复 |
| ServerLock | 如下所示 |
| LeftAlt key | 覆盖左 Alt (Meta) 的默认值 |
| RightAlt key | 覆盖右 Alt (Meta) 的默认值 |
| ScrollLock key | 覆盖 ScrollLock (Compose) 的默认值 |
| RightCtrl key | 覆盖右 Ctrl (Control) 的默认值 |
| XLeds | 允许程序使用 LED |
| VTSysreq | 使用 Alt-SysReq-Fn |
| VTinit command | 运行 /bin/sh -c |

## 第3章：安装与配置 XFree86

### 虚拟终端

Linux 支持虚拟终端。虚拟终端是连接到你屏幕的伪终端终端。X 使用一个虚拟终端，但你可能有更多。

每个虚拟终端都会接管你的整个显示器并呈现出一个传统的文本终端，就像你登录时看到的那样。特殊的键序列允许你在虚拟终端之间切换。当你这样做时，屏幕会被清除，你会看到下一个虚拟终端。

当你有一整个屏幕的 `xterm` 终端窗口时，虚拟终端并不很有价值。X 环境允许你使用选择的字体，提供许多行，支持滚动条，并支持复制和粘贴——这些是虚拟终端都不具备的。因此，我们很少使用虚拟终端。

但有一个地方虚拟终端大派用场：如果你的 X 显示器锁死了，你可以切换到另一个虚拟终端并杀死所有的 X 进程。

大多数笔记本电脑都有一个特殊的 Fn 键，用于为键盘功能键提供第二组功能。笔记本键盘上的 Fn 键不应与这里使用的 Fn 符号混淆。

对于键位映射，你可以将每个键设置为以下内容之一：

- Compose
- Control
- Meta
- Shift
- Lock
- ScrollLock

## 第3章：安装与配置 XFree86

```
### Protocol "Xqueue"
AutoRepeat 500 5
### ServerNumLock
### Xled 1 2 3
LeftAlt Meta
RightAlt ModeShift
### RightCtl Compose
### ScrollLock ModeLock
EndSection
```

注意，我们把这些内容注释掉了。

### 配置指针部分 (Pointer Section)

鼠标——在 X 术语中称为 pointer——设置起来相当简单，但你必须注意一些技巧。之所以这样，主要是因为许多厂商的鼠标（例如罗技 Logitech）被设置为模拟其他厂商的鼠标，最著名的微软鼠标。正因如此，你可能需要对你的鼠标“撒谎”。

例如，我们的测试系统之一使用一个串行罗技鼠标。这只鼠标由罗技设计，用于模拟微软串行鼠标。奇怪的是，罗技鼠标有三个按钮（这对 X 来说是一件好事，因为大多数 X 期望三键鼠标），而微软串行鼠标只有两个按钮。

当我们配置 XF8Config 文件时，我们声称自己的罗技鼠标实际上是微软鼠标（罗技鼠标的另一种常见选择是声称它们是 Mouseman 鼠标）。

在 Pointer 部分，你必须指定的两个键是鼠标的类型（例如 Microsoft）以及如果是串行鼠标，连接的端口。借此，我们的 Pointer 部分非常短：

```
Section "Pointer"
Protocol "Microsoft"
Device "/dev/ttyS0"
EndSection
```

请务必输入你拥有的鼠标类型以及它连接的设备，而不仅仅是复制我们的配置。协议必须是表 3.9 中列出的选项之一。

### 表 3.9 指针协议 (Pointer Protocols)

| 协议 (Protocol) |
| --- |
| BusMouse |
| Logitech |
| Microsoft |
| MMSeries |
| Mouseman |
| MouseSystems |
| PS/2 |
| MMHitTab |
| Xqueue |
| OSMouse |
