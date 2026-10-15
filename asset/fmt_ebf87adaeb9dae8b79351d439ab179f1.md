
对于 Xorg 来说，最重要的文件是位于 `/etc/X11` 目录中的 `xorg.conf` 配置文件。该文件包含对 X 正确运行至关重要的配置信息，通常在 Fedora 安装期间创建。如果您需要在安装后更改任何内容，应使用 `system-config-display` 应用程序，本章稍后将对此进行介绍。与硬件、监视器、显卡和输入设备相关的信息存储在 `xorg.conf` 文件中，因此，如果您决定在文本编辑器中对其进行修改，请小心！

当然，我们不会让您盲目地去编辑如此重要的文件。让我们看看文件的内容，以便您了解 X 正在寻找什么。`xorg.conf` 文件的组件，即各个部分，指定了 X 会话或服务器布局，以及服务器使用的文件路径名、直接与服务器相关的任何选项、所需的任何可选支持模块、与连接到系统的鼠标和键盘相关的信息、安装的显卡、正在使用的监视器，以及当然 Fedora 使用的分辨率和颜色深度。在该文件的 12 个部分中，以下是基本组件：

- `ServerLayout`——定义显示，定义一个或多个屏幕布局，并命名输入设备。
- `Files`——定义颜色、字体或字体服务器端口号的位置。
- `Module`——告诉 X 服务器加载哪些图形显示支持代码模块。
- `InputDevice`——定义输入设备，如键盘和鼠标；可以使用多个设备。
- `Monitor`——定义任何连接显示的能力；可以使用多个监视器。
- `Device`——定义一个或多个显卡，并指定要启用或禁用的任何可选功能（如果有）。
- `Screen`——定义一个或多个分辨率、颜色深度、可能的默认颜色深度以及其他设置。

以下部分对这些元素提供了简短描述；`xorg.conf` 手册页包含所有选项和用于自定义桌面设置的其他关键字的完整文档。

### ServerLayout 部分

如前所述，`xorg.conf` 文件的 `ServerLayout` 部分定义显示和屏幕布局，并命名输入设备。自动配置的 `xorg.conf` 文件中典型的 `ServerLayout` 部分可能如下所示：

```
Section "ServerLayout"
    Identifier    "single head configuration"
    Screen      0     "Screen0" 0 0
    InputDevice "Mouse0" "CorePointer"
    InputDevice "Keyboard0" "CoreKeyboard"
    InputDevice "DevInputMice" "AlwaysCore"
EndSection
```

在此示例中，使用单个显示（数字指定屏幕位置），并在该会话中使用两个默认输入设备 `Mouse0` 和 `Keyboard0`。

### Files 部分

`xorg.conf` 文件的 `Files` 部分可能如下所示：

```
Section "Files"
RgbPath "/usr/lib/X11/rgb"
FontPath "unix/:7100"
EndSection
```

此部分列出了可用的会话颜色（通过名称，在文本文件 `rgb.txt` 中）以及到 X 字体服务器的端口号。字体服务器 `xfs` 在启动时开始运行，不需要活动的 X 会话。如果未使用字体服务器，`FontPath` 条目可以改为列出 `/usr/lib/X11/fonts` 目录下的每个字体目录，如下例所示：

```
FontPath "/usr/lib/X11/fonts/100dpi:1"
FontPath "/usr/lib/X11/fonts/misc:1"
FontPath "/usr/lib/X11/fonts/75dpi:1"
FontPath "/usr/lib/X11/fonts/type1:1"
FontPath "/usr/lib/X11/fonts/Speedo"
...
```

这些目录包含在 X 会话期间可供使用的默认压缩字体。您可以使用 `/etc/X11/fs` 目录下名为 `config` 的文件来配置字体服务器。该文件包含字体服务器使用的字体列表或目录。通过在此文件中添加备用服务器条目并重启字体服务器，您可以指定在 X 会话期间使用的远程字体服务器。这有助于集中字体支持并减少本地存储需求（尽管随 Fedora 和 X 安装的近 5,000 种字体仅需 25MB）。

### Module 部分

`xorg.conf` 文件的 `Module` 部分指定为 X 会话加载的可加载模块或驱动程序。此部分可能如下所示：

```
Section "Module"
Load "dbe"
Load "extmod"
Load "fbbdevhw"
Load "glx"
Load "record"
Load "freetype"
Load "type1"
Load "dri"
EndSection
```

这些模块的范围可以从特殊的视频卡支持到字体光栅化器。模块位于 `/usr/lib/modules` 目录下的子目录中。

### InputDevice 部分

`InputDevice` 部分配置特定设备，如键盘或鼠标，如下例所示：

```
Section  "InputDevice"
    Identifier  "Keyboard0"
    Driver      "kbd"

    Option      "XkbModel"  "pc105"
    Option      "XkbLayout" "us"
EndSection
Section  "InputDevice"
    Identifier  "Mouse0"
    Driver      "mouse"
    Option      "Protocol"  "IMPS/2"
    Option      "Device"  "/dev/input/mice"
    Option      "ZAxisMapping" "4 5"
    Option      "Emulate3Buttons" "yes"
EndSection
```

您可以配置多个设备，并且可能存在多个 `InputDevice` 部分。前面的示例指定了一个基本键盘和一个两键 PS/2 鼠标（实际上，是一个戴尔触摸板指针）。指定使用 USB 设备的 `InputDevice` 部分可以同时使用（以启用 PS/2 和 USB 指针的鼠标操作），可能如下所示：

```
Section  "InputDevice"
    Identifier  "Mouse0"
    Driver      "mouse"
    Option      "Device"  "/dev/input/mice"
    Option      "Protocol"  "IMPS/2"
    Option      "Emulate3Buttons" "off"
    Option      "ZAxisMapping" "4 5"
EndSection
```

### 注意

如果您更改了计算机的指向设备，随后应运行 Fedora 的 `system-config鼠标` 客户端，该客户端会自动更新系统的 `xorg.conf` 文件。

## 警告

从 Fedora Core 3 开始，鼠标设备的位置从 `/dev/mouse` 更改为 `/dev/input/mice`。不幸的是，当 `system-config显示器` 写入 `xorg.conf` 文件时，有时会出现一些混乱，仍然将鼠标映射到 `/dev/mouse` 而不是 `/dev/input/mice`。这时候懂一点 `vi` 知识就很有用了！

### 监视器部分

监视器部分配置在 `ServerLayout` 部分中指定的显示设备，如以下示例所示：

```
Section "Monitor"
    Identifier "Monitor0"
    VendorName "Monitor Vendor"
    ModelName "Monitor Model"
    DisplaySize 300 220
    HorizSync 31.5-48.5
    VertRefresh 50-70
    Option "dpm"
EndSection
```

请注意，X 服务器会根据此部分中的水平和垂直同步值以及刷新率自动确定最佳的视频时序。如果需要，旧式的模式行条目（用于 XFree86 4.0 之前的发行版和服务器）可能仍可使用。如果在配置 X 时自动检测到监视器（请参阅本章后面“配置 X”部分），其定义和功能将从 `MonitorsDB` 数据库插入到您的 `xorg.conf` 文件中。此数据库包含 600 多种监视器，位于 `/usr/share/hwdata` 目录中。

### 设备部分

设备部分提供了关于计算机所使用的视频图形芯片组的详细信息，如以下示例所示：

```
Section "Device"
    Identifier "Videocard0"
    Driver "radeon"
    VendorName "Videocard vendor"
    BoardName "ATI Radeon Mobility M6"
EndSection
```
