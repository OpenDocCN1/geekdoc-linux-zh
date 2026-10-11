
配置文件可以包含全局选项和本地选项。全局选项适用于所有日志文件，而本地选项仅适用于特定的日志文件。本地选项会覆盖全局设置的选项。可以使用多个配置文件，但如果发生冲突，则最后一个文件中的指令将覆盖第一个文件中的指令。以下是一个 logrotate.conf 文件的示例：

```
# see "man logrotate" for details
# rotate log files weekly
weekly

# keep 4 weeks worth of backlogs
rotate 4

# send errors to root
errors root

# create new (empty) log files after rotating old ones
create

# uncomment this if you want your log files compressed
compress

# RPM packages drop log rotation information into this
#directory
include /etc/logrotate.d

# no packages own lastlog or wtmp -- we'll rotate them here
/var/log/wtmp {
    monthly
    create 0664 root utmp
    rotate 1
}

/var/log/lastlog {
    monthly
    rotate 1
}

# system-specific logs may be configured here
```

配置文件使用许多不同的命令来提供日志轮换的指令。所使用的命令在表 11-5 中列出并进行了说明。

## 表 11-5 logrotate 命令

| 命令 | 用途 |
| --- | --- |
| compress | 使用 gzip 压缩旧日志。 |
| copytruncate | 复制旧日志，然后将其截断。 |
| create | 为文件创建权限。如果未指定权限，则使用旧文件的权限。 |
| daily | 每天轮换日志文件。 |
| delaycompress | 在下次轮换时压缩日志文件。 |
| errors mailto | 将错误消息发送到指定的地址。 |
| ifempty | 轮换空日志文件。 |
| include filename | 用于将文件名读取到配置文件中。 |
| mail mailto | 指定在日志文件被删除时发送日志文件的邮件地址。 |
| monthly | 每月轮换日志文件。 |
| nocompress | 不压缩日志文件。 |
| nocopytruncate | 不复制并截断。 |
| nocreate | 指定不创建新的日志文件。 |
| nodelaycompress | 立即压缩日志文件。 |
| noolddir | 日志文件不会移动到另一个目录。 |
| noifempty | 空日志文件不会被轮换。 |
| olddir directory | 旧日志文件被移动到指定的目录。 |
| postrotate | 在日志轮换后运行脚本。 |
| prerotate | 在日志轮换前运行脚本。 |
| rotate n | 指定要保留的旧日志文件数量。 |
| size n | 当日志文件达到指定大小时进行轮换。可与 n（字节）、k（千字节）和 M（兆字节）一起使用。 |

### 使用日志文件识别问题

仅仅保留日志文件并不能解决或预防系统上的问题。为了让日志文件发挥作用，您必须定期审查记录的数据。`dmesg` 命令可用于显示系统消息。该命令使用以下语法：

```
dmesg [options]
```

`dmesg` 命令显示来自内核环形缓冲区的系统消息。使用 `-n level` 选项将显示特定级别的消息。消息级别在 `kernel.h` 文件中定义。`-c` 选项在显示内容后清空缓冲区。如果同时使用这两个选项，第一个选项将被忽略。

以下是输入 `dmesg` 命令后收到的输出示例：

