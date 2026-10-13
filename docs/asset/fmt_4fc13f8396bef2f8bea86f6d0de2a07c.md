
Quotas for user cloobie:

/dev/hda3 blocks in use: 58, limits (soft = 3000, hard = 5000)

inodes in use: 41, limits (soft = 500, hard = 1000)

保存文件。最后一步，你必须再次使用 `edquota` 设置宽限期，这次使用 `-t` 选项。如果超过了较低的“软”限制，你的新用户将收到警告：

```bash
# edquota -t cloobie
```

然后你可以为文件数量或磁盘设置宽限期警告：
时间单位可以是天、小时、分钟或秒
在对用户执行软限制之前的宽限期：
/dev/hda3 block grace period: 1 days, grace period: 1 days

如果你想立即警告用户，可以将宽限期设置为一天（你也可以使用分钟或秒）。最后，你可以使用 `quota` 命令检查新的配额：

```bash
# quota cloobie
Disk quotas for user cloobie (uid 502):
Filesystem blocks quota limit grace files quota limit grace
/dev/hda3 58 3000 5000 41 500 1000
```

使用配额有时是必要的。如果你的磁盘空间非常紧张，这可能是管理硬盘资源的一种方法。

# 基础 SuSE 系统管理

## 总结

本节介绍了你维护运行 SuSE Linux 的计算机所需的某些基本系统管理技能。你还学习了如何在 Linux 运行时获取计算机内存内部运行的信息，以及如何控制后台进程、用户和系统资源（如磁盘空间）。

## 问答

- 我尝试将 pico 定义为我的默认编辑器，但要么收到错误信息，要么 vi 仍然运行了。我漏掉了什么？
- ：请确保你已经安装了 pico 程序（使用 `y` 或 `rpm`）。pico 编辑器通常是 pine 邮件程序发行的一部分，但也作为一个独立的 rpm 文件包含。
- 我使用 `userdel` 从系统中删除了用户，但 `/home` 下的用户目录还在。为什么？
- ：像 `userdel` 这样的工具可能不会删除用户目录。你应该使用 `yast` 来删除用户以及用户的文件和目录。你可能还需要删除用户的邮件文件（位于 `/var/spool/mail` 目录中）。
- SuSE Linux 还带了哪些其他用于管理用户的工具？
- ：要处理一次性创建几十或数百个新用户的管理工作，请参阅 `newusers` 命令。

## 练习

- 使用 `osview` 或 `xload` 等其他 X11 工具查看系统进程。这些工具有什么不同？
- `/home` 和 `/var/spool` 目录可能包含属于你的 SuSE Linux 系统的文件。如何轻松地“找到”系统中属于某个用户的所有文件？

![](img/cbf420b293bae71df92ae05ab020555_502.png)

# 第 22 小节

# 文件与文件系统

本节继续介绍系统管理基础，并向你介绍 Linux 下的文件处理。你将学习如何挂载文件系统、管理文件系统表（fstab）以及格式化软盘。你将看到如何保护文件和目录。你还将学习如何从命令行或 X 会话期间安装或卸载软件。

在本节中，你将：

- 学习 SuSE Linux 是如何组织的
- 读取系统的文件系统表
- 格式化软盘
- 在 Linux 下读取、写入或格式化 DOS 软盘
- 学习读取 Linux 目录列表
- 学习更改文件权限和所有权
- 使用 `rpm` 和 `yast` 安装或删除软件

这些操作需要将不同的软件组件安装在你的 SuSE Linux 文件系统的不同部分。如果你再次查看文件系统列表，你会看到 `/mnt`，即挂载目录（mount directory）。传统上这是挂载其他系统的地方，尽管 SuSE Linux 专门为这些介质包含了 `/floppy` 和 `/cdrom` 目录。下一节将讨论如何让这些系统出现在挂载目录下。

## 使用 mount 命令访问其他文件系统

