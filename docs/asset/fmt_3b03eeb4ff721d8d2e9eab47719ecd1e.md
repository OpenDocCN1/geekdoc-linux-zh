
`dev` 解析文件系统上的字符或块特殊设备。`nodev` 不要解析文件系统上的字符或块特殊设备。`diratime` 更新此文件系统上的目录访问时间。这是 `nodiratime` 不在此文件系统上更新 inode 访问时间。`dirsync` 文件系统内的所有更新都应同步进行。这允许 `create`, `link`, `unlink`, `symlink`, `mkdir`, `rmdir`, `rename` 和 `rename`。`exec` 允许执行二进制文件。`noexec` 不允许在挂载的文件系统上直接执行二进制文件。（直到最近，还可以使用命令如 `/lib/ld.so` `/mnt/` 来运行二进制文件）。`group` 允许普通用户（即非 root）挂载文件系统，如果其所属的某个组与设备匹配。这包括 `nosuid` 和 `node`（除非被后续选项覆盖，如选项行中的 `version` 每次修改 inode 时，`noatime` 不在此文件系统上更新 inode 访问时间。`nosuid` 不允许设置用户标识位。`nodev` 不允许设置用户标识位。`_netdev` 该文件系统位于网络上。`nofail` 如果设备不存在则不报告错误。`relatime` 更新 inode 访问时间。`sync` 到文件系统的所有 I/O 都应同步进行。

建议的格式为 `x-<appname>.<option>`（例如 `x-systemd.automount`）。`x-mount.mkdir[<mode>]` 允许创建一个目标目录（挂载点）。可选参数 `<mode>` 指定了以八进制表示的用于 `mkdir(2)` 的文件系统访问模式。默认模式为 0755。此功能仅支持 root 用户。

# 特定于文件系统的挂载选项

以下选项仅适用于某些文件系统。我们按照文件系统对其进行排序。

它们都遵循 `-o` 标志。

支持哪些选项取决于运行的内核。更多信息可以在内核源码子目录 `Documentation/filesystems` 中找到。

# ADFS 的挂载选项

`uid=value` 和 `gid=value`

设置文件系统中文件的所有者和组（默认：`uid=gid=0`）。

`ownmask=value` 和 `othmask=value`

分别为 ADFS 的“所有者”权限和“其他”权限设置权限掩码（默认分别为 0700 和 0077）。另请参见 `/usr/src/linux/Documentation/filesystems/adfs.txt`。

# AFFS 的挂载选项

`uid=value` 和 `gid=value`

设置文件系统根的所有者和组（默认：`uid=gid=0`，但如果使用了未指定具体值的 uid 或 gid 选项，则采用当前进程的 uid 和 gid）。

`setuid=value` 和 `setgid=value`

设置所有文件的所有者和组。

`mode=value`

将所有文件的所有者设置为 `value & 0777`，忽略原始权限。为具有读取权限的目录添加搜索权限。该值以八进制给出。

`protect`

不允许允许对文件系统上的保护位进行任何更改。

`usemp`

在第一次同步或卸载时，将文件系统根的 uid 和 gid 设置为挂载点的 uid 和 gid，然后清除此选项。很奇怪……

`verbose`

为每次成功挂载打印一条信息消息。

`prefix=string`

在跟随链接时，在卷名之前使用的前缀。

`volume=string`

在跟随符号链接时，在 '/' 之前使用的前缀（长度最多 30）。

`reserved=value`

（默认：2。）设备开头未使用的块块数。

`root=value`

显式指定根块的位置。

`bs=value`

指定块大小。允许的值为 512, 1024, 2048, 4096。

`grpquota|noquota|quota|usrquota`

这些选项会被接受但被忽略。（然而，quota 工具可能会对 `/etc/fstab` 中的字符串做出反应）。

# CIFS 的挂载选项

请参见 `mount.cifs(8)` 手页的选项部分（必须安装 cifs-utils 包）。

# COHERENT 的挂载选项

无。

# DEBUFS 的挂载选项

`debugfs` 文件系统是一个伪文件系统，传统挂载在 `/sys/kernel/debug`。从内核版本 3.4 开始，`debugfs` 具有以下选项：

`uid=n`, `gid=n`

设置挂载点的所有者和组。

`mode=value`

设置挂载点的模式。

# DEVPTS 的挂载选项

