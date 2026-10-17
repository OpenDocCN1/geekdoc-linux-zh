
进入`/path/to/xxx`目录，找到`xxx.json`。

在表达式`cvar = avar + bvar`中，加法运算符（`+`）将`avar`与`bvar`相加，得到它们的和`cvar`

在`List.of(arg0, arg1, arg2)`中，`List`接口的工厂方法`of()`接受一系列的元素，返回包含它们的只读列表。

之后我们这样调用`cmd`命令：`cmd arg0 arg1 arg2`。

```
if (condVar > someVal) {console.log("xxx")}
```
这是示例文本的重复，实际任务是对以下提供的待排版文本进行处理。

---

以下是根据要求对提供文本的排版结果：

### `lsdev` 命令

```
$ lsdev
Device DMA IRQ I/O Ports
...
acpi 9
ACPI           4000–4003 4004–4005 4008–400b 4020–4021
ahci           d240–d247 d248–d24b d250–d257 d258–d25b
ata_piix       14  15       0170–0177 01f0–01f7 0376–0376 03f6–03f6
cascade        4
dma                     0080–008f
dma1                    0000–001f
dma2                    00c0–00df
e1000                   d010–d017
enp0s3          19
fpu                     00f0–00ff
i8042           1  12
Intel                   d100–d1ff     d200–d23f
keyboard                0060–0060     0064–0064
ohci_hcd:usb1   22
PCI                     0000–0cf7 0cf8–0cff 0d00–ffff
pic1                    0020–0021
pic2                    00a0–00a1
piix4_smbus             4100–4108
rtc0            8        0070–0071
rtc_cmos                  0070–0071
snd_intel8x0    21
timer                     0
timer0                  0040–0043
timer1                  0050–0053
vboxguest       20
vboxvideo       18
vga+                    03c0–03df
$ 
```

这为你提供了一个查看所有运行在系统上的设备的重要信息的地方，使其易于识别任何可能导致问题的冲突。

> **注意** `lsdev` 工具是 `procinfo` 包的一部分。在某些 Linux 发行版中，你可能需要手动安装该包。

## `lsblk` 命令

`lsblk` 命令行命令显示有关安装在 Linux 系统上的块设备的信息。默认情况下，`lsblk` 命令显示所有块设备，如清单 23.6 所示。

### 清单 23.6: `lsblk` 命令的输出

```
$ lsblk
NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT
loop0 7:0 0 34.6M 1 loop /snap/gtk-common-themes/818
loop1 7:1 0 2.2M 1 loop /snap/gnome-calculator/222
...
sda 8:0 0 10G 0 disk
sda1 8:1 0 10G 0 part
ubuntu--vg-root 253:0 0 9G 0 lvm /
ubuntu--vg-swap_1 253:1 0 976M 0 lvm [SWAP]
sr0 11:0 1 1024M 0 rom
$ 
```

如果你注意清单 23.6 的末尾，`lsblk` 命令还会指示相关的块，例如设备映射的 `LVM` 卷和相关的物理硬盘。你可以通过添加命令行选项来修改 `lsblk` 输出，以查看有关块的更多信息。`-S` 选项仅显示系统中 `SCSI` 块设备的信息：

```
$ lsblk -S
NAME HCTL TYPE VENDOR MODEL REV TRAN
sda 2:0:0:0 disk ATA VBOX HARDDISK 1.0 sata
sr0 1:0:0:0 rom VBOX CD-ROM 1.0 ata
$
```

这是查看系统上安装的不同 `SCSI` 驱动器的一种快速方法。

## `dmesg` 命令

内核环形缓冲区记录内核级事件的发生情况。由于它是环形缓冲区，缓冲区区域填满后，事件消息会被覆盖。你可以使用 `dmesg` 命令查看内核环形缓冲区中的当前消息。每当你安装新设备时，监控它都很有帮助，如清单 23.7 所示。

