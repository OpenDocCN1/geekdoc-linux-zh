
在初始检入期间，如果没有给出 `-i`，`ci` 将从标准输入获取文本，以文件结束符或单独包含 `( )` 的行结束。如果可能，将提示用户进行交互，参见 `-i`。

# 第一部分：用户命令

与旧版本 RCS 的向后兼容，裸的 `-t` 选项是

- `-t`

如果前者于后者且存在新版本，则将 RCS 文件的修改时间设置为新版本的时间；否则更新 RCS 文件的修改时间。如果你锁定了一个版本，它通常会将 RCS 文件的修改时间更新为当前时间，锁存储在 RCS 文件中，移除需要更改 RCS 文件。这可以通过两种方式创建比工作文件新的 RCS 文件：`file -M` 可以创建一个带有更改的工作文件，而工作文件保持不变。这两种情况可能会导致工作文件对 `RCS` 文件的 `make(1)` 依赖产生过度重新编译。`-t` 选项通过查看 RCS 文件的时间来抑制这种重新编译。谨慎使用此选项；即使更改应该影响与 RCS 文件相关的另一个工作文件，它也会抑制事件。例如，如果 RCS 之间的时间是 01:00（当前时间为 04:00），`file -d` 将 RCS 文件设置为 02:00 而不是通常的 04:00；这会导致 `-t` 错误地认为另一个文件比 RCS 文件新。

- `-login`

将登录名分配给检出版本的作者。对于作者，如果无可用作者，则使用 `-k`。

- `-V`

打印 RCS 版本号。

- `-n`

模拟 RCS 版本信息；参见 `co(1)`。

- `-xsuffix`

指定 RCS 的后缀。空后缀匹配任何以 `/` 结尾的路径。`-x` 选项可以指定后缀列表，例如 `-x` 匹配任何以 `/` 结尾的路径。

# 第一部分 用户命令

- 检查宿主机是否支持 RCS setuid。如果有任何疑问，请咨询可靠的专家。如果 setuid 系统按照 POSIX 1003.1a Draft 5 中描述的那样工作最好，因为 RCS 可以在真实用户和有效用户之间轻松切换，即使真实用户是 root。如果不是，最好是 setuid 系统支持 POSIX 1003.1-1999 的保存 setuid `(_POSIX_SETUID_ID)`；此操作仅在真实用户或有效用户为 root 时才会失败。如果 RCS 检测到 setuid 失败，它将立即退出。

- 选择一个用户作为该用户组的 RCS 管理员。`A` 在用户的 RCS 文件上调用 RCS 命令。`A` 不应该是 root 或任何具有特殊权限的用户。相互猜疑的用户组应使用不同的管理员。

- 选择一个路径 `B` 来包含供用户执行的 `ci` 副本。

- 让 `A` 设置 `B`，其中包含 `ci` 和 `co` 的副本，这些副本通过从标准安装目录 `D` 复制命令并设置为 `A`，如下所示：

  ```
  mkdir B; cp c[io] B; chmod -w,-u B/c[io]
  ```

- 让每个用户将 `B` 置于其路径之前，如下：

  ```
  PATH=$B:$SPATH; export PATH # ordinary shell
  set path=$B $SPATH # shell
  ```

- 让 `A` 创建 RCS 目录 `R`，且仅对 `A` 有写权限，如下：

  ```
  mkdir R; chmod -w R
  ```

- 如果只想允许用户读取 RCS 文件，请将它们放入组 `G`，并让 `A` 如下保护 RCS 目录：

  ```
  chgrp G; chmod -w,-x R
  ```

- 让 `A` 将旧的 RCS 文件（如果有）复制到 `R`，以确保 `A` 拥有它们。

RCS 文件的访问列表限制了谁可以提交（check in）和锁定版本。默认访问列表是空的，这允许任何可以读取 RCS 文件的用户获得提交权限。特别是，`res -a` 将访问限制为仅限 `A`。

- 在初始提交之前，让 `A` 使用 `res -i` 初始化任何新的 RCS 文件，如果你想限制检查出访问，请添加 `-a` 选项。

- 仅给 `ci`、`co` 和 `resclean` 赋予 setuid 权限；不要赋予 `res` 或任何其他命令。

