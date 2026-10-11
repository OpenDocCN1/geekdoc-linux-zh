

服务器。如果在发行版设置过程中安装 X，设置程序通常会检测出正确的视频芯片组并安装相应的服务器。如果在初始设置完成后安装 X，则必须手动安装正确的 X 服务器。例如，要在 Red Hat 系统上安装 S3 服务器，你需要安装 `XFree86-S3-3.3.6-33.1386.rpm` 软件包。

## 表 9-1 XFree v3 X 服务器

| X 服务器 | 支持的芯片组 |
| :--- | :--- |
| X3DL | 用于 3Dlabs 显卡的服务器。 |
| X8514 | 用于基于 8514 的显卡的服务器。 |
| XAGX | 用于基于 AGX 的显卡的服务器。 |
| XFB | 帧缓冲区驱动程序，可用于某些没有特定 X 服务器的显卡。 |
| XI128 | 用于 Number Nine Imagine I28 显卡的服务器。 |
| XMachine32 | 用于 ATI Mach 32 显卡的服务器。 |
| XMachine64 | 用于 ATI Mach 64 显卡的服务器。 |
| XMachine8 | 用于 ATI Mach 8 显卡的服务器。 |
| XMono | 用于单色视频显示的服务器。 |
| XP9K | 用于基于 P9000 的显卡的服务器。 |
| XS3 | 用于基于 S3 的显卡的服务器。 |
| XS3V | 用于基于 S3 Virge 的显卡的服务器。 |
| XSVGA | 用于 VESA 超级 VGA 显卡的服务器。 |
| XVGA16 | VGA 16 色服务器。许多没有专用 X 服务器的显卡可以使用此服务器。 |
| XX32 | 用于基于 ET4000/W32 的显卡的服务器。 |

> **考试提示** 安装 XFree v3 时，需要为你的视频芯片组安装正确的 X 服务器。

从 XFree v4 开始，X 服务器已得到整合。你无需为特定的视频芯片组安装特定的服务器，只需安装主服务器，并在 X 配置文件中指定要使用的芯片组驱动程序即可。缺点是，目前 XFree v4 并不支持 XFree v3 支持的所有视频芯片组。

在 X 的任一版本中，文件 `/etc/X11/X` 实际上是一个指向你希望运行的 X 服务器的链接。请考虑以下示例：

```
[root@redhat X11]# ls -l X
lrwxrwxrwx 1 root root 29 Aug 21 15:32 X ->
../../../usr/X11R6/bin/XF86_SVGA
```

这表明 `/etc/X11/X` 文件链接到了 `/usr/X11R6/bin/XF86_SVGA`，即 SVGA X 服务器。由于 XFree v4 没有独立的 X 服务器，`X` 文件链接到相同的服务器，如下所示：

```
debian:/etc/X11# ls -l X
lrwxrwxrwx 1 root root 20 Dec 11 10:55 X ->
/usr/bin/X11/XFree86
```

文件 `/usr/bin/X11/XFree86` 是 v4 版本的 X 服务器，并将始终是链接的目标。

X 服务器的主要配置文件是 `XF86Config` 文件。该文件的格式在 XFree v3 和 v4 之间相似，但存在一些细微差异。如果你使用提供的工具创建此文件，则无需担心这些差异。

XFree v4 中最好的改进之一是速度。与 XFree v3 相比，XFree v4 明显提高了性能。新版本还为游戏和图形应用程序提供了更强大的硬件加速支持。

# 配置 X

## 2.10 X

![](img/96d9ccd181675a8ae8b6a1146c919d2b_372_0.png)

- 安装并配置 XF86。验证显卡和显示器是否受 X 服务器支持，安装正确的 X 服务器，配置 X 服务器，安装 X 字体服务器，安装 X 所需的字体（可能需要手动编辑 /etc/X11/XF86Config 中的 "Files" 部分），并根据显卡和显示器定制和调整 X。命令：XF86Setup, x86config。文件：/etc/X11/XF86Config, .xresources。

配置 X 窗口系统可能会让新的 Linux 用户望而却步。它可能会变成一个非常复杂的问题，伴随着奇怪的错误消息和不可思议的结果。由于大多数发行版现在在检测系统硬件和显示器方面做得非常出色，用户不需要再执行过去所需的所有步骤。但是，如果你手动安装 X 或有特殊的设置，你可能仍需要自己配置 X。这里介绍的两个配置工具可用于任何发行版。此外，每个发行版通常都提供自己的特定于发行版的工具。例如，Red Hat 使用 Xconfigurator，Mandrake 使用 DrakX，Debian 使用 anXious 和 Dax。

