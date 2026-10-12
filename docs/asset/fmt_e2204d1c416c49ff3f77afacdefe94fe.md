
取消你想要激活的任何指令的注释；如果你不想激活它们，请保留其注释状态（这是通常的默认状态）。示例中的指令效果如表 12.3 所示。

| 表 12.3: 模块指令 |
| 指令 | 效果 |
| --- | --- |
| `Load "dbe"` | 加载双缓冲扩展（Double Buffer Extensions），允许将连续图像加载到不同的缓冲区。 |
| `Option "omit XFree86-DGA"` | 禁用直接图形访问（Direct Graphics Access）扩展。 |
| `Load "type1"` | 加载 PostScript type1 字体模块。 |
| `Load "freetype"` | 加载命名的 TrueType 克隆程序 |

其他扩展模块可以在 `/usr/X11R6/lib/modules/extensions` 目录下找到。

# 输入Device — 键盘

`InputDevice` 节指定指针（鼠标）和键盘。虽然 `InputDevice` 是 `XFree86` 4 版本的默认设置，但旧的 `Keyboard` 和 `Pointer` 模块仍然可以使用。通常，有两个 `InputDevice` 节：每个键盘和每个指向设备各一个。

正如你预期的那样，其中一个 `InputDevice` 节指定了与键盘运行相关的信息，包括键盘类型和协议。虽然该节不再作为默认值使用，但 `XFree86` 4 版本仍然能识别它。尽管 Red Hat Linux 7.1 使用 `XFree86` 4 版本，但键盘和 `Pointer` 节（而非 `InputDevice`）是 Red Hat Linux 7.1 默认 `XF86Config` 配置文件的一部分。这里显示了一个没有注释的典型 `InputDevice` 节：

```
Section "InputDevice"
# Option "Protocol" "Xqueue"
# Identifier "Keyboard1"
# Driver "keyboard"
# Option "AutoRepeat" "500 5"
# Option "XkbDisable"
# Option "Xleds" "1 2 3"
# Option "LeftAlt" "Meta"
# Option "RightAlt" "ModeShift"
# Option "RightCtl" "Control"
# Option "ScrollLock" "Compose"
# Option "XkbDisable"
# Option "XkbModel" "pc101"
# Option "XkbModel" "pc102"
# Option "XkbModel" "pc104"
# Option "XkbModel" "pc105"
# Option "XkbModel" "pc106"
# Option "XkbModel" "microsoft"
# Option "XkbLayout" "us"
# Option "XkbLayout" "de"
# Option "XkbVariant" "nodeadays"
# Option "XkbOptions" "ctrl:swapcaps"
# Option "XkbRules" "xfree86"
# Option "Xkbkeymap" "xfree86(us)"
EndSection
```

这看起来是一个复杂的节，但正如表 12.4 描述的，它实际上简单。

# 表 12.4: 键盘指令

| 指令 | 效果 |
| --- | --- |
| `"Protocol" "Xqueue"` | `Xqueue` 协议用于各种 Sun Solaris 服务器 (`SRV3`, `SRV4`)。如果缺少此行，`XFree86` 默认使用 `Standard`，它适用于所有其他系统。 |
| `Identifier`, `Driver` | 管理员分配给键盘和键盘驱动程序的名称。 |
| `AutoRepeat` | 该指令用于指定在按下按键后开始自动重复前等待多久，以及按键重复的频率。所有值单位均为毫秒。在上一个示例中，`AutoRepeat:500` 表示按键按住 500 毫秒（半秒）后开始自动重复，然后按键每隔 5 毫秒重复一次。 |
| `Xeds` | 该指令指定用户可以使用 `xset` 命令控制哪些键盘 LED 灯（例如 `Num Lock` 和 `Caps Lock`）。 |
| `LeftAlt`, `RightAlt`, `RightCtl`, and `ScrollLock` | 最初在 Unix 工作站上的 Windows 键盘与标准 PC 键盘有明显区别。这些键盘包括 `Meta`、`ModeShift` 等特殊键， |

