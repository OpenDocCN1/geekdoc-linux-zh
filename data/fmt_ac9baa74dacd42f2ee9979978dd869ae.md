
## SCSI 控制器

- ATA PIO (DPT PM201) (`CONFIG_SCSI_PIO`) [M/n/y/?] n
- ISA/EISA/PCI 和通用 ISA/DMA (`CONFIG_SCSI_ISA`) [M/n/y/?] n
- Future Domain xx (`CONFIG_SCSI_FUTURE_DOMAIN`) [M/n/y/?] n
- Generic NCR5380 (`CONFIG_SCSI_GENERIC_5380`) [M/n/y/?] n
- NCR53c40 (`CONFIG_SCSI_NCR53C40`) [M/n/y/?] n
- Parallel Port (`CONFIG_SCSI_PPA`) [M/n/y/?] n
- PAS16 (`CONFIG_SCSI_PAS6`) [M/n/y/?] n
- Qlogic FAS (`CONFIG_SCSI_QLOGIC_FAS`) [M/n/y/?] n
- Seagate ST-02 Future Domain (`CONFIG_SCSI_SEAGATE`) [M/n/y/?] n
- Trantor T128 (`CONFIG_SCSI_T28`) [M/n/y/?] n

在本节中，你将列出你拥有的 SCSI 控制器或其他网卡。这个问题涉及到 Linux 支持的特殊设备。

## 网络设备

- 网络设备支持 (`CONFIG_NETDEVICE`) [Y/n/?] y
- Dummy 驱动支持 (`CONFIG_DUMMY`) [M/n/y/?] y
- EQ 负载均衡 (`CONFIG_EQUAL`) [M/n/y/?] n

EQ 是一种使用单根并行线连接两台机器的方法。你可能不需要。

- PLIP（并行端口）支持 (`CONFIG_PLIP`) [M/n/y/?] n

PLIP 带有并行线。再次，这可能是好主意。

- PPP（点对点）支持 (`CONFIG_PPP`) [M/n/y?] y

CCP 压缩器仅以模块形式构建。

PPP 是互联网服务提供商和其他人常用的流行的串口协议。

- SLIP（串口）支持 (`CONFIG_SLIP`) [M/n/y?] n

SLIP 是一种过时的 PPP 协议。如果没有请不要使用。

- 无线网络接口 (`CONFIG_NET_RADIO`) [M/n/y?] n

如果你在使用数据包无线且系统中有一个网卡，请选 Yes。

- 以太网（10 或 100Mbit）(`CONFIG_NET_ETHERNET`) [Y/n/y?] y

如果你有以太网卡，请选 Yes。

- 3COM 卡 (`CONFIG_NET_VENDOR_3COM`) [Y/n/y?] y
  - 3c501 支持 (`CONFIG_EL1`) [M/n/y?] n
  - 3503 支持 (`CONFIG_EL2`) [M/n/y?] n
  - 3509/3579 支持 (`CONFIG_EL3`) [M/n/y?] y
  - 3590 系列（592/595/597）“Vortex”支持 (`CONFIG_VORTEX`) [M/n/y?] n
- AMD LANCE 和 PCnet (AT1500 和 NE2100) (`CONFIG_LANCE`) [Y/n/y?] n
- 西数据/SMC 卡 (`CONFIG_NET_VENDOR_SMC`) [Y/n/y?] n
- 其他 ISA 卡 (`CONFIG_NET_ISA`) [Y/n/y?] n
- EISA, VLB, PCI 和板载控制器 (`CONFIG_NET_EISA`) [Y/n/y?] n
- 口袋和便携适配器 (`CONFIG_NET_POCKET`) [Y/n/y?] n
- 令牌环驱动支持 (`CONFIG_TR`) [Y/n/y?] n
- FDDI 驱动支持 (`CONFIG_FDDI`) [N/n/y?] n
- Arcnet 支持 (`CONFIG_ARCNET`) [M/n/y?] n

在这里，你列出你拥有的以太网或其他网卡。

## ISDN 子系统

ISDN 支持 (`CONFIG_ISDN`) [M/n/y?] n

如果你有 ISDN，你需要在这里配置。

## CD-ROM 驱动程序

支持非 SCSI/IDE/ATAPI CDROM 驱动器 (`CONFIG_CD_NO_IDESCSI`) [Y/n?]

