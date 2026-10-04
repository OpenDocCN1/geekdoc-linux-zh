
# BIOS-e820 内存映射

```
BIOS-e820: 000000000ffb0000 - 00000000010000 (reserved)
```

OMB HIGHMEM. 247MB LOWMEM.

zapping low mappings.

Node 0 totalpages:63472

DMA zone: 4096 pages, FIFO:14

Normal zone: 59376 pages, LIFO:31

Highmem: 0 pages, FIFO:1

DMI present.

# ACPI 表

```
ACPI: RSDP (v000) @0x000f6d0
ACPI: RSDT (v000) 0x4230e231 0x000000 @0x7f300
ACPI: FADT (v001) 0x4230e231 0x000000 @0x7f00
ACPI: MADT (v001) 0x4230e231 0x000000 @0x7f6d0
ACPI: DSDT (v001) 0x4230e231 0x010000 @0x7f00
```

ACPI: PM-Timer IO Port: `0x408`

Built 1 zonists

Kernel command line: `ro root=/ quiet`

mapped 4G trampoline to `fff4000`.

# CPU 初始化

Initializing CPU

CPU 0 irqstacks, hard=`023d4000` soft=`023d4000`

PID hash table entries: 1024 (order: 10, 16384 bytes)

Detected `2794.983 MHz` processor.

Using tsc for high-res

Console: colour VGA+80x25

Dentry cache hash table entries: 32768 (order: 5, 131072 bytes)

Inode-cache hash table entries: 16384 (order: 4, 65536 bytes)

Memory: `247368k/253888k` available (`2068k` kernel code, `5836k` reserved, `647k` data, `144k` init, `0` highmem)

Calibrating delay loop... `5521.40 BogoMIPS` (lpj=`2760704`)

Security Scaffold v1.0.0 initialized

SELinux: Initializing.

SELinux: Starting in permissive mode

There is already a security framework initialized, register_security failed.

selinux_register_security: Registering security module capability

Capability LSM initialized as secondary

Mount-cache hash table entries: 512 (order: 0, 4096 bytes)

CPU: After generic identify, caps: `bfebbfff 00000000 00000000 00000000`

CPU: After vendor identify, caps: `bfebfbbf 00000000 00000000 00000000`

monitor/wait feature present.

using wait in idle threads.

CPU: Trace cache: `12K` oops, L1 cache: `16K`

CPU: L2 cache: `1024`

CPU: After all inits, caps: `bfebf3ff 00000000 00000000 00000000`

Intel machine architecture supported.

Intel machine architecture reporting enabled on CPU.

CPU0: Intel P4/Xeon identified MCE MSRs (`12`) available

CPU1: Intel(R) Pentium(R) `2.80GHz` stepping `0`

Enabling fast FPU save and restore... done.

unmasked SIMD FPU support... done.

Checking 'hit' instruction... OK.

ACPI: IRQ Level Trigger.checking image is itfs...

Freeing intrd memory: `387k` freed

# 总线与驱动初始化

NET: Registered family `16`

PCI: BIOS revision `2.1` entry at `0xfb4c`, last bus=`0`

PCI: Using type v2.051

ACPI: Subsystem revision `2004`

ACPI: Using PIC for interrupt

ACPI: Root Bridge [`PCI0`] (`00:00`)

PCI: Probing hardware (bus `00`)

PCI: Ignoring BAR-3 of IDE controller `0000:0f.1`

PCI: Transparent bridge - `0000:0e.0`

ACPI: PCI Interrupt Table [`SB_PCI0_PRT`]

ACPI: PCI Interrupt Table [`SB_PCI0.HUB_PRT`]

ACPI: PCI Interrupt Link [`LNKA`] (IRQs `3 4 5 9 10 14`)

ACPI: PCI Interrupt Link [`LNKB`] (IRQs `3 4 5 9 10 14`)

ACPI: PCI Interrupt Link [`LNKC`] (IRQs `3 4 5 9 10 14`)

ACPI: PCI Interrupt Link [`LNKD`] (IRQs `3 4 5 9 10 14`)

ACPI: PCI Interrupt Link [`LNKE`] (IRQs `3 4 5 9 10 14`)

ACPI: PCI Interrupt Link [`LNKF`] (IRQs `3 4 5 9 10 14`)

ACPI: PCI Interrupt Link [`LNKI`] (IRQs `3 4 5 9 10 14`)

apm: BIOS version `1.2` Flags `0x07` (Driver version `1.16ac`)

pm: overridden by ACPI.

audit: initializing network socket (disabled)

audit(`11d295b8033.823:0`): initialized

Total TLB memory allocated, `0`

VFS: Disk quotas `dquot_6.5`

Dquot-cache hash table entries: 1024 (order 0, 4096 bytes)

Linux:Initializing Cryptographic API

ksign: Installing public key data

Loading keyring

- Added public key `6ECDA687281A73E5`
- User ID: Red Hat, Inc. (Kernel Module GPG key)

