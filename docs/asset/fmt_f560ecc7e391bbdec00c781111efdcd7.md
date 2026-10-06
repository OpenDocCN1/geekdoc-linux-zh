
表 5-3 列出了用于 `find` 命令的一些常用准则列表。

## 表 5-3 用于 `find` 命令的常用准则

| 准则 | 说明 |
| - | - |
| `-amin -x` | 搜索在 x 分钟内访问过的文件 |
| `-amin +x` | 搜索在 x 分钟前访问过的文件 |
| `-atime -x` | 搜索在 x 天内访问过的文件 |
| `-atime +x` | 搜索在 x 天前访问过的文件 |
| `-empty` | 搜索空文件或目录 |
| `-fype x` | 如果文件在特定的文件系统上（n 可以是 ext2, ext3 等），则搜索该文件 |
| `-group x` | 搜索属于特定组或 GID (x) 的文件 |
| `-inum -x` | 搜索 inode 编号为 x 的文件 |
| `-mmin -x` | 搜索在 x 分钟内修改过的文件 |
| `-mmin +x` | 搜索在 x 分钟前修改过的文件 |
| `-mtime -x` | 搜索在 x 天内修改过的文件 |
| `-mtime +x` | 搜索在 x 天前修改过的文件 |
| `-name x` | 搜索特定的文件名（x 可以包含通配符） |
| `-regexp x` | 使用正则表达式而非通配符元字符搜索特定的文件名 |
| `-size -x` | 搜索大小小于 x 的文件 |
| `-size x` | 搜索大小为 x 的文件 |
| `-size +x` | 搜索大小大于 x 的文件 |

# 第 5 章 LINUX 文件系统管理

| 表 5-3 用于 `find` 命令的常用准则（续） |
| 准则 | 说明 |
| --- | --- |
| `-type x` | 搜索类型为 x 的文件，其中 x 为：<br>◆ b 表示块文件<br>◆ c 表示字符文件<br>◆ d 表示目录文件<br>◆ p 表示命名管道<br>◆ f 表示普通文件<br>◆ l 表示符号链接（快捷方式）<br>◆ s 表示套接字 |
| `-user x` | 搜索属于特定用户或 UID (x) 的文件 |

虽然可以使用 `find` 命令根据许多标准搜索文件，但如果被搜索的目录和文件数量很大，可能需要几分钟才能完成搜索。为了减少缩小目录树的时间，尽可能通过子目录进行搜索。搜索 `/usr/local/bin` 目录及其子目录所需的时间更少。同样，如果你搜索的文件名是一个可执行文件，使用 `which` 命令可能可以在更短时间内找到该文件。`which` 命令只搜索 Bash Shell 中名为 `PATH` 的特殊变量列出的目录。在探索 `which` 命令之前，你必须理解 `PATH` 的用法。

可执行文件存储在分散在目录树中的目录中。回想 FHS（文件层次结构），在典型的 Red Hat Linux 安装后，大多数可执行文件存储在分散在目录树中的目录中。为了确保用户不需要为像 `ls`（它是可执行文件 `/bin/ls`）这样的命令指定完整路径，存在一个名为 `PATH` 的特殊变量，每当用户登录 Linux 系统时都会被放入内存。回想一下，你可以使用 `echo` 命令配合元字符 `$` 查看内存中变量的内容：

```
[server1 root]# echo $PATH
/usr/kerberos/sbin:/usr/kerberos/bin:/usr/local/sbin:/usr/local/bin:/sbin:/usr/bin:/bin:/usr/sbin/X11R6:/root/bin #
[server1 root]# _
```

