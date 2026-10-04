
# 第 3 章 逐步安装指南

## [1] 分区磁盘

在此步骤之后，安装程序将继续检测硬件，启动分区器，并显示分区方法屏幕（见图 3-21）。文本分区器中可用的许多选项在图形化分区器中同样可用。本节描述了如何使用文本分区器手动对硬盘进行分区。有关受保护分区的描述，请参阅第 56 页。

![](img/556454b01d95450a92edff64b47580d6_115_1.png)

**图 3-21** 分区方法屏幕

| 这是您当前配置的分区和挂载点的概述。选择一个分区以修改其设置（文件系统、挂载点等），选择空空间以创建分区，或选择一个设备以初始化其分区表。 |
| :--- |
| 引导式分区 |
| 分区帮助 |
| SCSI3 (0,0,0) (sda) - 214.7 GB Vmware, Vmware Virtual S |
| 撤销分区更改 |
| 完成分区并将更改写入磁盘 |
| <返回上页 |

**图 3-22** 分区概述屏幕

### 手动分区

当您在分区方法屏幕（图 3-21）上选择“手动”时，文本分区器会显示分区概述屏幕，该屏幕列出了系统中的硬盘以及这些磁盘上的分区。如果硬盘没有分区，分区器将仅显示有关硬盘的信息（高亮显示）。图 3-22 显示了一个 200+ 兆字节的没有分区（且没有分区）的磁盘。

如果您想设置 RAID，请在继续之前参阅第 73 页。

如果分区概述屏幕显示硬盘上没有分区也没有空空间（如图 3-22 所示），则该硬盘没有分区表：如果显示了至少一个分区或空空间，则磁盘具有分区表，您可以跳过此步骤并继续“在下方创建分区”。

要创建表，高亮显示您想要创建分区表的磁盘并按 `RETURN`。安装程序会询问您是否想在该设备上创建新的分区表，并警告说这样做将破坏磁盘上的所有数据。高亮并按 `RETURN`。安装程序将显示分区磁盘屏幕，显示有一个与磁盘一样大的空空间块的磁盘（图 3-23）。

要创建分区，高亮显示带有 `FREE SPACE`（空空间）的行并按 `RETURN`。分区器询问您想如何使用该空空间；选择“创建新分区”并按 `RETURN`。下一个分区器要求您指定新分区的尺寸。您可以输入百分比（例如 `50%`）或 GB 允许的数字数（例如 `30 GB`）。按 `RETURN`。随后，分区器要求您指定新分区的类型（主或逻辑；见第 31 页），并询问您想在空空间的开头还是结尾创建分区。通常在何处创建分区并不重要。回答完这些每个问题后，按 `RETURN`。分区器随后显示分区设置屏幕（图 3-24）。

要更改分区设置屏幕上的设置，请使用方向键将高亮移动到您想要更改的设置上并按 `RETURN`。分区器将显示一个允许您更改设置的屏幕。

![](img/556454b01d95450a92edff64b47580d6_117_0.png)

**图 3-23** 分区概述屏幕

#### 指定分区类型

“用作”允许您指定文件系统的类型。默认值为 `ext3`，这是大多数文件系统的良好选择。如果您想更改文件系统，高亮显示挂载点并按 `RETURN`。分区器将显示分区设置屏幕（图 3-24）。

#### 指定挂载点

挂载点允许您为该分区指定挂载点。如果您留空所有条目未标记，安装程序将使用 root。

![](img/556454b01d95450a92edff64b47580d6_117_1.png)

**图 3-24** 分区设置屏幕

#### 启动标志

您需要更改的另一个设置是启动标志。如果您留空未标记，安装程序会将该分区标记为可启动。

![](img/556454b01d95450a92edff64b47580d6_118_0.png)

**图 3-25** 如何使用此分区屏幕

| | 分区磁盘 |
| :--- | :--- |
| 这是您当前配置的分区和挂载点的概述。选择一个分区以修改其设置（文件系统、挂载点等），选择空空间以创建分区，或选择一个设备以初始化其分区表。 | |
| 引导式分区 | |
| 分区帮助 | |
| SCSI3 (0,0,0) (sda) - 214.7 GB Vmware, Vmware Virtual S | |
| 撤销分区更改 | |
| 完成分区并将更改写入磁盘 | |
| <返回上页 | |
| 配置软件 RAID | |
| SCSI3 (0,0,0) (sda) - 214.7 GB Vmware, Vmware Virtual S | |
| # primary 100.0 GB raid | |
| pr/log 114.7 GB FREE SPACE | |
| SCSI3 (0,1,0) (sdb) - 214.7 GB Vmware, Vmware Virtual S | |
| # primary 100.0 GB raid | |
| pr/log 114.7 GB FREE SPACE | |

**图 3-27** 设置 RAID 的分区器

![](img/556454b01d95450a92edff64b47580d6_122_0.png)

