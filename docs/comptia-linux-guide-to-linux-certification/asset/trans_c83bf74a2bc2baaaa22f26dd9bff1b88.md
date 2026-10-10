

![](img/c27875544958897d817484d558c208c8_520_0.png)

或者，你可以在使用 `dump` 命令时指定文件系统挂载点。命令 `dump -0uf /dev/st0 /data` 与前一个示例中使用的命令等效。

`/etc/dumpdates` 文件的内容现在显示已经执行了完整备份：

```bash
[root@server1 ~]# cat /etc/dumpdates
/dev/sda3 0 Sat Aug 28 10:39:12 2015 -0400
[root@server1 ~]#
```

要执行第一次增量备份并查看 `/etc/dumpdates` 文件的内容，你可以将新磁带放入 SCSI 磁带驱动器并执行以下命令：

```bash
[root@server1 ~]# dump -1uf /dev/st0 /dev/sda3
DUMP: Date of this level 1 dump: Sat Aug 28 10:41:09 2015
DUMP: Date of last level 0 dump: Sat Aug 28 10:39:12 2015
DUMP: Dumping /dev/sda3 (/data) to /dev/st0
DUMP: Label: none
DUMP: Writing 10 Kilobyte records
DUMP: mapping (Pass I) [regular files]
DUMP: mapping (Pass II) [directories]
DUMP: estimated 255 blocks.
DUMP: Volume 1 started with block 1 at: Sat Aug 28 10:41:10 2015
DUMP: dumping (Pass III) [directories]
DUMP: dumping (Pass IV) [regular files]
DUMP: Closing /dev/sda3
DUMP: Volume 1 completed at: Sat Aug 28 10:41:10 2015
DUMP: Volume 1 250 blocks (0.24MB)
DUMP: 250 blocks (0.24MB) on 1 volume(s)
DUMP: finished in less than a second
DUMP: Date of this level 1 dump: Sat Aug 28 10:41:09 2015
DUMP: Date this dump completed: Sat Aug 28 10:41:10 2015
DUMP: Average transfer rate: 0 kB/s
DUMP: DUMP IS DONE
[root@server1 ~]# cat /etc/dumpdates
/dev/sda3 0 Sat Aug 28 10:39:12 2015 -0400
/dev/sda3 1 Sat Aug 28 10:41:09 2015 -0400
[root@server1 ~]#
```

要查看归档的内容，你可以指定 `restore` 命令的 `-t` 选项，后跟归档信息。要查看之前执行的完整备份的内容，你可以将相应的磁带放入磁带驱动器并执行以下命令：

```bash
[root@server1 ~]# restore -tf /dev/st0
Dump date: Sat Aug 28 10:39:12 2015
Dumped from: the epoch
Level 0 dump of /data on server1.class.com:/dev/sda3
Label: none
2 .
11 ./lost+found
12 ./inittab
13 ./hosts
14 ./issue
17 ./aquota.user
15 ./aquota.group
[root@server1 ~]#
```

要提取上述输出中显示的完整备份，你可以指定 `restore` 命令的 `-r` 选项，后跟归档信息。此外，你可以指定 `-v` 选项来列出已恢复的文件名，如以下示例所示：

```bash
[root@server1 ~]# restore -vrf /dev/st0
Verify tape and initialize maps
Input is from a local file/pipe
Input block size is 32
Dump date: Sat Aug 28 10:39:12 2015
Dumped from: the epoch

Level 0 dump of /data on server1.class.com:/dev/sda3
Label: none
Begin level 0 restore
Initialize symbol table.
Extract directories from tape
Calculate extraction list.
Make node ./lost+found
Extract new leaves.
Check pointing the restore
extract file ./inittab
extract file ./hosts
extract file ./issue
extract file ./aquota.group
extract file ./aquota.user
Add links
Set directory mode, owner, and times.
Check the symbol table.
Check pointing the restore
[root@server1 ~]#
```

## 使用刻录软件

`tar`、`cpio` 和 `dump` 命令以逐字符或逐块格式将数据复制到备份介质中。因此，它们通常用于创建磁带和硬盘介质上的文件备份副本，因为这些介质接受该格式的数据。