`mount` 命令位于 `/bin` 目录，是一个至关重要的程序，不仅被系统管理员或 sysadmins 使用，SuSE Linux 在启动和关闭期间也会使用。该命令用于挂载文件系统并使其在你的目录树中可用。在启动期间，主 Linux 分区（一个 ext2 文件系统）被挂载到 `/`，或者你可以在工作时使用 `mount` 和 `unmount` 命令进行挂载和卸载。`mount` 命令可以识别并挂载（取决于你内核模块的配置）多个文件系统。

本节侧重于最常见的文件系统，例如用于 Linux 的 ext2、DOS 的 vfat 以及用于 CD-ROM 的 iso9660。对不同文件系统的支持（例如提供长文件名的 VFAT）包含在 `/lib/modules/2.2.1/` 中。SuSE Linux 启动时启用 VFAT 支持。VFAT（以及其他文件系统）的支持位于 `/lib/modules/` 中。

## 理解文件系统表 /etc/fstab

当你启动 Linux 时，运行运行的脚本之一位于 `/etc/rc` 目录下。该脚本首先挂载交换分区（在安装 SuSE Linux 时创建），然后在检查错误后将你的根分区挂载为读/写模式。如果一切正常，它将使用以下命令挂载文件系统表 `/etc/fstab` 中描述的所有文件系统：

```
mount -a nonfs
```

## 处理文件与你的系统

此命令会挂载 `/etc/fstab` 中描述的所有文件系统，但除了旨在自动挂载的项（例如 CD-ROM），该文件是一个短文本文件：

| <device> | <mountpoint> | <filesystem> | <options> | <dump> | <fsck> |
| :--- | :--- | :--- | :--- | :--- | :--- |
| /dev/hda6 | swap | ext2 | defaults | 0 | 1 |
| /dev/hda1 | | ext2 | defaults | 0 | 1 |
| /dev/hdc | /cdrom | iso9660 | ro,noauto,user | 0 | 0 |
| /dev/fd0 | floppy | auto | noauto,user | 0 | 0 |
| none | /proc | proc | defaults | 0 | 0 |

fstab 列显示了设备名称、文件系统挂载的位置、文件系统类型、任何挂载选项、dump 命令（在第 23 小节“备份和恢复你的系统”中讨论）以及在重启期间检查文件系统的顺序。你的文件系统表看起来将与这里显示的示例不同，特别是当你的计算机使用 SCSI 接口时。这里描述的文件系统表仅仅是一个示例。fstab 的行显示了 Linux ext2 文件系统；/proc 进程目录；SuSE Linux 交换目录；软盘（/dev/fd0）；以及 CD-ROM 设备（/dev/cdrom，这是一个符号链接）。

你应该知道，编辑文件系统表本质上是危险的。你在第 21 小节“基础系统管理”中学习过这一点。在添加硬盘、新分区等内容之前，请务必制作备份副本。确保你手头有 SuSE Linux 启动盘（在安装期间创建）。如果情况出现意外，你可以用软盘启动，使用命令挂载你硬盘上的 SuSE Linux 分区，然后复制并恢复 `/etc/fstab` 文件。通常情况下，root 操作员挂载和卸载文件系统。如果你听取我的建议，不要一直以 root 身份运行 Linux，你将必须使用以下命令：

```
su -c "mount /cdrom"
```

这条命令将挂载插入的 CD-ROM 到 `/cdrom` 目录。该命令更正式的形式是：

```
su -c "mount -t iso9660 /dev/hdc /cdrom"
```

此命令使用 `mount` 命令指定文件系统 iso9660 和设备 hdc（你的可能不同）挂载到 `/cdrom`。

看起来很多吗？如果你想让这个过程变得简单，可以使用 `mount` 命令的 user 选项。这样你就不需要使用 `su` 命令来挂载 CD-ROM、输入密码或输入命令行。例如，用你喜欢的文本编辑器（以 root 身份）打开 `/etc/fstab` 文件，并将原始 fstab 项更改为：

```
/dev/hdc /cdrom iso9660 noauto,ro,user,dev,exec 0 0
```

ro 选项指定设备为只读。exec 选项允许任何人从 CD-ROM 运行程序。在做出更改后保存文件。你将能够在无需作为 root 操作员的情况下挂载 CD-ROM，通过使用：

```
mount /dev/hdc
```

或者

```
mount /cdrom
```
