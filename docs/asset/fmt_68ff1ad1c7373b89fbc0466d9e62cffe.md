
# 第 5 章 Linux 文件系统管理

即使文件或目录没有执行权限，系统也允许你设置特殊权限。然而，如果在没有执行权限的文件或目录上设置特殊权限，那么无效的特殊权限将以大写显示，如图 5-8 所示。

要设置特殊权限，你可以将它们可视化在模式的左侧，如图 5-9 所示。

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_0.png)

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_1.png)

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_2.png)

因此，要在某个文件或目录上设置所有特殊权限，你可以使用 `chmod 7777 name`，如图 5-9 所示。`SUID` 和 `SGID` 位通常设置在文件上。要更改之前使用的文件的权限，使其他能够能够组成员的身份查看并执行该文件，你可以使用命令 `chmod 6755 file`，如下例所示：

```
[root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
```

```
drwx------ 2 root root 4096 May 3 21:41 dir2
-rw-r--r-- 1 root root 0 May 3 21:40 file1
-rw-r--r-- 1 root root 0 May 3 21:41 file2
[root@server1]# chmod 6755 file1
[root@server1]# ls -l
total 12
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root root 4096 May 3 21:41 dir2
drwxr-sr-x 1 root root 0 May 3 21:40 file1
drwxr-sr-x 1 root root 0 May 3 21:41 file2
```

同样，要在之前使用的目录 `dir1` 上设置粘滞权限，你可以使用命令 `chmod 1777 dir1`，这允许所有用户（包括其他人）向目录添加文件。因为你赋予了写权限；但由于你设置了粘滞位，用户只能删除他们自己的文件，而不能删除他人的。如下所示：

```
[root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root 4096 May 3 21:41 dir2
-rw-r--r-- 1 root root 0 May 3 21:40 file1
-rw-r--r-- 1 root root 0 May 3 21:41 file2
[root@server1]# chmod 1777 dir1
[root@server1  ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096  3 21:39 dir1
drwxr-xr-x 2 root 4096  3 21:41 dir2
-rw-r--r1 1 root root 0  3 21:40 file1
-rw-r1r1 1 root root 0  3 21:41 2
```

```
[root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root 4096 May 3 21:41 dir2
drwxr-sr-x 1 root root 0 May 3 21:40 file1
drwxr-sr-x 1 root root 0 May 3 21:41 file2
```

注意，所有特殊权限都需要执行权限才能正常工作；`SUID` 和 `SGID` 作用于可执行文件，而 `SGID` 和粘滞位作用于目录（目录必须具有执行权限才能访问）。

## 设置特殊权限

使用 `ls -l` 命令显示的文件模式没有特殊权限部分。然而，由于特殊权限需要执行权限，它们在使用 `ls -l` 命令时会掩盖执行权限，如图 5-7 所示。

即使文件或目录没有执行权限，系统也允许你设置特殊权限。然而如果在没有执行权限的文件或目录上设置了特殊权限，那么无效的特殊权限将以大写显示，如图 5-8 所示。

要设置特殊权限，你可以将它们可视化在模式的左侧，如图 5-9 所示。

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_0.png)

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_1.png)

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_2.png)

因此，要在某个文件或目录上设置所有特殊权限，你可以使用 `chmod 7777 name`，如图 5-9 所示。`SUID` 和 `SGID` 位通常设置在文件上。要更改之前使用的文件的权限，使其他能够以组成员的身份查看并执行该文件，你可以使用命令 `chmod 6755 file`，如下例所示：

```
[root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
```

```
drwx------ 2 root root 4096 May 3 21:41 dir2
-rw-r--r-- 1 root root 0 May 3 21:40 file1
-rw-r--r-- 1 root root 0 May 3 21:41 file2
[root@server1]# chmod 6755 file1
[root@server1]# ls -l
total 12
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root root 4096 May 3 21:41 dir2
drwxr-sr-x 1 root root 0 May 3 21:40 file1
drwxr-sr-x 1 root root 0 May 3 21:41 file2
```

同样，要在之前使用的目录 `dir1` 上设置粘滞权限，你可以使用命令 `chmod 1777 dir1`，这允许所有用户（包括其他人）向目录添加文件。因为你赋予了写权限；但由于你设置了粘滞位，用户只能删除他们自己的文件，而不能删除他人的。如下所示：

```
[root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root 4096 May 3 21:41 dir2
-rw-r--r-- 1 root root 0 May 3 21:40 file1
-rw-r--r-- 1 root root 0 May 3 21:41 file2
```

注意，所有特殊权限都需要执行权限才能正常工作；`SUID` 和 `SGID` 作用于可执行文件，而 `SGID` 和粘滞位作用于目录（目录必须具有执行权限才能访问）。

与 `SUID` 不同，`SGID` 在同时应用于文件和目录时均具有功能。正如同 `SUID` 允许普通用户执行编译好的二进制程序并在执行期间成为该文件的所有者一样，`SGID` 则允许普通用户执行编译好的二进制程序，并成为该文件所属组的成员。因此，如果一个文件属于 "sys" 组并且设置了 `SGID` 权限，那么任何执行该文件的用户在执行期间都将是 "sys" 组的成员。如果某个命令或文件要求执行它的用户具有应用到 sys 组的相同的权限，那么在文件上设置 `SGID` 可以简化为用户执行该文件分配权限的分配。

`SGID` 在设置在目录时还具有一种特殊功能。当用户创建一个文件时，请记住你的用户名将分别成为该文件的主所有者和组所有者。然而，如果用户在一个设置了 `SGID` 权限的目录中创建文件，则用户的用户名将成为文件的所有者，而目录的组将成为文件的所有者。

