
要将文件刻入 CD-R/RW 或 DVD-R/RW 盘，你可以使用刻录工具。这些工具中许多是 `cdrecord` 和 `dvdrecord` 程序的接口，以及 `mksofis` 和 `cda2wav`。在 KDE 上，你可以使用 `KOnCD`、`CD-Rh` 和 `CreateCD`；在 GNOME 上，有 `GNOME Toaster`、`GNOME CD Master` 和 `cd-re`。通过 `cdrecord` 和 `dvdrecord`，你可以直接将文件刻入 CD-R/RW。`mksofis` 用于创建 CD 镜像，`cda2wav` 从音乐 CD 采样。对于 DVD+R/RW 驱动器，请使用 `dvd+rw` 工具，如 `growsis` 和 `dvd+-rw-format`（参见第 30 章）。

你也可以一次复制或移动目录。`cp` 和 `mv` 都可以将目录作为第一个目录名称，允许你将目录复制或移动到另一个目录（参见表 10-5）。第一个参数是要复制或移动的目录名称，第二个参数是将其放置的目标目录名称。用于文件的路径结构也适用于移动或复制目录。

你可以同样轻松地将子目录从一个目录复制到另一个目录。要复制目录，`cp` 命令要求你使用 `-r` 选项。`-r` 选项表示“递归”（recursive）。它指示 `cp` 命令复制目录以及其可能包含的任何子目录。换句话说，会复制该目录的整个目录树。在下一个示例中，`thankkyou` 目录被复制到 `oldletters`。现在存在两个 `thankkyou` 子目录，一个在 `letters` 中，另一个在 `oldletters` 中。

```
$ cp -r letters/thankyou oldletters
$ ls -l letters
/thankyou
$ ls -l oldletters
/thankyou
```

## 删除文件和目录：rm 命令

作为 Linux 用户，你会发现你使用的文件数量会迅速增加。在 Linux 中生成文件很容易。应用程序作为编辑器，以及如 `cp` 等命令都可以轻松创建文件。最终，许多文件会变得过时无用。你可以使用 `rm` 命令删除它们。`rm` 命令可以接受任意数量的参数，允许你列出多个文件名并同时删除它们。在下一个示例中，用户删除文件。

使用 `rm` 命令时要小心，因为它是不可的。一旦文件被删除，无法恢复（没有撤销）。当你使用 `-i` 时，系统会对每个文件进行提示并询问是否删除。如果你输入 `y`，文件将被删除。如果你输入其他内容，文件不会删除。在下一个示例中，`rm` 命令被指示在删除每个文件前请求确认。

```
$ rm -i proposal oldprop
Remove proposal? n
Remove oldprop? y
$
```

### 表 10-5：文件操作

| 命令 | 执行 |
|---|---|
| `cp filename filename` | 复制操作接受两个参数：原始文件和新副本的名称。你可以对文件使用路径来跨目录复制：`$ cp today reports/monday` |
| `cp -r dirname dirname` | 将子目录从一个目录复制到另一个目录。复制的目录包括其所有的子目录：`$ cp -r letters/thankyou oldletters` |
| `mv filename filename` | 移动（重命名）。第一个 `mv` 是移动操作。第二个参数可以是新的文件名或目录路径。如果它是目录名称，则文件将字面上移动到该目录，从而更改文件的路径：`$ mv today /home/chris/reports` |
| `mv dirname dirname` | 移动目录。在这种情况下，第一个和最后一个都是目录：`$ mv lets/thankyou oldletters` |
| `ln filename filename` | 为文件创建称为“链接”的附加名称。可以在一个目录中创建一个链接，引用另一个目录中的文件：`$ ln today reports/monday` |
| `rm filenames` | 删除（擦除）文件。可以接受任意数量的文件名作为参数。字面上删除指向该文件的链接。如果一个文件有多个链接，你需要删除所有它们才能删除该文件：`$ rm today weather weekend` |

## 链接：ln 命令

