
> **警告**：`mkfs` 命令将销毁目标设备上的所有数据。

> **注意**：`mkfs` 的用法语法和支持的选项因不同的 Unix、Linux 和 BSD 平台而异。上述示例是在 Linux 系统上创建的。请参阅 `man mkfs` 以查找适用于您系统的正确用法语法。

### 常用用法示例

- `mkfs -t [FSTYPE] [设备]`：在指定驱动器上创建文件系统
- `mkfs -ct [FSTYPE] [设备]`：在格式化之前检查坏块

### `fsck`

**用途：** 检查和修复文件系统。

**用法语法：** `fsck` `[选项]` `[文件系统]`

```bash
# fsck -n /
fsck 1.40.8 (13-Mar-2008)
e2fsck 1.40.8 (13-Mar-2008)
/dev/sda1 contains a file system with errors, check forced.
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
...
```

`fsck` 检查指定文件系统的错误，并在必要时进行修复。在上面的示例中，检查了 `/` 文件系统的错误。使用 `-n` 选项指示 `fsck` 仅检查而不修复指定的文件系统。这是必要的，因为在这种情况下，`/` 文件系统是一个处于活动状态（已挂载）的文件系统，除非首先将其卸载，否则无法修复。

> **警告**：切勿使用 `fsck` 命令来修复已挂载的文件系统，因为这会导致数据损坏。在 Linux 中，您可以通过在命令行中输入 `sudo touch /forcefsck` 来在下次重新启动时安全地运行 `fsck`。其他系统可能需要启动恢复介质才能使用 `fsck`。有关系统中用法的更多信息，请参阅 `man fsck`。

#### 常用用法示例

| 命令 | 描述 |
| :--- | :--- |
| `fsck [文件系统]` | 检查并修复指定的文件系统 |
| `fsck -n [文件系统]` | 检查指定的文件系统而不进行修复 |

### `badblocks`

**用途：** 检查磁盘驱动器中的坏块。

**用法语法：** `badblocks` `[选项]` `[设备]`

```bash
# badblocks -v /dev/sda
Checking blocks 0 to 8388607
Checking for bad blocks (read-only test): done
Pass completed, 0 bad blocks found.
```

`badblocks` 命令是一个 Linux 实用程序，用于搜索磁盘驱动器中的坏块。在上面的示例中，`badblocks` 命令用于检查 `/dev/sda` 中是否存在坏块。包含 `-v` 选项以在扫描期间显示详细状态信息。

健康的磁盘驱动器不应有坏块。如果发现坏块，应立即更换驱动器以避免数据丢失。

> **警告**：默认的 `badblocks` 测试是只读的，通常可以安全地用于活动文件系统。指定 `-w` 选项将执行读写测试，并销毁指定磁盘上的所有数据。它仅应用于测试不包含重要数据的磁盘，因为该磁盘将被完全覆盖。

#### 常用用法示例

- `badblocks [设备]`：检查指定设备中的坏块
- `badblocks -v [设备]`：在检查时显示详细信息
- `badblocks -w [设备]`：对磁盘执行读写测试

### `tune2fs`

**用途：** 调整 Linux 文件系统参数。

**用法语法：** `tune2fs` `[选项]` `[设备]`

```bash
# tune2fs -l /dev/sda5
tune2fs 1.41.9 (22-Aug-2009)
Filesystem volume name:   <none>
Last mounted on:          /
Filesystem UUID:          68dfb151-492b-489a-80d8-0623900de3ba
Filesystem magic number:  0xEF53
Filesystem revision:      1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index
filetype needs_recovery extent flex bg_sparse super_large_file
Filesystem flags:         signed_directory_hash
Default mount options:     (none)
Filesystem state:         clean
...
```

`tune2fs` 命令显示并编辑 Linux 系统上的文件系统设置。它支持 ext2、ext3 和 ext4 文件系统。在上面的示例中，使用 `-l` 参数来显示关于指定文件系统的详细信息。

`fsck` 最常用于调整文件系统的 `fsck` 间隔。这是系统自动对文件系统运行 `fsck` 的间隔。下一个示例显示了控制此设置的变量。

```bash
# tune2fs -l /dev/sda5 | grep -Ei 'check|max'
Maximum mount count:      32
Last checked:             Wed Mar 24 14:14:20 2010
Check interval:           15552000 (6 months)
Next check after:         Mon Sep 20 14:14:20 2010
```

#### 常用用法示例

- `tune2fs -l [设备]`：显示指定文件系统的相关信息
- `tune2fs -c [计数] [设备]`：强制 `fsck` 命令在指定次数的挂载后检查文件系统
- `tune2fs -i [间隔] [设备]`：强制 `fsck` 命令在指定的间隔（以天、周或月为单位）检查文件系统

### `mount` / `umount`

**用途：** 挂载本地和远程文件系统。

**用法语法：** `mount` `[选项]` `[源]` `[目标]`

```bash
# mount /dev/sdb1 /mnt/Seagate
```

`mount` 命令用于挂载文件系统。在上面的示例中，设备 `/dev/sdb1` 被挂载在 `/mnt/Seagate` 目录下。这是挂载本地文件系统的示例。

> 本地文件系统可以配置为在启动时自动挂载，使用 `/etc/fstab` 文件。

`mount` 也可以用于通过 NFS 挂载远程文件系统，如下一个示例所示。

```bash
# mount 10.10.1.48:/home/nick /mnt/nick
```

在此示例中，远程机器（10.10.1.48）上的 `/home/nick` 通过 NFS 共享，并挂载在本地 `/mnt/nick`。

> 要使此操作生效，必须在远程系统上正确配置 NFS。NFS 设置通过 `/etc/exports` 文件管理。

`umount` 命令用于卸载文件系统，如下一个示例所示。

**用法语法：** `umount` `[选项]` `[目录]`

```bash
# umount /mnt/Seagate
```

#### 常用用法示例

- `mount`：显示所有已挂载的文件系统
- `mount [设备] [目录]`：挂载指定设备
- `mount [IP]:[远程] [本地]`：挂载指定的 NFS 共享
- `umount [路径]`：卸载文件系统

### `mkswap`

**用途**：创建交换空间存储。

**用法语法**：`mkswap [OPTIONS] [DEVICE]`

```
# mkswap /dev/sdb1
Setting up swap space version 1, size = 522076 KiB
no label, UUID=cc5b16c-985f-4723-a5c4-e4dd2377aad
Creating swap storage using the mkswap command
```

`mkswap` 命令用于在 Linux 系统上创建交换空间。交换空间用于存储很少访问的内存数据。这可以释放内存供活跃的程序使用。在上面的示例中，`mkswap` 命令用于在 `/dev/sdb1` 分区上创建交换空间存储。

> **提示**
