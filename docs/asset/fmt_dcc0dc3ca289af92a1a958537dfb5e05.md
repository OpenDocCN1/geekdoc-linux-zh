
# /proc 文件系统条目说明

| 路径 | 描述 |
| :--- | :--- |
| `apm` | 关于高级电源管理的信息 |
| `cmdline` | 包含内核当前的位置 |
| `cpuinfo` | 关于计算机处理器的信息 |
| `devices` | Linux 系统当前使用的字符设备和块设备列表 |
| `execdomains` | 系统中进程的执行域列表；执行域允许进程以特定方式执行 |
| `fb` | Linux 系统使用的帧缓冲设备列表；通常包括视频适配器设备 |
| `filesystems` | Linux 内核支持的文件系统列表 |
| `interrupts` | 系统中使用的 `IRQ` 列表 |
| `iomem` | 包含当前使用的内存地址 |
| `iports` | 包含为设备保留的内存地址范围 |
| `isapnp` | Linux 系统中 `ISA` 插槽即插即用设备列表 |
| `kcore` | 代表计算机内部的物理内存；此文件不应被查看 |
| `dg` | 是内核消息的临时存储位置 |
| `ksys` | 包含用于加载模块的导出内核符号 |
| `loadavg` | 关于处理器的性能统计 |
| `locks` | 包含被内核锁的文件列表 |
| `mdstat` | 多磁盘 `RAID` 硬件的配置 |
| `meminfo` | 关于物理和虚拟内存的信息 |
| `misc` | 杂项设备列表（主设备数=10） |
| `modules` | Linux 内核当前加载的模块列表 |
| `mounts` | 当前挂载的文件系统列表 |
| `partitions` | 关于加载到内存中的分区表的信息 |
| `pci` | 关于 `PCI` 设备的信息 |
| `swap` | 关于交换分区的信息 |
| `scsi` | 关于 `SCSI` 设备的信息 |
| `version` | 包含内核版本 |

## 安装故障排除 339

正在校准延迟循环...73.00 `BogMIPS`

内存：381868k/393204k 可用 (1269k 内核代码, 8888k 预留, 90k 数据, 220k 中断, 0k 高内存)

`Dentry-cache` 哈希表条目: 65536 (order: 7, 524288 bytes)

`Inode-cache` 哈希表条目: 32768 (order: 6, 262144 bytes)

`Mount-cache` 哈希表条目: 8192 (order: 4, 65536 bytes)

`Buffer-cache` 哈希表条目: 32768 (order: 5, 131072 bytes)

`Page-cache` 哈希表条目: 131072 (order: 8, 1048576 bytes)

`CPU`：厂商初始化前，特性: 0183f9ff00000000000000，厂商: 0

`CPU`：L1 缓存: 16K, L1 数据: 16K

`CPU`：L2 缓存: 128K

支持 `Intel` 机器检查架构。

已启用 `Intel` 机器检查报告 `CPU#`。

`CPU`：厂商初始化后，特性: 0183f9ff0000000000000000

`CPU`：通用初始化后，特性: 0183f9ff0000000000000000

`CPU`：共同特性: 0183f9ff0000000000000000

`CPU`：`Intel` 赛扬 (Mendoza) 步进: 00

正在启用 `FPU` 保存和恢复...完成。

正在检查 `'hlt'` 指令... `OK`。

使用 `UNIX` 进行 `POSIX` 符合性测试

`mntr`: v1.40 (20010327) Richard Gooch (rgooch@atnf.csiro.au)

`mtr`: 检测到类型: `Intel`

`PCI`: `PCI BIOS` 版本 2.10 位于 0xf06d0，最后总线=1

`PCI`: 使用配置类型 1

`PCI`: 正在探测硬件

未知桥接资源 0: 假设为透明的

未知桥接资源 1: 假设为透明的

未知桥接资源 2: 假设为透明的

`PCI`: 在 00:04.0 使用 `IRQ` 请求 `PIIX` [0086/7110]

限制直接 `PCI/PCI` 传输。

`isapnp`: 正在扫描 `PnP` 卡卡...

`isapnp`: 正在调用 02:00 的查询

`isapnp`: `SB` 音频查询 - 增大端口范围

`isapnp`: 正在调用 02:02 的查询

`isapnp`: `E3B2` 查询 - 添加两个端口

`isapnp`: 卡卡 `'D-Link De-220P PNP ISA Card'`

`isapnp`: 卡卡 `'Creative SB AWE64 PnP'`

`isapnp`: 共检测到 2 个即插用卡

适用于 `Linux 2.4` 的 `Linux NET4.0`

