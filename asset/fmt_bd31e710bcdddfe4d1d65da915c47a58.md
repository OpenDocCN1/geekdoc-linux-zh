
## 描述

`mke2fs` 用于创建 ext2、ext3 或 ext4 文件系统，通常在磁盘分区中创建。`*device*` 是对应于设备的特殊文件（例如 `/dev/hdXX`），`*blocks-count*` 是设备上的块数。如果省略，`mke2fs` 将自动计算文件系统大小。如果作为 `mkfs.ext3` 调用，则会创建一个日志，就像指定了 `-j` 选项一样。

新创建的文件系统的参数默认值，如果没有被下面列出的选项覆盖，将由 `/etc/mke2fs.conf` 配置文件控制。更多信息请参见 `mke2fs.conf(5)` 手册页。

## 选项

`-b block-size`

以字节为单位指定块的大小。有效的 `block-size` 值为每块 1024、2048 和 4096 字节。如果省略，则根据文件系统大小和文件系统的预期用途启发式确定 `block-size`（参见 `-T` 选项）。如果 `block-size` 前面带有负号（'-'），`mke2fs` 将确定块大小。

`-c`

在创建文件系统之前检查设备是否有坏块。如果指定了此选项，速度将慢得多。

`-C cluster-size`

以字节为单位指定簇的大小。如果启用了 bigalloc 功能，有效的 `cluster-size` 值范围为 2048 到 256M。（详情请参见 `ext4(5)` 手册。）

`-D`

在创建文件系统时使用直接 I/O。这对于稀疏文件和存储很有用。

`-E extended-options`

设置扩展选项。扩展选项用逗号分隔。`-E` 选项仍然支持：

`mp_update_interval`

调整初始更新。指定的间隔必须小于 300 秒。

`stride`

为条带（stripe）配置文件系统。这是每个条带中的块数。

`stripe_width`

为条带宽度（stripe-width）配置文件系统。这是 RAID 中承载数据的磁盘数量（对于 RAID 5，有一个校验盘）。

`resize=max-online-resize`

预留足够的空间以便块组描述符可以增长。

`lazy_atomic_init=<0 禁用, 1 启用>`

如果启用了 uninit_bg 功能，inode 表将不会完全初始化。这加快了文件系统的初始化，但需要内核在后台完成文件系统的初始化。如果省略了该选项，默认为 1。

`lazy_journal_init=<0 禁用, 1 启用>`

如果启用，`mke2fs` 将不会对 inode 进行完全清零。这加快了文件系统的初始化，但系统在此之前崩溃会有很小的风险。如果省略了该选项，默认为 1。

`root_owner=<uid:gid>`

指定根目录的数字用户 ID 和组 ID。如果没有指定 UID:GID，将使用运行 `mke2fs` 的用户和组 ID。在 `mke2fs` 1.42 及之前的版本中，根目录的 UID 和组 ID 默认设置为运行 `mke2fs` 的用户的 UID 和组 ID。`root_owner=` 选项允许显式指定这些值，并为不期望文件系统内容发生的用户避免副作用。

`test_fs`

在文件系统分区中设置标记，指示其可能使用实验性内核代码（例如 ext4 文件系统）挂载。

`discard`

在 mkfs 时尝试丢弃块，这对于固态设备和精简存储很有用。当设备宣布丢弃也会清零（随后的读取返回零），则会将所有未清零的 inode 表标记为清零。这显著加快了文件系统的初始化。这是默认设置。

`nodiscard`

在 mkfs 时不丢弃块。

`-f fragment-size` 以字节为单位指定碎片的大小。

`-F` 即使设备不在分区或块设备上，或者其他参数不合理也强制 `mke2fs` 创建文件系统。为了让 `mke2fs` 即使在文件系统在使用或挂载的情况下也能创建（这是一个非常危险的操作），必须指定两次此选项。

`-g blocks-per-group` 指定块组中的块数。用户通常没有设置此参数的理由，因为默认值是最优的。此选项通常供开发测试用例的开发者。如果启用了 bigalloc 功能，`-g` 选项

将指定块组中的簇数量。

`-G number-of-groups` 在 ext4 文件系统中创建一个更大的虚拟块组（或“flex-bg 组”）。这可以提高元数据的局部性，并提升元数据工作负载下的性能。组组的数量必须是 2 的幂次，且只有在启用了 `flex_bg` 文件系统功能时才能指定。

