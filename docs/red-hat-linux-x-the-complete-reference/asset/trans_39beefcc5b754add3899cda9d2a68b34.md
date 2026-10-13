
![](img/32a48d8db4c23e6e2eb70d1e5034c976_243_0.png)

## ABC Amber CHM Converter Trial version

Please register to remove this banner.

http://www.processestext.com/abchm.html

## The mtools Utilities: msdos

您的 Linux 系统提供了一组名为 *mtools* 的实用程序，可让您轻松访问格式化为 MS-DOS 的软盘和硬盘（请参阅表 10-6）。

### Copying Files to a DOS Floppy

*mcopy* 命令可让您在软盘驱动器中的 MS-DOS 软盘或硬盘上的 Windows 分区之间复制文件。无需执行挂载等特殊操作即可使用。借助 mtools，您无需挂载 MS-DOS 分区即可访问它。对于 MS-DOS 软盘，将磁盘放入软盘驱动器，然后您就可以使用 mtool 命令访问这些文件。例如，要将文件从 MS-DOS 软盘复制到 Linux 系统，请使用 *mcopy* 命令。您使用 *a:* 指定 MS-DOS 磁盘作为 A 驱动器。与普通 DOS 路径名不同，使用 mtool 命令的路径名使用正斜杠而不是反斜杠。A 驱动器上的 *docs* 目录将通过路径名 *a:/docs* 引用，而不是 *a:\docs*。与 MS-DOS 默认将第二个参数设为当前目录不同，您始终需要为 *mcopy* 提供第二个参数。下一个示例将文件 *mydata* 复制到 MS-DOS 磁盘，然后将磁盘上的 *preface* 文件复制到当前 Linux 目录。

```
$ mcopy mydata a:
$ mcopy a:/preface .
```

**Note** 目前，mtools 无法访问 Windows XP、NT 和 2000 NTFS 分区。

### mtools Commands

您可以使用 *mdir* 命令列出 MS-DOS 磁盘上的文件，并使用 *mcd* 命令在其中更改目录。下一个示例列出软盘驱动器中 MS-DOS 磁盘上的文件，然后更改到该驱动器上的 *docs* 目录：

```
$ mdir a:
$ mcd a:/docs
```