要将文件写入 CD 和 DVD 介质，你必须使用一个允许你选择要复制的数据、组织该数据、构建 CD 或 DVD 文件系统，并将整个文件系统（包括数据）写入 CD 或 DVD 的程序。回顾第 2 章，执行此操作的程序被称为光盘刻录软件。图 11-2 展示了 **GnomeBaker CD/DVD Writer** 光盘刻录软件。你可以以 root 用户身份使用 `yum install gnomebaker` 命令在 Fedora 20 系统上安装 GnomeBaker CD/DVD Writer，并通过导航至 Activities、Show Applications、GnomeBaker CD/DVD Writer 从 GNOME 桌面启动它。

![](img/c27875544958897d817484d558c208c8_522_0.png)

图 11-2 GnomeBaker CD/DVD Writer

## 软件安装

大多数 Linux 管理员的主要职责通常包括安装和维护软件包。Linux 软件可以是已预先编译以在特定硬件架构（如 64 位 Intel (x86-64)）上运行的二进制文件，也可以是源代码，源代码必须在使用前在本地架构上编译。获取并编译源代码的最大优点是源代码不是为特定的硬件架构创建的。编译完成后，程序在其编译的架构上原生执行。

![](img/c27875544958897d817484d558c208c8_522_1.png)

获取 Linux 软件最常见的方法是通过互联网。附录 C 列出了一些托管 Linux 开源软件下载的常见网站。

![](img/c27875544958897d817484d558c208c8_522_2.png)

从互联网下载软件文件时，你可能会注意到互联网站点列出了文件的校验和值，该值是根据确切的文件内容计算的。为了确保在下载后完整接收到文件，你应该验证校验和值是否仍然相同。你可以使用几种 `*sum` 命令之一，具体取决于用于创建校验和的算法。例如，你可以使用 `md5sum programfile` 命令检查 MD5 校验和，使用 `sha1sum programfile` 命令检查 SHA-1 校验和，使用 `sha256sum programfile` 命令检查 SHA-256 校验和，或者使用 `sha512sum programfile` 命令检查 SHA-512 校验和。

程序源代码通常以 [tarball] 格式分发，你可以对其进行解压缩。解压缩后，你可以提取源代码并将其编译。预先编译的二进制程序也可以以 tarball 格式分发，但它们通常以用于包管理器的格式分发。

回顾第 1 章，包管理器提供了分发程序的标准格式，以及一个中央数据库来存储关于系统上已安装软件包的信息；这使得软件包可以被查询并轻松卸载。如今大多数 Linux 发行版，包括 Fedora，使用 Red Hat 包管理器 (RPM)。然而，Debian 和基于 Debian 的 Linux 发行版，如 Ubuntu Linux，使用 Debian 包管理器 (DPKG)。

![](img/c27875544958897d817484d558c208c8_523_0.png)

> 几乎所有主流 Linux 发行版都使用 RPM 或 DPKG。然而，它们并非 Linux 系统上可用的唯一包管理器。例如，Arch Linux 使用 Pacman 包管理器。

### 将源代码编译为程序

如今，大多数开源软件开发者在将源代码编译为二进制程序的程序上是标准化的。由于大多数源代码以 tarball 格式出现，你必须解压缩并提取文件。这会在当前目录下创建一个包含源代码的子目录。此外，该目录通常包含一个 README 文件，其中有关于程序的信息，以及一个包含安装说明的 INSTALL 文件。

在源代码目录内，安装的第一步是运行 `configure` 程序。这会执行系统要求的初步检查，并在当前目录中创建一个名为 `Makefile` 的文件，列出要编译的内容。

接下来，你可以键入 `make` 命令，该命令查找 `Makefile` 文件，并使用其中的信息通过适用于本地硬件架构的适当编译器程序将源代码编译为二进制程序。例如，用 C 编程语言编写的软件使用 GNU C 编译器（`gcc`）进行编译。编译后，程序包含的二进制文件保留在源代码目录中。要将文件复制到文件系统上的适当位置，例如 `PATH` 变量中列出的目录，你必须键入 `make install`。

![](img/c27875544958897d817484d558c208c8_523_1.png)

> 大多数 Linux 程序在编译后安装在 `/usr/local` 目录的子目录中。

程序编译并复制到文件系统上的正确位置后，你可以从系统中删除源代码目录及其内容。

