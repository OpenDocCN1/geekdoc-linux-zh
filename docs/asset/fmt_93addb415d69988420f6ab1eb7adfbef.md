
| `HorizSync` | 30-60 |

| `VerRefresh` | 50-90 |

| #Modes: | 名称 点钟 | 水平计时 | 垂直计时 |

| `ModelLine` | 640x480* | 25 | 640 672 768 800 | 480 492 525 |

| `ModelLine` | 800x600* | 36 | 800 840 912 1024 | 600 600 625 |

| `ModelLine` | 1024x768* | 45 | 1024 1028 1224 1264 | 768 776 818 836 |

你的显示器部分可以有多个定义，因此对于每个显示器，你必须提供表 21.7 所示的信息。

### 表 21.7 显示器部分选项

| 选项 | 说明 |
| :--- | :--- |
| `Identifier` string | 显示器标识符字符串。 |
| `VendorName` string | 标识制造商。 |
| `ModelName` string | 标识名称和型号。 |
| `Bandwidth` value | 显示器的带宽。 |
| `HorizSync` range | 有效水平同步频率（kHz）。如果你有多同步显示器，这可以是一个范围；对于固定频率显示器，则是一系列单值。 |
| `VertRefresh` range | 指定垂直刷新频率。它们可以像 `HorizSync` 值一样，列为一个范围或一系列单值。 |
| `Gamma` value | 你的显示器的伽马校正值。 |
| `ModelLine` values | 指定在显示器上显示的每个分辨率对应的一系列值。 |

对于每个分辨率，你都需要显示器部分需要一个 `ModelLine` 条目。该条目的格式如下：

```
ModelLine "name" dotclock Horizontal Freq Vertical Freq
```

水平和垂直频率是一组以 kHz 为单位的四个值。你可以通过运行 `x86Config` 程序（将在本节的“运行 `x86Config` 程序”部分讨论）或从 XFree86 软件包随附的各种文档文件中获取大多数值。对于初始测试，最好输入一个标准配置，然后探测你的系统以获取更合适的值。

**设备部分（The Device Section）** 设备部分向 XFree86 描述你的系统的显卡。标准 VGA 的设备部分如下：

- Section "Device"
- Identifier "SVGA"
- VendorName "Trident"

![](img/c03a7f3ab2607b66f899c70357fa9e7e_462_0.png)

# 第 21 章 安装 Windows 系统

`BoardName` `TVG89`

`Chipset` `tvga8900c`

`VideoRam` 1024

`Clocks` 25.30 28.32 45.00 36.00 57.30 65.10 50.40 39.90

`Option`

`EndSection`

唯一可能难以获得的是时钟值。你的显卡使用这些值来产生时钟信号，从而提供在显示器上显示信息所需的频率。如果你获取的这些值完全错误，可能会烧毁你的显示器！你可以通过以下方式获取此值：运行 `x86Config` 程序（在后文的“运行 `x86Config` 程序”部分讨论）或从 XFree86 软件包随附的各种文档文件中获取。对于初始测试，最好输入一个标准配置，然后探测你的系统以获取更合适的值。

**显示器部分（The Monitor Section）** 显示器可能是 XF86Config 文件中最重要的部分——也是最危险的部分。此文件中的错误信息可能会对系统造成灾难性的破坏，请务必小心！

`SuperProbe` 程序和制造商文档将极大有助于创建这一部分。你也可以使用文件 `/usr/X11R6/lib/X11/doc/modesDB.txt` 和 `/usr/X11R6/lib/X11/doc/monitors` 来查找关于你特定显示器的信息。

一个典型的显示器部分如下：

- Section 'Monitor'
- Identifier "Sanyo 1450 NI"
- VendorName "Sanyo"

## 配置 XFree86 435

