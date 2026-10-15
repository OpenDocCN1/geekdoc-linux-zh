

## 配置 mtools：/etc/mtools.conf

mtools 对 MS-DOS 或 Windows 95、98 或 ME 分区的访问由 /etc/mtools.conf 文件配置。此文件列出了多个不同的默认 MS-DOS 或 Windows 分区和磁盘驱动器。每个驱动器或分区都用特定的设备名称标识。软盘驱动器的条目已预先输入，使用设备名称 /dev/fd0 和 /dev/fd1 分别表示第一个和第二个软盘驱动器。/etc/mtools.conf 文件中的条目形式为驱动器标签，后跟 file 和等号，然后是您希望与此标签关联的驱动器或分区的设备名称。设备名称用引号括起来。例如，假设第一个硬盘分区是 MS-DOS 分区且设备名称为 /dev/hda1，则以下条目将此分区标识为 MS-DOS 系统上的 C 驱动器：

```text
drive c: file="/dev/hda1"
```

您必须拥有分区的正确设备名称。这些设备名称列在 /etc/fstab 文件中，也可以在 root 用户桌面上的 Linuxconf 本地驱动器访问面板中查看。如果您有 SCSI 硬盘，则硬盘分区形式为 sd，后跟硬盘的字符和其中的分区号。例如，sda1 指的是 SCSI 硬盘上的第一个分区。IDE 硬盘形式为 hd，也后跟字符和分区号——hda1 指的是 IDE 硬盘上的第一个分区。

在大多数发行版中，默认的 /etc/mtools.conf 文件已为您安装（请参阅以下 /etc/mtools.conf 示例）。该文件对 C 驱动器有注释条目：一个用于 SCSI 硬盘分区，一个用于 IDE 分区。两者均以前置的 # 注释掉。如果您有 IDE 硬盘（大多数用户都是），则需要从 IDE 硬盘分区条目中删除前置的 # 符号，并保留 SCSI 分区条目前面的 # 符号。此外，如果您的 IDE 硬盘上的 MS-DOS 分区不是第一个分区，则必须更改设备名称。例如，如果 MS-DOS 分区是第二个分区，则设备名称将为 /dev/hda2。如果您有多个 MS-DOS 分区，可以为每个分区添加条目，并为每个分区分配不同的标签。以下示例将 d: 标签分配给 IDE 驱动器上的第四个硬盘分区：

```text
drive d: file="/dev/hda4"
```

### /etc/mtools.conf

```text
# Linux floppy drives
drive a: file="/dev/fd0" exclusive mformat_only
drive b: file="/dev/fd1" exclusive mformat_only
# First SCSI hard disk partition
#drive c: file="/dev/sda1"
# First IDE hard disk partition
drive c: file="/dev/hda1"
drive d: file="/dev/hda5"
# dosemu floppy image
drive m: file="/var/lib/dosemu/diskimage"
# dosemu hdimage
drive n: file="/var/lib/dosemu/diskimage" offset=8832
# Atari ramdisk image
drive o: file="/tmp/atari_rd" offset=136
mtools_lower_case=1
```

## 复制文件到 DOS 分区

一旦 DOS 硬盘分区被引用，您就可以使用其驱动器号在它们之间以及与 Linux 分区之间复制文件。以下命令将文件 mypage.html 复制到 c: 分区的 webstuff 目录中并重命名为 mypage.htm。请注意使用正斜杠而不是反斜杠。

```text
$ mcopy mypage.html c:/webstuff/mypage.htm
```

由于 DOS 和 Linux 处理文本文件换行符的方式不同，因此在将 DOS 文本文件复制到 Linux 分区时应始终使用 -t 选项。以下命令将 c:/project 目录中的 mydoc.txt 文件复制到 /newdocs 目录：

```text
$ mcopy -t c:/project/mydoc.txt /newdocs
```

## 归档和压缩文件

归档用于备份文件或将它们组合成一个包，然后可以通过 Internet 传输为一个文件或发布在 FTP 站点上以便轻松下载。Linux 和 Unix 系统上使用的标准归档实用程序是 tar，其中存在多个 GUI 前端。您可以从中选择的压缩程序包括 GNU zip（gzip）、Zip、bzip 和 compress。

### 使用 File Roller 归档和压缩文件

Red Hat 提供了 File Roller 工具（可从 Accessories 菜单访问），它作为归档和压缩文件的 GUI 前端运行，让您可以使用 GUI 界面执行 zip、gzip、tar 和 bzip2 操作（见图 10-4）。您可以检查归档内容、提取所需文件并创建新的压缩归档。当您创建归档时，您可以通过指定其文件名扩展名来确定其压缩方法，例如 gzip 使用 .gz 或 bzip2 使用 .bz2。您可以从 File type 菜单中选择不同的扩展名，或自行输入扩展名。要同时归档和压缩文件，您可以选择组合扩展名，如 .tar.bz2，它既使用 tar 归档又压缩

![图 10-4：File Roller 归档和压缩工具](img/6c226e8ba1efd427dec3bf582418d33f_235_0.png)