`PATH` 变量列出了当在命令行上执行命令时未指定相对或绝对路径时，系统将搜索可执行文件的目录。在先述输出中，当用户在命令行上输入 `ls` 命令并按回车时，系统识别出该命令不是绝对路径（例如 `/bin/ls`）或相对路径（例如 `../bin/ls`），然后在在 `/usr/kerberos/sbin` 目录中查找 `ls` 可执行文件，然后 `/usr/kerberos/bin` 目录，接着是 `/usr/local/sbin` 目录，依此类推。如果 `PATH` 变量中的所有目录都搜索完毕仍未找到 `ls` 命令，shell 将向用户发送错误消息，说明未找到命令。在先述输出中，`/bin` 目录在 `PATH` 变量中，因此找到了 `ls` 命令并执行，但是在先搜索了 `PATH` 变量中之前的目录之后。

要在 `PATH` 变量的目录中搜索名为 "grep" 的文件，你可以将 "grep" 作为 `which` 命令的参数并接收以下输出：

```
[root@server1 sbin]# which grep
/bin/grep
[root@server1 root]# _
```

如果搜索的文件在 `PATH` 变量目录中不存在，`which` 会告诉你它在目录中未找到，如下输出所示：

```
[root@server1 sbin]# which grepper
/usr/bin/which: no grepper in (/usr/kerberos/sbin:/usr/kerberos:bin:/usr/local/sbin:usr/local/bin:/sbin:/bin:/usr/sbin:X11R6/bin:root)
[root@server1]# _
```

### 文件链接

回想文件可以链接到彼此。这种链接发生在两种方式之一：一个文件可能是另一个文件的指针或快捷方式（符号链接），或者两个文件共享相同的数据（硬链接）。

为了更好地理解文件是如何链接的，你必须理解 inode。在结构层次上，文件系统有三个部分：

- 超块 `superblock`
- inode 表
- 数据块

超块是包含文件系统通用信息的部分，以及 inode 和数据块的数量。inode 表由若干个 inode（节点）组成；每个 inode 描述一个文件或目录并包含一个唯一标识。更重要的是，inode 存储了文件大小、数据块位置、修改日期、权限和所有权等信息。当文件被删除时，只有指向数据的 inode 被删除。组成数据以及文件名存储在数据块中，并被引用。在文件系统的术语中，块被称为分配单元，因为它们是磁盘空间的分配单位。

> 注意 每个文件和数据块必须有 inode。所有设备文件除外。特殊设备文件将在第 6 章“文件系统管理”中讨论。

目录只是用于组织其他文件的文件；它们也有 inode 和数据块，但它们的数据块包含文件名列表。

硬链接文件是彼此的直接副本，因为它们共享相同的 inode 和 inode 编号。所有硬链接文件的大小相同，当其中一个文件被修改时，其他硬链接文件也会随之更新。硬链接文件之间的这种关系如图 5-1 所示。你可以无限硬链接文件，但硬链接文件必须位于同一个文件系统中。这是因为 inode 编号仅在同一个文件系统中是唯一的，而硬链接是通过忽略这一规则被识别的。

**图 5-1** 硬链接文件的结构

要创建硬链接，你必须使用 `link` 命令并指定两个参数：要硬链接的现有文件以及将创建的目标文件。每个参数可以是文件的绝对或相对路径。以用户 root 家目录的目录为例：

```
[root@server1]# ls -l
total 520
drwx-xr-x 3 root 4096 Apr 8 07:12 Desktop
--rw-rxr-x 1 root 519964 Apr 7 09:59 file1
--rw-rxr-x 1 root 1244 Apr 27 18:17 file3 [root@server1]# _
```

## 链接文件 第5章

如果你想为名为 `file1` 的文件创建一个硬链接 `file2`（如图 5-1 所示），你可以在命令行提示符输入 `ln file1 file2` 命令；这将创建一个名为 `file2` 的文件并将其与 `file1` 硬链接。之后要查看硬链接文件名，你可以使用 `ls -1` 命令：

```
[rootserver1]# # ln file1 file2
[rootserver1]# # ls -1
total 1032
drwx-xr-x 2 root 4096 Apr 8 07:12 Desktop
-rwxr-xr-x 2 root 519964 Apr 7 09:59 file1
-rwxr-xr-x 2 root 519964 Apr 7 09:59 file2
-rwxr-xr-x 1 root 1244 Apr 27 18:17 file3 [rootserver1]# _
```

