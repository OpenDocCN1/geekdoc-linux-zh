
如果你想要一个显示目标、源、类型和使用率的输出，可以使用：

```bash
$ df -h --output=target,source,fstype,pcent
Mounted on               Filesystem      Type    Use%
/dev                    udev            devtmpfs 0%
/run                    tmpfs           tmpfs   1%
/        /dev/sda1       ext4    25%
/dev/shm                tmpfs           tmpfs   32%
/run/lock               tmpfs           tmpfs   0%
/sys/fs/cgroup          tmpfs           tmpfs   0%
/run/user/119           tmpfs           tmpfs   1%
/run/user/1000          tmpfs           tmpfs   1%
/media/carol/part1      /dev/sdb1       ext4    2%
/media/carol/part3      /dev/sdb3       ext4    3%
/media/carol/part2      /dev/sdb2       ext4    3%
/media/carol/Samsung External Hard Drive /dev/sdc1 fuseblk 75%
```

`df` 还可以通过向 `--output=` 传递以下字段来检查 inode 信息：

- `itotal`

  文件系统中 inode 的总数。

- `iused`

  文件系统中已使用的 inode 数量。

- `iavail`

  文件中可用的 inode 数量。

- `ipcent`

  文件系统中已使用 inode 的百分比。

例如：

```bash
$ df --output=source,fstype,itotal,iused,ipcent
Filesystem    Type      Inodes  IUsed  IUse%
udev          devtmpfs  735764    593    1%
tmpfs         tmpfs     744858   1048    1%
/dev/sda1     ext4      7069696 318651   5%
tmpfs         tmpfs     744858    222    1%
tmpfs         tmpfs     744858      3    1%
tmpfs         tmpfs     744858     18    1%
tmpfs         tmpfs     744858     22    1%
tmpfs         tmpfs     744858     40    1%
```

### 维护 ext2、ext3 和 ext4 文件系统

为了检查文件系统错误（并希望修复它们），Linux 提供了 `fsck` 实用工具（记住“filesystem check”的意思，你就永远不会忘记这个名字）。在最基本的使用形式中，你可以通过在 `fsck` 后跟想要检查的文件系统位置来调用它：

```bash
# fsck /dev/sdb1
fsck from util-linux 2.33.1
e2fsck 1.44.6 (5-Mar-2019)
DT_2GB: clean, 20/121920 files, 369880/487680 blocks
```

> **警告** 切勿在已挂载的文件系统上运行 `fsck`（或相关实用工具）。如果这样做，可能会丢失数据。

`fsck` 本身不会检查文件系统，它只是调用适合该文件系统类型的相应实用工具进行检查。在上面的示例中，由于未指定文件系统类型，`fsck` 默认假设为 ext2/3/4 文件系统，并调用了 `e2fsck`。

要指定文件系统，请使用 `-t` 选项，后跟文件系统名称，例如 `fsck -t vfat /dev/sdc`。或者，你可以直接调用特定于文件系统的实用工具，例如用于 FAT 文件系统的 `fsck.msdos`。

**提示** 输入 `fsck` 然后按两次 Tab 键，以查看系统中所有相关命令的列表。

`fsck` 可以接受一些命令行参数。以下是其中一些最常用的参数：

- `-A`

  这将检查 `/etc/fstab` 中列出的所有文件系统。

- `-C`

  在检查文件系统时显示进度条。目前仅适用于 ext2/3/4 文件系统。

- `-N`

  这将打印将要执行的操作并退出，而不会实际检查文件系统。

- `-R`

  当与 `-A` 一起使用时，这将跳过对根文件系统的检查。

- `-V`

  详细模式，在操作期间打印比平时更多的信息。这对于调试很有用。

ext2、ext3 和 ext4 文件系统的特定实用工具是 `e2fsck`，也称为 `fsck.ext2`、`fsck.ext3` 和 `fsck.ext4`（这三个只是指向 `e2fsck` 的链接）。默认情况下，它以交互模式运行：当发现文件系统错误时，它会停止并询问用户要做什么。用户必须输入 `y` 来修复问题，输入 `n` 表示不修复，或者输入 `a` 表示修复当前问题以及所有后续问题。

当然，坐在终端前等待 `e2fsck` 询问该怎么办并不是时间的有效利用方式，特别是如果你正在处理大型文件系统时。因此，有一些选项可以让 `e2fsck` 以非交互模式运行：

- `-p`

  这将尝试自动修复发现的任何错误。如果发现需要系统管理员介入的错误，`e2fsck` 将提供问题描述并退出。

- `-y`

  这将对所有问题回答 `y`（是）。

- `-n`

  与 `-y` 相反。除了对所有问题回答 `n`（否）之外，这还将使文件系统以只读方式挂载，因此无法修改。

- `-f`

  强制 `e2fsck` 检查文件系统，即使其被标记为“干净”，即已正确卸载。

### 微调 ext 文件系统

ext2、ext3 和 ext4 文件系统有许多可由系统管理员调整或“微调”的参数，以更好地满足系统需求。用于显示或修改这些参数的实用工具称为 `tune2fs`。

要查看任何给定文件系统的当前参数，请使用 `-l` 参数，后跟代表分区的设备。下面的示例显示了对机器上第一个磁盘的第一个分区（`/dev/sda1`）执行此命令的输出：

```bash
# tune2fs -l /dev/sda1
tune2fs 1.44.6 (5-Mar-2019)
Filesystem volume name:   <none>
Last mounted on:          /
Filesystem UUID:          6e2c12e3-472d-4bac-a257-c49ac07f3761
Filesystem magic number:  0xEF53
Filesystem revision #:    1 (dynamic)
Filesystem features:      has_journal ext_attr resize_inode dir_index filetype
                         needs_recovery extent 64bit flex_bg sparse_super large_file huge_file dir_nlink extra_isize
                         metadata_csum
Filesystem flags:         signed_directory_hash
Default mount options:    user_xattr acl
Filesystem state:         clean
Errors behavior:          Continue
Filesystem OS type:       Linux
Inode count:              7069696
Block count:              28255605
Reserved block count:     1412780
Free blocks:              23007462
Free inodes:              6801648
First block:              0
```

### 文件系统属性

- 块大小：4096

- 碎片大小：4096

- 组描述符大小：64

- 保留的 GDT 块数：1024

- 每组块数：32768

- 每组碎片数：32768

- 每组 inode 数：8192

- 每组节点块数：512

- 灵活块组大小：16