- 不要使用其他命令调用 RCS 命令；setuid 比你想象的要复杂得多！

## 环境

`RCSINIT`

附加在参数列表之前的选项，用空格分隔。反斜杠转义选项。`RESINIT` 选项附加在大多数 RCS 命令的列表之前。实用的 `RCSINIT` 选项包括 `-a,-v,-x,` 和 `-z`。

`TMPDIR`

临时目录的名称。如果没有设置，则会检查环境变量 `TMP` 和 `TMPDIR` 并采用找到的第一个值；如果哪个都没有设置，则使用取决于主目录的默认值，通常为 `/tmp`。

## 诊断

对于每个版本，`ci` 会读取 RCS 文件、工作文件，以及已存入版本和前一个版本的数量。当当（且仅当）所有操作都成功时，退出状态为零。

## 标识

作者：Walter F. Tichy。

手册页：5.17；发布日期 1995年6月16日

版权所有 © 1982, 1988, 1989 Walter F. Tichy

版权所有 © 1990, 1991, 1992, 1993, 1994 Paul Eggert

# 另见

`co(1)`, `emacs(1)`, `ident(1)`, `make(1)`, `rcs(1)`, `rsclean(1)`, `rcsdiff(1)`, `rcsintro(1)`, `rcsmerge(1)`, `rlog(1)`, `setuid(2)`, `rcsfile(5)`

Walter F. Tichy, “RCS—A System for Version Control,” Software Practice & Experience 15, 7 (1985年7月), 637–65.

GNU, 1995年6月16日

## cidentd

`cident`—cidentd 服务器

## 概要

```
cident [-usqvahn] [-f file] [-l file] [-t seconds]
```

## 描述

`cident` 提供身份验证信息。

`cident` 是一个 RFC 1314- 和 931-cident 守护进程。它在端口（默认 113）上接受连接，并对连接命令的查询做出回答。

`cident` 在命令结束时通常会终止。用户主目录下的 `.authfile` 用于向请求系统提供任何……

- `-u`

  开启使用用户主目录下的 `.authfile`，向请求系统提供用户提供的任何信息。这会被 `-a` 选项和系统文件覆盖如下：

  ```
  myname          name-to-given      # 提供此 userid
  hideme                    # 隐藏用户 id
  host-ip         name-to-given      # 为他们提供的 userid
  host-ip         no-info             # 向他们隐藏你
  ```

  `host-ip` 可以是点点表示法的 IP 或名称。文件以最后设置的为我们获取的内容。

- `-s`

  单次查询后关闭连接。

- `-Q`

  在 1 个连接后退出守护进程（默认 1.0b）。

- `-v`

  开启到 syslog 的详细日志记录。

- `-n`

  让 `cident` 表现像旧样式一样，没有特殊之处。

- `-a`

  启用 `/etc/cident.users` 选项，如果指定了 `-u`，则覆盖该文件。格式如下：

  ```
  username        name-to-given      # 提供此 userid
  hideme                    # 隐藏用户 id
  all             name-to-given      # 为所有
  all             no-info             # 全部
  host-ip         name-to-given      # 为他们提供的 userid
  host-ip         no-info             # 向他们隐藏你
  ```

  `host-ip` 可以是点点表示法的 IP 或名称。文件以最后设置的为我们获取的内容。

- `-h`

  显示帮助。

- `-f`

  指定文件。

- `-l`

  指定文件。

- `-t`

  超时秒数。

# 第一部分 用户命令

如果没有指定参数，`cident` 在默认分支上运行。

# 文件

`.authfile`

`/etc/cident.users`

# 另见

`ident(1)`

# Bug

我所知的没有。

## cksum

`cksum`—字节校验和

## 概要

```
cksum [--help] [--version] [file...]
```

## 描述

`cksum` 计算每个文件的（CRC）。通常用于确保传输的文件（如网络）没有损坏。算法由 BSD 指定。

可用选项为：

- `--help`

  打印用法并退出。

- `--version`

  打印版本信息。

## clear

`clear`—清除屏幕

## 概要

```
clear
```

## 描述

`clear` 调用 `tput(1)` 清除屏幕。这会导致屏幕清空。

# 另见

`reset(1)`, `stty(1)`, `tput(1)`
