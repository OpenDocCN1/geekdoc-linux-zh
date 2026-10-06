
一个 SCSI 适配器可以管理八个设备（宽 SCSI 为 16 个）。其中一个设备就是适配器本身。

SCSI 总线是一种带有 50 根线的平线。外部使用特种屏蔽线。SCSI 设备连接到该总线。

构建 SCSI 总线时，请记住以下点：

- SCSI 总线始终有两个端。不存在分支。
- 每个端都必须有终止器。（较新的 SCSI 设备可以自行终止。）
- 两个 SCSI 设备之间的距离必须大于 10 厘米（4 英寸）。
- 总线的最大长度为 3 米（10 英尺）。
- 总线末端总有一个设备。

# SCSI 类型

不同代的 SCSI 随时间演变：

- SCSI（或 SCSI2）。经典的 SCSI。

它可以管理八个设备（七个加上适配器），并使用带有 50 根线的电缆。

SCSI 在 1986 年成为标准。

- SCSI2。经典 SCSI 指集的扩展，用于访问硬盘以外的其他设备。

SCSI2 有两种变体：

- Fast SCSI2（比原始快）。
- Wide SCSI2（支持 16 个设备）。

- SCSI3（或 Ultra SCSI）。比 Fast SCSI2 快得多，并使用其他电缆。

为了访问超过八个设备，宽 SCSI 变体使用 68 根线的电缆（16 位总线）而不是 50 根（8 位总线）。

## 描述常见的硬件组件和资源 711

表 13-2 概述了不同的 SCSI 变体，包括它们的传输速率。

### 表 13-2

| 总线 | 传输速率：标准 | 传输速率：快速 | 传输速率：极速 |
|---|---|---|---|---|
| 8 位 | 50 | 5 MB/sec | 10 MB/sec | 20 MB/sec |
| 16 位 | 68 | 10 MB/sec | 20 MB/sec | 40 MB/sec |

## SCSI 总线地址

每个 SCSI 设备都需要一个 SCSI ID，这是一个用于访问该设备的唯一数字地址。编号从 0 开始。

通常情况下，主机适配器的 ID 为 7。数字越大，优先级越高。编号与总线的物理顺序无关。

你必须在主机适配器上或通过设备上的开关设置设备 ID。

如果你对子设备进行地址（例如磁盘架中的四块硬盘），你需要使用 LUN（逻辑单元号）。对于 SCSI 总线，子设备显示为单个设备。

此外，你可以将多个主机适配器连接到计算机。第一个总线标记为数字 0。

通过这三个数字，你可以对以下 SCSI 设备进行寻：

```
bus_number, SCSI-ID, LUN
```

## SCSI BIOS

SCSI 不识别任何标准 BIOS；访问 SCSI 设备是由操作系统的设备驱动程序完成的。

因此，如果主机适配器没有自己的 BIOS，则无法从 SCSI 设备启动。

## 从 SCSI 设备启动

如果你想从 SCSI 设备启动，需要在 SCSI BIOS 中配置设备的 SCSI ID 和传输速率。

在该 BIOS 内部，你可以选择想要启动的设备。

你必须告诉系统 BIOS 你想要从 SCSI 设备启动。你无法在系统处选择特定的 SCSI 设备。

在启动系统后，系统 BIOS 会将启动过程委托给 SCSI BIOS。

## 从 YaST 获取硬件配置信息

若要从 YaST 控制中心获取有关你的硬件配置的信息：

### 硬件 > 硬件信息

在扫描硬件几秒钟后，YaST 会显示一个与图 13-1 类似的对话框，总结有关检测到的硬件的信息。

![](img/39399c9366aee7ad257a7d2d6505f1a1_733_0.png)

图 13-1

## 硬件信息 (/proc/)

`/proc/` 目录允许你查看存储在内核空间中的硬件信息。例如，如果你输入：

```
cat /proc/cpuinfo
```

输出由存储在内核内存中的数据生成，提供 CPU 型号和缓存大小等信息。

你可以使用 `cat`、`more` 或 `less` 等命令配合文件名（例如 `cat /proc/cpuinfo`）来查看可用信息。