`-bytes-per-inode` 指定每个索引的字节数。`mkefs` 会为磁盘上每 `bytes-per-inode` 字节的空间创建一个索引（inode）。`bytes-per-inode` 比例越大，创建的索引数量就越少。此值不应小于文件系统的块大小（blocksize），因为这样创建的索引数量将超过实际使用的数量。请注意，在文件系统创建后无法更改此比例，因此在决定此参数的值时要小心。

`-i inode-size` 指定每个索引的大小。`inode-size` 值必须是 2 的幂次，且大于或等于 128。`inode-size` 越大，索引表消耗的空间就越多，这会减少文件系统的可用空间并可能对性能产生负面影响。文件系统创建后无法更改此值。在内核 2.6.10 和某些早期内核中，可以使用大于 128 字节的索引来存储扩展属性以提高性能。旧版内核不可见大索引中的扩展属性，且 2.4 内核将不支持此类文件。默认索引大小由 `mkefs.conf` 文件控制。大多数文件系统的默认大小为 256 字节，小型文件系统除外，其大小为 128 字节。

`-j` 使用 ext3 日志创建文件系统。如果未指定 `-J` 选项，将使用默认日志参数来根据文件系统的大小创建一个合适大小的日志，并存储在文件系统内部。请注意，你必须使用支持 ext3 的内核才能实际利用日志功能。

`-J journal-options` 使用命令行上指定的选项创建 ext3 日志。日志选项用逗号分隔，并可以使用等号（'='）带入参数。支持以下日志选项：
    - `size=journal-size`：创建一个大小为 `journal-size` MB 的内部日志（即存储在文件系统内部）。日志的大小至少为 1024 个文件系统块（例如，如果使用 1kb 则为 1MB，使用 4ks 则为 4MB 等），且不能超过 10,240,000 个文件系统块或总文件大小的一半（以较者为准）。
    - `device=external-journal`：将文件系统挂载到位于 `external-journal` 的日志块设备。外部日志必须已使用 `mkefs -O journal external-journal` 命令创建。注意，`external-journal` 创建时使用的块大小必须与新文件系统相同。此外，支持将多个文件系统挂接到单个外部日志，但 Linux 内核和 `e2fsck(8)` 目前尚未共享外部日志。

`external-journal` 也可以通过 `LABEL=label` 或 `UUID=UUID` 指定，以便通过日志开始处 ext2 超数据块中存储的卷卷标或 UUID 来定位外部日志。使用 `dumpe2fs(8)` 显示设备的卷标和 UUID。另见 `tune2fs(8)` 的 `-L` 选项。

一个文件系统只能提供 `size` 或 `device` 选项中的一个。

`-l` 从文件名读取坏块列表。注意，坏块列表中的块号必须使用与 `m2fs` 相同的块大小生成。因此，`m2fs` 的 `-c` 选项是在格式前检查磁盘坏块的一种更简单且不易出错的方法，因为 `m2fs` 会自动为 `badblocks` 程序解析正确的参数。

`-L new-volume-label` 将文件系统的卷标设置为 `new-volume-label`。卷标的最大长度为 16 字节。

`-m` 设置 `reserved-blocks-percentage` 指定预留给超级用户的文件系统百分比。这可以避免碎片，并确保 root 拥有的守护进程（如 `syslog(8)`）在非特权进程被阻止写入文件系统后仍能正常运行。默认百分比为 5%。

`-M last-mounted-directory` 设置文件系统的挂载目录。这对于某些通过避开挂载目录来确定文件系统应该挂载在何处的工具可能有用。

`-n` 使 `m2fs` 不创建文件系统，而是显示如果创建将执行的操作。这可以用于确定特定文件系统的备份超数据块（superblock）的位置，前提是再次使用原始创建文件系统时传递的 `m2fs` 参数（当然，还要加上 `-n` 选项！）。

`-N number-of-inodes` 覆盖文件系统预留索引数量的默认计算（基于块数量和 `bytes-per-inode` 比例）。这允许用户指定所需的索引数量。

`-o creator-os` 覆盖文件系统“操作系统”特性的默认值。`creator` 字段由编译 `m2fs` 可执行文件时的目标操作系统名称设置。

