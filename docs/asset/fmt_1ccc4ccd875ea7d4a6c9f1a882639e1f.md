
`fat={12|16|32}` 指定 12、16 或 32 位。这将覆盖自动 FAT 类型检测。请谨慎使用！

`charset=value` 用于转换 8 位字符和 16 位 Unicode 的字符集。默认是 `utf8859-1`。长文件名以 Unicode 格式存储。

`Nfs` 如果设置，将启用目录项的内存索引，以减少 NFS 客户端操作中 `EXTALE` 错误的范围。仅在文件系统通过 NTFS 导出时使用。

`UTC` 此选项禁用从本地时间（Windows 在 FAT 上使用）到 UTC（Linux 内部使用）的时间戳转换。这在挂载设置为 UTC 的设备（如数字相机）时特别有用，可以避免本地时间的陷阱。

`Quiet` 开启静默标志。尝试检查子文件会返回错误，尽管它们会失败。请谨慎使用！

`showexec` 如果设置，只有当文件的扩展部分为 `.EXE`、`.COM` 或 `.BAT` 时，才允许文件的执行权限位。默认关闭。

`FAT` 上的 `sysATTR_SYS` 属性被处理为 Linux `IMMUTABLE`（不可变）标志。默认关闭。

如果设置，文件系统将尝试比通常频繁地刷新磁盘。默认关闭。

`usefree` `FSINFO` 的“空闲簇”视图。它将用于确定空闲簇的数量。对于 Rock Ridge 无意义。

如果文件长度的高字节包含其他垃圾数据，设置此挂载选项以忽略文件长度的高位位。这意味着文件不能大于 16MB。

```
session=x
```

在多会话 CD 上选择会话数量。（自 2.3.4 版本起）

```
sbsector=xxx
```

Session 从扇区 `xxx` 开始。（自 2.3.4 版本起）

以下选项与 `vfat` 相同，只有在使用使用微软 Joliet 扩展进行编码的光盘时，指定这些选项才有意义。

```
iocharset=value
```

用于将 CD 上的 16 位 Unicode 字符转换为 8 位字符的字符集。默认值为 `iso8859-1`。

```
utf8
```

将 CD 上的 16 位 Unicode 字符转换为 UTF-8。

# JFS 挂载选项

`iocharset=name`

用于从 Unicode 转换为 ASCII 的字符集。默认不进行转换。使用 `charset=utf8` 进行 UTF8 翻译。这需要在内核内核的 `.config` 文件中设置 `CONFIG_NLS_UTF8`。

`resize=value`

将卷调整大小为块。JFS 只支持扩展卷，不支持缩小卷。此选项仅在以读写模式挂载卷的重新挂载期间有效。`resize` 若不带值，将卷扩展到整个分区的大小。

`nointegrity`

不写入日志。此选项的主要用途是允许在从备份介质恢复卷时获得更高的性能。如果系统异常结束，则无法保证卷的完整性。

`integrity`

默认值。将元数据更改提交到日志。使用此选项重新挂载之前指定了 `nointegrity` 选项的卷，以恢复正常行为。

`errors={continue|ro|panic}`

定义遇到错误时的行为。（忽略错误并仅标记文件系统为错误并继续，或将文件系统重新挂载为只读，或发生恐慌并停止系统。）

`noquota|quota|usrquota|grpquota`

这些选项会被接受但忽略。

# MINIX 挂载选项

无。

# MSDOS 挂载选项

参见 `fat` 的挂载选项。如果 `msdos` 文件系统检测到不一致，它会报告错误并将文件系统设置为只读。可以通过重新挂载使文件系统恢复为可写。

# NCPFS 挂载选项

与 `nfs` 一样，`ncpfs` 实现向 `mount` 系统调用期望一个二进制参数（`struct nfs_mount_data`）。该参数由 `mount(8)` 构建，而当前版本的 `mount` (2.1) 不知道 `ncpfs` 的信息。

# NFS 和 NFS4 挂载选项

参见 `nfs(5)` 手页的选项部分（必须安装 `nfs-utils` 包）。`nfs` 和 `nfs4` 实现向 `mount` 系统调用期望一个二进制参数（`struct nfs_mount_data`）。该参数由 `mount(8)` 构建，而当前版本的 `mount` (2.1) 不知道 `nfs` 和 `nfs4` 的信息。

# NTFS 挂载选项

`iocharset=name`

返回文件名时使用的字符集。与 VFAT 不同，NTFS 会抑制包含不可读字符的名称。已废用。

`nls=name`

早名为 `iocharset` 的选项的新名称。

`utf8`

使用 UTF-8 转换文件名。

