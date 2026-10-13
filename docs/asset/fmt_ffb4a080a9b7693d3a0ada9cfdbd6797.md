
首先将项目存档拷贝到 `/usr/src` 目录，然后移动到 `/usr/src` 并解压 `linux-v2_2_14-0w2.tar.gz` 存档，然后返回 `/usr/src` 并使用 `linux-v2_2_14-0w2.diff` 文件补丁我们的内核。`linux-v2_2_14-0w2.diff` 包含了补丁，我们从补丁移除所有文件。

**注意**：所有与 `linux-v2_2_14-0w2` 补丁相关的安全消息都应该记录在 `/var/log/messages` 文件中。

内核的补丁步骤已完成。现在按照剩余部分构建 Linux 内核并重启。

## 编译

确保 `/usr/include/asm`、`/usr/include/linux` 和 `/usr/include/scsi` 子目录是内核核心的软链接。`asm`、`linux` 和 `scsi` 目录是对应 Linux 架构源码目录的软链接，例如 `/usr/src/include/asm` 用于“asm”。

- 在终端中输入以下命令：
```
[root@deep $] cd /usr/include/
[root@deep] rm -rf /usr/include/linux scsi
[root@deep] ln -s /usr/src/include/asm asm
[root@deep] ln -s /usr/src/include/linux linux
[root@deep] ln -s /usr/src/include/scsi scsi
```
这是配置的一个非常重要的部分，将 `/usr/include` 下的 `asm`、`linux` 和 `scsi` 目录链接到新内核的同名目录。`include` 目录包含了编译 Linux 内核所需的头文件和依赖项。

**注意**：上述两个步骤清理了开发团队可能意外留在源码树中的任何内容。你可以通过三种方式之一来配置内核：第一种是使用 `make config` 命令，它提供了一个基于文本的界面；第二种是使用 `make menuconfig` 命令，它提供了一个易于使用的菜单；第三种是使用 `make xconfig` 命令，它提供了一个完整的图形界面。在本章中，我们将使用 `make config` 命令来设置你的 Linux 服务器配置。

- 在终端中输入以下命令加载内核配置：
```
[root@deep $] cd /usr/src/linux/
[root@deep linux]# rm -f
(cd include) ln -s asm-i86 asm
/bin/sh scripts/Configure arch/i86/config.in > arch/i86/defconfig
# Using Defaults found in arch/i86/
defconfig
```

## 内核配置

### 代码成熟度选项 (Code maturity level options)

### 处理器类型和特性 (Processor type and features)

处理器族 (386, 486, 586/5x86, Pentium/K6/TSC, PPro/6x86)，最大物理内存 (1GB, 2GB)，内存类型范围支持 (Memory Type Range support)，对称多处理支持 (Symmetric multi-processing support)。

### 可加载模块支持 (Loadable module support)

启用可加载模块 (Enable loadable module)。

#### 通用设置 (General setup)

网络支持 (Networking support)，PCI 支持 (PCI support)，PCI 模式 (BIOS, Direct)，PCI 奇异功能 (PCI quirks)，向后兼容 (Backwards-compatible)，MCA 支持 (MCA support)，SGI 虚拟工作站支持 (SGI Virtual workstation)，系统 IPC (System IPC)，BSD 进程计数 (BSD Process Accounting)，内核支持 (Kernel support)，a.out 二进制文件支持 (Kernel support for a.out)，ELF 二进制文件支持 (Kernel support for ELF)，MISC 二进制文件支持 (Kernel support for MISC)，并行端口支持 (Parallel port)，高级电源管理支持 (Power Management)。

### 即插即用 (Plug and play)

即插即用支持 (PNP)。

#### 块设备 (Blocks)

