

不被直接支持的鼠标通常可以通过模拟更常见的类型（例如 Microsoft 或 Logitech）来使用。XF86Config 文件中的鼠标部分标记为 "pointer"（源自 pointing device，即指点设备），其外观如下：

```
Section "Pointer"
    Protocol "Microsoft"
    Device "/dev/mouse"

# When using XQUEUE, comment out the above two lines, and uncomment
# the following line.
# Protocol "Xqueue"

# Baudrate and SampleRate are only for some Logitech mice
# BaudRate 9600
# SampleRate 150

# Emulate3Buttons is an option for 2-button Microsoft mice
# Emulate3Buttons

# ChordMiddle is an option for some 3-button Logitech mice
# ChordMiddle

EndSection
```

Protocol 部分是鼠标名称或要使用的模拟类型。支持的鼠标系统名称列在 xconfig 或 XF86Config 的手册页（man page）中，因此，如果你使用的鼠标来自 Microsoft 或 Logitech 以外的供应商，请查阅手册页或其他随附文档以查找要指定的协议名称。识别鼠标类型的另一种方法是在 Linux 启动时观察启动信息：它通常会识别出鼠标的类型。

Microsoft 鼠标必然使用 Microsoft 协议。许多 Logitech 鼠标设备与 Microsoft 兼容，而较新的版本则使用 MouseMan 协议。Dexxa 以及许多其他鼠标设备供应商都模拟 Microsoft 鼠标，因此可以使用 Microsoft 协议。

Device 条目使用 Linux 设备术语指定鼠标连接的端口。在大多数情况下，条目 `/dev/mouse` 就足够了，因为 Linux 安装过程通常已经配置好了鼠标。如果你使用的是在 IBM PS/2 型号的 PS/2 端口上配置的鼠标，请使用 PS/2 设备驱动程序，而不是串口设备驱动程序。有效的设备驱动程序的列表可以在手册页或随 XFree86 提供的文档文件中找到，但大多数版本支持以下设备：

![Image](img/e8e6b47ac20475e23d48b4c476f5d891_442_0.png)

- `/dev/mouse`：使用 Linux 默认鼠标驱动程序
- `/dev/importbm`：仅适用于 Microsoft 总线鼠标
- `/dev/logibm`：仅适用于 Logitech 总线鼠标
- `/dev/psaux`：PS/2 端口鼠标

总线鼠标需要在 XFree86 和内核中都设置特定的 IRQ。请确保这两处的 IRQ 相同。

与键盘一样，xqueue 用户也有一个选项。由于大多数 XFree86 安装不使用 Xqueue，因此请保留该行处于注释状态。正如注释所示，波特率（baud rate）和采样率（sampling rate）行仅适用于一些较旧的 Logitech 鼠标设备。大多数鼠标设备不需要这些行，因此请保持它们被注释掉。如果你的鼠标没有这些设置就无法工作，请尝试 9600 波特率，如果不起作用，再尝试 1200 波特率。XFree86 的某些早期版本倾向于指定波特率，但请先尝试不指定该项。

Emulate3Buttons 选项对于拥有两键鼠标的用户很有用。启用后，Emulate3Buttons 允许你通过同时按下左右鼠标按钮来模拟按下中间按钮。许多 Linux（和 UNIX）应用程序会利用鼠标的三个按钮，因此这对于 Microsoft 及兼容鼠标用户来说是一个有用的选项。

最后，ChordMiddle 选项用于某些 Logitech 鼠标型号。如果使用 Logitech 驱动程序，请尝试在 XFree86 下不开启此选项的情况下使用鼠标。如果鼠标行为不正常，请尝试取消该行的注释。大多数 Logitech 鼠标设备不需要开启 ChordMiddle。

## 显示器型号

正确设置显示器是配置 XFree86 的重要步骤，而且很容易出错。如果某些设置不正确，可能会损坏显示器，因此请小心！耐心和良好的判断力会有所帮助，但显示器的操作手册是一个更好的信息来源。

如果不确定任何设置，请选择最基础的级别，直到获取更多信息为止。例如，如果不确定显示器是否支持高分辨率，请坚持使用 VGA 或 SVGA，直到得到确认。