`uni_xlate=[0|1|2]`

对于 0（或 'no' 或 'false'），对未知字符不使用转义序列。对于 1（或 'yes' 或 'true'）或 2，使用以 "." 开头的 `vfat` 式四字节转义序列。

`posix=[0|1]`

如果启用（`posix=1`），文件系统将区分大小写名称，并以硬链接形式呈现而非抑制。

`uid=value`, `gid=value` and `umask=value`

设置文件系统上的文件权限。默认以八进制形式给出文件。由 root 拥有，其他人不可读。

# PROC 挂载选项

```
uid=value and gid=value
```

这些选项被识别，但据我所知它们没有影响。

# RAMFS 挂载选项

`Ramfs` 是一个基于内存的文件系统。挂载它就拥有它。卸载它就消失了。自 Linux 2.3.9 起存在。没有挂载选项。

# REISERFS 挂载选项

`Reiserfs` 是一个日志文件系统。指示 3.6 版本的 `reiserfs` 软件挂载 3.5 版本的系统系统，使用 3.6 格式处理新创建的对象。该文件系统将不再与 `reiserfs` 工具兼容。

`hash={reiserfs|r5|detect}`

选择 `reiserfs` 使用何种哈希函数在目录内查找文件。

由 Yuki Yu 发明的 `reiserfs` 哈希函数。它速度快且保留局部性，将字典顺序上接近的文件名映射到接近的哈希值。不应使用此选项，因为它会导致高概率的冲突。

由 Jeremy Fitzhardinge 实现的 Davis-Meyer 文件系统。它使用哈希排列名称中的位。它具有高随机性，因此在某些 CPU 开销下具有低哈希冲突概率。如果在使用 `r5` 哈希时遇到 `HASHISION` 错误，可以使用此项。

修改后的 `reiserfs` 哈希。默认使用它，除非文件系统具有巨大的目录和异常的文件名模式，否则最佳选择。

通过检查正在挂载的文件系统来检测使用的是何种哈希函数，并将此信息写入 `reiserfs` 超数据块（`superblock`）。这仅在首次挂载旧文件系统时有用。

`hashed_relocation` 调整块分配器。这在某些情况下可能提供性能改进。

`no_unhashed_relocation` 调整块分配器。这在某些情况下可能提供性能改进。

`noborder` 禁用 Yuki Yu 发明的边界算法。这在某些情况下可能提供性能改进，但代价是失去 `reiserfs` 从崩溃中恢复的能力。开启此选项时，`reiserfs` 执行所有的日志操作，写入其日志区域的除外。`nolog` 的实现正在进行中。

`notail` 默认情况下，`reiserfs` 将小文件和“文件尾部”（`file tails`）直接存储在树中。

`replay` 使用 `reiserfsck` 重放日志中的事务。

`resize=number` 重新挂载选项，允许分区在线扩展。用于逻辑卷管理（LVM）。`user_xattr` 扩展属性。`attr(5)` 手页。

`enable` POSIX 访问控制列表。`acl(5)` 手页。

`barrier=none/flush` 启用或禁用日志代码中的写入屏障，以强制磁盘提交的正确顺序。`reiserfs` 文件系统默认不启用屏障。除非你的磁盘有电池保护，否则掉电时会导致文件系统损坏。

# ROMFS 挂载选项

无。

# QUASHFS 挂载选项

无。

# SMBFS 挂载选项

与 `nfs` 一样，`smbfs` 实现向 `mount` 系统调用期望一个二进制参数（`struct smb_mount_data`）。该参数由 `smount(8)` 构建，而当前版本的 `mount` (2.1) 不知道 `smbfs` 的信息。

# SYSV 挂载选项

无。

# TMPFS 挂载选项

`size=nbytes` 覆盖文件系统的默认大小。大小以字节给出，并向上对齐到整页。默认是内存的一半。当未指定 `size` 或 `nr_blocks` 时，`size` 参数也接受后缀 `%` 以将此 `tmpfs` 实例限制为物理内存的百分比：默认为 `size=50`

`nr_blocks=` 与 `size` 相同，但单位是 `PAGE_CACHE_SIZE`

`nr_inodes=` 该实例的最大 inode 数量。默认是物理内存页数，或（在具有高内存的机器上）低内存页数，取两者较小者。

`tmpfs` 尺寸挂载选项（`size`, `nr_blocks` 和 `nr_inodes`）接受后缀 `k`, `m` 或 `g`（对应二进制单位 klo, mega 和 giga），并可以在重新挂载时更改。

`mode=` 设置根目录的初始权限。

`uid=` 用户 ID。

