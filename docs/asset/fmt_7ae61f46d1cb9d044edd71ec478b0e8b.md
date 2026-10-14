
### xscreensaver-command -prefs

## 第15章：配置X11显示

290

按下回车后，你可以使用`xscreensaver-command`客户端及其命令行选项来控制屏幕保护。例如，要启动屏幕保护，使用该客户端如下：

```
xscreensaver-command -activate
```

要查看当前设置，使用`-prefs`选项如下：

```
xscreensaver-command -prefs
```

黑屏是工作站闲置时提供显示器隐私的一种方法，但它没有提供任何安全措施。在接下来几节中讨论的其他客户端提供了更高的安全性。

### 使用多头显示

XFree86发行版的新功能之一是支持 Xinerama，即多头显示，类似于苹果Mac支持15年的功能。要利用此功能，你必须使用XFree86 4.X系列并在系统中安装一个或多个兼容的显卡。

XFree86提供了多种类型的多显示器支持。首先，拥有多个X实例（运行多个X会话）可以支持一个或多个显示器分辨率和色彩深度。最后，单个X实例可以利用Xinerama，允许窗口跨越物理

### 选择显卡

任何支持的显卡都允许你使用 Xinerama。一些优质显卡包括 Matrox 的产品，它们内置了双或四头支持。这种支持将节省你购买额外显卡的费用，对于需要单个显卡的专用系统来说是完美的解决方案。

## 兼容的客户端和窗口管理器

目前支持多头显示的窗口管理器有 Enlightenment、sawfish 以及可能还有 Window Maker。

## 配置 XF86Config

等等，你需要在 XF86Config文件中创建几个特殊章节来创建多显示器的支持。对多个设备、显示器、屏幕的支持已内置在 FreeX86 4.0.1中。你的要任务是为每个显示器、视频设备和屏幕创建唯一的条目。

例如，如果你的系统将使用两个显示器——一个是15英寸液晶显示器（LCD），另一个是17英寸同步显示器——为每个创建一个“Monitor”章节，并提供如下唯一的标识符：

```
Section "Monitor"
Identifier "NECXV17"
HorizSync 31-65
VertRefresh 55-100
EndSection
```

```
Section "Monitor"
Identifier "LCD"
HorizSync 31-65
VertRefresh 56-75
EndSection
```

在这个示例中，X会话将使用标记为“NECXV17”的NEC XV17和标记为“LCD”的三星LCD显示器。如果你计划使用两块显卡，你将

## 第 15 章：配置 X11 显示

以确定显卡报告的 BusIDs。要查找视频显卡的 BusID，你可以使用带有`-scanpci`命令行选项的 X 服务器，如下所示：

```bash
# XFree86 -scanpci
...
正在探测 PCI 设备 (总线:设备:函数)

(1:0:0) Matrox 未知卡 (0x2179) 使用 Matrox MGA G400 AGP
```

此示例显示了在台式电脑上使用 Matrox G400 双头 AGP 视频卡时的结果 (1:0:0)。请注意，尽管卡上内置了两个视频适配器，但 G400 显并没有报告两个 PCI BusID。如果你安装了两个显卡，X 服务器应该报告两个唯一的 BusID。

接下来你应该定义你的图形设备。同样，在如下的 "Device" 部分为每个设备包含一个唯一的标识符：

```
Section "Device"
Identifier  "G4001"
Driver      "mga"
Option      "DigitalScreen "yes"
BusID       "PCI:1:0:0"
Screen      0
VideoRam    32768
EndSection
```

```
Section "Device"
Identifier  "G4002"
Driver      "mga"
BusID       "PCI:1:0:0"
Screen      1
VideoRam    32768
EndSection
```

在此示例中，注意每个设备都分配了一个唯一的标识符。Driver 字段指定了 XFree86 驱动程序 `mga_drv.o`，这样当 X 启动时，就会从 `/usr/X11R6/lib/modules/drivers` 目录加载该驱动程序。如果显示器是 LCD 面板，该驱动程序需要 `DigitalScreen` 选项（在这种情况下，“yes” 设置表示 LCD 将被用于特定的显卡）。接下来，每个 `Device` 定义都被分配了一个屏幕编号，从第一个屏幕开始为 0。

现在你已经定义了显示器和视频设备，你需要为它们中的每一个创建一个独立的 "Screen" 部分，使用屏幕编号、设备标识符和显示器标识符，如下所示：

```
Section "Screen"
Identifier "Screen 0"
Device "G4001"
Monitor "LCD"
DefaultDepth 16
Subsection "Display"
Depth 16
Modes "1024x768" "1280x1024"
Virtual 1024 768
ViewPort 0 0
EndSubsection
EndSection
```

```
Section "Screen"
Identifier "Screen 1"
Device "G4002"
Monitor "NECXV17"
DefaultDepth 16
Subsection "Display"
Depth 16
Modes "1024x768" "1280x1024"
Virtual 1024 768
ViewPort 0 0
EndSubsection
EndSection
```

每个 "Screen" 部分都使用你之前的定义，并包含一个带有色彩深度和分辨率设置的 "Display" 子部分。为了避免任何问题，此示例使用了在每个显示器上都相同的设置。如你所见，“Screen”部分决定了显卡到显示器的分配以及显示器的特性。

当你决定如何安排显示器时，你需要创建或编辑一个多个 `ServerLayout` 部分。每个部分将至少使用两个屏幕编号，并带有屏幕 ID 和位置信息或放置关键字，以指定相对于主显示器将哪个显示器放在何处。`ServerLayout` 部分使用来自至少两个 "Screen" 部分的信息。

例如，要定义一个名为 "Dual-head" 的布局，将显示器并排并将 LCD 在左侧，请创建一个如下 `ServerLayout` 部分：

```bash
Section "ServerLayout"
Identifier "Dual-head"
Screen "Screen 0" LeftOf "Screen 1"
Screen "Screen 1"
InputDevice "Mousel" "CorePointer"
InputDevice "Keyboard1" "CoreKeyboard"
EndSection
```

此布局创建了一个连续显示，你可以在显示器之间的虚拟边界上绘制窗口或活动客户端。在编辑 X86Config 后，使用 `startx` 命令启动你的 X 会话。你还需要按照如下方式使用 `+xinerama` 命令行选项来启用你的布局：

```bash
# startx --+xinerama
```

你的 XF86Config 文件可以有多个 `ServerLayout` 部分。例如，如果你只是想要同步显示，而不是在显示器之间进行连续显示，请使用如下布局：

```bash
Section "ServerLayout"
Identifier "Simultaneous"
Screen "Screen 0"
Screen "Screen 1"
InputDevice "Mousel" "CorePointer"
InputDevice "Keyboard1" "CoreKeyboard"
EndSection
```

在此示例中，两个显示器将同时显示相同的 X 会话。你可以通过使用 X 服务器的 `-layout` 命令行选项以及布局名称来要使用的布局，如以下任一示例所示：

```bash
# startx --+xinerama -layout Dual-head
# startx --+xinerama -layout Simultaneous
```

## 配置 twwm 窗口管理器

你可能会在你的 Linux 发行版的 CD-ROM 中找到许多此类窗口管理器（特别是如果你使用 SUSE Linux）。KDE 和 GNOME 是大多数 Linux 用户最流行的桌面环境。你还将发现从头构建和安装某些窗口管理器是多么简单。
