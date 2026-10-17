
这里的 `token` 可以是 `error`, `scanc`, `mlqueue`, `mlcomplete`, `ilqueue`, `ilcomplete`, `hlccomplete`。`level` 控制日志的详细程度，可以是任何大于 0 的整数。

SCSI 部分的剩余问题是针对 SCSI 主机适配器的。你应该只针对你已安装的适配器选择支持。

# 第 VII 部分：性能调优

## 网络设备支持

在本节中，你将配置各种网络设备功能。

网络设备支持 (`CONFIG_NETDEVICES`) [Y/n/?]

因为你正在为服务器配置内核，你必须对前面的问题选 yes。

ARCnet 支持 (`CONFIG_ARCNET`) [N/y/m/?]

除非你拥有 ARCnet 网卡，否则选择默认即可。

虚拟网络驱动程序支持 (`CONFIG_DUMMY`) [M/n/y/?]

此驱动允许你拥有一个虚拟网络接口设备，可欺骗网络客户端程序。将其保持为模块（module）可能很有用；因此推荐默认。

EOL（串行负载负载）支持 (`CONFIG_EQUALIZER`) [N/y/m/?]

此功能对于大多数服务器配置没有用。建议选择默认答案。

以太网 (10 或 100Mbit) (`CONFIG_NET_ETHERNET`) [Y/n/y]

又一个不用思考的选择。
以下问题的回答取决于你拥有什么类型的网卡；因此请根据情况回答：

- 3COM 网卡 (`CONFIG_NET_VENDOR_3COM`) [N/y/?]
- AMD LANCE 和 PCnet (AT1500 和 NE2100) 支持 (`CONFIG_LANCE`) [N/y/m/?]
- 西数据/SMC 网卡 (`CONFIG_NET_VENDOR_SMC`) [N/y/?]
- Racal-Interlan (MiCom) NI 网卡 (`CONFIG_NET_VENDOR_RACAL`) [N/y/?]
- 其他 ISA 网卡 (`CONFIG_NET_ISA`) [N/y/?]
- EISA, VLB, PCI 及板载控制器 (`CONFIG_NET_EISA`) [Y/n/?]
- AMD PCnet32 (VLB 和 PCI) 支持 (`CONFIG_PCNET32`) [y/m/?]
- Apricot Xenon-II 板载以太网 (`CONFIG_APRICOT`) [y/m/?]
- CS89x0 支持 (`CONFIG_CS990`) [y/m/?]
- 通用 DEChip EtherWORKS PCI/EISA (`CONFIG_DE4X`) [y/m/?]
- DEchip Tulip (dc21x4) PCI 支持 (`CONFIG_ELCP`) [y/m/?]
- Digi Intl. RightSwitch SE-X (`CONFIG_DGRS`) [y/m/?]
- EtherExpressPro/100 支持 (`CONFIG_EXPRESS_PR1000`) [y/m/?]
- PCI NE2000 支持 (`CONFIG_NE2K`) [y/m/?]
- TI ThunderLAN 支持 (`CONFIG_FLAN`) [y/m/?]
- VIA Rhine 支持 (`CONFIG_RHINE`) [y/m/?]
- Pocket 和 portland 适配器 (`CONFIG_POCKET`) [y/m/?]
- FDDI 驱动支持 (`CONFIG_FFDI`) [y/m/?]
- 帧继 DLCI 支持 (`CONFIG_DLCI`) [y/m/?]
- P（点点）支持 (`CONFIG_PPP`) [y/m/?]
- SLIP（串行线路）支持 (`CONFIG_SLIP`) [y/m/?]
- 无线局域网（无线电）（`CONFIG_RADIO`） [y/m/?]
- Token Ring 驱动支持 (`CONFIG_TR`) [y/m/?]
- 控制器 Hostess SV-11 支持 (`CONFIG_HOSTESS_SV11`) [y/m/?]
- COSA/sync 串口板支持 (`CONFIG_COSA`) [y/m/?]
- Creek Hardware VPN（实验性）（`CONFIG_RCP`） [y/m/?]
- WAN 驱动 (`CONFIG_DRIVERS`) [y/m/?]
- 以太网 LAP 驱动 (`CONFIG_LAPETHER`) [y/m/?]
- X25 异步驱动 (`CONFIG_X25`) [y/m/?]