`devpts` 文件系统是一个伪终端，传统挂载在 `/dev/pts`。为了获取伪终端，进程打开 `/dev/ptmx`；随后伪终端的编号将提供给该进程，伪终端从可以通过 `/dev/pts/<number>` 访问。

这会将新创建的 PTY 的所有者或组设置为指定值。如果未指定，它们将设置为创建进程的 UID 和 GID。例如，如果有一个设备为 5 的 tty 组，`gid=5` 将导致新创建的 PTY 属于 tty 组。

将新创建的 PTY 的模式设置为指定值。默认为 0600。`mode=620` 和 `gid=5` 的值使得 "mesgy" 成为新创建 PTY 上的默认值。

创建一个 `devpts` 文件系统的私有实例，使得在此新实例中分配的 pty 索引独立于 `devpts` 其他实例中创建的索引。

所有不带此 `newinstance` 选项的 `devpts` 挂载都共享同一组 pty 索引（即旧模式）。每个带有 `newinstance` 选项的 `devpts` 挂载都有私有的 pty 索引集。

此选项主要用于支持 Linux 内核中的容器。它从 2.6.29 版本的 Linux 内核开始实现。此外，只有在内核配置中启用了 `CONFIG_DEVPTS_MULTIPLE_INSTANCES`，此选项才有效。

要有效使用此选项，`/dev/ptmx` 必须是指向 `pts/ptmx` 的符号链接。详情请参见 Linux 内源码中的 `Documentation/filesystems/devpts.txt`。

为 `devpts` 文件系统中新的 `ptmx` 设备设置模式。

为了兼容旧内核，`newinstance` 选项在从 2.6.29 开始的 Linux 内核版本中不再实现。此外，只有在内核配置中启用了 `CONFIG_DEVPTS_MULTIPLE_INSTANCES`，此选项才有效。

此选项主要用于支持 Linux 内核中的容器。它从 2.6.29 版本的 Linux 内核开始实现。此外，只有在内核配置中启用了 `CONFIG_DEVPTS_MULTIPLE_INSTANCES`，此选项才有效。

# EXT 的挂载选项

无。注意，`ext4` 不支持，但 `mfs2fs(8)` 支持。

# EXT2 的挂载选项

`ext2` 文件系统预留了可用空间的百分比（默认为 5%，见 `mke2fs(8)` 和 `tune2fs(8)`）。这些选项决定了谁可以使用预留块。（大致：具有指定 uid 或属于指定组的用户。）

# EXT3 的挂载选项

`ext3` 文件系统是日志文件系统。默认启用日志（见 `mke2fs(8)` 和 `tune2fs(8)`）。

# EXT4 的挂载选项

`ext4` 文件系统是大多数现代 Linux 发行版的默认选择。它支持许多功能，如 extents 和延迟分配（见 `mke2fs(8)` 和 `tune2fs(8)`）。

# EXT3 挂载选项

`ext3` 文件系统是 `ext2` 文件系统的一个版本，增加了日志（journaling）功能。它支持 `ext2` 的所有选项，以及以下新增选项：

- `journal=update`

将 `ext3` 文件系统的日志更新为当前格式。

- `journal=inum`

当日志已存在时，此选项将被忽略。否则，它指定了代表 `ext3` 文件系统日志文件的 inode 编号；`ext3` 将创建一个新日志，并覆盖编号为 `inum` 的文件的旧内容。

- `journal_dev=devnum`

当外部日志设备的主设备号/次设备号发生变化时，此选项允许用户指定新的日志位置。日志设备通过其编码在 `devnum` 中的新主设备/次设备号来识别。

- `norecovery=noload`

挂载时不加载日志。请注意，如果文件系统不是以干净的方式卸载的，跳过日志重放（replay）将导致文件系统包含不一致的内容，从而引发各种问题。

- `data={journal=ordered|writeback}`

指定文件数据的日志模式。元数据记录日志。若要在根文件系统上除 `ordered` 以外的模式，请将该模式传递给内核，例如 `rootflags=data=journal`。

- `journal`

所有数据在写入主文件系统之前都会提交到日志中。

- `ordered`

这是默认模式。在元数据提交到日志之前，所有数据都会被强制直接写入主文件系统。

- `writeback`

不保留数据顺序 - 数据可能在元数据提交到日志后才写入主文件系统。据传这是吞吐量最高的选项。尽管，它保证了文件系统内部的完整性，但可能允许在崩溃和日志恢复后，文件中出现旧数据。

