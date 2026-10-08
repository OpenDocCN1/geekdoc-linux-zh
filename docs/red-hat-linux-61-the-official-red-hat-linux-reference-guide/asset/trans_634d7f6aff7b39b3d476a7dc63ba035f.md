

# 第 9 章 网络文件系统 (NFS)

| 100003 | 2 | udp | 2049 | nfs |
| 100003 | 3 | udp | 2049 | nfs |
| 100221 | 1 | udp | 1028 | nlockmgr |
| 100221 | 3 | udp | 1028 | nlockmgr |
| 100221 | 4 | udp | 1028 | nlockmgr |

- -p 选项显示指定主机上的 portmap，如果没有列出特定主机，则默认到 localhost。可以从 rpcinfo 文件中获取其他选项。
从该输出中可以看出，显然有多种 NFS 服务正在运行。如果其中一个 NFS 服务没有正确启动，portmap 将无法将客户端来自该服务的 RPC 请求映射到正确的端口。在许多情况下，以 root 身份重启 NFS (`/sbin/service nfs restart`) 将使这些服务正确地向 portmap 注册并开始工作。

# 9.2. NFS 服务器配置文件

使用 NFS 配置服务器共享文件和目录是一个简单的过程。每个文件系统都通过 NFS 导出给远程用户，而与这些文件相关的访问权限位于 `/etc/exports` 文件中。该文件由 `exportfs` 命令读取，为 `rpc.mountd` 和 `rpc.nfs` 提供允许授权主机远程挂载文件系统所需的信息。
`exportfs` 命令允许 root 用户在不重启服务的情况下选择性地导出或取消目录。当向 `exportfs` 传递选项时，导出的文件系统将被写入到 `/var/lib/nfs/stab`。由于 `rpc.mount` 在决定文件系统的访问权限时引用 `xtab`，因此对导出文件列表的更改将立即生效。
使用 `exportfs` 时可以使用多种选项：

- -r — 通过在 `/etc/lib/nfs/stab` 中构建新的导出列表，使 `/etc/exports` 中列出的所有目录都被导出。此选项实际上根据 `/etc/exports` 中已做的任何更改刷新导出列表。
- a — 根据传递给 `exportfs` 的其他选项，对所有目录进行导出或取消导出。
- o — 允许用户指定 `/etc/exports` 中未列出的导出目录。此额外的文件系统必须以在 `/etc/exports` 中指定的相同方式写入。此选项用于在将导出的文件系统永久添加到导出文件列表之前对其进行测试。
- i — 忽略 `/etc/exports`；仅使用从命令行提供的选项来定义导出的文件系统。
- u — 取消远程用户挂载的目录。命令 `exportfs -ua` 实际上在保持各种 NFS 守护进程运行的同时挂 NFS 共享。要允许 NFS 共享继续，输入 `exportfs -r`。
- v — 详细输出，在执行 `exportfs` 命令时，将更详细地显示导出或取消导出的文件系统。

如果未向 `exportfs` 命令传递任何选项，它将显示当前导出的文件系统列表。
也可以通过 `service nfs reload` 命令重载 NFS 服务来对 `/etc/exports` 进行更改。这在重新导出 `/etc/exports` 文件的同时保持 NFS 守护进程运行。

# 第 9 章 网络文件系统 (NFS)

# 9.2.1. /etc/exports