### 清单 23.7: `dmesg` 命令的部分输出

```
[ 2525.499216] usb 1-2: new full-speed USB device number 3 using ohci-pci
[ 2525.791093] usb 1-2: config 1 interface 0 altsetting 0 endpoint 0x1 has invalid maxpacket 512, setting to 64
[ 2525.791107] usb 1-2: config 1 interface 0 altsetting 0 endpoint 0x81 has invalid maxpacket 512, setting to 64
[ 2525.821079] usb 1-2: New USB device found, idVendor=abcd, idProduct=1234
[ 2525.821088] usb 1-2: New USB device strings: Mfr=1, Product=2, SerialNumber=3
[ 2525.821094] usb 1-2: Product: UDisk
[ 2525.821099] usb 1-2: Manufacturer: General
[ 2525.821104] usb 1-2: SerialNumber: [ 2525.927096] usb-storage 1-2:1.0: USB Mass Storage device detected
[ 2525.927096] usb-storage 1-2:1.0: USB Mass Storage device detected
[ 2525.927950] scsi host3: usb-storage 1-2:1.0
[ 2525.928033] usbcore: registered new interface driver usb-storage
[ 2525.940376] usbcore: registered new interface driver uas
[ 2526.961754] scsi 3:0:0:0: Direct-Access General UDisk 5.00 PQ: 0 ANSI: 2
[ 2526.966646] sd 3:0:0:0: Attached scsi generic sg2 type 0
[ 2526.992707] sd 3:0:0:0: [sdb] 31336448 512-byte logical blocks: (16.0 GB/14.9 GiB)
[ 2527.009197] sd 3:0:0:0: [sdb] Write Protect is off
[ 2527.009200] sd 3:0:0:0: [sdb] Mode Sense: 0b 00 00 08
[ 2527.026764] sd 3:0:0:0: [sdb] No Caching mode page found
[ 2527.026770] sd 3:0:0:0: [sdb] Assuming drive cache: write through
[ 2527.127613] sdb: sdb1
[ 2527.229943] sd 3:0:0:0: [sdb] Attached SCSI removable disk
```

`dmesg` 命令的输出显示了内核采取的识别插入系统的新 `USB` 设备的步骤。

由于内核负责检测设备并安装正确的模块，当设备没有正确工作时，`dmesg` 命令是一个很好的故障排除工具。它可以帮助你确定硬件设备模块是否未正确加载。

# 处理 `PCI` 设备

`lspci` 命令允许你查看 Linux 系统上当前安装和识别的 `PCI` 和 `PCIe` 设备。有许多命令行选项可以包含在 `lspci` 命令中以显示有关安装在系统上的 `PCI` 和 `PCIe` 卡的信息。表 23.1 显示了一些常用且实用的选项。

### 表 23.1 `lspci` 的命令行选项

| 选项 | 描述 |
| :--- | :--- |
| `-A` | 定义访问 `PCI` 信息的方法 |
| `-b` | 从卡的角度显示连接信息 |
| `-k` | 显示每个已安装 `PCI` 卡的内核驱动程序模块 |
| `-m` | 以机器可读格式显示信息 |

## 使用 `PCI` 设备

`lspci` 命令用于显示 `PCI` 设备的信息。以下是可用的选项：

- `-n`：以数字形式而非文本形式显示供应商和设备信息
- `-q`：查询集中式 `PCI` 数据库以获取已安装 `PCI` 卡的信息
- `-t`：显示树状图，展示卡与总线之间的连接
- `-v`：显示关于卡的附加信息（详细模式）
- `-x`：显示卡信息的十六进制转储

不带任何选项的 `lspci` 命令输出会显示连接到系统的所有设备，如图 23.8 所示。

### 图 23.8：使用 `lspci` 命令

