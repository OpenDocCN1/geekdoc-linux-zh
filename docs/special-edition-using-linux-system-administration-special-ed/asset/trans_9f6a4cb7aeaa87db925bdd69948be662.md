
```text
# cat file-max
4096
# cat inode-max
4096
```

要令文件表的大小加倍，我们只需将这两个值都加倍：

```text
# echo 8192 > /proc/sys/fs/file-max
# echo 8192 > /proc/sys/fs/inode-max
```

## 对称多处理

对称多处理是一种专门的计算机架构，通过让多个处理器共同运行进程来显著提升系统性能。对称多处理基于共享内存架构，所有处理器通过同一条系统总线访问同一物理内存。这种架构对可以有效并行运行的 CPU 数量施加了一些实际限制。大多数 SMP 系统在使用两到十六个处理器时扩展性良好；超过这个范围后，继续增加处理器所带来的性能提升幅度会下降。SMP 架构的主要瓶颈之一在于共享总线。不过，随着新技术和更高总线速度的出现，有效利用更多处理器已成为可能。

其基本概念很简单：多个处理器协同工作，共同分担系统的工作负载。然而，实际实现相当复杂，而且扩展性并非线性——这意味着将 CPU 数量翻倍并不会带来双倍的性能。

操作系统必须经过专门设计才能发挥 SMP 架构的优势。高效而智能的任务调度是对称多处理系统的核心。调度是一种将进程分配到不同 CPU 上运行的机制。在对称多处理操作系统中，只存在一个运行队列。进程从该运行队列中被取出，并根据不同的算法分配到各个 CPU 上。整个进程可以映射到某个 CPU，也可以将不同线程映射到不同 CPU。多线程进程在对称多处理环境中获益最大。

SMP 是在 Linux 2.0 内核中引入的。相关代码一直在不断改进，并且在 2.2.x 内核中引入了更细粒度的锁定机制。这使得进程访问内核时能够获得更好的性能。

要构建支持 SMP 的内核，您只需在配置内核时对“Symmetrical MultiProcessing Support”选项回答“Yes”。内核构建过程的其余部分与单处理器内核的情况相同。

在 SMP 机器上编译内核时，可以通过使用 `-jX` 选项调用 make 来运行并行编译进程，其中 X 是最大编译进程数。

构建并安装 SMP 内核后，您可以通过查询 `/proc` 文件系统中的 `cpuinfo` 值来确认所有 CPU 是否都已被使用。在双 Pentium 系统上，典型输出如下：

```text
# cat /proc/cpuinfo
processor       : 0
vendor_id       : GenuineIntel
cpu family      : 6
model           : 1
model name      : Pentium Pro
stepping        : 9
cpu MHz         : 199.434636
cache size      : 256 KB
fdiv_bug        : no
hlt_bug         : no
sep_bug         : no
f00f_bug        : no
fpu             : yes
fpu_exception   : yes
cpuid level     : 2
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov
bogomips        : 199.07
processor       : 1
vendor_id       : GenuineIntel
cpu family      : 6
model           : 1
model name      : Pentium Pro
stepping        : 9
cpu MHz         : 199.434636
cache size      : 256 KB
fdiv_bug        : no
hlt_bug         : no
sep_bug         : no
f00f_bug        : no
fpu             : yes
fpu_exception   : yes
cpuid level     : 2
wp              : yes
flags           : fpu vme de pse tsc msr pae mce cx8 apic sep mtrr pge mca cmov
bogomips        : 199.07
```

您还可以使用 `dmesg` 命令检查系统的启动信息。双 CPU 系统的典型 dmesg 输出如下：

