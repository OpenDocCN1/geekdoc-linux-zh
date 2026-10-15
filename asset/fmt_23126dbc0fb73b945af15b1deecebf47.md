
与其简单地引用磁盘类型、数量和分区号，不如Solaris 磁盘上每个分区（“slice”）的设备文件名包含四个标识符：控制器 (`c`)、目标 (`t`)、磁盘 (`d`) 和切片 (`s`)。因此，设备文件

```
/dev/disk/c0t3ds0
```

标识了磁盘 0 的切片 0，以及位于 SCSI 目标 ID 为 3 的控制器 0。更复杂的是，磁盘设备文件同时存在于 `/dev/disk` 和 `/dev/rdsk` 目录中，分别对应块设备和原始设备条目。原始设备和块设备指向同一个物理分区，但用于不同的语境：使用原始设备仅允许进行小量数据的操作，而块设备可以配合缓冲区使用以增加数据传输率。使用块设备接口还是原始设备接口并不总是很明确，但低级系统命令（如执行磁盘维护的 `fsck` 命令）通常使用原始接口。

命令在整个磁盘上操作（例如报告磁盘使用的 `df` 命令），并很可能使用块设备。

要在 Solaris 系统上安装新硬盘，只需按照以下步骤操作：

1. 通过执行此命令为系统重配置启动做准备：

   `# /reconfigure`

2. 使用此命令同步磁盘数据并关闭系统：

   `# sync; init 0`

3. 切断系统电源，并将新硬盘连接到外部 SCSI 链，或将其安装到合适的磁盘槽中。

4. 检查 SCSI 设备 ID 是否与任何现有 SCSI 设备冲突。如果存在冲突，只需使用切换器更改 ID；

5. 开启电源，如果出现 OpenBoot 监控器，则使用 `boot` 命令加载内核：

   `ok boot`

下一步是（假设你已经决定了在硬盘上创建哪些分区）使用上述提供的信息运行 `format` 程序。除了创建切片外，`format` 还会显示有关现有磁盘和切片的信息，并可用于修复故障磁盘。当在不带命令行参数的情况下调用 `format` 时：

```
## format
```

它会显示当前磁盘的列表，并要求管理员输入要格式化的磁盘编号。在此刻选择一个磁盘进行格式化是非破坏性的，即使你犯了错，也可以随时退出 `format` 程序而不损坏数据。例如，在带有三个 1.0G SCSI 磁盘的 SPARC-20 系统上，`format` 打开打开屏幕：

```
Searching for disks ...
AVAILABLE DISK SELECTIONS:
0.c0t1d0 <SUN1.05 cyl 2036 alt 2 hd 14 sec 72>
```

## 第 13 章：磁盘分区与格式

`/ommuf@,e000000/sbus@,e000100/espdma@f,40000/esp@f,80000/sd1,0`

1. `c0t2d0` <SUN1.5 cyl 2036 alt 2 hd 14 sec 72>

/ommuf@,e000000/sbus@,e000100/espdma@f,40000/esp@f,80000/sd2,0

2. `c0t3d0` <SUN1.5 cyl 2036 alt 2 hd 14 sec 72>

/ommuf@,e000000/sbus@,e000100/espdma@f,40000/esp@f,80000/sd3,0

指定磁盘（输入其编号）：

也可以向 `format` 传递一个命令行选项，其中包含要格式化的磁盘（或磁盘）——例如

```
# format /dev/rdsk/c0t2d0
```

在选择适当的磁盘后，如果磁盘之前格式化过，将出现消息

`[disk formatted]`

这是一条重要信息，因为一个常见的错误是从已格式化和未格式化的可用选项中误认为目标磁盘。菜单看起来如下：

- FORMAT MENU（格式菜单）：

  `disk` - 选择磁盘

  `type` - 选择（定义）磁盘类型

  `partition` - 选择（定义）分区表

  `current` - 描述当前磁盘

  `format` - 格式化并分析磁盘

  `fdisk` - 运行 fdisk 程序

  `repair` - 修复缺陷扇区

  `show` - 翻译磁盘地址

  `label` - 将标签写入磁盘

  `analyze` - 表面分析

  `defect` - 列出缺陷

  `backup` - 搜索并显示标签

  `save` - 保存新的分区定义

  `volume` - 设置卷名称

  `quit` - 执行并返回