# 显示器

到目前为止，你看到的配置指令大部分是自明易懂且不易于使用的。对于连接到计算机的每个显示器，你需要一个独立的 `Monitor` 节。考虑以下示例 `Monitor` 节：

```
Section "Monitor"
Identifier "monitor"
VendorName "LG"
ModelName "StudioWorks"
HorizSync 30-70
VertRefresh 50-160
EndSection
```

表 12.6 描述了 `Monitor` 节的各种指令。

# 表 12.6：显示器指令

| 指令 | 解释 |
| --- | --- |
| `Identifier` | 此指令使用用户指定的名称来标识显示器的规格，该名称在 `XF86Config` 文件的其他部分用于引用该显示器。 |
| `VendorName` | 此指令用于标识所定义的显示器厂商。此值对 `XFree86` 的运行没有影响，因此最好分配一个有意义的值，以便您在日后识别该定义。 |
| `ModelName` | 此指令用于标识所定义的显示器型号。此值对 `XFree86` 的运行没有影响，因此最好分配一个有意义的值，以便您在日后识别该定义。 |
| `HorizSync` | 此指令指定您的显示器的水平同步频率（单位为 kHz）。您可以像示例中那样指定一个范围，或者在列表中提供一组离散值，并用逗号隔开各个范围（例如， 15-25, 30-50）。请务必查阅您的显示器文档并为您的显示器提供正确的值。如果您在此处输入错误的值，可能会破坏或损坏您的显示器。 |
| `VertRefresh` | 此指令指定您的显示器支持的垂直刷新率（单位为 Hz）。您可以像示例中那样指定一个范围，或者在列表中提供一组离散值，并用逗号隔开数值（例如， 40-50, 80-100）。请务必查阅您的显示器文档并为您的显示器提供正确的值。如果您在此处输入错误的值，可能会破坏或损坏您的显示器。 |

# Modes（模式）

对于连接到计算机的每一个显示器，您都需要一个独立的 `Modes` 部分。考虑以下示例 `Modes` 部分：

```
Section "Modes"
Identifier "Modes [0]"
line "640x480" 46.02 640 656 760 832 480 490 498 522
line "800x600" 71.91 800 808 928 1000 600 612 622 632
line "1024x768" 117.53 1024 1088 1208 1360 768 783 829
line "1600x1200" 200 1600 1616 1968 2080 1200 1200 1212 1253
EndSection
```

Modelines（模式行）指定了您的显示器可能的模式。`Modes` 将分辨率、点时钟（dot clock）和时序结合，以确定如何显示到显示器。`X` 服务器在尝试加载时会删除 `X86Config` 文件中发现的任何不兼容模式。然而，要获取这些行的正确信息是非常困难的。通常，最好让您的 `XFree86` 配置软件为您创建这些行，而不是对它们进行修改。

如果您有多个显示器，最好将 `Modes` 信息整合到对应的 `Monitor` 部分中，以避免混淆。

表 12.7 描述了第一行 Modeline 中每个数字从左到右的功能。

# 表 12.7：Modeline 项目

| 项目 | 解释 |
| --- | --- |
| `640x480` | 像素单位屏幕分辨率 |
| `46.02` | 点时钟，单位为 MHz |
| `640` | 显示的水平像素 |
| `656` | 水平同步开始 |
| `760` | 水平同步结束 |
| `832` | 水平同步总和 |
| `480` | 显示的垂直像素 |
| `490` | 垂直同步开始 |
| `498` | 垂直同步结束 |
| `522` | 垂直同步总和 |

表示第一行 Modeline 的另一种方式 `Modeline "640x480" 46.02 640 656 760 832 480 490 498 522` 如下：

```
Mode                640x480
DotClock            46.02
HTimings            640 656 760 832
VTimings            480 490 498 522
EndMode
```
