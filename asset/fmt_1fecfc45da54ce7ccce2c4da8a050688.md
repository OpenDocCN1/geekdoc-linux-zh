
```bash
[root@server1 ~]# find /var -size +4096k
/var/lib/rpm/Packages
/var/lib/rpm/Basenames
/var/lib/PackageKit/system.package-list
/var/log/journal/034ec8ccdf4642f7a2493195e11d7df6/user-1000.journal
/var/log/journal/034ec8ccdf4642f7a2493195e11d7df6/user-42.journal
/var/log/journal/034ec8ccdf4642f7a2493195e11d7df6/system.journal
/var/cache/yum/x86_64/20/updates/gen/prestdelta.xml
/var/cache/yum/x86_64/20/updates/gen/primary_db.sqlite
/var/cache/yum/x86_64/20/updates/gen/filelists_db.sqlite
/var/cache/yum/x86_64/20/updates/gen/other_db.sqlite
/var/cache/yum/x86_64/20/updates/gen/updatelistsfo.xml
/var/cache/dnf/x86_64/20/fedora-filenames.solvx
/var/cache/dnf/x86_64/20/fedora.solv
/var/cache/dnf/x86_64/20/fedora-filenames.solvx
/var/tmp/kdecache-user1/plasma_theme_interral-system-colors.kcache
/var/tmp/kdecache-user1/plasma_theme_Heisenbug_v19.90.2.kcache
/var/tmp/kdecache-user1/icon-cache.kcache
[root@server1 ~]# 
```

此外，如果你只想查找 `/boot` 目录下的所有目录，可以输入以下命令：

```bash
[root@server1 ~]# find /boot -type d
/boot
/boot/lost+found
/boot/grub2
/boot/grub2/locale
/boot/grub2/themes
/boot/grub2/themes/suse
/boot/grub2/i386-pc
/boot/grub2/fonts
/boot/extlinux
/boot/efi
/boot/efi/Efi
/boot/efi/EFI/BOOT
/boot/efi/EFI/fedora
/boot/efi/EFI/fedora/fonts
/boot/efi/efi/System
/boot/efi/efi/System/Library
/boot/efi/efi/System/Library/CoreService
[root@server1 ~]# 
```

表 4-3 提供了一些常用于 `find` 命令的常见标准列表。

| 标准 | 描述 |
|---|---|
| `-amin -x` | 搜索少于 `x` 分钟前访问的文件 |
| `-amin +x` | 搜索多于 `x` 分钟前访问的文件 |
| `-atime -x` | 搜索少于 `x` 天前访问的文件 |
| `-atime +x` | 搜索多于 `x` 天前访问的文件 |
| `-empty` | 搜索空文件或目录 |
| `-fstype x` | 搜索位于特定文件系统 `x` 上的文件（其中 `x` 可以是 `ext2`、`ext3` 等） |
| `-group x` | 搜索属于特定组或 `GID (x)` 的文件 |
| `-inum x` | 搜索 `inode` 编号为 `x` 的文件 |
| `-mmin -x` | 搜索少于 `x` 分钟前修改的文件 |
| `-mmin +x` | 搜索多于 `x` 分钟前修改的文件 |
| `-mtime -x` | 搜索少于 `x` 天前修改的文件 |
| `-mtime +x` | 搜索多于 `x` 天前修改的文件 |
| `-name x` | 搜索特定的文件名 `x`（`x` 可以包含通配符） |
| `-regex x` | 使用正则表达式而非通配符元字符搜索特定文件名 |
| `-size -x` | 搜索小于 `x` 大小的文件 |
| `-size x` | 搜索大小为 `x` 的文件 |
| `-size +x` | 搜索大于 `x` 大小的文件 |
| `-type x` | 搜索类型 `x` 的文件，其中 `x` 为：<br>• `b` 表示块文件<br>• `c` 表示字符文件<br>• `d` 表示目录文件<br>• `p` 表示命名管道<br>• `f` 表示常规文件<br>• `l` 表示符号链接（快捷方式）<br>• `s` 表示套接字 |
| `-user x` | 搜索由特定用户或 `UID (x)` 拥有的文件 |

虽然 `find` 命令可以基于许多标准搜索文件，但如果要搜索的目录和文件数量庞大，完成搜索可能需要几分钟时间。为了减少搜索所需时间，尽可能通过指定子目录来缩小搜索的目录范围。与搜索 `/usr` 目录及其所有子目录相比，搜索 `/usr/local/bin` 目录及其子目录所需的时间更少。此外，如果你要搜索的文件名是可执行文件，使用 `which` 命令通常可以在更短的时间内找到该文件。`which` 命令只搜索当前 `BASH Shell` 中名为 `PATH` 的特殊变量中列出的目录。在深入了解 `which` 命令之前，你必须理解 `PATH` 的用法。

