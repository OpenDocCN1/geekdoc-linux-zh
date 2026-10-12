
此驱动程序允许您拥有一个虚拟网络接口设备，您可以用它来欺骗网络客户端程序。将其作为模块保留可能会很方便；因此，建议采用默认值。

- EQL（串行线路负载均衡）支持 [CONFIG_EQUALIZER] [N/y/m/?]
- 以太网（10 或 100Mbit） [CONFIG_NET_ETHERNET] [Y/n/?]

以下问题的答案取决于您拥有的网卡类型；请据此回答：

- 3COM 网卡 [CONFIG_NET_VENDOR_3COM] [N/y/?]
- AMD LANCE 和 PCnet (AT1550 和 ME1200) 支持 [CONFIG_LANCE] [N/y/m/?]
- Western Digital/SMC 网卡 [CONFIG_NET_VENDOR_SMC] [N/y/?]
- Racal-Interlan (NI) 网卡 [CONFIG_NET_VENDOR_RACAL] [N/y/?]
- 其他 ISA 网卡 [CONFIG_NET_ISA] [N/y/?]
- EISA、VLB、PCI 和板载控制器 [CONFIG_NET_EISA] [Y/n/?]
- AMD PCnet32 (VLB 和 PCI) 支持 [CONFIG_PCNET32] [N/y/m/?]
- Apricot Xen-II 板载以太网 [CONFIG_APRICOT] [N/y/m/?]
- CS89x0 支持 [CONFIG_CS89x0] [N/y/m/?]
- 通用 DECchip 和 DIGITAL EtherWORKS PCI/EISA [CONFIG_DE4X5] [N/y/m/?]
- DECchip tulip (dc21x4x) PCI 支持 [CONFIG_DEC_ELCEP] [N/y/m/?]
- Digi Intl. RightSwitch SE-X 支持 [CONFIG_DIGI_RIGHTSWITCH] [N/y/m/?]
- EtherExpressPro/100 支持 [CONFIG_EXPRESS_PRO100] [Y/n/m/?]
- PCI ME2000 支持 [CONFIG_ME2K_PCI] [N/y/m/?]
- TI ThunderLAN 支持 [CONFIG_TLAN] [N/y/m/?]
- VIA Rhine 支持 [CONFIG_VIA_RHINE] [N/y/m/?]
- 便携式适配器 [CONFIG_NET_POCKET] [N/y/?]
- FDDI 驱动支持 [CONFIG_FDDI] [N/y/?]
- 帧中继 DLCI 支持 [CONFIG_DLCI] [N/y/m/?]
- PPP（点对点）支持 [CONFIG_PPP] [N/y/m/?]
- SLIP（串行线路）支持 [CONFIG_SLIP] [N/y/m/?]
- 无线局域网（非业余无线电） [CONFIG_NET_RADIO] [N/y/?]

- 令牌环驱动支持 [CONFIG_TR] [N/y/?]
- Control Hostess SV-11 支持 [CONFIG_HOSTESS_SV11] [N/m/?]
- COSA/RAP 同步串口板支持 [CONFIG_COSA] [N/m/?]
- Red Creek 硬件 VPN (实验性) [CONFIG_RPCPI] [N/y/m/?]
- WAN 驱动 [CONFIG_WAN_DRIVERS] [N/y/?]
- 以太网 LAP 驱动 [CONFIG_LAPETHERNET] [N/y/m/?]
- X.25 异步驱动 [CONFIG_X25_ASY] [N/y/m/?]

## 业余无线电、ISDN 和旧版 CD-ROM 支持

我假设您不打算使用业余无线电、ISDN 或旧版 CD-ROM 支持；因此，以下问题的默认答案已足够：

- 业余无线电支持 [CONFIG_HAMRADIO] [N/y/?]
- ISDN 支持 [CONFIG_ISDN] [N/y/m/?]
- 非 SCSI/IDE/ATAPI CDROM 驱动器支持 [CONFIG_CD_NO_IDESCSI] [N/y/?]

## 注意

![](img/f9ec99365f159bfe663f8ac29732663c_526_0.png)

如果您计划使用 ISDN 网卡为服务器提供互联网连接，我强烈建议您购买 ISDN 路由器，而不是内置网卡。我使用内置网卡的经验让我得出了这个结论。我试过几个知名品牌的 ISDN 网卡，它们工作得并不理想。除了要处理另一张网卡的问题（PC 上的 IRQ 和 I/O 地址资源是有限的），当您考虑到专用 ISDN 本身在美大部分地区都是一项相当昂贵的服务时，内置网卡和外置 ISDN 路由器之间的价格差异并不显著。

## 字符设备

在本节中，您将被询问关于终端配置的问题。

- 虚拟终端 [CONFIG_VT] [Y/n/?]

此功能允许您拥有虚拟终端。除非您是在嵌入式 Linux 系统中安装内核，否则需要默认答案。

- 虚拟终端上的控制台支持 [CONFIG_VT_CONSOLE] [Y/n/?]

此功能允许您将虚拟终端变为系统控制台。出于与上一个答案相同的原因，这是必需的。

- 串口上的控制台支持 [CONFIG_SERIAL_CONSOLE] [N/y/?]

如果您想使用计算机的串口作为系统控制台，请更改默认答案。

