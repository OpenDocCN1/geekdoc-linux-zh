
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

如图所示，显示了 Linux 版本、硬件检测、配置和错误等信息。当您试图配置未正确工作的硬件时，这些信息极其有用。在此输出中，您可以看到系统启动期间发生的检查。在此期间会检查所有硬件，以及 CPU 类型和缓存。内存容量以及系统中安装的硬盘得到验证。您可以在这里找到有关已加载协议、适配器（如网卡、鼠标）和文件系统的信息。如果您的系统存在错误或问题，`dmesg` 工具提供了彻底的数据来定位问题源头。

**提示** `dmesg` 输出非常长；因此您应该使用 `less` 或 `more` 命令。

### 调度作业

#### 目标 2.11 管理任务

- 通过调度作业在将来运行，自动执行系统管理任务。使用 `cron` 定期运行作业，使用 `at` 在特定时间运行作业，管理 `cron` 和 `at` 作业，配置用户访问 `cron` 和 `at` 服务的权限。