从上面的列表中可以看出，`file1` 和 `file2` 共享同一个索引，因为它们具有相同的大小、权限、所有者、修改日期等。还要注意，`file1` 的链接计数（设置的权限数量）已从 1 增加到上述输出中的数字。链接计数 1 表示该文件仅由一个索引共享。与另一个文件硬链接的文件共享两个节点，因此链接计数为 2。同样地，与三个其他文件硬链接的文件共享四个节点，因此链接计数为 4。

尽管硬链接共享相同的索引，但删除一个链接文件不会删除所有其他已链接的文件。通过删除其中一个文件可以移除硬链接，这会降低链接计数。

要查看硬链接文件的 inode 编号以验证它们是否相同，除了任何其他选项外，你可以在 `ls` 命令上使用 `-i` 选项。inode 编号位于每行目录列表的左侧，如下面的输出所示：

```
[rootserver1]# # ls -li
total 1032
drwx-xr-x 2 root 4096 Apr 8 07:12 Desktop
-rwxr-xr-x 2 root 519964 Apr 7 09:59 file1
-rwxr-xr-x 2 root 519964 Apr 7 09:59 file2
-rwxr-xr-x 1 root 1244 Apr 27 18:17 file3 [rootserver1]# _
```

> 注意：目录文件通常不是硬链接的，因为这会导致两个目录包含相同的内容。然而在某些情况下，root 用户能够使用 `ln` 命令的 `-F` 或 `-d` 选项来硬链接目录。只有那些经常添加文件并需要保持相同文件内容的目录通常会被硬链接。

## 第5章 LINUX 文件系统管理

符号链接（如图 5-2 所示）与硬链接不同，因为它们不与其目标文件共享相同的 inode 和 inode 编号；一个仅仅是指向另一个的指针，因此两个文件的大小不同。符号链接文件中的数据块仅包含指向目标文件的路径。当用户编辑符号链接文件时，实际上是在编辑目标文件。因此，如果目标文件被删除，符号链接对于一个不存在的文件将不再发挥功能。

> 符号链接有时被称为“软链接”（soft links）或“symlinks”。

图 5-2 符号链接文件的结构

要创建符号链接，你使用 `ln` 命令中的 `-s` 选项。要创建一个名为 `file4` 的指向 `file3` 的符号链接（如图 5-2 所示），你可以使用 `ln -s file3 file4`。在命令行提示符使用 `ln -s file3 file4`。符号链接的参数可以是绝对路径或相对路径。要查看创建的符号链接，你可以使用 `ls -l` 命令，如下所示：

```
[rootserver1]# # ln -s file3 file4
ls -l
total 1032
drwx-xr-x 2 root 4096 Apr 8 07:12 Desktop
-rwxr-xr-x 2 root 519964 Apr 7 09:59 file1
-rwxr-xr-x 2 root 519964 Apr 7 09:59 file2
-rwxr-xr-x 1 root 1244 Apr 27 18:17 file3
-lrwxrwxrwx 1 root root 0 Apr 27 18:17 file4 -> file3
```

## 链接文件 权限

硬链接与符号链接的区别在于符号链接不与其目标文件共享相同的 inode 和 inode 编号；一个仅仅是指向另一个的指针，因此两个文件的大小不同。符号链接文件中的数据块仅包含指向目标文件的路径。当用户编辑符号链接文件时，实际上是在编辑目标文件。因此，如果目标文件被删除，符号链接对于一个不存在的文件将不再发挥功能。

## 链接文件 目录权限

### 文件目录权限

```
-rw-r--r-- 1 user root 3578 Mar 29 09:58 Home
-rw-r--r-- 1 user root 1791 Mar 29 09:58 Start Here
drw------ 2 user root 4096 Mar 29 09:58 Trash
```

