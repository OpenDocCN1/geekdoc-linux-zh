

要了解 HAL 关于您系统的信息，请运行 `lshal` 命令：

```bash
$ lshal
Dumping 96 device(s) from the Glocal Device List:
udi = '/org/freedesktop/Hal/devices/computer'
info.addons = ['hal_add_on_cpufreq', 'hal_add_on_acpi'] (string list)
...
org.freedesktop.Hal.Device.SystemPowerManagement.method signatures = ['i', 'i', 'i', 'i', 'i', 'b'] (string list)
org.freedesktop.Hal.Device.SystemPowerManagement.method power_managements =
power_management.acpi.linux.version = '20060707' (string)
power_management.can_hibernate = true (bool)
power_management.can_suspend = true (bool)
power_management.can_suspend_to_brid = false (bool)
power_management.can_suspend_to_disk = true (bool)
power_management.can_suspend_to_ram = true (bool)
power_management.is_powersave_set = false (bool)
power_management.type = 'acpi' (string)
...
udi = '/org/freedesktop/Hal/devices/pci_8086_27c0'
info.linux.driver = 'ata_pidx' (string)
info.parent = '/org/freedesktop/Hal/devices/computer' (string)
info.product = '82801GB/GR/GH (ICH7 Family) SATA IDE Controller' (string)
info.subsystem = 'pci' (string)
info.udi = '/org/freedesktop/Hal/devices/pci_8086_27c0' (string)
info.vendor = 'Intel Corporation' (string)
...
```

在这冗长的输出中，您可以看到关于系统硬件的各种信息，例如本例中的 SATA IDE 磁盘控制器。您可以在 `www.freedesktop.org/Soft/hare/hal` 上了解更多关于 HAL 的信息。

## 使用 kudzu 重新配置硬件

在早期版本的 CentOS 中，当您向计算机添加或移除硬件并重新启动时，启动过程中会出现一个窗口，提示已添加或移除硬件，并询问您是否希望重新配置它。检测和重新配置硬件的程序称为 kudzu。

kudzu 程序是一个硬件自动检测和配置工具，在启动时自动运行。如果愿意，也可以在 Linux 运行时启动 kudzu。无论哪种情况，kudzu 执行以下操作：

1.  它检查连接到计算机的硬件。
2.  它将找到的硬件与存储在 `/etc/sysconfig/hwconf` 文件中的硬件信息数据库进行比对。
3.  基于检测到的新添加或已移除的硬件，它提示您更改系统配置。

以下是 kudzu 能够检测到的硬件列表（根据 kudzu 的 README 文件），随后描述了 kudzu 如何配置该设备。kudzu 也可能检测到其他设备（如 USB 设备）。

-   **网络设备** — 如有必要，添加以太网接口别名（eth0, eth1 等），并迁移旧的设备配置或创建新的配置。
-   **SCSI** — 为 scsi_hostadapter 添加别名。
-   **声卡** — 运行 sndconfig 命令来配置和测试声卡。
-   **鼠标** — 运行 mouseconfig 命令来配置和测试鼠标。
-   **调制解调器** — 将新的调制解调器设备链接到 /dev/modem。
-   **CD-ROM** — 将 CD-ROM 设备链接到 /dev/cdrom。
-   **扫描仪** — 将新的扫描仪设备链接到 /dev/scanner。
-   **键盘** — 运行 kbdconfig 命令重新配置键盘。此外，如果您使用的是串行控制台，它会确保 /etc/inittab 和 /etc/security 已配置为供串行控制台使用。

以下是设备移除时 kudzu 采取的操作列表：

-   **网络** — 移除以太网接口的别名（eth0, eth1 等）。
-   **SCSI** — 移除 SCSI 主适配器的别名（scsi_hostadapter）。
-   **调制解调器** — 移除到 /dev/modem 的链接。
-   **CD-ROM** — 移除到 /dev/cdrom 的链接。
-   **扫描仪** — 移除到 /dev/scanner 的链接。

要运行 kudzu，可以重新启动系统（在重启过程中，kudzu 会自动运行），或者简单地运行 kudzu 命令（以 root 用户身份在 shell 中）。对于自上次运行 kudzu 以来添加或移除的任何硬件，系统会询问您是否希望配置它、不配置它或不做任何操作。

> **注意** 可移动设备，如数码相机、USB 闪存盘和 webcam（网络摄像头），使用 hald 守护进程进行即时检测和配置。hald 守护进程依赖于 Udev 设备管理设施，在这些类型的设备连接时动态创建设备和挂载点（如果需要）。有关如何检测 CD 和数码相机的描述，请参阅第 7 章。