`-O feature[...]` 使用给定的特征（文件系统选项）创建文件系统，覆盖默认选项。启用的特征由 `base_features` 关系设置，该关系可能位于 `/etc/m2fs.conf` 配置文件的 `[defaults]` 部分，也可能位于 `-T` 选项指定的用法页的 `[fs_types]` 子节中，并由文件系统和用例的 `[fs_types]` 节中发现的特征进一步修改。详情请参阅 `m2fs(5)` 手册。在 `[fs_types]` 节中找到的文件系统特定设置将覆盖 `[defaults]` 中的默认设置。

特征集由一组用逗号分隔的待启用特征组成。要禁用某个特征，只需在特征名称前加上插入符号（'^'）或减号（'-'）。特征“none”将清除所有特征。有关可设置的特征的更多详细信息，请参阅 `ext4` 手册页。

`-q` 静默退出。适用于 `m2fs` 在脚本中运行。

`-r revision` 设置新文件系统的版本。注意，2内核支持版本 0。默认创建版本 1。

`-S` 仅写入超数据块和组描述符。当超数据块和组位图损坏时非常有用。在使用此选项后应立即运行 `e2fsck` 程序并指定正确的块大小。

`-fstype` 指定要创建的文件系统类型（例如 ext2, ext3, ext4 等）。如果未指定此选项，`mk2fs` 将根据运行命令（例如使用 `mkfs.ext2`、`mkfs.ext3` 等名称）或 `/etc/mk2fs.conf` 文件定义的默认值来选择类型。

如果使用 `-O` 选项添加或删除新创建文件系统的文件系统选项，生成的文件系统可能不支持请求的 `fstype`（例如，“mk2fs -t ext3 -O extent /dev/sdXX”创建的文件系统不支持内核中的 ext3 实现；而“mkfs.ext3 -O ^journal /dev/hdXX”创建的文件系统没有日志，不支持内核中的 ext3 文件系统）。

`-T usage-type[...]` 指定文件系统的用途，以便 `mk2fs` 为该用途选择最优的文件系统参数。`/etc/mk2fs.conf` 中支持的用法类型。用户可以使用逗号列表指定一个或多个用法。如果未指定此选项，`mk2fs` 将根据要创建的文件系统的大小选择单一默认用法。如果文件系统大小小于或等于 3 MB，`mk2fs` 将使用 `floppy` 类型。如果文件系统大小大于 3 MB 且小于等于 512 MB，`mk2fs(8)` 将使用 `small` 类型。如果文件系统大小大于或等于 4 TB 且小于 16 TB，`mk2fs(8)` 将使用 `big` 类型。如果文件系统大小大于或等于 16 TB，`mk2fs(8)` 将使用 `huge` 类型。否则，`mk2fs(8)` 将使用默认类型 `default`。

`-U UUID` 使用指定的 UUID 创建文件系统。

`-v` 详细执行。

`-V` 打印 `mk2fs` 的版本并退出。

# 环境

## `MKE2FS_SYNC`

如果设置为非零整数值，则该值将用于确定在 inode 格初始化期间调用 `sync(2)` 的频率。

## `MKE2FS_CONFIG`

确定配置文件的位置（参见 `mke2fs.conf(5)`）。

## `MKE2FS_FIRST_META_BG`

如果设置为非零整数值，则该值将用于确定第一个元数据块组（meta block group）。
这主要用于调试。

## `MKE2FS_DEVICE_SESIZE`

如果设置为非零整数值，则该值将用于确定设备的物理扇区大小。

## `MKE2FS_SKIP_CHECK_MSG`

如果设置，则不显示由于挂载次数或检查间隔导致的文件系统自动检查的消息。

# way

此版本的 `mke2fs` 由 Theodore Ts’o <tytso@mit.edu> 编写。

# 缺陷

`mke2fs` 接受 `-f` 选项，但目前忽略了它，因为第二个扩展文件系统尚不支持碎片（fragments）。可能还有其他此类问题。请向作者报告。

# 可用性

`mke2fs` 是 e2fsprogs 包的组件，可以在 http://e2fsprogs.sourceforge.net 获取。

## 参见

`mke2fs.conf(5)`, `badblocks(8)`, `dumpe2fs(8)`, `e2fsck(8)`, `tune2fs(8)`, `ext4(5)`

# MKFS

### 名字

`mkfs` - 构建 Linux 文件系统

## 概要

```
mkfs [options] [-t type] [fs-options] device [size]
```

## 描述

