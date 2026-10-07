
`/boot/lost_found`

`/boot/grub`

`/boot/grub2/fonts`

`/boot/efi`

`/boot/efi/BOOT`

`/boot/efi/fedora`

`/boot/efi/System`

`/boot/efi/CoreServices`

`/boot/loader`

`[root@server1 ~]#`

## 表 4-3 find 命令常用的标准

| 标准 | 说明 |
| --- | --- |
| -amin -x | 搜索访问小于 x 分钟的文件 |
| -amin +x | 搜索访问超过 x 分钟的文件 |
| -atime -x | 搜索访问小于 x 天的文件 |
| -atime +x | 搜索访问超过 x 天的文件 |
| -empty | 搜索空文件或目录 |
| -fst x | 在文件系统中搜索（x 可以是 ext2, ext3 等） |
| -group x | 搜索属于组或 GID (x) 的文件 |
| -inum x | 搜索 inode 号为 x 的文件 |
| -mmin -x | 搜索修改小于 x 分钟的文件 |
| -mmin +x | 搜索修改超过 x 分钟的文件 |
| -mtime -x | 搜索修改小于 x 天的文件 |
| -mtime +x | 搜索修改超过 x 天的文件 |
| -name x | 搜索特定文件名（x 可以包含通配符） |
| -regex x | 使用正则表达式而非通配符搜索特定文件名 |
| -size x | 搜索大小小于 x 的文件 |
| -size +x | 搜索大小大于 x 的文件 |
| -type x | 搜索类型为 x 的文件 |
| b | 块设备文件 |
| c | 字符文件 |
| d | 目录文件 |
| p | 命名管道 |
| l | 符号链接（快捷方式） |
| s | 套接字 |
| -user x | 搜索属于用户或 UID (x) 的文件 |

`find` 命令可用于许多标准搜索文件，如果搜索的目录和文件很多，搜索可能需要几分钟。为了缩短搜索时间，在搜索 `/usr/local/bin` 及其子目录时指定指定目录，与搜索 `/` 相比。如果你正在搜索可执行文件，使用 `which` 命令可能更快找到文件。在执行前应设置环境变量 `PATH` 以理解 `PATH` 的用法。可执行文件存储在目录树中。大多数可执行文件存储在 `bin` 目录周围，但在 Fedora 安装后不需要搜索目录树周围。为了确保用户指定以下命令：

## 第 4 章 文件系统管理

`which` 是可执行文件 `/usr/bin/ls`，一个特殊变量 `PATH` 被于用户登录 Linux shell 的内存中。你可以通过 `echo` 命令查看内存中的变量：

```
[root@server1 ~]# echo $PATH

/root/local/bin:/root/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin

[root@server1 ~]#
```

`PATH` 变量列出了在命令行执行命令未指定绝对路径时搜索的目录。假设 `PATH` 变量按顺序定义，如果用户在命令行使用 `ls` 命令并按回车，系统识别出该命令不是绝对路径（例如 `/usr/bin/ls`）或相对路径（例如 `../usr/bin/ls`），然后在 `/root/local/bin` 目录中查找可执行文件，然后是 `/root/local/sbin` 目录，接着是 `/usr/local/bin` 目录，然后是 `/usr/sbin` 目录，最后是 `/usr/bin`。如果搜索了 `PATH` 变量中的所有目录都没有找到命令，shell 会向用户给出未找到命令的错误信息。在这里，`/usr/bin` 目录在 `PATH` 变量中，`ls` 命令被执行，但没有搜索 `PATH` 变量中的之前的目录。

要列出 `PATH` 变量中文件 "grep" 的目录，可以使用 "grep" 命令并接收如下输出：

```
[root@server1 ~]# alias grep

alias grep='--color=auto'

which grep

[root@server1 ~]#
```

