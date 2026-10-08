
## 描述

`cramfs` 文件系统上的文件每次对一页进行 `zlib` 压缩，允许随机读取访问。元数据不压缩，但采用一种简洁的表示方式呈现，比传统文件系统更节省空间。

该文件系统故意设计为只读以简化其设计；压缩文件的随机写访问很难实现。`cramfs` 附带了一个工具 (`mkramfs`)，用于将文件打包成新的 `cramfs` 镜像。

文件大小限制在 `16MB` 以下。

文件系统最大大小略小于 `272MB`。（文件系统上的最后一个文件必须在 `256MB` 块之前开始，但可以延伸到之外。）

# 参数

目录即我们想要生成压缩文件系统的目录树的根目录。

文件将包含 `cram` 文件系统，稍后可以挂载。

## 选项

- `-v` 启用详细输出。
- `-E` 将所有警告视为错误，并反映在命令返回值中。
- `-b blocksize` 使用定义的块大小，该大小必须是页大小的倍数。
- `-e edition` 在超级块中使用定义的文件系统版本号。
- `-N big, little, host` 使用定义的字节序。值默认为主机字节 (`host`)。
- `-i file` 将文件插入 `cramfs` 文件系统。
- `-n name` 设置 `cramfs` 文件系统的名称。
- `-p Pad` 按 `512` 字节对齐以启动代码。
- `-s` 此选项被忽略。最初的 `-s` 用于开启目录条目排序。
- `-z` 创建显式空洞。使用此选项需要 `2.3.39` 或更高版本的内核。
- `-V` 显示版本信息并退出。
- `-h` 显示帮助信息并退出。

## 退出状态

`0` 成功
`8` 操作错误，例如无法分配内存

# 另

`mount(8)`, `fsck.cramfs(8)`

# 可用性

示例命令是 `util-linux` 包的一部分，可从 Linux 内核存档中获取

# MKE2FS

## 名称
`mke2fs` - 创建 `ext2`/`ext3`/`ext4` 文件系统

## 语法

```
mke2fs [ -c ] [ -b block-size ] [ -D ] [ -f fragment-size ] [ -g blocks-per-group ] [ -G number-of-groups ] [ -i bytes-per-inode ] [ -I inode ] [ -j ] [ -J journal-options ] [ -N number-of-inodes ] [ -n ] [ -m reserved-blocks-percentage ] [ -o creator-os ] [ -O feature,... ] [ -q ] [ -r fs-revision-level ] [ -E extended-options ] [ -v ] [ -F ] [ -L volume-label ] [ -M last-mounted-directory ] [ -S ] [ -t fs-type ] [ -T usage-type ] [ -U UUID ] [ -V ] device [ blocks-count ]
```

```
mke2fs -O journal_dev [ -b block-size ] [ -L volume-label ] [ -n ] [ -q ] [ -v ] external-journal [ blocks-count ]
```

## 描述

`mke2fs` 用于创建 `ext2`、`ext3` 或 `ext4` 文件系统，通常在磁盘分区中创建。`device` 是对应设备的特殊文件（例如 `/dev/sda`），`blocks-count` 是设备上的块数。如果省略，`mke2fs` 会自动计算文件系统大小。如果用作 `mkfs.ext3` 调用，且指定了 `-j` 选项，则创建一个日志。新创建的文件系统的参数默认值如果未被下面的选项覆盖，将由 `/etc/mke2fs.conf` 文件控制。详见 `mke2fs.conf(5)`。

## 选项