可执行文件可以存储在目录树中分散的各个目录中。回想一下 `FHS`（文件系统层次结构标准），大多数可执行文件存储在某些名为 `bin` 或 `sbin` 的目录中，但在典型的 `Fedora Linux` 安装之后，目录树中分散着 20 多个 `bin` 和 `sbin` 目录。为了确保用户不需要指定如 `ls` 等命令的完整路径名（即可执行文件 `/usr/bin/ls` 的路径），存在一个名为 `PATH` 的特殊变量，它在用户每次登录 `Linux` 系统时都被放入内存中。回想一下，你可以使用 `$` 元字符与 `echo` 命令来查看内存中某个变量的内容：

```bash
[root@server1 ~]# echo $PATH
/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin
[root@server1 ~]# 
```

`PATH` 变量列出了当在命令行执行命令时未指定相对路径名或绝对路径名时，用于搜索可执行文件的目录。在前面的输出中，当用户在命令行输入 `ls` 命令并按下回车键时，系统会识别出该命令不是绝对路径名（例如 `/usr/bin/ls`）或相对路径名（例如 `../usr/bin/ls`），然后开始在 `/usr/local/sbin` 目录中查找 `ls` 可执行文件，接着是 `/usr/local/bin` 目录，然后是 `/usr/sbin` 目录，依此类推。如果搜索了 `PATH` 变量中的所有目录且未找到 `ls` 命令，`Shell` 会向用户显示错误消息，指出未找到该命令。在前面的输出中，`/usr/bin` 目录在 `PATH` 变量中，因此 `ls` 命令会被找到并执行，但在此之前必须先搜索 `PATH` 变量中位于其前的目录。

要搜索 `PATH` 变量中的目录以查找名为“grep”的文件，可以将单词“grep”作为 `which` 命令的参数，得到以下输出：

```bash
[root@server1 ~]# which grep
alias grep='grep --color=auto'
/usr/bin/grep
[root@server1 ~]# 
```

如前一个输出所示，`which` 命令还会列出特定命令的任何命令别名。在我们的示例中，`grep` 命令的路径是 `/usr/bin/grep`，但它还有一个别名，确保每次用户运行 `grep` 命令时，都会使用 `--color=auto` 选项运行。

如果要在 `PATH` 变量的目录中搜索不存在的文件，`which` 命令会告知你该文件在哪些目录中未找到，如下面的输出所示：

```bash
[root@server1 ~]# which grepper
/usr/bin/which: no grepper in
(/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/root/bin)
[root@server1 ~]# 
```

除了 `locate`、`find` 和 `which` 之外，还有许多不同的命令可用于在文件系统上搜索文件。例如，`whereis` 是 `find` 的简化版本。

![](img/c27875544958897d817484d558c208c8_175_0.png)

## 链接文件

文件可以通过两种方式相互链接。在**符号链接**（或软链接）中，一个文件是另一个文件的指针或快捷方式。在**硬链接**中，两个文件共享相同的数据。

为了更好地理解文件如何链接，你必须了解文件在文件系统上是如何存储的。在结构层面，文件系统有三个主要部分：超级块（`superblock`）、`inode` 表和数据块（`data blocks`）。

**超级块**是包含文件系统总体信息的部分，例如 `inode` 和数据块的数量，以及每个数据块存储多少数据（以千字节为单位）。**inode 表**由几个 `inode`（信息节点）组成；每个 `inode` 描述文件系统中的一个文件或目录，并包含一个唯一的 `inode` 编号用于识别。更重要的是，`inode` 存储诸如文件大小、数据块位置、最后修改日期、权限和所有权等信息。当文件被删除时，只有其 `inode`（作为指向实际数据的指针）被删除。构成文件内容的实际数据以及文件名存储在**数据块**中，这些数据块由 `inode` 引用。在独立于文件系统的术语中，块被称为分配单元，因为它们是磁盘空间分配存储的单位。

每个文件和目录都必须有一个 `inode`。除特殊设备文件外，所有文件也有与 `inode` 关联的数据块。特殊设备文件在第 5 章中讨论。

![](img/c27875544958897d817484d558c208c8_175_1.png)

回想一下，目录仅仅是用于组织其他文件的文件；它们也有 `inode` 和数据块，但其数据块包含位于该目录内的文件名列表。

![](img/c27875544958897d817484d558c208c8_175_2.png)

硬链接文件共享同一个 `inode`。因此，它们共享相同的 `inode` 编号和数据块，但数据块允许多个文件名。因此，当一个硬链接文件被修改时，其他硬链接文件也会随之更新。这种关系

### 图 4-1 硬链接文件的结构

![](img/c27875544958897d817484d558c208c8_176_0.png)

硬链接文件可以在图 4-1 中看到。你可以无限次地为文件创建硬链接；但是，硬链接文件必须位于同一个文件系统上。

要创建硬链接，你必须使用 `ln` 命令并指定两个参数：要创建硬链接的现有文件和将作为现有文件的硬链接创建的目标文件。每个参数可以是文件的绝对路径或相对路径。以根用户主目录的以下内容为例：

```bash
[root@server1 ~]# ls -l
total 520
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--r-x 1 root root 519964 Apr 7 09:59 file1
-rw-r--xr-x 1 root root 1244 Apr 27 18:17 file3
[root@server1 ~]# _
```

