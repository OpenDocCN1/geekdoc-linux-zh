
## 输入设备和显示器

-   **InputDevice**——定义输入设备，例如键盘和鼠标；可以使用多个设备。
-   **Monitor**——定义连接显示器的功能特性；可以使用多个显示器。
-   **Device**——定义一个或多个显卡，并指定要启用或禁用的可选功能（如果有）。
-   **Screen**——定义一个或多个分辨率、颜色深度，可能还包括默认颜色深度以及其他设置。

以下各节简要介绍了这些元素；xorg.conf 手册页包含了关于所有选项以及可用于自定义桌面设置的其他关键词的完整文档。

### ServerLayout 部分

如前所述，xorg.conf 文件中的 *ServerLayout* 部分定义了显示器和屏幕布局，并指定了输入设备的名称。来自自动配置的 xorg.conf 文件的典型 *ServerLayout* 部分可能如下所示：

```
Section "ServerLayout"
    Identifier      "single head configuration"
    Screen          0     "Screen0"  0  0
    InputDevice     "Mouse0"   "CorePointer"
    InputDevice     "Keyboard0"   "CoreKeyboard"
    InputDevice     "DevInputMice"   "AlwaysCore"
EndSection
```

在此示例中，使用了单个显示器（数字指定了屏幕的位置），并且使用两个默认输入设备 *Mouse0* 和 *Keyboard0* 进行会话。

### Files 部分

xorg.conf 文件中的 *Files* 部分可能如下所示：

```
Section "Files"
    RgbPath         "/usr/X11R6/lib/X11/rgb"
    FontPath        "unix/:7100"
EndSection
```

此部分列出了可用的会话颜色（按名称，在文本文件 rgb.txt 中）以及到 X 字体服务器的端口号。字体服务器 *xfs* 在启动时启动，并且不需要活动的 X 会话。如果未使用字体服务器，*FontPath* 条目可以改为列出 /usr/X11R6/lib/X11/fonts/ 目录下的每个字体目录，如下例所示：

```
FontPath "/usr/X11R6/lib/X11/fonts/100dpi"
FontPath "/usr/X11R6/lib/X11/fonts/misc"
FontPath "/usr/X11R6/lib/X11/fonts/75dpi"
FontPath "/usr/X11R6/lib/X11/fonts/type1"
FontPath "/usr/X11R6/lib/X11/fonts/Speedo"
...
```

这些目录包含在 X 会话期间可用的默认压缩字体。使用 /etc/X11/fs 目录下名为 config 的文件来配置字体服务器。该文件包含字体服务器使用的字体列表或目录。在此文件中添加备用服务器条目并重启字体服务器后，您可以指定在 X 会话期间使用的远程字体服务器。这有助于集中字体支持并减少本地存储需求（尽管红帽 Linux 和 X 安装的近 5,000 种字体仅需 25MB）。

### Module 部分

xorg.conf 文件中的 Module 部分指定要为 X 会话加载的可加载模块或驱动程序。此部分可能如下所示：

```
Section "Module"
    Load "dbe"
    Load "extmod"
    Load "fbdevhw"
    Load "glx"
    Load "record"
    Load "freetype"
    Load "type1"
    Load "dri"
EndSection
```

这些模块的范围可以从特殊的显卡支持到字体光栅化器。模块位于 /usr/X11R6/lib/modules 目录下的子目录中。

### InputDevice 部分

InputDevice 部分配置特定设备，例如键盘或鼠标，如下例所示：

```
Section "InputDevice"
    Identifier "Keyboard0"
    Driver "kbd"
    Option "XkbModel" "pc105"
    Option "XkbLayout" "us"
EndSection

Section "InputDevice"
    Identifier "Mouse0"
    Driver "mouse"
    Option "Protocol" "IMPS/2"
    Option "Device" "/dev/input/mice"
    Option "ZAxisMapping" "4 5"
    Option "Emulate3Buttons" "yes"
EndSection
```

您可以配置多个设备；并且可能存在多个 `InputDevice` 部分。前面的示例指定了基本键盘和双键 PS/2 鼠标（实际上是戴尔触控板指针）。同时可以使用指定 USB 设备使用的 `InputDevice` 部分（以启用 PS/2 和 USB 指针的鼠标操作），可能如下所示：

```
Section "InputDevice"
    Identifier "Mouse0"
    Driver "mouse"
    Option "Device" "/dev/input/mice"
    Option "Protocol" "IMPS/2"
    Option "Emulate3Buttons" "off"
    Option "ZAxisMapping" "4 5"
EndSection
```

> **注意**
> 
> 如果您更改了计算机的指向设备，则应随后运行 Fedora 的 system-config-mouse 客户端，该客户端会自动更新系统的 xorg.conf 文件。

