
| Filesystem | lk-blocks | Used | Available | Use% | Mounted on |
|---|---|---|---|---|---|
| /dev/hda5 | 381139 | 75222 | 286239 | 21% | |
| /dev/hda1 | 46636 | 8646 | 35582 | 20% | /boot |
| /dev/hda3 | 1423096 | 48216 | 1302588 | 4% | /home |
| none | 47160 | 0 | 47160 | 0% | /dev/shm |
| /dev/hda2 | 3889924 | 1661608 | 2030720 | 46% | /usr |
| /dev/hda6 | 256667 | 44297 | 199118 | 19% | /var |
| /dev/hdb1 | 3858204 | 32828 | 3629388 | 1% | /backup |

如你所示，`/dev/hdb1` 已挂载在 `/backup` 上。现在它已经挂载，你可以按需要使用它。就像你之前对 `/dev/sdb1` 操作一样，如果你希望在启动时挂载文件系统，可以在 `/etc/fstab` 中添加条目。这将在本章节 fstab 部分进行讨论。

正如你看到的，`fdisk` 允许我们创建许多不同的文件系统。同样，Linux 中使用的许多其他命令也支持许多不同的文件系统。例如，当你执行 `mount` 命令时，可以使用 `-t` 选项来指定要挂载的文件系统类型。`mount` 命令的帮助页列出了许多可以使用 `-t` 选项的文件系统类型。要查看如何使用 `mount` 挂载 DOS 软磁盘或 CD-ROM 驱动器，请参第 87 页。

## 使用 fsck 和 e2fsck、inodes 和 superblock 进行文件系统维护

本节介绍文件系统的维护。大多数示例将引用你在本章之前操作过的 SCSI 完整性服务器。尽管如此，这些工具和实用程序在带有 IDE 器的 IA-32 系统上的工作原理相同。再次提醒，使用几乎所有这些工具时，必须以 root 身份登录。

### fsck 和 e2fsck

`fsck`（file system check）是一个用于 Linux 和 UNIX 系统文件系统维护的程序。`fsck` 检查文件系统的一致性，并可以对损坏的文件系统进行许多“救命性”修复。`fsck` 可以带有多个选项运行。用于 ext2 文件系统检查的程序是 `e2fsck`。如果你尝试在 *ext2* 或 *ext3* 文件系统上运行 `fsck`，你会发现 `fsck` 会自动调用 `e2fsck`。以下是 `e2fsck` 一些常用的选项：

- `-b superblock`

通常，`e2fsck` 使用块来查找分区相关信息。然而，如果块 1 的 ID 损坏，你可以指定一个通常存在 8192 个块之后的块号。你可以指定 8193、16385 等作为备用。你也可以通过在创建文件系统时记录它们（如早前的列表所示），或使用 `mke2fs` 程序配合 `-n` 选项来打印出创建 superblock 的位置，从而找到备用的 superblock。`mke2fs` 的 `-b` 选项（用于指定文件系统的块大小）必须被指定，这样打印出的 superblock 位置才会准确。欲需更多信息，请参阅 `e2fsck` 和 `mke2fs` 的帮助页。

- `-c`

运行 `badblocks` 程序以找到文件系统上的坏块，并将它们添加到坏块 inode 中。

- `-f`

即使文件系统被认为是干净的，也强制进行文件系统检查。

- `-y`

对所有问题都回答 *yes*（是），以便 `e2fsck` 可以以非交互模式运行。

- `-v`

在 *verbose*（详细）模式下运行。

若要使用 `-y` 和 `-v` 选项在分区 `/dev/sdb1` 上运行 `e2fsck`，应执行以下操作：

```bash
[root@localhost]# umount /backup

[root@localhost]# e2fsck
Usage: e2fsck [-prycdfFSV] [-b blocksize]
      [-I inode_buffer_blocks] [-P process inode_size]
      [-l bad_blocks_file] [-C fd] [-ext-journal] device
```

# 使用 fsck 和 e2fsck、节点（inodes）以及超级块进行文件系统维护

| 字段 | 说明 |
| :--- | :--- |
| fstype | 可以是多种类型之一，包括 ext2 本地文件系统版本2、ext3 本地文件系统版本3、msdos 本地 MS-DOS 分区、nfs 远程挂载的 NFS、用于交换的交换分区或 iso9660 本地 CD-ROM 文件系统 |
| options | 与文件系统类型相关的选项。这些是 -o 参数。 |
| dump frequency | `dump` 命令使用，用于确定哪些文件系统需要备份。 |
| pass # | 指定 e2fsck 在重新启动时检查文件系统的顺序。 |
| Comments | 任何你想写的内容，只要前面有 #（井号或交叉号）即可。 |

