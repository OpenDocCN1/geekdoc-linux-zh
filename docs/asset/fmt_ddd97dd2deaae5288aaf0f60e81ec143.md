
要运行 kudzu，请重启（在重启期间，kudzu 会自动运行）或直接运行 `kudzu` 命令（在 shell 中作为 root 用户）。对于自上次运行 `kudzu` 以来添加或删除的硬件，系统会询问你是否想配置它或什么都不做。

> 注意：可移动设备（如数字相机、USB 闪存器和摄像头）使用 `uald` 守护进程进行实时检测和配置。`hold` 守护进程依赖 `Udev` 设备管理功能，在连接此类类型的设备时动态创建设备和挂载点（如果需要）。请参阅第 8 章查看有关如何检测 CD 和数字设备的描述。

## 配置模块

在理想的世界里，安装并启动 Linux 后，所有的硬件都应该被检测到并可以访问。虽然 Fedora 和 Red Hat Enterprise Linux 系统正在快速接近这一目标，但有时你必须采取特殊步骤才能让计算机硬件正常工作。

Fedora 和 RHEL 系统带有工具，用于配置介在你运行的程序（如 CD 播放器和网络浏览器）与它们使用的硬件（如 CD-ROM 驱动器和网卡）之间的驱动程序。意图是仅让系统需要的最关键的驱动程序构建在内核中；这些被称为驻留驱动程序。其他根据需要动态添加的驱动程序被称为可加载模块。目前的趋势是保持基础内核尽可能精简，以便每个运行的系统只有少数驱动程序，并且它可以动态添加其所需的内容。

## 列出已加载的模块

要查看当前加载到计算机运行内核中的哪些模块，你使用 `lsmod` 命令。这里是一个示例：

| Module | Size | Used by |
|---|---|---|
| `snd_seq_oss` | 38912 | 0 |
| `snd_seq_midi_event` | 93444 | 1 `snd_seq_oss` |
| `snd_seq` | 67728 | 4 `snd_seq_oss`,`snd_seq_midi_event` |
| `snd_seq_device` | 8328 | 2 `snd_seq_oss`,`snd_seq` |
| `autofs` | 16512 | 0 |
| `ne2k_pci` | 9056 | 0 |
| `8390` | 13568 | 1 `ne2k_pci` |
| `ohci1394` | 41860 | 0 |
| `ieee1394` | 284464 | 1 `ohci1394` |
| `floppy` | 65712 | 0 |
| `sg` | 36120 | 0 |
| `scsi_mod` | 124600 | 1 `sg` |
| `parport_pc` | 39724 | 0 |
| `parport` | 47336 | 1 `parport_pc` |
| `ext3` | 128424 | 2 |
| `jbd` | 86040 | 1 `ext3` |

此输出显示了在 Linux 系统上加载的各种模块。该系统加载的模块包括几个支持 ALSA 声音系统的模块，包括一些提供 OSS 兼容性的模块（`snd_seq_oss`）。

要查找有关任何已加载模块的信息，你可以使用 `modinfo` 命令。例如，你可以输入以下内容：

```
modinfo snd-seq-oss
filename: /lib/modules/2.6.23.1-31.fc8/kernel/core/seq/oss/snd-seq-oss.ko
alias: sound-version-?
alias: sound-version-8
license: GPL
description: OSS-compatible sequencer module
author: Takashi Iwai <iwai@suss.de>
srcversion: B37590BB804039AACACE5D7
depends: snd-seq-oss,snd-midi-event,snd-seq-device
vermagic: 2.6.23-0.61.rc1.9 SMP mod_unload 686 4STACKS
parm: maxlen=maximum queue length (int)
parm: snd_seq_debug=debug option (int)
```

此输出告诉你是模块的位置（`filename`）、作者以及描述等其他信息。输出描述 `snd-seq-oss` 为一个 OSS 兼容的序列器模块。

第 10 章：理解系统管理 435

你可以使用 `-d` 选项列出描述，使用 `-a` 选项查看，或者使用 `-n` 选项查看。

### 加载模块

