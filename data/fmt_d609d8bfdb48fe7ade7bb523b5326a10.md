
# systemctl reload autofs

```
使用 `/etc/auto.misc` 文件中的默认配置，你现在应该能够通过直接访问配置的目录自动将 CD 挂载到 `/misc/cd` 目录。一旦驱动器中插入了 CD，以下命令应该可以运行：
```

# ls /misc/cd
```

- 等待至少五分钟并重复之前的命令。你看到了什么？

## 场景与解决方案

你需要为标准 Linux 分区、交换空间（swap）和一个逻辑卷（LV）配置多个分区。
你想根据 UUID 在启动过程中设置一个挂载。
你需要格式化……

- 使用 `fdisk`、`gdisk` 或 `parted` 实用创建分区，然后使用 `t` 或 `set` 命令修改它们的分区类型。
- 使用 `blkid` 命令识别卷的 UUID，并在 `/etc/fstab` 文件系统类型中使用该 UUID。
- 使用 `mkfs.xfs` 命令格式化目标卷。
- 使用如 `mkfs.ext2`、`mkfs.ext3` 或 `mkfs.ext4` 的命令格式化目标卷。
- 使用 `pvs` 命令将 PV 合并到 VG；使用 `vgcreate` 命令创建 LV；格式化 LV 以备。

- 你想设置逻辑卷。
你想在不破坏其他分区的情况下添加新文件系统。
你想扩展用 XFS 文件系统格式化的 LV 的可用空间。

- 使用可用或新安装的驱动器上的可用空间。
- 使用 `lvextend` 命令增加 LV 的可用空间，然后使用 `xfs_growfs` 命令相应地扩展格式化的文件系统。

# 304 第 7 章 存储与文件系统管理

# 文件系统格式

- 3. 像 XFS 这样的日志文件系统的主要优势是什么？
- 4. 使用什么命令将 `/dev/sdb3` 格式化为默认的 Red Hat 文件系统格式？

# Linux 基本文件系统与目录

- 5. 在默认的 RHEL 9 安装中，哪个文件系统挂载在与顶层根目录分开的目录上？
- 6. 列出 `/` 目录下两个不适合与包含顶层根目录的卷分开挂载的目录。

# 逻辑卷管理器 (LVM)

- 7. 在创建一个新分区并将其设置为逻辑卷管理器类型后，使用什么命令将其添加为 PV？
- 8. 在给逻辑卷（LV）增加更多空间后，使用什么命令扩展底层的 XFS 文件系统以填充空间？

# 文件系统管理

- 9. 要更改本地文件系统的挂载选项，需要编辑哪个文件？
- 10. 在 `/etc/fstab` 文件中添加什么内容可以设置 ext4 文件系统 `/dev/sda6` 挂载在 `/usr` 且为只读并带有其他选项？假设找不到 `/dev/sda6` 的 UUID。同时假设 dump 值为 1，文件检查顺序为 2。

# 自动挂载器 (Automounter)

- 11. 如果你启动了 autofs 进程并想要从计算机 `server1.example.com` 读取共享 NFS 目录列表，你会使用什么与自动挂载相关的命令？
- 12. 列出与 RHEL 9 上默认安装的自动挂载相关的配置文件。

## 实验题

Red Hat 以电子化提供考试。因此，本章的实验可以在随书的配套网站上获得。如果你尚未在系统上安装 RHEL，请参阅第 1 章的安装说明。每个实验的答案紧随在自测答案之后。

## 自测答案

# 存储管理与分区

- 1. 用于列出所有连接硬盘上配置分区的 `fdisk` 命令选项是 `fdisk -l`。
- 2. 在创建交换分区后，你可以使用 `mkswap devicename` 和 `swapon devicename` 命令来初始化并激活该卷；将设备文件替换为卷（如 `/dev/sda1` 或 `/dev/VolGroup00/LogVol03`）以代替 `devicename`。

# 文件系统格式

- 3. 像 XFS 这样的日志文件系统的主要优势是数据恢复更快。
- 4. 将 `/dev/sdb3` 格式化为默认 Red Hat 文件系统格式的命令是 `mkfs.xfs /dev/sdb3`。命令 `mkfs -t xfs /dev/sdb3` 也是可以的答案。

# Linux 基本文件系统与目录

- 5. `/boot` 是与 `/` 分开挂载的。
- 6. 这个问题有很多正确答案；不适合分开挂载的目录包括 `/include`、`/bin`、`/dev` 和 `/etc`。（相比之下，几个目录本质上显示作为挂载的占位符，包括 `/media` 和 `/mnt`。）

# 逻辑卷管理器 (LVM)

- 7. 在创建一个新分区并将其设置为逻辑卷文件类型后，将其添加为 PV 的命令是 `pvcreate /dev/sdb2`。例如，如果分区是 `/dev/sdb2`，则命令为 `/dev/sdb2`。
- 8. 在给逻辑卷（LV）增加更多空间后，扩展底层系统以填充新空间的命令是 `xfs_growfs`。

# 文件系统管理

- 9. 要更改本地文件系统的选项，请编辑 `/etc/fstab`。
- 10. 由于 UUID 未知，你需要使用卷的设备文件（在此例下为 `/dev/sda6`）。要添加到 `/etc/fstab` 的行如下：

```
/dev/sda6 /usr      ext4      defaults,ro      1 2
```

# 306 第 7 章 存储与文件系统管理

# 自动挂载器

- 11. 如果你启动了 autofs 进程并想要从服务器 `server1.example.com` 读取共享 NFS 目录列表，你用于列出这些目录的自动挂载相关命令是 `cat /etc/auto.net server1.example.com`。
- 12. 与 RHEL 9 默认安装的自动挂载相关的配置文件包括 `master` 和 `auto.misc`，都在 `/etc` 目录下。

## 实验答案

## 实验 1

此实验假设新设备作为 `/dev/sdb` 可用。如果设备名称不同，请相应替换。

- 1. 运行 `parted /dev/sdb`。使用以下命令创建新分区：

```
(parted) mkpart
Partition type? primary/extended? primary
File system type? [ext2]? xfs
Start? 1MiB
End? 1025MiB
```

注意文件系统从 1MiB 开始。如果输入 0MiB 会发生什么？

- 2. 输入 `print` 显示磁盘上的分区表。输入 `q` 退出 parted。

- 3. 格式化新文件系统：

```bash
# mkfs.xfs /dev/sdb1
```

- 4. 创建挂载点：

```bash
# mkdir /test1
```

- 5. 查找设备的 UUID：

```bash
# blkid /dev/sdb1
```

- 6. 使用找到的 UUID 将以下行添加到 `/etc/fstab`：

```
/dev/sdb1 /test1 xfs uuid=UUID defaults 0 0
```

- 7. 运行 `mount -a` 挂载文件系统。

- 8. 使用 `df -h` 验证卷已挂载。

# 实验 2

此实验假设设备作为 `/dev/sdb` 可用。如果设备名称不同，请相应替换。

- 1. 运行 `parted /dev/sdb`。使用以下命令创建新分区：

```
(parted) mkpart
Partition type? primary/extended? primary
File system type? [ext2]? xfs
Start? 1MiB
End? 1025MiB
```

注意文件系统从 1MiB 开始。如果输入 0MiB 会发生什么？

- 2. 输入 `print` 显示磁盘上的分区表。输入 `q` 退出 parted。

- 3. 格式化新文件系统：

```bash
# mkfs.xfs /dev/sdb1
```

- 4. 创建挂载点：

```bash
# mkdir /test1
```

- 5. 查找设备的 UUID：

```bash
# blkid /dev/sdb1
```

- 6. 使用找到的 UUID 将以下行添加到 `/etc/fstab`：

```
/dev/sdb1 /test1 xfs uuid=UUID defaults 0 0
```

- 7. 运行 `mount -a` 挂载文件系统。

- 8. 使用 `df -h` 验证卷已挂载。

## 实验 3

此实验假设设备作为 `/dev/sdb` 可用。如果设备名称不同，请相应替换。

- 1. 运行 `parted /dev/sdb`。使用以下命令创建新分区：

```
(parted) mkpart
Partition type? primary/extended? primary
File system type? [ext2]? xfs
Start? 1MiB
End? 1025MiB
```