以下是生成信息的一些常用文件名：

- `/proc/devices`。 显示你的 Linux 系统上使用的设备。
- `/proc/cpuinfo`。 显示处理器信息。
- `/proc/ioports`。 显示你服务器上的 I/O 端口。
- `/proc/interrupts`。 显示你 Linux 系统的 IRQ 分配。

## 诊断硬件问题 713

- `/proc/dma`。 显示你的 Linux 系统上使用的 DMA 通道。
- `/proc/bus/pci/devices`。 显示你 Linux 系统上的 PCI 信息。
- `/proc/scsi/scsi`。 显示你 Linux 系统上 SCSI 信息的摘要。
- `/proc/bus/usb/devices`。 显示你 Linux 系统上 USB（通用串行总线）设备的信息。
- `/proc/bus/usb/drivers`。 显示你 Linux 系统上 USB 驱动的信息。

若要获取所有可用文件名的列表，输入 `ls -al /proc`。

![](img/39399c9366aee7ad257a7d2d6505f1a1_734_0.png)

## 目标 2 诊断硬件问题

诊断硬件问题有多种方法，包括：

- 查看启动消息
- 获取已安装硬件的信息
- 列出、加载和卸载内核模块
- 查找当前配置
- 非 Linux 计算机上的硬件

## 查看启动消息

当计算机启动时，大量信息会在屏幕上滚动，通常快到无法阅读。即使有关于硬件问题的信息，你几乎也没有机会理解它。

这些消息存储在 `/var/log/boot.msg` 中，直到达到 `/etc/inittab` 中设置的默认运行级别。

除了该文件外，内核消息存储在内存中大小为 16 KB 的环形缓冲区中。

使用 `less var/log/boot.msg` 查看启动时写入的日志文件。

命令 `dmesg` 显示内核环形缓冲区的内容。

如果计算机在启动时出现问题，这两个文件都可以对何种错误提供无价的提示。

## 获取已安装硬件的信息

当你需要关于机器中安装的特定硬件的信息时，拿螺丝刀打开机器并不总是可行方案。在大多数情况下，这甚至不是必要的。

若要获取已安装硬件的信息，请使用以下工具：

- `lspci`
- `hwininfo`
- `hdparm`
- `/sys/` 文件系统

### lspci

`lspci` 提供了连接到总线的设备的简单概述。

```
lspci
0000:00.0 Host bridge: Intel Corp. 440BX/DX - 8243BX/DX (rev 03)
0000:01.0 PCI bridge: Intel Corp. 440BX/DX - 8243BX/DX (rev 03)
0000:04.0 ISA bridge: Intel Corp. 3271AB/EB/MB PII ISA (rev 02)
0000:04.1 IDE interface: Intel Corp. 3271AB/EB/MB PII IDE (rev 01)
0000:04.2 USB Controller: Intel Corp. 3271AB/EB/MB PII USB (rev 01)
0000:04.3 Bridge: Intel Corp. 3271AB/EB/MB PII ACPI (rev 02)
0000:06.0 SCSI storage controller: Adaptec AHA-2490U/U2-7890
0000:09.0 Multimedia audio controller: Ensoniq ES1370
0000:0a.0 Ethernet controller: Realtek Co., RTL8139 (rev 05)
0000:0d.0 Ethernet controller: Intel Corp. 82557/8 (rev 10)
0000:01.0 VGA controller: Nvidia TNT2
```

### hwininfo

`lspci` 的输出可能太简略。`hwininfo` 是用于查找已安装硬件的工具。

## 诊断硬件问题

使用 `hwinfo` 可以获取已安装硬件的信息。`hwinfo` 帮助显示如下：

```
hwinfo --help
Usage: hwinfo [options]
  --short        just short
  --logfile      write info to logfile
  --debug        show debug level
  --version      show version
  --dump-db      dump data
  --hw-item     probe for hw_item
one of:
  cdrom, floppy, network, gfxcard,
  mouse, keyboard, sound, modem, storage-ctrl,
  pcmia, pcmia-ctrl, wan, zip
```

注意：调试 信息仅存储在日志中（如果不带任何参数，`hwinfo` 将检查所有类别）。

