

# 790 章 第 22 章 NFS：共享文件系统

```
/var/lib/nfs/rmtab
```

（远程挂载表）在服务器上，该文件列出了被客户端系统挂载的目录树：

```
$ cat /var/lib/nfs/rmtab
192.168.0.12:/p16:0x00000002
```

上述输出显示 /p1 被 192.168.0.12 挂载。`rmtab` 文件由 `mountd` 在挂载和卸载目录时进行更新。该文件“大多是装饰性的”（参见 `mount` 页面），可能并不准确。

/proc/mounts 在客户端上，这个伪文件显示内核挂载表，其中列出了由本地系统挂载的文件。在接下来的示例中，`grep` 显示包含字符串 `nfs` 且紧跟一个空格的行。必须对这个空格加引号，这样可以排除掉不包含与挂载文件相关的字符串的行。

```
$ grep nfs /proc/mounts
plum:/p16 /mnt nfs rw,vers=3,rsize=131072,wsize=131072,hard,intr,proto=tcp,timeout=600,retrans=2,sec=sys,addr=plum 0 0
```

# showmount：显示 NFS 状态信息

在不带任何选项的情况下，`showmount` 工具显示允许挂载本地目录的系统列表。你通常使用 `showmount` 显示服务器正在导出的目录树列表。要显示远程系统的信息，请将远程系统的名称作为参数。`showmount` 显示的信息可能不完整，因为它依赖于 `mountd` 并信任远程服务器报告的准确性。

在接下来的示例中，192.168.0.12 被允许挂载本地目录，但你不知道具体是哪些目录：

```
$ showmount
Hosts on plum:
192.168.0.12
```

如果 `showmount` 显示类似 `RPC: Program not registered` 的错误，则说明服务器上没有运行 NFS。使用 `nfs-kernel-server` 初始化脚本（第 782 页）在服务器上启动 NFS。

- -a (All) 显示客户端系统列表，并指示每个客户端系统可以挂载哪些目录。这些信息存储在 `/etc/exports` 中。在接下来的示例中，显示 192.168.0.12 可以从本地系统挂载：

```
$ sbin/showmount -a
All mount points on plum:
192.168.0.12:/p16
```

- -e (exports) 显示导出的目录列表以及每个目录导出的目标系统。

```
$ showmount -e
Export list for plum:
/p16 192.168.0.12
```

# exportfs：维护导出的目录树列表

`exportfs` 工具维护 `/var/lib/nfs/stab` 文件（第 789 页）。当调用 `mount` 时，它会检查此文件以确认该系统是否被允许挂载请求的目录树。通常，`exportfs` 使用简单的选项被调用，并根据 `/etc/exports` 的更改修改 `stab` 文件。当带有客户端和目录参数被调用时，它可以从 `stab` 维护的列表中添加或删除由参数指定的目录树，而无需引用 `exports` 文件。`exportfs` 命令的格式如下：

```
/usr/sbin/exportfs [options] [client:dir ...]
```

其中 `options` 是一个或多个选项（在下一节中讨论），`client` 是 `dir` 导出的系统名称，`dir` 是正在导出目录树根部目录的绝对路径。在不带任何参数的情况下，`exportfs` 会报告哪些目录树导出到了哪些系统：

```
$ exportfs
/home      grape
/p16      jam
/p16      192.168.0.12
```

系统在启动时会执行以下命令（位于 `nfs-kernel-server` 初始化脚本中）。该命令重新导出 `/etc/exports` 中的条目，并从 `/var/lib/nfs/stab` 中移除无效条目；`stab` 会与 `/etc/exports` 同步：

```
$ sudo exportfs -r
```

# 选项

- -a (all) 导出 `/etc/exports` 中指定的目录树。此选项不会取消你已从 exports 中删除的条目（即，它不会从 `/var/lib/nfs/stab` 中移除条目）；请使用 -r 执行此任务。
- -f (flush) 从内核导出表中移除所有内容。
- -i (ignore) 忽略 `/etc/exports`；仅使用命令行指定的指定。
- -o (options) 你可以像在 exports 文件中那样的指定选项。例如，`exportfs -i -o dog/home exports/home` 在本地系统上以只读方式导出 /home。
- -r (reexport) 重新导出 `/etc/exports` 中的条目。
- -u (unexport) 卸载导出的目录树。
- -v (verbose) 详细模式，提供更详细的信息。

