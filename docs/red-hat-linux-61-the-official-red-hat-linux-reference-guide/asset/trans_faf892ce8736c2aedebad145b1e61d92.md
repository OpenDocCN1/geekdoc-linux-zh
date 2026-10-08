

# 第 7 章 X Window 系统

必须至少有两个输入设备（InputDevices）：一个默认鼠标，一个默认键盘。选项 `CorePointer` 和 `CoreKeyboard` 表明这些是主鼠标和键盘。

- 选项 <option-name> — 可选条目，用于指定该节的额外参数。此处列出的任何选项将覆盖 `ServerFlags` 部分中列出的选项。

将 <option-name> 替换为 XF86Config 页面中此节列出的有效选项。

可以创建多个 `ServerLayout` 节。然而，除非通过命令行参数指定备用的 `ServerLayout` 节，否则服务器只会读取第一个。

### 3.7.1. Files

`Files` 节设置了 XFree86 服务器至关重要的路径，例如字体路径。以下示例说明了一个典型的 `Files` 节：

```
Section "Files"
RgbPath "/usr/X11R6/lib/rgb"
FontPath "/unix:/7100"
EndSection
```

以下条在 `Files` 节中常用：

- RgbPath — 指定 RGB 颜色数据库的位置。该数据库定义了 XFree86 中所有有效的颜色名称，并将它们与特定的 RGB 值绑定。
- FontPath — 指定 XFree86 服务器必须连接到哪里从 xfs 服务器获取字体。默认情况下，FontPath 为 `unix:7100`。这告诉 XFree86 服务器使用端口 7100  UNIX 域套接字进行进程间通信（IPC），以获取字体信息。有关 XFree86 和字体的更多信息，请参见第 7.4 节字体。
- ModulePath — 可选参数，指定存储 XFree86 模块的备用目录。

### 3.7.1. Module

`Module` 节指定 XFree86 服务器从 `/usr/X11R6/lib/modules/` 加载哪些模块。模块为 XFree86 服务器添加附加功能。以下示例说明了一个典型的 `Module` 节：

```
Section "Module"
Load "dbe"
Load "extmod"
Load "fbdevhw"
Load "glix"
Load "record"
Load "freetype"
Load "types1"
Load "dri"
EndSection
```

### 7.3.1.6. InputDevice

每个 `InputDevice` 节为 XFree86 服务器配置一个设备。系统通常至少有两个 `InputDevice` 节：键盘和鼠标。以下示例说明了一个典型的鼠标 `InputDevice` 节：

```
Section "InputDevice"
  Identifier "Mouse0"
  Driver "mouse"
  Option "Protocol" "IMPS/2"
  Option "Device" "/dev/input/mice"
  Option "Emulate3Buttons" "no"
  EndSection
```

以下条目在 `InputDevice` 节中常用：

- Identifier — 为此 `InputDevice` 节指定唯一名称。这是一个必选条目。
- Driver — 指定 XFree86 为设备加载的设备驱动程序名称。
- Option — 指定与设备相关的选项。对于鼠标，这些选项通常包括：
  - Protocol — 指定鼠标使用的协议，如 IMPS/2。
  - Device — 指定物理设备的位置。
  - Emulate3Buttons — 指定当同时按下鼠标按钮时是否允许两个按钮像三个按钮一样工作。

查阅 XF86Conf 页面获取此节的有效选项列表。
默认情况下，`InputDevice` 节带有注释，允许用户配置额外选项。

### 7.3.1.7. Monitor section

每个 `Monitor` 节配置系统使用的一种类型显示器。虽然 `Monitor` 节是最小配置，但对于机器使用的每种显示器类型，可能会出现额外的实例。

配置显示器的最佳方法是在安装过程中配置 X，或使用 X 配置工具。有关 X 配置工具的更多信息，请参阅《Red Linux 入门指南》中的“音频、视频和通用娱乐” 章节。

此示例说明了一个显示器的典型 `Monitor` 节：

