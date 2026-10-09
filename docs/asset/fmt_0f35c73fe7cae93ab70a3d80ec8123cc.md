
# 库

`/usr/local`

**本地层次结构** 存储添加到系统的本地重要文件和目录。子目录可以包括 `bin`, `games`, `include`, `lib`, `sbin`, `share` 和 `src`。

`/usr/man`

在线手册

`/usr/sbin`

**非关键系统管理二进制文件** 见 `/sbin`。

`/usr/share`

**与架构无关的数据** 子目录可以包括 `dict`, `doc`, `games`, `info`, `locale`，`man`, `misc`, `terminfo`, 和 `zoneinfo`。

`/usr/share/doc`

# 文档

`/usr/share/info`

# GNU info 系统主目录

`/usr/src`

# 源代码

`/var`

**可变数据** 内容随系统运行而变化的文件保留在 `/var` 下的子目录。最常见的例子是临时文件、系统日志文件、损坏文件和用户邮箱文件。子目录可以包括 `cache`, `lib`, `lock`, `log`, `opt`, `run`, `spool`, `tmp`, 和 `yp`。旧版本的 Linux 将此类文件分散在 `/usr` 的几个子目录中（`/usr/adm`, `/usr/mail`, `/usr/spool`, `/usr/tmp`）。

`/var/log`

**日志文件** 包含 `lastlog`（每个用户最后登录的记录）、`messages`（来自 `syslogd` 的系统消息）和 `wtmp`（所有登录/注销记录）。

`/var/spool`

**池化应用程序数据** 包含 `anacron`, `at`, `cron`, `lpd`, `mail`, `mqueue`, `samba` 和其他目录。文件 `/var/spool/mail` 通常在 `/var` 中有一个符号链接。

# 操作目录

本节涵盖了删除目录、在目录之间复制和移动文件以及移动目录。它还描述了如何使用路径让你的 Linux 工作变得更容易。

# rmdir: 删除目录

`rmdir` 删除一个目录。（注意：该节的 OCR 文本在源文件中严重损坏/乱码；已根据标准 Linux 命令上下文进行处理）。

## 访问权限

除了 `SELux` 实施的控制（第 400 页）外，Red Hat Linux 支持两种方法来控制谁可以访问文件以及他们如何访问文件：传统的访问权限和访问控制列表（ACLs，第 185 页）。ACL 提供了更细粒度的访问权限控制。本节描述了传统的访问权限。

有三类用户可以访问文件：文件所有者（owner）、文件所属组的成员（group；有关组的更多信息，请参阅第 451 页）以及其他所有用户（other）。用户可以通过三种方式尝试访问普通文件：尝试读取、写入或执行。

## ls | 显示权限

当我使用 `-l` 选项和一个或多个文件名调用 `ls` 时，`ls` 会显示关于文件的一行信息。示例显示了两个文件的信息。`letter.0610` 文件包含一封信的文本，而 `check_spell` 包含一个 shell 脚本，这是一个用高级脚本语言编写的程序：

```bash
$ ls -l letter.0610 check_spell

-rw-r--r-- 1 alex pubs 3355 May 2 10:52 letter.0610

-rwxrxr-x 2 alex pubs 852 May 5 14:03 check_spell
```

从左到右，`ls` 命令显示的字段包含以下信息（参考图 6-12）：

- 文件类型（第一个字符）
- 文件的访问权限（接下来的九个字符）
- ACL 标志（如果文件具有 ACL，见第 185 页）
- 文件的链接数（第 190 页）
- 文件所有者的名称（通常是创建文件的人）
- 文件所属组的名称
- 文件的字符大小（字节）
- 文件创建或最后修改的日期时间
- 文件名

| 文件类型 | 文件访问权限 | ACL 链接 | 所有者 | 组 | 大小 | 修改日期和时间 | 文件名 |
|---|---|---|---|---|---|---|---|
| -rw-r--r-- | | | alex | pubs | 2048 | Aug 12 13:15 | memo |

`letter.0610` 的文件类型（第一列）是连字符（-），因为它是一个普通文件（目录文件在该列中显示为 `d`）。

接下来的三个字符指定了文件所有者的访问权限：`r` 表示读取权限，`w` 表示写入权限，`x` 表示执行权限。空格表示所有者不具备该位置应出现的权限。

同样地，接下来的三个字符代表组的权限，最后三个字符代表其他（所有其他用户）的权限。在之前的示例中，所有者所有的 `letter.0610` 可以读取和写入文件，而组和其他用户只能读取文件，且不允许任何人执行。虽然可以为任何文件允许执行权限，但对包含文档（如信件）的文件分配执行权限是没有意义的。`check_spell` 文件是一个可执行的 shell 脚本，因此对它分配执行权限是合适的。（所有者、组和其他用户都有执行权限。）

## chmod: 更改访问权限

文件所有者控制哪些用户有权访问文件以及他们如何访问。当你拥有一个文件时，可以使用 `chmod`（更改模式）实用程序更改文件的访问权限。在接下来的示例中，为所有（`a`）用户添加（`+`）读取和写入（`rw`）权限：

```bash
$ chmod a+rw letter.0610

ls -l letter.0610

-rw-rw-rw- 1 alex pubs 3355 May 2 10:52 letter.0610
```