你可以使用 `ln` 命令为文件赋予多个名称，以便从不同的目录访问它。添加的名称通常被称为链接。Linux 支持两种类型的链接：硬链接和符号链接。硬链接字面上是同一个文件的另一个名称，而符号链接要灵活得多，可以在不同系统间工作，而硬链接局限于本地文件系统。此外，硬链接引入了安全隐患，因为它们允许通过可能具有公共访问权限的链接访问你可能保护的原始文件。链接通常通过符号链接实现。

### 符号链接

要设置符号链接，使用带有 `-s` 选项的 `ln` 命令以及两个参数：原始文件名和新添加的文件名。`ls` 操作列出这些文件名，但只会存在一个物理文件。

```
$ ln -s original-file-name added-file-name
```

在下一个示例中，`today` 文件被赋予了附加名称 `weather`。它只是 `today` 文件的另一个名称。

```
$ ls
today
$ ln -s today weather
$ ls
today weather
```

可以通过对同一个文件多次使用 `ln` 命令为文件赋予多个名称。在下一个示例中，`today` 文件被赋予了 `weather` 和 `weekend` 两个名称。

```
$ ln -s today weather
$ ln -s today weekend
$ ls
today weather weekend
```

如果你列出符号链接和文件的完整信息，你会发现显示的信息是不同的。在下一个示例中，用户使用带有 `-l` 选项的命令列出了 `link` 和 `/home/george/veglist` 的信息。行的第一个字符指定文件类型。`link` 的类型表示它是一个符号链接，而不是普通文件。数字项“group”是文件的大小。`link` 的大小只有 4 字节。`link` 只是一个包含另一个文件路径的符号文件，而路径只占用几个字节。

```
$ ls lunch /home/george/veglist
lrw-rw-r-- 1 chris group 4 Feb 14 10:30 lunch
-rw-rw-r-- 1 george group 793 Feb 14 10:30 lunch
```

| command | description |
|---|---|
| `mcopy filename` | 在 MS-DOS 磁盘或 Linux 系统之间复制文件。以下命令将文件从 MS-DOS 软盘复制到您的 Linux 系统：`mcopy filename directory-or-filename`。以下命令将文件从 Linux 复制到软驱器中的 MS-DOS 软盘： |
| `mcd directory-name` | 在 MS-DOS 文件系统上更改目录。 |
| `mdir` | 列出软驱中 MS-DOS 磁盘上的文件。 |
| `mattrib` | 更改 MS-DOS 文件的属性。 |
| `mdel filename` | 删除 MS-DOS 文件。 |
| `mformat` | 在软盘上添加 MS-DOS 文件系统。 |
| `mlabel` | 创建卷标标签。 |
| `mmd directory-name` | 创建 MS-DOS 目录。 |
| `mrd directory-name` | 删除 MS-DOS 目录。 |
| `mread filename` | 将 MS-DOS 文件低级读取（复制）到 Unix。 |
| `mren filename` | 重命名 MS-DOS 文件。 |
| `mtype filename` | 显示 MS-DOS 文件的内容。 |
| `mwrite filename` | 将 Unix 文件低级写入（复制）到 MS-DOS。 |

## 配置 mtools: /etc/mtools.conf

`mtools` 对 MS-DOS 或 Windows 95, 98 或 ME 分区的访问是通过 `/etc/mtools.conf` 文件配置的。该文件列出了若干默认的 MS-DOS 或 Windows 分区和驱动器。每个驱动器或分区都用特定的设备名称标识。您的软驱已经输入，使用设备名称 `/dev/f0` 和 `/dev/fd1` 分别代表第一个第二个软驱。`/etc/mtools.conf` 中的条目格式为设备标签，后跟文件，然后是将您标识的驱动器或分区名称括在引号中。例如，第一个硬盘分区是 MS-DOS 分区，名为 `/dev/hda1`，后续条目将此识别为 MS-DOS 系统上的 C 盘：

```
drive c: file="/dev/hda1"
```

