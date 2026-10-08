

# 168
# cpio

警告信息且不会替换文件。（您可以使用 -u 选项无条件地覆盖现有文件。）

# 复制出模式 (Copy-Out Mode)

cpio -o（复制出）读取标准输入获取路径名列表，并将这些文件同路径名和状态信息一起复制到标准输出。默认情况下，输出对齐到 512 字节边界，或由 -B -C 选项指定的块大小，或者在需要时使用某些依赖于设备的块大小（例如对于 CTC 磁带）。

# 传递模式 (Pass Mode)

cpio -p（传递）读取标准输入获取文件路径名列表，并根据下述选项将这些文件有条件地创建并复制到目标目录树中。

# 注意

cpio 存档中允许的最大路径名长度由头部类型决定。下表了每个支持的存档类型的正确值。

| 类型 | 命令行选项 | 最大路径名长度 |
| :--- | :--- | :--- |
| BINARY | -o | 256 |
| POSIX | -OH od | 256 |
| ASCII | -oc | 1023 |
| CRC | -OH crc | 1023 |
| USTAR | -OH ustar | 255 |

当您指定命令行选项 -H tar 时，创建的存档为 USTAR 格式，这意味着使用命令行选项 -i -H tar 读取存档将是错误。相反，请使用命令行选项 -i -H ustar 读取存档。选项 -i -H tar 指的是较旧的 tar 格式。这些更改是在 Solaris 9 版本中引入的新特性。

只有超级用户（super）可以复制特殊文件。

块以 512 字节为单位报告。
如果文件具有 000 权限、包含超过 0 个字符的数据，且用户不是 root，则该文件不会被保存或恢复。

存储在头部（/usr/include/archives.h）中的节点号是一个无符号短型，占用 2 字节。此限制将节点号的范围限制在 0 到 65535。硬链接文件必须在此范围内，这在不同厂商的机器之间移动 cpio 存档时可能会出现问题。

当卷管理守护进程运行时，通过设备名称（例如 /dev/rdiskette）访问磁盘可能无法成功。详情请参阅 man(1)。

当从硬盘检索或复制文件时，您必须使用与从硬盘复制文件到磁带时相同的块因子。因此，您必须指定 -B 选项。

# cpio 169
# 选项

# 选项

- -i 复制入（Copy in）。从标准输入提取文件。
- -o 复制出（Copy out）。读取标准输入获取路径名列表，并将这些文件复制到标准输出。
- -p 传递。读取标准输入获取文件路径名列表。

您可以任意顺序将以下选项附加到 -o、-i 或 -p 选项之后。

- @ 在存档中包含扩展属性。默认情况下，cpio 不会将扩展属性放入存档。使用此选项时，cpio 会查找要放置在存档中的文件的扩展属性并将它们作为具有特殊类型的普通文件添加。。在 -i 或 -p 上使用 -H 选项会指示 cpio 同普通文件数据一起恢复扩展属性数据。提取属性记录的尝试将被忽略。扩展文件属性是 Solaris 9 版本中引入的新特性。
- -a 复制后更新输入文件的访问时间。链接文件的访问时间不会重置（与 -m 互斥）。
- -A 将文件追加到存档。-A 选项需要 -H 选项。仅对硬盘分区上的存档有效。
- -b 反转每个字内字节的顺序。（仅与 -i 选项一起使用。）
- -B 将输入/输出对齐到记录的 512 字节。当不使用此选项和 -C 选项时，默认缓冲区大小为 512 字节。-B 不适用于传递选项；-B 仅对指向或源自字符设备（例如 /dev/rmt）的数据有意义。
- -c 以 ASCII 形式读取或写入头部信息以实现可移植性。此头部没有相关的 UID 或 GID 限制。基于 SVR4 的机器使用此选项，或使用 -H unknown。-c 选项意味着使用扩展的设备号，这仅在基于 SVR4 的系统上支持。在 Solaris 1.x 或交互式 UNIX 之间传输文件时，使用 -H unknown。
- -C bufsize 将输入/输出对齐到记录的 bufsize 字节，其中 bufsize 被替换为正整数。当不使用此选项和 -B 选项时，默认缓冲区大小为 512 字节。-C 不适用于传递选项；-C 仅对指向或源自字符设备（例如 /dev/rmt）的数据有意义。
- -d 根据需要创建目录。
- -E 指定输入文件（file），该文件包含要从存档中提取的文件名列表（每行一个）。

# 170
# cpio

- -f 复制所有模式模式之外的文件。
- -H header 头部。以格式读取或写入头部信息。当源机器和目标机器不同时，始终使用此选项或 -c 选项（与 -f 互斥）。可用的头部格式列在下方。
- -bar Bar 格式。仅与 -i 选项一起使用（只读）。
- -crc 带有扩展设备号和每个文件一个额外校验和的 ASCII 头部。此头部格式没有相关的 UID 或 GID 限制。
- -od 带有扩展设备号的 ASCII 头部。此头部格式没有 UID 或 GID 限制。基于 SVR4 的机器使用此选项，或使用 -H unknown。-c 选项意味着使用扩展的设备号，这仅在基于 SVR4 的系统上支持。在 Solaris 1.x 或交互式 UNIX 之间传输文件时，使用 -H unknown。
- -od 带有扩展设备号的 ASCII 头部。此头部格式没有 UID 或 GID 限制。基于 SVR4 的机器使用此选项，或使用 -H unknown。
- -tar tar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
-
- -tar tar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar tar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
- -ustar ustar 格式。此头部允许 UIDs 和 GIDs 扩展到 255。