```
Section "Monitor"
  Identifier "Monitor0"
  VendorName "Monitor Vendor"
  ModelName "DDC Probed Monitor - ViewSonic G773-2"
  DisplaySize "320 240"
  HorizSync "50.0 - 70.0"
  VertRefresh "50.0 - 180.0"
  EndSection
```

# 第 7 章 X Window 系统

> **警告**
> 如果手动编辑 `/etc/X11/xF86Config` 中 `Monitor` 节的值，请务必小心。不的值可能会损坏或破坏显示器。请咨询显示器文档获取安全操作参数列表。

以下是 `Monitor` 节中常用的条目：

- Identifier — 为此 `Monitor` 节指定唯一名称。这是一个必选条目。
- VendorName — 可选参数，指定显示器的厂商。
- ModelName — 可选参数，指定显示器的型号名称。
- DisplaySize — 可选参数，以毫米指定显示器的尺寸。
- HorizSync — 指定水平同步频率范围（kHz）。
- VertRefresh — 指定垂直刷新频率范围（kHz）。
- Modeline — 可选参数，指定显示器支持的特定分辨率范围。
- Option <option-name> — 可选条目，指定此节的额外参数。请参见 XF86Config 页面。

### 7.3.1. Device

每个 `Device` 节为系统配置一个显卡。虽然 `Device` 节是最小配置，但每个显卡可能会有额外的实例。配置显卡的最佳方法是在安装过程中配置 X，或使用 X 配置工具。详情参见《Red Linux 入门指南》。

以下示例说明了一个显卡的典型 `Device` 节：

```
Section "Device"
  Identifier "Videocard0"
  Driver "mga"
  VendorName "Videocard"
  BoardName "Matrix G200"
  VideoRam 8192
  Option "dpms"
EndSection
```

以下条在 `Device` 节中常用：

- Identifier — 为此 `Device` 节指定唯一名称。这是一个必选项。
- Driver — 指定 XFree86 必须加载的驱动程序。驱动列表可以在 `/usr/X11R6/lib/data` 中找到。
- VendorName — 可选参数，指定显卡厂商。
- BoardName — 可选参数，指定显卡型号。
- VideoRam — 可选参数，指定显卡上的可用显存（KB）。对于具有多个头器的系统，这是必要的。
- Screen — 指定 `Device` 节连接的显示器。此选项仅适用于具有多个头部的显卡。如果多个显示器连接到同一块显卡的不同头部，则必须存在多个 `Device` 节，且每个节必须有不同的 `Screen` 值。

`Screen` 值必须是整数。显卡的第一个头部的值为 0。每个额外的头部该值加 1。

- Option <option-name> — 可选条目，指定此节的额外参数。请参见 XF86Config 页面。

常用的选项之一是 `dpms`，它激活显示器的电源管理功能。

### 7.3.1. Screen

每个 `Screen` 节通过引用 `Device` 和 `Monitor` 节将一个显卡（或显卡头部）绑定到一个显示器。虽然一个 `Screen` 是最小配置，但机器上的每种显卡和显示器组合可能会出现额外的实例。

以下示例说明了一个典型的 `Screen` 节：

```
Section "Screen"
Identifier "Screen0"
Device "Videocard0"
Monitor "Monitor0"
DefaultDepth 16
SubSection "Display"
Depth 24
Modes "1280x1024" "1280x960" "1152x864" "1024x768" "800x600" "640x480"
EndSection
SubSection "Display"
Depth 16
Modes "1152x864" "1024x768" "800x600" "640x480"
EndSection
EndSection
```

以下条在 `Screen` 节常用：

- Identifier — 为此 `Screen` 节指定唯一名称。这是一个必选条目。
- Device — 指定 `Device` 节的唯一名称。这是一个必选条目。
- Monitor — 指定 `Monitor` 节的唯一名称。这是一个必选条目。
- DefaultDepth — 指定默认颜色深度（位）。在之前的示例中，16（提供数千种颜色）是默认值。允许存在多个 `DefaultDepth` 条目，但必须至少有一个。