假设你想要为 `file1` 创建一个硬链接，并将新的硬链接命名为 `file2`，如图 4-1 所示。为了实现这一点，你需要在命令提示符处输入命令 `ln file1 file2`；名为 `file2` 的文件将被创建，并与 `file1` 硬链接。要在创建后查看硬链接的文件名，你可以使用 `ls -l` 命令：

```bash
[root@server1 ~]# ln file1 file2
[root@server1 ~]# ls -l
total 1032
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--r-x 1 root root 519964 Apr 7 09:59 file1
-rw-r--xr-x 2 root root 519964 Apr 7 09:59 file2
-rw-r--xr-x 1 root root 1244 Apr 27 18:17 file3
[root@server1 ~]# _
```

从上面的长列表中可以看出，`file1` 和 `file2` 共享同一个 `inode` 和数据段，因为它们具有相同的大小、权限、所有权、修改日期等。还要注意，`file1` 的链接数（权限组后面的数字）在上面的输出中从 1 增加到了 2。链接数为 1 表示只有一个 `inode` 由文件共享。如果一个文件与另一个文件硬链接，则共享两个 `inode`，因此其链接数为 2。类似地，一个文件如果与另外三个文件硬链接，则共享四个 `inode`，因此其链接数为 4。

尽管硬链接共享同一个 `inode` 和数据段，但删除一个硬链接文件并不会删除其他所有硬链接文件；它只是移除一个文件名引用。删除硬链接可以通过移除其中一个文件来实现，这会导致链接数降低。

要查看硬链接文件的 `inode` 编号以验证它们是否相同，除了其他选项外，你还可以使用 `ls` 命令的 `-i` 选项。`inode` 编号位于目录列表中每一行的左侧，如下面的输出所示：

```bash
[root@server1 ~]# ls -li
total 1032
37595 drwx------ 3 root root 4096 Apr 8 07:12 Desktop
1204 -rwxr-xr-x 2 root root 519964 Apr 7 09:59 file1
1204 -rwxr-xr-x 2 root root 519964 Apr 7 09:59 file2
17440 -rwxr-xr-x 1 root root 1244 Apr 27 18:17 file3
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_177_0.png)

> 目录文件通常不会被硬链接，因为结果将包含两个内容相同的目录。然而，在某些情况下，`root` 用户可以使用 `ln` 命令的 `-F` 或 `-d` 选项来硬链接目录。通常只有那些经常添加文件且需要保持相同文件内容的目录才会被硬链接。例如，在 `Fedora 20` 中，`/etc/init.d` 目录被符号链接到 `/etc/rc.d/init.d` 目录。

符号链接（如图 4-2 所示）与硬链接不同，因为它们不与其目标文件共享相同的 `inode` 和数据块；一个是另一个的指针，因此两个文件具有不同的大小。符号链接文件中的数据块仅包含目标文件的路径名。当用户编辑符号链接文件时，实际上是在编辑目标文件。因此，如果目标文件被删除，符号链接将不起作用，因为它指向一个不存在的文件。

![](img/c27875544958897d817484d558c208c8_177_1.png)

> 符号链接有时被称为“软链接”或“symlinks”。

要创建符号链接，你需要使用 `ln` 命令的 `-s` 选项。要创建一个指向 `file3` 的名为 `file4` 的符号链接，如图 4-2 所示，你可以在命令提示符处输入 `ln -s file3 file4`。与硬链接一样，指定的参数可以是绝对路径或相对路径。

![](img/c27875544958897d817484d558c208c8_177_2.png)

### 图 4-2 符号链接文件的结构

要在创建后查看符号链接的文件名，你可以使用 `ls -l` 命令，如下面的示例所示：

```bash
[root@server1 ~]# ls -l file3 file4
[root@server1 ~]# ls -l
total 1032
drwx------   3 root  root     4096 Apr  8 07:12 Desktop
-rwxr-xr-x   2 root  root    519964 Apr  7 09:59 file1
-rwxr-xr-x   2 root  root    519964 Apr  7 09:59 file2
-rwxr-xr-x   1 root  root      1244 Apr 27 18:17 file3
lrwxrwxrwx   1 root  root        5 Apr 27 19:05 file4 -> file3
[root@server1 ~]# _
```

从上面的输出中可以看出，`file4` 不共享相同的 `inode`，因为其权限、大小和修改日期与 `file3` 不同。此外，符号链接比硬链接更容易识别；文件类型字符（在权限之前）是 `l`，表示这是一个符号链接，并且文件名使用箭头指向目标。`ls -F` 命令还通过附加一个 `@` 符号来指示符号链接，如下面的输出所示：

```bash
[root@server1 ~]# ls -F
Desktop/  file1*  file2*  file3*  file4@
[root@server1 ~]# _
```

硬链接和符号链接之间的另一个区别在于，符号链接不需要与其目标位于同一个文件系统上。相反，它们指向目标文件名，并且不需要相同的 `inode`，如下面的输出所示：
