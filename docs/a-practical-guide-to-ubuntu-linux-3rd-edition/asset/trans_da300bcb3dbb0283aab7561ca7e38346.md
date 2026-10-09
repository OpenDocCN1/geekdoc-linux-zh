

| 设备 | 挂载点 | 类型 | 选项 | 转储 | 通过 |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/fd0 | /media/floppy0 | auto | rw, user, nosuid, noauto | 0 | 0 |

指定文件系统类型为 **auto** 会导致系统探测文件系统以确定其类型，并允许用户挂载各种软盘。如有必要，创建 **/media/floppy0** 目录。插入一张软盘并尝试挂载它。软盘必须经过格式化（使用 **fdformat**，这将删除软盘上的所有数据）。在以下示例中，第一条命令后的错误消息通常表明软盘上没有文件系统。在某些情况下，**mount** 命令可能会挂起。如果发生这种情况，弹出软盘以显示提示符。使用 **mkfs**（第 458 页）创建文件系统——但务必小心，因为 mkfs 会销毁软盘上的所有数据。

```
$ mount /dev/fd0
mount: I could not determine the filesystem type, and none was specified

$ mkfs /dev/fd0
mke2fs 1.41.11 (14-Mar-2010)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
184 inodes, 1490 blocks
72 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=1572864
1 block group
8192 blocks per group, 8192 fragments per group
184 inodes per group

Writing inode tables: done
Writing superblocks and filesystem accounting information: done

This filesystem will be automatically checked every 36 mounts or
180 days, whichever comes first.  Use tune2fs -c or -i to override.
```

现在再次尝试 mount 命令：

```
$ mount /dev/fd0
$ mount
/dev/fd0 on /media/floppy0 type ext2 (rw,noexec,nosuid,nodev,user= sam)

$ df -h /dev/fd0
Filesystem     Size  Used Avail Use% Mounted on
/dev/fd0       1.4M  19K 1.3M  2% /media/Floppy0
```

不带任何参数的 mount 命令以及 **df -h /dev/fd0** 显示该软盘已挂载并准备就绪，可供使用。

## umount：卸载文件系统

只要文件系统不包含任何正在使用（打开）的文件或目录，umount 工具就会卸载该文件系统。例如，登录用户的工作目录不能位于你试图卸载的文件系统上。下一条命令卸载之前挂载的 CD：
`$ umount /media/cdrom0`

卸载软盘或远程（NFS）目录层次结构的方式与卸载硬盘分区的方式相同。

umount 工具会查阅 /etc/fstab 以获取必要信息，然后从服务器卸载相应的文件系统。当某个进程在你试图卸载的文件系统上打开了一个文件时，umount 会显示类似以下的消息：
`unmount: /home: device is busy`

### 当因正在使用而无法卸载设备时

**提示** 当某个进程在需要卸载的设备上打开了文件时，使用 fuser 确定哪个进程打开了该文件并将其终止。例如，当你想要卸载软盘时，输入命令 `fuser -ki /media/floppy0`（将本地系统上软盘的挂载点替换 /media/floppy0）。在与你确认后，该命令将终止使用该软盘的进程。

使用 umount 的 -a 选项来卸载所有未在使用中的已挂载文件系统。你永远不会卸载挂载在 / 上的文件系统。你可以将 -a 与 -t 选项结合使用，以卸载给定类型（ext4, nfs 或其他）的文件系统。例如，以下命令卸载所有未在使用中的已挂载 nfs 目录层次结构：
`$ sudo umount -at nfs`

## fstab：记录文件系统

系统管理员维护 /etc/fstab 文件，该文件列出了本地和远程目录层次结构，其中大部分在系统启动时自动挂载。fstab 文件有六列，其中连字符表示没有值的列占位符：

- 1. **名称**——本地块设备（第 504 页）的名称、标签或 UUID 编号，或指向远程目录层次结构的指针。安装系统时，Ubuntu 对固定设备使用 UUID 编号。它在 fstab 中指定 UUID 的每一行前都加上一条注释，注明设备名称。在安装过程中在 fstab 中使用 UUID 编号可以避免对一致设备命名的需求。由于 udev（第 502 页）动态管理设备命名，安装程序可能不知道例如第一个磁盘没有命名为 /dev/hda1 而是 /dev/sda1，但它始终知道设备的 UUID 编号。使用 UUID 编号识别设备还能确保在移除或交换设备时，分区和挂载点正确关联。有关 UUID 编号的更多信息，请参见 /dev/disk/by-uuid（第 489 页）。你可以通过使用形式 `LABEL=xx` 来使用本地文件系统的卷标，其中 xx 是卷标。参考第 458 页的 `etlabel`。

远程目录层次结构显示为 `hostname:pathname`，其中 hostname 是容纳该文件系统的远程系统的名称，pathname 是要挂载的目录在远程系统上的绝对路径名。

- 2. **挂载点**——文件系统/目录层次结构要挂载到的目录文件的名称。如果该目录尚不存在，请使用 `mkdir` 创建该目录。参见第 35 页和第 507 页。

