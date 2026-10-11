
```
-rw-r--r--  1 sueb  sueb         5542 Jul 15:37 .canna

-rw-r--r--  1 sueb  sueb           820 Jul 15:37 .emacs

-rw-r--r--  1 sueb  sueb         118 Jul 15:37 .gtkrc

-rw-r--r--  1 sueb  sueb        4096 Jul 15:37 .kde

drwx-xr-xr  2 sueb  sueb        4096 Jul 15:37 .x-enas

-rw-r--r--  1 sueb  sueb        3511 Jul 15:37 .zshrc

[root@server1]#
```

## 管理组

目前，向系统添加组的最简单方法是使用编辑器处理 `/etc/group` 文件。另一种方法是使用 `groupadd` 命令。向系统添加一个名为 `group1` 并为其分配 GID `492`，可以使用以下命令：

```
[root@server1]# groupadd -g 492 group1

[root@server1]#
```

然后，你可以使用 `usermod` 命令的 `-G` 选项添加成员。将用户 `maryj` 添加到该组并查看添加情况，可以使用以下 `usermod` 命令：

```
[root@server1]# usermod -G group1 maryj

[root@server1]# tail /etc/group

group1:x:492:maryj
```

还有一个命令可以修改组名和 GID，以及 `groupdel` 命令可以从系统中删除组。要查看你所属的组列表，只需运行 `groups` 命令；要查看每个组的 GID，只需运行 `id` 命令。主组总是由每个命令列出。以下是 root 用户执行这些命令的输出：

```
[root@server1]# groups

root bin disk

uid=0(root) gid=0(root) groups=0(root), 1(bin), 2(daemon), 3(sys), 4(adm), 6(disk), 10(wheel)

[root@server1]#
```

你可以从前面的输出中看到 root 用户的主组是 root。该组作为 root 用户创建的所有文件的组所有者，如下所示所示：

```
[root@server1]# touch samplefile

[root@server1]# ls -l samplefile

-rw-r--r-- 1 root root 0 Jul 17 samplefile

[root@server1]# _
```

要将主组临时更改为 `groups` 和 `id` 命令输出中的另一个组，可以使用 `newgrp` 命令。之后创建任何新文件都具有新的组所有者。以下输出演示了更改 root 用户主组的影响：

```
[root@server1]# newgrp sys

[root@server1]# id

uid=0(root) gid=3(sys) groups=0(root), 1(bin), 2(daemon), 3(sys), 4(adm), 6(disk), 10(wheel)

[root@server1]# touch sample2

[root@server1]# ls -l sample2

-rw-r--r-- 1 root sys 0 Jul 17 sample2

[root@server1]# _
```