请记住，文件或目录的所有者以及 root 用户有权更改特定文件或目录的权属。如果普通用户更改了其所属的文件或目录的所有权，该用户将无法重新获得所有权。相反，该文件或目录的新所有者必须将其更改回原始所有。然而，之前的示例涉及 root 用户，他始终拥有重新获得所有权：

```
[root@server1]# chown file
[root@server1]# chown -R root
[root@server1]# ls -l
```

total 4
drw------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--r-- 1 root root 0 Apr 29 15:40 file1
total 16
-rw------- 1 root root 163 Mar 29 09:55 Floppy
-rw-r--r-- 1 root root 3578 Mar 29 09:58 Home
-rw-r--r-- 1 root root 1791 Mar 29 09:58 Start Here
drw------ 2 root root 4096 Mar 29 09:58 Trash

正如 `change`（更改所有者）命令可以更改文件或目录的所有者一样，你也可以使用 `chgrp`（更改组）命令来更改文件或目录的组所有者。`chgrp` 命令至少接受两个参数：新的组所有者以及文件或目录。与 `change` 命令一样，`chgrp` 命令也接受 `-R` 选项来递归更改整个目录的所有权。要递归地更改文件和 Desktop 目录的组所有，你可以执行以下命令：

```
[root@server1]# chgrp file1
[root@server1]# chgrp -R Desktop
[root@server1]# ls -l
```

total 4

drw------ 3 root root 4096 Apr 8 07:12 Desktop

-rw-r--r-- 1 root root 0 Apr 29 15:40 file1

total 16

-rw------- 1 root root 163 Mar 29 09:55 Floppy

-rw-r--r-- 1 root root 3578 Mar 29 09:58 Home

-rw-r--r-- 1 root root 1791 Mar 29 09:58 Start Here

drw------ 2 root root 4096 Mar 29 09:58 Trash

```
[root@server1]#

## 第 5 节 LINUX 文件系统管理

普通用户只能将文件或目录的组更改为他们所属的某个组。通常情况下，当文件需要由他人维护时，你会同时更改该文件的所有权和组所有权。因此，你可以使用 `chown` 命令同时更改所有者和组所有者。要递归地将 file1 和 Desktop 的所有者更改为 user1，组所有者更改为 root，你可以输入以下命令：

```
[root@server1]# chown user1.root file1
[root@server1]# chown -R user1.root Desktop
[root@server1]# ls -l
total 4
drwx------ 3 user root 4096 Apr 8 07:12 Desktop
-rw-r--r-- 1 user root 0 Apr 29 15:40 file1
total 16
-rw------- 1 user root 163 Mar 29 09:55 Floppy
-rw-r--r-- 1 user root 3578 Mar 29 09:58 Home
-rw-r--r-- 1 user root 1791 Mar 29 09:58 Start Home
drwxrwx-- 2 user root 4096 Mar 29 09:58 Trash
```
[root@server1]#

注意在上述输出中显示的 `chown` 命令中，`.` 字符前后没有空格。你也可以在 `chown` 命令中使用 `:` 字符代替 `.` 字符来同时更改所有者和组所有权（例如，`chown -R user1:root Desktop`）。

出于安全考虑，位于用户主目录中的大多数文件应属于该用户；用户主目录中的某些文件（尤其是隐藏文件和目录）需要此功能正常工作。为了避免以后出现问题，将 file1 和 Desktop 的所有权改回 root 用户，你可以输入以下：

```
[root@server1]# chown root.root file1
[root@server1]# chown -R root.root Desktop
[root@server1]# ls -l
total 4
```

### 文件目录权限

```
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-r--r-- 1 root root 0 Apr 29 15:40 file1
```
[root@server1 root]# ls -l
Desktop total 16
-drwx------ 1 root root 163 Mar 29 09:58 Floppy
-rw-r--r-- 1 root root 3578 Mar 29 09:58 Home
-rw-r--r-- 1 root root 1791 Mar 29 09:58 Start Here
drwx------ 2 root root 4096 Mar 29 09:58 Trash

[root@server1]#

## 管理和目录权限
