
操作系统以两步过程加载：

- 1. 一个名为 LILO（Linux Loader）的小型引导程序由系统的 BIOS 加载。
- 2. LILO 加载 Linux 内核文件。

## LILO

LILO 是面向基于 x86 的 Linux 系统的引导加载程序。它可以从软盘和硬盘引导 Linux 内核镜像，也可用于引导其他操作系统，如 DOS、OS/2、Windows 9x 和 Windows NT。

LILO 由一组程序、数据文件和一个配置文件组成。它包含映射安装程序 `/sbin/lilo`、位于 `/etc/lilo.conf` 的配置文件、若干数据文件以及引导加载程序本身。这些数据文件和引导加载程序通常位于 `/boot` 目录中，分别名为 `boot.b`、`map` 和 `chain.b`。LILO 的引导加载程序部分由 BIOS 加载，随后加载 Linux 内核或其他操作系统的引导扇区。

LILO 引导加载程序本身分为两部分。第一部分非常小，存储在软盘或硬盘的引导扇区中。引导加载程序的这一部分知道从何处加载第二阶段的引导加载程序。引导加载程序的两部分通常都存储在文件 `/boot/boot.b` 中。

当通过运行映射安装程序 `/sbin/lilo` 安装 LILO 时，它会把引导加载程序的第一部分写入软盘的引导扇区或主硬盘的主引导记录。参数通常通过配置文件 `/etc/lilo.conf` 传递给 LILO。下面显示了一个典型的 `lilo.conf` 文件：

```text
boot=/dev/sda
map=/boot/map
install=/boot/boot.b
prompt
timeout=50
delay=100
image=/boot/vmlinuz-2.2.12smp
        label=linux
        root=/dev/sda1
        initrd=/boot/initrd-2.2.12smp.img
        read-only
image=/boot/vmlinuz-2.2.5-15smp
        label=linux-old
        root=/dev/sda1
        initrd=/boot/initrd-2.2.5-15.smp.img
        read-only
```

此配置会将 LILO 引导加载程序安装到主硬盘 `/dev/sda` 的主引导记录上。LILO 将使用引导加载程序 `/boot/boot.b` 和映射文件 `/boot/map`。`root=/dev/sda1` 这一行告诉 LILO Linux 根文件系统位于分区 `/dev/sda1` 上。`image=/boot/vmlinuz-2.2.12smp` 行指定了 Linux 内核的名称。第二行 `image=/boot/vmlinuz-2.2.5-15smp` 告诉 LILO，备用的旧内核镜像 `/boot/vmlinuz-2.2.5-15smp` 可用于引导，并可通过命令行选项传递给 LILO 来指定。`initrd=` 行指定了可用的 RAM 磁盘镜像，如果你需要为系统维护而在 RAM 磁盘中引导备用根文件系统，可以使用这些镜像。这些内核镜像名称和位置存储在 LILO 映射文件中。

`prompt` 选项指示引导加载程序始终提示输入可在引导时输入的命令行选项。`timeout=50` 选项为提示设置五秒超时。如果没有输入命令行选项，系统会在等待五秒后继续引导。

`delay=100` 指示引导加载程序在引导期间按下 Shift 键时等待十秒。否则，将引导提到的第一个内核镜像。如果按下了 Shift 键，引导加载程序会提示输入要引导的内核镜像名称。当你安装新内核时，此选项非常有用。LILO 提供了一种引导旧内核的方法，以防新内核出现问题。

LILO 提供了许多可能性和选项。要了解 LILO，请阅读通常位于 `/usr/doc/lilo-0.21` 目录下的文档——`Technical_Guide.ps` 和 `User_Guide.ps`。

## 内核初始化与硬件配置

在引导的这一阶段，内核已被 LILO 加载，开始执行并初始化自身。内核最先做的事情之一是检查系统上可用的内存。内核为自身、内部数据存储和缓冲区保留固定数量的内存。相关信息会打印到系统控制台上，并记录在 `/var/log/dmesg` 中。例如，会打印类似以下消息，说明可用系统内存以及其中有多少被内核保留。

```text
Memory: 387200k/393216k available (1044k kernel code, 416k reserved,\
  4184k data, 68k init)
```

内核完成自身初始化后，开始探测系统以查看存在哪些设备。当构建自定义内核时，通常会配置包含一组用于系统上预期设备的驱动程序。通用内核可能包含比你系统上实际拥有的更多设备的支持。当内核检测到这些设备时，它会打印关于它们的非常简短的消息。以下是双 CPU 机器上的启动消息示例输出，显示了内核检测并配置的各种设备。你系统上的输出消息将根据安装的硬件和外设类型而有所不同：

