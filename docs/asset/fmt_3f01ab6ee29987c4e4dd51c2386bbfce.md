
Samba 使 Linux 计算机能够作为一个安全、复杂的文件和打印服务器。到此时，你应该已经成功运行了一个配置良好的 Samba 服务器，并学习了使 Samba 实用的命令和选项。你还学习了几个关于排查 Samba 设置的技巧。

Samba 以及组成 Samba 套件的各种程序提供了许多高级选项。有关 Samba 的更多信息，请阅读你发行版光盘中 `/usr/doc/HOWTO/SMB-HOWTO` 的 Samba HOWTO。最后，你可以在 `http://www.samba.org` 找到大量关于 Samba 信息。

# 系统管理与维护

## 第三部分

### 本部分

- 文件系统、磁盘和其他设备 423
- 使用 Linux 打印 463
- TCP/IP 网络管理 489
- 连接到互联网 543
- 红帽图形化管理工具 569
- 基础系统管理 609
- 高级系统管理 647
- GNU 项目实用 663
- 备份与恢复 695
- 系统安全 709

# 文件系统、磁盘，和其他设备

作者：David Pitts

## 本章内容

* 字符设备 424
* 块设备 425
* 文件系统 426
* `mount` 命令 426
* 用户挂载工具 431
* 设置文件系统 431
* 创建新文件系统 433
* 使用 fsck 图形化创建和编辑文件系统 436
* 修复文件系统 439
* 各种硬件 441
* 字符设备 451

## 字符设备

Linux 设计中最简单且优雅的方面之一是将一切都表示为文件。甚至存储文件的设备也被表示为文件。

硬件设备与提供接口的驱动程序相关；代表硬件设备（或简称设备）的特殊文件保存在 `/dev` 目录下。设备可以是块设备或字符设备。

设备是指可以从中读取字符序列的设备——例如在键盘上键入按键序列或通过串口行发送的字节序列。块设备是存储数据并提供对其所有部分的平等访问设备；软磁盘和硬盘都是块设备。块设备有时被称为随机访问设备，而字符设备有时被称为顺序访问设备。对于后者，你可以从硬盘的任何随机部分获取数据，但你必须按照发送的顺序从串口行检索数据。

当你对文件执行某些操作时，内核可以通过查看其模式（或位置）判断出涉及的文件是否为设备。不同的主设备号和次设备号区分不同的设备节点。主设备号告诉内核该设备节点代表它的哪一个驱动程序。例如，主设备数为 3 的块设备是 IDE 磁盘，主设备数为 8 的块设备是 SCSI 磁盘。每个驱动程序负责其所驱动硬件的多个实例，这些实例由次设备号的值指示。例如，次号为 0 的 SCSI 磁盘代表“第一个” SCSI 磁盘，而次号 1 到 15 代表其上 15 个可能的分区。内核会为你打印主、次设备号：

```
ls -l --sort /dev/
brw-rw---- 1 root disk 8 0 Sep 1994 /dev/sda
brw-rw---- 1 root disk 8 1 Sep 1994 /dev/sda1
brw-rw---- 1 root disk 8 2 Sep 1994 /dev/sda2
brw-rw---- 1 root disk 8 3 Sep 1994 /dev/sda3
brw-rw---- 1 root disk 8 4 Sep 1994 /dev/sda4
brw-rw---- 1 root disk 8 5 Sep 1994 /dev/sda5
brw-rw---- 1 root disk 8 6 Sep 1994 /dev/sda6
brw-rw---- 1 root disk 8 7 Sep 1994 /dev/sda7
brw-rw---- 1 root disk 8 8 Sep 1994 /dev/sda8
brw-rw---- 1 root disk 8 9 Sep 1994 /dev/sda9
brw-rw---- 1 root disk 8 10 Sep 1994 /dev/sda10
brw-rw---- 1 root disk 8 11 Sep 1994 /dev/sda11
brw-rw---- 1 root disk 8 12 Sep 1994 /dev/sda12
brw-rw---- 1 root disk 8 13 Sep 1994 /dev/sda13
brw-rw---- 1 root disk 8 14 Sep 1994 /dev/sda14
brw-rw---- 1 root disk 8 15 Sep 1994 /dev/sda15
brw-rw---- 1 root disk 8 16 Sep 1994 /dev/sdb
```