如你所见，在 `/etc/fstab` 示例中，cdrom 有几个选项，包括用于只读的 `ro`。`sa`（虚拟内存）位于 `/dev/sda2`。`/proc` 关联了一个 `none`，因为它是内核参数的接口，而不是其他文件系统。`/dev/pts` 也关联了一个 `none`，因为它是 telnet 和 login 等程序远程访问你系统的方式。

你可以轻松地向 `/etc/fstab` 添加条目，这样系统在启动时就会挂载它们。由于你想使用标签（label）挂载 `/dev/sdb1`，请先使用 `elabel` 命令创建一个标签。之后，再次运行 `elabel` 命令以显示结果：

```bash
root@localhost root]# /sbin/elabel /dev/sdb1

root@localhost root]# /sbin/elabel /dev/sdb1

root@localhost root]#
```

如你所见，我们已经完成了所需的标记。现在，为了在启动时自动挂载新分区，请向 `/etc/fstab` 文件中添加以下行并保存文件。如果你想检查分区是否在启动时被挂载到正确的位置，请重启并重新登录，或者执行以下命令：

```bash
root@localhost root]# mount -a

root@localhost root]# df
```

| 文件系统 | 块 | 已用 | 挂载点 |
| :--- | :--- | :--- | :--- |
| dev/sda3 | 64850 | 24193 | 63256 | /boot |
| dev/sda1 | 104184 | 6120 | 98064 | /efi |
| none | 102456 | 0 | 102456 | /shm |
| dev/sdb1 | 3500150 | 32828 | 3191068 | /backup |
| dev/sdb1 | 1 | full | |

`mount -a` 读取 `/etc/fstab` 并挂载文件中列出的所有文件系统。`df` 请求系统报告系统上所有空闲磁盘。它报告 `dev/sdb1` 挂载在 `/backup`。

`mount` 命令在本章中已经用到，但还没有详细介绍，因为你使用 `mount` 执行的大部分工作都是基础性的。尽管如此，该命令有很多选项，你可以在手册（man page）中查看。然而，`mount` 命令的基本形式如下：

```bash
mount [options] device
```

你已经在示例中使用了一些 `mount` 选项。以下列出了一些更常用的选项：

- `-a` 挂载 `/etc/fstab` 中的文件系统。这在前面的示例中已使用。
- `-t fstype` 指定要挂载的文件系统类型，但 `mount` 通常会自动检测类型，所以你通常不需要此选项。
- `-o options` 使用 `-o` 时，你可以指定许多选项，例如 `ro` 只读、`rw` 读写、`noauto` 禁止自动挂载。

# 使用 fsck 和 e2fsck、节点（inodes）以及超级块进行文件系统维护

现在你已经知道如何挂载文件系统，应该知道如何卸载它。Linux 使用 `umount`（注意是 umount，而不是 unmount）命令来卸载文件系统：

```bash
umount [-f] device
```

只要文件系统未被在使用中，它将立即被卸载。“在使用中”意味着你正处于该目录中，或者有一个进程打开了位于挂载文件系统上的文件。因此，如果你处于要卸载的文件系统的目录中，你可能需要切换目录，或者可能需要使用 `kill` 停止连接到文件系统的进程。同样，如果你在要卸载的文件系统中打开了一个文件，你必须关闭它。你可能需要使用 `umount -f` 强制卸载文件系统，或者进入 Linux 所称为“单用户模式”。

## Linux 日志文件

你的 Linux 系统上发生最重要的活动都记录在日志文件中。你的 Linux 系统有很多日志文件。其中最重要的是 `syslog`，它是系统事件日志器，许多程序使用它执行记录。

`syslog` 支持消息排序，允许根据重要性对消息进行排序，然后发送到相应的目的地。`syslog` 由 `syslogd`（日志守护进程）、`loglog`（一组向 syslog 提交消息的库例）和 `logger`（一个从系统提交日志条目的的用户级命令）组成。`syslog` 在启动时启动。如果你想查看它是否在系统中运行，请使用 `ps` 命令显示系统上运行的所有进程。

要指定放置特定日志记录的文件，请使用 `/etc/syslog.conf`。该文件的通用格式具有一个选择字段（selector）和一个操作字段（action）。这两个字段都有多个子级别（levels）。例如，选择字段可以从信息级（info）到紧急级（emerg），操作字段可以从所有用户（*）到写入文件（filename），发送到屏幕。`/etc/syslog.conf`

`/etc/syslog.conf` 文件如下：

```bash
## 将所有内核消息记录到控制台
kern.* /dev/console

# 除了 mail 以外，记录所有信息级（info）或更高级别的消息
*.info /var/log/messages

# authpriv 文件有限制访问
authpriv.* /var/log/secure

# 将邮件消息记录到一个地方
mail.* /var/log

# 记录 cron 信息
cron.* /var/log

# 保存 crit 级及以上的错误
*.crit /var/log

# 记录 boot
local.* /var/boot
```

