
## 文件和目录权限

表 5-5 用于 chmod 命令的条件

| 类别 | 操作 | 权限 |
| :--- | :--- | :--- |
| u (用户) | + (添加权限) | r (读取) |
| g (组) | - (移除权限) | w (写入) |
| o (其他人) | = (使权限等于) | x (执行) |
| a (所有类别) | | |

例如，取前面使用过的目录列表：

```
[root@server1 root]# ls -l
total 28
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-rw-rw- 1 root root 282 Apr 29 22:06 file1
-rw-rw-rw- 1 root root 282 Apr 29 22:06 file2
-rwxrwxrwx 1 root root 282 Apr 29 22:06 file3
--------- 1 root root 282 Apr 29 22:06 file4
-rw-rw-r- 1 root root 282 Apr 29 22:06 file5
-rw-r-r-r- 1 user1 sys 282 Apr 29 22:06 file6 
[root@server1 root]# 
```

若要更改 file1 的模式为 rw-r--r--，你必须为该文件的用户添加写入权限，为文件组添加读取权限并移除写入权限，以及为其他人添加读取权限并移除执行权限。

根据表 5-5 中列出的信息，你可以使用以下命令：

```
[root@server1 root]# chmod u+w,g+r,o+x file1
[root@server1 root]# ls -l
total 28
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rw-rw-r- 1 root root 282 Apr 29 22:06 file1
-rw-rw-rw- 1 root root 282 Apr 29 22:06 file2
-rwxrwxrwx 1 root root 282 Apr 29 22:06 file3
--------- 1 root root 282 Apr 29 22:06 file4
-rw-rw-r- 1 root root 282 Apr 29 22:06 file5
-rw-r-r-r- 1 user1 sys 282 Apr 29 22:06 file6 
[root@server1 root]# 
```

> **注意**
> 应确保在 chmod 命令中使用的所有条件之间没有空格，因为所有条件仅组成第一个参数。

你也可以使用表 5-5 中的 e 条件来指定要更改的确切权限。要将前面输出中 file2 的模式更改为与 file1 (rw-r--r--) 相同，你可以使用以下 chmod 命令：

```
[root@server1 root]# chmod u=rw,g=r,o=r file2
[root@server1 root]# ls -l
total 28
drwx------  3 root  root     4096 Apr  8 07:12 Desktop
-rw-r--r--   1 root  root       282 Apr 29 22:06 file1
-rw-r--r--   1 root  root       282 Apr 29 22:06 file2
-rw-rw-rw-   1 root  root       282 Apr 29 22:06 file3
---------- 1 root  root       282 Apr 29 22:06 file4
-rw-r-r--   1 root  root       282 Apr 29 22:06 file5
-rw-r--r--   1 user1 sys      282 Apr 29 22:06 file6
[root@server1 root]#
```

如果用户、组和其他类别要更改的权限相同，你可以使用“a”字符来表示表 5-5 和以下示例中所示的所有类别，例如为 file1 的用户、组和其他添加执行权限时：

```
[root@server1 root]# chmod a+x file1
[root@server1 root]# ls -l
total 28
drwx------  3 root  root     4096 Apr  8 07:12 Desktop
-rw-rw-rw  1 root  root       282 Apr 29 22:06 file1
-rw-r--r--   1 root  root       282 Apr 29 22:06 file2
-rw-rw-rw-  1 root  root       282 Apr 29 22:06 file3
---------- 1 root  root       282 Apr 29 22:06 file4
-rw-r-r--   1 root  root       282 Apr 29 22:06 file5
-rw-r--r--   1 user1 sys      282 Apr 29 22:06 file6
[root@server1 root]#
```

然而，如果没有指定影响用户的类别的字符，则假定影响所有用户，如以下示例中为 file2 的用户、组和其他添加执行权限时所示：

```
[root@server1 root]# chmod +x file2
[root@server1 root]# ls -l
total 28
drwx------  3 root  root     4096 Apr  8 07:12 Desktop
-rw-rw-rw  1 root  root       282 Apr 29 22:06 file1
-rw-rw-rw  1 root  root       282 Apr 29 22:06 file2
-rw-rw-rw  1 root  root       282 Apr 29 22:06 file3
---------- 1 root  root       282 Apr 29 22:06 file4
-rw-r-r--   1 root  root       282 Apr 29 22:06 file5
-rw-f--r--   1 user1 sys      282 Apr 29 22:06 file6
[root@server1 root]#
```

上述所有 `chmod` 示例都使用表 5-5 中列出的符号作为更改文件或目录权限的条件。你或许会选择使用数字条件配合 `chmod` 命令来更改权限。所有权限都以二进制 2 的幂次形式存储在文件或目录的 inode 中：

- 读取 = 2^3 = 4
- 写入 = 2^1 = 2
- 执行 = 2^0 = 1

因此，文件或目录的模式可以使用数字 421421421 来表示，而不是 rwxrwxrwx。因为权限被归类为用户、组和其他，你可以进一步简化，使用仅三个数字，每个数字代表相应类别权限的总和，如图 5-4 所示。

![](img/09bf13b782f71165e17bb3839040c96a_203_0.png)

