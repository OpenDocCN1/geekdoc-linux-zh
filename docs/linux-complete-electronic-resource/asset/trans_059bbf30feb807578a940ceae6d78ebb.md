
`/etc/sshrc` 此文件中的命令由 **ssh** 在用户登录时、在启动用户的 shell（或命令）之前执行。有关更多信息，请参阅 **sshd** 手册页。

`$HOME/.ssh/rc` 此文件中的命令由 **ssh** 在用户登录时、在启动用户的 shell（或命令）之前执行。有关更多信息，请参阅 **sshd** 手册页。

# 安装

**Ssh** 通常安装为 suid root。它仅在 rhosts 认证时需要 root 权限（rhosts 认证要求连接必须来自特权端口，而分配此类端口需要 root 权限）。它还需要能够读取 `/etc/ssh_host_key` 以执行 **RSA** 主机认证。可以在没有 root 权限的情况下使用 **ssh**，但 rhosts 认证将被禁用。**Ssh** 在建立与远程主机的连接后立即放弃任何额外权限。

在确保 **ssh** 的安全性方面投入了大量工作。但是，如果您发现安全问题，请立即向 <ssh-bugs@cs.hut.fi> 报告。

# 作者

Tatu Ylonen <ylo@cs.hut.fi>

关于新版本的信息、邮件列表以及其他相关问题，可以在 ssh **WWW** 主页 `http://www.cs.hut.fi/ssh` 上找到。

# 参见

sshd(8), ssh-keygen(1), ssh-agent(1), ssh-add(1), scp(1), make-ssh-known-hosts(1), rlogin(1), rsh(1), telnet(1)

# SU(1)

## 名称

**su** 以替代的用户和组 ID 运行 shell。

## 概要

```
su [-flmpP] [-c command] [-s shell] [--login] [--fast] [--preserve-environment] [-command=command] [--shell=shell] [-] [-help] [-version] [user [arg...]]
```

## 描述

本文档不再维护，可能不准确或不完整。Texinfo 文档现在是权威来源。

本手册页记录 GNU 版本的 su。su 允许一个用户暂时成为另一个用户。它运行具有 USER 的实际和有效用户 ID、组 ID 和辅助组的 shell。如果没有给出 USER，默认是 root（超级用户）。运行的 shell 取自 USER 的密码条目，如果在那里没有指定，则默认为 /bin/sh。如果 USER 有密码，除非是由实际用户 ID 为 0（超级用户）的用户运行，否则 **su** 会提示输入密码。

默认情况下，su 不更改当前目录。它从 USER 的密码条目设置环境变量 'HOME' 和 'SHELL'，如果 USER 不是超级用户，则将 'USER' 和 'LOGNAME' 设置为 USER。默认情况下，shell 不是登录 shell。

如果提供一个或多个 ARG，它们将作为附加参数传递给 shell。

su 不会特殊处理 /bin/sh 或其他 shell（例如将 argv[0] 设置为 "-su"，仅向某些 shell 传递 -c 等）。

在具有 syslog 的系统中，可以编译 su 以使用 syslog 报告失败的，以及可选的成功的 **su** 尝试。

## 选项

- `-c` *COMMAND*, `--command=COMMAND` 将 *COMMAND*（单个命令行）通过 -c 选项传递给 shell，而不是启动交互式 shell。
- `-f`, `--fast` 将 -f 选项传递给 shell。这通常仅对 csh 和 tcsh 有意义，对于这些 shell，-f 选项可以防止读取启动文件（.cshrc）。对于 Bourne 类 shell，-f 选项会禁用文件名模式扩展，这通常不是期望的行为。
- `-help` 在标准输出上打印用法消息并成功退出。
- `-l`, `--login` 将 shell 设为登录 shell。这意味着：取消设置除 `TERM`、`HOME` 和 `SHELL`（如上所述进行设置）以及 `USER` 和 `LOGNAME`（如上所述进行设置）之外的所有环境变量。如果运行 su 的用户不是超级用户，且 USER 的 shell 受到限制，则受限 shell 是指未列在 /etc/shells 文件中或内部编译的文件列表中且该文件不存在的 shell。此选项的部分行为可以被 --login 和 --shell 覆盖。
- `-m`, `-p`, `--preserve-environment` 不更改环境变量 `HOME`、`USER`、`LOGNAME` 或 `SHELL`。运行环境变量 `SHELL` 中指定的 shell，而不是来自 /etc/passwd 的 USER 的 shell，除非运行 su 的用户不是超级用户且 USER 的 shell 受到限制。受限 shell 是指未列在 /etc/shells 文件中或内部编译的文件列表中且该文件不存在的 shell。此选项的部分行为可以被 --login 和 --shell 覆盖。
- `-s`, `--shell` *shell* 运行 SHELL，而不是来自 /etc/passwd 的 USER 的 shell，除非运行 su 的用户不是超级用户且 USER 的 shell 受到限制。
- `--version` 在标准输出上打印版本信息并成功退出。