- `barrier=0` / `barrier=1`

启用/禁用屏障（barriers）。`barrier=0` 禁用，`barrier=1` 启用。写屏障强制日志提交在磁盘上的排序，使得易性写缓存可以安全使用，但会有一定的性能损失。`ext3` 文件系统默认不启用屏障。除非你的磁盘带有电池备份或其他，否则请务必启用屏障，以免在断电时导致文件系统损坏。

- `commit=nsec`

每隔 `nsec` 秒同步一次数据和元数据。默认值为 5 秒。设置为 0 则不默认同步数据。

- `user_attr`

扩展属性。详见 `attr(5)` 手册页。

- `acl`

启用 POSIX 控制列表。详见 `usrquota=aquota.user/grpjquota=aquota.group/jqfmnt=vfs0`。除了旧的配额系统（如 `ext2`，`jqfmt=vsold` 版本1），`ext3` 还支持日志配额（版本2配额）。`jqfmt=vfsv0` 启用日志配额。对于日志配额，需要选项 `usrquota=aquota.user` 和 `grpjquota=aquota.group` 来告知配额系统使用哪些配额数据库文件。日志配额的优点是即使在崩溃后也不需要进行配额检查。

# EXT4 挂载选项

`ext4` 文件系统是 `ext3` 文件系统的高级版本，它结合了扩展性和可靠性增强，以支持大文件系统。

选项 `journal_dev`, `noload`, `data`, `commit`, `orlov`, `oldalloc`, `[nouser_xattr]` `[noacl]`, `bsdmf`, `minid`, `debug`, `errors`, `data_err`, `grpid`, `bsgrroups`, `nogprid`, `sysgroups`, `resgid`, `resid`, `sb`, `quota`, `noquota`, `grpquota`, `usrjquota`, `jrpquota` 和 `jqfmnt` 与 `ext3` 和 `ext2` 向后兼容。

- `journal_checksum`

启用日志事务的校验和检查。这将允许 `e2fsck` 中的恢复代码和内核检测内核中的损坏。这是一个兼容性更改，旧版本的内核会忽略它。

- `journal_async_commit`

提交块可以在不等待描述符块（descriptor blocks）的情况下直接写入磁盘。如果启用，旧版本内核将无法挂载该设备。这将内部启用 `journal_checksum`。

- `barrier=0`/`barrier=1`

这启用/禁用屏障。`barrier=0` 禁用，`barrier=1` 启用。写屏障强制日志提交在磁盘上的排序，使得易性写缓存可以安全使用，但会有一定的性能损失。`ext3` 文件系统默认不启用屏障。除非你的磁盘带有电池备份或其他，否则请务必启用屏障，以免在断电时导致文件系统损坏。

- `commit=nsec`

每隔 `nsec` 秒同步一次数据和元数据。默认值为 5 秒。设置为 0 则不默认同步数据。

- `user_attr`

扩展属性。详见 `attr(5)` 手册页。

- `acl`

启用 POSIX 控制列表。详见 `usrquota=aquota.user/grpjquota=aquota.group/jqfmnt=vfs0`。除了旧的配额系统（如 `ext2`，`jqfmt=vsold` 版本1），`ext3` 还支持日志配额（版本2配额）。`jqfmt=vfsv0` 启用日志配额。对于日志配额，需要选项 `usrquota=aquota.user` 和 `grpjquota=aquota.group` 来告知配额系统使用哪些配额数据库文件。日志配额的优点是即使在崩溃后也不需要进行配额检查。

- `journal_checksum`

启用日志事务的校验和检查。这将允许 `e2fsck` 中的恢复代码和内核检测内核中的损坏。这是一个兼容性更改，旧版本的内核会忽略它。

- `journal_async_commit`

提交块可以在不等待描述符块的情况下直接写入磁盘。如果启用，旧版本内核将无法挂载该设备。这将内部启用 `journal_checksum`。

- `barrier=0`/`barrier=1`

这启用/禁用屏障。`barrier=0` 禁用，`barrier=1` 启用。写屏障强制日志提交在磁盘上的排序，使得易性写缓存可以安全使用，但会有一定的性能损失。`ext3` 文件系统默认不启用屏障。除非你的磁盘带有电池备份或其他，否则请务必启用屏障，以免在断电时导致文件系统损坏。

- `commit=nsec`