如前面的输出所示，命令还会列出特定命令的任何别名。在本例中，`grep` 命令路径为 `/usr/bin/grep`，但它还有一个别名确保用户每次运行 `grep` 时都使用 `--color=auto` 运行。

如果搜索的文件在 `PATH` 目录中不存在，命令将告诉你在哪些目录中没有找到，如下输出所示：

```
[root@server1 ~]# which grep

/usr/bin/which: no grepper in (/root/local/bin:/root/local/sbin:/usr/sbin:/usr/bin)

[root@server1 ~]#
```

该命令有两个替代方案：`type` 命令显示 `which` 命令通常输出的第一个位置，而 `where` 命令显示命令的位置以及任何帮助页和信息，如下输出所示：

```
[root@server1 ~]# type grep

grep is aliased to '--color=auto'

[root@server1 ~]# whereis grep

grep:/usr/bin/grep /usr/share/man/man1/grep.1.gz

/usr/share/man/man1/grep.info.gz /usr/share/info/grep.info

[root@server1 ~]#
```

## 链接文件

文件可以用一种或两种方式链接。符号链接是一个电子文件，指向另一个被从祖先抑制的文件（见 X 章）。要命名，硬链接共享相同的数据。

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

为了更好地理解文件是如何链接的，你必须理解文件是如何存储在文件系统中。从结构上来说，文件系统三个三个部分：

- 超块 (Superblock)
- Inode 表 (Inode table)
- 数据块 (Data blocks)

超块是包含文件系统信息的区域，例如 inode 和数据块的数量，以及数据块以 KB 为单位存储的数据。Inode 表由多个 inode（信息节点）组成；每个 inode 描述文件系统上的一个文件或目录，并包含一个唯一的标识数字。重要的是，inode 存储了文件大小、数据位置、最后修改时间、权限和所有者等信息。当文件被删除时，只有 inode（作为指向实际数据的指针）被删除。组成文件内容和文件名存储在数据块中，由 inode 引用。在与文件系统无关的术语中，块被称为分配单位，是分配磁盘空间存储的单位。

> 注意：每个文件和目录必须有一个 inode。除了特殊设备外，所有文件都具有与 inode 关联的数据块。特殊设备文件将在第 5 章中讨论。

> 注意：回想一下，目录只是用于组织其他文件的文件；它们拥有 inode 和数据块，但其数据块包含位于目录内的文件名列表。

硬链接文件共享相同的 inode 和 inode 号。因此，它们共享相同的 inode 号和数据块，但数据块允许存在多个文件名。那么，当修改一个硬链接文件时，其他硬链接文件也会同步更新。硬链接文件之间的这种关系如图 4-1 所示。你可以对一个文件进行无限次链接；但硬链接文件必须位于同一个文件系统中。

**图 4-1** 硬链接文件的结构

| INODE | DATA BLOCKS |
| --- | --- |
| Inode 号: 1204 | |

要创建一个硬链接，你必须使用 `ln` (link) 命令并指定两个参数：要链接的现有文件和将创建的作为现有文件硬链接的目标文件。每个参数可以是文件的绝对路径或相对路径。例如，root 用户主目录的内容：

```
[root@server1 ~]# ls -l

total 520

drwx--xr-x 3 root 4096 8 07:12 Desktop

-rwxr-xr-x 1 root 519964 7 Apr 09:59:21 file2

-rwxr-xr-x 1 root 1224 27 Apr 18:17 file3

[root@server1 ~]#
```

## 第 4 章 Linux 文件系统管理

假设你想对 file1 和新的硬链接文件 file2 创建硬链接。要实现这一点，你在命令提示符处输入 `ln file1 file2`；会创建一个名为 file2 的文件并将其与 file1 硬链接。要查看硬链接文件名的创建，可以使用 `ls -1` 命令：