## hdparm

你可以使用 `hdparm` 工具来获取和设置 IDE 硬盘的参数。

你可以通过输入以下命令来查看硬盘的分区情况：

```bash
fdisk -l
```

## /sys/ 文件系统

在过去，确定哪个接口（软件组件）属于哪个设备（物理对象）是非常困难的。

随着内核 2.6.x 版本引入了 `sysfs` 文件系统，这种情况发生了变化。`sysfs` 是一个挂载在 `/sys/` 下的虚拟文件系统。

在虚拟文件系统中，没有物理设备来存储信息。相反，文件是由内核动态生成的。

`sysfs` 代表了 Linux 系统中所有的设备和接口。

在 `sysfs` 中，有四个主要的目录：

- `/sys/bus` 和 `/sys/devices`。这些目录包含了系统硬件的不同表示形式。设备即在此处被表示。

例如，以下路径表示一个连接到 USB 总线的数码相机：`/sys/bus/usb/devices/1-1/`

该目录包含若干提供设备信息的文件。

以下是该目录下的文件列表：

| bMaxPower manufacturer | bcdDevice bNumConfigurations maxchild | bConfiguration bNumInterfaces power | bDeviceClass detach_state product | bDeviceProtocol devnum serial | bDeviceSubClass indexPath speed | bAttributes bVendor version |

| :--- |

例如，通过读取 `manufacturer` 文件的内容，你可以确定设备的制造商：

```bash
cat manufacturer
OLYMPUS
```

在这种情况下，系统连接了一台奥林巴斯（Olymp码）相机。

- `/sys/class` 和 `/sys/block`。设备的接口在这两个目录下表示。

例如，属于该数码相机的接口由以下目录表示：

```bash
/sys/block/sda/
```

名为 `sda` 的目录代表像 SCSI 硬盘一样访问的数码相机。

## 诊断硬件问题

以下是 `sda` 目录的内容：

```
dev queue removable size
device range sda1 stat
```

子目录 `sda1` 代表相机内存卡第一个分区的接口。

例如，通过读取 `sda1/size` 的内容，你可以确定分区的大小：

```bash
cat sda1/size
31959
```

该分区的大小为 31959 个 512 字节块，大约是 16 MB。

为了将接口与设备连接，使用了文件系统链接。

在奥林巴斯数码相机的示例中，存在从 `/sys/block/sda/device` 到对应设备的链接：

```bash
11 device
lrwxrwxr-x 1 root root 0 ../devices/
pci0000:00:0000:00:id1d:0/usb1-1/1-1.0/host0:0:0:0
```

通过这种方式，系统所有的接口都与其对应的设备相连。

除了 `sysfs` 中的表示外，`/dev/` 目录下还有设备文件。

应用程序访问设备接口时需要这些文件。**设备文件**（device file）这个名称具有误导性，使用**接口文件**（interface file）更为合适。

## 列出、加载和卸载内核模块

一旦通过上述方法确定了硬件类型，就会出现这个问题：控制设备的模块是否加载？

你可以使用命令 `lsmod` 来检查。

```bash
da10:~ # lsmod
Module Size Used
raid5 20736 1
xor 15240 1 raid5
nvram 8456 0
speedtest_lib 3712 0
freq_table 4612 0
snd_seq_oss 31232 0
snd_pcm_oss 57512 0
snd_mixer_oss 18944 1 snd_pcm_oss
...
```

通常，内核模块会在系统启动或当 USB 设备等热插拔硬件连接到机器时自动加载。

## 查询当前配置

你也可以手动加载模块：

```bash
modprobe kernel_module
```

你可以使用以下命令卸载未使用的内核模块：

```bash
rmmod
```

硬件设备的配置存储在 `/etc/` 目录下的文件中。

这些文件在设备启动初始化时被使用。

在许多情况下，配置是通过 `/proc` 文件系统中的文件完成的。

类似于 `/sys` 文件系统，这是一个虚拟文件系统，它不存储在硬盘上，而是在系统启动时创建的。

你可以使用 `cat` 读取当前配置，在某些情况下也可以更改运行时配置。