- 扩展哑串口驱动选项 [CONFIG_SERIAL_EXTENDED] [N/y/?]

除非您在上一个问题中启用了串口作为系统控制台，否则请保持此处的默认值。

- Unix98 PTY 支持 [CONFIG_UNIX98_PTYS] [Y/n/?]

此功能提供对 UNIX 98 伪终端编号约定的支持，该约定优于传统的 Linux 伪终端编号约定。您应该保持默认值。

如果您保持默认值，将会被问到以下问题以设置系统可使用的最大 UNIX 98 PTY 数量：

- 最大 Unix98 PTY 使用数量 (0-2048) [CONFIG_UNIX98_TTY_COUNT] [256]

在大多数情况下，默认值应该足够。

- 鼠标支持（非串口鼠标） [CONFIG_MOUSE] [Y/n/?]

此功能允许您在能够使用此类设备的终端上使用鼠标。建议采用默认值。

- QIC-02 磁带支持 [CONFIG_QIC02_TAPE] [N/y/m/?]

如果您有 QIC-02 磁带驱动器，可以选择在此处添加对它的支持。

- 看门狗定时器支持 [CONFIG_WATCHDOG] [N/y/?]

如果您想创建一个看门狗定时器，以便在发生故障时重新启动系统，请在此回答 yes。如果您启用此功能，必须使用 mknod 程序创建一个名为 /dev/watchdog 的特殊设备（主设备号,次设备号=130,10）。然后，您可以使用一个看门狗守护进程程序，每分钟向该特殊设备写入一次。如果内核检测到守护进程一分钟内未向设备写入，它将重新启动系统。

- /dev/nvram 支持 [CONFIG_NVRAM] [N/y/m/?]

此功能允许您创建特殊设备 /dev/nvram，以对实时时钟中的非易失性内存进行读写访问。除非您知道自己在做什么，否则请保持默认值。

- 增强型实时时钟支持 [CONFIG_RTC] [N/y/?]

此功能允许您创建一个特殊设备 /dev/rtc，用于访问系统中的实时时钟。除非您知道自己在做什么，否则请保持默认值。

## 视频和游戏杆支持

因为您正在配置服务器系统，我假设系统上没有视频采集硬件或游戏杆；因此，您应该接受以下问题的默认答案：

- Video For Linux [CONFIG_VIDEO_DEV] [N/y/m/?]
- 游戏杆支持 [CONFIG_JOYSTICK] [N/y/m/?]

## Ftape，软盘磁带设备驱动程序

如果您有基于软盘控制器的磁带驱动器，需要选择在此处添加对它的支持。

- Ftape (QIC-80/Travan) 支持 [CONFIG_FTAPE] [N/y/m/?]

## 文件系统

在本节中，您将为各种特定于文件系统的功能配置内核。

- 配额支持 [CONFIG_QUOTA] [N/y/?]

如果您希望内核内建磁盘配额支持，请在此选择 yes。

- 内核自动挂载器支持 [CONFIG_AUTOFS_FS] [Y/y/n/m/?]

如果您希望远程文件系统（如 NFS 文件系统）自动挂载和卸载，请选择在此处添加对自动挂载器的直接支持或基于模块的支持。

以下是各种特定于供应商的文件系统支持问题。请根据您的需求回答：

- Amiga FFS 文件系统支持 [CONFIG_AFFS_FS] [N/y/m/?]
- Apple Macintosh 文件系统支持 (实验性) [CONFIG_HFS_FS] [N/y/m/?]
- DOS FAT 文件系统支持 [CONFIG_FAT_FS] [N/y/m/?]
- ISO 9660 CDROM 文件系统支持 [CONFIG_ISO9660_FS] [N/y/m/?]
- Microsoft Joliet CDROM 扩展 [CONFIG_JOLIET] [N/y/?]
- Minix 文件系统支持 [CONFIG_MINIX_FS] [N/y/m/?]
- NFS 文件系统支持 (只读) [CONFIG_NFS_FS] [N/y/m/?]
- OS/2 HPFS 文件系统支持 (只读) [CONFIG_HPFS_FS] [N/y/m/?]
- /proc 文件系统支持 [CONFIG_PROC_FS] [Y/n/?]

/proc 文件系统是任何现代 Linux 系统的必备项；因此，强烈建议采用默认答案。

- 用于 Unix98 PTYs 的 /dev/pts 文件系统 [CONFIG_DEVPTS_FS] [Y/n/?]

如果您选择添加对 UNIX 98 伪终端的支持，则需要在此处添加 /dev/pts 文件系统支持。

- ROM 文件系统支持 [CONFIG_ROMFS_FS] [N/y/m/?]

大多数系统不需要此类文件系统。

- 第二扩展文件系统支持 [CONFIG_EXT2_FS] [Y/m/n/?]

扩展文件系统是 Linux 的主要文件系统；因此，默认答案是必须的。

以下问题的默认答案适用于大多数系统：

- System V 和 Coherent 文件系统支持 [CONFIG_SYSV_FS] [N/y/?]
- UFS 文件系统支持 [CONFIG_UFS_FS] [N/y/m/?]

请注意，如果您选择挂载由其他操作系统（如 Solaris x86 或 BSD）创建的磁盘分区，则需要 UFS 文件系统支持。