```text
Linux version 2.2.5-15smp (root@porky.devel.redhat.com) (gcc version egcs-2.91.66
 19990314/Linux (egcs-1.1.2 release)) #1 SMP Mon Apr 19 22:43:28 EDT 1999
Intel MultiProcessor Specification v1.4
        Virtual Wire compatibility mode.
OEM ID: COMPAQ Product ID: PROLIANT  APIC at: 0xFEE00000
Processor #1 Pentium(tm) Pro APIC version 16
Processor #0 Pentium(tm) Pro APIC version 16
I/O APIC #2 Version 1 at 0xFEC00000.
Processors: 2
mapped APIC to ffff0000 (fe000000)
mapped IOAPIC to ffffd000 (fec00000)
Detected 19943487 Hz processor.
Console: colour VGA+ 80x25
Calibrating delay loop... 199.07 BogoMIPS
Memory: 387200K/393216K available (1044K kernel code, 416K reserved,\
 4184K data, 68K init)
VFS: Diskquota version 6.4.0 initialized
Checking 386/387 coupling... OK, FPU using exception 16 error reporting.
Checking 'hlt' instruction... OK.
POSIX conformance testing by UNIFIX
rtr: v1.26 (19981001) Richard Gooch (rgooch@atnf.csiro.au)
per-CPU timeslice cutoff: 50.10 usecs
CPU1: Intel Pentium Pro stepping 09
calibrating APIC timer...
..... CPU clock speed is 199.4250 MHz.
..... system bus clock speed is 66.4747 MHz.
Booting processor 0 eip 2000
Calibrating delay loop... 199.07 BogoMIPS
OK.
CPU0: Intel Pentium Pro stepping 09
Total of 2 processors activated (398.13 BogoMIPS).
enabling symmetric I/O mode... ...done.
ENABLING IO-APIC IRQs
init IO APIC IRQs
 IO-APIC pin 0, 16, 17, 18, 19, 20, 21, 22, 23 not connected.
...MP BIOS bug: 8254 timer not connected to IO-APIC
...trying to set up timer as ExtINT... ... (found pin 0) ... works.
number of MP IRQ sources: 16.
number of IO-APIC registers: 24.
testing the IO APIC....................
..... register #0: 02000000
....... physical APIC id: 02
..... register #1: 0170011
....... max redirection entries: 0017
....... IO APIC version: 0011
..... register #2: 02000000
....... arbitration: 00
.... IRQ redirection table
NR Log Phy Mask Trig IRR Pol Dest Deli Vect:
00 001 00 0 0 0 0 0 7 51
01 000 00 0 0 0 0 0 1 59
02 000 00 0 0 0 0 0 1 51
03 000 00 0 0 0 0 0 1 61
04 000 00 0 0 0 0 0 1 69
05 0FF 0 1 1 0 0 1 1 71
06 000 00 0 0 0 0 0 1 79
07 000 00 0 0 0 0 0 1 81
08 000 00 0 0 0 0 0 1 89
09 0FF 0 1 1 0 1 1 1 91
0a 000 00 0 0 0 0 0 1 99
0b 000 00 0 0 0 0 0 1 A1
0c 000 00 0 0 0 0 0 1 A9
0d 000 00 1 0 0 0 0 0  A0
0e 000 00 0 0 0 0 0 1  B1
0f 000 00  0  0  0  0  1  1  B9
10 000 00  1  0  0  0  0  0  00
11 000 00  1  0  0  0  0  0  00
12 000 00  1  0  0  0  0  0  00
13 000 00  1  0  0  0  0  0  00
14 000 00  1  0  0  0  0  0  00
15 000 00  1  0  0  0  0  0  00
16 000 00  1  0  0  0  0  0  00
17 000 00  1  0  0  0  0  0  00
IRQ to pin mappings:
IRQ0 -> 1
IRQ1 -> 1
IRQ3 -> 3
IRQ4 -> 4
IRQ5 -> 5
IRQ6 -> 6
IRQ7 -> 7
IRQ8 -> 8
IRQ9 -> 9
IRQ10 -> 10
IRQ11 -> 11
IRQ12 -> 12
IRQ13 -> 13
IRQ14 -> 14
IRQ15 -> 15
.............................. done.
PCI: PCI BIOS revision 2.10 entry at 0xf005e
PCI: Using configuration type 1
PCI: Probing PCI hardware
PCI: Device 00:00 not found by BIOS
PCI: BIOS reporting unknown device 00:a2
PCI: 00:00 [8086/1237]: Passive release enable (00)
PIIX3: Enabling Passive Release
Linux NET4.0 for Linux 2.2
Based upon Swansea University Computer Society NET3.039
NET4: Unix domain sockets 1.0 for Linux NET4.0.
NET4: Linux TCP/IP 1.0 for NET4.0
IP Protocols: ICMP, UDP, TCP, IGMP
Initializing RT netlink socket
Starting kswapd v 1.5
Detected PS/2 Mouse Port.
Serial driver version 4.27 with MANY_PORTS MULTIPORT SHARE_IRQ enabled
ttyS00 at 0x03f8 (irq = 4) is a 16550A
ttyS01 at 0x02f8 (irq = 3) is a 16550A
pty: 256 Unix98 ptys configured
Real Time Clock Driver v1.09
RAM disk driver initialized: 16 RAM disks of 4096K size
PIIX3: IDE controller on PCI bus 00 dev 01
PIIX3: 100% native mode: will probe irqs later
    ide0: BM-DMA at 0x1000-0x1007, BIOS settings: hda:pio, hdb:pio
hda: HITACHI CDR-7930, ATAPI CDROM drive
ide0 at 0x1f0-0x1f7,0x3f6 on irq 14
hda: ATAPI 8X CD-ROM drive, 128KB Cache
Uniform CDROM driver Revision: 2.54
Floppy drive(s): fd0 is 1.44M
FDC 0 is a National Semiconductor PC87306
md driver 0.90.0 MAX_MD_DEVS=256, MAX_REAL=12
```

