
### 配置选项

- `ServerAliveCountMax`
- `StrictHostKeyChecking`
- `TCPKeepAlive`
- `UpdateHostKeys`
- `UsePrivilegedPort`
- `User`
- `UserKnownHostsFile`
- `VerifyHostKeyDNS`
- `-P` `port`

指定要连接的远程主机上的端口。
- `-P`

保留传输的原始文件的修改时间、访问时间和模式。
- `-Q`

静默模式：禁用进度计量器以及来自 `ssh(1)` 的警告和诊断消息。
- `-R` `num_requests`

指定在任何时刻允许未完成请求的数量。增加此值可能会略微提高文件传输速度，但会增加内存使用量。默认值为 64 个未完成请求。
- `-r`

在上传和下载时递归复制整个目录。注意，`sftp` 在树遍历过程中不会遵循符号链接。
- `-S` `program`

用于加密连接的 `program` 名称。该程序必须理解 `ssh(1)` 选项。
- `-s` `subsystem` | `sftp_server`

指定远程主机上的 SSH2 子系统或 sftp 服务器的路径。路径对于使用协议版本 1 的 `sftp` 或远程 `sshd(8)` 未配置 sftp 子系统的情况很有用。
- `-v`

提高日志级别。此选项也会传递给 `ssh`。

## 交互式命令

进入交互模式后，`sftp` 理解一组类似于 `ftp(1)` 的命令。命令不区分大小写。包含空格的路径名必须用引号括起来。路径名中包含的任何由 `shell(3)` 识别的特殊字符都必须用反斜杠 `'\`' 转义。

- `bye`

退出 `sftp`
- `cd` `path`

更改远程目录为 `path`
- `chgrp` `grp` `path`

将文件 `path` 的组更改为 `grp` `path` 可能包含 `shell(3)` 字符，并且可能匹配多个文件。`grp` 必须是数字 GID。
- `chmod` `mode` `path`

将文件 `path` 的权限更改为 `mode` `path` 可能包含 `shell(3)` 字符，并且可能匹配多个文件。
- `chown` `own` `path`

将文件 `path` 的所有者更改为 `own` `path` 可能包含 `shell(3)` 字符，并且可能匹配多个文件。`own` 必须是数字 UID。
- `df` [ `-h` | `-i` ] [ `path` ]

显示持有当前目录或指定时的 `path` 的文件系统的使用信息。如果指定了 `-h` 标志，容量信息将使用“人类可读”后缀显示。`-i` 标志请求除了容量信息外还显示 inode 信息。此命令仅在实现了“statvfs@openssh.com”扩展的服务器上受支持。
- `exit`

退出 `sftp`
- `get` [ `-afPpr` ] `remote-path` [ `local-path` ]

检索 `remote-path` 并将其存储在本地机器上。如果未指定本地 `path` 名称，则其将使用与远程机器上相同的名称。`remote-path` 可能包含 `shell(3)` 字符，并且可能匹配多个文件。如果确实如此且指定了 `local-path`，则 `local-path` 必须指定一个目录。

如果指定了 `-a` 标志，则尝试恢复现有文件的部分传输。请注意，恢复假设本地文件的任何部分副本与远程副本匹配。如果远程文件内容与您本地的部分副本不同，则结果文件可能会损坏。

如果指定了 `-f` 标志，则将在文件传输完成后调用 `flush(2)` 以将文件刷新到磁盘。

如果指定了 `-P` 或 `-p` 标志，则完整的文件权限和访问时间也将被复制。

如果指定了 `-r` 标志，则目录将被递归复制。注意，`sftp` 在执行递归传输时不会遵循符号链接。
- `help`

显示帮助文本。
- `lcd` `path`

更改本地目录为 `path`
- `lls` [ `ls-options` [ `path` ] ]

显示 `path` 或当前目录如果未指定 `path` 的本地目录列表。`ls-options` 可能包含本地系统 `ls(1)` 命令支持的任何标志。`path` 可能包含 `shell(3)` 字符，并且可能匹配多个文件。
- `lmkdir` `path`

创建由 `path` 指定的本地目录
- `ln` [ `-s` ] `oldpath` `newpath`

从 `oldpath` 创建指向 `newpath` 的链接。如果指定了 `-s` 标志，则创建的链接是符号链接，否则是硬链接。
- `lpwd`

打印本地工作目录。
- `ls` [ `-1afhlnrSt` [ `path` ] ]

显示 `path` 或当前目录如果未指定 `path` 的远程目录列表。`path` 可能包含 `shell(3)` 字符，并且可能匹配多个文件。

以下标志被识别并相应地改变 `ls` 的行为：

- `-1`

产生单列输出。
- `-a`

列出以点 `'.'` 开头的文件
- `-f`

不对列表进行排序。默认排序顺序是字典序。
- `-h`

与长格式选项一起使用时，使用单位后缀：Byte, Kilobyte, Megabyte, Gigabyte, Terabyte, Petabyte, and Exabyte 以将位数减少到四个或更少，使用 2 的幂作为大小 `K=1024, M=1048576` 等。
- `-l`

显示附加详细信息，包括权限和所有权信息。
- `-n`

产生带有以数字形式表示的用户和组信息的长列表。
- `-r`

反转列表的排序顺序。
- `-S`

按文件大小对列表进行排序。
- `-t`

按最后修改时间对列表进行排序。
- `lumask` `umask`

将本地 umask 设置为 `umask`
- `mkdir` `path`

创建由 `path` 指定的远程目录
- `progress`

切换进度计量器的显示。
- `put` [ `-afPpr` ] `local-path` [ `remote-path` ]

上传 `local-path` 并将其存储在远程机器上。如果未指定远程路径名称，则其将使用与本地机器上相同的名称。`local-path` 可能包含 `shell(3)` 字符，并且可能匹配多个文件。如果确实如此且指定了 `remote-path`，则 `remote-path` 必须指定一个目录。

如果指定了 `-a` 标志，则尝试恢复现有文件的部分传输。请注意，恢复假设远程文件的任何部分副本与本地副本匹配。如果本地文件内容与部分本地副本不同，则结果文件可能会损坏。

如果指定了 `-f` 标志，则将向服务器发送请求以在文件传输后调用 `flush(2)`。请注意，这仅由实现了“flush”扩展的服务器支持。

如果指定了 `-P` 或 `-p` 标志，则完整的文件权限和访问时间也将被复制。

如果指定了 `-r` 标志，则目录将被递归复制。注意，`sftp` 在执行递归传输时不会遵循符号链接。
- `pwd`

显示远程工作目录。
- `quit`

退出 `sftp`
- `reget` [ `-Ppr` ] `remote-path` [ `local-path` ]

恢复下载 `remote-path` 相当于设置 `-a` 标志的 `get`。
- `reput` [ `-Ppr` ] [ `local-path` ] `remote-path`

恢复上传 `local-path` 相当于设置 `-a` 标志的 `put`。
- `rename` `oldpath` `newpath`

将远程文件从 `oldpath` 重命名为 `newpath`
- `rm` `path`

删除由 `path` 指定的远程文件
- `rmdir` `path`

移除由 `path` 指定的远程目录
- `symlink` `oldpath` `newpath`

从 `oldpath` 创建指向 `newpath` 的符号链接