`gid=` 组 ID。

`mpol=[default[prefer:Node|bind:NodeList|interleave|interleave:NodeList]]` 为该实例中的所有文件设置 NUMA 内存分配策略（如果内核启用了 `CONFIG_NUMA`）——动态调整：`mount remount ...`

`default` 优先从本地节点分配内存

`prefer:Node` 优先从给定的 Node 分配内存

`bind:NodeList` 仅从 NodeList 中的节点分配内存

`interleave` 交替从每个节点分配

`interleave:NodeList` 交替从 NodeList 中的每个节点分配

`NodeList` 格式为逗号分隔的数字和范围列表，范围是两个由连字符分隔的数字，表示范围内最小和最大的节点编号。例如，`mpol=bind:0-3,5,7-95`

因此，建议从自动挂载选项中省略 `mpol` 选项。当 `tmpfs` 已经挂载到 `MountPoint` 时，可以通过 `mount -o remount,mpol=Policy:NodeList MountPoint` 将其添加。

# UBIFS 挂载选项

`UBIFS` 是一种运行在 `UBI` 卷之上的闪存文件系统。注意，不支持 `atime` 且始终处于关闭状态。设备名称可以指定为：

- `ubiX_Y`：设备号 X，卷号 Y
- `ubiY`：设备号 0，卷号 Y
- `ubiX:NAME`：设备号 X，名为 NAME 的卷
- `ubi:NAME`：设备号 0，名为 NAME 的卷

可以使用替代的分隔符 `!` 代替 `:`。以下是可用的挂载选项：

- `bulk_read`: 启用批量读取。禁用 VFS 预读，因为会减慢文件系统。批量读取是一种内部优化。如果数据位于一个 0 而不是分散在多个读取请求中，某些闪存的读取可能会更快。例如，OneNand 在读取超过一个 NAND 页时会执行“边读边加载”。
- `no_bulk_read`: 不进行批量读取。这是默认值。
- `chk_data_crc`: 检查数据 CRC-32 校验和。这是默认值。
- `no_chk_data_crc`: 不检查 CRC-32 校验和。使用此选项时，文件系统在读取时不检查 CRC-32，但会在内部索引信息上进行检查。此选项仅影响读取，不影响写入。写入数据时始终会计算 CRC-32。
- `compr={none|lzo|zlib}`: 选择在写入新文件时使用的默认压缩器。如果使用 `none` 选项挂载，仍然可以读取压缩文件。

# UDF 挂载选项

`udf` 是由光存储技术协会定义的“通用磁盘格式”文件系统，通常用于 DVD-ROM。另请参考 `iso9660`。

- `gid=`: 设置默认组。
- `umask=`: 设置默认 umask。值为八进制表示。
- `uid=`: 设置默认用户。
- `hide=`: 显示原本隐藏的文件。
- `ndelete`: 在列表中显示已删除的文件。
- `nostrict`: 取消严格一致性。
- `iocharset`: 设置 NLS 字符集。
- `bs=`: 设置块大小。（除非为 2048，否则可能无效）。
- `novrs`: 跳过卷序列识别。
- `session=`: 设置 CDROM 会话从 0 开始计数。默认值：最后一个会话。
- `anchor=`: 覆盖标准的锚点位置。默认值：256。
- `volume=`: 覆盖 VolumeDesc 的位置。（未使用）。
- `partition=`: 覆盖 PartitionDesc 的位置。（未使用）。
- `lastblock=`: 设置文件系统的最后一个块。
- `fileset=`: 覆盖 fileset 块位置。（未使用）。
- `rootdir=`: 覆盖根目录位置。（未使用）。

# UFS 挂载选项

`ufstype=value`

`UFS` 是一种广泛用于不同操作系统的文件系统。问题在于不同实现之间的差异。某些实现实现的功能没有文档说明，因此很难通过挂载选项识别 `ufs` 的类型。这就是为什么用户必须通过挂载选项指定 `ufs` 的类型。可能的值有：

- `old`: `ufs` 的旧格式，这是默认值，只读。（不要忘记提供 `-r` 选项。）
- `44bsd`: 用于由类 BSD 系统（NetBSD, FreeBSD, OpenBSD）创建的文件系统。
- `ufs2`: 用于 FreeBSD 5.x，支持读读写。
- `5xbsd`: `ufs2` 的别名。
- `sun`: 用于在 Sparc 上由 SunOS 或 Solaris 创建的文件系统。
- `sunx86`: 用于在 x86 上由 Solaris 创建的文件系统。
- `hp`: 用于 HP-UX 创建的文件系统，只读。
- `nextstep`: 用于由 NeXTStep（在 NeXT 工作站上）创建的文件系统（目前为只读）。
- `nextstep-cd`: 用于 NextStep CDROM（`block_size == 2048`），只读。
- `openstep`: 用于 OpenStep 创建的文件系统（目前为只读）。Mac OS X 也使用相同的文件系统类型。
- `onerror=value`: 设置发生错误时的行为。
- `panic`: 如果遇到错误，导致内核恐慌（`kernel panic`）。
- `[lock|umount|repair]`: 这些挂载选项目前不起作用；当遇到错误时，会在控制台打印消息。