pci_hotplug: PCI Hot Plug PCI Core version: `0.5`

vesafb: probe of vesafb failed with error `-6`

# Linux 简介：安装与编程

ACPI: 风扇 [`FAN`] (已开启)

ACPI: 处理器 [`CPU0`] (支持 C1, 2 个节流状态)

ACPI: 温度区域 [`THRM`] (`56 C`)

isapnp: 正在扫描 PnP 卡...

isapnp: 未找到即插用设备

实时时钟驱动程序 v1.12

Linux appgart interface v0.100 (c) Dave Jones

appgart: 检测到 Intel 845G 芯片组。

appgart: 用于 agpg内存的最大主内存: `196M`

appgart: 检测到 `8060K` 被盗占内存。

appgart: AGP 窗口为 `128M` @ `0xd8000000`

serie: `18042` AUX 端口位于 `0x60,0x64` irq `12`

serie: `18042` KBD 端口位于 `0x60,0x64` irq `1`

Serial: 8250/16550 驱动版本: `1.9` `$8` 端口，已启用 IRQ 共享

tty0 I/O `0x3fb` (irq = `4`) 为 16550A

RAMDISK 驱动程序初始化: `16` 个大小为 `16384K`、块大小为 `1024` 的磁盘

divert: 未为非以太设备分配 `divert_blk`

统一多平台 E-IDE 驱动程序版本: `7.00alpha2`

ide: 为 PI 模式使用 `33MHz` 系统总线；用 `idebus=xx` 覆盖

ICH4: PCI 插槽 `0000:00:1f.1` 处的 IDE 控制器

ACPI: PCI_interrupt `0000:00:11f.1[A]` -> GSI `9` (电平, 低) -> IRQ `9`

ICH4: 芯片组版本 `2`

ICH4: 非 100% 原生模式：稍后将探测 irqs

ide0: `0x0f00-0xf0f7` 处的 BM-DMA，BIOS 设置 hda:DMA, hdb:DMA

ide1: `0x0f08-0xf0f8` 处的 BM-DMA，BIOS 设置 hdc:pio, hdb:pio

正在探测 IDE 接口 ide0...

hda: SAMSUNG SP0411N, ATK DISK 驱动器

hdb: SAMSUNG CDRW/DVD SM-352F, ATAPI CD/DVD-ROM 驱动器

使用 cfq 调度器

ide0 `0x11f0-0x1f7,0x33f6` 位于 irq `14`

正在探测 IDE 接口 ide1...

正在探测 IDE 接口 ide1...

正在探测 IDE 接口 ide2...

ide2: 探测前等待就绪失败！

正在探测 IDE 接口 ide3...

ide3: 探测前等待就绪失败！

ide4: 探测前等待就绪失败！

ide5: 探测前等待就绪失败！

# Debian Linux 安装指南

hda: 最大请求大小: `1024KIB`

hda: `78242976` 扇区 (`40060 MB`) 带有 `2048KIB` 缓存, ChS=`16383/255/63`, UDMA(`100`)

hda: 支持缓存刷新

hda: hda1 hda2 < hda5 hda6 hda7 hda8 >

hdb: ATAPI `52X` DVD-ROM 读写驱动器, `2048kB` 缓存, UDMA(`33`)

统一 CD-ROM 驱动程序版本: `3.20`

ide-floppy 驱动 `0.99.newide`

usbcore: 注册新驱动 `hiddev`

usbcore: 注册新驱动 `usbdid`

drivers/usb/input/hid-core: v2.0:USB HID 核心驱动

mice: 所有鼠标的 PS/2 鼠标命令

input: `isa00060/serio0` 上的 AT 翻译 2 键绑定

input: `isa00060/serio1` 上的 PS/2 通用鼠标

md: md 驱动程序 `0.90.0` MAX_MD_DEVS=`26`, MD_SB_DISKS=`27`

NET: 已注册协议族 `2`

IP: 路由缓存哈希大小为 `512` 桶，`16`字节

TCP: 已配置哈希表（已 `16384` 绑定 `4681`）

初始化 IPsec 网络套接字

NET: 已注册协议族 `1`

NET: 已注册协议族 `17`

ACPI: (支持 S0 S1 S4 S5)

ACPI: 唤醒设备

LPB PCI HUBO UAR1 USB0 USB1 USB2 USB3 MODM

释放未使用的内核内存: `144k`

kjournal 启动。提交间隔 `5` 秒

EXT3-fs: 挂载了有序数据模式的文件系统。

SELinux: 运行时禁用。

SELinux: 正在注销 netfilter 钩子

为 `2.6.9-1.667` 插入软盘驱动

软驱器(s): fd0 为 `1.44M`

FDC 0 是 `1991` 年后的 82077

sis900.c: v1.08.07 `11/02/2003`

ACPI: PCI 中断 `0000:01:06.00[A]` -> GSI `11` (电平, 低) -> IRQ `11`

divert: 为 eth0 分配 `divert_blk`