```
[root@server1]# ln file1 file2

[root@server1]# ls -1

total 1032

drw---r-- 3 root root 4096 Apr 8 07:12 Desktop

-rwrw-xr-x 2 root root 519964 Apr 7 09:59 file1

-rwrw-xr-x 2 root root 519964 Apr 7 09:59 file2

-rwrw-xr-x 1 root root 1224 Apr 27 18:17 file3

[root@server1]#
```

注意随后的列表显示 file1 和 file2 共享相同的 inode 和数据，因为它们具有相同的大小、权限、修改日期等。此外，file1（权限权限集下方）的链接计数（link count）在之前的条目中从一增加到了二。链接计数表示该文件仅报告了一个 inode。与另一个文件硬链接的文件共享两个 inode，因此链接计数为二。同样，与三个其他文件硬链接的文件共享四个 inode，因此链接计数为四。

尽管硬链接共享相同的 inode 和数据，但删除一个硬链接不会删除所有其他硬链接文件；它只是删除了一个引用。删除硬链接可以通过删除其中一个文件来实现，这会降低链接计数。要验证它们是否相同，除了使用任何其他选项外，你还可以在 `ls` 命令中配合 `-i` 选项。inode 号位于每行目录的左侧，如下所示：

```
[root@server1]# ls -i

total 1032

drw---r-- 3 root root 4096 Apr 8 07:12 Desktop

1204-rwrw-xr-x 2 root root 519964 Apr 7 09:59 file1

1204-rwrw-xr-x 2 root root 519964 Apr 7 09:59 file2

17440-rwrw-xr-x 1 root root 1224 Apr 27 18:17 file3

[root@server1]#
```

> 注意：在 Linux 系统上，目录文件通常不硬链接，因为结果将包含两个目录。然而，root 有能力使用 `ln` 命令的 `-F` 或 `-d` 选项硬链接目录。符号链接（如图 4-2 所示）与硬链接不同，它们不与目标共享相同的 inode 和数据；一个是另一个的指针，因此两个文件的大小不同。符号链接中的数据块仅包含指向目标的路径。当用户编辑符号链接时，实际上是在编辑目标文件。因此，如果目标文件被删除，符号链接将失效，因为它指向一个不存在的文件。

> 注意：符号链接有时被称为“软链接”（soft links）或“symlinks”。

**图 4-2** 符号链接文件的结构

| FILE3 | |
| --- | --- |
| **INODE** | **DATA BLOCKS** |
| inode 号: 17440 | |

| FILE4 | |
| --- | --- |
| **INODE** | **DATA BLOCKS** |
| inode 号: 19926 | |

要创建一个符号链接，使用 `ln` 命令中的 `-s` 选项。例如，要创建一个名为 file4 的符号链接，可以在命令提示符输入 `ln -s file3 file4`。与硬链接一样，指定的参数可以是绝对路径或相对路径。查看创建后的符号链接，可以使用 `ls -l` 命令，如下：

```
[root@server1]# ln -s file3 file4

[root@server1]# ls -l

total 1032

drwxr-xr-x 3 root 4096 Apr 8 07:12 Desktop

-lrwxr-xr-x 2 root root 519964 Apr 7 09:59 file1

-lrwxr-xr-x 2 root root 519964 Apr 7 09:59 file2

-lrwxr-xr-x 1 root root 1224 Apr 27 18:17 file3

-lrwxrwxr-wx 1 root root Apr 27 19:05 file4 -> file3

[root@server1]#
```

注意前面的输出，file4 不共享相同的 inode，因为其权限、大小和修改日期与文件不同。此外，符号链接比硬链接更容易识别；文件名前的类型字符为 `l`，表示符号链接，`ls -F` 命令通过附加 `@` 符号也指示符号链接，如下：

```
[root@server1]# ls -F

Desktop/ file1* file2* file3* file4@

[root@server1]#

total 1032

drwxr-xr-x 3 root 4096 Apr 8 07:12 Desktop

-lrwxr-xr-x 2 root root 519964 Apr 7 09:59 file1

-lrwxr-xr-x 2 root root 519964 Apr 7 09:59 file2

-lrwxr-xr-x 1 root root 1224 Apr 27 18:17 file3

-lrwxrwxr-wx 1 root root Apr 27 19:05 file4 -> file3

[root@server1]#
```

