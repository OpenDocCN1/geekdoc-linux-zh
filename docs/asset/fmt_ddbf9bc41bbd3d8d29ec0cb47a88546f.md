
# 目录权限说明

请记住，目录只是具有 inode 和数据区的特殊文件，但数据区包含的是该目录内容的列表。如果你想读取该列表（例如使用 `ls` 命令），则需要对目录具有读取权限。要修改该列表（通过添加或删除文件），则需要对目录具有写入权限。因此，如果你想使用 `vi` 等文本编辑器在目录中创建新文件，你必须对该目录具有写入权限。类似地，当使用 `cp` 命令将源文件复制到目标目录时，会在目标目录中创建一个新文件，对于复制成功，你必须对目标目录具有写入权限。相反，要删除某个特定文件，你必须对包含该文件的目录具有写入权限。同样重要的是要注意，对目录具有写入权限的用户能够删除其中的所有文件和子目录。

目录上的执行权限有时被称为搜索权限，其工作原理类似于电灯开关。当电灯开关打开时，你可以浏览房间并使用其中的物体。然而，当电灯开关关闭时，你看不到房间里的物体，也无法四处走动并查看它们。没有对目录具有执行权限的用户将被阻止列出目录内容、添加和删除文件，以及操作该目录内的文件和子目录，无论用户对这些文件和子目录拥有什么权限。简而言之，在 Linux 中拒绝用户访问目录及其所有内容的快速方法就是移除该目录上的执行权限。由于目录上的执行权限对于用户访问至关重要，除非目录必须是私有的，否则通常通过其他类别授予所有用户。

| 权限 | 文件的定义 | 目录的定义 |
| :--- | :--- | :--- |
| 读取 | 允许用户打开并读取文件内容 | 允许用户列出目录内容（前提是她也被授予了执行权限） |
| 写入 | 允许用户打开、读取和编辑文件内容 | 允许用户向目录添加或从目录移除文件（前提是她也被授予了执行权限） |
| 执行 | 允许用户执行内存中的文件（如果是程序文件或脚本） | 允许用户进入目录并操作目录内容 |

**表 4-4** Linux 权限

## 更改权限

要更改特定文件或目录的权限，可以使用 `chmod`（更改模式）命令。`chmod` 命令至少接受两个参数；第一个参数指定用于更改权限的标准（表 4-5），其余参数指示要更改的文件名。

以之前使用的目录列表为例：

```
[root@server1 ~]# ls -l
total 28
drwx------  3 root   root    4096 Apr  8 07:12 Desktop
-rw----w---x 1 bob    proj     282 Apr 29 22:06 file1
----------rw- 1 root   root      282 Apr 29 22:06 file2
-rwxrwxrwx  1 root   root      282 Apr 29 22:06 file3
----------  1 root   root      282 Apr 29 22:06 file4
-rw-f--r--  1 root   root      282 Apr 29 22:06 file5
-rw-f--r--  1 user1 sys       282 Apr 29 22:06 file6
[root@server1 ~]# _
```

要将 `file1` 的模式更改为 `rw-r--r--`，你必须为该文件的所有者添加写入权限，为该文件的属组添加读取权限并移除写入权限，并为其他类别添加读取权限并移除执行权限。

| 类别 | 操作 | 权限 |
| :--- | :--- | :--- |
| `u` (用户) | `+` (添加权限) | `r` (读取) |
| `g` (组) | `-` (移除权限) | `w` (写入) |
| `o` (其他) | `=` (使权限相等) | `x` (执行) |
| `a` (所有类别) |  |  |

**表 4-5** 在 `chmod` 命令中使用的标准

根据表 4-5 中列出的信息，你可以使用以下命令：

```
[root@server1 ~]# chmod u+w,g+r-w,o+rx-x file1
[root@server1 ~]# ls -l
```

```
total 28
drwx------  3 root    root        4096 Apr  8 07:12 Desktop
-rw-f--r--  1 bob     proj          282 Apr 29 22:06 file1
--r---r-rw  1 root    root          282 Apr 29 22:06 file2
-rwxrwxrwx  1 root    root          282 Apr 29 22:06 file3
------r----  1 root    root          282 Apr 29 22:06 file4
-rw-f--r--  1 root    root          282 Apr 29 22:06 file5
-rw-f--r--  1 user1   sys           282 Apr 29 22:06 file6
[root@server1 ~]# _
```

![](img/c27875544958897d817484d558c208c8_186_0.png)

你应该确保在 `chmod` 命令中使用的任何标准之间没有空格，因为所有标准仅构成第一个参数。

你也可以使用表 4-5 中的 `=` 标准来指定要更改的确切权限。要将前面输出中 `file2` 的模式更改为与 `file1`（`rw-r--r--`）相同，你可以使用以下 `chmod` 命令：

