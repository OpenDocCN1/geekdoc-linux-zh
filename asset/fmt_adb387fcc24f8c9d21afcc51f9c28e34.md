
| `/dev/fd0` | `/mnt/floppy` | `ext2` | `defaults,noauto` | 0 | 0 |

| `/dev/hdc` | `/mnt/cdrom` | `iso9660` | `ro,noauto` | 0 | 0 |

| `/dev/hda1` | `/mnt/dos` | `vfat` | `noauto,dev,exec,suid` | 0 | 0 |

| `/dev/sda4` | `/mnt/zip` | `vfat` | `noauto,dev,exec,suid` | 0 | 0 |

| `/dev/hde1` | `/mnt/flash` | `vfat` | `noauto,dev,exec,suid` | 0 | 0 |

`fstab` 列显示设备名称、文件系统将被挂载的位置、文件系统类型、任何挂载选项、`dump` 命令（在第 23 小时，“Archiving”中讨论）是否需要检查要归档的文件，以及在重启期间检查文件系统的顺序。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_504_0.png)

> 你的文件系统表与此处显示的示例会有所不同，特别是如果你的计算机使用 SCSI 接口。这里描述的文件系统表仅是一个示例。

`fstab` 行显示一个 Linux `ext2` 文件系统；`/proc` 或内核进程目录；OpenLinux 交换目录；一个软盘驱动器（`/dev/fd0`）；CD-ROM 设备（在此列表中，OpenLinux CD-ROM 设备，`/dev/cdrom`，是指向 `/dev/hdc` 的符号链接）；与 Linux `ext2` 分区在同一硬盘上的 DOS 文件系统分区（因为两个系统都使用 `/dev/hda` 设备）；一个 Iomega Zip 驱动器（`/dev/sda4`）的条目；以及闪存 RAM 卡上的 DOS VFAT 文件系统。

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_504_1.png)

> 你应该知道编辑文件系统表本质上是危险的。你在第 21 小时，“Basic System Administration.”中学习了如何添加配额。在添加硬盘、新分区等之前，务必先制作备份副本。确保你手头有 OpenLinux 启动盘（安装期间创建）。如果出现问题，你可以用软盘启动，使用 `mount` 命令将硬盘上的 OpenLinux 分区挂载，然后复制并恢复原始的 `/etc/fstab` 文件。

通常，`root` 操作员挂载和卸载文件系统。如果你听从我的建议，不总是以 `root` 身份运行 Linux，你将必须使用 `su` 命令来挂载和卸载文件系统：

```
# su -c "mount /mnt/cdrom"
```

该命令将插入的 CD-ROM 挂载到 `/mnt/cdrom` 目录。该命令的更正式版本（取决于你的系统中符号链接 `/dev/cdrom` 指向的内容）是

```
# su -c "mount -t iso9660 /dev/hdc /mnt/cdrom"
```

该命令使用 `mount` 命令指定文件系统类型 `iso9660` 和要挂载到 `/mnt/cdrom` 目录的设备 `hdc`（你的可能不同）。

这看起来打字很多吗？如果你想让这个过程更简单，使用 `mount` 命令的 `user` 选项。你就不需要使用 `su` 命令来挂载 CD-ROM、输入密码或输入长命令行。例如，使用你喜欢的文本编辑器（以 `root` 操作员身份）打开 `/etc/fstab` 文件，并将原始的 `fstab` 条目更改为

```
/dev/hdc    /mnt/cdrom    iso9660 noauto,ro,user,dev,exec  0 0
```

`ro` 选项指定设备以只读方式挂载。`exec` 选项将允许任何人从 CD-ROM 运行程序。保存文件以应用更改。你将能够使用以下命令在不成为 `root` 操作员的情况下挂载 CD-ROM：

```
# mount /dev/hdc
```

或

```
# mount /mnt/cdrom
```

这将自动将你的 CD-ROM 的文件系统挂载到 `/mnt/cdrom` 路径。你还将能够使用 `umount` 命令切换你的磁盘，例如：