XFree86Config 文件中的显示器部分为了方便起见被划分为更小的子部分。我们可以更详细地查看这些子部分。第一个部分询问关于显示器类型和型号的信息。该子部分如下所示：

```
Section "Monitor"
    Identifier "Generic Monitor"
    VendorName "Unknown"
    ModelName "Unknown"
```

此部分中的条目仅为文本字符串，对 XFree86 没有实际的配置值。只有在 XFree86 启动时文本字符串被回显给你，或者某个实用程序显示配置信息时，才会使用它们。你可以输入这些项目的适当值，使 XFree86 在使用上更加友好。

下一个子部分处理显示器的水平带宽。这是一个重要的部分，你应该尝试查找显示器的实际数值。随 XFree86 提供的文档中列出了特定品牌的一些设置，特别是在 Monitors 和 VideoModes.doc 文档中。请检查你的发行版目录中的任何规范文档文件。如果你找不到这些设置的具体数值，除非你知道你的显示器能够支持更高的值，否则使用最低设置作为默认值。带宽部分如下所示：

```
# Bandwidth is in MHz unless units are specified

Bandwidth 25.2
```

```
# HorizSync is in KHz unless units are specified.
# HorizSync may be a comma separated list of discrete values, or a
# comma separated list of ranges of values.
# NOTE: THE VALUES HERE ARE EXAMPLES ONLY. REFER TO YOUR MONITOR'S
# USER MANUAL FOR THE CORRECT NUMBERS.

HorizSync 31.5 # typical for a single frequency fixed-sync monitor

# HorizSync 30-64 # multisync
# HorizSync 31.5, 35.2 # multiple fixed sync frequencies
# HorizSync 15-25, 30-50 # multiple ranges of sync frequencies
```

带宽设置旁边有很好的注释，如前面的代码所示。例如，如果你正在安装多同步（multisync）显示器，你可以注释掉 31.5K Hz 行，并取消 30-64 KHz 行的注释。

垂直刷新率在另一个子部分中设置，它对显示器的健康状况至关重要，其重要性与带宽相当。再次，请查阅文档以获取更多信息。垂直刷新率子部分的代码如下所示：

```
# VertRefresh is in Hz unless units are specified.
# VertRefresh may be a comma separated list of discrete values, or a
# comma separated list of ranges of values.
# NOTE: THE VALUES HERE ARE EXAMPLES ONLY. REFER TO YOUR MONITOR'S
# USER MANUAL FOR THE CORRECT NUMBERS.

VertRefresh 60 # typical for a single frequency fixed-sync monitor

# VertRefresh 50-100 # multisync
# VertRefresh 60, 65 # multiple fixed sync frequencies
# VertRefresh 40-50, 80-100 # multiple ranges of sync frequencies
```

文件中的注释再次提供了帮助，显示了最常见的设置。这些可以作为参考，但你应该查阅文档以获取具体细节。

正确设置视频模式非常重要，因为过高的视频分辨率可能会导致雪花、黑屏或系统崩溃。前面提到的 SuperProbe 实用程序可以帮助确定支持的视频模式，尽管大多数显示器在其文档中都有良好的支持模式列表。XFree86 的 Monitors 文件也列出了许多流行显示器及其模式。设置视频模式的子部分如下：

```
# Modes can be specified in two formats. A compact one-line format, or
# a multi-line format.

# A generic VGA 640x480 mode (hsync = 31.5kHz, refresh = 60Hz)
# These two are equivalent

# Modeline "640x480" 25.175 640 664 760 800 480 491 493 525

Mode "640x480"
    DotClock 25.175
    HTimings 640 664 760 800
    VTimings 480 491 493 525
EndMode

# These two are equivalent

# Modeline "1024x768i" 45 1024 1048 1208 1264 768 776 784 817 Interlace

Mode "1024x768i"
    DotClock 45
    HTimings 1024 1048 1208 1264
    VTimings 768 776 784 817
    Flags "Interlace"
EndMode
```

上述示例显示了标准 VGA（640×480）分辨率和高分辨率（1,024×768）。你可以修改这些条目以匹配你特定的分辨率需求。从上面的代码中可以看出，你需要知道显示器和视频卡的点时钟（dot clock）以及水平和垂直时序。请查阅文档！请注意，你可以在单行中指定模式的所有详细信息，但更详细的列表更容易阅读和操作。