基于斯康西大学计算机协会 `NET3.03`

初始化 `RT netlink` 套字

找到并启用简单启动标志扩展。

`apm`: `BIOS` 版本 1.22 标志 0x03 (驱动版本 1.14)

`mntr`: `scbios`: 进入

启动 `kaswap v1.8`

`VFS`: 磁盘配额厂商 `dquot 6.5.0` 已初始化

`pty`: 配置 2048 个 `Unix98 pts`

串口驱动程序版本 5.05c (2001-07-08)，带有 `MANY_PORTS`

`MULTIPORT SHARE_IRQ SERIAL_PCI ISAPNP` 已启用

# 第 7 章 高级安装

`tty00 = 0x03f8 (irq = 4)` 是 `16550A`

`tty01 = 0x02f8 (irq = 3)` 是 `16550A`

实时时钟驱动 v1.10

`block`: 队列扇区低 253208kb/122136kb，每队列 768 插槽

`RAMDISK` 驱动程序已初始化：16 个 `RAM` 磁盘，大小4096K

通用平台-EIDE 驱动版本: 6.31

`ide`: 为 33MHz `PCI` 总线使用 `PIO` 模式；覆盖 `idebus=xx`

`PIIX4`: `PCI` 总线 上的 `IDE` 控制器

`PIIX4`: 原生模式；稍后探测

`PIIX4`: 100% 原生模式

`ide-BM-DMA` 在 0xd800-0xd07，`BIOS` 设置: `hda:DMA, hdb:pio`

`ide-BM-DMA` 在 0xd08-0xdf，`BIOS` 设置: `hdc:DMA, hdc:DMA`

`hda`: `QUANTUM FIREDISK CX.4`, `ATA` 磁盘

`hdb`: `QUANTUM FIREDISK10c10`, `ATA` 磁盘

`dc`: `ATAPI CDROM`, `ATA/CD-ROM` 磁盘

`ide0` 在 0x01f0-0x177,0x3f6，`irq 14`

`ide1` 在 0x0170-0x177,0x376，`irq 15`

`da`: 12594960 扇区 (649 MB)，带 418K 缓存，784/255/63, `UDMA(33)`

`hdc`: 2004480 扇区 (1026 MB)，带 418K 缓存，885/16/63, `UDMA(33)`

`ide-floppy` 驱动程序:0.97

分区段: `hda: hda1 [2457/63] hdc1 hdc2 hdc3 hdc4 hdc5` = 软盘驱动器: `fd0` 是 1.4M

`ide-floppy` 驱动程序:0.97

`md: md 0 MAX_DEVS=256, MD_DISKS=27`

`md: 自动检测 raid`

`md: 完成`

`Net: Linux TCP/IP`

`IP` 协议: `ICMP, UDP, TCP`

`IP: 4096` 桶路由表，32K

`TCP: 哈希表 (已建立 32768)`

`Linux 4.0` 的 `SMP` 多播套接字 0.0

`RAMDISK`: 块 0 处的压缩镜像

释放 `initrd` 内存:319k

`VFS`: 挂载根 (`ext2`) 文件系统

日志设备已加载

`EXT3-fs: 以顺序挂载`

释放未使用内存:220k

添加交换:51407k (优先级 -1)

`usb: 已注册 userfs`

`usb-uhci: 已注册新集线器`

`usb-uhci.c: 版本 1.25 时间 17:36:49 2001`

`usb-uhci.c: 已启用高带宽`

`PCI: 为设备 00:04.0 找到 IRQ 10`

`usb-uhci.c: I/O 0x0400 上的 UHCI，IRQ 10`

`usb-uhci.c: 检测到 2 个端口`

`usb: 新总线已注册，分配总线号 1`

`hub: 检测到 2 个端口`

`usb-uhci.c: v2.51: 通用主机控制器驱动程序`

`EXT3 FS: 2.4.0.8, 2001年8月25日，于 (22,2)，内部日志`

日志启动。提交间隔 5 秒

`EXT3 FS: 2.4.0.8, 2001年8月25日，于 (22,1)，内部日志`

`ext3-fs: 以顺序数据挂载`

日志启动。提交间隔 5 秒

`EXT3 FS: 2.4.0.8, 2001年8月25日，于 (22,5)，内部日志`

`ext3-fs: 以顺序数据挂载`

```
078: FIFO 为 16 字节
078: 写阈值为 9
078: 阈值为 8 位
078: 中断为 ISA 脉冲
078: ECP 端口 cfgA=0x010 cfgB=0x48
078: ECP 设置 irq=7=常用或其他方法
```