最后，粘滞位（sticky bit）曾用于文件以传递内存中的锁；如今，粘滞位仅在目录上执行有用的功能。回想之前的内容，应用于目录的写权限允许你向该目录添加和删除任何文件。因此，如果你对某个目录有写权限但对其中的内部文件没有权限，你就可以删除所有这些文件。考虑一家公司需要一个公共目录，赋予所有员工添加文件的能力；该目录必须赋予每个人写权限。

遗憾的是，写权限也赋予了员工删除其中所有文件和目录的能力，包括他人添加到目录的文件。如果在这个公共目录上除了写权限外还应用了粘滞位，员工可以向目录添加文件，但只能删除自己添加的文件，而不能删除他人的。

> 注意，所有特殊权限都需要执行权限才能正常工作；`SUID` 和 `SGID` 作用于可执行文件，而 `SGID` 和粘滞位作用于目录（目录必须具有执行权限才能访问）。

## 设置特殊权限

使用 `ls -l` 命令显示的文件模式没有专门的特殊权限部分。然而，由于特殊权限需要执行权限，它们在使用 `ls -l` 命令时会掩盖执行权限，如图 5-7 所示。

即使文件或目录没有执行权限，系统也允许你设置特殊权限。然而，如果在没有执行权限的文件或目录上设置了特殊权限，那么无效的特殊权限将以大写显示，如图 5-8 所示。

要设置特殊权限，你可以将它们可视化在模式的左侧，如图 5-9 所示。

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_0.png)

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_1.png)

![](img/df366d41b9a1c9a1775f9fd70c3244fb_209_2.png)

因此，要在某个文件或目录上设置所有特殊权限，你可以使用 `chmod 7777 name`，如图 5-9 所示。`SUID` 和 `SGID` 位通常设置在文件上。要更改之前使用的文件的权限，使其他能够以组成员的身份查看并执行该文件，你可以使用命令 `chmod 6755 file`，如下例所示：

```
[root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
```

```
drwx------ 2 root root 4096 May 3 21:41 dir2
-rw-r--r-- 1 root root 0 May 3 21:40 file1
-rw-r--r-- 1 root root 0 May 3 21:41 file2
[root@server1]# chmod 6755 file1
[root@server1]# ls -l
total 12
drwx------ 3 root root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root root 4096 May 3 21:41 dir2
drwxr-sr-x 1 root root 0 May 3 21:40 file1
drwxr-sr-x 1 root root 0 May 3 21:41 file2
```

同样，要在之前使用的目录 `dir1` 上设置粘滞权限，你可以使用命令 `chmod 1777 dir1`，这允许所有用户（包括其他人）向目录添加文件。因为你赋予了写权限；但由于你设置了粘滞位，用户只能删除他们自己的文件，而不能删除他人的。如下所示：

```
[root@server1]# ls -l
total 12
drwx------ 3 root 4096 Apr 8 07:12 Desktop
drwxr-xr-x 2 root 4096 May 3 21:39 dir1
drwxr-xr-x 2 root 4096 May 3 21:41 dir2
-rw-r--r-- 1 root root 0 May 3 21:40 file1
-rw-r--r-- 1 root root 0 May 3 21:41 file2
```

注意，所有特殊权限都需要执行权限才能正常工作；`SUID` 和 `SGID` 作用于可执行文件，而 `SGID` 和粘滞位作用于目录（目录必须具有执行权限才能访问）。

### 总结

- Linux 文件系统管理中，`SGID` 在同时应用于文件和目录时均具有功能。
- `SUID` 允许普通用户执行编译好的二进制程序并在执行期间成为文件所有者。
- `SGID` 允许普通用户执行编译好的二进制程序并成为文件所属组的成员。
- 如果文件属于特定组并设置了 `SGID`，执行者将成为该组成员。
- `SGID` 设置在目录时，新在该目录下创建的文件所属组将变为目录的组。
- 粘滞位（sticky bit）现在仅在目录上很有用。
- 目录的写权限允许添加或删除任何文件，但设置粘滞位可以限制用户只能删除自己的文件。
- 所有特殊权限都需要执行权限才能正常工作。

## 术语

- `/bin`: 包含所有用户使用的二进制命令的目录。
- `/boot`: 包含 Linux 内核和引导加载文件的目录。
- `/dev`: 包含设备文件的目录。
- `/etc`: 包含系统特定配置文件的目录。
- `/home`: 用户主目录的默认位置。
- `/lib`: 包含供 `/bin` 和 `/sbin` 命令使用的共享程序库的目录。
- `/mnt`: 用于挂载磁盘（如软盘和光驱）的空目录。
- `/opt`: 存储附加软件程序的目录。
- `/proc`: 包含进程和内核信息的虚拟目录。
- `/root`: root 用户的家目录。
- `/sbin`: 包含系统管理二进制命令的目录。
- `/tmp`: 存放程序创建的临时文件的目录。
- `/usr`: 包含系统命令和工具的目录。
- `/usr/local`: 大多数附加程序的所在地。
- `/var`: 包含日志文件和溢出数据的目录。
- `chgrp`: 用于更改文件或目录组所有者的命令。
- `chmod`: 用于更改文件或目录模式（权限）的命令。
- `chown`: 用于更改文件或目录所有者和组所有者的命令。
- `cp`: 用于创建文件和目录副本的命令。
- `data blocks`: 文件系统分配单元，文件内容和文件名均存储其中。
- `Filesystem Hierarchy Standard (FHS)`: 规定 Linux 系统中文件和目录位置的标准。
- `find`: 使用各种准则在文件系统中查找文件的命令。

# 关键术语 第5章 195
