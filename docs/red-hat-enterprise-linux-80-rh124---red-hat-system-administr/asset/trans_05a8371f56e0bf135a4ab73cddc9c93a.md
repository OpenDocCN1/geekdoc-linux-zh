

# 第一章 | 访问 Linux 系统

要挂载文件系统，目标目录必须已经存在。`/mnt` 目录默认存在，并打算用临时挂载点。

你可以使用 `/mnt`，或者更好的做法是在 `/mnt` 下创建一个子目录作为临时挂载点，除非你有充分的理由将其挂载到文件系统层次结构中的特定位置。

> 重要提示
> 如果作为挂载点的目录不为空，则在文件系统挂载之前复制到该目录的任何文件在文件系统卸载之前都是无法访问的。

这种方法在短期内运行良好。然而，如果系统中添加或删除了设备，操作系统检测设备的顺序可能会发生变化。这将改变与该存储设备关联的设备名称。更好的方法是根据文件系统内置的某些特征进行挂载。

# 通过文件系统 UUID 挂载

与文件系统关联的一个稳定标识符是它的 UUID，这是一个非常长的十六进制数字，作为文件系统的一部分，且除非重新创建，否则它将保持不变。

`lsblk -fp` 命令列出设备的完整路径，以及 UUID 和挂载点，以及分区中的文件系统类型。如果文件系统未挂载，则挂载点将为空。

```
[root@host ~]# lsblk -fp
NAME FSTYPE UUID MOUNTPOINT
/dev/vda
/dev/vda1 xfs 23ea8883-a396-494a-82e5-1538a5b821c /boot
/dev/vda2 swap cdf6162d-534c-4bd6-b458-cab1b81a72ea [SWAP]
/dev/vda3 xfs 4438f15-2f9d-4745-ae2e-20844f27262/
/dev/vdb
/dev/vdb1 xfs 46f543d-78c9-4526-a857-244811e2d88
```

通过文件系统的 UUID 挂载文件系统。

```
[root@host ~]# mount UUID="46f543d-78c9-4526-a857-244811e2d88" /mnt/data
```

# 可移动存储设备的自动挂载

如果你已登录并使用图形桌面环境，它会在插入可移动存储介质时自动挂载。

可移动存储设备挂载在 `/run/media/USERNAME/LABEL`，其中 `USERNAME` 是登录图形环境的用户名，`LABEL` 是一个标识符，通常是创建文件时赋予的文件的名称（如果有的话）。

在移除设备之前，你应该卸载它。

# 卸载文件系统

关机和重启程序会自动卸载所有文件系统。作为此过程的一部分，内存缓存的任何文件系统数据都会刷新到存储设备，从而确保文件系统不会发生数据损坏。

> 警告
> 文件系统数据缓存在内存中。因此，为了避免损坏磁盘上的数据，在拔掉驱动器之前卸载它们是关重要的。卸载程序在释放驱动器之前同步数据，以确保数据完整性。

要卸载文件系统，`unmount` 命令需要挂载点作为参数。

```
[root@host ~]# unmount /mnt/data
```

如果挂载的文件系统正在使用中，则无法卸载。要使 `unmount` 命令成功，所有进程都需要停止访问挂载点下的数据。

在下面的示例中，卸载失败是因为文件系统正在使用（shell 将 `/mnt/data` 作为当前工作目录），生成了错误消息。

```
[root@host ~]# cd /mnt/data
[root@data]# unmount /mnt/data
unmount: /mnt/data: target is busy.
```

`lsof` 命令列出指定目录中的所有打开文件以及访问它们的进程。这对于识别哪些进程阻止了文件系统的成功卸载很有用。

| COMMAND | PID USER FD TYPE DEVICE SIZE/OFF NODE NAME |
| :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- | :--- |
| bash | 1593 | root | cwd | DIR | 253,17 | 6 | 128 | /mnt/data |
| lsof | 2532 | root | cwd | DIR | 253,17 | 19 | 128 | /mnt/data |
| lsof | 2533 | root | cwd | DIR | 253,17 | 19 | 128 | /mnt/data |

一旦识别出进程，就可以采取行动，例如等待进程完成或向进程发送 `SIGTERM` 或 `SIGKILL`。在这种情况下，将当前工作目录更改到挂载点之外即可。

```
[root@data]# cd
[root@host ~]# /mnt /data
```

> 注意
> 文件系统卸载失败的一个常见原因是 Bash shell 正将挂载点或其子目录作为当前工作目录。使用 `cd` 命令离开文件系统解决此问题。

# 参考

lsblk(8), mount(8), umount(8) 和 lsof(8) 手页

# 引导练习

# 挂载和卸载文件系统

在此练习中你将练习挂载和卸载文件系统。

预期结果
你应该能够在指定的挂载点挂载一个新的文件系统，然后卸载它。