PC 软磁盘支持 (PC floppy disk support)，增强 IDE/MFM 磁盘/CDROM/软盘支持 (Enhanced IDE/MFM disk/cdrom/floppy support)，在主接口上使用旧式磁盘驱动 (Use old-style disk driver on primary interface)，包含 IDE/ATA-2 磁盘支持 (Include IDE/ATA-2 disk support)，包含 IDE/ATAPI CDrom 支持 (Include IDE/ATAPI CDrom support)，包含 IDE/ATAPI 磁带支持 (Include IDE/ATAPI tape support)，包含 IDE/ATAPI 软盘支持 (Include IDE/ATAPI floppy support)，SCSI 仿真支持 (SCSI emulation support)，CMD640 芯片支持 (CMD640 chipset support)，2100 芯片支持 (2100 chipset support)，通用 IDE 支持 (Generic IDE support)，通用 PCI 总线主数据支持 (Generic PCI bus-master data support)，板载离线芯片支持 (Board off-chip chipset support)，可用时使用旧 DMA (Use old DMA when available)，其他 IDE 支持 (Other IDE support)，回环设备支持 (Loopback device)，多个驱动器支持 (Multiple drives)，RAM 磁盘 (RAM disk)。

关于本书的意见和建议应邮寄至 `gmourani@videetron.ca`

- NCR5C88X SCSI 支持 (CONFIG, SCSI, NCR5C88X) [N/y]
- SYM5C38X SCSI 支持 (CONFIG, SCSI, SYM5C38X) [N/y]
- PAS16 SCSI 支持 (CONFIG, SCSI, PAS16) [N/y]
- PCI2100 支持 (CONFIG, SCSI, PCI2100) [N/y]
- PCI2220 支持 (CONFIG, SCSI, PCI2220) [N/y]
- PSI5240 支持 (CONFIG, SCSI, PSI5240) [N/y]
- QLogic SCSI 支持 (CONFIG, SCSI, QLOGIC_FAS) [N/y]
- QLogic ISP 支持 (CONFIG, SCSI, QLOGIC_ISP) [N/y]
- QLogic FC 支持 (CONFIG, SCSI, QLOGIC_FC) [N/y]
- Seagate ST-02 和 Future Domain Tmc-8bx SCSI 支持 (CONFIG, SCSI_SEAGATE) [N/y]
- Tekramic DMC390IT 和 ARC7974 SCSI 支持 (CONFIG, SCSI_DMC390) [N/y]
- Trant T128T1/F728 SCSI 支持 (CONFIG, SCSI, T128) [N/y]
- UltraStar 14f/34f 支持 (CONFIG, SCSI_U14) [N/y]
- UltraStar SCSI 支持 (CONFIG, SCSI__ULTRASTOR) [N/y]

# 网络设备支持

网络设备支持 (CONFIG, NETDEVICES) [N/y]

# ARCNet 设备

- ARCNet 支持 (CONFIG, ARCNET) [N/y]
- 虚拟驱动支持 (CONFIG, DUMMY) [N/y]
- EQL (线路负载均衡) 支持 (CONFIG, EQUALIZER) [N/y]
- AMD LANCE 和 PCI 卡 (AT1500 和 NE5100) 支持 (CONFIG, LANCE) [N/y]
- 西部数据/MC 卡 (CONFIG, NET_VECTOR_CMC) [N/y]
- Racal-Intermedia (MCI) 支持 (CONFIG, NET_VECTOR_RACAL) [N/y]
- 其他 ISA 卡 (CONFIG, NET_ISA) [N/y]
- EISA, VLB 和 PCI 卡 (CONFIG, PCNET_EISA) [N/y]
- AMD P60/VLB 和 PCI 支持 (CONFIG, PCNET32) [N/y]
- 以太网上的 Apricot Xen-10 (CONFIG, APRICOT) [N/y]
- CS8960 支持 (CONFIG, CS8960) [N/y]
- DM1020 PCI 以太网适配器支持 (实验)(CONFIG, DM1020) [N/y]
- GeekDech 图形与数字; EtherWorks PCISEA (CONFIG, DE4X5) [N/y]
- Decculp Duchip (de21x4) PCI 支持 (CONFIG, DELC_ELCP) [N/y]
- 旧版 DecChip Tulli (de21x4) PCI 支持 (CONFIG, DELC_ELCP) [N/y]
- Dig High-Speed X X 支持 (CONFIG, DIG_GRS) [N/y]
- EthernetExpressPro100 支持 (CONFIG, EADDRESS_PRO100) [N/y]
- PCI NE2100 支持 (CONFIG, NET_2K) [N/y]
- TI Thunder 支持 (CONFIG, TLAN) [N/y]
- Via 支持 (CONFIG, VIA_RHINE) [N/y]
- SIS 9000 PCI 快以太网适配器支持 (CONFIG, SISS9000) [N/y]
- 数据包和便携适配器 (CONFIG, NET_POCKET) [N/y]