如果磁盘尚未格式化，则不会显示该消息。如果磁盘已格式化，将显示消息

`[disk formatted]`

由于您提供的原始文本中未提供待翻译的英文原文，请提供具体的需要翻译的内容。

# Sun Solaris 9.0 系统与网络管理员全方位考试指南

挂载点（Mount Points）简单来说就是使用 `mkdir` 命令创建的空直目录。UFS 的优秀特性之一是它对潜在挂载点具有一对多的映射关系：这意味着一个文件系统可以被挂载，其文件和目录可以在不同的挂载点上进行操作、卸载和重新挂载。当文件系统使用不同的挂载点挂载时修改的所有数据都会被保留。例如，你将 `/dev/disk/c0t2d0s5` 挂载到 `/export/home`，创建一个名为 `pwaters` 的目录（即 `/export/home/pwaters`），卸载文件系统，然后将其重新挂载到 `/usr/local`，`pwaters` 文件夹的内容仍然可用，尽管绝对路径变成了新的（`/usr/local/pwaters`）。

以下是创建挂载文件系统的步骤：

```
# mkdir /export/home
# mount /dev/disk/c0t2d0s5 /export/home
# cd /export/home
# mkdir pwaters
# ls
pwaters
```

也没有什么阻止你将文件系统挂载到不同的挂载点，并保留所有数据：

```
# umount /export/home
# mkdir /usr/local
# mount /dev/disk/c0t2d0s5 /usr/local
# cd /usr/local
# ls
pwaters
```

`mkdir` 命令用于创建挂载点，挂载点等同于目录。如果你想在现有目录的下一级创建一个挂载点，可以使用不带任何选项的 `mkdir` 命令。然而，如果你想在现有目录的几级之下创建一个挂载点，则需要向 `mkdir` 命令传递 `-p` 选项。例如，以下命令将创建挂载点 `/staff`，因为父目录 `/` 已经存在：

```
# mkdir /staff
```

但是，为了创建挂载点 `/staff/nfs/pwaters`，如果 `/staff` 目录尚未存在，则你应该使用 `-p` 选项：

```
# mkdir -p /staff/nfs/pwaters
```

一旦创建了挂载点，将文件系统附加到挂载点上。例如，要将文件系统 `/dev/disk/c0t3d0s5` 挂载到挂载点 `/export/home`，可以使用以下命令：

```
# mount /dev/disk/c0t2d0s5 /export/home
```

## 第 13 章：磁盘分区与格式化

`mount` 命令假设将挂载一个 UFS。如果目标文件系统不是 UFS，则需要使用 `-F` 选项在命令行中指定文件系统类型。支持的文件系统类型包括：

- `- nfs` 网络文件系统 (NFS)
- `pcfs` MS-DOS 格式文件系统
- `s5fs` 系统兼容文件系统

所有当前已挂载文件的详情存储在 `/etc/mnttab` 文件中。绝对不应直接编辑此文件，即使是超级用户。`/etc/mnttab` 文件将包含类似下面的条目：

```
# cat /etc/mnttab
/dev/dsk/c0t0d0s /usr rw,largefiles,suid,dev=1100000 921334412
/proc /proc dev dev=228000 922234448
/fd/fd fd rw,suid,dev=224000 922234448
mtt /etc/mnttab mfs dev=2340000 922234442
swap tmp tmpfs dev=9223441
/dev/dsk/c0t0d0s /usr rw,inner,oner-panic,suid,dev=1100005 922234441
```

## 卸载本地文件系统

在正常操作中，如果文件系统的点和选项在虚拟文件系统表（`/etc/fstab`）中指定，则它会在启动时挂载。系统在关机前会被挂载。然而，有时你可能会发现必要手动卸载文件系统。例如，如果需要使用 `fsck` 命令检查文件系统的完整性；或者，如果文件系统的挂载点将被修改，则需要卸载文件系统并重新挂载到新的挂载点。

> **注意** 不要将同一个文件系统挂载到两个不同的挂载点。

## 配置 /etc/fstab

如果你希望磁盘在重启后可用，你必须在虚拟文件系统表（`/etc/fstab`）中创建一个条目。类似下面的条目：

```
/dev/dsk/c0t2d0s /dev/rdsk/c0t2d0s /export/home ufs 2 yes -
```

该条目包含了切片的块和行设备详情、挂载点、文件系统类型、fsck 指令以及在启动时强制挂载的挂载标记。