`mkfs` 用于在设备（通常是硬盘分区）上构建 Linux 文件系统。`*device*` 参数可以是设备名称（例如 `/dev/hda1`, `/dev/sdb2`），也可以是包含该文件系统的普通文件。`*size*` 参数是用于文件系统的块分数。

`mkfs` 返回的退出码在成功时为 0，失败时为 1。

实际上，`mkfs` 仅仅是 Linux 下可用的各种文件系统构建器（`mkfs./type`）的前端。程序在查找特定于文件系统的构建器时，会在多个目录中进行，例如 `/sbin`, `/sbin/fs`, `/sbin/fs.d`, `/etc/fs` 等（精确列表在编译时定义，但至少包含 `/sbin` 和 `/sbin/fs`），最后在 `PATH` 环境变量列出的目录中查找。更多细节请参见特定构建器的手册页。

## 选项

`-t, --type` 指定要构建的文件系统类型。如果没有指定，则使用默认文件系统类型（当前为 ext2）。

`fs-options` 传递给实际文件系统构建器的特定系统选项。虽然不保证，但大多数文件系统构建器都支持以下选项。

`-V, --verbose` 生成详细输出，包括执行的所有特定于文件系统的命令。多次指定此选项将抑制任何特定文件系统命令的执行。这实际上对于测试非常有用。

`-V, --version` 显示版本信息并退出。（当 `-V` 是唯一参数时，它仅显示版本信息，否则它将作为 --verbose 运行。）

`-h, --help` 显示帮助并退出。

# 缺陷

所有通用选项必须位于特定文件系统选项之前，且不能与之合并。某些特定文件系统的程序不支持 `-V`（详细）选项，且不返回有意义的退出码。此外，某些特定文件系统的程序不会自动检测设备大小，并要求指定 `size` 参数。

## 作者

David Engel (`david@ods.com`) Fred N. van Kempen (`waltje@uwalt.nl.mugnet.org`) Ron Sommeling (`sommel@sci.kun.nl`) 本手册页页廉耻地改用了 Remy Card 针对 ext2 文件系统的版本。

## 参见

`fs(5)`, `badblocks(8)`, `fschk(8)`, `mkdosfs(8)`, `mke2fs(8)`, `mkfs.bfs(8)`, `mkfs.ext2(8)`, `mkfs.ext3(8)`, `mkfs.ext4(8)`, `mkfs.minix(8)`, `mkfs.msdos(8)`, `mkfs.vfat(8)`, `mkfs.xfs(8)`, `mkfs.xiafs(8)`

# 可用性

`mkfs` 命令是 util-linux 包的组成，可以在 `ftp://ftp.kernel.org/pub/linux/utils/util-linux/` 获取。

# MKFS.MINIX

### 名字

`mkfs.minix` - 创建 Minix 文件系统

## 概要

```
mkfs.minix [-c|-l filename] [-n length] [-i inodecount] [-v] device [size-in-blocks]
```

## 描述

`mkfs.minix` 在设备（通常是磁盘分区）上创建一个 MINIX 文件系统。设备通常如下形式：

- `/dev/hda1-8` (IDE 磁盘 1)
- `/dev/hdb1-8` (IDE 磁盘 2)
- `/dev/sda1-8` (SCSI 磁盘 1)
- `/dev/sdb1-8` (SCSI 磁盘 2)

`size-blocks` 参数是所需的文件系统大小，以块为单位。它仅为了向下兼容。如果忽略，大小将自动确定。仅允许大于 10 且小于 65536 的块数。

## 选项

`-c` 在创建文件系统之前检查设备的坏块。如果发现任何坏块，将打印计数。

`-n length` 指定文件系统的最大长度。允许的值只有 14 和 30。默认值为 30。

`-i inodecount` 指定文件系统的 inode 数量。

`-l filename` 从文件中读取坏块列表。

`-1` 创建 Minix 1 版本的文件系统。

`-2` 创建 Minix 2 版本的文件系统。

`-3` 创建 Minix 3 版本的文件系统。

# 退出码

`mkfs.minix` 返回的退出码之一如下：

- `0` 无错误
- `8` 操作错误
- `16` 语法错误

## 参见

`mkfs(8)`, `fsck(8)`, `reboot(8)`

# 可用性

`mkfs.minix` 命令是 util-linux 包的组件，可以在 `util-linux/` 处（同上）获取。

# MKFS.FAT

### 名字

`mkfs.fat` - 在 Linux 下创建 MS-DOS 文件系统

## 概要
```
