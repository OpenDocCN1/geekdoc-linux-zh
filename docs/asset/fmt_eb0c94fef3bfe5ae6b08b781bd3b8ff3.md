
请记住，权限通过只允许特定用户访问为文件和目录提供安全性，并且设置文件和目录权限有指导准则，以确保权限不会过于严格或过于宽松。对于维护安全至关重要的是创建新文件和目录后赋予的权限。新文件在创建时被赋予 `rw-r--r--`（因为除非必要，否则不应具有执行权限），新目录被系统赋予 `rwxr-xr-x`。这些默认权限过于宽松，因为它们允许对目录的完全访问以及对几乎所有文件的访问。因此，一个名为 `umask`（用户掩码）的变量会在新文件和目录创建后立即剥夺某些权限。你最常见的 `umask` 是 `022`，它指定在新文件和目录首次创建并由系统权限时，不从组中剥夺任何权限（0），从其他用户中剥夺写权限（2）。

> 注意 19
> 请记住，`umask` 仅适用于新建的文件和目录；它永远不会用于修改现有文件和目录的权限。你必须使用 `chmod` 命令来修改现有权限。

## 第 4 章 Linux 文件系统管理

图 4-5 显示了如何使用 `umask 022` 更改创建后新文件或目录的权限示例。

**图 4-5** 执行 umask 022 计算

| | 新文件 | 新目录 |
|---|---|---|
| 系统分配的权限 | rw-rw- | rwxrxr-wx |
| - umask | 0 2 | 0 2 |
| = 结果权限 | rw-r-r-- | rwxrxr-x |

要验证 `umask`，可以使用 `umask` 命令并注意输出中的最后三个数字。其输出功能如图 4-5 所示，使用 `touch` 命令创建新文件并使用 `mkdir` 命令创建新目录，如下输出所示：

由于 `umask` 是内存中的一个变量，它可以被更改。要更改新的 `umask` 作为 `umask` 命令的参数，例如你想将 `umask` 更改为 `007`；新文件和目录的权限计算如图 4-6 所示。

**图 4-6** 执行 umask 007 计算

| | 新文件 | 新目录 |
|---|---|---|
| 系统分配的权限 | rw-rw- | rwxrxr-wx |
| - umask | 0 7 | 0 7 |
| = 结果权限 | rw------- | rwx------ |

要更改新的 `umask` 作为 `umask` 命令的参数，例如你想将 `umask` 更改为 `007`：

```bash
[root@server1]# ls -l
total 28
drwxr-xr-x 3 root root       4096 Apr 8 07:12 Desktop
-rw-r--r-- 1 bob proj        282 Apr 29 22:06 file1
-rw-r--r-- 1 root root       282 Apr 29 22:06 file2
-rw-r--r-- 1 root root       282 Apr 29 22:06 file3
-rw-r--r-- 1 root root       282 Apr 29 22:06 file4
-rw-r--r-- 1 root root       282 Apr 29 22:06 file5
-rw-r--r-- 1 user1 root       282 Apr 29 22:06 file6
[root@server1]# ls -l
total 16
drrw-xr-x 1 root root       163 Mar 29 09:58 Work
drrw-xr-x 1 root root       3578 Mar 29 09:58 Home
drrw-xr-x 1 root root       1791 Mar 29 09:58 Start Here
drwxr-xr-x 2 root root       4096 Mar 29 09:58 Trash
[root@server1]#
```

```bash
[root@server1]# ls -l
total 16
dr------ 3 root root 4096 8 07:12 Desktop
drwxr-xr-x 2 root root 4096 3 23:19 dir
-rw------- 1 root root 0 May 3 21:40 file1
```

## 图 4-9 普通权限和特殊权限的数值表示

| 4 2 1 | 4 2 1 | 4 2 1 | 4 2 1 |
| :--- | :--- | :--- | :--- |
| SUID | SGID | 粘滞位 (Sticky Bit) | RWXWRXR |

| 特殊 (Special) | 用户 (User) |  (Group) | 其他 (Other) |
| 7 | 7 | 7 | 7 |

