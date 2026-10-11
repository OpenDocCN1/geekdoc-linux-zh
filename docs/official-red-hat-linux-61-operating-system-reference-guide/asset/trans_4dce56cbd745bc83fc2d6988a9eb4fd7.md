
## 2.13.5 初始脚本实用工具

`chkconfig` 实用程序提供了一个简单的命令行工具，用于维护 `/etc/rc.d` 目录层次结构。它免除了系统管理员直接操作 `/etc/rc.d` 中众多符号链接的需求。

此外，还有 `ntsysv` 实用程序，它提供基于屏幕的界面，相比之下 `chkconfig` 提供的是命令行界面。

有关更多详细信息，请参见 `chkconfig` 和 `ntsysv` 的手册页（man pages）。

## 2.13.6 在启动时运行程序

文件 `/etc/rc.d/rc.local` 会在启动时、所有其他初始化完成之后以及每次更改运行级别（runlevels）时执行。你可以在这里添加额外的初始化命令。例如，你可能想要启动额外的守护进程（daemons），或者初始化打印机。此外，如果你需要设置串行端口，可以编辑 `/etc/rc.d/rc.serial`，它会在启动时自动执行。

默认的 `/etc/rc.d/rc.local` 仅仅创建一个带有你的内核版本和机器类型的漂亮登录横幅。

## 2.13.7 关闭系统

要关闭 Red Hat Linux，请输入 `shutdown` 命令。你可以阅读 `shutdown` 的手册页以获取完整细节，但最常见的两种用法是：

```
shutdown -h now
shutdown -r now
```

每个命令都会干净地关闭系统。在关闭所有内容后，`-h` 选项将停止机器（halt），而 `-r` 选项将重新启动（reboot）。

尽管现在的 `reboot` 和 `halt` 命令足够“智能”，在系统处于运行级别 1-5 时运行时会自动调用 `shutdown`，但这是一种坏习惯，因为并非所有类 Linux 操作系统都具有此功能。

## 2.14 救援模式

当出现问题时，有多种方法可以进行修复。然而，这些方法要求你对系统有充分的了解。我们将介绍你可以启动救援模式的方法，从而运用你自己的知识来拯救系统。

### 2.14.1 什么是救援模式？

救援模式是一个术语，用于描述一种完全从软盘、CD 或其他介质启动小型 Linux 环境的方法。

本节中的后续内容可能在某个时刻帮助你从问题中恢复。

顾名思义，救援模式是用来将你从某种困境中解救出来的。在正常操作下，你的 Red Hat Linux 系统使用位于系统硬盘上的文件来执行一切任务——运行程序、存储文件等等。

然而，有时你可能无法让 Linux 完全运行到足以访问系统硬盘上的文件的状态。通过使用救援模式，即使无法直接从该硬盘运行 Linux，你仍然可以访问存储在系统硬盘上的文件。

通常，你需要进入救援模式基于以下两个原因之一：

- 你无法引导 Linux，并且希望修复它。
- 你遇到硬件或软件问题，想要从系统硬盘上获取几个重要文件。

让我们更仔细地查看这些场景。

### 无法引导 Linux

很多时候，这是由在安装 Red Hat Linux 之后安装了其他操作系统引起的。某些其他操作系统假设你的计算机上没有其他操作系统，并会覆盖原本包含 LILO 引导加载程序的引导主记录（Master Boot Record，或 MBR）。如果 LILO 以这种方式被覆盖，你就走运了——除非你能进入救援模式。

### 硬件/软件问题

在此类别下，可能有与运行 Linux 的系统一样多的不同情况。例如，硬盘故障以及在构建新内核后忘记运行 LILO 只是两个可能导致你无法引导 Red Hat Linux 的实例。如果你能进入救援模式，你可能能够解决问题——或者至少获取你最重要文件的副本。

要在救援模式下引导你的系统，请在安装引导提示符下输入以下参数：

```
boot: linux rescue
```

你可以通过以下方式之一到达安装引导提示符：

- 通过从随你的 Red Hat Linux 盒装套装提供的软盘或 CD-ROM 引导你的系统。
- 通过网络或 PCMCIA 引导软盘进行引导。这些方法假设你的网络连接正常工作，并要求你识别网络主机和传输类型。有关如何指定这些信息的说明，请参见第 10 章 *通过文本模式安装 Red Hat Linux* 中的“通过网络安装”部分。

一旦你的系统进入救援模式，会出现一个提示符：

```
bash#
```

从这个提示符，你可以运行下面列出的命令：

