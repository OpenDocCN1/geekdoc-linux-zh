

+   • chmod—更改文件的权限。 使用 chmod 的最简单方法是使用八进制权限表示，例如 chmod 644 filename.txt 将 filename.txt 的权限更改为 644 (-rw-rw-rw-)。 你也可以通过使用 u、g、o 和 a 分别表示用户、组、其他用户和所有权限的代码，结合加号 (+) 、减号 (-) 或等号 (=) 以及 r、w 或 x 代码来表示读、写和执行权限，来更改单个位。 例如，chmod a+x program 给所有用户（所有者、组和其他人）对文件 program 的执行权限。 chmod go-rw filename.txt 从 filename.txt 中移除组和其他用户的读和写访问权限。

chown、chgrp 和 chmod 命令都适用于文件和目录。 还有一个 -R 或 --recursive 开关可将这些命令应用于整个目录树，例如 chown edgar /home/edgar --recursive。

表 9.1 列出了一些常见的权限代码、其字符串等价物和含义。 请记住，这些并不是唯一可能的权限； 共有 9 个位可用，因此有 512 种可能的权限，不包括链接和目录等特殊文件的变体。

## TABLE 9.1 Sample Permissions and Their Meanings

| Octal Code | Permissions | Meaning |
|---|---|---|
| 644 | -rw-r--r-- | 文件所有者可以读和写文件，其他所有人只能读。 |
| 640 | -rw-r----- | 文件所有者可以读和写文件，文件所属组成员可以读它，但其他人无法访问它。 |
| 755 | -rwxr-xr-x | 文件所有者可以读、写和执行文件，其他所有人可以读或执行它。 |
| 711 | -rwx--x--x | 文件所有者可以读、写和执行文件，其他所有人只能执行它。 |
| 444 | -r--r--r-- | 所有人都可以读文件，没有人可以写或执行它。 |

## Ownership and Permissions on Non-Linux Filesystems

如果你使用 Linux 服务器来提供非 Linux 文件系统，特别是 HFS 或 FAT 文件系统，你会遇到 Linux 对这些外来文件系统的所有权和权限的处理。 因为 Linux 非常依赖所有权和权限功能，所以 Linux 基本上在非原生文件系统上伪造这些功能。 例如，如果你挂载一个 FAT 文件系统，Linux 会为该文件系统上的文件分配一组默认的权限和所有权。 你可以通过 mount 命令的选项或 /etc/fstab 文件中的条目来指定这些内容。 如果你发出完整的 mount 命令，这些选项出现在 -o 参数之后，例如 mount /dev/fd0 /mnt/floppy -t vfat -o uid=500。 在 /etc/fstab 条目的情况下，这些选项放在第四列。 在这两种情况下，多个选项可以用逗号分隔。 最相关的选项总结在表 9.2 中。

## TABLE 9.2 Mount Options for Non-Linux Filesystems

| Option | Filesystems | Meaning |
|---|---|---|
| uid=value | msdos, vfat, hfs, hpfs, ntfs, iso9660 | 设置所有文件的所有者 ID。 |
| gid=value | msdos, vfat, hfs, hpfs, ntfs, iso9660 | 设置所有文件的组 ID。 |
| umask=value | msdos, vfat, hfs, hpfs, ntfs, iso9660 | 设置将从文件中移除的权限位，以八进制表示。 例如，值 000 会导致文件具有 -rwxrwxrwx 权限，而值 022 会导致文件具有 -rwxr-xr-x 权限。 |
| nonumtail | vfat | 通常，VFAT 文件系统会在文件名超过 8.3 限制时创建带有数字尾部的底层 8.3 文件名，例如 longfi-1.txt 对应 long-filename.txt。 此选项在可能的情况下消除这些尾部，从而得到类似 longfile.txt 的 8.3 文件名。 |
| conv=[t]ext|[b]inary|[a]uto | UNIX/Linux、DOS/Windows/OS/2 和 MacOS 在文本文件中的行尾处理方式各不相同。 此选项设置转换选项：text 将所有文件视为文本文件，binary 将所有文件视为二进制文件（不转换），auto 则尝试通过文件名扩展名或其他线索来判断。 binary 是推荐的默认设置。 |
| case=lower|asis | hpfs, hfs | 将所有文件转换为小写或保持大小写不变。 默认值为 hpfs 的 lower，hfs 的 asis。 |
| fork=cap|double|netatalk | hfs | 以各种格式显示 Macintosh 资源分支数据。 如果你使用 Netatalk 进行 Macintosh 文件共享，netatalk 是首选格式。 |
| afpd | hfs | 使文件系统的处理更兼容 Netatalk。 |
| creator=xxxx | hfs | 将新文件的文件的 Macintosh 创建者代码设置为指定的四字母代码。 |
| norock | iso9660 | 如果存在，则不使用 Rock Ridge 扩展。 |
| nojoliet | iso9660 | 如果存在，则不使用 Joliet 文件系统。 |
| noauto | All filesystems | 不要在系统启动时挂载文件系统。 推荐用于可移动介质。 仅在 /etc/fstab 中使用。 |
| user | All filesystems | 允许非 root 用户挂载文件系统。 仅在 /etc/fstab 中使用。 |
| loop | All filesystems | 将磁盘映像挂载为可移动磁盘或分区。 |

mount 命令的手册页列出了这些和其他文件系统的其他选项。 支持最新的 Linux 文件系统（主要是 HFS 和 NTFS）并未在 mount 手册页中完全描述，因此你应该查阅内核源代码树中的文档文件，以获取有关这些文件系统挂载选项的更多信息。