- `-b block-size` 指定以字节为单位的块大小。有效的 `block-size` 值为每块 `1024`、`2048` 和 `4096` 字节。如果省略，`block-size` 将根据文件系统大小和对文件系统的预期用途通过启发式方法确定（见 `-T` 选项）。如果 `block-size` 前有负号（`'-'`），`mke2fs` 将使用启发式方法确定合适的块大小，条件是块大小至少是 `block-size` 的倍数。
- `-c` 在创建文件系统之前检查设备是否有坏块。如果指定了此选项，将使用较慢的读写测试代替快速只读测试。
- `-C cluster-size` 为使用 `bigalloc` 功能的文件系统指定以字节为单位的簇大小。有效的 `cluster-size` 值为 `2048` 到 `256M`。只有在启用 `bigalloc` 时才能指定此值。如果启用了 `bigalloc`，默认簇大小为块大小的 `16` 倍。
- `-D` 在写入磁盘时使用直接 I/O。这可以节省大量的缓冲区缓存内存，可能会影响运行在繁忙服务器上的其他应用程序。然而，此选项将使 `mke2fs` 运行慢得多，使用直接 I/O 是一种权衡。
- `-E extended-options` 为文件系统设置扩展选项。扩展选项用逗号分隔并可以使用等号（`'='`）带任何参数。`-E` 选项在早期 `mke2fs` 版本中使用 `-R`。为了向后兼容，仍然接受 `-R` 选项，但已弃用。支持的扩展选项如下：
  - `mmp_update_interval=interval` 调整初始 MMP 更新间隔（秒）。指定 `0` 使用默认间隔。指定的间隔必须小于 `300` 秒。需要启用 MMP 功能。
  - `stride=stride` 为具有步长的文件系统设置 `stride`。这是在移动到下一个磁盘之前读取或写入的块数，有时被称为块大小。这在单个磁盘上放置文件系统位图时会影响块分配器。
  - `stripe_width=stripe-width` 为具有带宽的文件系统设置带宽。这通常是 `stripe-size * N`，其中 `N` 是 RAID 中数据磁盘的数量（例如 RAID 5 有一个奇校验磁盘，因此 `N` 将是磁盘数减 `1`）。这允许块分配器在写入数据时尽可能避免对 RAID 带宽进行读改写。
  - `resize=max-online-resize` 保留足够的空间，以支持具有在线调整功能的文件组描述符。
  - `lazy_inode_init=<0 禁用, 1 启用>` 如果启用了 `uninit_bg` 功能，节点不会被 `mke2fs` 完全初始化。这会显著加快文件系统的初始化，但需要内核在首次挂载时在后台完成文件系统的初始化。如果省略选项值，默认为 `1` 以启用延迟清零。
  - `lazy_journal_init=<0 禁用, 1 启用>` 如果启用，节点日志不会被 `mke2fs` 完全清零。这会显著加快文件系统的初始化，如果系统在日志被完全覆盖之前崩溃存在微小风险。如果省略选项值，默认为 `1` 以启用延迟日志。
  - `discard` 在 `mkfs` 时尝试释放块（初始释放块对于固态设备和稀疏精制存储很有用）。当设备宣布释放也会清零数据时（释放后的任何读取都会返回零），将所有未清零的节点表标记为已清零。这大大加快了文件系统的初始化。这是默认。
  - `nodiscard` 不在 `mkfs` 时尝试释放块。
- `-f fragment-size` 指定以字节为单位的分块。
- `-F` 强制 `mke2fs` 创建文件系统，即使设备不是块设备上的分区，或者其他参数不合理。为了强制 `mke2fs` 在即使文件系统似乎在使用或已挂载的情况下创建文件系统（非常危险的操作），必须指定两次此选项。
- `-g blocks-per-group` 指定块组中的块数。用户通常没有设置此参数，因为默认值对文件系统是最优的。（对于在 RAID 阵列上创建文件系统的管理员来说，使用 `-E` 选项指定带 RAID 参数比操作每组块数要好。）此选项通常供开发测试用例的开发者。如果启用了 `bigalloc` 功能，则 `-g` 将指定块组中包含的簇数量。
- `-G number-of-groups` 指定在 `ext4` 文件系统中打包的块的数量以创建一个更大的虚拟块组（或 "`flex_bg`"）。这改进了元数据密集型工作负载的局域性（locality）和性能。块组的数量必须是 `2` 的幂，且只有在启用了 `flex_bg` 文件系统时才能指定。
- `-i bytes-per-inode` 指定每个 `inode` 的字节数。`mke2fs` 为磁盘上每 `bytes-per-inode` 字节的空间创建一个 `inode`。`bytes-per-inode` 比例越大，创建的 `inode` 越少。此值不应小于文件系统的块大小，否则创建的 `inode` 数量将超过限制。注意，文件系统创建后无法更改此比例，因此在决定该值时要小心。调整文件系统会更改 `inode` 的数量。
- `-I inode-size` 指定每个 `inode` 的大小。`inode-size` 值必须是 `2` 的幂或等于 `128`。`inode-size` 越大，`inode` 表消耗的空间越多，从而减少文件系统中的可用空间。文件系统创建后无法更改此值。在 `2.6.10` 及更早的内核中，可以使用比 `128` 字节更大的 `inode` 来存储扩展属性以提高性能。在旧内核中，大 `inode` 中的扩展属性不可见，且 `2.4` 内核将不支持此类文件。默认 `inode` 大小由 `mk2fs.conf` 文件控制（对于大多数系统为 `256` 字节，小系统除外）。
- `-j` 创建带有 `ext3` 日志的文件系统。如果未指定 `-J` 选项，将使用默认日志参数创建合适大小的日志（取决于文件系统的大小）存储在文件系统中。注意，你必须使用支持 `ext3` 的内核来实际使用日志。
- `-J journal-options` 使用命令行上指定的选项创建 `ext3` 日志。日志选项用逗号分隔，并可以使用等号（`'='`）带参数。支持以下日志选项：
  - `size=journal-size` 创建一个内部日志（即存储在文件系统内部），大小为 `journal-size` 兆字节。日志的大小至少为 `1024` 块（例如，使用 `1k` 块，`4MB` 使用 `4k` 块等），并且可能不超过 `240,000` 块或文件系统大小的一半（以较小者为准）。
  - `device=external` 将文件系统附加到位于外部的日志。日志可能已经使用与文件系统相同的块大小创建。此外，支持将多个文件系统附加到单个外部日志，Linux 内核和 `efsck(8)` 目前尚未共享外部日志。
  - 与其指定设备名称，也可以通过 `LABEL=label` 或 `UUID=UUID` 通过 `ext2` 超头存储的卷标签或 UUID 来指定外部日志。使用 `dumpe2fs(8)` 显示日志设备的卷标签和 UUID。另见 `tune2fs(8)` 的 `-L` 选项。
  - 文件系统只能给出 `size` 或 `device` 选项之一。