您必须拥有分区的正确名称。设备名称列在 `/etc/fstab` 中，或者可以通过用户桌面上的 Linuxconf 本地磁盘访问面板查看。当您有 SCSI 硬盘时，硬盘分区格式为 `sd`，后跟一个字符和一个分区的数字。例如，`sd` 指向 SCSI 硬盘上的第一个分区。IDE 驱动器的格式为 `hd`，后跟一个字符和一个分区号，代表 IDE 硬盘的第一个分区。

在大多数发行版中，系统已为您安装了默认的 `/etc/mtools.conf` 文件（参见 `/etc/mtools.conf` 示例）。包含 C 盘、一个 SCSI 硬盘以及一个 IDE 分区的配置。两者前面都有 `#` 号注释。如果您有一个 IDE 硬盘（大多数用户都是如此），您需要删除 IDE 硬盘分区条目前的 `#` 符号，并保留 SCSI 分区条目前的 `#` 符号。如果您的 MS-DOS 分区不是第一个（例如是第二个分区），则设备名称必须是该设备名称。例如，MS-DOS 分区将是 `/dev/hda2`。如果您有多个 MS-DOS 分区，可以为每个分区添加条目，并分配不同的标签。以下示例显示了 IDE 驱动器上第四个硬盘分区的 `sd` 标签：

```
#tux floppy drives
drive a: file="/dev/fd0" exclusive mformat_only
drive b: file="/dev/fd1" exclusive mformat_only
# First SCSI hard disk partition
drive c: file="/dev/sdb1"
# First IDE hard disk partition
drive d: file="/dev/hda1"
drive e: file="/dev/hda5"
#dosemu floppy image
drive n: file="/var/lib/dosemu/diskimage"
#dosemu hdimage
drive q: file="/var/lib/dosemu/diskimage" offset=8832
#Atari ramdisk image
drive o: file="/tmp/atari_rd" offset=136
mtools_lower_case=1
```

## 将文件复制到 DOS 分区

一旦引用了 DOS 硬盘分区，您就可以使用它们的驱动器字母将文件复制到或从 Linux 分区。以下命令将 `mydoc.html` 文件复制到 c 分区下的 `webstuff` 目录并重命名为 `mydocht`。注意这里使用的是正斜杠而不是反斜杠。

```
$ mcopy mypage.html c:/webstuff/mypag.htm
```

由于 DOS 和 Linux 文本文件中换行符的，在将 DOS 文本文件复制到 Linux 分区时，应始终使用 `-t` 选项。以下命令将 `mydoc.txt` 文件从 `c/project` 目录复制到 `/newdocs`

```
$ mcopy -t c:/project/mydoc.txt /newdocs
```

## 归档和压缩文件

归档用于备份文件或将其合并为一个包，然后可以作为单个文件通过互联网传输，或发布到 FTP 站点以便下载。Linux 和 Unix 系统上使用的标准归档工具是 `tar`，它有多个 GUI 前端。您有多种压缩程序可以选择，包括 GNU zip `gzip`、Zip、`bzip` 和 `compress`。

### 使用 File Roller 归档和压缩文件

Red Hat 提供了 File Roller 工具。File Roller 是一个归档文件的图形界面，允许您创建、提取和管理压缩归档。您有多种压缩程序可以选择，包括 GNU zip `gzip`、Zip、`bzip` 和 `compress`。

| 选项 | 描述 |
| :--- | :--- |
| `t` | 列出归档中的文件名。 |
| `r` | 将文件追加到归档中。 |
| `U` | 使用新文件和修改的文件更新归档；仅添加自归档以来修改的文件或归档中已不存在的文件。 |
| `--delete` | 从归档中删除文件。 |
| `w` | 在归档每个文件之前等待用户确认；允许你选择性地更新归档。 |
| `x` | 从归档中提取文件。 |
| `m` | 从归档中提取文件时，不分配新的时间戳。 |
| `M` | 创建可能存储在多张软磁盘上的多卷归档。 |
| `f archive-name` | 将磁带归档保存到文件归档名称，而不是默认磁带设备。当给定归档名称时，f 将 tar 归档存在该名称的文件。 |
| `f device-name` | 将 tar 归档保存到设备（如软磁盘或磁带）。`/dev/fd0` 是你的软磁盘的设备名称；默认设备存储在 `/etc/default/tar-file` 中。 |
| `v` | 在归档时显示每个文件名。 |
| `z` | 使用 `gzip` 压缩或解压归档文件。 |
| `j` | 使用 `bzip2` 压缩或解压归档文件。 |