```text
# dmesg
Linux version 2.2.5-15smp (root@porky.devl.redhat.com) (gcc version egcs-2.91.66\
19990314/Linux (egcs-1.1.2 release)) #1 SMP Mon Apr 19 22:43:28 EDT 1999
Intel MultiProcessor Specification v1.4
        Virtual Wire compatibility mode.
OEM ID: COMPAQ   Product ID: PROLIANT    APIC at 0xFEE00000
Processor #1 Pentium(tm) Pro APIC version 16
Processor #0 Pentium(tm) Pro APIC version 16
I/O APIC #2 Version 1 at 0xFEC00000.
Processors: 2
mapped APIC to ffff0000 (fee00000)
mapped IOAPIC to fffffd000 (fec00000)
Detected 199.434636 Hz processor.
Console: colour VGA+ 80x25
Calibrating delay loop... 199.07 BogoMIPS
Memory: 387200k/393216k available (1044k kernel code, 416k reserved, 4184k data, 68k init)
VFS: Diskquotas version quota_6.4.0 initialized
Checking 386/387 coupling... OK, FPU using exception 16 error reporting.
Checking 'hlt' instruction... OK.
POSIX conformance testing by UNIFIX
mtrr: v1.26 (19981001) Richard Gooch (rgooch@atnf.csiro.au)
per-CPU timeslice cutoff: 50.0 usecs.
CPU1: Intel Pentium Pro stepping 09
calibrating APIC timer ...
..... CPU clock speed is 199.4418 MHz.
..... system bus clock speed is 66.4804 MHz.
Booting processor 0 eip 2000
Calibrating delay loop... 199.07 BogoMIPS
OK.
CPU0: Intel Pentium Pro stepping 09
Total of 2 processors active (398.13 BogoMIPS).
enabling symmetric IO mode... ...done.
ENABLING IO-APIC IRQs
init IO-APIC 0
IO-APIC pin 0, 16, 17, 18, 19, 20, 21, 22, 23 not connected.
...MP-BIOS bug: 8254 timer not connected to IO-APIC
...trying to set up timer as ExtINT... .. (found 0) ... works.
number of MP IRQ sources: 16.
number of IO-APIC registers: 24.
testing the IO APIC:.......................
.... register #0: 02000000
........ : physical APIC id: 02
........ register #1: 00170011
........ : max redirection entries: 0017
........ : IO APIC version: 0011
........ register #2: 00000000
........ : arbitration: 00
```

## 故障排除

在构建、安装和使用新内核的过程中，可能会出现大量问题。其中包括：

- 您的内核无法编译。
- 您的新内核无法启动。
- 您的系统无法启动。
- 您的系统找不到压缩的内核映像文件。
- 内核升级后，您无法编译其他程序。
- 您的内核太大且太慢。
- 您的并口或打印机出现问题。
- 您的 CD-ROM 驱动器出现问题。

### 内核无法编译

您的新内核无法编译可能有以下几种原因：

- 补丁操作失败。
- 您的内核源代码树已损坏。
- 您的 gcc 版本太旧。
- 您到 `/usr/include/linux` 的链接可能错误或缺失；请参阅内核的 `README` 文件，了解如何正确设置这些链接。

如果一个标准、稳定、干净的内核源代码树无法编译，这说明系统存在严重问题，许多工具可能需要重新安装。同时也不应排除硬件问题，例如内存故障。

### 新内核无法启动

您的系统无法用新构建并测试过的内核启动，可能的原因包括：

- 您忘记运行 lilo。
- LILO 配置不正确；例如，启动条目中的一个小错误就可能阻止 LILO 启动您的新内核。
- 您忘记添加 ext2fs 文件系统支持。这对 Linux 系统至关重要。

### 系统无法启动

如果即使正确配置并安装了 LILO，您的系统仍然无法启动，那么请用软盘或 CD-ROM 启动系统，并准备另一张可启动软盘。

要制作一张可启动软盘，请按以下步骤操作：

1. 使用一张启动/根分区组合软盘启动系统，例如可以从 `ftp://metalab.unc.edu/pub/linux/recovery` 获取的软盘。

2. 确定您拥有可用内核映像的位置。这通常是以下位置之一：
   - `/vmlinux`
   - `/boot/vmlinuz`
   - `/usr/src/linux/arch/i386/boot/bzImage`

3. 确定存放您的根文件系统（`/`）和 `/usr` 文件系统的磁盘分区。例如，在简单的系统上，`/dev/hda1` 可能同时包含 `/` 和 `/usr`。

4. 您的启动/根分区组合软盘应该带有一个 ram disk 启动。如果 ram disk 上不存在 `/mnt` 目录，请创建一个：

   ```text
   # mkdir /mnt
   ```