```
[root@server1 ~]# chmod u=rw,g=r,o=r file2
[root@server1 ~]# ls -l
```

```
total 28
drwx------  3 root    root        4096 Apr  8 07:12 Desktop
-rw-f--r--  1 bob     proj          282 Apr 29 22:06 file1
-rw-f--r--  1 root    root          282 Apr 29 22:06 file2
-rwxrwxrwx  1 root    root          282 Apr 29 22:06 file3
------r----  1 root    root          282 Apr 29 22:06 file4
-rw-f--r--  1 root    root          282 Apr 29 22:06 file5
-rw-f--r--  1 user1   sys           282 Apr 29 22:06 file6
[root@server1 ~]# _
```

如果要更改的权限对于用户、组和其他类别是相同的，你可以使用 `a` 字符来指代所有类别，如表 4-5 所示，并在以下示例中为 `file1` 的用户、组和其他类别添加执行权限：

```
[root@server1 ~]# chmod a+x file1
[root@server1 ~]# ls -l
```

```
total 28
drwx------  3 root    root        4096 Apr  8 07:12 Desktop
-rwxr-xr-x  1 bob     proj          282 Apr 29 22:06 file1
-rw-f--r--  1 root    root          282 Apr 29 22:06 file2
-rwxrwxrwx  1 root    root          282 Apr 29 22:06 file3
------r----  1 root    root          282 Apr 29 22:06 file4
-rw-f--r--  1 root    root          282 Apr 29 22:06 file5
-rw-f--r--  1 user1   sys           282 Apr 29 22:06 file6
[root@server1 ~]# _
```

然而，如果没有指定要影响的用户类别字符，则假定影响所有用户，如下所示为给 `file2` 的用户、组和其他添加执行权限的示例：

```
[root@server1 ~]# chmod +x file2
[root@server1 ~]# ls -l
total 28
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
-rwxr-xr-x 1 bob proj 282 Apr 29 22:06 file1
-rwrxr-x 1 root root 282 Apr 29 22:06 file2
-rwxrwxrwx 1 root root 282 Apr 29 22:06 file3
---------- 1 root root 282 Apr 29 22:06 file4
-rw-r--- 1 root root 282 Apr 29 22:06 file5
-rw-r-r--- 1 user1 sys 282 Apr 29 22:06 file6
[root@server1 ~]# _
```

上述所有 `chmod` 示例均使用表 4-5 中列出的符号作为更改文件或目录权限的标准。您也可以改用数字标准配合 `chmod` 命令来更改权限。所有权限都以二进制 2 的幂形式存储在文件或目录的 inode 中：

- 读 = 2² = 4
- 写 = 2¹ = 2
- 执行 = 2⁰ = 1

因此，文件或目录的模式可以用数字 421421421 来表示，而不是 `rwxrwxrwx`。由于权限被归类为用户、组和其他，因此可以进一步简化，使用三个数字，每个数字代表一个类别的权限总和，如图 4-4 所示。

同样地，要表示模式 `rw-r--r--`，可以使用数字 644，因为用户具有读和写权限（4 + 2 = 6），组具有读权限（4），其他具有读权限（4）。模式 `rwxr-x--` 也可以表示为 750，因为用户具有读、写和执行权限（4 + 2 + 1 = 7），组具有读和执行权限（4 + 1 = 5），其他没有权限（0）。表 4-6 列出了不同的权限及其对应的数字。

要将之前使用的 `file1` 文件的模式更改为 `r-xr---`，可以使用命令 `chmod 540 file1`，如下例所示：

![](img/c27875544958897d817484d558c208c8_187_0.png)

### 表 4-6 模式中权限的数字表示

| 模式（仅一段） | 对应数字 |
| :--- | :--- |
| `rwx` | 4 + 2 + 1 = 7 |
| `rw-` | 4 + 2 = 6 |
| `r-x` | 4 + 1 = 5 |
| `r--` | 4 |
| `-wx` | 2 + 1 = 3 |
| `-w-` | 2 |
| `--x` | 1 |
| `---` | 0 |

```
[root@server1 ~]# chmod 540 file1
[root@server1 ~]# ls -l
total 28
drwx------  3 root  root   4096 Apr   8 07:12 Desktop
-rw-r----   1 bob   proj    282 Apr 29 22:06 file1
-rwxr-xr-x   1 root  root    282 Apr 29 22:06 file2
-rwxrwxrwx   1 root  root    282 Apr 29 22:06 file3
----------   1 root  root    282 Apr 29 22:06 file4
-rw-f--r--   1 root  root    282 Apr 29 22:06 file5
-rw-f--r--   1 user1 sys    282 Apr 29 22:06 file6
[root@server1 ~]# _
```

同样地，要将目录中所有以单词 “file” 开头的文件的模式更改为 644（这是文件的常见权限），可以使用以下命令：