**图 3-28** 指定软件 RAID，按 `RETURN` 键，并确认你是否要将更改写入硬盘。从下一个屏幕开始，选择 **Create MD**（MD 代表多磁盘）并按 `RETURN` 键。然后选择 RAID 0、1 或 5。第 35 页描述了不同类型的 RAID 阵列。分区器要求你指定 RAID 阵列中活动设备的数量 (2) 和空间的数量 (0)。分区器在这些字段中输入的值通常是正确的。接下来选择用于 RAID 阵列的活动设备（使用空格键为每个设备选择一个星号；图 3-28）并按 `RETURN` 键。

从下一个屏幕（再次询问是否要创建 MD 设备的屏幕）中选择 **Select From** 并按 `RETURN` 键。现在你需要告诉安装程序挂载 RAID 阵列的位置。突出 RAID 阵列。在示例中，这一行 **100.0 GB FREE SPACE**（此行在图 3-29 中突出显示，但在分区创建后显示）。按 `RETURN` 键。如果 RAID 阵列不包含 FREE SPACE 字样且未显示分区，突出 RAID 阵列行，按 `RETURN` 键，突出 **Delete** 分区并按 `RETURN` 键。RAID 阵列行现在应该包含 **FREE SPACE**。按照第 70 页“创建分区”下的其他说明设置此分区。在示例中，100 GB 被挂载在 `/home` 上的 ext3 文件系统使用。

要完成此操作，请使用第一块硬盘上的剩余空空间创建一个可引导的 `/root` 分区，并在第二个设备上创建一个 4 GB 的交换空间分区。图 3-29 显示了包含这些更改的分区概述屏幕。突出 **Finishing and write changes to disk** 并按 `RETURN` 键。

| 分区磁盘 | |
| :--- | :--- |
| 这是你当前配置的分区和挂载点的概述。选择分区以修改其设置（文件系统、挂载点等）、选择空闲空间以创建分区，或选择设备以初始化其分区表。 | |
| 配置软件 RAID | |
| 引导式分区 | |
| 关于分区的帮助 | |
| RAID1 设备 #0 - 100.0 GB 软件 RAID 设备 | |
| #1 100.0 GB 2513 | |
| SCSI:(0,0,0) - 214.7 GB ATA QEMU HARDDISK | |
| #primary 100.0 GB K raid | |
| #primary 114.7 GB B f ext | |
| SCSI:(0,1,0) - 214.7 GB ATA QEMU HARDDISK | |
| #primary 100.0 GB K raid | |
| #2 4.0 GB f swap | |
| prl/log 110.7 GB FREE SPACE | |
| 撤销分区的更改 | |
| 完成分区并将更改写入磁盘 | |
| <返回> | |

**图 3-29** 完成的分区表

## X 窗口系统

如果你正在安装如 GNOME 这样的图形桌面环境，那么在安装 Ubuntu 时，你会安装 X 窗口系统的 X.org (x.org 和 freedktop.org) 实现。X 窗口系统版本 X11R7.2 包含了几乎 50 个软件包。X 配置文件保存在 `/etc/X11` 中；引导初始设置的配置文件是 `/etc/X11/xorg.conf`。你可以使用“屏幕和图形偏好”窗口（下文将讨论）图形化地配置 `xorg.conf`，或者使用文本编辑器手动编辑它（第 77 页）。

### displayconfig-gtk: 配置显示

一旦安装了（图形化）系统，“屏幕和图形偏好”窗口（下一页第 30–30 页）将允许你配置 X.org，识别显示器类型和视频（图形）卡。要显示此项，选择 **Main menu: System:Administration:Screens** 和 **Graphics**，或从终端模拟器或运行应用程序窗口 (ALT-F2) 输入命令 `gksudo displayconfig-gtk`。此实用程序修改 `xorg.conf` 文件。

#### 备份 xorg.conf

> **提示** 在你对 `/etc/X11/xorg.conf` 进行更改之前（无论是图形化还是手动），请为该文件创建一个备份副本。如果你在图形界面上遇到问题，可以使系统进入恢复模式（第 512 页），将备份覆盖到新的 `xorg.conf`，并重启系统。

指定显示器。“屏幕和图形偏好”窗口的“屏幕”（Screen）选项卡允许你指定一个或两个显示器的型号、分辨率和频率。如果你指定了显示器，它将允许你指定其中一个作为主显示器，并描述两个显示器的空间关系。点击窗口左侧的 **Screen 1** 来指定一个显示器的特性；点击 **Screen 2** 来指定另一个。如果只有一个显示器，点击其中一个显示器的单选按钮 **Disabled**。

通常情况下，系统会探测显示器。

![](img/556454b01d95450a92edff64b47580d6_122_0.png)

**图 3-30** “屏幕和图形偏好”窗口，“屏幕”选项卡

其中 `id_name` 是设备的唯一名称，`drv_name` 是用于该设备的驱动程序。`displayconfig-gtk` 工具通常创建多个 Device（设备）部分。

以下部分定义了一个名为 `Keyboard0` 的键盘，它使用 `kbd` 驱动。键盘模型为 105 键 PC 键盘。如果您使用的是美国微软 自然键盘，可以将 `pc105` 改为 `microsoft`，尽管差异微乎其微。

```conf
Section "InputDevice"
Identifier "Keyboard0"
Driver "kbd"
Option "XkbModel" "pc105"
Option "XkbLayout" "us"
EndSection
```

