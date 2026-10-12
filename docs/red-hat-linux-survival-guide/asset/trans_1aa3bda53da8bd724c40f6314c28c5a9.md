
如果您希望支持 Apple Macintosh 文件系统，请启用此选项。

```
BFS file system support (EXPERIMENTAL) (CONFIG_BFS_FS) [N/y/m/?]
```

如果您希望支持 BFS 文件系统，请启用此选项。

```
DOS FAT fs support (CONFIG_FAT_FS) [N/y/m/?]
```

如果您希望支持 DOS 文件系统，请启用此选项。

```
EFS file system support (read only) (EXPERIMENTAL) (CONFIG_EFS_FS) [N/y/m/?]
```

如果您希望支持 EFS 文件系统，请启用此选项。

```
Virtual memory file system support (former shm fs) (CONFIG_TMPFS) [Y/n/?]
```

如果您希望创建将所有文件保存在虚拟内存中的 Tmpfs 文件系统，请通过选择默认答案来启用此选项。与 RAM 磁盘不同，Tmpfs 文件系统不是固定大小的。

```
Simple RAM-based file system support (CONFIG_RAMFS) [N/y/m/?]
```

如果您希望将文件保存在 RAM 中，请使用 Tmpfs 而不是简单的基于 RAM 的文件系统。推荐使用默认选项。

```
ISO 9660 CD-ROM file system support (CONFIG_ISO9660_FS) [Y/m/n/?]
```

这将启用标准 CD-ROM 文件系统支持，并且应在大多数系统上启用；推荐使用默认答案。

```
Microsoft Joliet CD-ROM extensions (CONFIG_JOLIET) [N/y/?]
```

Joliet 文件系统是 ISO9660 的 Microsoft 扩展，仅应在计划使用刻录为 Joliet 文件系统的 CD-ROM 媒体的用户启用。

```
Minix fs support (CONFIG_MINIX_FS) [N/y/m/?]
```

Minix fs 是 Linux 原生文件系统（ext2）的前身；您很可能不需要此支持。

```
FreeVxFS file system support (VERITAS VxFS(TM) compatible) (CONFIG_VXFS_FS) [N/y/m/?]
```

大多数系统不需要 FreeVxFS 文件系统支持，因此默认答案很可能合适。

```
NTFS file system support (read only) (CONFIG_NTFS_FS) [N/y/m/?]
```

如果您计划以只读模式在 Linux 系统上挂载 Windows NT/2000 文件系统（NTFS），请启用其支持，否则选择默认答案。

```
OS/2 HPFS file system support (CONFIG_HPFS_FS) [N/y/m/?]
```

如果您计划在 Linux 系统上挂载 IBM OS/2 HPFS 文件系统，则启用其支持，否则选择默认答案。

```
/proc filesystem support (CONFIG_PROC_FS) [Y/n/?]
```

/proc 文件系统是任何现代 Linux 系统必备的；因此强烈推荐使用默认答案。

```
/dev file system support (EXPERIMENTAL) (CONFIG_DEVFS_FS) [N/y/?]
```

如果您希望使用 devfs 文件系统代替传统的 /dev 目录，则应在此处启用它。由于 /dev 对 Linux 操作至关重要，而 devfs 尚未成熟，我建议您在 devfs 成为标准之前选择默认答案。

```
/dev/pts filesystem for Unix98 PTYs (CONFIG_DEVPTS_FS) [Y/n/?]
```

如果您选择添加对 UNIX 98 伪终端的支持，则需要在此处添加 /dev/pts 文件系统支持。

```
QNX4 file system support (read only) (EXPERIMENTAL) (CONFIG_QNX4FS_FS) [N/y/m/?]
```

如果您计划在 Linux 系统上使用 QNX4 文件系统，请通过选择“是”来启用其支持；否则，选择默认答案。

```
ROM filesystem support (CONFIG_ROMFS_FS) [N/y/m/?]
```

大多数系统不需要此类文件系统。

```
Second extended fs support (CONFIG_EXT2_FS) [Y/m/n/?]
```

Extended fs 是 Linux 的主要文件系统；因此，默认答案是必须的。

```
System V and Coherent filesystem support (CONFIG_SYSV_FS) [N/y/m/?]
```

对于此问题，默认答案应适用于大多数系统：

```
UDF file system support (read only) (CONFIG_UDF_FS) [N/y/m/?]
```

如果您计划在 Linux 系统上使用 UDF 文件系统，则启用其支持；否则选择默认答案。