每隔 `nsec` 秒同步一次数据和元数据。默认值为 5 秒。设置为 0 则不默认同步数据。

- `user_attr`

扩展属性。详见 `attr(5)` 手册页。

- `acl`

启用 POSIX 控制列表。详见 `usrquota=aquota.user/grpjquota=aquota.group/jqfmnt=vfs0`。除了旧的配额系统（如 `ext2`，`jqfmt=vsold` 版本1），`ext3` 还支持日志配额（版本2配额）。`jqfmt=vfsv0` 启用日志配额。对于日志配额，需要选项 `usrquota=aquota.user` 和 `grpjquota=aquota.group` 来告知配额系统使用哪些配额数据库文件。日志配额的优点是即使在崩溃后也不需要进行配额检查。

## FAT 挂载选项

(注意：`fat` 并不是独立的文件系统，而是 `mdsdos`、`umsdos` 和 `vfat` 文件系统的共同部分。)

`blockSize={512|1024|2048}`

设置块大小（默认值为 512）。此选项已过时。

`uid=value` and `gid=value` 设置所有文件的所有者和组。（默认值：当前进程的 uid 和 gid）

`umask=value`

设置 `umask`（未包含的权限位）。默认值为当前进程的 `umask`。值以八进制形式给出。

`dmask=value`

设置仅应用于目录的 `umask`。默认值为当前进程的 `umask`。值以八进制形式给出。

`fmask=value`

设置仅应用于普通文件的 `umask`。默认值为当前进程的 `umask`。值以八进制形式给出。

`allow_utime=value`

此选项控制 `mtime.atime` 的权限检查。

如果当前进程是文件组 ID 的成员，则你可以更改时间戳。

其他用户也可以更改时间戳。默认取决于 `dmask` 选项设置。如果目录可写，也允许 `utime(2)`。即 `-dmask & 22`。

通常 `utime(2)` 检查当前进程是否为文件所有者或具有 `CAP_FOWNER` 权限。FAT 文件系统在磁盘上没有 uid/gid，因此普通检查缺乏活性。通过此选项你可以放宽限制。

`check=value` 可以选择三种严格程度的检查：

- `r[relaxed]`: 接受并等同大小写，长文件名部分会被截断（例如，`verylongname.foobar` 变为 `verylong.foo`），每个名称部分（文件名和扩展名）允许前导和嵌入空格。

- `n[normal]`: 与 `relaxed` 类似，但拒绝许多特殊字符（*、?、空格等）。这是默认值。

- `s[strict]`: 与 `normal` 类似，但名称可能包含 Linux 使用但 MS-DOS 不接受的长部分和某些特殊字符（+、=、空格等）。

`value=value` 设置在 FAT 和 VFAT 文件系统上转换为短名称时使用的代码页。默认使用代码页 437。

`conv={b[binary]|[ext][auto]}` Fat 文件系统可以在内核中执行 CRLF<->NL（MS-DOS 文本格式到 UNIX 格式）转换。可用以下转换模式：

- 不进行任何翻译。这是默认值。

- `text`: 对所有文件进行 CRLF<->NL 翻译。

- `auto`: 对所有没有“已知”扩展名的文件进行 CRLF<->NL 翻译。已知扩展名列表可以在 `sfs/misc.c` 的开头找到（从 2.0 开始，列表为：`exe, com, bin, app, sys, drv, ovl, ovr, obj, bib, dll, pif, arc, zip, lha, lzha, zoo, tar, z, arj, tz, tzp, ptz, gz, tgz, def, gib, mtif, gl, jpg, pxcm, tfm, vf, gf, pk, pxl, dvi`）。

使用 `Iseeks` 而不是内核文本转换的程序。某些人的数据因这种翻译而损坏了。请小心！

对于以二进制模式挂载的文件系统，提供了转换工具（`fromdos/tomdos`）。此选项已过时。

`cvf_format=module` 强制驱动程序使用 CVF（压缩卷文件）模块而不是自动检测。内核支持它们，`cvf_format=xxx` 选项也控制按需加载 CVF 模块。此选项已过时。

`debug` `cvf_option=option` 传递给 CVF 模块。此选项已过时。开启调试标志。打印字符串和文件系统参数列表（如果参数看起来一致，也会打印这些参数）。如果设置，当块空闲时向块设备发出丢/TRIM 命令。这对于 SSD 设备和稀疏/稀填充 LUN 很有用。
