
注意，即使在 `jane` 给出密码后，她仍然使用 `sudo` 命令以 root 身份运行命令（第一次挂载失败，第二次成功）。注意，他在执行 root sudo 时没有被提示输入密码。这是因为在成功输入密码后，在接下来的几分钟内可以输入任意 `sudo` 命令，而无需再次输入。（你可以通过设置 `/etc/sudoers` 文件中的 `passwd_timeout` 值将超时时间从五分钟改为任何长度）。

上一个示例为你放入 `wheel` 组的每个人授予了简单的“全有全无”管理权限。然而。

# 管理 Fedora 和 RHEL

## 配置硬件

本节描述了如何：

- **配置硬件** — 当你将硬件连接到计算机时，Linux 将简单地检测并识别它们。在启动期间，内核将探测 IDE 驱动器、PCI 卡和其他硬件。在 Linux 运行期间，插入的 USB 设备将被检测。
- **管理文件系统** — 当你添加或删除硬件时，Linux 将自动挂载任何文件系统。
- **监控性能** — 如果你遇到性能问题，可以使用工具确定原因。

### 检查硬件

有时 Fedora 或 RHEL 无法正确检测和配置你的硬件会导致你无法安装。在这种情况下，我建议你在安装之前尝试确定你的硬件。请参考第 2 章关于安装前检查硬件的信息。

### 使用 kudzu 重新配置硬件

当你为计算机添加或删除硬件并重启 Linux 时，启动过程中会出现窗口提示硬件已添加或删除，并询问是否要重新配置。检测并配置硬件的程序称为 `kudzu`。

`kudzu` 程序是一个启动时自动运行的硬件检测和配置工具。如果你愿意，可以在 Linux 运行时启动它。无论何种方式，如下：

1. 检查连接到计算机的硬件。
2. 将发现硬件与存储在 `/etc/sysconfig/hwconf` 文件中的硬件信息数据库进行比较。
3. 根据检测到的新增或删除硬件，提示你更改系统配置。

以下是 `kudzu` 可以检测的硬件列表（根据 `kudzu` README 文件），随后是 `kudzu` 配置设备的描述。除了 USB 设备外，还可以检测到其他设备。

# 第 10 章：理解系统管理

- **键盘** — 运行 `kbdconfig` 命令来重新配置键盘。以及

以下是移除设备时所采取的操作列表：

- **网络** — 移除太网接口的别名（`eth0`, `eth1` 等）。
- **SCSI** — 移除 SCSI 主机适配器的别名（`scsi_hotadapter`）。
- **调制解器** — 移除指向 `/dev/modem` 的链接。
- **CD-ROM** — 移除指向 `/dev/cdrom` 的链接。
- **扫描仪** — 移除指向 `/dev/scanner` 的链接。

要运行 `kudzu`，可以手动运行（在重启期间，`kzu`会自动运行），或者简单地在 shell 中以 root 身份运行 `kudzu` 命令。对于自上次运行 `kudzu` 以来添加的任何硬件，它都会询问你是想配置它、忽略它，还是什么都不做。

> 注意：可移动设备（如数码相机、USB 闪存驱动和网络摄像头）通过半守护进程（half daemon）进行检测并即时配置。该半守护进程依赖 Udev 设备管理，在连接此类类型的设备时动态创建设备和挂载点（如果需要）。请参见第 8 章关于如何检测 CD 和数码相机的描述。

## 配置模块

在理想的世界中，安装并启动 Linux 后，所有的硬件都应该被检测到并可用。虽然 Fedora 和 Red Hat Linux 系统正在快速向那个世界靠近，但有时你必须采取特殊步骤让计算机硬件正常工作。

Fedora 和 RHEL 系统自带用于配置驱动程序的程序（如 CD 播放器和网络浏览器）与它们使用的硬件（如 CD-ROM 驱动程序和网卡）之间的工具。其意图是将最关键的驱动构建到内核中；这些被称为*驻留驱动*（resident drivers）。根据需要动态添加的其他驱动程序被称为*加载模块*（loadable modules）。趋势是保持基本内核尽可能精简，以便每个运行的系统只有几个驻留驱动，并且它可以动态添加所需的内容。