```text
$ lspci
00:00.0 Host bridge: Intel Corporation 440FX - 82441FX PMC [Natoma] (rev 02)
00:01.0 ISA bridge: Intel Corporation 82371SB PIIX3 ISA [Natoma/Triton II]
00:01.1 IDE interface: Intel Corporation 82371AB/EB/MB PIIX4 IDE (rev 01)
00:02.0 VGA compatible controller: InnoTek Systemberatung Gmbh VirtualBox
   Graphics Adapter
00:03.0 Ethernet controller: Intel Corporation 82540EM Gigabit Ethernet
   Controller (rev 02)
00:04.0 System peripheral: InnoTek Systemberatung Gmbh VirtualBox Guest
   Service
00:05.0 Multimedia audio controller: Intel Corporation 82801AA AC'97 Audio
   Controller (rev 01)
00:06.0 USB controller: Apple Inc. KeyLargo/Intrinsic USB
00:07.0 Bridge: Intel Corporation 82371AB/EB/MB PIIX4 ACPI (rev 08)
00:08.0 SATA controller: Intel Corporation 82801IHR/IHEM (ICH9M/ICH9M-E) SATA
   Controller [AHCI mode] (rev 02)
$
```

您可以使用 `lspci` 命令的输出来排查 `PCI` 卡问题，例如当卡未被 Linux 系统识别时。

## 使用 `USB` 设备

您可以使用 `lsusb` 命令查看连接到您的 Linux 系统的 `USB` 设备的基本信息。表 23.2 展示了该命令可用的选项。

### 表 23.2：`lsusb` 命令选项

| 选项 | 描述 |
| :----- | :---------- |
| `-d` | 仅显示指定供应商 ID 的设备 |
| `-D` | 仅显示具有指定设备文件的设备信息 |
| `-s` | 仅显示使用指定总线的设备信息 |
| `-t` | 以树状格式显示信息，展示相关设备 |
| `-v` | 显示设备的附加信息（详细模式） |
| `-V` | 显示 `lsusb` 程序的版本 |

`lsusb` 程序的基本输出如图 23.9 所示。

### 图 23.9：`lsusb` 输出

```text
$ lsusb
Bus 001 Device 003: ID abcd:1234 Unknown
Bus 001 Device 002: ID 80ee:0021 VirtualBox USB Tablet
Bus 001 Device 001: ID 1d6b:0001 Linux Foundation 1.1 root hub
$
```

大多数系统都集成了标准 `USB` 集线器，用于将多个 `USB` 设备连接到 `USB` 控制器。幸运的是，市场上只有少数几种 `USB` 集线器，因此所有 Linux 发行版都包含了与每个 `USB` 集线器通信所需的设备驱动程序。这保证了您的 Linux 系统至少能检测到 `USB` 设备的连接。

## 支持显示器

两个基本元素控制着 Linux 系统的视频环境：显卡和显示器。为了显示任何类型的文本或图形，您的 Linux 系统必须知道如何与这两者交互。这就是 `X Window System` 软件发挥作用的地方。

`X Window System` 由麻省理工学院（`MIT`）开发，旨在为与显示器交互提供标准协议。由于最后定义的版本是第 11 版，因此 `X Window System` 通常简称为 `X` 或 `X11`。

`X11` 系统运行在 Linux 系统的图形桌面环境之下，如图 23.1 所示。

### 图 23.1：标准的 Linux 图形环境

![](img/c0a399aca0d18f8822d714ad0a173123_722_0.png)

`X11` 的职责是与您系统视频环境的硬件层面（显卡、显示器、键盘和鼠标）进行交互，并提供一个标准接口，供任何桌面管理软件（如 `KDE` 或 `GNOME`）使用。正因为如此，`X11` 软件必须能够与所有这些硬件设备进行交互。

Linux 最初的 `X11` 软件是 `XFree86` 软件包。它因难以配置且难以在不同的视频硬件类型上正常工作而闻名。因此，出现了较新的 `X11` 软件包，并变得更加常见：