# 测试服务器配置

在服务器上运行 NFS 挂载，系统会显示以下内容：

```
$ grep nfs /proc/mounts
plum:/p16 /mnt nfs rw,vers=3,rsize=131072,wsize=131072,hard,intr,proto=tcp,timeout=600,retrans=2,sec=sys,addr=plum 0 0
```

检查 mountd 是否正在运行：

```
$ ps aux | grep mountd
```

使用 rpcinfo 检查 NFS 服务：

```
$ rpcinfo -p
```

查看挂载状态：

```
$ df -h
```

查看导出列表：

```
$ showmount -e
```

在客户端挂载点：

```
$ grep nfs /proc/mounts
plum:/p16 /mnt nfs rw,vers=3,rsize=131072,wsize=131072,hard,intr=proto=tcp,timeout=600,retrans=2,sec=sys,addr=plum 0 0
```

查看服务器导出的目录：

```
$ showmount -e
Export list for plum:
/p16 192.168.0.12
```

重新导出配置：

```
$ sudo exportfs -r
```

# autofofs：按需挂载目录树

autofofs 目录树类似于任何其他目录树，但在被需要之前保持未挂载状态（按需挂载）。系统在空闲 5 分钟后会自动卸载 autofofs 目录树。挂载的目录树是管理大量系统的一个重要部分。automount 服务在安装包含大量服务器或目录树时特别有用。它有助于消除服务器之间的依赖。

当启动一个使用传统 fstab 挂载的系统且 NFS 服务器宕机时，系统可能需要很长时间才能启动，因为它在等待服务器超时。同样，当有两个服务器互相挂载目录树时，可能会挂起，因为它们都在尝试挂载对方的目录树。这种情况被称为服务器之间的依赖。autofofs 功能通过在进程尝试访问时从另一个系统挂载目录树来解决这些问题。当进程尝试访问未挂载的 autofofs 目录树中的某个目录时，内核会通知 automount 服务，由其挂载目录树。你必须使用类似 /home/zach 访问 autofofs 挂载点的命令来触发导致 automount 挂载 autofofs 目录树的请求；只有这样系统才能显示或使用 autofofs 目录树。在使用它命令之前，zach 不出现在 /home 中。

# 前提条件

安装以下软件包：

- autofofs

当安装 autofofs 包时，dpkg postinst 脚本会启动 automount 服务。在配置 automount 后，运行以下命令重启 automount：

```
sudo service autofofs restart
```

在活动服务器上更改 automount 配置后，使用 reload 代替 restart 以干扰自动挂载的文件系统。

# autofofs：按需挂载目录树

autofofs 目录树类似于任何其他目录树，但在被需要之前保持未挂载状态（按需挂载）。系统在空闲 5 分钟后会自动卸载 autofofs 目录树。挂载的目录树是以一致方式管理大量系统的重要部分。automount 服务在安装包含大量服务器时特别有用。它有助于消除服务器之间的依赖。

当你启动一个使用传统 fstab 挂载的系统且 NFS 服务器宕机时，系统可能需要很长时间才能启动，因为它在等待服务器超时。同样，当有两个服务器互相挂载目录树时，可能会挂起，因为它们都在尝试挂载对方的目录树。这种情况被称为服务器之间的依赖。autofofs 功能通过在进程尝试访问时从另一个系统挂载目录树来解决这些问题。当进程尝试访问未挂载的 autofofs 目录树中的某个目录时，内核会通知 automount 服务，由其挂载目录树。你必须使用类似 /home/zach 访问 autofofs 挂载点的命令来触发导致 automount 挂载 autofofs 目录树的请求；只有这样系统才能显示或使用 autofofs 目录树。在使用它命令之前，zach 不出现在 /home 中。

控制 automount行为的主文件是 /etc/auto.master。一个简单的示例如下：

```
$ /etc/auto.master
/free    /etc/auto.misc  --timeout=60
/plum     /etc/auto.plum
```

auto.master 文件有三列。第一列指定 autofofs 挂载点的父目录——即要挂载 autofofs 目录树的位置。（示例中的 /free 和 /plum 目录不是挂载点，但将作为挂载目录树的位置。）