若要更改键盘支持的语言，请更改 `XkbLayout` 选项的参数，例如改为 `fr` 代表法语。

下一个 `InputDevice` 部分定义了一个名为 `Mouse0` 的鼠标，它使用 `mouse` 驱动。`Device` 选项指定了一个 PS2 设备。`ZAxisMapping` 选项将 Z 轴（鼠标轮）映射到虚拟鼠标 4 和 5，用于滚动窗口。更多信息请参阅第 258 页的“重映射鼠标按钮”。当设置为 `YES` 时，`Emulate3Buttons` 允许双键鼠标的用户通过同时按下两个按钮来模拟三键鼠标。

```conf
Section "InputDevice"
Identifier "Mouse0"
Driver "mouse"
Option "Protocol" "IMPS/2"
Option "Device" "/dev/psaux"
Option "ZAxisMapping" "4 5"
Option "Emulate3Buttons" "no"
EndSection
```

下一个 `InputDevice` 部分与上一个类似，`Device` 选项指定了一个 USB 鼠标。关于此选项的讨论，请参阅第 78 页的“ServerLayout Section”。

```conf
Section "InputDevice"
## 如果普通的 CorePointer 鼠标不是 USB 鼠标，则
# 此输入设备可以在 AlwaysCore 模式下使用，以便您
## 同时使用鼠标。
Identifier "DevInputMice"
Driver "mouse"
Option "Protocol" "IMPS/2"
Option "Device" "/dev/input/mice"
Option "ZAxisMapping" "4 5"
Option "Emulate3Buttons" "no"
EndSection
```

### Monitor SECTION

`xorg.conf` 文件必须至少包含一个 Monitor（显示器）部分。设置此部分最简单的方法是使用 `displayconfig-gtk` 工具，它可以通过探测自动确定显示器类型，或者允许您从显示器列表中选择类型。

不要猜测 `HorizSync` 或 `VertRefresh` 的值。如果您手动配置 Monitor，请猜测扫描率（`HorizSync` 和 `VertRefresh`）。在较旧的显示器上，选择过高的扫描率可能会损坏硬件。以下部分定义了一个名为 `Monitor0` 的显示器。`VendorName` 和 `ModelName` 仅供参考，不影响系统运行。可选的 `DisplaySize` 指定了屏幕以毫米为单位的高度和宽度，允许 X 计算显示器的 dpi（每英寸点数）。`HorizSync` 和 `VertRefresh` 指定了显示器垂直刷新和水平同步的范围；这些值可以从制造商获得。`Option` 选项指定显示器符合 DPMS（第 103 页）标准（即具有内置节能功能）。

| Section | |
| :--- | :--- |
| Identifier | "Monitor0" |
| VendorName | "Monitor" |
| ModelName | "Dell D1" |
| DisplaySize | 360x290 |
| HorizSync | 31.0 - 70.0 |
| VertRefresh | 50.0 - 120.0 |
| Option | "dpms" |

Monitor 部分可以定义 DDC（显示数据通道）；显示器可以使用 DDC 向显卡通报其属性。如果您忽略或注释掉 `HorizSync` 和 `VertRefresh` 行，X 将使用 DDC 探测来确定恰当的值。

### Device SECTION

`xorg.conf` 文件必须至少包含一个 Device（设备）部分，以指定系统中的显卡类型。`VendorName` 和 `BoardName` 仅供参考，不影响。设置此部分最简单的方法是使用 `displayconfig-gtk` 工具，它通常通过探测来确定显卡类型。以下 Device 部分指定 `Videocard0` 使用 `nv` 驱动并在 PCI 总线上定位它：

| Section | |
| :--- | :--- |
| Identifier | "Videocard" |
| Driver | "nv" |
| VendorName | "Videocard vendor" |
| BoardName | "NVIDIA GeForce4 (generic)" |
| BusID | "PCI:3:0" |

### Screen SECTION

`xorg.conf` 文件必须包含至少一个 Screen（屏幕）部分。该部分将 Device 部分中指定的显卡绑定到 Monitor 部分指定的显示器。以下 Screen 部分指定 `Screen0` 由 `Video0` 和 `Monitor0` 组成，两者都在文件的其他地方定义。`DefaultDepth` 指定了默认色彩深（第 102 页），`Display` 子部分可以覆盖它。每个 Screen 部分必须至少有一个 Display 子部分。后续示例中的子部分指定了色彩深度和三种 Modes（模式）。`Modes` 指定了以每英寸点（dpi）为单位的屏幕分辨率。第一个 Mode 是默认模式；您可以在 X 运行时使用 `CTRL-ALT-.` 在 Modes 之间切换。在输入命令时必须使用数字键上的加号或减号。X 会忽略无效的 Modes。

```conf
Section "Screen" "Screen0"
Device "Video0"
Monitor "Monitor0"
DefaultDepth 24
Subsection "Display"
Depth 24
Modes "1024x768" "800x600" "640x480"
EndSection
```

如果您忽略或注释掉 `Depth` 和 `Modes` 行，X 将使用 DDC 探测来确定最佳值。

### MULTIPLE MONITORS
