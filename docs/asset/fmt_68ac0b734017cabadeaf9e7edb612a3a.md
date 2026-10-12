
列表 540 - 列出 Linux 上所有可被全世界写入的目录

如上图所示，有几个目录似乎允许所有人写入，其中包括 `/usr/local/james/bin` 目录。这确实值得进一步调查。

## 18.1.1.10 枚举未挂载磁盘

在大多数系统中，磁盘在启动时会自动挂载。因此，人们很容易忘记那些未挂载但可能包含有价值信息的磁盘。我们应始终查找未挂载的磁盘，如果它们存在，则检查其挂载权限。

在基于 Windows 的系统中，我们可以使用 `mountvol` 命令来列出所有当前已挂载的磁盘以及已物理连接但未挂载的磁盘。

```
c:\Users\student>mountvol

Creates, deletes, or lists a volume mount point.

...

Possible values for VolumeName along with current mount points are:

    \\:?\Volume{25721a7f-0000-0000-0000-100000000000}\

    *** NO MOUNT POINTS ***

    \\:?\Volume{25721a7f-0000-8000-0000-602200000000}\

    C:\

    \\:?\Volume{78fa80a6-3519-11e8-a4dc-806e6f6e6963}\

    D:\
```

列表 541 - 列出 Windows 上所有可用的可挂载磁盘

在这种情况下，系统有两个挂载点，分别映射到 C: 和 D: 磁盘。我们还注意到，有一个卷的全局唯一标识符 GUID 为 `25721a7f-0000-0000-0000-100000000000`，但它没有挂载点。这可能很有趣，我们可能希望进一步调查。

在基于 Linux 的系统中，我们可以使用 `mount` 命令来列出所有已挂载的文件系统。此外，`/etc/fstab` 文件列出了将在启动时挂载的所有磁盘。

> 请记住，系统管理员可能使用了自定义配置或脚本来挂载那些未在 `/etc/fstab` 文件中列出的磁盘。

因此，良好的实践不仅是扫描 `/etc/fstab`，还要使用 `mount` 收集关于已挂载磁盘的信息。

```
student@debian:~$ cat /etc/fstab

# /etc/fstab: static file system information.

#

# <file system> <mount point> <type> <options> <dump> <pass>

# / was on /dev/sda1 during installation

UUID=fa336f7a-8cf8-4cd2-9547-2208b6cf58b7 / ext4 errors=remount-ro 0 1

# swap was on /dev/sda5 during installation

UUID=8b701d25-e29e-49dc-b61b-1b9047088150 none swap sw 0 0

/dev/sr0 /media/cdrom0 udf,iso9660 user,noauto 0 0
```

```
student@debian:~$ mount

sysfs on /sys type sysfs (rw,nosuid,nodev,noexec,relatime)

proc on /proc type proc (rw,nosuid,nodev,noexec,relatime)

udev on /dev type devtmpfs (rw,nosuid,relatime,size=505664k,nr_inodes=126416,mode=755)

depts on /dev/pts type devpts (rw,nosuid,noexec,relatime,gid=5,mode=620,ptmxmode=000)

tmpfs on /run type tmpfs (rw,nosuid,noexec,relatime,size=102908k,mode=755)

/dev/sda1 on / type ext4 (rw,relatime,errors=remount-ro,data=ordered)

securityfs on /sys/kernel/security type securityfs (rw,nosuid,nodev,noexec,relatime)

tmpfs on /dev/shm type tmpfs (rw,nosuid,nodev)

tmpfs on /run/lock type tmpfs (rw,nosuid,nodev,noexec,relatime,size=5120k)

tmpfs on /sys/fs/cgroup type tmpfs (ro,nosuid,nodev,noexec,mode=755)
```

列表 542 - 列出 Linux 上 `/etc/fstab` 的内容和所有已挂载磁盘

输出显示了一个交换分区和该 Linux 系统的主 ext4 磁盘。此外，我们可以使用 `lsblk` 查看所有可用的磁盘。

```
student@debian:~$ /bin/lsblk

NAME MAJ:MIN RM SIZE RO TYPE MOUNTPOINT

fd0 2:0 1 4K 0 disk

sda 8:0 0 5G 0 disk

├sda1 8:1 0 4.7G 0 part /

├sda2 8:2 0 1K 0 part

└sda5 8:5 0 334M 0 part [SWAP]
```

列表 543 - 在 Linux 上使用 lsblk 列出所有可用磁盘

我们注意到 `sda` 磁盘由三个不同的分区组成，这些分区带有编号。在某些情况下，显示系统中所有本地磁盘的信息可能会揭示未挂载的分区。根据系统配置，或错误配置，我们随后可能能够挂载这些分区，并搜索有趣的文档、凭据或其他允许我们提升权限或更好地在网络上立足的信息。

## 18.1.1.11 枚举设备驱动程序和内核模块

另一种常见的权限提升方法涉及利用设备驱动程序和内核模块。我们将在本模块稍后查看实际的利用技术，但让我们先看一下一种重要的枚举技术。由于该技术依赖于将漏洞与相应的利用工具匹配，我们需要编译一份目标系统上已加载的驱动程序和内核模块列表。

在 Windows 上，我们可以使用 `driverquery` 命令开始搜索。我们将提供 `/v` 参数以获取详细输出，并提供 `/fo csv` 以请求以 CSV 格式输出。

为了过滤输出，我们将在 PowerShell 会话中运行此命令。在 PowerShell 中，我们将把输出管道传输到 `ConvertFrom-CSV` 命令以及 `Select-Object`，这将允许我们选择特定的对象属性或包括“显示名称”、“启动模式”和“路径”在内的对象集合。

```
c:\Users\student> powershell

PS C:\Users\student> driverquery.exe /v /fo csv | ConvertFrom-CSV | Select-Object 'Display Name', 'Start Mode', Path
```