# 以太网 (10 或 100 Mbps)

以太网 (10 或 100 Mbps) [N/y]
- 3COMC 卡 (CONFIG, NET_VECTOR_2CMC) [N/y]
- AMD LANCE 和 PCI 卡 (AT1500 和 NE5100) 支持 (CONFIG, LANCE) [N/y]
- 西部数据/MC 卡 (CONFIG, NET_VECTOR_CMC) [N/y]
- Racal-Intermedia (MCI) 支持 (CONFIG, NET_VECTOR_RACAL) [N/y]
- 其他 ISA 卡 (CONFIG, NET_ISA) [N/y]

## 以太网 (1000 Mbps)

- SysKonnet-SK988X 支持 (CONFIG, SK98LN) [N/y]
- FFDI 驱动 (点对点) 支持 (CONFIG, FFDI) [N/y]
- PPP (点到线) 支持 (CONFIG, PPP) [N/y]
- SLIP (串口) 支持 (CONFIG, SLIP) [N/y]
- 无线局域网 (无线电) (CONFIG, NET_RADIO) [N/y]

## 令牌环设备

- 令牌环驱动支持 (CONFIG, Th) [N/y]
- Channel 支持 (CONFIG, NET_FC) [N/y]

## WAN 接口

- MultiGate (COMX) 串口板支持 (CONFIG, COMX) [N/y]
- 帧中继 DLCI 支持 (CONFIG, NET_DLCI) [N/y]

© Copyright 1999-2000 Gerard Maurani and Open Network Architecture ®84

关于本书的意见和建议应邮寄至 `gmourani@videotron.ca`

- WAN 驱动 (CONFIG_WAN_DRIVERS) [N/y]
- SBN12-xx 支持 (CONFIG_SBN) (NEW)

# 业余无线电

- 业余无线电支持 (CONFIG_HAMRADIO) [N/y]

# IrDA 子系统

- IrDA 支持 (CONFIG_IRDA) [N/y]

# ISDN 子系统

- ISDN 支持 (CONFIG_ISDN) [N/y]

# 旧 CD-ROM 驱动 ( SCSI, IDE)

- 非 SCSI/IDE/ATAPI CD 驱动支持 (CONFIG_CD_NO_IDE) [N/y]

## 字符设备

- 虚拟终端 (CONFIG_VT_CONSOLE) [N/y]
- 虚拟终端串口支持 (CONFIG_VT_SERIAL) [N/y]
- 标准/通用串口支持 (CONFIG_SERIAL) [N/y]
- 串口扩展支持 (CONFIG_SERIAL_EXTENDED) [N/y]
- 扩展串口驱动 (CONFIG_SERIAL_NONSTANDARD) [N/y]
- Unix 支持 (CONFIG_PTYS) [N/y]
- Unix98 支持 (CONFIG_UNIX98_PTYS) [N/y]
- 0-2048 的最大 PTYS 数 (CONFIG_UNIX98_PTY_COUNT) [256]
- 鼠标支持 (CONFIG_MOUSE) [N/y]

## 鼠标

- ATIX 总支持 (CONFIG_BUSMOUSE) [N/y]
- Logitech 鼠标支持 (CONFIG_BUSMOUSE) [N/y]
- Microsoft 鼠标支持 (CONFIG_MS_MOUSE) [N/y]
- 2 鼠标支持 (CONFIG_PSMOUSE) [N/y]
- 82C710 鼠标端口 (基础)(CONFIG_82C710_MOUSE) [N/y]
- PC10 设备垫板 (CONFIG_PC10_PAD) [N/y]

## 摇杆支持

- 摇杆支持 (CONFIG_JOYSTICK) [N/y]
- 02 带支持 (CONFIG_QIC02_TAPE) [N/y]
- 看门计时 (CONFIG_WATCHDOG) [N/y]
- /dev/nvram 支持 (CONFIG_NVRAM) [N/y]
- 增强实时时钟 (CONFIG_RTC) [N/y]