| 命令 | 命令 | 命令 | 命令 |
| :--- | :--- | :--- | :--- |
| anaconda | gzip | mkfs.ext2 | ps |
| badblocks | head | mknod | python |
| bash | hwclock | mkraid | python1.5 |
| cat | ifconfig | mkswap | raidstart |
| chatter | init | mlabel | raidstop |
| chmod | insmod | mnd | rcp |
| chroot | less | mmount | rlogin |
| clock | ln | mmove | rm |
| collage | loader | mdprobe | rmdown |
| cp | ls | mount | route |
| cpio | lsattr | mpartition | rpm |
| dd | ddprobe | depmod | df |
| e2fsck | fdisk | fsck | fsck.ext2 |
| ftp | genhdlist | gnome-pty-helper | grep |
| gunzip | lsmod | mattrib | mbadblocks |
| mcd | mcopy | mdel | mdeltree |
| mdir | mdu | mformat | minfo |
| mkdir | mke2fs | mrd | mread |
| mren | mshowfat | mt | mtools |
| mtype | mv | mzip | open |
| pico | ping | probe | re |
| sed | sh | sync | tac |
| tail | tar | touch | traceroute |
| umount | uncpio | uniq | zcat |

然而，如果你的根文件系统未受损，你可以挂载它，然后运行任何标准 Linux 实用程序。例如，假设你的根文件系统在 /dev/hda5。以下是如何挂载此分区：

```
mount -t ext2 /dev/hda5 /foo
```

其中 /foo 是你创建的一个目录。

现在你可以运行 chroot、fsck、man 和其他实用程序。此时，你正在单用户模式下运行 Linux。

如果你不知道你的 Linux 分区的名称，你可以猜测：挂载不存在的分区不会造成任何伤害。

### 直接启动单用户模式

你也许可以直接启动单用户模式。如果你的系统能够启动，但在完成启动后不允许你登录，请尝试重新启动并在 LILO 引导提示符下指定以下选项之一：

```
LILO boot: linux single
LILO boot: linux emergency
```

在单用户模式下，你的计算机将启动到运行级别 1。你的本地文件系统将被挂载，但网络不会被激活。你将获得一个可用的系统维护 shell。

在紧急模式下，你将被引导到最简化的环境。根文件系统将以只读方式挂载，几乎不会设置任何内容。与 `linux single` 相比，其主要优势在于不会加载 init 文件。如果 init 损坏或无法工作，你仍然可以挂载文件系统以恢复数据，避免在重新安装过程中丢失数据。

### 一个实用技巧

你是否曾经重新构建了一个内核，迫不及待地想尝试你的新作品，但在运行 LILO 之前就重新启动了？而且你在 `lilo.conf` 中没有旧内核的条目？请继续阅读……

在许多情况下，你可以从 Red Hat Linux 引导盘引导你的 Red Hat Linux/Intel 系统，并挂载好你的根文件系统，随时可以使用。方法如下：在引导盘的 `boot:` 提示符下输入以下命令：

```
linux single root=/dev/hdXX initrd=
```

（将 `/dev/hdXX` 中的 XX 替换为你根分区对应的适当字母和数字。）

这是做什么的？首先，它以单用户模式启动引导，并将根分区设置为你自己的根分区。空的 `initrd` 规格跳过了引导盘上与安装相关的映像，这将导致你立即进入单用户模式。

有缺点吗？不幸的是，有。因为 Red Hat Linux 引导盘上的内核仅内置了 IDE 支持，所以使用基于 SCSI 系统的用户将无法使用此技巧。在这种情况下，你必须使用上面提到的引导/救援磁盘组合。

# 3 系统配置

Red Hat Linux 的主要优点之一是操作系统可以配置为执行几乎任何事情。过去，这意味着手动编辑有时晦涩难懂的配置文件，然后重启系统服务，并祈祷你的更改是否正确完成。此外，对于新用户来说，各种配置选项可能令人困惑，因为他们可能不知道在哪里查找特定的配置文件。

Red Hat Linux 提供了两个系统配置实用程序：`linuxconf` 和控制面板。控制面板为各种 Red Hat 系统配置工具提供启动器，包括 `linuxconf`。有关如何使用控制面板及其包含的工具的说明，可以在 3.2 节 *使用控制面板进行系统配置* 中找到。

`linuxconf` 配置工具可以减轻系统配置的一些负担。`Linuxconf` 既是：

- 一个配置接口——你在用户界面中输入配置系统所需的值。
- 一个配置激活器——当你满意于你的编辑时，你告诉 `linuxconf` 应用你所做的更改。

虽然 `linuxconf` 几乎可以做控制面板工具能做的一切，但在两个领域控制面板仍占优势：

- 打印机配置
- 加载内核模块以支持新硬件

让我们看看 `linuxconf`。

## 3.1 使用 `linuxconf` 进行系统配置

`Linuxconf` 允许你配置和控制系统的各个方面，并且能够处理广泛程序和任务。`linuxconf` 的完整文档本身就可以单独成书，这显然超出了我们所能涵盖的范围
