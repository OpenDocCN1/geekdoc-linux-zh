
author:         Jaroslav Kysela <peres@suse.cz>, Thomas Sailor

<sailer@ife.ee.eezh.cz>

version:       411FDA3B2ED30C62AB8E67

alias:          pci:v0000127d.040000088sv*sd*bc*ci*

alias:          pci:v0000127d.040000017sv*sd*bc*ci*

alias:          

depends:       snd_seq,snd_raemir,7 SMP_mod_unload 686 4KSTACK

parm:           `index`:Ensoniq AudioPCI 声卡的索引值 (array of int)

parm:           `id`:Ensoniq AudioPCI 声卡的 ID 字符串 (array of char)

parm:           `enable`:启用 Ensoniq AudioPCI 声卡 (array of bool)

parm:           `ystick`:摇杆端口地址 (array of it)

如果你需要添加或删除加载模块以使系统正常工作，可以使用 `modprobe` 命令。你也可以使用 `modprobe` 列出所有可用模块并删除模块。以下是示例：

```
# modprobe -l | grep -c-qcam     列出所有模块，然后查找 c-qcam
/lib/modules/2.6.21-1.3228.fc7/kernel/drivers/media/video/c-qcam.ko
# modprobe c-qcam                加载 Color QuickCam 模块
# modprobe -r c-qcam               删除 Color QuickCam 模块
```

> 注意 你可能会发现 `insmod` 命令相比，modprobe 可以智能地加载模块依赖关系。由于原因，我们建议只使用 `modprobe`。

你可以使用 `sysctl` 命令用系统控制内核参数。你还可以将参数永久地添加到 `/etc/sysctl.conf` 文件中，以便它们可以一组加载或在重启时加载。以下是一些示例：

```
# sysctl -a | less             列出所有内核参数
kernel.panic = 0
kernel.exec_shield = 1
--...
# sysctl kernel.hostname         显示特定参数的值
# sysctl -p                        从 /etc/sysctl.conf 加载参数
# sysctl -w kernel.hostname=joe      设置 kernel.hostname 的值
```

## 第 10 章：管理系统

如前所述

### 探测硬件

如果你只是想泛泛地了解你计算机的硬件，有几个命令可以尝试。`lspci` 命令列出你计算机上 PCI 设备的信息：

```
# lspci
List PCI hardware items
00:00.00 Host bridge: VIA Technologies, Inc. VT8375 [KM266/KL266] Host Bridge
00:01.00 PCI bridge: VIA Technologies, Inc. VT8633 [Apollo Pro226 AGP]
00:10.00 USB Controller: VIA Technologies, Inc. VT82xxxxx UHCI USB 1.1
00:11.0 ISA bridge: VIA Technologies, Inc. VT8235 ISA Bridge
00:12.00 Ethernet controller: VIA Technologies, Inc. VT6102 [Rhine-II]
01:00.0 VGA compatible controller: SJ Inc. VT8375 [ProSavage8/KM266]
```

```
# lspci -v
List PCI hardware items with more details
# lspci -vv
List PCI hardware items with even more details
```

使用 `dmidecode` 命令，你可以显示硬件组件的信息，包括关于 BIOS 支持哪些功能的信息。
这是一个示例：

```
# dmidecode | less
List hardware components
# dmidecode 2.7
SMBIOS 2.3 present.
32 structures occupying 919 bytes.
Table at 0x000F0100.
```

```
Handle 0x0000, DMI type 0, 20 bytes.
BIOS Information
Vendor: Award Software International, Inc.
Version: F2
Release Date: 10/06/2003
Processor Information
Socket Designation: Socket A
Type: Central Processor
Family: Athlon
Manufacturer: AMD
ID: 44 06 00 00 FF FB 83 01
Signature: Family 6, Model 4, Stepping 4
Flags:
FPU (Floating-point unit on-chip)
VME (Virtual mode extension)
DE (Debugging extension)
```

你可以使用 `hdparm` 命令来查看和更改与硬盘相关的信息。

> 警告！虽然查看硬盘功能的信息是安全的，但更改其中某些设置可能会损坏你的硬盘。

这里是打印硬盘信息的一些示例：

```
# hdparm /dev/sda             Display hard disk settings (SATA or SCSI drive)
/dev/sda:
IO_support = 0 (default 16-bit)
readonly   = 0 (off)
readahead  = 256 (on)
geometry   = 30401/255/63, sectors = 488395055, start = 0
```

```
# hdparm /dev/hda             Display hard disk settings (IDE drive)
# hdparm -I /dev/sda                   Display detailed information
/dev/sda:
```

ATA device, with non-removable media
Model Number: FUJITSU MPG3409AT E
Serial Number: VH06T19RV9W
Firmware Revision: 82C5

### 总结

SUSE 和其他 Linux 系统让你能够轻松地监控和修改运行系统的许多方面，以确保其以最高性能运行。`free`、`top`、`vmstat`、`slabtop`、`iostat` 和 `dstat` 等命令让你看到系统如何使用内存、CPU 和存储设备。通过 `date`、`hwclock` 和 `cal` 等命令以及 NTP 等服务，你可以监控和管理系统的日期和时间设置。

要管理系统启动时设置的功能和启动的服务，你可以修改与 GRUB 启动和运行级别相关的功能。你可以使用 `service` 和 `chconfig` 等命令启动、停止、列出、添加和删除单个系统服务。`reboot`、`halt` 和 `shutdown` 命令可以让你安全地停止或重启计算机。

在管理计算机硬件方面，`lsmod`、`modinfo` 和 `modprobe` 等命令让你处理可加载模块。你可以通过 `lspci`、`dmidecode` 和 `hdparm` 等命令查看硬件信息。

## 11 管理网络连接

在 Linux 中连接网络通常只需将计算机的网络网卡连接到 ISP 的硬件（如 DSL 或电缆调制解调器）。然而，如果你的网络接口没有启动或需要某些手动干预，有很多命令可用于配置网络接口、检查网络连接和设置特殊路由。

本章涵盖了许多用于配置和操作网络网卡（NIC）的有用命令，例如 `ifconfig`。特别涵盖了配置有线以太网、无线以太网和调制解调器网络硬件的方法。在硬件连接和网络接口就绪后，本章描述了如 `netstat`、`dig` 和 `ping` 等获取网络信息的命令。

### 本章内容

- 使用 ethtool 处理网络网卡