```
UFS filesystem support (CONFIG_UFS_FS) [N/y/m/?]
```

请注意，如果您选择挂载由其他操作系统（如 Solaris x86 或 BSD）创建的磁盘分区，则需要 UFS 文件系统支持。

## 网络文件系统

在本节中，您为高级网络文件系统配置内核。

```
Coda filesystem support (advanced network fs) (CONFIG_CODA_FS) [N/y/m/?]
```

Coda 文件系统尚未流行到足以推荐，我不建议将其添加到内核中；您可以选择将其作为模块添加。

```
NFS filesystem support (CONFIG_NFS_FS) [Y/m/n/?]
```

如果您计划使用 NFS，请选择默认答案。在这种情况下，您还必须在下面选择是否要支持 NFS 版本 3 客户端：

```
Provide NFSv3 client support (CONFIG_NFS_V3) [N/y/?]
```

由于 NFS 版本 3 相当新，您应该启用它以体验其优势。

如果您希望将 Windows 9x/NT 文件系统作为 SMB 文件系统挂载到 Linux 系统上，则需要选择“是”或将此功能设为模块。

```
NCP filesystem support (to mount NetWare volumes) (CONFIG_NCP_FS) [N/y/m/?]
```

除非您计划在 Linux 系统上挂载 NetWare 卷，否则选择默认答案。

## 分区类型

如果您希望支持基于 BSD、Macintosh、Solaris 等的磁盘分区，请相应地回答以下问题：

```
BSD disklabel (BSD partition tables) support (CONFIG_BSD_DISKLABEL) [N/y/?]
```

```
Macintosh partition map support (CONFIG_MAC_PARTITION) [N/y/?]
```

```
SMD disklabel (Sun partition tables) support (CONFIG_SMD_DISKLABEL) [N/y/?]
```

```
Solaris (x86) partition table support (CONFIG_SOLARIS_X86_PARTITION) [N/y/?]
```

在大多数情况下，默认答案已足够。

## 控制台驱动程序

在本节中，您可以设置以下内容：

```
VGA text console (CONFIG_VGA_CONSOLE) [Y/n/?]
```

如果您希望拥有 VGA 文本控制台，请选择默认答案。

```
Video mode selection support (CONFIG_VIDEO_SELECT) [N/y/?] ?
```

如果您希望在内核启动时指定文本模式，请选择“是”以启用此选项，或选择默认答案。

```
MDA text console (dual-headed) (EXPERIMENTAL) (CONFIG_MDA_CONSOLE) [N/y/m/?]
```

您很可能不使用 MDA 或单色 Hercules 显卡，因此默认设置对大多数情况应该是合适的。

```
Support for frame buffer devices (EXPERIMENTAL) (CONFIG_FB) [N/y/?]
```

帧缓冲是一个编程接口，可用于许多视频设备，使图形开发非常便携。如果您的视频硬件支持帧缓冲，请启用此选项。

## 声音

如果您正在设置工作站，那么您很可能有一块声卡。在这种情况下，您应以下面回答“是”：

```
Sound card support (CONFIG_SOUND) [N/y/m/?]
```

从上述之后列出的特定厂商声卡问题列表中选择合适的声卡硬件支持。

## USB 支持

大多数现代 PC 都具有 USB 支持，因此您应选择以下问题的默认答案：

```
Support for USB (CONFIG_USB) [Y/m/n/?]
```

系统会询问您是否希望为 USB 硬件启用详细调试消息。选择默认答案。

```
USB verbose debug messages (CONFIG_USB_DEBUG) [N/y/?]
```

## 内核 Hacking

本节中唯一的选项是 Magic SysRq 键的支持。如果您通过对以下问题回答“是”来启用此键的支持，您将能够在系统崩溃时按下 SysRq+Alt+PrintScreen 来转储状态信息。

```
Magic SysRq key (CONFIG_MAGIC_SYSRQ) [N/y/?]?
```

这仅对内核开发人员有用，因此如果您不是开发人员，请在此处选择“否”。

在您回答完所有这些问题后，配置脚本将在 /usr/src/linux 目录中创建 .config 文件。您可能希望查看此文件的内容，以确保所有功能都按您认为的方式配置。

![](img/9eb7e89292d2f85707b4d49102c865b7_296_0.png)

> 如果您对如何进一步配置内核不感兴趣，但已准备好编译内核，请跳过接下来的两个部分，并继续进行“编译、安装和启动新内核。”
