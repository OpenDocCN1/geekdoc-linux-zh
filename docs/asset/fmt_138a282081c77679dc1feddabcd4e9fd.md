
| `u` (用户) | `+` (添加权限) | `r` (读取) |
| :--- | :--- | :--- |
| `g` (组) | `-` (移除权限) | `w` (写入) |
| `o` (其他人) | `=` (使权限等于) | `x` (执行) |
| `a` (所有类别) | | |

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

若要更改 `file1` 的模式为 `rw-r--r--`，你必须为该文件的用户添加写入权限，为文件组添加读取权限并移除写入权限，以及为其他人添加读取权限并移除执行权限。

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
>
> 应确保在 `chmod` 命令中使用的所有条件之间没有空格，因为所有条件仅组成第一个参数。

你也可以使用表 5-5 中的 `e` 条件来指定要更改的确切权限。要将前面输出中 `file2` 的模式更改为与 `file1` (`rw-r--r--`) 相同，你可以使用以下 `chmod` 命令：

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
-rw-f--r--   1 user1 sys      282 Apr 29 22:06 file6
[root@server1 root]#
```

如果用户、组和其他类别要更改的权限相同，你可以使用“`a`”字符来表示表 5-5 和以下示例中所示的所有类别，例如为 `file1` 的用户、组和其他添加执行权限时：

```
[root@server1 root]# chmod a+x file1
[root@server1 root]# ls -l
total 28
drwx------  3 root  root     4096 Apr  8 07:12 Desktop
-rw-rw-rw  1 root  root       282 Apr 29 22:06 file1
-rw-f--r--   1 root  root       282 Apr 29 22:06 file2
-rw-fw-rw-  1 root  root       282 Apr 29 22:06 file3
---------- 1 root  root       282 Apr 29 22:06 file4
-rw-f-r--   1 root  root       282 Apr 29 22:06 file5
-rw-f--r--   1 user1 sys      282 Apr 29 22:06 file6
[root@server1 root]#
```

然而，如果没有指定影响用户的类别的字符，则假定影响所有用户，如以下示例中为 `file2` 的用户、组和其他添加执行权限时所示：

```
[root@server1 root]# chmod +x file2
[root@server1 root]# ls -l
total 28
drwx------  3 root  root     4096 Apr  8 07:12 Desktop
-rw-fw-rw  1 root  root       282 Apr 29 22:06 file1
-rw-fw-rw  1 root  root       282 Apr 29 22:06 file2
-rw-fw-rw  1 root  root       282 Apr 29 22:06 file3
---------- 1 root  root       282 Apr 29 22:06 file4
-rw-f-r--   1 root  root       282 Apr 29 22:06 file5
-rw-f--r--   1 user1 sys      282 Apr 29 22:06 file6
[root@server1 root]#
```

上述所有 `chmod` 示例都使用表 5-5 中列出的符号作为更改文件或目录权限的条件。你或许会选择使用数字条件配合 `chmod` 命令来更改权限。所有权限都以二进制 2 的幂次形式存储在文件或目录的 inode 中：

- 读取 = $2^3 = 4$
- 写入 = $2^1 = 2$
- 执行 = $2^0 = 1$

因此，文件或目录的模式可以使用数字 `421421421` 来表示，而不是 `rwxrwxrwx`。因为权限被归类为用户、组和其他，你可以进一步简化，使用仅三个数字，每个数字代表相应类别权限的总和，如图 5-4 所示。

![](img/09bf13b782f71165e17bb3839040c96a_203_0.png)

同样，要表示模式 `rw-r-r--`，你可以使用数字 `644`，因为用户有读取和写入权限 ($4+2=6$)，组有读取权限 ($4$)，其他有读取权限 ($4$)。模式 `rwxr-x---` 也可以表示为 `750`，因为用户有读取、写入和执行权限 ($4+2+1=7$)，组有读取和执行权限 ($4+1=5$)，其他没有权限 ($0$)。表 5-6 提供了不同权限及其对应数字的列表。

要更改前面使用的 `file1` 文件的模式为 `r-xr-----`，你可以使用命令 `chmod 540 file1`，如下例所示：

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
| `rwx` | `4 + 2 + 1 = 7` |
| `rw-` | `4 + 2 = 6` |
| `r-x` | `4 + 1 = 5` |
| `r--` | `4` |
| `-wx` | `2 + 1 = 3` |
| `-w-` | `2` |
| `--x` | `1` |
| `---` | `0` |