> **警告**
> 
> 从 Fedora Core 3 开始，鼠标设备的位置从 /dev/mouse 更改为 /dev/input/mice。不幸的是，当 system-config-display 编写 xorg.conf 文件时，有时会出现一点混淆，仍然将鼠标映射到 /dev/mouse 而不是 /dev/input/mice。这正是需要一点 vi 知识的地方！

### Monitor 部分

Monitor 部分配置在 `ServerLayout` 部分中声明的指定显示设备，如下例所示：

```
Section "Monitor"
    Identifier "Monitor0"
    VendorName "Monitor Vendor"
    ModelName "Monitor Model"
    DisplaySize 300 220
    HorizSync 31.5-48.5
    VertRefresh 50-70
    Option "dpms"
EndSection
```

请注意，X 服务器会根据此部分中的水平和垂直同步及刷新值自动确定最佳视频时序。如有需要，旧式的 modeline 条目（用于 XFree86 4.0 之前的发行版和服务器）仍可能使用。如果在配置 X 时自动检测到了显示器（见本章后面“配置 X”一节），其定义和功能将从 MonitorsDB 数据库插入到您的 xorg.conf 文件中。此数据库包含超过 600 个显示器，位于 /usr/share/hwdata 目录中。

### Device 部分

Device 部分提供有关计算机使用的视频图形芯片组的详细信息，如下例所示：

```
Section "Device"
    Identifier    "Videocard0"
    Driver        "radeon"
    VendorName    "Videocard vendor"
    BoardName     "ATI Radeon Mobility M6"
EndSection
```

此示例标识安装的显卡使用 ATI Mobility M6 图形芯片组。Driver 条目告诉 Xorg 服务器从 /usr/X11R6/lib/modules/drivers 目录加载 radeon_drv.o 模块。不同的芯片组有不同的选项。例如，这里是 NeoMagic 视频芯片组的条目：

```
Section "Device"
    Identifier    "NeoMagic (laptop/notebook)"
    Driver        "neomagic"
    VendorName    "NeoMagic (laptop/notebook)"
    BoardName     "NeoMagic (laptop/notebook)"
    Option        "externDisp"
    Option        "internDisp"
EndSection
```

在此示例中，Device 部分指定了显卡的驱动程序（neomagic_drv.o）并启用两个芯片组选项（externDisp 和 internDisp），以允许在笔记本电脑的 LCD 屏幕和连接的显示器上显示。

Xorg 服务器支持数百种不同的视频芯片组。如果您配置了 X11 但随后更改了安装的显卡，则需要编辑现有的 Device 部分或使用本章讨论的某个 X 配置工具生成新的 xorg.conf 文件，以反映新显卡的功能。您可以在配套的手册页或 /usr/X11R6/lib/_X11/doc 目录下的 README 文件中找到关于某些芯片组选项的详细信息。您应该查看这些来源以获取有关优化和故障排除的提示。

### Screen 部分

Screen 部分将前面各部分的信息关联起来（使用 Screen0、Device 和 Monitor Identifier 条目）。它还可以为会话指定一个或多个颜色深度和分辨率。以下是一个示例：

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
    EndSubSection
EndSection
```

在此示例中，数千种颜色的颜色深度和 1024×768 的分辨率是默认值，可选分辨率为 800×600 和 640×480。如果显卡和显示器的组合支持，可以使用具有不同颜色深度和分辨率（例如 Depth 24 设置为数百万种颜色）的多个 Display 子部分条目。您还可以使用 DefaultDepth 条目（在示例中为 24，即数百万种颜色）以及特定的颜色深度来标准化安装中的显示深度。

您还可以指定大于显示器或笔记本电脑显示硬件支持的桌面分辨率。此设置在 Display 子部分中称为虚拟分辨率。例如，这允许 800×600 显示在一个 1024×768 的虚拟窗口内平移（即滑动）。

> **注意**
> 
> 如果您的显示器和显卡支持多种分辨率并且设置配置正确，您可以使用键组合 Ctrl+Alt+小键盘+ 或 Ctrl+Alt+小键盘- 在 X 会话期间即时更改分辨率。

### 配置 X

虽然可以使用 Fedora 安装程序在安装期间配置 X，但如果 PC 的显卡未被识别，则可能会出现问题。如果您无法在安装期间配置 X（见第 3 章“安装 Fedora”），请不要指定启动到图形化配置，并跳过安装中的 X 配置部分。请注意，某些安装（例如服务器安装）不需要配置 X 以支持活动的 X 会话，但可能需要安装 X 和相关软件以支持远程用户和客户端。

除了其他工具外，您可以使用以下配置工具来创建可用的 xorg.conf 文件：

