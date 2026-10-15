
xorg.conf 配置文件包含多个区段（section），每个区段定义了输入输出系统的不同元素。每个区段本身可能包含一个或多个子区段（subsection），用于进一步定义输入或输出设备。区段的基本格式如下：

```
# Comment for a section
Section "Name"
EntryName EntryValue
--
--
Subsection "Subname"
EntryName EntryValue
--
--
EndSubsection
EndSection
```

区段和子区段区域由名称/值对组成，用于定义设备的设置，例如鼠标类型或显示器可用的显示模式。

# 预定义区段

`xorg.conf` 文件中使用九个预定义的区段名称：

+   `Device`：描述显卡的特性。
+   `DRI`：包含直接渲染基础设施的信息，其中包含许多显卡中的硬件加速功能。
+   `Files`：列出字体文件的路径名以及用于显示的颜色数据库文件。
+   `InputDevice`：列出键盘和鼠标或其他指点设备（如轨迹球、触摸板或数位板）的信息。
+   `Module`：定义要加载的 X 服务器扩展模块和字体模块。
+   `Monitor`：列出显示器规格。
+   `ServerFlags`：列出用于控制 X Windows 环境特性的 X 服务器选项。
+   `ServerLayout`：组合一个或多个 `InputDevice` 和 `Screen` 区段，为 X Windows 环境创建布局。
+   `Screen`：定义由 X 服务器使用的显卡和显示器组合。

这些区段按需出现。也就是说，你只会看到 X.Org 配置文件中定义的那些实际用于描述工作站设备的区段。因此，如果你没有定义任何特殊的字体或颜色文件，那么在你的 Ubuntu 工作站上的配置文件中就不会看到 `Files` 区段。

# 配置示例

为了演示 X.Org 配置文件布局，让我们看一下来自 Ubuntu 工作站的示例配置文件。

```
Section "InputDevice"
Identifier "Generic Keyboard"
Driver "kbd"
Option "XkbRules" "xorg"
```

## 第 3 部分：管理工作站

```
Option "XkbModel" "pc105"
Option "XkbLayout" "us"
EndSection

Section "InputDevice"
Identifier "Configured Mouse"
Driver "mouse"
Option "CorePointer"
EndSection

Section "InputDevice"
Identifier "Synaptics Touchpad"
Driver "synaptics"
Option "SendCoreEvents" "true"
Option "Device" "/dev/psaux"
Option "Protocol" "auto-dev"
Option "HorizEdgeScroll" "0"
EndSection

Section "Device"
Identifier "Configured Video Device"
EndSection

Section "Monitor"
Identifier "Configured Monitor"
EndSection

Section "Screen"
Identifier "Default Screen"
Monitor "Configured Monitor"
Device "Configured Video Device"
EndSection

Section "ServerLayout"
Identifier "Default Layout"
Screen "Default Screen"
InputDevice "Synaptics Touchpad"
EndSection
```

此配置文件定义了多个输入和输出设备区段。第一个区段定义了一个 `InputDevice`——具体来说，是一个标准的美式 105 键键盘作为输入设备。该设备的区段标识符 `Generic Keyboard` 声明了设备的名称。X.Org 用于管理该设备的驱动程序通过 `Driver` 条目定义。之后，该区段包含了一些定义键盘设备特定特性的选项。

第二个区段也定义了一个 `InputDevice`，但这一次它定义了标准鼠标，使用标准的鼠标驱动程序且没有附加选项。在下一个区段中，你会看到又一个 `InputDevice` 的定义，但这个定义的是笔记本电脑上使用的触摸板。触摸板使用通用的 `Synaptics` 驱动程序与触摸板交互，并定义了一些选项来控制触摸板的操作方式。

在三个 `InputDevice` 区段之后，接下来的三个区段定义了工作站的视频环境：

```
Section "Device"
Identifier "Configured Video Device"
EndSection
```

```
Section "Monitor"
Identifier "Configured Monitor"
EndSection
```

```
Section "Screen"
Identifier "Default Screen"
Monitor "Configured Monitor"
Device "Configured Video Device"
EndSection
```

你可能注意到配置文件中定义的设备区段和显示器区段有些奇怪。配置文件不包含任何针对显卡设备或显示器的驱动程序或设置。

这个 X.Org 特性相对较新。当设备在配置文件中没有任何设置时，它会强制 X.Org 软件在每次启动新的 X Windows 会话时自动尝试检测该设备。

Ubuntu 从 8.04 版本开始使用这种方法，以帮助在安装后更方便地添加新的显卡和显示器功能。通过在每次系统启动时自动检测视频环境，Ubuntu 可以检测到你何时安装了新硬件。自动检测新硬件所需的时间并不长，因此相对于自动检测新硬件的优势来说，重新检测硬件带来的性能损失很小。

配置文件中的 `Screen` 区段将显示器和显卡捆绑为一个供 X.Org 使用的单一设备。使用此配置，X.Org 知道哪块显卡和哪个显示器配对使用。虽然此功能在单显示器情况下有些微不足道，但如果你有双显示器和双显卡，则它是必需的。

> 如果 X.Org 无法检测到你的显卡和显示器（或错误地检测到它们），你可以在 `xorg.conf` 文件中手动输入设置。当 X.Org 检测到设备的手动设置时，它不会尝试自动检测该设备，而是使用预定义的值。

> 对于显卡，你需要输入用于控制显卡的显卡驱动程序名称，以及定义显卡设置所需的任何附加选项。以下是 `xorg.conf` 配置文件中手动显卡条目示例：

```
Section "Device"
Identifier "Videocard0"
Driver "nv"
VendorName "Videocard vendor"
BoardName "nVidia GeForce 2 Go"
EndSection
```

*接上页*

显示器也是如此。您可以手动在 `xorg.conf` 配置文件中定义显示器的设置，这样 X.Org 就不会尝试自动检测它。以下是一个用于显示器的设置示例：

```
Section "Monitor"
Identifier "Monitor0"
Vendorname "Monitor Vendor"
ModelName "HP G72"
DisplaySize 320 240
HorizSync 30.0 - 85.0
VertRefresh 50.0 - 160.0
Option "dpms"
EndSection
```

如果您使用的是特殊的显卡或显示器，制造商通常会提供所需的 X Windows 驱动程序和配置设置。

一旦您定义了显卡和显示器，就必须定义一个 `Screen` 部分来将两个设备关联起来，并为屏幕定义功能特性：

```
Section "Screen"
Identifier "Screen0"
Device "Videocard0"
Monitor "Monitor0"
DefaultDepth 24
Subsection "Display"
Viewport 0 0
Depth 16
Modes "1024x768" "800x600" "640x480"
EndSubSection
EndSection
```

# Ubuntu 视频配置

安装 Ubuntu 之后，您可以使用桌面上提供的图形工具对 X Windows 系统进行一些手动更改。本节将引导您了解这些用于定制视频环境的工具。

## 屏幕分辨率工具

Ubuntu 中的 X.Org 环境正在快速发展和变化。每个新的 Ubuntu 发行版中都会实现进一步的改进和新想法。目前，在 Ubuntu 桌面中配置视频设置的核心工具是屏幕分辨率工具。

通过面板菜单选择“系统 ▸ 首选项 ▸ 屏幕分辨率”启动屏幕分辨率工具。主屏幕分辨率工具对话框如图 16-2 所示。

![](img/39e65eeb4f54001ede08c6114ae3cc6c_424_0.png)

### 图 16-2：屏幕分辨率对话框