```
[root@server1 ~]# chmod 644 file*
[root@server1 ~]# ls -l
total 28
drwx------  3 root  root   4096 Apr   8 07:12 Desktop
-rw-f--r--   1 bob   proj    282 Apr 29 22:06 file1
-rw-f--r--   1 root  root    282 Apr 29 22:06 file2
-rw-f--r--   1 root  root    282 Apr 29 22:06 file3
-rw-f--r--   1 root  root    282 Apr 29 22:06 file4
-rw-f--r--   1 root  root    282 Apr 29 22:06 file5
-rw-f--r--   1 user1 sys    282 Apr 29 22:06 file6
[root@server1 ~]# _
```

与 `chown` 和 `chgrp` 命令一样，使用 `-R` 选项可以递归地更改目录及其所有内容的权限，如下例中更改 `Desktop` 目录的模式所示：

```
[root@server1 ~]# chmod -R 755 Desktop
[root@server1 ~]# ls -l
total 28
drwxr-xr-x  3 root  root   4096 Apr   8 07:12 Desktop
-rw-f--r-- 1 bob proj 282 Apr 29 22:06 file1
-rw-f--r-- 1 root root 282 Apr 29 22:06 file2
-rw-f--r-- 1 root root 282 Apr 29 22:06 file3
-rw-f--r-- 1 root root 282 Apr 29 22:06 file4
-rw-f--r-- 1 root root 282 Apr 29 22:06 file5
-rw-f--r-- 1 user1 sys 282 Apr 29 22:06 file6
[root@server1 ~]# ls -l Desktop
total 16
-rwxr-xr-x 1 root root 163 Mar 29 09:58 Floppy
-rw-f-xr-x 1 root root 3578 Mar 29 09:58 Home
-rw-f-xr-x 1 root root 1731 Mar 29 09:58 Start Here
drwxr-xr-x 2 root root 4096 Mar 29 09:58 Trash
[root@server1 ~]# _
```

## 默认权限

请记住，权限通过对文件和目录仅提供特定用户的访问权限来提供安全保护，并且有一些常见的准则用于设置文件和目录的权限，以防止权限过于严格或过于宽松。对于维护安全同样重要的一点是，在创建新文件和目录后分配给它们的权限。当系统创建新文件时，会赋予其 `rw-rw-` 权限（因为除非必要，否则不应授予执行权限），而新目录在系统创建时会被赋予 `rwxrwxrwx` 权限。这些默认权限对于大多数文件来说过于宽松，因为它们允许其他用户完全访问目录，并几乎完全访问文件。因此，系统中有一个称为 `umask`（用户掩码）的特殊变量，它会在新文件和目录创建后立即移除部分权限。你通常会发现最常见的 `umask` 是 022，它指定在新文件和目录创建并由系统赋予权限时，不从中移除用户的任何权限（0），移除组的写权限（2），并移除其他的写权限（2）。

![](img/c27875544958897d817484d558c208c8_189_0.png)

> **注意**：请记住，`umask` 仅适用于新创建的文件和目录；它从不用于修改现有文件和目录的权限。你必须使用 `chmod` 命令来修改现有权限。

图 4-5 展示了一个 `umask` 022 在创建新文件或目录后如何用于更改其权限的示例。

| | 新文件 | 新目录 |
| :--- | :--- | :--- |
| 系统分配的权限 | `rw-rw-rw-` | `rwxrwxrwx` |
| - `umask` | 0 2 2 | 0 2 2 |
| = 结果权限 | `rw-r--r--` | `rwxr-xr-x` |

**图 4-5 执行 `umask` 022 计算**

要验证使用的 `umask`，你可以使用 `umask` 命令并注意输出中的最后三位数字。要确保 `umask` 按图 4-5 所示起作用，只需使用 `touch` 命令创建一个新文件，并使用 `mkdir` 命令创建一个新目录，如下所示的输出：

```
[root@server1 ~]# ls -l
total 28
drwx------  3 root  root    4096 Apr  8 07:12 Desktop
[root@server1 ~]# umask
0022
[root@server1 ~]# mkdir dir1
[root@server1 ~]# touch file1
[root@server1 ~]# ls -l
total 8
drwx------  3 root  root    4096 Apr  8 07:12 Desktop
drwxr-xr-x  2 root  root    4096 May  3 21:39 dir1
-rw-f--r--  1 root  root      0 May  3 21:40 file1
[root@server1 ~]# _
```

由于 `umask` 是存储在内存中的变量，因此可以更改它。要更改当前的 `umask`，你可以将新的 `umask` 指定为 `umask` 命令的参数。例如，假设你想将 `umask` 更改为 007；新文件和目录的结果权限如图 4-6 中计算所示。

要将 `umask` 更改为 007 并查看其效果，你可以在命令行中输入以下命令：