开始之前
在工作站上以 `student` 用户身份登录。
从工作站运行 `lab fs-mount` 命令。该命令运行一个脚本来判断 `host,servera` 是否可达。该脚本在 `servera` 的第二个磁盘上创建一个分区。

```
[student@workstation ~]$ lab fs-mount
```

1. 使用 `ssh` 命令以 `student` 用户登录 `servera`。

```
[student@workstation ~]$ ssh servera
[student@servera ~]$
```

2. `servera` 的第二个磁盘 (`/dev/vdb`) 添加了一个带有文件系统的分区。通过 UUID 将新可用分区挂载到新创建的挂载点 `/mnt/namespace`。使用 `su -` 命令切换到 root 用户以手动挂载设备。

```
[student@servera ~]$ su -
Password: redhat
[root@servera ~]$
```

2.2. 创建 `/mnt/namespace` 目录。

3. 使用带有 `-fp` 选项的 `lsblk` 命令设备 `/dev/vdb` 的 UUID。

```
[root@servera ~]# lsblk -fp /vdb
NAME FSTYPE UUID MOUNTPOINT
/dev/vdb xfs 04c511a-b005-4ec2-981f-42d1fc65
```

4. 在 `/mnt/namespace` 目录上使用 UUID 挂载文件系统。将 UUID 替换为上一个命令中 `vdb` 磁盘的 UUID。

```
[root@servera ~]# mount UUID="04c511a-b005-4ec2-981f-42d1fc65" /mnt/namespace
```

5. 验证 `/vdb` 设备已挂载在 `/mnt/namespace` 目录上。

```
[root@servera ~]# lsblk -fp /vdb
NAME FSTYPE UUID MOUNTPOINT
/dev/vdb xfs 04c511a-b005-4ec2-981f-42d1fc65 /mnt/namespace
```

3. 切换到 `/mnt/namespace` 目录并创建一个新目录 `/mnt/namespace/newdir` 以及一个空文件 `/mnt/namespace/myfile`。

3.1. 切换到 `/mnt/namespace` 目录。

```
[root@servera ~]# cd /mnt/namespace
```

3.2. 创建目录 `/mnt/namespace/newdir`。

```
[root@namespace]# mkdir newdir
```

3.3. 创建空文件 `/mnt/namespace/myfile`。

```
[root@namespace]# touch myfile
```

4. 卸载挂载在 `/mnt/namespace` 上的文件系统。

4.1. 当 shell 的当前目录仍为 `/mnt/namespace` 时，使用 `umount` 命令卸载 `/mnt/namespace`。`umount` 命令无法卸载设备。

```
[root@namespace]# umount /mnt/namespace
umount: /mnt/namespace: target is busy.
```

4.2. 将 shell 的当前目录更改到 `/root`。

```
[root@namespace]# cd
[root@~]#
```

4.3. 现在成功卸载 `/mnt/namespace`。

```
[root@~]# umount /mnt/namespace
```

5. 退出 `servera`。

```
[root@servera ~] exit
logout
[student@servera ~]$ exit
logout
Connection to servera closed.
[student@workstation]$
```

# 完成

在工作站上运行 `lab fs-mount finish` 脚本完成此练习。

```
[student@workstation ~]$ lab fs-mount finish
```

引导练习结束。

# 在系统中查找文件

# 目标

完成本节后，你应该能够 `find` 和 `locate` 在挂载的文件系统上搜索文件。

# 搜索文件

系统管理员需要在文件系统上搜索符合特定标准的文件本节讨论了两个可以在文件系统层次结构中搜索文件的命令。

- `locate` 命令在预先生成的索引中搜索文件名或文件路径并立即返回结果。
- `find` 命令通过遍历文件系统层次结构实时搜索文件。

# 按名称查找文件

`locate` 命令根据名称或文件路径查找文件。它很快，因为它从 *locate* 数据库中查找信息。该数据库不是实时更新的，必须频繁更新以确保结果准确。这意味着 `locate` 将无法找到自上次更新数据库以来创建的文件。

`locate` 数据库每天自动更新。然而，**root** 用户可以随时发布 `updatedb` 命令强制立即更新。

```
[root@host ~]# updatedb
```

`locate` 命令限制了非特权用户的结果。为了看到结果名称，用户必须对文件所在的目录具有搜索权限。

使用 `passwd` 在宿主机上所有者重建的目录树按名称或路径搜索文件。

```
[user@host ~]$ locate passwd
/etc/passwd
/etc/passwd-
/etc/pam.d/passwd
/etc/security/opasswd
/usr/bin/passwd
/usr/bin/grub2-mkpassword-pbkdf2
/usr/bin/lpppasswd
/usr/bin/passwd
...output omitted...
```

当文件名或路径仅与搜索查询的部分匹配时，将返回结果。

```
[root@host ~]# locate image
/etc/selinux/targeted/contexts/virtual_image_context
/usr/bin/grub2-miimage
```

