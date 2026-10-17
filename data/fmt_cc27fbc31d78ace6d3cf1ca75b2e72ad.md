
在本书的第 1 章中，我展示了如何使用 `crontab` 设置周期性任务（称为 cron 任务）。Linux 系统定期间隔执行这些任务。备份系统是使用 `crontab` 策略的良好方法：如下：

- 每周日凌晨 1:15，你的系统将整个磁盘备份到磁带上。
- 周一至周六，你的系统在凌晨 3:10 执行增量备份，仅保存那些过去 24 小时内变化的文件。

要设置此自动计划，请以 root 身份登录并在名为 `backups` 的文件中输入以下行（此示例假设使用 SCSI 驱动器）：

```
15 1 * * 0 cvf /dev/st0 /
10 3 * * 1-6 cvf /dev/st0 'find / -mtime -1 -type f'
```

接下来，使用以下 `crontab` 命令提交此任务计划：

```
crontab backups
```

现在你已经设置好了自动备份。你唯一需要做的是每天向磁带驱动器中放入一块新磁带。记住也要给每块磁带都贴上合适的标签。

## 访问 DOS/Windows 文件系统

如果你在硬盘上安装了 Microsoft Windows 95/98/Me，你可能已经已经在 Fedora Core 下挂载了 DOS 分区。如果还没有，你可以轻松地在 Fedora Core 中挂载 DOS 分区。挂载使 DOS 目录显示为 Linux 文件系统的一部分。为了容易识别 DOS 分区，你可能想将第一个 DOS 分区挂载为 `/dos0`，第二个以此此类推。

要确定你的 DOS 硬盘分区是否已设为自动挂载，请输入 `grep` 命令在 `/etc/fstab` 文件中查找字符串 `vfat`：

```
grep vfat /etc/fstab
```

如果输出显示包含 `vfat` 的一个或多行，则则你的 Fedora 系统会自动挂载 DOS 分区。

![](img/d9230b719dc0ef80851f363d8c6f571_477.png)

### 挂载 DOS

在 Fedora Core 中挂载 DOS 分区，请使用以下命令：

```
mount -t vfat /dev/sda1 /dos0
```

如果你想卸载 DOS 分区，请使用 `umount` 命令：

```
umount /dos0
```

![](img/d9230b719dc0ef80851f363d8c6f571_478.png)

### 挂载 CD

在 Fedora Core 中挂载 CD 驱动器，请使用以下命令：

```
mount -t iso9660 /dev /mnt/cd
```

如果你想卸载 CD 驱动器，请使用 `umount` 命令：

```
umount /mnt/cd
```

![](img/d9230b719dc0ef80851f363d8c6f571_479.png)

### 挂载软磁盘

在 Fedora Core 中挂载软磁盘，请使用以下命令：

```
mount -t vfat /dev/fd0 /mnt/floppy
```

如果你想卸载软磁盘，请使用 `umount` 命令：

```
umount /mnt/floppy
```

![](img/d9230b719dc0ef80851f363d8c6f571_480.png)

## 使用 mtools

- 4. 注销并以普通用户身份登录。
- 5. 为了确认你可以作为普通用户挂载 DOS 软盘而不仅仅是 root，请向 A 盘插入一张 DOS 软盘并输入以下命令：

```
mount /a
```

挂载操作成功，当你输入命令 `ls /a` 时，你会看到 DOS 软盘的文件列表。
- 6. 要卸载 DOS 软盘，请输入 `umount /a`。

### 挂载 NTFS 分区

如今，大多数电脑硬盘上都预装了 Windows XP 和 Windows 2000。Windows XP, 2000 以及 Windows NT 通常都使用 NTFS 文件系统 (`NTFS`)。Linux 支持对 NTFS 分区的只读访问，而 Fedora Core 并没有包含访问 NTFS 分区所需的 `ntfs.ko` 内核模块。

如果你在 Windows XP 系统上安装了 Fedora Core 并想要访问 NTFS 分区上的文件，可以在内核配置步骤选择 NTFS 模块后编译内核（详细说明请参阅本微型书籍的第 6 章关于配置、编译和安装内核的介绍）。

重启并从新内核启动后，以 root 身份登录，输入以下命令为 NTFS 分区创建一个挂载点（在此情况下，我是在 `/mnt` 目录下创建一个挂载点）；