因此，要对文件或目录设置所有特殊权限，可以使用命令 `chmod 7777`，如图 4-9 所示。然而，SUID 和 SGID 位通常设置在文件。为了更改之前使用的文件权限，使得所有者和组组成员可以访问，可以使用 `chmod 6755 file`，如下例所示：

```
[root@server1 ~]# ls -1
total 12
drwx------ root root 4096 Apr 8 07:12 Desktop
drwx-xr-x root root 4096 May 3 21:39 dir1
drwx------ root root 4096 May 3 21:41 dir2
-rw-r--x root root 0 3 21:41 file1
-rwx------ root root 0 3 21:41 file2
[root@server1 ~]# chmod 6755 file1
[root@server1 ~]# ls -1
total 12
drwx------ root root 4096 Apr 8 07:12 Desktop
drwx-xr-x root root 4096 May 3 21:39 dir1
drwx------ root root 4096 May 3 21:41 dir2
-rws-sr-x root root 0 3 21:41 file1
-rwx------ root root 0 3 21:41 file2
```

同样，要在你之前使用的目录上设置粘滞位，可以使用命令 `chmod 1777`，这允许用户（包括其他人）向该目录添加文件。这是因为你拥有写入权限；但是由于你设置了粘滞位，用户只能删除他们在目录中拥有的文件。如下所示：

```
[root@server1 ~]# ls -1
total 12
drwx------ root root 4096 Apr 8 07:12 Desktop
drwx-xr-x root root 4096 May 3 21:39 dir1
drwx------ root root 4096 May 3 21:41 dir2
-rws-sr-x root root 0 3 21:41 file1
-rwx------ root root 0 3 21:41 file2
[root@server1 ~]# chmod 1777 dir1
[root@server1 ~]# ls -1
total 12
drwx------ root root 4096 Apr 8 07:12 Desktop
drwx-xr-x root root 4096 May 3 21:39 dir1
drwx------ root root 4096 May 3 21:41 dir2
-rws-sr-x root root 0 3 21:41 file1
-rwx------ root root 0 3 21:41 file2
```

此外，请记住，在没有执行权限的情况下分配特殊权限将使它们失效。例如，在带有特殊权限且带有执行权限的长列表中，你可能会忘记给用户、组或其他人赋予执行权限。在这种情况下，特殊权限将以大写形式显示，如下例所示， `dir2` 在模式位中指示粘滞位（t）的位置下方没有赋予执行权限：

```
[root@server1 ~]# ls -l
total 12
drwx--- 3 root 4096 Apr 8 07:12 Desktop
drwxrxrwt 2 root 4096 May 3 21:39 dir1
drwx------ 2 root 4096 May 3 21:41 dir2
-rws-sr-x 1 root 0 May 21:40 file1
-rw-r--r-- 1 root 0 May 21:42 file2
[root@server1 ~]# chmod 1775 dir2
[root@server1 ~]# ls -l
total 12
drwx--- 3 root 4096 Apr 8 07:12 Desktop
drwxrxrwt 2 root 4096 May 3 21:39 dir1
drwx------ 2 root 4096 May 3 21:41 dir2
-rws-sr-x 1 root 0 May 21:40 file1
-rw-r--r-- 1 root 0 May 21:42 file2
[root@server1 ~]#
```

## 在访问控制列表 (ACL) 中设置自定义权限

访问控制列表 (ACL) 是一份可以为其分配权限的用户和组的列表。如前所述，Linux 默认的 ACL 包含三个实体：用户、组和其他。但在某些情况下，你可能需要为单个用户或组对文件或目录分配一组特定的权限。

例如，为单个用户或组对文件或目录分配特定的权限。

```
[root@server1 ~]# ls -l
total 12
drwx------ root root 4096 Apr 8 07:12 Desktop
drwx-xr-x root root 4096 May 3 21:39 dir1
drwx------ root root 4096 May 3 21:41 dir2
-rw-r--x root root 0 3 21:41 file1
-rwx------ root root 0 3 21:41 file2
```