```
# umount /dev/hdc
```

或

```
# umount /mnt/cdrom
```

尽管你应该仅在 Linux 在独立计算机上使用时才启用这种便利，并且仅针对某些类型的文件系统，例如 CD-ROM，但它很方便，特别是对于可移动文件系统（例如 Iomega Zip 磁盘或闪存内存卡）。另一种可移动文件系统是久经考验的软盘驱动器。下一节讨论软盘驱动器并随后讨论一个软盘实用程序包，可能在 Linux 下处理软盘时使生活更轻松。

## 格式化软盘

本节向你介绍四个可用于从 Linux 命令行格式化软盘的程序。我也一步步带你完成该过程。如果你想备份文件或使用软盘安装和测试新软件，你可能会觉得这些信息有用。你还将学习如何使用 `ext2` 文件系统以 Linux 原生格式格式化然后挂载你的软盘。

软盘设备位于 `/dev` 目录下；其中有相当多。您会找到对应几乎所有类型软盘设备的设备。您可以查看 `/dev` 目录中的软盘设备：

```
# ls /dev/fd*
/dev/fd0      /dev/fd0h880  /dev/fd0u3520  /dev/fd1h1494
/dev/fd1u743
/dev/fd0Compaq0  /dev/fd0u1040  /dev/fd0u360  /dev/fd1h1500
/dev/fd1u1760
/dev/fd0h1440  /dev/fd0u1120  /dev/fd0u3840  /dev/fd1h350
/dev/fd1u1840
/dev/fd0u360  /dev/fd0u1440  /dev/fd0u720  /dev/fd1h410
/dev/fd1u1920
/dev/fd0h1200  /dev/fd0u1600  /dev/fd0u800  /dev/fd1h420
/dev/fd1u2880
/dev/fd0h1440  /dev/fd0u1680  /dev/fd0u820  /dev/fd1h720
/dev/fd1u3290
/dev/fd1u1476  /dev/fd0u1722  /dev/fd0u830  /dev/fd1h880
/dev/fd1u3520
/dev/fd1u4950  /dev/fd0u1743  /dev/fd1  /dev/fd1u1840
/dev/fd1u360  /dev/fd0u1760  /dev/fd1Compaq0  /dev/fd1u1120
/dev/fd1u1680  /dev/fd0u1840  /dev/fd1d360  /dev/fd1u1440
/dev/fd1u720
/dev/fd0h410  /dev/fd0u1920  /dev/fd1h1200  /dev/fd1u1600
/dev/fd0h800  /dev/fd0h420  /dev/fd0u2880  /dev/fd1h1440  /dev/fd1u1680
/dev/fd0h820  /dev/fd0u3200  /dev/fd1h1476  /dev/fd1u1722
/dev/fd0h720  /dev/fd0u830
```

最常用的 3.5 英寸、1.44MB 软盘设备是

- `/dev/fd0` — Drive A

- `/dev/fd1` — Drive B

若干受支持的软盘格式列在 `/etc` 目录中的 `fdprm`，即软盘驱动器参数文件里。请查看文件的一部分：

```
# /etc/fdprm   floppy disk parameter table

# Common disk formats. Names are of the form
# actual media capacity/maximum drive capacity
# (Note: although 5.25" HD drives can format disks at 1.44M, they're
# listed
# as 1200 because that's the common maximum size.)

# 360/360    size sec/t hds trk stre gap rate spec1 fmt_gap
720  9  2  40  0 0x2A 0x02 0xDF  0x50
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_506_0.png)

1280/1280  2400  15  2  80  0  0x1B  0x00  0xDF  0x54

360/720    720   9  2  40  1  0x2A  0x02  0xDF  0x50

720/720   1440   9  2  80  0  0x2A  0x02  0xDF  0x50

720/1440  1440   9  2  80  0  0x2A  0x02  0xDF  0x50

360/1200   720   9  2  40  1  0x23  0x01  0xDF  0x50