## 无线电、ISDN 和旧 CD-ROM

我假设你不会使用无线电、ISDN 或旧 CD-ROM，因此以下默认答案为：

- 无线电支持 (`CONFIG_HAMRADIO`) [y/m]
- ISDN 支持 (`CONFIG_ISDN`) [y/m/]
- 支持非 SCSI/IDE/ATAPI CD-ROM 驱动 (`CONFIG_CD_ROM`) [y/m/]

如果你计划使用 ISDN 卡为服务器提供互联网连接，我强烈建议使用 ISDN 路由器而不是内部卡。我使用内部卡的经验得出了这个结论。我尝试过一些工作不良好的 ISDN 卡。除了 PC 上 IRQ 和 I/O 地址资源有限的问题外，内部卡和 ISDN 路由器之间的价格差异并不显著，考虑到 ISDN 本身相当贵。

## 字符设备

在本节中，你将被问及终端配置。

虚拟终端 (`CONFIG_VT`) [Y/n/?]:

此功能允许你拥有虚拟终端。除非你在嵌入式系统中安装内核，否则需要默认答案。

虚拟终端控制台支持 (`CONFIG_VT_CONSOLE`) [Y/n/?]:

此功能允许将虚拟终端转换为系统控制台。原因与上一个相同。

串口控制台支持 (`CONFIG_SERIAL_CONSOLE`) [N/y/?]:

如果你喜欢使用电脑的串口作为系统控制台，请更改默认答案。

扩展串口驱动选项 (`CONFIG_SERIAL_EXTENDED`) [N/y/?]:

除非你在上一个问题中将串口作为系统控制台，否则在此更改默认值。

Unix98 PTY 支持 (`CONFIG_UNIX98_PTYS`) [Y/n/?]:

此功能提供了 UNIX 98 伪终端编号的支持，优于传统的 Linux 伪终端约定。你应该保持默认设置。

如果你保持默认设置，将被询问以下问题以设置系统可以使用的 UNIX 98 PTY 最大数量：

正在使用的 Unix98 PTY 最大数量 (0-2048) (`CONFIG_UNIX98_PTY_COUNT`) [256]:

对于大多数情况，默认值应该足够了。

鼠标支持（非串口鼠标） (`CONFIG_MOUSE`) [Y/n/?]:

此功能允许你在可以使用此类设备的终端上使用鼠标。建议默认。

QIC-02 磁带支持 (`CONFIG_QIC02_TAPE`) [N/y/m]:

如果你有 QIC-02 磁带，可以在这里选择添加支持。

看门计时器支持 (`CONFIG_WATCHDOG`) [N/y/y?]:

如果你想创建一个看门计时器以便在故障时重启系统，请在此选 yes。如果你启用了此功能，则必须使用 `mod` 程序创建一个名为 `/dev/watchdog` 的特殊设备（主设备130，次设备10）。然后你可以使用一个看门守护程序向该设备写入数据。

`/dev/nvram` 支持 (`CONFIG_NVRAM`) [N/y/m?]:

此功能允许你创建特殊设备 `/dev/nvram`，用于读写访问实时钟中的非易失性内存。除非你清楚自己在做什么，否则保持默认。

增强实时钟支持 (`CONFIG_RTC`) [N/y/y?]:

此功能允许你创建一个特殊设备 `/dev/rtc`，用于访问系统中的实时钟。除非你清楚自己在做什么，保持默认。

## 视频和摇杆支持

因为你正在配置服务器系统，我假设系统中没有视频硬件采集或摇杆，因此你应该接受以下问题的默认答案：

- Linux 视频 (`CONFIG_VIDEO_DEV`) [N/y/m?]
- 摇杆支持 (`CONFIG_JOYSTICK`) [N/y/m?]

## FTAPE，磁带设备驱动程序

