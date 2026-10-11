

## 删除文件和目录

```bash
[root@server1 root]# rm -f hosts2
[root@server1 root]# ls -F
Desktop/  myprogram*  myscript2*  proj_files/
[root@server1 root]_
```

要删除目录，可以使用 `rmdir` 命令；但是，`rmdir`（remove directory）命令只有在目录不包含任何文件时才会将其删除。若要删除目录及其内部的文件，必须使用 `rm` 命令并指定要删除的是一个包含文件的目录（`-r`）。正如之前所述，在使用 `cp` 命令复制目录时，需要使用递归选项（`-r`）；同样，若要删除一个装满文件的目录，也可以使用 `rm` 命令的递归选项（`-r`）。例如，如果 root 用户希望删除 `proj_files` 子目录及其内部的所有文件，且不希望系统提示确认每个文件的删除，则她必须使用 `rm -rf proj_files` 命令，如下例所示：

```bash
[root@server1 root]# ls -F
Desktop/  myprogram*  myscript2*  proj_files/
[root@server1 root]# rmdir proj_files
rmdir: `proj_files': Directory not empty
[root@server1 root]# rm -rf proj_files
[root@server1 root]# ls -F
Desktop/  myprogram*  myscript2*
[root@server1 root]_
```

> **提示**
> 在大多数命令中，例如 `rm` 和 `cp`，`-r` 和 `-R` 选项的含义相同（递归）。

> **注意**
> 如果对要递归删除的目录中实际存在哪些文件不确定，`rm` 命令的 `-r` 选项非常危险。因此，`rm` 命令的 `-r` 选项常被称为 `-resumé` 选项；如果你误用该选项，可能需要准备你的简历了。

需要注意的是，前述的文件管理命令被 Linux 用户、开发人员和系统管理员普遍使用。表 5-2 总结了这些常见的文件管理命令。

表 5-2 常见的 Linux 文件管理命令

| 命令 | 描述 |
| :--- | :--- |
| `mkdir` | 创建目录 |
| `rmdir` | 删除空目录 |
| `mv` | 移动/重命名文件和目录 |
| `cp` | 复制文件和包含大量文件的目录（配合 `-r` 选项） |
| `alias` | 显示 BASH shell 别名 |
| `rm` | 删除文件和包含大量文件的目录（配合 `-r` 选项） |

## 查找文件

在使用前一节提到的文件管理命令之前，必须知道所涉及文件的位置。在 Linux 目录树中查找文件最快的方法是使用 `locate` 命令，它是 `slocate`（或 secure locate）命令的快捷方式。例如，要查看根目录下所有文件名中包含单词“initab”（作为完整名称或一部分）的文件，只需在命令提示符下输入 `locate initab`，其输出如下：

```bash
[root@server1 root]# locate initab
/usr/share/terminfo/a/ansi+initab
/usr/share/vim/vim62/syntax/initab.vim
/usr/share/man/ja/man5/initab.5.gz
/usr/share/man/pl/man5/initab.5.gz
/usr/share/man/it/man5/initab.5.gz
/usr/share/man/man5/initab.5.gz
/usr/share/man/fr/man5/initab.5.gz
/usr/share/man/ko/man5/initab.5.gz
/etc/initab
[root@server1 root]# _
```

通常情况下，`locate` 命令返回的信息量过大，无法在屏幕上完全显示，因为它搜索的是文件系统上的所有文件。通常，可以使用 `more`（或 `less`）命令来暂停输出，例如 `locate initab | more`，或者确保被搜索的单词非常具体。`locate` 命令在一个预制的数据库中查找，该数据库包含系统上所有文件的列表。这个数据库的索引方式类似于教科书，以便于快速搜索，但随着文件的添加和移除（这是经常发生的情况），数据库可能会变得过时。因此，`locate` 命令使用的数据库（`/var/lib/locate/locate.db`）每天会自动更新，也可以在命令提示符下通过运行 `updatedb` 或 `slocate -u` 命令手动更新。

一种较慢但更通用的文件定位方法是在文件系统上使用 **`find` 命令**。`find` 命令不使用预制的文件索引，而是从特定目录开始，递归搜索目录树以找到满足特定条件的文件。`find` 命令的格式如下：

```text
find <起始目录> -条件 <要查找的内容>
```

例如，要在 `/etc` 目录下方查找名为 "inittab" 的任何文件，可以使用命令 `find /etc -name inittab`，输出如下：

```bash
[root@server1 root]# find /etc -name inittab
/etc/inittab
[root@server1 root]# _
```

也可以将通配符元字符与 `find` 命令一起使用；但是，这些通配符必须受到保护，以免被 shell 解释，因为它们只能由 `find` 命令解释。为此，确保任何通配符元字符都包含在引号字符内。以下是使用 `find` 命令配合通配符元字符查找 `/etc` 目录下所有以 "host" 开头的文件的示例输出：

```bash
[root@server1 root]# find /etc -name "host*"
/etc/hosts.deny
/etc/hosts.canna
/etc/log/scripts/shared/hostlist
/etc/ups/hosts.conf
/etc/hosts.allow
/etc/host.conf
/etc/hosts
[root@server1 root]# _
```

虽然按名称搜索是 `find` 命令最常用的条件，但还可以使用许多其他条件。要查找从 `/var` 目录开始、大小超过 4096K（千字节）的所有文件，可以使用以下命令：

```bash
[root@server1 root]# find /var -size +4096k
/var/log/lastlog
/var/lib/rpm/Packages
/var/lib/rpm/Filemacs
/var/lib/rpm/Basenames
/var/lib/canna/dic/canna.zipcode.ctd
/var/lib/imap/db/_db.004
/var/lib/slocate/slocate.db
[root@server1 root]# _
```

此外，如果只想查找 `/mnt` 目录下的所有目录，可以输入以下命令：

```bash
[root@server1 dev]# find /mnt -type d
/mnt
/mnt/floppy
/mnt/cdrom
[root@server1 root]# _
```

表 5-3 列出了与 `find` 命令配合使用的一些常见条件。

表 5-3 与 `find` 命令配合使用的常见条件

| 条件 | 描述 |
| :--- | :--- |
| `-amin -x` | 搜索 x 分钟前访问过的文件 |
| `-amin +x` | 搜索超过 x 分钟前访问过的文件 |
| `-atime -x` | 搜索 x 天前访问过的文件 |
| `-atime +x` | 搜索超过 x 天前访问过的文件 |
| `-empty` | 搜索空文件或目录 |
| `-fstype x` | 搜索位于特定文件系统 x 上的文件（x 可以是 ext2、ext3 等） |
| `-group x` | 搜索由特定组或 GID (x) 拥有的文件 |
| `-inum x` | 搜索 inode 编号为 x 的文件 |
| `-mmin -x` | 搜索 x 分钟内修改过的文件 |
| `-mmin +x` | 搜索超过 x 分钟内修改过的文件 |
| `-mtime -x` | 搜索 x 天内修改过的文件 |
| `-mtime +x` | 搜索超过 x 天内修改过的文件 |
| `-name x` | 搜索特定文件名 x（x 可以包含通配符） |
| `-regex x` | 使用正则表达式而不是通配符元字符搜索特定文件名 |
| `-size -x` | 搜索大小小于 x 的文件 |
| `-size x` | 搜索大小等于 x 的文件 |
| `-size +x` | 搜索大小大于 x 的文件 |
| **`-type x`** | 搜索类型为 x 的文件，其中 x 可以是： |
| - | `b` 表示块文件 |
| - | `c` 表示字符文件 |
| - | `d` 表示目录文件 |
| - | `p` 表示命名管道 |
| - | `f` 表示常规文件 |
| - | `l` 表示符号链接（快捷方式） |
| - | `s` 表示套接字 |
| **`-user x`** | 搜索由特定用户或 UID (x) 拥有的文件 |

虽然 *find* 命令可以根据许多条件搜索文件，但如果被搜索的目录和文件数量很大，完成搜索可能需要几分钟。为了减少搜索所需的时间，尽可能通过指定子目录来缩小搜索范围。与搜索 `/usr` 目录及其所有子目录相比，搜索 `/usr/local/bin` 目录及其子目录所需的时间更短。此外，如果要查找的文件名是可执行文件，那么通常可以使用 **`which`** 命令更快地找到它。*which* 命令只搜索当前 BASH shell 中名为 **PATH** 变量的特殊变量中列出的目录。在探讨 *which* 命令之前，必须理解 PATH 的用法。

可执行文件可以存储在目录树中分散的各个目录中。回顾 FHS 可知，大多数可执行文件存储在名为 `bin` 或 `sbin` 的目录中，但在典型的 Red Hat Linux 安装完成后，目录树中散落着 20 多个 `bin` 和 `sbin` 目录。为了确保用户在执行 *ls* 这样的命令（即可执行文件 `/bin/ls`）时无需指定完整的路径名，存在一个名为 **PATH** 的特殊变量，每当用户登录到 Linux 系统时，该变量会被放入内存中。回顾一下，可以使用 `$` 元字符配合 *echo* 命令来查看内存中某个变量的内容：

```bash
[root@server1 root]# echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin:/usr/X11R6/bin:/root/bin
[root@server1 root]# _
```

**PATH** 变量列出了当在命令行执行命令时未指定相对路径或绝对路径的情况下，用于搜索可执行文件的目录。在上面的输出中，当用户在命令行输入 *ls* 命令并按下 Enter 键时，系统会识别出该命令既不是绝对路径名（例如，`/bin/ls`）也不是相对路径名（例如，`../bin/ls`），然后开始在 `/usr/kerberos/sbin` 目录中查找 *ls* 可执行文件，接着在 `/usr/kerberos/bin` 目录中查找，然后是 `/usr/local/sbin`