X 服务器的配置文件是 `XF86Config`。

# 手动配置 XF86Config 文件

主要的 X 窗口配置文件是 /etc/X11/XF86Config。虽然你现在不再需要手动构建此文件，但如果出现问题或需要进行简单更改，你仍应熟悉其布局。该文件分为几个部分，其语法如下：

```
Section "Section Name"
  This is a command
EndSection
```

> **注意**
> XFree86 v4 使用名为 *XF86Config-4* 的配置文件。

以下部分用于 *XF86Config* 文件，通常按此顺序排列：

- Files
- ServerFlags
- Keyboard
- Pointer
- Monitor
- Device
- Screen

## Files

*Files* 部分用于 RGB（红绿蓝）设置和字体路径。可以指定多个字体路径，并且所有这些路径都会被搜索。如果找不到可用的字体，X 服务器将会崩溃。以下是 *Files* 部分的示例。

> **在现实世界中**
> 即使你使用字体服务器来管理所有字体，通常也需要指定 *misc* 字体目录的路径。此路径提供基本的系统字体。

```
# ***********************************************
# Files section.  This allows default font and rgb paths to be set.
# ***********************************************
Section "Files"

# The location of the RGB database.  Note. this is the name of the
# file minus the extension (like ".txt" or ".db").  There is normally
# no need to change the default.
RgbPath		"/usr/X11R6/lib/X11/rgb"

# Multiple FontPath entries are allowed (they are concatenated together)
# By default, Red Hat 6.0 and later now use a font server independent of
# the X server to render fonts.
	FontPath		"/usr/X11R6/lib/X11/fonts/TrueType"
	FontPath		"unix/:7" 

EndSection
```

此示例使用了两个字体路径。第二个路径定义了字体服务器：

```
FontPath		"unix/:7"
```

字体服务器可以在本地系统或跨网络运行。它可以同时为许多系统提供字体。上面指定的行表明使用的是本地字体服务器，因为端口号是 7。

此部分中另一个可能的条目是 ModulePath，用于加载动态模块。这在 XFree v4 中得到了广泛使用。

**考试提示**

为了应对考试，**Files** 部分中最重要的是了解字体配置。

## ServerFlags

此部分设置几个服务器选项。表 9-2 显示了此部分的可能条目。很多时候，此部分是空的或被完全注释掉。可以看出，许多杂项设置都归入此处。

**表 9-2**
**ServerFlags 条目**

| 条目 | 功能 |
| :--- | :--- |
| NoTrapSignals | 告诉 X 服务器不要意外捕获信号并干净地退出。 |
| DontZap | 禁用使用 Ctrl-Alt-Backspace 键组合来终止 X 服务器。 |
| DontZoom | 禁用使用 Ctrl-Alt-KeyPad Plus 和 Ctrl-Alt-KeyPad Minus，这些通常用于更改屏幕分辨率并起到变焦作用。 |
| `AllowNonLocalXvidtune` | 允许 xvidtune 客户端从远程系统连接。xvidtune 客户端将在本章后续部分详细讨论。 |
| `DisableVidMode` | 禁用 xvidtune 使用的 VidMode 扩展功能的部分。 |
| `AllowNonLocalModInDev` | 允许来自远程主机的用户连接并更改运行环境中的键盘和鼠标设置。 |
| `DisableModInDev` | 禁用允许远程更改输入设置的扩展功能。 |
| `AllowMouseOpenFail` | 通常，如果无法打开鼠标设备，X 服务器将无法启动。此选项允许在这种情况下启动 X 服务器。 |

## Keyboard

正如你所期望的，此部分配置键盘设备。它有许多不同的配置条目，涉及键盘设置。也可以在此处定义 Meta 键。Meta 键是那些改变下一个按下键的功能的键。例如，Ctrl 和 Alt 通常是 Meta 键。以下是此部分的示例。

```text
Section  "Keyboard"
    Protocol  "Standard"

# when using XQUEUE, comment out the above line, and uncomment the
# following line
#Protocol  "Xqueue"
    AutoRepeat  500 5

# Let the server do the NumLock processing. This should only be
# required when using pre-R6 clients
#ServerNumLock

# Specify which keyboard LEDs can be user-controlled (eg, with xset(1))
#XLEDs          1 2 3

#To set the LeftAlt to Meta, RightAlt key to ModeShift,
#RightCtl key to Compose, and ScrollLock key to ModeLock:
    LeftAlt     Meta
    RightAlt    Meta
```