现在，你可以使用以下命令挂载 NTFS 分区：

```
mount /dev/hda2 /mnt/xp -t ntfs -r -umask=0222
```

将 `/dev/hda2` 替换为系统中 NTFS 分区的设备名称。大多数电脑都预装了 Windows XP，第二个分区是第二个（`/dev/hda2`）——第一个分区（`/dev/hda1`）通常是用于存放 Windows XP 安装文件的隐藏分区。

![](img/d9230b719dc0efd80851f363d8c6f571_481_0.png)

访问 MS-DOS 文件系统的方法是使用 `mount` 命令挂载硬盘或软盘，然后使用 `ls` 和 `cp` 等 Linux 命令来操作已挂载的 DOS 文件系统。这种挂载 DOS 文件系统的方法对于硬盘来说是可行的。Linux 可以在启动时自动挂载 DOS 分区，你可以随时访问硬盘上的 DOS 目录。

### 使用 mtools

然而，如果你想快速查看 DOS 软盘的目录列表，挂载可能会变得非常繁琐。首先，你必须挂载软盘驱动器。然后你必须使用 `ls` 命令。最后，在弹出软盘之前，你还必须使用 `umount` 命令。

这种情况正是 mtools 包大显身手的地方。mtools 包实现了大多数常用的 DOS 命令：这些命令的名称与 DOS 相同，只需在每个命令前加上一个 `m` 前缀。因此，获取目录列表的命令是 `mdir`，`mcopy` 用于复制文件。mtools 最棒的部分在于，你不需要挂载软盘就可以使用 mtools 命令。

由于 mtools 命令会直接读写物理设备（软盘），你必须以 root 身份登录才能执行这些命令。如果你想让任何用户都能使用 mtools 命令，你必须修改软盘设备的权限设置。使用以下命令允许任何人对第一个软盘驱动器进行读写：

![](img/d9230b719dc0efd80851f363d8c6f571_482_0.png)

```
chmod +rw /dev/fd0
```

### 尝试 mtools

要 m mtools，遵循以下步骤：
- 1. 将一张 MS-DOS 软盘放入系统的 A 盘。
- 2. 输入 `mdir`。

你会看到软盘的内容（标准的 DOS 目录列表格式）。

通常，你使用 mtools 工具集来访问软盘。默认配置文件 `/etc/mtools.conf` 设置为将软盘驱动器作为 A 盘访问。你也可以编辑它为你的 DOS 硬盘分区定义 C 和 D 盘，你也可以通过 Linux 的 `mount` 命令挂载它们来访问硬盘分区。由于你可以在启动时自动挂载硬盘分区，因此通过 Linux 命令访问它们通常同样简单。

### 理解 /etc/mtools.conf 文件

mtools 包可以使用默认设置工作，但如果你遇到任何错误，请检查 `/etc/mtools.conf` 文件。该文件包含了 mtools 工具所可见的驱动器定义（如 A、B 和 C）。以下是典型的 `/etc/mtools.conf` 文件的几行：

```
drive a: file="/dev/fd0" exclusive mformat_only
drive b: file="/dev/fd1" exclusive mformat_only

# 第一个 SCSI 磁盘分区
drive c: file="/dev/sda1"

# Windows 98 PC上的第一个 IDE 磁盘分区
drive c: file="/dev/hda1"

# 内部 IDE Zip 驱动器
drive e: file="/dev/hda4"
```

井号 (`#`) 表示注释的开始。每行定义一个驱动器字母、关联的 Linux 设备名称以及指示如何访问驱动器的关键字。在这个示例中，前两行定义了驱动器 A 和 B。第三行定义驱动器 C 为第一个驱动器（`/dev/hda1`）上的第一个分区。如果你有其他的 DOS 驱动器（例如 D），可以添加另一行来定义 D。如果你的系统是一个高密度 3.5 英寸软盘驱动器，不需要更改 `/etc/mtools.conf` 文件中的任何内容即可访问软盘驱动器。如果你还想访问硬盘上的任何 DOS 分区，请取消注释并编辑适当的驱动器行。对于内置 IDE (ATAPI) 驱动器，尝试将 `/dev/hda4` 作为设备并在 `/etc/mtools.conf` 中添加以下行：

```
drive e: file="/hda4"
```