- 3. **类型**——要挂载的文件系统/目录层次结构的类型。本地文件系统通常为 `ext2`、`ext4` 或 `iso9660` 类型，远程目录层次结构为 `nfs` 或 `cifs` 类型。第 505 页的表 12-1 列出了文件系统类型。

- 4. **挂载选项**——以逗号分隔的挂载选项列表，例如文件系统是否用于读写（`rw`，默认值）或只读（`ro`）。参见第 508 页和第 778 页，并参考 mount 和 nfs 手册页中的选项列表。

- 5. **转储**——由 `dump`（第 603 页）使用，以确定何时备份文件系统。

- 6. **Fsk**——指定 `fsck` 检查文件系统的顺序。根（//）在此列中应为 1。挂载到根目录下一级目录的文件系统应为 2。挂载到另一个已挂载文件系统（非根文件系统）上的文件系统应为 3。例如，如果 `local` 是与 `usr` 不同的独立文件系统，并挂载在 `usr` 上（作为 `/usr/local`），则 `local` 应为 3。不需要检查的文件系统和目录层次结构（例如，远程挂载的目录层次结构和 CD/DVD）应为 0。

以下示例展示了一个典型的 fstab 文件：

```
$ cat /etc/fstab
# /etc/fstab: static file system information.
#
# <file system> <mount point> <type> <options> <dump> <pass>
proc /proc proc defaults 0 0
# / was on /dev/sda1 during installation
UUID=8f3c51c2-a42c-49b1-9f03-db2140cb7eb5 / ext4 defaults,errors=remount-ro 0 1
# /home was on /dev/sda2 during installation
UUID=39fc600f-91d5-4c9f-8559-727050d76f45 /home ext4 defaults 0 2
# swap was on /dev/sda3 during installation
UUID=a68fb957-2ae7-4ae5-8656-23alc6f8cd14 none swap sw 0 0
/dev/sda5 /pl5 ext4 defaults 0 2
/dev/sda6 /pl6 ext4 defaults 0 2
/dev/sdb /media/cdrom0 udo,iso9660 user,nosuid,noauto 0 0
/dev/fd0 /media/floppy0 auto rw,user,nosuid,noauto 0 0
dos:/p04 /p04 nfs defaults 0 0
```

在上面的示例中，/pl5 和 /pl6 没有使用 UUID 编号，因为这些设备是在系统安装后由管理员添加到 fstab 中的。

## fsck：检查文件系统完整性

fsck（文件系统检查）工具验证文件系统的完整性，并在可能的情况下修复发现的问题。由于许多文件系统修复可能会破坏数据，特别是在非日志记录文件系统（第 1155 页）上，例如 ext2，fsck 默认在做出任何一页修复之前都会要求你确认。

### 不要在已挂载的文件系统上运行 fsck

- 不要在已挂载的文件系统上运行 fsck。当你试图检查已挂载的文件系统时，fsck 会警告你并询问是否继续。请回答 no。你可以在已挂载的文件系统上使用 -N 选项运行 fsck，因为它不会写入文件系统；因此，运行它不会造成任何伤害。有关更多信息，请参见第 504 页。

当 fsck 修复损坏的文件系统时，它可能会发现未链接的文件：即丢失了目录信息的文件。这些文件没有文件名。fsck 工具将这些文件的 inode 编号作为名称赋予它们，并将它们存储在包含该文件的文件系统中的 lost+found 目录（第 488 页）中。你可以使用 file（第 170 页）来确定这些文件的类型，并使用 less 查看可读文件。由于 ls -l 会显示这些文件的拥有者名称，因此你可以将它们归还给它们的拥有者。

以下命令检查在 /etc/fstab（第 510 页）中标记为需要检查的所有未挂载文件系统，除了根文件系统：

```
$ sudo fsck -RA
```

-RA 选项使 fsck 检查 fstab 中列出的文件系统。与 -RA 选项一起使用时，-R 选项使 fsck 不检查根文件系统。你可以使用类似以下命令之一来检查特定的文件系统：

```
$ sudo fsck /home
```

或者

```
$ sudo fsck /dev/sda2
```

## tune2fs：更改文件系统参数

tune2fs 工具显示和修改 ext2、ext3 和 ext4 文件系统上的文件系统参数。此工具还可以为 ext2 文件系统设置日志记录，从而将其转换为 ext3 文件系统。随着越来越可靠的硬件和软件的出现，系统往往重启频率降低，因此定期检查文件系统变得很重要。默认情况下，在系统启动过程中，在分区被挂载之前，会在每个分区上运行 fsck。（由 tune2fs 调度的检查与系统崩溃或硬盘错误后执行的检查是独立的，调度方式也不同[参见上一节]。）

取决于标志，fsck 可能只是显示一条消息，说明文件系统是干净的，而不做任何其他操作。分区越大，假设是非日志记录文件系统，检查它所花费的时间就越长。这些检查往往是不必要的。tune2fs 工具帮助你找到在每次