# Linux 视频

- Linux 视频 (CONFIG_VIDEO_DEV) [N/y]
- 双话 PC 内部支持 (CONFIG_DTT) [N/y]

## 软磁盘驱动

- 软磁盘 (QIC-80/盘) 支持 (CONFIG_FTAPE) [NEW]

## 文件系统

- 配额支持 (CONFIG_QUOTA) [N/y]
- 内核自动挂载支持 (CONFIG_AUTOFS_FS) [N/y]
- Amiga 文件系统支持 (CONFIG_AFFS_FS) [N/y]
- Apple Macintosh 文件系统支持 (实验性)(CONFIG_HFS_FS) [N/y]
- FAT 支持 (CONFIG_FAT_FS) [N/y]
- ISO 9660 CDROM 文件系统支持 (CONFIG_ISO9660_FS) [N/y]
- Microsoft 联合 CD (CONFIG_JOLET) [N/y]
- Mine (CONFIG_FS) [N/y]
- NTFS 文件系统支持 (只读) (CONFIG_NTFS_FS) [N/y]
- OS/2 HPFS 文件系统支持 (CONFIG_HPFS_FS) [N/y]
- /proc 文件系统支持 (CONFIG_PROC_FS) [N/y]

© Copyright 1999-2000 Gerard Maurani and Open Network Architecture ®85

关于本书的意见和建议应邮寄至 `gmourani@videotron.ca`

- Unix 的 /dev/ptys 文件系统 (CONFIG_DEVPTS_FS) [N/y]
- ROM 文件系统支持 (CONFIG_ROMFS_FS) [N/y]
- 扩展第二文件系统支持 (CONFIG_EXT2_FS) [N/y]
- System V 和一致性文件系统支持 (CONFIG_SYS_FS) [N/y]
- UFS 文件系统支持 (CONFIG_UFS_FS) [N/y]

## 网络文件系统

- Coda 文件系统支持 (高级网络 fs) (CONFIG_CODA_FS) [N/y]
- NFS 文件系统支持 (CONFIG_NFS_FS) [N/y]
- SMB 文件系统支持 (挂载共享等等) (CONFIG_SMB_FS) [N/y]
- NCP 文件系统支持 (挂载 NetWare 卷) (CONFIG_NCP_FS) [N/y]

## 分区类型

- BSD disklabel (BSD 分区类型) (CONFIG_BSD_DISKLABEL) [N/y]
- Macintosh 分区支持 (CONFIG_MAC_PARTITION) [N/y]
- SMD label (Sun 分区类型) (CONFIG_SMD_DISKLABEL) [N/y]
- Solaris (x86) 分区支持 (CONFIG_SOLARIS_X86_PARTITION) [N/y]

## 控制台驱动

- VGA 控制台 (CONFIG_VGA_CONSOLE) [N/y]
- 视频模式选择支持 (CONFIG_VIDEO_SELECT) [N/y]

## 音频

- 声卡支持 (CONFIG_SOUND) [N/y]

(安全选项仅当您的内核通过补丁时才会出现。)

## 安全选项

- 非可执行用户区域 (CONFIG_SECURE_STACK) [Y]
- 自动化和模拟 gcc 工具链 (CONFIG_SECURE_MARK) [Y]
- /tmp 中的受限链接 (CONFIG_SECURE_LINK) [Y]
- /tmp 中的受限 FIFO (CONFIG_SECURE_FIFO) [Y]
- 受限 /proc (CONFIG_SECURE_PROC) [Y]
- 对 fd0, 1 和 2 的特殊处理 (CONFIG_SECURE_FD_0_2) [Y]
- 在 exec 上强制 RLIMIT_NPROC (CONFIG_SECURE_RLIMIT_NPROC) [Y]
- 销毁使用的共享内存段 (CONFIG_SECURE_SHM) [Y]

# 内核黑客

现在，返回 `/usr/src/linux/`（如果不在那里的话）。你需要编译新内核。你可以使用以下命令执行：
```