eth0: 地址 `1` 处的 SIS 900 MII

eth0: `0x000` 处的 SIS 900 以太网, `00:1f.5`

ACPI: PCI 中断 `0000:000:1f.5[B]` -> GSI `5` (电平, 低) -> IRQ `5`

PCI: 设置设备 `0000:00:1f.5` 的延迟定时器为 `64`

intel8x0 测量值为 `4926`

intel8x0 时钟为 `48000`

ACPI: PCI 中断 `0000:01:d.7[D]` -> GSI `3` (电平, 低) -> IRQ `3`

ehci_hcd `0000:01:d.7`: EHCI 控制器

PCI: 设置设备 `0000:01:d.7` 的延迟定时器为 `64`

ehci_hcd `0000:01:d.7`: irq `3`, pci 内存 `121200`

ehci_hcd `0000:01:d.7`: 已注册 USB, 分配总线 `1`

PCI: 设备 `0000:01:d.7` 不支持 `128` 缓存大小

ehci_hcd `0000:01:d.7`: USB 2, EHCI 1.0, 驱动 `2004-10`

hub `0-1.0`: USB 集线器

hub `0-1.1`: `4` 端口

USB 通用接口 v2.2

ACPI: PCI 中断 `0000:00:01d[A]` -> GSI `10` (电平, 低) -> IRQ `10`

uhci_hcd `0000:00:01d.0`: UHCI 控制器

PCI: 设置设备 `0000:00:01d.0` 的延迟定时器为 `64`

uhci_hcd `0000:00:01d.0`: irq `10`, I/O 基础 `0000d800`

uhci_hcd `0000:00:01d.0`: 已注册 USB, 分配总线 `2`

hub `2-0.1`: USB 集线器

hub `2-0.1`: `2` 端口

ACPI: PCI 中断 `0000:00:01d[B]` -> GSI `11` (电平, 低) -> IRQ `11`

uhci_hcd `0000:00:01d.1`: UHCI 控制器

PCI: 设置设备 `0000:00:01d.1` 的延迟定时器为 `64`

uhci_hcd `0000:00:01d.1`: irq `11`, I/O 基础 `0000d000`

uhci_hcd `0000:00:01d.1`: 已注册 USB, 分配总线 `3`

hub `3-0.1`: USB 集线器

hub `3-0.1`: `2` 端口

ACPI: PCI 中断 `0000:00:01d.2[C]` -> GSI `9` (电平, 低) -> IRQ `9`

uhci_hcd `0000:00:01d.2`: UHCI 控制器

PCI: 设置设备 `0000:00:01d.2` 的延迟定时器为 `64`

uhci_hcd `0000:00:01d.2`: irq `9`, I/O 基础 `0000a400`

uhci_hcd `0000:00:01d.2`: 已注册 USB, 分配总线 `4`

hub `4-0.1`: USB 集线器

hub `4-0.1`: `2` 端口

md: 自动检测 RAID 阵列。

md: 自动运行 ...

md: 自动运行完成。

NET: 已注册协议族 `10`

在设备 `02369a00(lo)` 上禁用隐私扩展

IPv6 over IPv4 隧道驱动

divert: 未为非以太设备分配 `divert_blk`

ACPI: 电源按钮 (FF) [`PWRF`]

ACPI: 睡眠按钮 (CM) [`SLPB`]

hda1 上的 EXT3 FS，内部日志

device-mapper: `4.1.0-ioctl` (`2003-12-10`) 初始化: dm@uk.sistina

cdrom: 失败。

EXT2-fs 交换 (设备 hdc7): ext2_fill_super: 挂载 ext3 文件系统为 ext2

在 `/dev/hda8` 上添加 `522072k` 交换分区。优先级:-1 区域:1

port0: `0x37` (`0x778`) 处的 PC 样式 [`PCSPP,TRISTATE,EPP`]

port0: irq `7`

ip_tables: (C) 2000-202 版本 `1983` 桶，每个连接跟踪 `356` 字节

eth0: 媒体链路 `100mbps` 全双工

# lspci 命令示例

`lspci` 命令显示系统中所有的 PCI 总线及其连接的所有设备。这些信息在调试时非常有用。例如，以下输出是我的机器的。

```
00:00.0 桥接: Intel Corp. 8245AG/Brookdale-GE (集成) (显示)
00:00.2 显卡: Intel Corp. 8245AG/Brookdale-GE (集成) (显示)
00:00:1f.0 控制器: Intel Corp. 82801/DBL-DBM (ICH4) (USB1)
00:00:1f.1 控制器: Intel Corp. 82801/DBL-DBM (ICH4) (USB22)
00:00:1f.2 控制器: Intel Corp. 82801/DBL-DBM (ICH4) (USB3)
00:00:1f.5 控制器: Intel Corp. 82801/DBL-DBM (ICH4) (USB4)
00:01:06.0 控制器: Silicon Systems [SIS] Sis900 PCI Fast以太网
```