### 列出模块

要查看哪些模块已加载到计算机的运行内核中，你可以使用 `lsmod` 命令。例如：

```
# lsmod
Module              Size Used by
| snd_seq_oss | 38912 | 0 |
| snd_midi_event | 93444 | 1 snd_seq_oss |
| snd_seq | 67728 | 4 snd_seq_oss,snd_midi_event |
| snd_seq_device | 8328 | 2 snd_seq_oss,snd_seq |
| autofs | 16512 | 0 |
| ne2k_pci | 9056 | 0 |
| 8390 | 13568 | 1 ne2k_pci |
| ohci1394 | 41860 | 0 |
| ieee1394 | 284464 | 1 ohci1394 |
| floppy | 65712 | 0 |
| sg | 36120 | 0 |
| scsi_mod | 124600 | 1 sg |
| parport_pc | 39724 | 0 |
| parport | 47336 | 1 parport_pc |
| ext3 | 128424 | 2 |
| jbd | 86040 | 1 ext3 |
```

此输出显示了 Linux 系统上加载的各种模块，包括为了支持 ALSA 音频系统和 OSS 兼容性（`snd_seq_oss`）在该系统中加载的模块。

要查找关于任何模块的信息，你可以使用 `modinfo` 命令。例如，你可以输入：

```
# modinfo snd-seq-oss
filename: /lib/modules/2.6.25-8.i686/kernel/sound/core/oss/snd-seq-oss.ko
alias: sound-sequence~-1
alias: sound-sequence~-8
license: OSS-compatible sequencer module
author: Takashi Isai <tsisai@suse.de>
versversion: OC6CC71AFE69F8CC1866
depends: snd-seq-oss,snd-seq-midi-event,snd-seq-device
vermagic: 2.6.25-8.i686 SMP mod_unload 686 4STACKS
parm: maxlen=maximum queue length (int)
parm: snd_oss_debug=debug (int)
```

此输出可以告知你模块的位置（`filename`）、作者和描述等其他信息。输出将 `snd-seq-oss` 描述 OSS 兼容的序列器模块。你可以使用 `-d` 选项列出描述，使用 `-a` 选项查看模块的作者，或使用 `-n` 选项查看代表模块的对象文件。作者信息通常包含驱动程序创建者的电子邮件地址，因此如果你对它有问题或疑问，可以联系作者。

## 加载模块

你可以使用 `modprobe` 命令将任何已编译并安装（到 `/lib/modules`）的模块加载到运行的内核中。加载的最常见原因是你想使用硬件。这是一个示例：

```
# modprobe [module_name]
```

加载模块后，你可以使用 `lsmod` 检查它是否已加载。如果你需要移除模块，请使用 `modprobe -r` 命令：

```
# modprobe -r [module_name]
```

> 注意：如果模块正在使用中，将无法移除。你必须先停止使用该模块的进程。

## 移除模块

移除模块使用 `modprobe -r` 命令。如果模块正在使用中，将无法移除。你必须先停止使用该模块的进程。

> 注意：要防止模块自动加载，可以将其添加到 `/etc/blacklist`。

## 文件系统与磁盘空间

文件系统在 Linux 中的组织方式与 Windows 不同。文件系统的组织从你安装 Linux 开始。安装过程的一部分是将硬盘划分为分区。这些分区可以分配给：

- Linux 文件系统的一部分
- Linux 交换分区
- 其他文件系统类型（可能包含可启动的操作系统）

要查看硬盘上目前设置了哪些分区，请如下使用 `fdisk` 命令：

```
### fdisk -l
Disk /dev/sda: 40.0 GB 4020064320
255 heads, 63 sectors/track, 48285 cylinders
Units = cylinders of 16065 * 512 bytes = 8225280
```

| Device | Start | End | Blocks | Id System |
|---|---|---|---|---|
| /dev/sda | * | 1 | 13 | 104 Win32 |
| /dev/sdb | | 84 | 89 | 48195 | 83 Linux |
