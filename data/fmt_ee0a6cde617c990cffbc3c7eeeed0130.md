
| `vxfs` | RW | Veritas VxFS 日志文件系统。 |
| `xfs` | RW | SGI 为 Linux 开发的高性能日志文件系统。请参见 XFS 网站（http://oss.sgi.com/projects/xfs/）。 |

并非所有这些文件系统都受 `mount` 命令支持；请参阅 `mount(8)` 查看受支持的列表。

日志记录（Journaling）是一种在数据库系统中开创的技术，用于改进文件更新性能，使得在崩溃事件发生时的文件系统恢复既准确又快速。截至本文撰写时，有多种不同的日志文件系统可用，并在 GNU/Linux 世界中争夺主导地位。`ext3` 是其中之一；它具有向上兼容现有 `ext2` 文件系统的优势，而且在这两种类型之间来回转换文件系统非常容易。（参见 `tune2fs(8)`。）ReiserFS 和 XFS 也有强大的支持者。

`fat`、`msdos`、`umsdos` 和 `vfat` 文件系统都共享公共代码。通常，您应使用 `vfat` 来挂载 Windows FAT-32（或其他 FAT-xx）分区，如果您希望将 FAT 分区用作 GNU/Linux 系统的根文件系统，则使用 `umsdos`。

Coherent、MINIX、原始 System V 和 Xenix 文件系统的磁盘结构相似。`sysv` 文件系统类型支持所有这些；四个名称 `coherent`、`minix`、`sysv` 和 `xenix` 互为别名。`coherent` 和 `xenix` 名称最终将被移除。

BSD 快速文件系统多年来有所演变。`ufs` 文件系统支持 4.4 BSD 版本的读写操作，该版本是三个广泛使用的 BSD 操作系统（FreeBSD、NetBSD 和 OpenBSD）的基础。它还支持 Sun Solaris 文件系统的读写操作，适用于 SPARC 和 Intel x86 系统。原始 BSD 格式和 NeXTStep 操作系统格式支持只读。

`befs` 和 `ntfs` 的“RO”指定意味着这些类型的文件系统可以被挂载和读取，但不能在其上写入文件或删除文件。（这可能会随时间变化；请检查您的系统文档。）`cramfs`、`iso9660`、`romfs` 和 `udf` 文件系统标记为“RO”，因为其底层介质本质上是只读的。

有两种文件系统类型不再存在：`ext`（最初的扩展文件系统）和 `xiafs`（扩展了原始 MINIX 文件系统以支持更长的名称和更大的文件大小）。`xiafs` 和 `ext2` 大致同时出现，但 `ext2` 最终成为主导的文件系统。

### 8.1.3 挂载文件系统：`mount`

`mount` 命令挂载文件系统，将其内容拼接到系统文件层次结构中的挂载点。在 GNU/Linux 中，由于它必须处理所有已知的文件系统类型及其选项，因此有点复杂。通常，只有 root 可以运行 `mount`，尽管对于某些情况可以做出例外，本章稍后会有讨论。

您使用 `-t` 选项指定文件系统类型：

```text
mount [ 选项 ] 设备 挂载点
```

例如（`#` 是 root 提示符）：

```text
# mount -t iso9660 /dev/cdrom /mnt/cdrom        挂载 CD-ROM
# mount -t vfat /dev/fd0 /mnt/floppy             挂载 MS-DOS 软盘
# mount -t nfs files.example.com:/mnt /mnt/files  挂载 NFS 文件系统
```

您可以使用 `-t auto` 强制 `mount` 猜测文件系统类型。这通常可行，但如果您确切知道您拥有哪种文件系统，提供类型并避免 `mount` 猜测错误的机会会有帮助。`mount` 默认执行此猜测，因此 `-t auto` 并非严格必要。

GNU/Linux 系统通过 loopback 设备提供一种特殊的挂载方式。通过这种方式，包含在常规文件中的文件系统镜像可以像实际的磁盘设备一样被挂载。此功能非常有用，例如，用于 CD-ROM 镜像。它允许您创建并试用镜像，而无需将其刻录到可写 CD 并挂载该 CD。以下示例使用 Red Hat 9 GNU/Linux 发行版中的第一个 CD 镜像：

```text
# ls -l shrike-i386-disc1.iso                      检查 CD 镜像文件
-rw-r--R-- 1 arnold devel  68891488 Apr 11 05:13 shrike-i386-disc1.iso
# mount -t iso9660 -o ro,loop shrike-i386-disc1.iso /mnt/cdrom    将其挂载到 /mnt/cdrom
# cd /mnt/cdrom                                               进入该目录
# ls                                                          查看文件
    autorun      README.it       RELEASE-NOTES-fr.html
    dosutils     README.ja       RELEASE-NOTES.html
    EULA         README.ko       RELEASE-NOTES-it.html
```

> 来源：http://www.ife.ee.ethz.ch/musik/software/sag/subsection2_5_4_3.html。

```text
GPL             README_.pt          RELEASE-NOTES-ja.html
images          README_.pt_BR       RELEASE-NOTES-ko.html
isolinux        README_.zh_CN       RELEASE-NOTES-pt_BR.html
README          README_.zh_TW       RELEASE-NOTES-pt.html
README-Accessibility  RedHat        RELEASE-NOTES-zh_CN.html
README_.de      RELEASE-NOTES       RELEASE-NOTES-zh_TW.html
README_.es      RELEASE-NOTES-de.html RPM-GPG-KEY
README_.fr      RELEASE-NOTES-es.html TRANS.TBL
```

```text
# cd
# umount /mnt/cdrom
$ mount /dev/hda2 on / type ext3 rw / none on /proc type proc rw / usbdevfs on /proc/usb type usbdevfs rw / /dev/hda5 on / type ext3 rw / none on /dev/pts type devpts rw,gid=5,mode=620 / none on /dev/shm type tmpfs rw / none on /proc/sys/fs/binfmt_misc type binfmt_misc rw
# su
Password:
# cd /d
# umount /d
mount: /d: device is busy
# cd /
# umount /d
#
```

能够以这种方式挂载 ISO 9660 镜像在测试制作 CD 镜像的脚本时特别有用。您可以在常规文件中创建镜像，挂载它，并验证其是否正确排列。然后，一旦确定它是正确的，您可以将镜像复制到可写 CD（“烧录”该 CD）。loopback 功能对于挂载软盘镜像也很有用。

### 8.1.4 卸载文件系统：`umount`

`umount` 命令卸载文件系统，将其内容从系统文件层次结构中移除。用法如下：

```text
umount 文件或设备
```

正在卸载的文件系统必须不是*忙碌*的。这意味着没有进程在该文件系统上有打开的文件，并且没有进程以该文件系统上的目录作为当前工作目录：

## 8.2 文件系统管理文件

`/etc/fstab` 文件列出了可以挂载的文件系统。大多数在系统启动时自动挂载。格式如下：

```text
设备  挂载点  文件系统类型  选项  dump 频率  fsck 路径
```

（*dump 频率* 和 *fsck 路径* 是与当前讨论无关的管理功能。）例如，在我们的系统中，文件看起来像这样：