- `-l filename` 从文件名读取坏块列表。注意，块列表中的块号必须使用与 `mke2fs` 相同的块大小生成。因此，`mke2fs` 的 `-c` 选项是格式化之前检查坏块更简单不易出错的方法，`mke2fs` 会将正确的参数传递给 `badblocks` 程序。
- `-L new-volume-label` 设置文件系统的卷标签为 `new-volume-label`。卷标签的最大长度为 `16` 字节。
- `-m reserved-blocks-percentage` 设置为超级用户保留的文件系统块百分比。这避免了碎片，并允许 `root` 所有的守护进程（如 `syslog(8)`）在非特权进程写入文件系统后继续正常运行。默认百分比为 `5%`。
- `-M last-mounted-directory` 设置文件系统的挂载目录。这对于某些保持挂载目录可能有用，确定文件系统应该挂载在哪里。
- `-n` 使 `mke2fs` 不创建文件系统，而是显示如果创建它将会做什么。这可以确定特定文件系统备份超头的位置，只要再次使用最初创建文件系统时传递的 `mke2fs` 参数（在加上 `-n` 选项的情况下！）。
- `-N number-of-inodes` 覆盖文件系统保留 `inode` 数量的计算（基于块数量和 `bytes-per-inode` 比例）。这允许用户指定所需的 `inode` 数量。
- `-o creator-os` 覆盖文件系统“操作系统”字段的默认值。`creator` 字段默认设置为用于编译的 `mke2fs` 可执行文件名称。
- `-O feature[...]` 使用给定的特征（文件系统选项）创建文件系统，覆盖默认特征。默认启用的特征由 `base_features` 关系设置，该关系位于 `/etc/m2fs.conf` 配置文件的 `[defaults]` 节中，或由 `T` 选项指定的用例 `[fs_types]` 子节中，进一步修改文件系统和用例 `[fs_types]` 子节中的特征。更多细节请参 `mke2fs(5)` 手册。`[fs_types]` 节中的文件系统类型特定设置将覆盖 `[defaults]` 中的全局默认值。
- 文件系统特征将使用此选项指定的特征进行进一步编辑；如果没有给出此选项，则使用正在创建的文件系统类型的 `default_features` 关系或配置文件中的 `[defaults]` 节。
- 文件系统特征由一组用逗号分隔的可启用特征列表组成。要禁用某项特征，只需在名称前加脱字符（`^`）或减号（`-'`）。具有依赖关系的特征将无法成功删除。伪文件系统特征“`none`”将清除所有文件系统特征。
- 有关可以设置的特征的更多信息，请参 `ext4(5)` 手册。
- `-q` 静默执行。当 `mke2fs` 在脚本中运行时非常有用。
- `-r revision` 设置新文件系统的修订版本。注意，`1` 内核仅支持 `0` 版本的文件系统。默认创建版本为 `1` 的文件系统。
- `-S` 仅写入超头和组描述符。这在超头和组描述符损坏且需要恢复时非常有用。它会导致 `mke2fs` 不初始化 `inode` 表和块位图。在使用此选项后应立即运行 `efsck` 程序，且不保证数据可以挽救。
- `-fs-type` 指定要创建的文件系统类型（例如 `ext2`, `ext3`, `ext4` 等）。如果未指定此选项，`mke2fs` 将根据运行方式（例如使用 `mk2fs.ext2`、`mk2fs.ext3` 等名称）或通过 `/etc/mk2fs.conf` 定义的默认值来选择。这控制了默认使用的文件系统选项。
- 如果使用 `-O` 选项添加或删除文件系统选项，新创建的文件系统可能不支持请求的 `fs-type`（例如，“`mk2fs -t ext3 -O extent /dev/sdXX` 将创建一个被 Linux 内核 `ext3` 实现不支持的文件系统；而 `mk2fs-ext3 -O ^journal /dev/hdXX` 将创建一个不带日志的文件系统）。
- `-T usage-type[...]` 指定文件系统的用途，以便 `mke2fs` 为该用途选择最优的文件系统参数。支持的用例定义在配置文件 `/etc/mk2fs.conf` 中。用户可以使用逗号分隔列表指定一个或多个用例。
- 如果未指定此选项，`mke2fs` 将根据要创建的文件系统的大小选择单一默认用例。如果文件大小小于或等于 `3 MB`，`mke2fs` 将使用 `floppy` 文件系统类型。如果文件大小大于 `3 MB` 且小于等于 `512 MB`，`mke2fs(8)` 将使用 `small` 文件系统类型。如果文件大小大于或等于 `4 TB` 但小于 `16 TB`，`mke2fs(8)` 将使用 `big` 文件系统类型。如果文件大小大于等于 `16 TB`，`mke2fs(8)` 将使用 `huge` 文件系统类型。否则，`mke2fs(8)` 将使用默认文件系统类型 `default`。
- `-U` 使用指定的 UUID 创建文件系统。
- `-v` 详细执行。
- `-V` 打印 `mk2fs` 的版本号并退出。