| `ModelName` | 我的 14 英寸显示器* |
| :--- | :--- |
| `Bandwidth` | 60 |
| `HorizSync` | 30-60 |
| `VerRefresh` | 50-90 |
| #Modes: | 名称 点钟 | 水平计时 | 垂直计时 |
| `ModelLine` | 640x480* | 25 | 640 672 768 800 | 480 492 525 |
| `ModelLine` | 800x600* | 36 | 800 840 912 1024 | 600 600 625 |
| `ModelLine` | 1024x768* | 45 | 1024 1028 1224 1264 | 768 776 818 836 |

你的显示器部分可以有多个定义，因此对于每个显示器，你必须提供表 21.7 所示的信息。

### 表 21.7 显示器部分选项

| 选项 | 说明 |
| :--- | :--- |
| `Identifier` string | 显示器标识符字符串。 |
| `VendorName` string | 标识制造商。 |
| `ModelName` string | 标识名称和型号。 |
| `Bandwidth` value | 显示器的带宽。 |
| `HorizSync` range | 有效水平同步频率（kHz）。如果你有多同步显示器，这可以是一个范围；对于固定频率显示器，则是一系列单值。 |
| `VertRefresh` range | 指定垂直刷新频率。它们可以像 `HorizSync` 值一样，列为一个范围或一系列单值。 |
| `Gamma` value | 你的显示器的伽马校正值。 |
| `ModelLine` values | 指定在显示器上显示的每个分辨率对应的一系列值。 |

对于每个分辨率，你都需要显示器部分需要一个 `ModelLine` 条目。该条目的格式如下：

```
ModelLine "name" dotclock Horizontal Freq Vertical Freq
```

水平和垂直频率是一组以 kHz 为单位的四个值。你可以通过运行 `x86Config` 程序（将在本节的“运行 `x86Config` 程序”部分讨论）或从 XFree86 软件包随附的各种文档文件中获取大多数值。对于初始测试，最好输入一个标准配置，然后探测你的系统以获取更合适的值。

**设备部分（The Device Section）** 设备部分向 XFree86 描述你的系统的显卡。标准 VGA 的设备部分如下：

- Section "Device"
- Identifier "SVGA"
- VendorName "Trident"

![](img/c03a7f3ab2607b66f899c70357fa9e7e_462_0.png)

# 第 21 章 安装 Windows 系统

`BoardName` `TVG89`

`Chipset` `tvga8900c`

`VideoRam` 1024

`Clocks` 25.30 28.32 45.00 36.00 57.30 65.10 50.40 39.90

`Option`

`EndSection`

唯一可能难以获得的是时钟值。你的显卡使用这些值来产生时钟信号，从而提供在显示器上显示信息所需的频率。如果你获取的这些值完全错误，可能会烧毁你的显示器！你可以通过以下方式获取此值：运行 `x86Config` 程序（在后文的“运行 `x86Config` 程序”部分讨论）或从 XFree86 软件包随附的各种文档文件中获取。对于初始测试，最好输入一个标准配置，然后探测你的系统以获取更合适的值。

**显示器部分（The Monitor Section）** 显示器可能是 XF86Config 文件中最重要的部分——也是最危险的部分。此文件中的错误信息可能会对系统造成灾难性的破坏，请务必小心！

`SuperProbe` 程序和制造商文档将极大有助于创建这一部分。你也可以使用文件 `/usr/X11R6/lib/X11/doc/modesDB.txt` 和 `/usr/X11R6/lib/X11/doc/monitors` 来查找关于你特定显示器的器信息。

一个典型的显示器部分如下：

- Section 'Monitor'
- Identifier "Sanyo 1450 NI"
- VendorName "Sanyo"

## 配置 XFree86 435

| `ModelName` | 我的 14 英寸显示器* |
| :--- | :--- |
| `Bandwidth` | 60 |
| `HorizSync` | 30-60 |
| `VerRefresh` | 50-90 |
| #Modes: | 名称 点钟 | 水平计时 | 垂直计时 |
| `ModelLine` | 640x480* | 25 | 640 672 768 800 | 480 492 525 |