`/etc/exports` 文件控制哪些文件导出到远程主机并指定选项。空行会被忽略，可以通过以哈希标记 (`#`) 开头创建，长行可以使用反斜杠 (`\`) 换行。每个导出的文件系统都应单独占有一行。放置在导出文件系统之后的授权主机列表必须用空格字符分隔。每个主机的选项必须放置在主机标识符后的括号内，第一个和最后一个括号之间不能有空格。

在最简单的形式下，`/etc/exports` 只需要知道导出的目录和允许使用它的主机：

```
/some/directory bob.example.com
another/exported/directory 192.168.0.3
```

使用 `/bin/service nfs reload` 命令重新导出 `/etc/exports` 后，bob.example.com 主机将能够挂载 `/some/directory`，192.168.0.3 能够挂载 `another/exported/directory`。由于此示例中没有指定选项，将采取若干默认的 NFS 偏好：

- Read（读）——挂载此文件系统的主机将无法更改它。要允许主机更改文件系统，必须指定 `rw`（读写）选项。
- async（异步）——允许服务器在认为合适时写入磁盘。虽然如果主机以只读方式访问，或者主机对读写文件系统进行更改且服务器崩溃，这很重要，但可能会丢失数据。通过指定 `sync`（同步）选项，所有写入操作将提交到客户端请求的磁盘。这可能会提高性能。
- wdelay（写延迟）——如果 NFS 怀疑即将发生其他写入操作，则延迟写入磁盘。这可以通过减少磁盘被单独写入命令访问的次数来减少开销，从而提高性能。`no_wdelay` 选项关闭此功能，但仅在使用 `sync` 选项时可用。
- root_squash（根用户压缩）——通过将远程连接的 root 分配为 `nobody` 用户，剥夺其 root 权限。这实际上将 root 用户的权力“压缩”为本地用户，防止远程用户像在本地系统上作为 root 一样操作。`no_root_squash` 选项关闭根用户压缩。要压缩每个使用 root 的远程用户，使用 `all_squash` 选项指定。

如果未向 `exportfs` 命令传递任何选项，它将显示当前导出的文件系统列表。
对 `/etc/exports` 的更改也可以通过 `service nfs reload` 命令重载 NFS 服务来完成。这在重新导出 `/etc/exports` 文件的同时保持 NFS 守护进程运行。

# 第 9 章 网络文件系统 (NFS)

# 9.2.1. /etc/exports

`/etc/exports` 文件控制哪些文件导出到远程主机并指定了选项。空行会被忽略，可以通过以哈希标记 (`#`) 开头创建，长行可以使用反斜杠 (`\`) 换行。每个导出的文件系统都应单独占有一行。放置在导出文件系统之后的授权主机列表必须用空格字符分隔。每个主机的选项必须放置在主机标识符后的括号内，第一个和最后一个括号之间不能有空格。

在最简单的形式下，`/etc/exports` 只需要知道导出的目录和允许使用它的主机：

```
/some/directory bob.example.com
another/exported/directory 192.168.0.3
```

使用 `/bin/service nfs reload` 命令重新导出 `/etc/exports` 后，bob.example.com 主机将能够挂载 `/some/directory`，192.168.0.3 能够挂载 `another/exported/directory`。由于此示例中没有指定选项，将采取若干默认的 NFS 偏好：

- Read（读）——挂载此文件系统的主机将无法更改它。要允许主机更改文件系统，必须指定 `rw`（读写）选项。
- async（异步）——允许服务器在认为合适时写入磁盘。虽然如果主机以只读方式访问，或者主机对读写文件系统进行更改且服务器崩溃，这很重要，但可能会丢失数据。通过指定 `sync`（同步）选项，所有写入操作将提交到客户端请求的磁盘。这可能会提高性能。
- wdelay（写延迟）——如果 NFS 怀疑即将发生其他写入操作，则延迟写入磁盘。这可以通过减少磁盘被单独写入命令访问的次数来减少开销，从而提高性能。`no_wdelay` 选项关闭此功能，但仅在使用 `sync` 选项时可用。
- root_squash（根用户压缩）——通过将远程连接的 root 分配为 `nobody` 用户，剥夺其 root 权限。这实际上将 root 用户的权力“压缩”为本地用户，防止远程用户像在本地系统上作为 root 一样操作。`no_root_squash` 选项关闭根用户压缩。要压缩每个使用 root 的远程用户，使用 `all_squash` 选项指定。

> > 警告 `/etc/exports` 文件的格式非常精确，特别是关于空格字符的使用。请始终在保存另一个空格字符的导出文件系统时小心。然而，除注释行外，文件中不应有空格字符。
> 例如，这两行的含义并不相同：

```
/home bob.example.com (rw)
home bob.example.com
```

第一行允许来自 bob.example.com 的用户对 /home 目录具有读写权限。然而，这第二行允许 bob.example.com 的用户以只读方式挂载目录（默认值），但其他用户可以读写方式挂载它。

# 9.3. NFS 客户端配置文件

服务器提供的任何 NFS 共享都可以使用多种方法挂载。可以使用 `mount` 命令手动挂载共享。然而，这需要 root 用户每次系统重启时输入 `mount` 命令。自动挂载 NFS 共享的两种方法是通过修改 `/etc/fstab` 或使用 `autofofs` 服务。

# 9.3.1. /etc/fstab

在 `/etc/fstab` 文件中放置格式正确的行与挂载导出文件系统的效果相同。`/etc/fstab` 文件由 `/etc/rc.init.d/netfs` 脚本在系统启动时读取，列出的任何 NFS 共享将被挂载。

一个示例 `/etc/fstab` 如下：

```
<server>:/path/to/dir <local/mount/point> nfs <options> 0 0
```

`<server>` 对应导出文件系统的主机名、IP 地址或完全域名。

`<local/mount/point>` 指定挂载导出目录的本地系统。此挂载点在读取 `/etc/fstab` 之前必须存在，否则挂载将失败。

`nfs` 选项指定了要挂载的文件系统类型。

