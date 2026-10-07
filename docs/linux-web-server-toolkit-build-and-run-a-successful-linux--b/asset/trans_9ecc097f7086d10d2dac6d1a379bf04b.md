

# Linux Web 服务器工具包

（在 PC 上）用于模拟三键鼠标的某些功能（UNIX 工作站上常见）。该节如下：

| 节指针 |
|---|---|
| 协议 Microsoft |
| 设备 /dev/mouse |
| 节结束 |

# THE XF86CONFIG 显示器部分

在 XF86Config 的这一部分，事情开始变得复杂。Monitor（显示器）部分包含一个或多个显示器的定义，包括标识符、厂商名称、型号以及之前提到的所有频率值。

显示器部分最重要的部分是 ModeLines（模式行）。这一系列行定义了通过指定水平和垂直扫描的定时值，如何在显示器上创建特定的分辨率。问题在于，你不能凭空编写这些内容。如果你无法让配置工具为你创建它们，你应该在互联网上寻找一个使用与你显示器型号相同的示例文件。从该配置文件中复制 Monitor 部分并将其插入到你的文件中。

每个 ModeLine 都有一个名称，通常是分辨率，也可以是任何内容（注意它在引号中）。dotclock（点时钟）指定了该行使用的定时基准，用于生成创建该分辨率所需的水平和垂直定时值。每张显卡都可以生成特定的 dotclocks，如下一节所示。

如果你正确设置了 ModeLines，就不会损坏你的显示器，因为 X 服务器不会向显示器发送任何此处未列出的可行选项的内容。该节如下：

| Section Monitor Primary Monitor |
|---|---|
| Identifier Unknown |
| VendorName Unknown |
| Model | |
| HorSync 31.5-64.3 |
| VertRefresh 50-90 |
| Modeline 1152x864 64.97 1152 1168 1384 1480 864 865 875 985 interlace |
| Modeline 1024x768 75.00 1024 1048 1184 1238 768 771 777 806 |
| -hync -vsync |
| Modeline 800x600 50.35 800 856 976 1040 600 637 643 666 |
| +hync +vsync |
| Modeline 640x480 31.48 640 680 720 864 460 488 491 521 |
| EndSection |

Monitor 部分可以定义多个显示器。这就是为什么每个显示器都有一个标识符行。Screen（屏幕）部分（本章后文的“The XF86Config Screen section”）随后可以通过名称引用特定的显示器。这为你的系统支持多个硬件选项提供了一些灵活性。

# 第 5 章：安装 Linux

# THE XF86CONFIG 设备部分

XF86Config 的 Device（设备）部分定义了你正在使用的显卡。与 Monitor 部分一样，你可以定义多张显卡，然后指定其中一张作为目标来创建一个显示部分（section）。

Device 部分包含了许多与 Monitor 部分相同的行，例如厂商和型号名称。但 Device 部分还包含了几个关键选项，如下，这些选项在输入时可能具有挑战性：

- Chipset：这是作为显卡大脑的视频芯片类型。常见的高端视频芯片有 ET4000、S3 和 Cirrus Logic。你可以通过查看实际板卡或阅读规格表查看芯片组。
- VideoRam：这一行告诉你显卡上有多少千字节（KB）的内存。如果你的显卡有 2MB 内存，这一行的数字将是 2048。
- Clocks：这一行列出了显卡可以生成的所有 dotclocks。这是唯一真正困难的一行。你通常从配置工具或你显卡的规格表中获取这些值。你可以运行带有 `-probe` 选项的 X 来尝试获取显卡的时钟列表。

时钟值必须非常精确地列出小数值，并按正确的顺序排列——它们不是从低到高排列的！

- Options：这一行包含针对特定卡或芯片组的选项。这些选项由 X 服务器针对该特定卡进行解释。与 Pointer（指针）部分中的鼠标选项一样，除非你的特定显卡的文档指示要求，否则不要添加任何内容。

该节如下（注意此部分因系统而异）：

| Identifier | Primary Card |
|---|---|
| VendorName | Unknown |
| BoardName | None |
| Chipset | et4000w32i_rev_b |
| Clocks | 25.17 28.32 32.48 35.98 40.01 44.89 31.48 37.48 |
| 50.35 56.66 64.97 72.00 80.05 89.82 62.99 75.00 |

# THE XF86CONFIG 屏幕部分

这是 XF86Config 中你实际上在屏幕上显示内容的部分。它结合了其他部分的信息来定义屏幕上显示的内容。

# Linux Web 服务器工具包

在 Screen 部分中，可以为每个分辨率定义子部分。Screen 部分包含以下行：

- Driver：用于此屏幕的 X 服务器；对于每个驱动程序都可能有一个 Screen 部分，例如 Accel、VGA16 和 SVGA。这允许你在无需重新配置的情况下使用不同的驱动程序。
- Device：用于此屏幕的显卡定义的标识符字符串。
- Monitor：用于此屏幕的显示器定义的标识符字符串。
- Subsection "Display"：用于多个分辨率设置——每个 "Display" 包含：
- Depth：每个像素的位数（深度为 8 表示位深度颜色）。
- Modes：之前提到的 Monitor 定义中列出的行（当你使用时，这些是支持分辨率列表）。
- View：虚拟桌面的坐标。
- Virtual：虚拟桌面的大小——只要你有足够的显存就可以定义虚拟桌面。

该节如下：

| Screen Driver | Accel |
|---|---|
| Device | Primary Card |
| Monitor | Primary Monitor |
| Subsection | Display |
| Depth | 8 |
| Modes | 1152x864 64.97 1152 1168 1384 1480 864 865 875 985 |
| EndSection | Display |
| Depth | 15 |
| Modes | 1024x768 75.00 1024 1048 1184 1238 768 771 777 806 |
| EndSection | Display |
| Depth | 16 |
| Modes | 800x600 50.35 800 856 976 1040 600 637 643 666 |
| EndSection | |

# 第 5 章：安装 Linux

```
Subsection Display
Depth 24
Modes 1152x864 1024x768 800x600
EndSubsection
Subsection Display
Depth 32
Modes 640x480
EndSubsection
EndSection
```

本节解释了如何配置图形界面以使用桌面和其他图形工具。下一节通过引导你设置网络连接来完成 OpenLinux 的基础配置。

# 使用你的网络连接

在你安装并运行 OpenLinux 系统后，你就可以开始考虑连接其他计算机和互联网。如果你已经连接到带有互联网连接的本地网络，那么使用浏览器查看你喜爱的页面就是件简单的事。

你在安装过程中输入的网络信息被用于创建所有必要的配置文件，以确保你的网络连接正常工作。当然，事情并不总是按计划进行。

系统的网络配置由几个简单的部分组成。当你尝试访问网络系统时，如果不符合预期，可以从检查表 5–4 列出的项目开始。

存储网络配置信息的文件

| 文件名 | 用途 |
|---|---|
| /etc/hosts | 列你想连接的计算机的主机和 IP 地址。文件通常列出 localhost、你的 IP 地址，可能还有其他重要的机器。DNS 名称服务器用于查找其他系统，但在无法访问名称服务器时会使用此文件。 |
| /etc/networks | 列出你希望为了方便访问的网络地址和关联域名。 |
| /etc/resol.conf | 提供用于查找域名的名称服务器名称和 IP 地址。 |
| /etc/hostname | 提供此计算机的主机名。 |