硬链接和符号链接之间的另一个区别是，符号链接不需要与目标位于同一个文件系统中。相反，它们指向目标文件名，不需要相同的 inode 号，如下所示：

> 注意：与硬链接不同，符号链接通常用于目录以简化文件系统树。此外，目录的符号链接通常用于维护与其他 UNIX 和 Linux 系统的 FHS 兼容性。例如，在 Fedora Linux 上，由于这个原因，`/usr/tmp` 目录符号链接到 `/var/tmp` 目录。

## 文件和目录权限

回想所有用户必须使用用户名和密码登录 Linux 系统。登录后，通过用户名和组身份识别用户；对资源的访问访问取决于用户和组是否具有所需的权限。深入理解所有权和权限对于安全地运行 Linux 以及防止未经授权的用户访问敏感文件、目录和命令是必要的。

## 文件和目录所有权

当用户创建文件或目录时，他们的用户名和主组分别成为文件的所有者和组所有者，这影响了权限结构，正如下一节所示；但也决定了谁有能力修改文件和目录权限。只有 Linux 系统上的用户可以修改文件的权限或更改其所有权：文件的所有者或 root。查看当前用户可以使用 `whoami`。查看你的组身份和主组，可以使用 `groups`。以 root 身份登录这两个命令的示例如下：

```
[root@server1]# whoami

root

[root@server1]# groups

root bin daemon sys disk wheel

[root@server1]#
```

> 注意：在 Fedora Linux 上，root 用户默认只是一个组的成员（"root" 组）。

如果 root 用户创建一个文件，所有者是 "root"，组所有者也是 "root"。要快速创建一个空文件，可以使用 `touch` 命令：

```
[root@server1]# touch file1

[root@server1]# ls -l

total 4

drw-xr-r-- 3 root root 4096 Apr 8 07:12 Desktop

-rw-r--r-- 1 root root 0 Apr 29 15:40 file1

[root@server1]#
```

> 注意：虽然 touch 命令的主要目的是是将现有文件的修改日期更新为当前时间，但如果指定的文件不存在，它可以创建一个新文件。

## CompTIA Linux+ 与 LPIC-1：Linux 认证指南

从前一个输出中可以看出，文件的所有者是 "root"，组所有者是 "root" 组。要更改文件或目录的所有权，你可以使用 `chown`（更改所有者）命令，该命令接受两个参数：新所有者以及文件或目录。两者都可以是绝对路径或相对路径，你还可以通过 `chown` 命令的 `-R` 选项递归地更改整个目录树的权限。要将文件的所有者更改为新用户，并将 Desktop 及其所有内容的组所有者更改为 user1，你可以输入以下命令：

```
[root@server1 ~]# chown user1 file

[root@server1 ~]# chown -R Desktop

[root@server1 ~]# ls -l

total 4

drwxr-xr-x 3 user root 4096 Apr 8 07:12 Desktop

-rw-r--r-- 1 user root 0 Apr 29 15:40 file

-rw-r--r-- 1 user root 163 Mar 29 09:58 Work

-rw-r--r-- 1 user root 3578 Mar 29 09:58 Home

-rw-r--r-- 1 user root 1791 Mar 29 09:58 Start Here

drwxr-xr 2 user root 4096 Mar 29 09:58 Trash

[root@server1 ~]#
```

请记住，文件或目录的所有者可以更改特定文件或目录的所有权。如果用户更改了他们所拥的文件或目录的所有权，你将无法找回所有权；该文件或目录的新所有者必须将其更改回原始用户。然而，root 用户始终具有重新夺回所有权的能力：

```
[root@server1 ~]# chown root file
```