| Format | Comments |
| :--- | :--- |
| DOS FAT | 这是 MS-DOS 和 Windows 95 系统支持的基础。 |
| MSDOS | MS-DOS 风格的文件系统。 |
| VFXT | Windows 95 风格的文件系统。 |
| umsdos | 该文件系统使用 MS-DOS 文件系统，提供 Linux 风格的命名和保护。这是一种临时方案（hack），可能不会被使用。 |

/proc 文件系统支持 (`CONFIG_PROC_FS`) [Y/n/?] y

`/proc` 文件系统通过特殊文件访问内核信息。它非常有用，所以你应该对此问题回答 Yes。

NFS 文件系统支持 (`CONFIG_NFS_FS`) [Y/m/n/?] y

NFS 上的根文件系统 (`CONFIG_ROOT_FS`) [N/y/?] n

如果你想将计算机配置为 NFS 客户端，必须启用 NFS 文件系统支持。你也可以将根目录设置在未适配的 NFS 分区上。

SMB 文件系统支持（用于挂载 WfW 等）(`CONFIG_SMB_FS`) [M/n/y/ ] n

SMB 文件系统在你需要挂载 NT 或 Windows 组共享资源时非常有用。

ISO09660 cd-rom 文件系统支持 (`CONFIG_ISO09660_FS`) [Y/m/n/?] y

如果你有 CD-ROM，你需要能够处理 CD-ROM 格式（ISO-ISO9660）文件系统。

OS/2 HPFS 文件系统支持（只读） (`CONFIG_HPFS_FS`) [M/n/y/?] n

System V 和 Coherent 文件系统支持 (`CONFIG_SYSV_FS`) [M/n/y/?] n

UFS 文件系统支持（只读） (`CONFIG_UFS_FS`) [M/n/y/?] n

最后三个文件系统涉及 OS/2 操作系统、System-V UNIX 和 UFS（Berkeley UNIX、SunOS、SOLARIS）。如果你计划使用这些类型的文件系统，请启用它们。

## 字符设备

- 标准/通用串口支持 (`CONFIG_SERIAL`) [Y/m/n/?] y

### 构建新内核

如果你正在使用串口或调制解调器，则需要启用内核对它们的支持。

Digibord PC/Xx 支持 (`CONFIG_DIGI`) [N/y/] n

Cyclades 异步复用器支持 (`CONFIG_CYCLES`) [M/y/] n

Stallion 多端口串口支持 (`CONFIG_STALDRV`) [N/y/] n

SDL RISCom/8 卡支持 (`CONFIG_RISCOM8`) [M/y/] n

Linux 支持多种串口接口卡。请确定你正在使用的哪些板卡。

并行打印机支持 (`CONFIG_PRINTER`) [M/y/] y

如果你使用并行端口，你需要此驱动程序。

鼠标支持（非串口鼠标） (`CONFIG_MOUSE`) [Y/n/] n

如果你有串口鼠标，则不需要此驱动程序。其他类型的鼠标（如总线鼠标）需要该驱动程序。

用户杂杂项设备模块支持 (`CONFIG_UMISC`) [N/y/] n

如果你需要支持非常奇特的设备（如手写笔或触摸屏），请回答 Y。

QIC-02 带支持 (`CONFIG_QICO2_TAPE`) [N/y/] n

Ftape (QIC-80/Travan) 支持 (`CONFIG_FTAPE`) [M/y/] y

这些选项配置了对某些磁带设备的支持。这些设备中的每个都支持特定类型的磁带（与 SCSI 设备带不同，后者支持多种磁带）。

- 在 `./drivers/char/ftape/Makefile` 中为 ftape 设置 IObase/IRQ/DMA

高级电源管理 BIOS 支持 (`CONFIG_APM`) [N/y/] n

如果你有笔记本电脑，电源管理是很有用的。否则，它将不起作用。

看门定时器支持 (`CONFIG_WATCHDOG`) [N/y/] n

如果你的系统绝对、绝对必须运行，你就你需要一个看门定时器。它是什么？它是一个必须在你打开后至少每一分钟写入一次的设备。在定时器运行时如果未写入，计算机将重置。如果你的程序崩溃并未能滴答该设备，计算机将重置。希望你已经配置了启动脚本来重启程序并保持运行。

该设备对于一直运行的应用程序非常有用。

## 增强型实时时钟支持

增强型实时时钟支持 (`CONFIG_RTC`) [N/y/?] n

每台 PC 都有一个可编程的实时时钟。此驱动程序通过 `/dev/rtc` 文件访问该设备。如果你有需要此功能的应用程序，请启用此设备。

## 音频

声卡支持 (`CONFIG_SOUND`) [Y/n/m/?] n 回答 Yes。配置过程随后会询问你细节。