如果你有基于软盘控制器的磁带驱动，你需要在这里选择对其支持。

Ftape (QIC-80/Travan) 支持 (`CONFIG_FTAPE`) [N/y/m?]

## 文件系统

在本节中，你为各种文件系统特定功能配置内核。

- 配额支持 (`CONFIG_QUOTA`) [N/y/m?]

如果你希望在内核中内置磁盘配额支持，请在此处选择 yes。

内核自动挂载器支持 (`CONFIG_AUTOFS_FS`) [Y/m/n/?]

如果你希望自动挂载和卸载 NFS 等远程文件系统，请在此处选择添加直接或基于模块的自动挂载器支持。

以下是各种特定厂商的文件系统支持问题。请根据你的需求回答它们：

- Amiga FFS文件系统支持 (`CONFIG_AFFS_FS`) [Y/m/n/?]
- Apple Macintosh 文件系统支持（实验性） (`CONFIG_HFS_FS`) [Y/m/n/?]
- DOS FAT 文件系统支持 (`CONFIG_FAT_FS`) [Y/m/n/?]
- ISO 9660 CDROM 文件系统支持 (`CONFIG_ISO9660_FS`) [Y/m/n/?]
- Microsoft Jol CDROM 扩展 (`CONFIG_JOLIET`) [N/y/m/?]
- Minix 文件系统支持 (`CONFIG_MINIX_FS`) [Y/m/n/?]
- NTFS 文件系统支持（只读） (`CONFIG_NTFS_FS`) [Y/m/n/?]
- OS/2 HPFS 文件系统支持（只读） (`CONFIG_HPFS_FS`) [Y/m/n/?]

- `/proc` 文件系统支持 (`CONFIG_PROC_FS`) [Y/m/n/?]

`/proc` 文件系统是任何现代 Linux 系统的必备项，因此强烈建议使用默认答案。

- 用于 Unixx98 PTYs 的 `/dev/pts` 文件系统 (`CONFIG_DEVTS_FS`) [Y/m/n/?]

如果你选择添加对 UNIX 98 伪终端的支持，你则需要在此处添加 `/dev/pts` 文件系统支持。

- ROM 文件系统支持 (`CONFIG_ROMFS_FS`) [Y/m/n/?]

这类文件系统在大多数典型用法下不需要。

- 扩展 ext 文件系统支持 (`CONFIG_EXT2_FS`) [Y/m/n/?]

扩展 ext2 是 Linux 的主要文件系统，因此默认答案是必须的。

以下问题的默认答案适用于大多数系统：

- System V 和 Coherent 文件系统支持 (`CONFIG_SYSV_FS`) [Y/m/n/?]
- UFS 文件系统支持 (`CONFIG_UFS_FS`) [Y/m/n/?]

注意，如果你选择挂载由 Solaris x86 或 BSD 等其他操作系统创建的磁盘分区，则需要 UFS 文件系统支持。

### 第 20 章：内核黑客 641：网络文件系统

在这里，你可以为高级网络文件系统配置内核。

- Coda 文件系统支持（高级网络文件系统） (`CONFIG_CODA_FS`) [N/y/m/]

Coda 文件系统尚未足够流行，因此我不建议将其添加到内核；你可能会将其作为模块添加。

- NFS 文件系统支持 (`CONFIG_NFS_FS`) [Y/m/n/]

如果你计划使用 NFS，请使用默认答案。

- 模拟 SUN NFS 服务器 (`CONFIG_NFSD_SUN`) [N/y/?]

除非你希望你的 Linux NFS 服务器表现得像基于 Sun 的 NFS 服务器（允许 NFS 客户端访问本地文件系统上挂载点的目录），否则保持默认即可。

- SMB 文件系统支持（挂载 Windows 共享等） (`CONFIG_SMB_FS`) [N/y/m/]

如果你希望在 Linux 系统上将 Windows 9xr/NT 文件系统作为 SMB 文件系统挂载，你需要说 yes 或将此功能设置为模块。

- NCP 文件系统支持（挂载 NetWare 卷） (`CONFIG_NCP_FS`) [N/y/m/]