# 文件系统、磁盘和其他设备

## 第15 章

`ls -1` 的 (`--sort=none`) 选项确保设备按正确顺序显示。如果你只使用 `ls -1`，条目将按字母排序，`/dev/sda1` 在 `/dev/sda2` 之前。输出左侧的 `b` 表示这些条目是块设备（字符设备由 `c` 表示）。主、次设备号出现在时间字段之前，并用逗号分隔（这是 `ls -1` 占据的位置）。

## 块设备

如果你只有一个文件要存储，可以将其直接放在块设备上并读取。块设备具有固定容量，但你需要某种方法来标记数据的结束。块设备在大多数方面与文件相似，只是普通文件的长度由其包含的数据决定，而块设备的“长度”是其总容量。如果你向 100MB 的块设备写入 1MB 并读取内容，你会得到 1MB 的数据。考虑到这一限制，许多工具编码了可用数据量，因此适用于直接存储在块设备——例如 `tar` 和 `cpio` 适用于所有人，而 `dump` 仅适用于管理员（因为它需要访问块设备）。要将整个家目录备份到软磁盘，你输入：

```
$ cp $HOME /dev/fd0
$ find $HOME -print0 | cpio >/dev/fd0
```

`find` 和 `cpio` 的 `-print0` 和 `-0` 选项确保备份的文件名用 NUL 代替换行符。这确保了包含换行符的文件名。Unix 文件名中的非法字符是斜杠和 ASCII NULL。

这些备份工具专门用于将备份写入任何文件：事实上，它们是为顺序访问设备设计的，如磁带。

![](img/fbfff30e42d50bc753110a281d6cf_462_0.png)

## 文件系统

当你有多个数据项时，需要在设备上某种组织文件的方法。这些方法被称为文件系统。Linux 允许你使用任何组织方法来管理其存储设备。例如，你可以在软磁盘上使用 MS-DOS 文件系统，在硬盘上使用更快的 ext2 文件系统。

Linux 支持许多不同的文件系统：`ext2` 是它为 Linux 设计且非常高效。其他文件系统用于与其他系统兼容；例如软磁盘上的 `mdos` 和 `vfat` 文件系统；这些是 MS-DOS 和 Windows 95 的原生文件系统。在红帽 Linux 6.0 下，某些文件系统被构建在内核中：

```
$ /proc/filesystems
ext2
nodev proc
nodev iso9660
devpts
```

某些文件系统作为可加载模块可用：

```
$ ls /lib/modules/* -uname -r
autofs.0 binfmt_aut.0 binfmt_java.0 binfmt_misc.0
coda.0 fat.0 hfs.0 hpffs.0
lockd.0 minix.0 mdos.0 ncpfs.0
nnfs.0 nfsd.0 nls_cp437.0 nls_cp737.0
lls_cp775.0 nls_cp850.0 nls_cp852.0 nls_cp855.0
lls_cp857.0 nls_cp860.0 nls_cp861.0 nls_cp862.0
lls_cp863.0 nls_cp865.0 nls_cp866.0
lls_cp869.0 nls_cp874.0 nls_08851-1.0 nls_08859-15.0
lls_08859-2.0 nls_08859-3.0 nls_08859-4.0
lls_08859-6.0 nls_08859-8.0 nls_08859-9.0
lls_k018-r.0 romfs.0 smbfs.0
ufs.0 vfat.0
```

## mount 命令

使用 `mount` 命令将块设备挂载到文件系统上。你需要指定哪个设备包含文件系统、它是什么类型，以及在目录层次结构的哪个位置挂载它。

# 文件系统、磁盘及其他设备

## 15 章

`mount` 命令的格式如下：

```bash
mount [-t type] [-o options] device mount-point
```

`device` 必须是一个块设备；如果它包含冒号，则它可以是另一台用于挂载文件系统的机器名称（见第 17 章）。`mount-point` 应该是一个已存在的目录（否则会报错）；文件系统将出现在该位置。（该目录中原先的任何内容都将被隐藏）。文件系统类型和选项是可选的，且选项的种类和含义取决于所挂载文件系统的类型。如果你想要挂载的文件系统已经在 `/etc/fstab` 文件中指定了，那么你只需要指定挂载点或设备名称；其他细节将由 `mount` 命令从 `/etc/fstab` 中读取。以下是 `mount` 命令的一个用用示例：