# UMSDOS 挂载选项

请参考 `msdos` 的挂载选项。`dotsOK` 选项会被 `umsdos` 显式禁用。

# VFAT 挂载选项

首先，`fat` 的挂载选项会被识别。`dotsOK` 选项会被 `vfat` 显式禁用。此外还有

- `uni_xlate`: 将未处理的 Unicode 字符翻译为特殊的转义序列。这允许你备份和恢复用 Unicode 字符创建的文件名。如果没有此选项，在可以翻译时将使用 '?'。转义字符是 ':'；因为否则在 `vfat` 文件系统上是非合法的。使用的转义序列（其中 u 是 Unicode 字符）为：':', `(u & 0x3f), ((u>>6) & 0x3f), (u>>12)`。
- `posix`: 允许两个文件名大小不同的文件。此选项已过时。
- `nonumalt`: 在尝试 `name~name.ext` 之前，先尝试创建一个没有序列的短名称。
- `utf8`: UTF8 是控制台使用的 Unicode 文件系统 8 位编码。可以通过此选项为文件系统启用它。
- `shortname={lower|win95|mixed}`: 定义了符合 8.3 字符的文件名在创建和显示时的行为。如果启用 `utf8`，有四种模式：
    - `lower`: 强制短名称为小写，存储时短文件名不为大写。
    - `win95`: 强制短名称为大写，存储时短文件名不为大写。
    - `mixed`: 以原始方式显示，存储时短文件名不为大写。从 2.6.32 起即为默认值。

# USBFS 挂载选项

- `devuid=devgid=devmode=`: 定义新创建的文件获取的组 ID。当设置了 `devgid` 时，它获取所在目录的组 ID；否则它获取当前进程的 fgid，除非目录设置了 setgid 位。
- `busuid=busgid=busmode=`: 设置文件系统中 bus 目录的所有者、组和模式（默认值：`uid=0, mode=0644`）。
- `listuid=listgid=listmode=`: 设置 list 设备的所有者、组和模式（默认值：`uid=0, mode=0555`）。

# XENIX 挂载选项

无。

# XFS 挂载选项

- `allocsize=size`: 在进行延迟分配时设置缓冲 I/O 的尾文件预分配大小。此选项的有效值为页大小（通常为 4KiB）到 1GiB，按 2 的幂增加。默认行为是动态尾文件预分配大小，它根据文件内部模式使用启发式方法优化预分配大小。
- `attr2|noattr`: 这些选项启用/禁用对内联扩展属性存储方式的一种改进。当选择 `attr2` 时（在设置或删除扩展属性时）首次使用新格式，磁盘特性字段将更新以反映使用该格式。默认行为由磁盘特性指示 `attr2` 行为是否激活决定。如果设置了任何一个挂载选项，它将成为文件系统的新默认。启用 CRC 的文件系统始终使用 `attr2` ，因此将拒绝 `noattr` 挂载选项。
- `barrier|nobabler`: 启用/禁用用于日志和数据完整性操作的块层写入屏障。这允许支持写入屏障的设备驱动级缓存。
- `discard|nodiscard`: 向块设备发送命令以回收文件系统释放的空间。这对于 SSD 设备、精简的 LUN 和虚拟机镜像有用，可能会对性能产生。注意：目前建议使用 `fstrim` 应用程序通过 `discard` 挂载选项删除不需要的块，因为该选项对性能影响非常严重。
- `filestreams`: 让数据分配器在整个文件系统使用 filestreams 分配模式，而不仅仅是配置它的目录。当指定了 `keepib` 时，XFS 不删除空 簇并保留它们 ...磁盘。当未指定 `noed` 时，会将空 inode 簇返回到空闲空间。

## `inode32|inode64`

当指定 `inode32` 时，表示 XFS 将 inode 的创建限制在不会导致 inode 号的有效位 超过 32 位的位置。

当指定 `inode64` 时，表示 XFS 允许在文件系统的任何位置创建 inode，包括那些会导致 inode 号占用超过 32 位有效位的位置。