## 提取归档

用户可以使用 `x` 选项从磁带上提取目录。`xf` 选项从归档文件或设备中提取文件。`tar` 提取操作会生成所有子目录。在下一个示例中，`xf` 选项指示 `tar` 从 tar 文件 `myfile.tar` 中提取所有文件和子目录：

```
$ tar xf myfile.tar
mydir/
mydir/reports/
mydir/reports/weather
mydir/reports/monday
mydir/reports/friday
mydir/mymeeting
mydir/party
```

你使用 `r` 选项向已创建的归档中添加文件。`r` 选项将文件追加到归档中。在下一个示例中，用户将 `letters` 目录中的文件文件追加到 `myfile.tar` 归档中。在这里，目录 `mydocs` 及其文件被添加到 `myfile.tar` 归档中：

```
$ tar rv myfile.tar mydocs
mydocs/
mydocs/doc1
```

## 更新归档

如果你更改了之前归档的目录中的任何文件，可以使用 `u` 选项指示 `tar` 使用你修改的文件更新归档。`tar` 命令会将每个归档文件的最后更新时间与用户的副本进行比较，并复制自上次归档以来更改的任何文件。这些目录中新创建的文件也会添加到归档中。在下一个示例中，用户用 `mydir` 目录中任何最近修改或新创建的文件更新 `myfile.tar` 文件。在这种情况下，`gifts` 文件被添加到了 `mydir` 目录。

```
$ tar uv myfile.tar mydir
mydir/
mydir/gifts
```

如果你需要查看归档中存储了哪些文件，可以使用带有 `t` 选项的 `tar` 命令。下一个示例列出了 `myfile.tar` 归档中存储的所有文件：

```
tar tv myfile.tar
drwxr-xr-x root/root 0000-10-24 21:38:18 mydir/
drwxr-xr-x root/root 0000-10-24 21:38:51 mydir/reports/
-rw--r--r root/root 2200-10-24 21:38:40 mydir/reports/weather
-rw--r--r root/root 2200-10-24 21:38:45 mydir/reports/monday
-rw--r--r root/root 2200-10-24 21:38:51 mydir/reports/friday
-rw--r--r root/root 2200-10-24 21:38:18 mydir/mymeeting
-rw--r--r root/root 2200-10-24 21:36:42 mydir/party
drwxr-xr-x root/root 0000-10-24 21:48:45 mydocs/
-rw--r--r root/root 2200-10-24 21:48:45 mydocs/doc1
drwxr-xr-x root/root 0000-10-24 21:54:03 mydir/
-rw--r--r root/root 2200-10-24 21:54:03 mydir/gifts
```

## 归档到软磁盘

要将文件备份到特定设备，请指定设备为归档。对于软磁盘，你可以指定软磁盘驱动器。请使用空白软磁盘。此操作将删除磁盘之前存在的所有数据。在下一个示例中，用户在 `/dev/fd0` 设备上创建一个归档，并将其复制到 `mydir` 目录中的所有文件中：

```
$ tar cf /dev/fd0 mydir
```

要在设备上提取备份的文件，请使用 `x` 选项：

```
$ tar xf /dev/fd0 mydir
```

| 选项 | 说明 |
| :--- | :--- |
| `-c` | 将文件的压缩版本发送到标准输出；列出的每个文件分别进行压缩：`gzip -c mydata preface > myfiles.gz` |
| `-d` | 解压缩压缩文件；或者，您可以使用 `gunzip`：`gzip -d myfiles.gz`; `gunzip myfiles.gz` |
| `-h` | 显示帮助列表。 |