你可以使用 `modprobe` 将任何编译到内核的模块。例如，你可以加载一个连接到硬件的模块。

```
modprobe
```

模块加载后，你可以使用以下命令处理系统。

### 移除模块

你可以从内核中移除任何已加载的模块。例如，你可以使用：

```
rmmod
```

如果模块正在忙，则：

```
rmmod
```

防止该模块加载。`/etc/blacklist`

第三部分：管理 Fedora

有时硬件设备检测不当。在这种情况下，你可以考虑将模块添加到 `/etc/blacklist`。之后，你可以考虑将模块加载系统。

## 管理文件系统和磁盘空间

Linux 文件系统按层次结构组织，从根目录 (`/`) 开始向下延伸。作为 Fedora 或 RHEL 系统的管理员，你有责任确保所有磁盘驱动对用户可用。对于硬盘分区，你需要在文件系统中创建一个挂载点并连接磁盘。对于可移动媒体（如 CD、DVD、USB 驱动器或数字相机），当这些项目连接时，会自动创建并连接挂载点（在 `/media` 目录）。

交叉引用：第 2 章提供了使用磁盘配置磁盘分区的说明。第 4 章描述了 Linux 文件系统是如何组织的。你的文件系统的组织始于安装 Linux。安装过程的一部分是将你的硬盘（或磁盘）划分为分区。这些分区随后可以分配给：

- Linux 文件系统的一部分
- Linux 的交换空间（Swap）
- 其他文件系统类型（可能包含其他操作系统）

对于我们的目的，我想关注用于 Linux 文件系统的分区。要查看硬盘上当前设置了哪些分区，请使用如下 `fdisk` 命令：

```
fdisk -l
Disk /dev/sda: 40.0 GB, 40020664320
255 heads, 63 sectors/track, 4825 cylinders
Units = cylinders of 16065 * 512 bytes = 8225280 bytes
```

| Device Boot | Start | End | Blocks Id System |
|---|---|---|---|
| `/dev/sda1` * | 1 | 13 | 104 b | Win95 FAT32 |
| `/dev/sda2` | | 84 | 89 | 48195 83 Linux |
| `/dev/sda3` | | 90 | 522 | 3478072+ 83 Linux |

# 第10 章：理解系统管理

| `/dev/sda4` | 523 | 554 | 257040 | 5 | W5 Ext3 (LBA) |
| `/dev/sda5` | 523 | 554 | 257008+ | 82 | Linux swap / Solaris |

这显示了计算机同时运行 Linux 和微软 Windows 系统的磁盘分区情况。你可以使用 `/dev/sda3` 上的 Linux 分区，因为它拥有大部分的可用数据空间。这里有一个 Windows 分区 (`/dev/sda1`) 和一个 Linux 交换分区 (`/dev/sda5`)。此外，在 `/dev/sda2` 上还有一个较小的 `/boot` 分区（46MB）。在这种情况下，Linux 的根分区具有 3.3GB 的磁盘空间，并驻留在 `/dev/sda3` 上。

接下来，要查看哪些分区实际上被用于你的 Linux 系统，你可以使用 `mount` 命令（不带任何选项参数）。`mount` 命令可以向你显示可用磁盘分区中哪些已实际挂载，以及它们挂载在何处。

```
# mount
/dev/sda3 / type ext3 (rw)
/dev/sda2 /boot type ext3 (rw)
/dev/sda1 /mnt/win type vfat (rw)
none on /proc type proc (rw)
none on /sys type sysfs (rw)
none on /dev/pts type devpts (rw,gid=5,mode=620)
none on /dev/shm type tmpfs (rw)
none on /proc/fs/binfmt_misc type binfmt_misc (rw)
/dev/scd0 /media/cdrecorder iso9660
(ro,nousid,nodev,uhelper-hal)
```

> 注意：你可能会发现 `/proc`,`/sys`,`/dev/pts`,`/proc/fs/binfmt_misc`, `/dev` 以及与其他分区不相关的条目显示为文件系统。这是因为它们代表了不同的文件系统类型（`proc` 和 `devpts` 等）。然而，`none` 一词表示它们没有与独立的物理分区相关联。