以下是 `/proc/sys/` 的示例：

```bash
da10-: # cat /proc/sys/net/ipv4/ip_forward
0
da10-: # echo 1 > /proc/sys/net/ipv4/ip_forward
da10-: # cat /proc/sys/net/ipv4/ip_forward
1
```

`net/ipv4/ip_forward`:

该文件决定了 IP 数据包是否从一个网络接口路由到另一个接口。

如果文件中的值为 0，则不进行路由。

向文件中写入 1 则开启路由。

`/proc` 文件系统中其他包含有用信息的文件还包括：

- `/proc/cpuinfo`
- `/proc/filesystems`
- `/proc/interrupts`
- `/proc/ioports`
- `/proc/modules`
- `/proc/mounts`
- `/proc/partitions`
- `/proc/pci`
- `/proc/swaps`

## 描述多媒体组件 721

后续章节介绍了以下内容：

- ALSA PCM 类型
- 混合器 (Mixers)
- 缓冲与延迟
- WAV 的直接录制与播放
- 音频压缩
- ALSA 和 MIDI

## ALSA PCM 类型

PCM（脉冲编码调制）在涉及声卡时指的是数字输出接口。

你可以通过选择特定的 PCM 类型来影响 ALSA 访问声卡的方式。主要的 PCM 类型有 `hw` 和 `plughw`。

要理解这两种类型的区别，请考虑 PCM 设备是如何打开的。打开时必须对至少以下参数进行特定设置：

- 采样格式
- 采样频率
- 通道数
- 周期数（以前称为片段/fragments）
- 周期大小

例如，应用程序可能会尝试播放采样频率为 44.1 kHz 的 WAV 文件，尽管声卡并不支持该频率。

在这种情况下，ALSA 可以自动将插件层中的数据转换为声卡支持的格式。

这种转换影响以下参数：

- 采样格式
- 采样频率
- 通道数

通过选择 PCM 类型来激活插件层，请输入 `plughw`。

如果选择了 PCM 类型 `hw`，ALSA 将尝试使用应用程序所需的参数直接打开 PCM 设备。

## 第 13 节硬件基础

PCM 设备的完整标识符由 PCM 类型、冒号、声卡号和设备号组成，例如：

`plughw:0,0`

`dmix` 输出插件是 PCM 类型最近添加的项。它允许应用程序在不支持此项的声卡上共享对 PCM 设备的访问。

完整标识符为：

`plug:dmix`

关于 `dmix` 的更多信息，请参阅 http://alsa.opensrc.org/index.php?page=DmixPlugin。

![](img/39399c9366aee7ad257a7d2d6505f1a1_743_0.png)

## 混合器

混合器提供了控制计算机音频输出和输入音量及平衡的方便方法。

各种混合器之间的主要区别在于用户界面的外观。

然而，有些混合器是为特定硬件设计的。

`alsamixer` 是 `als` 包的一部分，可以在没有环境的情况下从命令行运行，如图 13–2 所示。

![](img/39399c9366aee7ad257a7d2d6505f1a1_743_1.png)

图 13-2

## 描述多媒体组件 723

你可以使用光标键控制应用程序。

使用 Q、W、E、Y、X 和 C 为左右通道设置不同的电平。

按 M 静音单个通道。在这种情况下，MM 会出现在静音控制器上方。

按 Esc 键退出 `alsamixer`。

音频输出的基本控制项有：

- Master（主音量）。设置主音量。
- PCM 和 CD。控制 PCM 和音频通道的各自权重。

按空格键确定录制源。

捕获控制器调节输入放大器。

使用 Line（线路）控制器还是 MIC（麦克风）控制器取决于录制源。

![](img/39399c9366aee7ad257a7d2d6505f1a1_744_0.png)

欲了解更多信息，输入 `man alsamixer`。

`alsamixergui` 是 `alsamixer` 的图形版本。

## 缓冲与延迟

Linux 以及所有其他多任务操作系统固有的问题是确保音频播放不被中断。

在多任务操作系统，通常会有多个进程并发运行。

由于处理器一次只能处理一个进程，操作系统调度器会为每个进程分配一定的时间。