# 环境

## `MKE2FS_SYNC`

如果设置为非零整数值，其值将用于确定在初始化 `inode` 表格期间调用 `sync(2)` 的频率。

## `MKE2FS_CONFIG`

确定配置文件的位置（参见 `mke2fs.conf(5)`）。

## `MKE2FS_FIRST_META_BG`

如果设置为非零整数值，其值将用于确定第一个元数据块组（`meta block group`）。
这主要用于调试目的。

## `MKE2FS_DEVICE_SESIZE`

如果设置为非零整数值，其值将用于确定设备的物理扇区大小。

## `MKE2FS_SKIP_CHECK_MSG`

如果设置，则显示因挂载次数或检查间隔引起的文件系统自动检查的消息。

## 作者

此版本的 `mke2fs` 由 Theodore Ts’o <`tytso@mit.edu`> 编写。

# 缺陷

`mke2fs` 接受 `-f` 选项，但目前忽略了它，因为第二个扩展文件系统尚未支持碎片（`fragments`）。可能存在其他缺陷。请向作者报告。

# 可用性

`mke2fs` 是 `e2fsprogs` 软件包的一部分，可以从 `http://e2fsprogs.sourceforge.net` 获取。

## 参见

`mke2fs.conf(5)`, `badblocks(8)`, `dumpe2fs(8)`, `e2fsck(8)`, `tune2fs(8)`, `ext4(5)`

# MKE2FS

> 名称

`mke2fs` - 创建 `ext2`/`ext3`/`ext4` 文件系统

## 概要

```
mke2fs [-c] [ -b block-size ] [ -D ] [ -f fragment-size ] [ -g blocks-per-group ] [ -G number-of-groups ] [ -i bytes-per-inode ] [ -I inode ] [ -j ] [ -J journal-options ] [ -N number-of-inodes ] [ -n ] [ -m reserved-blocks-percentage ] [ -o creator-os ] [ -O feature,... ] [ -q ] [ -r fs-revision-level ] [ -E extended-options ] [ -v ] [ -F ] [ -L volume-label ] [ -M last-mounted-directory ] [ -S ] [ -t fs-type ] [ -T usage-type ] [ -U UUID ] [ -V ] device [ blocks-count ]
```

```
mke2fs -O journal_dev [ -b block-size ] [ -L volume-label ] [ -n ] [ -q ] [ -v ] external-journal [ blocks-count ]
```