## 配置模块

在理想世界中，安装并启动 Linux 后，所有硬件都应被检测到并可访问。虽然 CentOS 系统正迅速向这个理想靠拢，但有时您必须采取特殊步骤才能使计算机硬件正常工作。

CentOS 系统配备了配置驱动程序的工具，这些驱动程序位于您运行的程序（如 CD 播放器和 Web 浏览器）与它们使用的硬件（如 CD-ROM 驱动器或网卡）之间。其意图是让系统所需的最关键驱动程序内置于内核中；这些称为 *驻留驱动程序*。根据需要在动态添加的其他驱动程序称为 *可加载模块*。趋势是保持基本内核尽可能精简，使得每个运行系统只有少数驻留驱动程序，并且可以动态添加其所需的内容。

### 列出已加载的模块

要查看当前加载到计算机上运行内核中的模块，您可以使用 `lsmod` 命令。示例如下：

```bash
# lsmod
Module                 Size  Used by
snd_seq_oss            38912   0
snd_seq_midi_event      9344   1 snd_seq_oss
snd_seq                67728   4 snd_seq_oss,snd_seq_midi_event
snd_seq_device         8328   2 snd_seq_oss,snd_seq
.
.
.
aufs                 16512   0
ne2k_pci              9056   0
8390                 13568   1 ne2k_pci
oncl1394              41660   0
fee1394               28464   1 ohci1394
floppy                 65712   0
sg                     36120   0
scsi_mod              124600   1 sg
parport_pc             39724   0
parport                47336   1 parport_pc
ext3                  128424   2
jbd                   86040   1 ext3
```

此输出显示了一个 Linux 系统上加载的各种模块。该系统加载的模块包括多个支持声音的模块，其中包括一些提供 OSS 兼容性的模块（snd_seq_oss）。

要查找有关任何已加载模块的信息，您可以使用 `modinfo` 命令。例如，您可以输入以下内容：

```bash
# modinfo snd-seq-oss
filename:    /lib/modules/2.6.18-128.el5/kernel/sound/core/seq/oss/snd-seq-oss.ko
alias:    sound-service-?-8
alias:    sound-service-?-1
license:    GPL
description:    OSS-compatible sequencer module
author:    Takashi Iwai <tiwai@use.de>
srcversion:    73084089714451A425C6D70
depends:    snd-seq,snd-midi-event,snd-seq-device,snd
gcc:    4.1
vermagic:    2.6.18-128.el5 SMP mod_unload 686 REGPARM 4KSTACKS
parm:
    maxqlen:maximum queue length (int)
dbg:
    seq_oss_dbg:debug option (int)
module_sig:
    883f3504977495a4f3f897cd3dced2112f38609e2cdaa6474f c1c8
    782529cf677976d2a5f17a2aa09f4b01bf2f0aff749281917
    deb66798af86d9cf59b3
```

此输出告知您模块的位置（filename）、作者和描述等信息。输出将 `snd-seq-oss` 描述为 OSS 兼容的序列器模块。您可以使用 `-d` 选项仅列出描述，使用 `-a` 选项查看模块的作者，或使用 `-n` 查看代表该模块的目标文件。作者信息通常包含驱动程序创建者的电子邮件地址，因此如果您遇到问题或疑问，可以联系作者。

## 加载模块

您可以使用 `modprobe` 命令将任何已编译和安装（到 `/lib/modules/<kernel version>/` 目录）的模块加载到正在运行的内核中。加载模块最常见的原因是：您希望临时使用某个功能（例如加载模块以支持必须访问的软盘上的特殊文件系统），或者需要标识一个将由特定硬件使用的模块，而该硬件无法被自动检测。

以下是使用 `modprobe` 命令加载 `parport` 模块的示例。`parport` 模块提供核心功能，以允许多个设备共享并行端口。

```bash
# modprobe parport
```

加载 `parport` 后，您可以加载 `parport_pc` 模块来定义通过该接口可用的 PC 式端口。`parport_pc` 模块允许您选择性地定义与共享并行端口的每个设备关联的地址和 IRQ 号。例如：

```bash
# modprobe parport_pc io=0x3bc irq=auto
```

在上面的示例中，设备被标识为具有地址 `0x3bc`。设备的 IRQ 是自动检测的。

`modprobe` 命令临时加载模块。在下次系统重启时，您输入的模块将消失。要确保每次系统启动时都加载该模块，请添加