- `X.org`：一个面向 Linux 的、用户友好的 `X11` 软件包，作为 `XFree86` 的直接替代品开发，但使用简单的基于文本的配置文件。它将配置文件存储在通用的 `/etc/X11` 目录中。
- `Wayland`：一个更简单、更安全的图形软件包，由 `Red Hat` 开发，并作为开源软件发布。`Wayland` 在 Linux 发行版中越来越受欢迎，甚至正在快速取代 `X.org`。它为每个用户在主目录的 `~/.config/wayland-*.conf` 文件中存储单独的配置文件。

`X.org` 和 `Wayland` 系统都尝试在每次启动时自动检测系统中安装的显卡、显示器、键盘和鼠标，并相应地动态更改配置文件。如果您对显卡或显示器进行了更改，它们会自动检测新设备并相应地调整配置，这使得更换新的视频设备变得轻而易举。

**警告**

`X.org` 和 `Wayland` 软件包包含多个支持常见显卡和显示器的不同驱动程序。然而，对于这两个软件包，如果它们无法识别您系统上的特定显卡或显示器，它们默认会使用通用驱动程序，这可能无法提供最佳质量的视频体验。如果您的 Linux 系统使用特殊的显卡或显示器，最好获取它们的 Linux 驱动程序，并按照文档手动安装更新的驱动程序。

## 使用打印机

与 Linux 中的视频环境一样，Linux 中的打印功能可能相当复杂。随着各种类型的打印机可供使用，安装正确的打印机驱动程序以及使用正确的打印机协议与之通信可能是一场噩梦。

幸运的是，`Common Unix Printing System`（`CUPS`）为我们解决了许多此类问题。`CUPS` 为在 Linux 系统上处理任何类型的打印机提供了通用接口。它接受使用 `PostScript` 文档格式的打印任务，并通过**打印队列**系统将其发送到打印机。

打印队列是用于存储待打印文件的临时区域。打印队列通常不仅配置为支持特定的打印机，还支持特定的打印格式，例如横向或纵向模式、单面或双面打印，甚至是彩色或黑白打印。可以将多个打印队列分配给单个打印机，或者多个打印机可以接受分配给单个打印队列的任务。

`CUPS` 软件使用 `Ghostscript` 程序将 `PostScript` 文档转换为不同打印机可理解的格式。`Ghostscript` 程序需要针对不同打印机类型的不同驱动程序，以便知道如何转换文档，使其能在某种类型的打印机上打印。这是通过配置文件和驱动程序完成的。幸运的是，`CUPS` 安装了许多用于市场上常见打印机的不同驱动程序，并自动设置使用它们的配置要求。配置文件存储在 `/etc/cups` 目录中。

要在 Linux 系统上定义新打印机，您可以使用 `CUPS` Web 接口。打开浏览器并导航到 URL `http://localhost:631`。图 23.2 展示了 `CUPS` 使用的 Web 接口。

![](img/c0a399aca0d18f8822d714ad0a173123_723_0.png)

`CUPS` Web 接口允许您定义新打印机、修改现有打印机以及检查发送到每个打印机的打印任务的状态。`CUPS` 不仅识别直接连接的打印机，您还可以使用几种标准网络打印协议（如 `Internet Printing Protocol (IPP)` 或 `Microsoft Server Message Block (SMB)` 协议）配置网络打印机。

除了 `CUPS` Web 接口，还有几个命令行工具可用于与打印队列交互：

- `lpc`：启动、停止或暂停打印队列。
- `lpq`：显示打印队列状态，以及队列中等待的打印任务。
- `lpr`：向打印队列提交新的打印任务。
- `lprm`：从打印队列中移除特定的打印任务。

如果您在命令行中工作，可以检查任何打印队列的状态，也可以提交打印任务。对于每个命令，要指定打印机，请使用 `-P` 命令行选项以及打印机名称，如图 23.10 所示。

### 图 23.10：在 Linux 中从命令行打印