大多数标准 MS-DOS 命令都作为 mtool 操作可用。您可以使用 *mmd* 创建 MS-DOS 目录，并使用 *mdel* 删除 MS-DOS 文件。表 10-6 中提供了 mtool 命令列表。例如，要显示第二个软盘驱动器中 MS-DOS 磁盘上驱动器 B 上的文件，请使用 *mtype* 和以 *b/* 为前缀的文件名：

```
$ mtype b:/readme
```

### Table 10-6: The mtools Access Commands

| 命令 | 执行 |
|---|---|
| `mcopy filename filename` | 将文件从 MS-DOS 磁盘复制到 Linux 系统或反之。以下命令将文件从 MS-DOS 软盘复制到 Linux 系统：`mcopy a:/filename directory-or-filename` 以下命令将文件从 Linux 复制到软盘驱动器中的 MS-DOS 软盘：`mcopy filename a:/filename` |
| `mcd directory-name` | 在您的 MS-DOS 文件系统上更改目录。 |
| `mdir` | 列出软盘驱动器中 MS-DOS 磁盘上的文件。 |
| `mattrib` | 更改 MS-DOS 文件的属性。 |
| `mdel filename` | 删除 MS-DOS 文件。 |
| `mformat` | 在软盘上添加 MS-DOS 文件系统。 |
| mlabel | 创建卷标。 |
| mmd directory-name | 创建 MS-DOS 目录。 |
| mrd directory-name | 删除 MS-DOS 目录。 |
| mread filename filename | 将 MS-DOS 文件低级读取（复制）到 Unix。 |
| mren filename filename | 重命名 MS-DOS 文件。 |
| mtype filename | 显示 MS-DOS 文件的内容。 |
| mwrite filename filename | 将 Unix 文件低级写入（复制）到 MS-DOS。 |

### Configuring mtools: /etc/mtools.conf

mtools 对 MS-DOS 或 Windows 95、98 或 ME 分区的访问由 /etc/mtools.conf 文件配置。此文件列出了多个默认的 MS-DOS 或 Windows 分区和磁盘驱动器。每个驱动器或分区都由特定的设备名称标识。软盘驱动器的条目已预先输入，使用设备名称 /dev/fd0 和 /dev/fd1 分别表示第一个和第二个软盘驱动器。/etc/mtools.conf 文件中的条目形式为驱动器标签，后跟术语 file 和等号，然后是您希望与此标签关联的驱动器或分区的设备名称。设备名称用引号括起来。例如，假设第一个硬盘分区是 MS-DOS 分区，其设备名称为 /dev/hda1，则以下条目将标识它为 MS-DOS 系统上的 C 驱动器：

```
drive c: file="/dev/hda1"
```

您必须为分区提供正确的设备名称。这些设备名称列在 /etc/fstab 文件中，也可以在 root 用户桌面上的 Linuxconf 本地驱动器访问面板中查看。如果您有 SCSI 硬盘，则硬盘分区形式为 sd，后跟硬盘的字符和其中的分区号。例如，sda1 指的是 SCSI 硬盘上的第一个分区。IDE 硬盘形式为 hd，后跟字符和分区号——hda1 指的是 IDE 硬盘上的第一个分区。

在大多数发行版中，默认的 /etc/mtools.conf 文件已为您安装（请参阅以下 /etc/mtools.conf 示例）。该文件对 C 驱动器有注释条目：一个用于 SCSI 硬盘分区，一个用于 IDE 分区。两者都以前面的 # 注释掉。如果您有 IDE 硬盘（大多数用户都有），则需要从 IDE 硬盘分区条目中删除前面的 # 符号，并保留 SCSI 分区条目前面的 # 符号。此外，如果 IDE 硬盘上的 MS-DOS 分区不是第一个分区，则必须更改设备名称。例如，如果 MS-DOS 分区是第二个分区，则设备名称为 /dev/hda2。如果您有多个 MS-DOS 分区，可以为每个分区添加条目，并为每个分区分配不同的标签。以下示例将 d: 标签分配给 IDE 驱动器上的第四个硬盘分区：

```
drive d: file="/dev/hda4"
```

### /etc/mtools.conf

```
# Linux floppy drives
drive a: file="/dev/fd0" exclusive mformat_only
drive b: file="/dev/fd1" exclusive mformat_only
# First SCSI hard disk partition
#drive c: file="/dev/sda1"
# First IDE hard disk partition
drive c: file="/dev/hda1"
drive d: file="/dev/hda5"
```

```
#dosemu floppy image
drive m: file="/var/lib/dosemu/diskimage"
#dosemu hdimage
drive n: file="/var/lib/dosemu/diskimage" offset=8832
#Atari ramdisk image
drive o: file="/tmp/atari_rd" offset=136
mtools_lower_case=1
```

### Copying Files to a DOS Partition

一旦引用了 DOS 硬盘分区，您就可以使用其驱动器号将文件从 Linux 分区复制到它们并从它们复制到 Linux 分区。以下命令将文件 mydoc.html 复制到 c: 分区中的 webstuff 目录并将其重命名为 mydoc.htm。请注意使用正斜杠而不是反斜杠。

```
$ mcopy mypage.html c:/webstuff/mypag.htm
```

由于 DOS 和 Linux 处理文本文件中的换行符的方式不同，因此在将 DOS 文本文件复制到 Linux 分区时应使用 -t 选项。以下命令将 c:/project 目录中的 mydoc.txt 文件复制到 /newdocs 目录：

```
$ mcopy -t c:/project/mydoc.txt /newdocs
```

## Archiving and Compressing Files

归档用于备份文件或将它们组合成一个包，然后可以作为一个文件通过 Internet 传输或发布到 FTP 站点以便轻松下载。Linux 和 Unix 系统上使用的标准归档实用程序是 tar，有多个 GUI 前端。您可以从中选择多个压缩程序，包括 GNU zip（gzip）、Zip、bzip 和 compress。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_247_0.png)

### Archiving and Compressing Files with File Roller

Red Hat 提供了 File Roller 工具（可从“附件”菜单访问），它作为归档和压缩文件的 GUI 前端运行，让您可以使用 GUI 界面执行 zip、gzip、tar 和 bzip2 操作（请参阅图 10-4）。您可以检查归档内容、提取所需文件并创建新的压缩归档。当您创建归档时，您可以通过指定文件名扩展名来确定其压缩方法，例如 gzip 的 .gz 或 bzip2 的 .bz2。您可以从“文件类型”菜单中选择不同的扩展名，也可以自行输入扩展名。要同时归档和压缩文件，您可以选择组合扩展名，如 .tar.bz2，它使用 tar 归档并使用 bzip2 压缩。单击“添加”按钮将文件添加到归档。要从归档中提取文件，请打开归档以显示归档文件列表。然后，您可以单击“提取”按钮提取特定文件或整个归档。其他可用的 GUI 工具有 guiTAR、LnxZip、Ark、KArchive 和 Xtar。

![](img/32a48d8db4c23e6e2eb70d1e5034c976_248_0.png)

Figure 10-4: File Roller archiving and compression tool

### Archive Files and Devices: tar

tar 实用程序为文件和目录创建归档。使用 tar，您可以归档特定文件，在归档中更新它们，并根据需要向该归档添加新文件。您甚至可以归档整个目录及其所有文件和子目录，所有这些都可以从归档中恢复。tar 实用程序最初设计用于在磁带上创建归档。术语 tar 代表 tape archive。您可以在任何设备上创建归档，例如软盘，或创建归档文件来保存归档。tar 实用程序非常适合备份文件或将多个文件组合成单个文件以通过网络传输（File Roller 是 tar 的 GUI 接口）。

> Note 作为 tar 的替代方案，您可以使用 pax。pax 设计用于处理不同类型的 Unix 归档格式，如 cpio、bcpio 和 tar。您可以提取、列出和创建归档。如果您处理的是使用不同归档格式的 Unix 系统创建的归档，pax 会很有帮助。

### Displaying Archive Contents

GNOME 和 K Desktop 中的两个文件管理器都能够自动显示 tar 归档文件的内容。内容显示为目录中的文件一样。您可以将文件列为图标或详细信息，按名称、类型或其他字段排序。您甚至可以显示文件内容。单击文本文件会使用文本编辑器打开它，图像会使用图像查看器显示。如果文件管理器无法确定用于显示文件的程序，它会提示您选择一个应用程序。两个文件管理器都可以在远程文件系统上的归档上执行相同的操作，例如 FTP 站点上的 tar 归档。您可以获取其内容的列表，甚至阅读其 readme 文件。Nautilus 文件管理器（GNOME）也可以提取归档。右键单击“归档”图标并选择“提取”。

### Creating Archives

在 Linux 上，tar 通常用于在设备或文件上创建归档。您可以使用 f 选项和设备或文件名将 tar 指向将文件归档到特定设备或文件。下一示例显示了使用 f 选项的 tar 命令的语法。设备或文件名通常称为归档名称。创建 tar 归档的文件时，文件名通常带有 .tar 扩展名。这只是一种约定，并非必需。您可以列出任意多个文件名。如果目录名称是