同样，要表示模式 rw-r-r-- ，你可以使用数字 644，因为用户有读取和写入权限 (4+2=6)，组有读取权限 (4)，其他有读取权限 (4)。模式 rwxr-x--- 也可以表示为 750，因为用户有读取、写入和执行权限 (4+2+1=7)，组有读取和执行权限 (4+1=5)，其他没有权限 (0)。表 5-6 提供了不同权限及其对应数字的列表。

要更改前面使用的 file1 文件的模式为 r-xr-----，你可以使用命令 `chmod 540 file1`，如下例所示：

```
[ root@server1 root]# chmod 540 file1
[ root@server1 root]# ls -l
total 28
drw----- 3 root root 4096 Apr 8 07:12 Desktop
-r-xr---- 1 root root 282 Apr 29 22:06 file1
-rwxr-xr-- 1 root root 282 Apr 29 22:06 file2
-rwxrwxrwx 1 root root 282 Apr 29 22:06 file3
---------- 1 root root 282 Apr 29 22:06 file4
-rw-f--r- 1 root root 282 Apr 29 22:06 file5
-rw-f-r-- 1 user1 sys 282 Apr 29 22:06 file6
[ root@server1 root]# _
```

表 5-6 模式权限的数字表示

| 模式 (仅一个部分) | 对应数字 |
| :--- | :--- |
| rwx | 4 + 2 + 1 = 7 |
| rw- | 4 + 2 = 6 |
| r-x | 4 + 1 = 5 |
| r-- | 4 |
| -wx | 2 + 1 = 3 |
| -w- | 2 |
| --x | 1 |
| --- | 0 |

同样，要将目录中所有以单词“file”开头的文件的模式更改为 644（这是文件的常见权限），你可以使用以下命令：

```
[root@server1 root]# chmod 644 file*
[root@server1 root]# ls -l
total 28
drw x----- 3 root root 4096 Apr 8 07:12 Desktop
-rw-f--r-- 1 root root 282 Apr 29 22:06 file1
-rw-f--r-- 1 root root 282 Apr 29 22:06 file2
-rw-f--r-- 1 root root 282 Apr 29 22:06 file3
-rw-f--r-- 1 root root 282 Apr 29 22:06 file4
-rw-f--r-- 1 root root 282 Apr 29 22:06 file5
-rw-f--r-- 1 user1 sys 282 Apr 29 22:06 file6
[root@server1 root]# _
```

与 chown 和 chgrp 命令类似，chmod 命令也可以通过使用 -R 选项来递归地更改目录及其所有内容的权限，如下例中更改 Desktop 目录的模式时所示：

```
[root@server1 root]# chmod -R 755 Desktop
[root@server1 root]# ls -l
total 28
drw x-xr-x 3 root root 4096 Apr 8 07:12 Desktop
-rw-f--r-- 1 root root 282 Apr 29 22:06 file1
-rw-f--r-- 1 root root 282 Apr 29 22:06 file2
-rw-f--r-- 1 root root 282 Apr 29 22:06 file3
-rw-f--r-- 1 root root 282 Apr 29 22:06 file4
-rw-f--r-- 1 root root 282 Apr 29 22:06 file5
-rw-f--r-- 1 user1 sys 282 Apr 29 22:06 file6
```

```
[root@server1 root]# ls -l Desktop
  total 16
  -rw-r-xr-x    1 root root     163 Mar 29 09:58 Floppy
  -rw-r-xr-x    1 root root    3578 Mar 29 09:58 Home
  -rw-r-xr-x    1 root root    1791 Mar 29 09:58 Start Here
  drwxr-xr-x    2 root root    4096 Mar 29 09:58 Trash
  [root@server1 root]# _
```

## 默认权限

回想一下，权限通过仅允许特定用户访问来为文件和目录提供安全性，并且有一些通用的准则来设置文件和目录的权限，使得权限既不会过于严格也不会过于宽松。同样重要的是，在创建新文件和目录后赋予它们的权限。系统在创建新文件时赋予其 rw-rw-rw- 权限（除非必要，否则不应赋予执行权限），系统在创建新目录时赋予其 rwxrwxrwx 权限。这些默认权限对大多数文件来说过于宽松，因为它们允许其他用户对目录拥有完全访问权限，对文件拥有几乎完全的访问权限。因此，系统中有一个名为 umask（用户掩码）的特殊变量，它会在新文件和目录创建后立即移除它们的权限。你会找到的最通用的 umask 是 022，它指定当新文件和目录在首次由系统赋予权限时，从用户那里不移除任何权限 (0)，从组成员那里移除写入权限 (2)，从其他用户那里移除写入权限 (2)。

> **注意**
> 请记住，umask 仅适用于新创建的文件和目录；它从不用于修改现有文件和目录的权限。你必须使用 chmod 命令来修改现有权限。

图 5-5 展示了如何通过使用 022 的 umask 在创建新文件或目录后更改其权限的示例。

要验证使用的 umask，你可以使用 umask 命令并注意输出中的最后三位数字。为了确保 umask 如“图 5-5”所示那样工作，只需使用 touch 命令创建一个新文件，并使用 mkdir 命令创建一个新目录，如下面的输出所示：

```
[root@server1 root]# ls -l
  total 28
  drwx------    3 root root    4096 Apr 8 07:12 Desktop
  [root@server1 root]# umask
  0022
```