```
Linux version 2.2.15-4mdx (root@10@inux.the-nashes.net
30 (ppc/release)) #2 Wed Jun 21 22:29:09 EDT 2000
Detected 75003357 Hz processor.
ide_setup: hdd=ide-scsi
Console: colour VGA+ 80x25
Calibrating delay loop... 1494.22 BogoMIPS
Memory: 257488k/262080k available (1208k kernel code
72k init, 0k bigmem)
Dentry hash table entries: 32768 (order 6, 256k)
Buffer cache hash table entries: 262144 (order 8, 10
Page cache hash table entries: 65536 (order 6, 256k)
VFS: Diskquotas version dquot_6.4.0 initialized
CPU: L1 I Cache: 64K L1 D Cache: 64K
CPU: L2 Cache: 512K
CPU: AMD AMD Athlon(tm) Processor stepping 01
Checking 386/387 coupling... OK, FPU using exception
Checking 'hlt' instruction... OK.
POSIX conformance testing by UNIFIX
mtrr: v1.35a (19990819) Richard Gooch (rgooch@atnf.c
PCI: PCI BIOS revision 2.10 entry at 0xfb4d0
PCI: Using configuration type 1
PCI: Probing PCI hardware
Linux NET4.0 for Linux 2.2
Based upon Swansea University Computer Society NET3.
NET4: Unix domain sockets 1.0 for Linux NET4.0.
NET4: Linux TCP/IP 1.0 for NET4.0
IP Protocols: ICMP, UDP, TCP, ICMP
TCP: Hash tables configured (ehash 262144 bhash 6553
Initializing RT netlink socket
Starting kswapd v1.5
Detected PS/2 Mouse Port.
Serial driver version 4.27 with MANY_PORTS MULTIPORT
ttyS00 at 0x03f8 (irq = 4) is a 16550A
ttyS01 at 0x02f8 (irq = 3) is a 16550A
pty: 256 Unix98 pty's configured
apm: BIOS version 1.2 Flags 0x07 (Driver version 1.1
Real Time Clock Driver v1.08
RAM disk driver initialized: 16 RAM disks of 4096K
Uniform Multi-Platform E-IDE driver Revision: 6.30
ide: Assuming 33MHz system bus speed for PIO modes;
VP_IDE: IDE controller on PCI bus 00 dev 39
VP_IDE: not 100% native mode: will probe irqs later
VT 8371
Chipset Core ATA-66
Split FIFO Configuration:  8 Primary buffers, thresh
                      8 Second. buffers, thresh
ide0: BM-DMA at 0x0400-0x0d07, BIOS settings: hda:DMA, hdb:DMA
ide0: VIA Bus-Master (U)DMA Timing Config Success
ide1: BM-DMA at 0x0d08-0x0d0f, BIOS settings: hda:DMA, hdb:DMA
ide1: VIA Bus-Master (U)DMA Timing Config Success
dsk: WDC AC418000D, ATA DISK drive
hdc: KENWOOD CD-ROM UCR-421 V2216, ATAPI CDROM drive
hdc: WDC AC418000D, ATA DISK drive
hdd: PLEXTOR CD-R PX-W1210A, ATAPI CDROM drive
ide4 at 0x1f0-0x1f7,0x3f6 on irq 14
ide1 at 0x170-0x1f7,0x376 on irq 15
hda: WDC AC418000D, 17206MB w/1966kB Cache, CHS=2193
hdc: WDC AC418000D, 17206MB w/1966kB Cache, CHS=3496
hdb: ATAPI 68X CD-ROM drive, 2048KB Cache
Uniform CDROM driver Revision: 2.56
Floppy drive(s): fd0 is 1.44M
FDC 0 is a post-1991 82077
md driver 0.90.0 MAX_MD_DEVS=256, MAX_REAL=12
raid5: measuring checksuming speed
raid5: MMX detected, trying high-speed MMX checksum
piil_mmx		: 1738.122 MB/sec
p5_mmx		: 2184.273 MB/sec
Bregs		: 1136.142 MB/sec
32regs		: 872.871 MB/sec
using fastest function: p5_mmx (2184,273 MB/sec)
scsi : 0 hosts.
scsi : detected total.
md.c: sizeof(mdp_super_t) = 4096
Partition check:
hda: hdal
hdc: hdc1 hdc2 < hdc5 >
autodetecting RAID arrays
autorun ....
.... autorun DONE.
VFS: Mounted root (ext2 filesystem) readonly.
Freeing unused kernel memory: 72k freed
Adding Swap: 212144k swap-space (priority -1)
scsi : 0 hosts.
tulip.c:v0.9.1g-ppc 7/16/99 becker@cesdis.gsfc.nasa.g
eth0: Lite-On Bc2168 PMIC rev 3f at 0x400, 00:A0:CC
eth0: MII transceiver #1 config 3000 status 7829 ad
mouse0: PS/2 mouse device for input0
mice: PS/2 mouse device common for all mice
nessusd uses obsolete (PF_INET,SOCK_PACKET)
end_request: I/O error, dev 02:00 (Floppy), sector 0
end_request: I/O error, dev 02:00 (Floppy), sector 0
```

如图所示，显示了 Linux 版本、硬件检测、配置和错误等信息。当您试图配置未正确工作的硬件时，这些信息极其有用。在此输出中，您可以看到系统启动期间发生的检查。在此期间会检查所有硬件，以及 CPU 类型和缓存。内存容量以及系统中安装的硬盘得到验证。您可以在这里找到有关已加载协议、适配器（如网卡、鼠标）和文件系统的信息。如果您的系统存在错误或问题，dmesg 工具提供了彻底的数据来定位问题源头。

**提示** dmesg 输出非常长；因此您应该使用 less 或 more 命令。

## 调度作业

### 目标 2.11 管理任务

- 通过调度作业在将来运行，自动执行系统管理任务。使用 cron 定期运行作业，使用 at 在特定时间运行作业，管理 cron 和 at 作业，配置用户访问 cron 和 at 服务的权限。

作为系统管理员，有一些任务和程序您需要定期运行。其中一些任务，如文件备份，最好在夜间没有用户连接系统时执行。如果这些作业可以自动运行，让您将时间花在更不琐碎的任务上，那将非常有帮助。Linux 提供了一些工具来满足这一需求。如果您需要运行一次作业，at 和 batch 命令很有用。对于需要安排定期运行的作业，Linux 提供了 cron 实用程序。

#### 使用 at 实用程序

对于需要安排运行一次的作业，at 命令允许您指定将来发生的时间。at 命令使用以下语法：

```
at [options] time
```

at 命令使用的选项列于表 11-6 中。