> **提示：你必须具有读取权限才能执行 shell 脚本**

因为 shell 在执行脚本中的命令（一个包含 shell 命令的文本文件）之前需要读取该 shell 脚本，因此你必须对文件拥有读取权限才能执行它。你还需要在命令行上直接执行 shell 脚本的执行权限。相比之下，二进制（程序）文件不需要读取；它们是直接执行的。运行一个二进制程序只需要执行权限。在下一个示例中，`chmod` 移除了其他用户的读取和执行（`x`）权限，但没有移除文件所有者（`alex`）和组成员（`pubs`）：

```bash
$ chmod o-x check_spell

ls -l check_spell

-rwxr--x- 2 alex pubs 852 May 5 14:03 check_spell
```

除了 `a`（所有）和 `o`（其他）外，你可以在参数中的任何时间使用 `g`（组）和 `u`（用户，指文件所有者）。你也可以使用绝对或数字参数。有关使用绝对参数的更多信息，请参阅第 227 页。更多信息请参阅第 451 页。

**提示：`chmod`, `o`, `u`**：在使用 `chmod` 时，很多人假设 `o` 代表 owner；并非如此。`o` 代表 other，而 `u` 代表 owner。缩写 UGO（用户-组-其他用户）可以帮助你记住权限的命名方式。

上述访问权限有一个例外。任何知道 `root` 密码的人都可以以超级用户身份登录，并获得所有文件的完全访问权限，无论文件的所有者或访问权限如何。

## Setuid 和 Setgid 权限

当你执行具有 `setuid`（用户 ID）权限的文件时，执行该文件的进程将获得该文件的特权。执行具有 `setgid` 权限的文件时，执行该文件的进程将获得文件所属组的特权。

接下来 Alex 给了其他人访问其 `info` 目录的权限：

```bash
$ chmod o+r /home/alex/info
```

当 Jenny 检查她在 `info` 访问权限时，她发现自己对该目录拥有读取和执行权限。现在她可以像其他人那样工作，但仍然无法读取 `financial`。（此限制是文件权限问题，而不是目录权限。）最后，Jenny 尝试使用 `touch` 创建一个名为 `newbie` 的文件。如果 Alex 给了她 `info` 目录的写权限，Jenny 就能在其中创建新文件：

```bash
$ ls -id /home/alex/info

drw-xr-- 2 alex pubs 52 Aug 21 09:31 /home/alex/info

$ ls -l /home/alex/info

total 8

-rw------- 1 pubs 34 Aug 21 09:31 financial

-rw-r--r-- 1 pubs 30 Aug 21 09:32 notes

$ cat /home/alex/info/financial

cat: financial: Permission denied

$ touch /home/alex/info/newfile

touch: cannot touch '/home/alex/info/newfile': Permission denied
```

## ACLs: 访问控制列表

访问控制列表（ACL）相比传统的 Linux 权限（180），对哪些用户可以访问特定目录和文件提供了更细粒度的控制。使用 ACL，你可以指定多个用户访问目录或文件的特定方式。由于 ACL 可能会降低性能，不要在存放系统文件的文件系统中启用它们，在这些地方传统的 Linux 权限已经足够。在移动、复制或归档文件时也需要小心：并不是所有工具都会保留 ACL。此外，你无法将 ACL 复制到不支持 ACL 的文件系统中。

### 注意：大多数用户不会保留 ACL

在配合 `-p`（保留）或 `-a`（归档）选项使用时，`cp` 在复制文件时会保留 ACL。Red Hat Linux 提供的另一个保留 ACL 的工具是 `mv`。当你使用带有 `-p` 或 `-a` 选项的 `cp` 且无法复制 ACL 时（而在 `mv` 无法保留 ACL 的情况下），该工具会执行操作并发出错误消息：

```bash
$ mv report /tmp

mv: preserving permissions for /tmp/report: Operation not supported
```

其他工具如 `tar`、`cpio` 和 `dump` 不支持 ACL。你可以使用带有 `-a` 选项的 `cp` 来复制目录层次结构，包括 ACL。

你永远无法将 ACL 复制到不支持 ACL 或未启用 ACL 支持的文件系统中。

一个 ACL 由一组规则组成。规则指定了特定用户或组如何访问与该 ACL 关联的文件。规则有两种：访问规则和默认规则。（文档中提到了访问 ACL 和默认规则，尽管只有一种类型的 ACL：即一份 [ACL](https://example.org) 列表，一个 ACL 可以包含两种类型的规则。）

访问规则指定了单个文件或目录的访问信息。默认 ACL 仅属于目录；它为目录中任何没有显式 ACL 的文件指定默认访问信息（ACL）。

## 启用 ACLs

Red Hat Linux 在 `ext2` 和 `ext3` 文件系统上支持 ACL，尽管其他文件系统也提供了对 ACL 的长期支持。要在 `ext2` 或 `ext3` 文件系统上使用 ACL，必须使用 `acl` 选项（默认是 `no_acl`）挂载设备。例如，如果你想挂载由 `/home` 表示的目录，以便对 `/home` 中的文件使用 ACL，你可以在 `/etc/fstab` 的选项列表中添加 `acl`：

```bash
$ grep home /etc/fstab

LABEL=/home /home ext3 defaults.acl 1 2
```
