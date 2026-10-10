
如之前所述，`xorg.conf` 中的 `ServerLayout` 部分定义了屏幕布局，并命名输入设备。一个自动配置的 `xorg.conf` 中的 `ServerLayout` 部分可能如下：

| Key | Value |
| :--- | :--- |
| Identifier | single head configuration |
| Screen | 0 0 |
| InputDevice | Mouse "CorePointer" |
| InputDevice | Keyboard "CoreKeyboard" |
| InputDevice | DevMice "Core" |

在这个示例中，使用了单一显示器，并使用了两个话输入设备：鼠标和键盘。

### Files 部分

`xorg.conf` 中的 `Files` 部分可能如下：

| Key | Value |
| :--- | :--- |
| RbPath | `/usr/lib/X11/rgb` |
| FontPath | `unix::7100` |

此部分列出了可用的会话颜色（通过名称，在 `rgb.txt` 文件中）以及到 X 服务器的端口号。字体服务器 `xfs` 在启动时已启动，不需要 X 会话。如果不使用字体服务器，`FontPath` 则可以列出 `/usr/lib/X11/fonts` 目录下的每个字体目录，或者在本例中：

```
FontPath "/usr/lib/X11/fonts/100dpi"
FontPath "/usr/lib/X11/fonts/misc"
FontPath "/usr/lib/X11/fonts/75dpi"
FontPath "/usr/lib/X11/fonts/type1"
FontPath "/usr/lib/X11/fonts/Speedo"
```

这些目录包含了在 X 会话期间可用的默认压缩字体。通过使用 `/etc/X11/fs` 目录下的 `config` 文件来配置字体服务器。该文件包含了字体服务器使用的字体列表或目录。通过在该文件中添加 `alternate-server` 并重启字体服务器，你可以为 X 会话指定远程字体服务器。

### Module 部分

`xorg.conf` 文件的 `Module` 部分指定了为 X 会话加载的模块或驱动程序。该部分可能如下：

```
Load "dbe"
Load "extdev"
Load "fbdevhw"
```

```
Load "glx"
Load "record"
Load "freetype"
Load "type1"
Load "dri"
```

这些模块涵盖了从特殊卡支持到字体光化器的内容。模块位于 `/usr/lib/modules` 目录下的子目录。

# InputDevice 部分

`InputDevice` 部分用于配置特定的设备（例如键盘或鼠标），如下例所示：

```
Section "InputDevice"
Identifier "Keyboard0"
Driver "kbd"

Option "XkbModel" "pc105"
Option "XkbLayout" "us"
```

```
Section "InputDevice"
Identifier "Mouse"
Driver "mouse"
Option "Protocol" "IMPS/2"
Option "Device" "/dev/input/mice"
Option "ZAxisMapping" "4 5"
Option "Emulate3Buttons" "yes"
```

你可以配置多个设备，可能会存在多个 `InputDevice` 部分。前面的示例指定了一个基础键盘和一个双键 PS/2 鼠标（实际上是一个 Dell 触控板指针）。可以同时使用一个指定 USB 设备的 `InputDevice` 部分（以同时启用 PS/2 和 USB 指针鼠标），其格式如下：

```
Section "InputDevice"
Identifier "Mouse"
Driver "mouse"
Option "Device" "/dev/input/mice"
Option "Protocol" "IMPS/2"
Option "Emulate3Buttons" "off"
Option "ZAxisMapping" "4 5"
```

如果你更改了电脑的指针设备，应该运行 Fedora 的 `system-config-mouse` 客户端，它会自动更新你系统的 `xorg.conf` 文件。

从 Fedora Core 3 开始，鼠标设备的位置从 `/dev/mouse` 变为 `/dev/input/mice`。遗憾的是，当 `system-config-display` 写入 `xorg.conf` 文件时，它有时会产生混乱并将鼠标映射到 `/dev/mouse` 而不是 `/dev/input/mice`。这时候一点 `vi` 知识就派上用场了！

# Monitor 部分

`Monitor` 部分配置 `ServerLayout` 部分中指定的显示设备，如下例所示：

```
Section "Monitor"
Identifier "Monitor0"
VendorName "Monitor Vendor"
ModelName "Monitor Model"
DisplaySize 300 220
HorizSync 31.5-48.5
VertRefresh 50-70
Option "dpms"
```

EndSection

X 服务器根据该部分中的水平和垂直同步以及刷新值自动确定最佳视频时序。如果需要，可能仍使用旧式的模式项（用于 XFree 4.6 之前的发行版和服务器）。如果你在配置 X 时（本章的“配置 X”章节）自动检测到显示器，其定义和功能将从 MonitorsDB 数据库插入 `xorg.conf` 文件中。该数据库包含 600 多种显示器，位于 `/usr/share/hwdata` 目录。

# Device 部分

`Device` 部分提供了电脑所使用的图形芯片组的细节，如下例所示：

```
Section "Device"
Identifier "Videocard0"
Driver "radeon"
VendorName "Videocard vendor"
BoardName "ATI Radeon Mobility M6"
```

EndSection

此示例识别出一个安装的显卡使用的是 ATI Mobility M6 图形芯片组。`Driver` 条目告诉 X 服务器使用 `/usr/lib/modules/drivers` 目录下的 `radeon_drv.o` 模块。不同的芯片组有不同的选项。例如，这里是 NeoMagic 视频芯片组的条目：

```
Section "Device"
Identifier "NeoMagic (laptop/notebook)"
Driver "neomagic"
VendorName "NeoMagic (laptop/notebook)"
BoardName "NeoMagic (laptop/notebook)"
Option "externDisp"
Option "internDisp"
EndSection
```

在此示例中，`Device` 部分指定了显卡的驱动程序（`neomagic_drv.o`），并启用了两个芯片组选项（`externDisp` 和 `internDisp`），允许在笔记本电脑的 LCD 屏幕和另一个显示器上进行显示。

X 服务器支持数百种不同的视频芯片组。如果你在配置 X11 之后更改了安装的显卡，你需要编辑 `Device` 部分或使用本章讨论的 X 配置工具之一生成新的 `xorg.conf` 文件，以引用新卡的功能。你可以在配套的手页中找到有关芯片组选项的详细信息。你应该查看这些资源以获取有关优化和故障排除的提示。

# Screen 部分

`Screen` 部分将之前部分的信息（使用 `Screen0`、`Device` 和 `Monitor` 标识条目）结合起来。它还可以为会话指定一个或多个色彩深度和分辨率。例如：

```
Section "Screen"
Identifier "Screen0"
Device "Videocard0"
Monitor "Monitor0"
DefaultDepth 24
SubSection "Display"
Viewport 0 0
Depth 16
Modes "1024x768" "800x600" "640x480"
EndSection
```

在此示例中，数千色的色彩深度和 1024x768 的分辨率是默认值，可选分辨率为 800x600 和 640x640。显卡和显示器的组合可以使用多个不同色彩深度和分辨率的 `Display` 子部分条目（带有如 `Depth 24` 用于数百万颜色）。你还可以使用 `DefaultDepth` 条目（值为 24 或 24）。

# 第 3 章 使用 GNOME

![](img/4473647b35365e8747aa8fb2cf969fd5_96_0.png)

图 3.6 你可以滚动为你的 X 会话选择一个新的显示器。