除非你计划在你的 Linux 系统上挂载 NetWare 卷，否则保持默认答案。

## 分区类型

如果你希望支持基于 BSD、Macintosh、Solaris 等磁盘分区，请相应回答以下问题：

- BSD 分区表支持 (`CONFIG_BSD_DISKABEL`) [y/]
- Macintosh 分区图支持 (`CONFIG_MAC_PARTITION`) [y/]
- Sun 分区表支持 (`CONFIG_SMD_DISKABEL`) [y/]
- Solaris (x86) 分区表支持 (`CONFIG_SOLARIS_X86_PARTITION`) [y/]

在大多数情况下，默认答案足够了。

## 控制台驱动

在此节中，你可以设置

- VGA 文本控制台 (`CONFIG_VGA_CONSOLE`) [Y/n/?]

如果你希望拥有 VGA 文本控制台，请保持默认。

- 视频模式选择支持 (`CONFIG_VIDEO_SELECT`) [y/?]

如果你希望在内核启动时指定文本模式，请设置此选项或保持默认。

## 音频

假设你可能在服务器系统中不需要声卡，你可以对以下问题保持默认答案：

- 声卡支持 (`CONFIG_SOUND`) [y/m/]

## 内核黑客

此节中唯一的可用选项是对 Magic SysRq 键的支持。如果你通过对以下问题回答 yes 来启用此键，即使在系统崩溃时也能通过 SysRq+Alt+PrintScreen 转储状态信息。

- Magic SysRq 键 (`CONFIG_MAGIC_SYSRQ`) [y/?]

这对于内核开发者有用。你应该在这里回答 no。一旦你回答了所有问题，配置脚本将在 `/usr/src/linux` 目录下创建一个 `.config` 文件。你可能想查看该文件的内容以确保所有功能都按照你的想法进行了配置。

> 你对如何配置内核不再感兴趣，但准备好编译内核，请跳过接下来两节直接进入“编译、安装和启动新内核”。

使用 `make config` 配置内核是一个很长的过程。它也有些麻烦；但如果你正好通过 Telnet 连接到远程服务器配置内核，它是非常合适的。基于行的界面可能并不优雅，但它适用于几乎所有场景，当上述两种方法不可用时，应被视为默认配置方法。

## 第 20 章：内核黑客
## 使用 menuconfig 配置内核

基于 `make config` 的配置脚本的一个主要问题是，如果你犯了错误，不重新开始就无法返回。此外，除非你使用文本编辑器查看 `/config` 文件，否则你无法检查你的选择。

## 第七部分：性能调优

最后，按照如下方式创建一个名为 `/boot/System.map` 的新符号链接：

```
ln -s /boot/System.map-2.2.2 /boot/System.map
```

你还需要按照如下方式创建一个新的内存磁盘（initial ramdisk）：

```
mkinitrd /boot/initrd-2.2.2.img 2.2.2.
```

在启动新内核之前，最后一步是为新内核准备 LILO。请参阅前面的“配置 LILO”章节，以了解有关如何在 `/etc/lilo.conf` 中为新内核创建一个新配置段的详细信息。一旦你修改了 `/etc/lilo.conf` 文件并运行了 `/sbin/lilo`，你就可以重启系统并尝试像在“使用新内核启动”中所讨论的那样使用新内核。

如果一切顺利，从现在起你将拥有一个全新的、自定义配置的内核，它将运行你所有喜爱的 Linux 应用程序。

> 提示：不要忘记使用 `mkbootdisk-device /dev/fd0 2.2.2` 命令制作新的启动软盘。

既然你已经知道如何从源码配置、编译、安装和启动新内核，你也应该知道，通常会遇到这样的情况：整个内核代码没有发生更改，只有其中一小部分被更改了。这就是你需要知道如何补丁内核源码并重新创建一个内核的时候。

# 补丁内核

需要补丁现有内核以使某些按照你想要的方式运行并不罕见。在这种情况下，你可以简单地补丁源码并重新构建内核。你可以使用以下命令从 `/usr/src` 目录补丁内核源码：

```bash
```
