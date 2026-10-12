
```
264 /evolution/mail/pop/michael1@yow.email.yow.org
548 /evolution/mail/pop
8 /evolution/mail/pop
560 /evolution
16 /evolution/meta/file
16 /evolution/meta/trash
28 /evolution/mets
8 /evolution/config
88240 /evolution
12 /../ifka
4 /emacs.d/auto-save-list
2 /emacs.d
4 /Mail-cd
7068 /gv/cache
28 /gftp
72 /root
294 /comps/po
568 /comp
10288 [root@Enterprise3 root#]
```

前面的数字是文件的大小，单位为千字节 `KB`，这是 `df` 和 `du` 命令的默认单位。相应的文件显示在右侧。例如，你可能会看到：：

`86240 /evolution`

第一个点 `.` 表示你从当前目录开始。斜杠 `/` 导航到子目录，例如 `evolution`。换句话说，这一行意味着有 86,240 千字节的磁盘空间被分配给了 `/evolution` 子目录。

`df` 命令显示了计算机上每个挂载文件系统的状况。如图 7.7 所示，`df -m` 命令访问每个文件系统并以兆字节 `MB` 为单位显示结果。它包含了任何其他文件系统，例如你当前挂载的软盘或 CD-ROM 驱动器。`-m` 选项给出兆字节为单位的结果，而 `-k` 选项将其切换为千字节。

# 图 7.7

`df -m` 的输出