# TAR(1)

## 名称

**tar** GNU 版本的 tar 归档实用工具。

## 概要

```
tar [ -1 ] A --catenate --concatenate | c --create | d --diff --compare | r --append | t --list | u --update | x --extract --get [ --time-preserve ] [ -b, --block-size N ] [ -B, --read-full-blocks ] [ _-c, --directory DIR ] [ --checkpoint ] [ -f, --file [HOSTNAME:]]F ] [ --force-local ] [ -F, --info-script F --new-volume-script F ] [ -G, --incremental ] [ -g, --listed-incremental F ] [ -h, --dereference ] [ -i, --ignore-zeros ] [ --ignore-failedread ] [ -k, --keep-old-files ] [ -K, --starting-file F ]
[ -I, --one-file-system ] [ -L, --tape-length N ]
[ -m, --modification-time ] [ -M, --multi-volume ]
[ -N, --after-date DATE, --newer DATE ]
[ -o, --old-archive, --portability ] [-O, --to-stdout ]
[ -p, --same-permissions, --preserve-permissions ]
[ -P, --absolute-paths ] [ --preserve ] [ -R, --record-number ]
[ --remove-files ] [ -s, --same-order, --preserve-order ]
[ --same-owner ] [ -S, --sparse ] [ -T, --files-from F ] [ --null ]
[ --totals ] [ -v, --verbose ] [ -V, --label NAME ] [ --version ]
[ -w, --interactive, --confirmation ] [ -W, --verify ] [ --exclude FILE ]
[ -X, --exclude-from FILE ] [ -Z, --compress, --uncompress ]
[ -z, --gzip, --ungzip ] [ --use-compress-program PROG ]
[ --blockcompress ] [ [-0-7] ] [ mbh ]

filename1 [ filename2, ... filenameN ]
directory1 [ directory2, ... directoryN ]
```

## 描述

本手册页记录 GNU 版本的 tar，这是一个旨在从称为 tarfile 的归档文件中存储和提取文件的归档程序。tarfile 可以制作在磁带驱动器上，但也很常见将 tarfile 写入普通文件。tar 的第一个参数必须是选项之一：A c d r u，后跟任意可选功能。tar 的最后一个参数是应归档的文件或目录的名称。使用目录名始终意味着应包含其下的子目录。

## 功能字母

必须使用以下选项之一：

- `-A`, `--catenate`, `--concatenate` 将 tar 文件追加到归档中。
- `-c`, `--create` 创建新的归档。
- `-d`, `--diff`, `--compare` 查找归档与文件系统之间的差异。
- `-delete` 从归档中删除（不适用于磁带！）。
- `-r`, `--append` 将文件追加到归档末尾。
- `-t`, `--list` 列出归档的内容。
- `-u`, `--update` 仅追加比归档中副本更新的文件。
- `-x`, `--extract`, `--get` 从归档中提取文件。

## 其他选项

- `--atime-preserve` 不更改已转储的 FILES 的访问时间。
- `-b`, `--block-size` *N* 块大小为 Nx512 字节（默认 N=20）。
- `-B`, `--read-full-blocks` 读取时重新分块（用于读取 4.2BSD 管道）。
- `-C`, `--directory` *DIR* 更改到目录 DIR。
- `--checkpoint` 在读取归档时打印目录名称。
- `-f`, `--file` [*HOSTNAME:*]*F* 使用归档文件或设备 F（默认 /dev/rmt0）。
- `--force-local` 即使归档文件包含冒号，也视为本地文件。
- `-F`, `--info-script` *F* `--new-volume-script` *F* 在每盘磁带结束时运行脚本（隐含 -M）。
- `-G`, `--incremental` 创建/列出/提取旧 GNU 格式的增量备份。
- `-g`, `--listed-incremental` *F* 创建/列出/提取新 GNU 格式的增量备份。
- `-h`, `--dereference` 不转储符号链接；转储它们指向的文件。
- `-i`, `--ignore-zeros` 忽略归档中的零块（通常意味着文件结束）。
- `--ignore-failed-read` 在遇到不可读 FILES 时不以非零状态退出。
- `-k`, `--keep-old-files` 保留现有文件；不从归档中覆盖它们。
- `-K`, `--starting-file` *F* 从归档中的文件 F 开始。
- `-l`, `--one-file-system` 在创建归档时停留在本地文件系统中。