你可以从该文件中看到内核相关的消息发送到控制台，邮件消息发送到 `/var/log/maill`，cron 消息发送到 `/var/log/cron` 等。在之前的列表中，你可以看到所有的日志都在 `/var/log` 中，这是最常见的位置。以下是 `/var/log` 目录的长列表：

```bash
ls -l /var/log
total 3664
-rw-r---- root 1425 Jan 28 20:08 ac.log
-rw-r---- root 9222 Jan 28 20:09 boot.log
-rw-r---- root 12509 Jan 24 22:15 boot.log.2
-rw-r---- root 75039 Jan 29 19:00 cron.log
-rw-r---- root 305847 Jan 26 04:02 cron.1
-rw-r--x root 207522 Jan 27 17:03 cron.2
-rw-r--x root 10234 Jan 26 20:08 dmesg
drwxr-xr-x root 4096 Jun 24 20:01
-rw-r---- root 14516 Nov 15 16:51 mail
-rw-r---- root 4096 Jun 24 20:02 httpd
-rw-r---- root 442 Jan 28 20:08 lastlog.log
drwxr-xr-x root 4096 Jul 28 22:08 jumpbuster
-rw-r---- root 79506 Jan 28 18:41 ksys.1
-rw-r---- root 79506 Jan 28 19:20 ksysms.2
-rw-r---- root 79506 Jan 28 19:06 ksysms.3
-rw-r---- root 79306 Jan 24 22:15 ksysms.4
-rw-r---- root 79506 Jan 24 20:07 ksym.5
-rw-r---- root 79506 Jan 24 18:38 ksym.6
-rw-r---- root 193900 Jan 29 01:05 lastlog
-rw-r---- root 7665 Jan 24 16:02 mailog.1
-rw-r---- root 13716 Jan 24 14:18 mailog.2
drwxrws-x root mailman 4096 Jan 24 06:02 mailman
-rw-r---- root 263242 Jan 29 04:53 messages
-rw-r---- root 173869 Jan 24 16:58 messages.2
-rw-r---- mysql mysql 0 Jan 24 06:02 mysqldlog.1
-rw-r---- mysql mysql 0 Jan 24 16:32 mysqldlog.2
drwxr-xr-x root 4096 Jan 20 12:54 news
drwxr-xr-x root 177984 Jan 29 17:00 new
-rw-r---- root 95922 Jan 29 04:02 pactt.1.gz
-rw-r---- root 20127 Jan 29 04:02 pactt.2.gz
-rw-r---- root 50909 Jan 27 04:02 pactt.3.gz
-rw-r---- root 23069 Jan 26 04:02 pactt.4.gz
-rw-r---- root 133068 Jan 29 04:02 pactt.5.gz
-rw-r---- root 50800 Jan 24 17:03 pactt.6.gz
-rw-r---- root 89431 Jan 24 17:04 pactt.7.gz
drwxr-xr-x postgres postgres 4096 Jan 24 10:04 pgsql
```

## 第 4 章 磁盘与文件系统主题

```
reboot system boot  2.48-e.12smp   Tue 28 19:41      (00:24)
root     pts/0            :0               Tue 28 19:21 - down  (00:18)
root     :0               :0               Tue 28 19:21 - down  (00:18)
reboot system boot  2.48-e.12smp   Tue 28 19:20      (00:19)
root     pts/0            :0               Tue 28 19:08      (00:10)
root     :0               :0               Tue 28 19:08      (00:10)
reboot system boot  2.48-e.12smp   Tue 28 19:06      (00:11)
root     pts/0            :0               Tue 28 16:44 - 19:04 (02:44)
root     :0               :0               Tue 28 16:44 - 19:04 (02:46)
reboot system boot  2.48-e.12smp   Tue 28 16:18 - down (3:20:49)
mp begins Thu Jan 16 16:40:33 2003
Fri Jan 24 22:15
```

此示例显示了 `wtmp` 中包含 22 个条目。

大多数文件会自动“轮转”（rotated），这意味着最新的文件扩展名为 `.1`，而最旧的文件具有更大的数字扩展名。

注意 `/var/log` 列表，某些如 samba 等应用程序的子目录。在 IA-32 系统上，`/var/samba` 目录许多许多日志将在 Samba 章节中用到，如下列表所示：

### 11 /var/log/samba

```
total 53
-rw-r--r--  1 root  root 0 Jun 15 11:15 4412b.log
-rw-r--r--  1 root  root  0 Aug 17 04:03 4457mxp.log.1
-rw-r--r--  1 root  root 118 Aug 17 04:03 4457mxp.log.2
-rw-r--r--  1 root  root 235 Jul 22 04:03 4457mxp.log.3
-rw-r--r--  1 root  root 664 Jun 23 04:03 4457mxp.log.4
-rw-r--r--  1 root  root 0 Jun 21 12:22 linuxdev
-rw-r--r--  1 root  root 25796 Oct 14 02:02 nmbd
```
