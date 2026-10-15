
Last cylinder +size +sizeM +sizeK (1-1044,def 1044): `+500m`

执行 `p` 更新后的分区表：

```
Command (m for help): p
Disk/dev/sdb: 8589 MB, 8589934592 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
```

| Device Boot Start End Blocks Id System |

| /dev/sdb1 1 62 497983+ 83 Linux |

使用 `w` 子命令将此信息写入磁盘并退出 `fdisk`：

```
Command (m for help): w
The partition table has been alerted!
Calling ioctl() to re-read partition table.
Syncing disks.
```

在命令行提示符处执行 `partprobe` 命令，强制内核重新读取更新的分表信息：

```
# partprobe
```

使用以下任意命令确认分区信息：

```
# fdisk -l /dev/sdb
Disk/dev/sdb: 8589 MB, 8589934592 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = cylinders of 16065 * 512 = 8225280 bytes
```

| Device Boot Start End Blocks Id System |

| /dev/sdb1 1 62 497983+ 83 Linux |

```
# grep sdb /proc/partitions
major minor #blocks name
8 0 497983 sdb1
```

# 创建交换分区

要在第二个 SCSI 磁盘 `/dev/sdb` 上创建一个用作交换分区的分区，请按照以下步骤操作：

在 `/dev/sdb` 磁盘上调用 `fdisk` 命令：

```
# fdisk /dev/sdb
```

## 2. 选择子命令 `n` 添加新分区

它会询问你想要创建一个扩展分区还是主分区。在此演示中，添加主分区 #2。你的输入将显示在以下加粗的文本中：

```
Command (m for help): n
Command action\ce extended
p partition (1-4)
p
Partition number (1-4): 2
```

## 3. 输入你希望分区开始的道面号 501

```
First cylinder (501-1044, default 501): 501
```

## 4. 指定分区大小

你可以输入任何道面号，`fdisk` 将自动计算分区大小。或者，你可以以 KB 或 MB 为单位输入大小。默认使用所有可用磁盘空间。在此演示中，使用 500MB。

```
Last cylinder +size or +sizeM +sizeK (532,522, default 522): +500m
```

## 5. 执行以列出已知的分区类型；其中显示的内容

```
Command (m for help): 1
0 Empty 1e Hidden W95 FAT1 80 Old Minix be Solaris boot
1 FAT12 24 NEC DOS 81 Linux /old Lin bf Slaris
2 XENIX root 39 Plan 9 82 Linux swap / So c1 DRDOS/sec (FAT-
3 XENIX us 3c PartitionMagic 83 Linux c4 DRDOS/sec (FAT-
4 FAT16 <32M 40 Venice 8026 84 OS/2 Hidden: C d6 DRDOS/sec (FAT-
5 Extended 41 PPC PreP Boot 85 Linux extended c7 Syria
6 FAT16 52 SFS 86 NTFS volume size da Non-FS data
7 HPFS/NTFS 44 QNX4.a 87 NTFS volume set de CP/MTOS /.
8 AIX 44 QNX4.x 2nd part 88 Linux plaintext ft De Utility
9 AIX table 44 QNX4.x 3rd part 89 Linux Lum df Bootl
a os/2 Boot Mang 50 OnTrck DM 93 Amoeba el dOS access
b W95 FAT32 51 OnTrck DM6 Aux4 94 Amoeba Beb ee DOS O
c W95 (FAT32) 52 CP/M 95 FSD/OS e4 Speed
w W95 (FAT16) 53 OnTrck DM6 Aux0 88 IBM help me Be fs
f W95 Ext'(ld) 54 OnTrck DM6 Auto a FreeBSD ef
10 OPUS 55 EZ-Drive a6 OpenBSD efi (FAT/12-
11 Hidden FAT12 56 Golden Boo a7 NEXTSTEP f0 Linux/PARISC
12 Compaq 55 Priam Edisk Darwin fl1 Speed
14 Hidden FAT16 <32M 4 61 Speed a9 NetBSD f4 Speed
16 FAT16 63 GNUD of Sysab Darwin f2 secondary
17 Hidden HPFS/NTF6 65 Novell b2 fd auto
18 AST 65 Novell bb fe LANStep
b W95 FAT30 35 Disk bb Wizard had FBT
c Hidden W95 FAT35 PC/IX
```

## 6. 执行 `p` 输出分区表

```
Command (m for help): p
Disk/dev/sdb: 8589 MB, 8589934592 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = cylinders of 16065 * 512 = 822520 bytes
```

| Device Boot Start End Blocks Id System |

| /dev/sdb1 1 62 497983+ 83 Linux |

| /dev/sdb2 63 124 498015 83 Linux |

## 7. 执行 `t` 将 `/dev/sdb2` 的类型更改为 swap (82)

```
Command (m for help): t
Selected partition 2
Hex code (type L to list codes): 82
Changed type of partition 2 to 82 (Linux / Solaris)
```

## 8. 使用 `w` 子命令将此信息写入磁盘并退出 `fdisk`

```
Command (m for help): w
The partition table has been altered
Calling ioctl() to re-read partition table.
Syncing disks.
```

## 9. 在命令行提示符处执行 `partprobe` 命令，强制内核重新读取更新的分区信息

```
# partprobe
```

## 10. 使用以下任意命令确认分区信息

```
# fdisk -l /dev/sdb
Disk/dev/sdb: 8589 MB, 8589934592 bytes
255 heads, 63 sectors/track, 1044 cylinders
Units = cylinders of 16065 * 512 = 822580 bytes
```

| Device Boot Start End Blocks Id System |

| /dev/sdb1 1 62 497983+ 83 Linux |

| /dev/sdb2 63 124 498015+ 82 Linux swap / Solaris |

```
# grep sdb /proc/partitions
```

# 删除分区

删除分区会从分区表中删除分区信息。让我们删除之前创建的 `sdb1` 和 `sdb2`。

## 1. 在 `/dev/sdb` 磁盘上执行 `fdisk` 命令

```
# fdisk /dev/sdb
```

## 2. 执行 `p` 输出分区表
