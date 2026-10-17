
```
lrwxxrwx 1 root root 17 3:11 S10Network -> .. /init.d/network
lrwxxrwx 1 root root 16 3:11 S30Syslog -> .. /init.d/syslog
lrwxxrwx 1 root root 16 3:11 S40scron -> .. /init.d/cron
lrwxxrwx 1 root root 14 3:32 S50Inet -> .. /init.d/init
lrwxxrwx 1 root root 13 3:11 S60nfs -> .. /init.d/nfs
lrwxxrwx 1 root root 15 3:11 S70nfs -> .. /init.d/nfs
lrwxxrwx 1 root root 18 3:11 S90lpd -> .. /init.d/lpd
```

## 第 2.13 节：启动过程、Init 和关机

`init`程序由内核在启动时运行。它负责启动所有启动时需要运行的标准进程。这些包括允许你登录的`getty`进程、`NFS`守护进程、`FTP`守护进程以及你希望机器启动时运行的任何程序。

SysV 正在迅速成为 Linux 世界中控制软件启动启动的标准，因为它比传统的 BSD `init`更易于使用、更强大且更灵活。

SysV `init`与 BSD `init`的区别在于，配置文件位于`/etc`的子目录中，而不是直接位于`/etc`中。在`/etc/rc.d`中，你会找到`rc.sysinit`和以下目录：

```
init.d
rc0.d
rc1.d
rc2.d
rc3.d
rc4.d
rc5.d
rc6.d
```

`init.d`目录包含各种脚本。基本上，对于在启动时或进入另一个运行级别时可能需要启动的服务，你都必须有一个脚本。服务包括网络、`nfs`、`sendmail`、`httpd`等。服务不包括那些必须运行一次后退出的内容。那些应该放在`rc.local`或`rc.serial`中的内容。

如果你想要`rc.local`，它应该位于`/etc/rc.d`中。大多数系统都包含了它，尽管它没做什么太大作用。如果你需要在启动时执行特定于串口的任务，也可以在`/etc/rc.d`中包含一个`rc.serial`文件。

事件链如下：

- 内核在几个地方查找`init`并运行它找到的第一个
- `init`运行`/etc/rc.d/rc.sysinit`
- `rc.sysinit`处理大部分引导加载程序的进程，然后运行`rc.serial`（如果存在）

## 第 2 章：系统管理

- `init`运行默认运行级别的所有脚本。
- `init`运行`rc.local`

默认运行级别在`/etc/initabb`中决定。你应该会有一个靠近顶部的行如下：

```
id:3:initdefault:
```

从这里，你可以查看第二列并看到默认运行级别是`3`。如果你想更改它，可以手动编辑`/etc/initabb`。编辑`initabb`文件时要务必小心。如果你搞乱了，可以通过重启并输入以下命令来修复：

```
LILO boot: linux single
```

这将允许你进入单用户模式，以便你将`initabb`重新编辑为原先的值。

现在，如何运行所有正确的脚本呢？如果你在`rc3.d`上输入`ls -1`，可能会看到类似的内容：

```
lrwxxrwx 1 root root 17 3:11 S10Network -> .. /init.d/network
lrwxxrwx 1 root root 16 3:11 S30Syslog -> .. /init.d/syslog
lrwxxrwx 1 root root 16 3:11 S40scron -> .. /init.d/cron
lrwxxrwx 1 root root 14 3:32 S50Inet -> .. /init.d/init
lrwxxrwx 1 root root 13 3:11 S60nfs -> .. /init.d/nfs
lrwxxrwx 1 root root 15 3:11 S70nfs -> .. /init.d/nfs
lrwxxrwx 1 root root 18 3:11 S90lpd -> .. /init.d/lpd
```

### 2.14 救援模式

当出现问题时，有几种方法可以修复它们。然而，这要求你对系统有良好的了解。我们将介绍你可以进入救援模式的方法，在救援模式下，你可以利用自己的知识来救救系统。

#### 2.14.1 什么是救援模式？

救援模式（Rescue mode）是一个术语，描述一种完全从磁盘、CD 或其他方法启动微型 Linux 环境的方法。

本节后续内容可能帮助你在某个时刻从问题中恢复。

顾如其义，救援模式是为了在遇到某种困境时营救你。在正常运行期间，你的 Red Hat Linux 系统使用系统硬盘上的文件来执行所有操作——运行程序、存储文件等。

然而，有时你可能无法让 Linux 完全运行，从而无法访问你系统硬盘上的文件。通过使用救援模式，即使你无法从该硬盘运行 Linux，也有可能访问存储在系统硬盘上的文件。

通常情况下，你由于两个原因之一需要进入救援模式：

- 你无法启动 Linux，并想要修复它。
- 你遇到了硬件或软件问题，并想要从系统硬盘中导出一些重要文件。

让我们仔细看看这两种场景。

#### 无法启动 Linux

很多情况下，这是由于在安装 Red Hat Linux 之后安装了另一个操作系统引起的。某些其他操作系统假设你的计算机上没有其他操作系统，并覆盖了最初包含 LILO 引导加载器的主引导记录（或 MBR）。如果 LILO 以这种方式被覆盖，那么你的运气就不太好了——除非你能进入救援模式。

#### 硬件/软件问题

此类类别下的不同情况与运行 Linux 的系统数量一样多。诸如硬盘损坏，以及在编译新内核后忘记运行 LILO 等问题，只是可能阻止你启动 Red Hat Linux 的两个实例。如果你能进入救援模式，你可能会解决问题——或者至少获得你最重要文件的副本。

若要在救援模式下启动系统，请在安装启动提示符处输入以下参数：

```
boot: linux rescue
```

你可以通过以下方式之一进入安装启动提示符：

- 通过从 Red Hat Linux 盒装版附带的软磁盘或 CD-ROM 启动系统。
- 通过网络或 PCMCIA 磁盘磁盘启动。这些方法假设你的网络连接正常，并要求你识别网络主机和传输类型。有关如何指定这些信息的说明，请参见第 10 章“通过文本模式安装 Red Hat Linux”中的“通过网络安装”。

一旦你的系统进入救援模式，会出现一个提示符：

```
bash#
```

从此提示符，你可以运行下面列出的命令：

| anaconda gzip mkfs.ext2 ps |
| badblocks head mknod python |
| bash hwclock mkraid python1.5 |
| cat config mkswap raidstart |
| chatter init mlabel raidstop |
| chmod insmod mmd rcp |
| chroot less mmount rlogin |
| clock ln move rm |
| collage loader modprobe rmod |
| cp ls mount route |
| cpio lsattr mpartition rpm |
| dd lsmod mrd rsh |
| ddcprobe mattrib mread sed |
| depmode mbadblocks mren sh |
| df mcd mshowfat sync |
| e2fsck mcopy mt tac |
| fdisk mdel mtools tail |
| fsck mdtree mtype tar |
| fsck.ext2 mdir mv touch |
| ftp mdu mzip traceroute |
| genhdlist m open umount |
| gnome-pty-helper minfo pico uncpio |
| grep mkdir ping uniq |
| gunzip mke2fs probe zcat |

然而，如果你的根文件系统未损坏，你可以挂载它，然后运行标准的 Linux 工具程序。例如，假设你的根文件系统位于`/dev/hda5`。以下是挂载此分区的方法：

```
mount -t ext2 /dev/hda5 /foo
```
