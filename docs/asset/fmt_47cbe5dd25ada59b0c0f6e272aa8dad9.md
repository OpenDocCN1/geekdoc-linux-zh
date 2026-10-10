
# fdisk -l

```
Disk /dev/sda: 11.6 GB, 11560550400 bytes
4 heads, 32 sectors/track, 176400 cylinders
Units = cylinders of 128 * 512 = 65536 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x0009c896

Device     Boot Start      End  Blocks Id System
/dev/sda1        1     76279  4883840 83 Linux
/dev/sda2     76280     91904  1000000 82 Linux swap / Solaris
/dev/sda3    91905    168198  4882816 83 Linux

Disk /dev/sdb: 52.4 GB, 52428848576 bytes
4 heads, 32 sectors/track, 800016 cylinders
Units = cylinders of 128 * 512 = 65536 bytes
Sector size (logical/physical): 512 bytes / 512 bytes
I/O size (minimum/optimal): 512 bytes / 512 bytes
Disk identifier: 0x000c406f

Device     Boot Start      End  Blocks Id System
/dev/sdb1        1     76292 48827120 83 Linux
```

如果你发现更改为不同的设备后系统能够正确启动，那么你可以编辑 GRUB 配置文件（GRUB 1 使用 `/boot/grub/grub.conf` 或 `/boot/grub/menu.lst`；大多数 GRUB 2 系统使用 UUID 并自动检测根分区）并永久更改 `root=` 行。顺便说一下，如果设备确实发生了变化，你可能还需要更改 `/etc/fstab` 中的相同条目。

对于使用分区标签的系统，无法挂载根文件系统的原因可能是添加了具有相同标签分区的磁盘，或者是管理员更改了根分区标签。诊断磁盘标签问题的最佳方法是编辑 `root=` 行，不指定标签，而是指定磁盘设备本身。同样，如果你不知道磁盘是如何布局的，请启动到救援磁盘并输入 `fdisk -l`。如果你发现将 root 设置为磁盘设备而不是标签后能够成功启动，你可以更新 GRUB 配置文件以使用磁盘设备而不是标签，或者你可以使用 `e2label` 程序将根分区的分区标签改回它应该有的状态。例如，要作为 root 将 `/` 标签分配给 `/dev/sda2`，你可以输入：

```bash
e2label /dev/sda2 /
```

在标签重复的情况下，也使用 `e2label` 工具将重复的根分区重命名为其他名称。你可以仅输入 `e2label` 和磁盘设备名称（如 `e2label /dev/sda2`）来显示当前设置的标签是什么。

如果你的系统使用 UUID 且内核找不到根分区，可能是因为 UUID 发生了变化。通常 UUID 应在格式化分区时分配，因此根分区出现这种情况是不寻常的。话虽如此，当有人基于使用 UUID 的系统克隆时经常发生这种情况。当他们为克隆的系统创建根分区时，它会获得一个新的 UUID，但在他们复制 GRUB 配置文件时，其中指定的是旧的 UUID。

与磁盘标签问题类似，解决此问题的快速方法是在 GRUB 菜单处编辑引导提示符，并将 `root=` 行更改为指定特定设备而不是 UUID。如果你发现这样能让你在引导过程中走得更远，那么你可以使用 `blkid` 命令查看分配给特定设备的 UUID：

```bash
$ sudo blkid -s UUID /dev/sda2
/dev/sda2: UUID="528c6527-24bf-4201-b98b-c175f7b66a0f"
```

一旦你知道 UUID 应该是什么，你就可以编辑 GRUB 配置文件（以及 `/etc/fstab`），使其引用正确的 UUID。

### 根分区损坏或失败

内核可能无法挂载根文件系统的另一个主要原因是文件系统损坏或磁盘本身完全故障。当文件系统被挂载时，如果检测到文件系统上的错误，它将自动启动修复过程；然而，在许多情况下，损坏足够严重，引导过程会把你放到一个基本 shell，以便你手动尝试修复文件系统。如果你的引导过程达到这种状态，请前往第 4 章的“修复损坏的文件系统”部分，了解如何纠正错误的详细信息。如果你担心磁盘完全故障，请查看第 10 章，该章节讨论了如何诊断硬件问题。

### 无法挂载辅助文件系统

许多服务器拥有在系统启动时可能自动挂载的多个文件系统。这些文件系统定义在 `/etc/fstab` 文件中，可能看起来如下：

```text
# /etc/fstab: static file system information.
# <file system>       <mount point>  <type> <options>  <dump>  <pass>
proc                  /proc        ext3  defaults        0    0
/dev/sda1             /            ext3  defaults        0    0
/dev/sda2             swap         swap  defaults        0    0
/dev/sda3             /var         ext3  defaults        0    0
/dev/sdb1             /home        ext3  defaults        0    0
```

在这个示例中，你可以看到除了位于 `/dev/sda1` 的 `/` 分区外，系统还从 `/dev/sda3` 挂载了 `/var`，并从 `/dev/sdb1` 挂载了 `/home`。如果 `/var` 或 `/home` 发生损坏且无法自动修复，或者找不到这些分区，引导过程将会停止，并将你带到一个 shell 提示符界面，以便你进一步调查问题。在这种情况下，只需重复你为解决根文件系统问题而可能执行的相同故障排查步骤，查找已变更的设备名称、新标签或不同的 UUID。

# 第 4 章

## 为什么无法写入磁盘？解决磁盘已满或损坏问题

![](img/362b627595d4f10aae346cc0cc8e74eb_79_0.png)

如果你让一个 DevOps 团队描述 Linux 服务器中哪一部分给他们带来了最多的麻烦，许多人会指向硬盘。不仅硬盘是你服务器上最容易发生故障的硬件（我们将在第 10 章中详细讨论），它通常也是你的应用程序的主要瓶颈之一。此外，如果你负责维护服务器，你还必须应对磁盘被占满和文件系统损坏的问题。上述所有问题都始于同一个症状：用户或程序无法将数据写入磁盘。

在 DevOps 组织中，当你排查代码问题时，记录调试数据尤其有价值。当你的某个自动化测试失败时，你需要确切知道导致失败的原因。然而，所有这些日志最终会累积起来，如果任其发展，它们最终会占满磁盘。当这种情况发生时，你可能不会自动知道是哪个目录占用了所有空间，而且当进程无法写入磁盘时，它们有时会以不寻常的方式失败。本章介绍了如何诊断和修复一些可能阻止你写入磁盘的常见问题。

### 当磁盘已满时

Linux 实际上在你用尽磁盘空间时会给出非常明显的提示：

```shell
$ cp /var/log/syslog syslogbackup
cp: writing `syslogbackup': No space left on device
```

当然，根据你的系统分区情况，你可能不知道是哪个分区被占满了。第一步是使用 `df` 工具列出所有已挂载的分区，以及它们的大小、已用空间和可用空间。如果添加 `-h` 选项，它会以人类可读的格式显示数据，而不是以 1K 块为单位：

```shell
$ df -h
Filesystem      Size  Used Avail Use% Mounted on
/dev/sda1        7.8G  7.4G   60K 100% /
none             245M  192M  245M   1% /dev
none               249M     0  249M   0% /dev/shm
none               249M    36K  249M   1% /var/run
none 249M 0 249M 0% /var/lock

none 249M 0 249M 0% /lib/init/rw
```
