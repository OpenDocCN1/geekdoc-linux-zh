
如果 `ifconfig` 报告 `EAGAIN` 错误，则表示存在中断冲突。该消息意味着在中断冲突清除后重试。为了解决问题，请将 `ifconfig` 报告的中断请求与 `/proc/interrupts` 的内容进行比较，以确定哪些设备冲突。PCI 设备使用的 IRQ 也在 `/proc/pci` 中报告。

如果 `ifconfig` 为 PCI NIC 报告 IRQ 为 0 或 255，则表示卡尚未分配 IRQ。这是由 BIOS 没有足够的线路供 PCI 设备使用（它们都分配给 ISA 设备而不是 PnP）或 BIOS 具有必须禁用的“PnP OS”或“Windows 9x support”选项引起的。

如果 PCI NIC 请求有效的 IRQ，但该中断已被另一块 PCI 设备使用，最简单的解决方案是通过系统 BIOS 将冲突设备放在另一个 IRQ 线上。PCI 卡无法自行设置 IRQ 线。这是在启动时由 PC BIOS 完成的。

### NIC Diagnostic Programs

如果您的 NIC 设备驱动程序正在加载且 IRQ 正常，但仍然有些问题，您可以从 Donald Becker 的“Linux at CESDIS”网站：http://cesdis.gsfc.nasa.gov/linux/linux.html at NASA 下载许多流行 NIC 的诊断实用程序的源代码。

使用源代码末尾提供的说明编译与您的 NIC 对应的程序，并以 root 身份运行它们以获取诊断信息。对于许多厂商 OEM 的流行的 Digital DC21040“tulip”系列，诊断实用程序称为 `tulip-diag`。编译程序的读出如下所示：

```
[root@wallace diag]# /usr/local/bin/diag/tulip-diag -m

tulip-diag.c:v1.12 7/31/99 Donald Becker (becker@cesdis.gsfc.nasa.gov)

Index #1: Found a Digital DS21140 Tulip adapter at 0xec80.

Port selection is MII, half-duplex.

Transmit started, Receive started, half-duplex.
```

Rx 进程状态为 'Waiting for packets'。
Tx 进程状态为 'Idle'。
传输阈值为 128。
在地址 3 找到 MII PHY，状态为 0x786d。
MII PHY #0 收发器寄存器：

```
3100 786d 2000 5c01 01e1 0021 0000 0000

0000 0000 0000 0000 0000 0000 0000 0000

0000 0000 0000 0000 0000 0000 0001 0000

8020 0c63 0000 3000 a3b9 0000 6505 001b
```

CESDIS 网站上的另一个有用工具是通用 `pci-config` 程序，它可以显示系统上所有 PCI 设备的读数。在前述 Digital Tulip 网卡的 PCI 设备号 4 上运行 `pci-config` 会得到以下结果：

```
[root@wallace diag]# ./pci-config -# 4

pci-config.c:v1.06 7/24/99 Donald Becker (becker@cesdis.gsfc.nasa.gov)

Device #4 at bus 0 device/function 20/0.

00091811 02600117 02000222 00002068 0000c81f ffaff80 00000000 00000000

00000000 00000000 200110b8 ffa80000 00000000 28140103

00000000 00000000 00000000 00000000 00000000 00000000 00000000

00000000 00000000 00000000 00000000 00000000 00000000 00000000

00000000 00000000 00000000 00000000 00000000 00000000 00000000

00000000 00000000 00000000 00000000 00000000 00000000 00000000

00000000 00000000 00000000 00000000 00000000 00000000 00000000

00000000 00000000 00000000 00000000 00000000 00000000 00000000

Base Address 0: I/O at 0000c8b0.

Base Address 1: Memory at ffaff80.
```

`pci-config` 实用程序可用于使设备进入睡眠、唤醒设备、将其设置为 Wake-on-LAN 模式，或显示 PCI 寄存器，如前面的列表所示。这些实用程序的文档位于源代码中。

## DOS 诊断

