
`umask` 仅适用于新创建的文件和目录；它从不用于修改现有文件和目录的权限。你必须使用 `chmod` 命令来修改现有权限。`umask` 在创建后更改新文件或目录权限的示例如图 4-5 所示。要验证所使用的 `umask`，可以使用 `umask` 命令并注意输出中的最后数字。为了确保 `umask` 功能如图 4-5 所示，可以使用 `touch` 命令创建新文件并使用 `mkdir` 命令创建新目录，如下输出所示：

```
[root@server1 ~]# ls -l
total 28
dw------ 3 root root      4096 Apr 8 07:12 Desktop
[root@server1 ~]# umask
0022
[root@server1 ~]# mkdir dir
[root@server1 ~]# touch file1
[root@server1 ~]# ls -l
total 8
dw------ 3 root root      4096 Apr 8 07:12 Desktop
drwx-xr-x 2 root root      4096 May 3 21:39 dir1
-rw-r--r-- 1 root root      0 May 3 21:40 file1
[root@server1 ~]#
```

由于 `umask` 是存储在内存中的变量，因此它可以更改。要更改当前的 `umask`，你可以指定一个新的 `umask` 作为 `umask` 命令的参数。例如，假设你想将 `umask` 更改为 007，新文件的权限将如下：

| umask | 新文件 / 新目录的权限 |
| --- | --- |
| 007 | 剥夺所有权限 |
| 022 | 剥夺组的写入权限 |
| 002 | 剥夺其他人的写入权限 |

# 设置特殊权限

使用 `ls -l` 命令显示的文件模式并没有用于特殊权限的栏目。然而，由于特殊权限需要执行权限，因此当使用 `ls -l` 命令显示时，它们会掩盖执行权限，如图 4-7 所示。

![](img/255973d661f18692a98dbc628624ab00_205_0.png)

即使文件或目录没有执行权限，系统允许你设置特殊权限。但是，特殊权限将无法发挥其功能。如果在没有执行权限的文件或目录上设置了特殊权限，那么无效的特殊权限将以大写形式显示，如图 4-8 所示。

![](img/255973d661f18692a98dbc628624ab00_205_1.png)

要设置特殊权限，你可以从模式的左侧可视化这些它们，如图 4-9 所示。

# 第 4 章 Linux 文件系统管理

| | 4 2 1 4 2 1 4 2 1 4 2 1 |
| :--- | :--- |
| SUIDID Sticky位 | r w x r w x r w x |
| 特殊 7 用户 7 组 7 其他 7 |

**图 4-9** 普通权限和特殊权限的数字表示

因此，若要对某个文件或目录设置所有特殊权限，你可以使用命令 `chmod 7777 filename`，如图 4-9 所示。然而，SUID 和 SGID 位通常被设置在文件上。为了更改之前使用的文件的权限，以便其他人可以作为组员的身份查看和编辑，你可以使用命令 `chmod 6755 file`，如下例所示：

```
root@server1 ~]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root 4096 May 3 21:39 dir2
-r-r--r-- 1 root root 0 May 3 21:40 file1
-rw-rw--rw 1 root root 0 May 3 21:40 file2
root@server1]# chmod 6755 file
root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root 4096 May 3 21:39 dir2
-r-r--r-- 1 root root 0 May 3 21:40 file1
-rw-rw--rw 1 root root 0 May 3 21:40 file2
```

类似地，若要在之前使用的目录设置粘滞位（Sticky Bit），你可以使用命令 `chmod 1777 dir`，这允许所有用户（包括其他人）向 dir 目录中添加文件。这是因为你赋予了写权限；由于你使用了粘滞位，用户只能删除它们在 dir 中拥有的的文件。如下所示：

```
root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
```

```
drwx------ 2 root 4096 May 3 21:41 dir2
-rwsr-sr-x 1 root 0 May 3 21:40 file1
-rw------- 1 root 0 May 3 21:41 file2
[root@server1 ~]# chmod 1777 dir1
[root@server1 ~]# ls -l
```

```
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-t 2 root 4096 May 3 21:39 dir1
drwx------ 2 root 4096 May 3 21:41 dir2
-rwsr-sr-x 1 root 0 May 3 21:40 file1
-rw------- 1 root 0 May 3 21:41 file2
[root@server1 ~]# 
```

此外，请记住，在没有执行权限的情况下分配特殊权限会使它们毫无用处。例如，你可能忘记给用户、组或其他人赋予执行权限，而长列表用特殊权限覆盖了执行权限。在这种情况下，特殊权限将以大写形式显示，如下例所示，当 dir 在模式中没有赋予指示粘滞位的（t）执行位置时：

```
[root@server1 ~]# ls -l
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-t 2 root 4096 May 3 21:39 dir1
drwx------ 2 root 4096 May 3 21:41 dir2
-rwsr-sr-x 1 root 0 May 3 21:40 file1
-rw------- 1 root 0 May 3 21:41 file2
```

同样，要移除属性，可以使用 `chattr` 命令配合 `-i` 选项，此处以 doc 文件所示：

```
[root@server1 ~]# chattr -i doc1
[root@server1 ~]# lsattr doc1
------------doc1
[root@server1 ~]#_
```

## 章节总结

- Linux 目录树遵循文件系统层级标准（FHS），这允许 Linux 用户和开发者在标准目录中定位系统文件。
- 许多文件管理命令旨在创建、更改位置或删除文件和目录。其中大多数命令包括 `cp`、`mv`、`rm`、`rmdir` 和 `mkdir`。