| 文件系统 | -blocks | 使用率% | 挂载点 |
| --- | --- | --- | --- |
| /dev/hda2 | 3560 | 194 95% | | |
| /dev/sda | 99 | 78% | /boot |
| home | 129 | 0% | /dev/shm |
| /dev/hdd1 | 1008 | 0 | /home |
| [root@Enterprise3 root#] | | | |

第 7 章 文件系统入门

# 扩展分区数据

Linux 在每个分区中都包含大量数据，你可以通过 `e2label` 和 `dumpe2fs` 等命令访问这些数据。当你安装 Red Hat Enterprise Linux 时，你在安装过程中创建的 Linux 分区会自动赋予适当的标签数据 `label data`。例如，我可以从此命令中获得以下内容：

```
# e2label /dev/sda1
/boot
```

正如你将在本章稍后部分看到的，标签是重要的。默认的 `/etc/fstab` 使用磁盘标签。你也可以在 GRUB 文件中找到磁盘标签。但当你使用 `fdisk` 配置新分区并使用 `mkfs` 对其进行格式化时，这两个命令都不会添加标签。如果你想将 `/home/mj` 目录挂载到 `/dev/sdb1` 分区上，还应该使用以下命令为它标记标签：

```
# e2label /dev/sdb1 /home/mj
```

或者，你可以使用 `dumpe2fs` 命令获取更多关于分区的信息。查看图 7.8，它展示了一个带有 `/boot` 标签的分区。

![](img/2feb3b41073cd1ed27e138a1bee4a0f2_277_0.png)

你甚至可以通过 `dumpe2fs` 输出中的 `Last Mount Time` 变量检查该分区挂载的时间；如果你在该行看到 `n/a`，则在该平台上没有挂载任何目录。

# 挂载目录

在读或写 Linux 分区之前，你需要挂载它。在没有任何帮助的情况下，你需要指定分区、正在挂载的目录以及与分区关联的格式。`mount` 命令的典型语法为：

```
# mount -t format partition directory
```

- 注意。格式 `format` 是分区的配置方式，例如 `ext3`、`reiserfs` 或 `xfs`。分区是被挂载的硬盘设备，例如 `/dev/sda` 或 `/dev/hda1`。目录也被称为挂载点，是分配给该分区的 Linux 目录结构，如 `/boot/`、`/home/` 或 `/var/`。

换句话说，可以使用以下命令将 `/home/mj` 目录挂载到格式化为 `ext3` 文件系统的 `/dev/sdb1` 分区上：

```
# mount ext3 /dev/sdb1 /home/mj
```

这比通常要求的要复杂。有了 `/etc/fystems` 配置文件中的格式列表，命令可以查找此文件并找到与 `/dev/sdb1` 分区匹配的格式。你只需要以下命令：

```
# mount /dev/sdb1 /home/mj
```

你可以让它变得更容易。如果你在 `/etc/fstab` 配置文件中添加以下行，你只需要指定分区或目录：

```
/dev/sdb1 /home/mj ext3 defaults 1 2
```

一旦在 `/etc/fstab` 中配置好，以下任一命令均有效：

```
# mount /dev/sdb1
# mount /home/mj
```

有时你还需要卸载文件系统。例如，你可以使用以下命令来执行卸载：

```
# umount /dev/sda1
# umount /home
```

注意，卸载命令的拼写是 `umount`，而不是 `umount`。

# 故障排除

文件系统的故障比启动问题更难诊断。正如你在第 11 章中看到的，有成熟的方法来处理启动问题。然而，文件系统问题通常需要故障排除。Linux 在启动过程中可能会遇到文件系统问题。如果文件系统损坏，可能需要检查根目录。图 7.9 显示了这种情况。

`fsck` 命令是一个重要的工具。Linux 使用它定期检查分区。如果文件系统损坏，你可能需要调整根目录。

第 7 章 文件系统入门

# 图 7.9

`df -m` 的输出

```
Initializing USB...
Checking root filesystem
Checking device /sda1
无法读取 superblock 或不包含正确的 ext2 superblock。正在尝试打开 /sdb
fsck: clean, 41/21684 files, 12727/19431 blocks

[ OK ]
[ OK ]
[ OK ]
[ OK ]
[ OK ]

*** 在检查文件系统时发生错误。
*** 将你带到 shell：系统在你退出时将重启
*** 输入 root 密码进行维护
（或按 Control-3 继续）：

[FAILED]
```

- 警告：`fsck` 命令用于检查并修复 Linux 文件系统。正如 `mkfs.ext3` 一样，它是相关文件系统命令的前端，如 `fsck.ext2`、`fsck.ext3` 和 `fsck.reiserfs`。如果文件系统格式已知，`fsck` 命令就是你需要的。如果分区被格式化为 `ext3`，则会自动调用 `fsck.ext3`。表 7.4 描述了该命令的关键选项。

| 选项 | 解释 |
| --- | --- |
| -a | 自动修复目标文件系统而不进行提示。应仅在 `/etc/sysinit` 中。 |
| -b | 使用不同的 superblock。你可以通过 `dumpe2fs` 命令找到可选的 superblock。 |
| -A | 检查 `/etc/stab` 列出的所有文件系统。 |
| -R | 当使用 A 时，跳过根 `/` 目录。 |
| -Y | 当 `fsck` 建议解决方案时，它将默认回答为“是”。 |

警告 不要在已挂载的分区上运行 `fsck`。这可能会导致严重的文件系统损坏。

注 顺便说，`fsck` 的发音各异；有人可能读作 es check，而另人可能会讨论分区上的 fish 命令。

# 自动分区检查

`fsck` 命令不再默认定期运行。不过，你可以使用 `tune2fs -c /dev/partition` 来更改此设置。要查找分区的挂载计数，请使用 `dumpe2fs` 命令。相关输出如图7.10所示。

| 最后挂载时间 | 3月25日 16:50:01 2024 |
|---|---|
| 最后写入时间 | 3月25日 16:50:01 2024 |
| 挂载计数 | 74 |
| 最大挂载计数 | 12月13日 06:39 2023 |
| 检查间隔 | 155200 (6) |
| 下次检查后 | 0 (user root) |
| 预留块 | 0 (group root) |
| 第一个 inode | 11 |
| inode 大小 | <none> |
| 日志 inode | 8 |
| 日志设备 | 00000 |

图 7.10 定期分区检查信息![](img/feb3b41073cd1ed27138a0f28_0.png)

# 挂载与重新挂载

挂载的选项之一是以只读模式挂载 `root /` 等文件系统。一旦你做了必要的更改，就可以通过所需的选项重新挂载目录来测试更改。或者，你可能希望以读写模式挂载文件系统。

最终，你可能需要相应更改 `/etc/fstab` 配置并重启 Linux。例如，如果你想以读写模式重新挂载 `root /` 目录，请使用以下命令：
