

这些模块的范围可以从特殊的显卡支持到字体光栅化器。模块位于 /usr/lib/modules 目录下的子目录中。

## The InputDevice Section

InputDevice 部分配置特定的设备，例如键盘或鼠标，如本例所示：

```
Section "InputDevice"
    Identifier  "Keyboard0"
    Driver      "kbd"

    Option      "XkbModel"      "pc105"
    Option      "XkbLayout"     "us"
EndSection
Section "InputDevice"
    Identifier  "Mouse0"
    Driver      "mouse"
    Option      "Protocol" "IMPS/2"
    Option      "Device"  "/dev/input/mice"
    Option      "ZAxisMapping" "4 5"
    Option      "Emulate3Buttons" "yes"
EndSection
```

你可以配置多个设备，并且可能存在多个 InputDevice 部分。前面的示例指定了一个基本的键盘和一个双按钮 PS/2 鼠标（实际上是一个戴尔触摸板指针）。一个指定使用 USB 设备的 InputDevice 部分可以同时使用（以启用 PS/2 和 USB 指针的鼠标操作），可能如下所示：

```
Section "InputDevice"
    Identifier  "Mouse0"
    Driver      "mouse"
    Option      "Device"  "/dev/input/mice"
    Option      "Protocol" "IMPS/2"
    Option      "Emulate3Buttons" "off"
    Option      "ZAxisMapping" "4 5"
EndSection
```

## The Monitor Section

Monitor 部分配置在 ServerLayout 部分中声明的指定显示设备，如本例所示：

```
Section "Monitor"
    Identifier  "Monitor0"
    VendorName  "Monitor Vendor"
    ModelName   "Monitor Model"
    DisplaySize 300    220
    HorizSync    31.5-48.5
    VertRefresh 50-70
    Option "dpms"
EndSection
```

请注意，X 服务器会根据本节中的水平和垂直同步及刷新值自动确定最佳视频时序。如果需要，旧式的 modeline 条目（由 XFree86 4.0 之前的发行版和服务器使用）仍可使用。如果在配置 X 时监视器被自动检测到（参见本章后面的“Configuring X”部分），其定义和功能将从 MonitorsDB 数据库插入到你的 xorg.conf 文件中。该数据库包含超过 600 台监视器，位于 /usr/share/hwdata 目录中。

## The Device Section

Device 部分提供了计算机使用的视频图形芯片组的相关信息，如本例所示：

```
Section "Device"
    Identifier  "Videocard0"
    Driver      "radeon"
    VendorName  "Videocard vendor"
    BoardName   "ATI Radeon Mobility M6"

EndSection
```

此示例将安装的显卡识别为使用 ATI Mobility M6 图形芯片组。Driver 条目告诉 Xorg 服务器从 /usr/lib/modules/drivers 目录加载 radeon_drv.o 模块。不同的芯片组具有不同的选项。例如，这里是 NeoMagic 视频芯片组的条目：

```
Section "Device"
    Identifier  "NeoMagic (laptop/notebook)"
    Driver      "neomagic"
    VendorName  "NeoMagic (laptop/notebook)"
    BoardName   "NeoMagic (laptop/notebook)"
    Option      "externDisp"
    Option      "internDisp"
EndSection
```

在此示例中，Device 部分指定了显卡的驱动程序（neomagic_drv.o），并启用了两个芯片组选项（externDisp 和 internDisp），以允许在笔记本电脑的 LCD 屏幕和外接显示器上显示。

Xorg 服务器支持数百种不同的视频芯片组。如果你在配置 X11 后随后更换了安装的显卡，你需要编辑现有的 Device 部分或使用本章讨论的 X 配置工具之一生成新的 xorg.conf 文件，以反映新卡的功能。你可以在配套的手册页中找到有关某些芯片选项的详细信息。你应该查看这些来源以获取优化和故障排除的提示。

## The Screen Section

Screen 部分将前几节的信息结合在一起（使用 Screen0、Device 和 Monitor Identifier 条目）。它还可以为会话指定一个或多个颜色深度和分辨率。以下是示例：

```
Section "Screen"
    Identifier "Screen0"
    Device     "Videocard0"
    Monitor    "Monitor0"
    DefaultDepth 24
    SubSection "Display"
        Viewport   0 0
        Depth      16
        Modes      "1024x768" "800x600" "640x480"
    EndSubSection
EndSection
```

在此示例中，默认颜色深度为数千色，分辨率为 1024x768，可选分辨率为 800x600 和 640x480。如果显卡和监视器组合支持，可以使用具有不同颜色深度和分辨率的多个 Display 子节条目（设置如 Depth 24 表示数百万色）。你也可以使用 DefaultDepth 条目（示例中为 24，即数千色），以及特定的颜色深度来标准化安装中的显示深度。

你还可以指定大于监视器或笔记本电脑显示屏硬件支持的桌面分辨率。此设置在 Display 子节中称为虚拟分辨率。这允许例如 800x600 显示在 1024x768 的虚拟窗口内平移（即滑动）。

> NOTE
> 如果你的监视器和显卡支持多种分辨率并且设置配置正确，你可以在 X 会话期间使用 Ctrl+Alt+小键盘+ 或 Ctrl+Alt+小键盘- 键组合实时更改分辨率。

## Configuring X

尽管 Ubuntu 安装程序可在安装期间用于配置 X，但如果 PC 的显卡未被识别，可能会出现问题。如果你在安装期间无法配置 X（参见第 1 章，“Installing Ubuntu”），请不要指定以图形配置启动，并跳过安装的 X 配置部分。请注意，某些安装，例如服务器，不需要为支持活动 X 而配置 X