即使在专用的 Linux 服务器上，包含一个可启动的 DOS 分区以存储和执行 DOS 实用程序也是有用的。许多品牌 PC，例如 Dell、Compaq 和 IBM，都包含专有的基于 DOS 的诊断工具，可使硬件故障排除更容易。还有一些商业 DOS 实用程序在测试硬件组件和压力测试内存芯片方面做得特别好。

在 DOS 分区中保留一个最小的 Windows 95（或更高版本）安装也可能很有用。其控制面板、系统、设备读数对于检查卡设置非常方便，特别是如果卡在 Windows 端工作但在 Linux 端不工作。读数可能会提供否则可能被遗漏的线索。Windows 95 分区也可以作为 Linux 的紧急存储来使用。

诊断程序对于硬件设备的初始配置很有用，但在系统运行良好后出现意外情况，例如硬件组件故障时，系统管理员的关注点会从设置转变为紧急救援。为此你需要一些救援工具。

## 构建和使用救援磁盘

尽管计算机系统变得越来越可靠，但组件有时仍会发生故障。硬盘驱动器作为机械设备，其故障率高于其他组件。当硬盘发生完全故障时，很少有系统管理员会尝试恢复驱动器上的任何数据。除非你使用 RAID，否则正常程序是插入新驱动器，从头开始构建基本操作系统，然后从备份中恢复所有重要文件和设置。

对于 Linux 系统而言，良好的备份程序的重要性怎么强调都不为过。备份是你最终的安全网。确保你的系统定期备份，并且定期通过从备份媒体中恢复随机选择的文件来测试备份磁带或其他媒体。

然而，许多磁盘故障并非完全故障。硬盘可能会出现坏点。Linux 在启动时通过在挂载分区之前使用 `fsck` 对每个分区的文件系统进行快速完整性检查来尝试监视逐渐出现的问题。在每几次重启期间，`fsck` 将对文件系统执行更彻底的检查。

当出现坏点时，它可能会破坏一些文件，损坏文件、目录结构或 inode 编号。这可能会影响整个子树，使其无法访问。更糟糕的是，它可能导致损坏的结构通过正常文件操作传播，破坏的数据比原始坏点所在的数据更多。

并非所有文件损坏都是由故障硬件造成的。作为系统管理员，出现人为错误并不罕见，例如意外擦除系统密码文件、设置后忘记 root 密码、安装新内核并忘记运行 `lilo` 创建新的引导信息，或错误编辑 `/etc/fstab`，导致系统无法启动。

当这些事情发生时，就该从你的工具包里取出 Linux 救援磁盘集了。救援系统是一张或一套软盘，允许你启动一个驻留在 RAM 中的非常小的 Linux 操作系统版本。一旦你在救援模式下联机，救援磁盘包含足够的基础工具，允许你尝试修复你的 Red Hat Linux 系统，或在严重恶劣的情况下尽可能恢复尽可能多的文件。

## 构建救援磁盘

显然，在需要时手边有救援磁盘比在危机中学习如何创建它更方便。救援磁盘应该是你在设置系统后创建的第一件事之一。

Red Hat 在其 CD-ROM 和其网站上提供预先制作的救援磁盘映像。如果你使用 Red Hat 系统的标准 CD-ROM 挂载点，救援磁盘映像将位于 `/mnt/cdrom/images/rescue.img`，你可以将它传输到软盘。

要从 Linux 创建救援磁盘，请插入 Red Hat CD-ROM 并将其挂载，并插入一张新的 1.44Mb 3.5 英寸空白软盘。以 root 身份输入以下命令（假设你的 1.44Mb 磁盘驱动器是 `/dev/fd0` 并且它是高密度 1.44Mb 驱动器）：

```
[root@wallace /root]# fdformat /dev/fd0H1440

Double-sided, 80 tracks, 18 sec/track. Total capacity 1440 kB.

Formatting ... done

Verifying ... done

[root@wallace /root]# mount /dev/cdrom /mnt/cdrom

[root@wallace /root]# cd /mnt/cdrom/images
```
