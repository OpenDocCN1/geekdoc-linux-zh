
![](img/cd7b8bd6bc2bb54927442d4cbe51a330_114_0.png)

图示标签指的是系统第一个 SCSI 磁盘上的分区 6。

在 2.4 内核下，Red Hat 可以支持多达 20 个 IDE/ATA 硬盘设备，在设备名称开头标记为 "h"。支持的分区数量取决于驱动器的文件系统类型，且不能超过 63。（详情参阅第 3 章。）

默认提供的常用 IDE/ATA 设备：

- 硬盘：
    - 整个设备 `hd[a–h]`
    - 设备分区 `hd[a–h][1–16]`
- 磁带：`ht0`

在 2.4 内核下，Red Hat 可以支持多达 12 个 SCSI 硬盘设备，在设备名称开头标记为 "s"。同样，支持的分区数量取决于驱动器的文件系统类型，且不能超过 15。（详情参阅第 3 章。）

默认提供的常用 SCSI 设备：

- 硬盘：
    - 整个设备 `sd[a–p]`
    - 设备分区 `sd[a–p][0–15]`
- 磁带：`st[0–7]`
- 光驱：`scd[0–7]`

Linux 命名方式较令人不安的方面之一是其相关的分配方法。设备根据在链上检测到的顺序分配字母编号，而不是通过 SCSI-ID 或 IDE/ATA 的主/从跳线决定。这种动态命名方案实际上相当稳定，但如果你在放置新磁盘时不小心，可能会导致意想不到的结果。

Solaris 使用 System V 命名规范，它使用数字来区分磁盘及其分区。每个操作系统似乎对这个主题都有其自己的小变体，在移动东西之前，保持清思路至关重要。虽然它不像 Linux 命名方案那样紧凑，但 Solaris 仍然确保了你获取了所有必要信息，如图 2.9 所示。

### 图 2.9

图示的 Solaris 设备名称。

![](img/cd7b8bd6bc2bb54927442d4cbe51a330_115_0.png)

图示标签指的是位于主控制器上 SCSI-ID 为 5 的磁盘上的分区 6（0 通常是主内部/外部控制器）。

注意，我们忽略了名称中的“d0”部分。这是因为磁盘号（或逻辑单元号，lun）通常为 0。如果你在 RAID（或具有负责多个磁盘的控制器的类似结构）中指定特定设备，那么 lun 就会变化。

正如你可能推出的那样，由于命名方案中包含了“目标 ID”，Solaris 的设备名称分配方法是基于驱动器的 SCSI-ID 或 IDE/ATA 主/从状态的。

注意，Solaris 在其高级命名方案中不区分 SCSI 和 IDE/ATA 设备。我们将在下一章的“设备”部分看到原因。现在，这里是一些默认提供的常用设备名称：

#### 管理磁盘硬件

第二章

- 硬盘：
    - 整个设备 `c0td0`
    - 设备分区 `c0td0s[0–7]`
- 磁带：`st[0–7]`
- 光驱：`scd[0–7]`

> 注意：关于设备及其在系统中的位置以及通用用途的更详细信息，请参见第 3 章的“分区”节。

## 让操作系统告诉你组成硬件

在本文写作时，还没有统一标准，操作系统与硬件是独立的。系统与硬件交互，但仍有一些属于硬件的信息。因此，当你想让 Red Hat 告诉你当前的硬件时，有几个地方可以查看并匹配问题。在收集系统信息时，`uname` 始终是一个很好的命令，可以告诉你 OS 级别、基础硬件和系统名称：

```
processor : 0
vendor_id : Genuine
cpu family : 6
model name : Pentium III (Coppermine)
stepping : 3
cpu MHz : 795.07
cache size : 256 KB
fdiv_bug : no
hlt_bug : no
sep_bug : no
f0f_bug : no
coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 3
wp : yes
flags : fpu vme pse tsc msr pae cx8 apic mtr pge mca xfsr xmm
bogomips : 1589.25
```

```
processor : 1
vendor_id : Genuine
cpu family : 6
model name : Pentium III (Coppermine)
stepping : 3
cpu MHz : 795.07
cache size : 256 KB
fdiv_bug : no
hlt_bug : no
sep_bug : no
f0f_bug : no
coma_bug : no
fpu : yes
fpu_exception : yes
cpuid level : 3
wp : yes
flags : fpu vme pse tsc msr pae cx8 apic mtr pge mca xfsr xmm
bogomips : 1589.25
```

`/proc/cpuinfo` 中的信息要密集得多，它告诉你 PCI 总线上的所有设备。以下列表来自一台包含 11 个设备的机器，包括控制器和磁盘：总线 0，功能 0：主机桥：Intel 未知设备（修订 0）。

![](img/cd7b8bd6bc2bb54927442d4cbe51a330_117_0.png)

### 基础操作

第一部分

| Vendor id | Device id | Type | Latency | Gnt | Memory |
| :--- | :--- | :--- | :--- | :--- | :--- |
| 8086 | 71a0 | PCI bridge | 64 | - | 0xf80000 [0xf80008] |
| 8086 | 71a1 | PCI bridge | 64 | 132 | - |
| 8086 | 71a2 | SCSI storage controller | 64 | 39 | 25 | 0x2800 [0x2001] |
| 8086 | 71a2 | SCSI storage controller | 64 | 39 | 25 | 0x2400 [0x2001] |
| 8086 | 71a4 | Ethernet controller | 64 | 6 | 56 | 0xf410200 [0xf410200] |
| 8086 | 71a4 | Ethernet controller | 64 | 6 | 56 | 0xf410000 [0xf410004] |
| 8086 | 71a4 | Ethernet controller | 64 | 6 | 56 | 0xf410100 [0xf410104] |
| 8086 | 71a6 | ISA bridge | 64 | - | - |
| 8086 | 71a6 | IDE interface | 64 | - | - |
| 8086 | 71a6 | USB Controller | 64 | - | - |
| 8086 | 71a8 | ACPI | 64 | - | - |
| 8086 | 71a0 | VGA compatible controller | 64 | 2 | 10 | 0xf600000 [0xf600008] |

#### 管理磁盘硬件

第 2 章

厂商 ID=1011. 设备 ID=23。

介质 devsel。支持快速背靠传输。支持主设备模式。

延迟=240. 最小握手=6。

## Solaris

在我们的 Solaris 参考平台上运行 `uname`，可以得到以下输出：

```
[sun:4] -uname -a
SunOS sun.my.com 5.8 Generic 108528-06 sun4u sparc SUN,Sun-Blade-100
```

现在我们知道了机器的名称（sun.my.com）、它运行的 Solaris 版本（SunOS 5.8 大约等于 Solaris 8），以及它是一台 Sun Blade 100（尽管并非所有的 `uname` 硬件识别都是如此）。

获取本地驱动列表最快的方法是运行 `format` 命令：

```
[sun:5] -format
Searching for disks...done
```

```
AVAILABLE DISK SELECTIONS:
0.c00d0<ST315320A cyl 2964 alt 2 16 sec 63>
/pci8f,0/ide/dad0,0
Specify disk (enter number):
```

按下 Ctrl+D 可终止格式化并返回命令提示符。

> 警示

如果你不知道自己在做什么，`format` 命令也是不可逆转地销毁磁盘最简单、最快的方法。一个小小的错误就可能完全抹除磁盘上的文件系统。

`print` 或 `list` 命令通常是安全的，但使用向驱动器写入数据的命令时（如 `sync`、`write` 等），请务必极度小心。

注意，这台机器只有一个磁盘，且 `format` 显示了关于它的大量底层信息。
