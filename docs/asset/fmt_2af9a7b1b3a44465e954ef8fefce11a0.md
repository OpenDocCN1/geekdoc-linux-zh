
> 注意：`allowed_hosts` 和 `(options)` 之间没有空格。如果包含空格，选项将应用于任何和所有 IP 地址，如果授予了写权限，这可能是非常危险的。

必须指定 `sync` 或 `async` 作为 NFS 选项。如果指定了 `sync`，服务器将等待请求写入磁盘后响应客户端。建议使用 `sync` 选项，因为它符合 NFS 协议。

要为导出目录授予读写权限，请使用 `rw` 选项。有关其他选项，请参阅上一个图形化配置部分。要查看 NFS 服务器选项的完整列表，请通过命令 `exports` 查看 man 页面。选项之间应用逗号分隔。

## 启动和停止 NFS 服务器

`root` 用户必须执行启动和重新加载 NFS 服务器的命令。启动 NFS 服务器，执行命令 `service nfs start`。停止服务器，执行命令 `service nfs stop`。如果服务器已启动且更改了 `/etc/exports` 配置文件，必须重新加载 NFS 服务器。使用命令 `service nfs reload` 强制服务器重新读取配置文件。

### 第 13 章 网络文件共享

要让服务在启动时自动启动，请作为 `root` 用户使用 `chkconfig`：`chkconfig nfs on`

要验证 NFS 服务器正在运行，执行命令 `service nfs status`。

## 分配静态 NFS 端口

参考 `/etc/services` 查看系统上其他服务已保留的端口列表，并将 1024 以上的端口分配给 `statd`、`mount`、`rquotad` 和 `lock` 服务。在本示例中，将使用以下端口：

- TCP 和 UDP 端口 3001 用于 `statd`
- TCP 和 UDP 端口 3002 用于 `lock`
- TCP 和 UDP 端口 3003 用于 `mount`
- TCP 和 UDP 端口 3004 用于 `rquotad`
- TCP 和 UDP 端口 3005 用于 `status`
- TCP 和 UDP 端口 3006 用于 `lock`

NFS 守护进程需要使用特定端口以配合某些防火墙设置。如果不需要强制特定端口，请将这些字段留。静态端口也可以通过图形配置工具分配。启动工具后，点击服务器设置（Server Settings）按钮。出现图 13.4 所示的对话框。

### 服务器设置

为了配合某些防火墙设置，守护进程需要使用特定端口。如果不需要强制特定端口，请将这些字段留。

| rpc.lockd (TCP) | rpc.lockd (UDP) |
|---|---|
| rpc.mount (TCP) | rpc.stat (TCP) |

图 13.4 分配静态端口

提供所需的端口并点击 OK。

## 连接到 NFS 共享

假设服务器允许客户端这样做，在客户端上挂载 NFS 导出三种方法：

- 使用 `mount` 命令配合服务器名称、导出目录和本地挂载点。
- 将导出添加到 `/etc/fstab`，以便在启动时自动挂载或可供挂载。
- 使用 `autofs` 服务在用户尝试访问时挂载共享。

### 使用 mount 连接到 NFS 共享

如果您只需要偶尔挂载共享（或者您正在测试导出），请使用 `mount` 命令。作为 `root` 创建挂载共享的目录，执行以下命令：

```
mount -o <options> server.example.com:/exporteddir /mountpoint
```

替换服务器名称、导出目录和本地挂载点。默认，共享以读写模式挂载，这意味着保留了服务器的所有文件权限。重要的是，文件权限是基于用户 ID 和组 ID 的，而不是 NFS 服务器上的用户名和组名。如果客户端被服务器允许，则共享目录将在客户端上指定的挂载点可用。

可以使用任何 NFS 选项替换 `<options>`，包括以下选项：

- `rsize=8192`
- `wsize=8192`
- `timeo=14`
- `intr`

`rsize` 值是从服务器读取数据时使用的字节数。`wsize` 是写入服务器时使用的字节数。两者的默认值均为 1024，但使用 8192 可以大幅提高吞吐量，并建议这样做。超时值是在进行 RPC 计算后发送传输之前等待的时间，以秒的十分分之一为单位。在第一次超时后，超时值将翻倍以进行重试，最长持续 60 秒，或直到发生主要超时。如果连接到慢速服务器或通过繁忙的网络，可以通过增加此超时值来获得更好的性能。`intr` 选项允许在硬挂载共享发生主要超时时中断文件操作。请参阅命令 `nfs` 的 NFS 页面以获取可用选项的完整列表。

## 使用 /etc/fstab 连接到 NFS 共享

在验证客户端可以挂载共享后，可以通过按照如下方式修改 `/etc/fstab` 文件来配置系统在启动时挂载：

```
server:/exported/dir /mountpoint nfs size=8192,wsize=8192,intr
```

将服务器名称、导出目录和挂载点替换为相应的值。第三列表示挂载点的类型为 `nfs`。

最后一列包含用逗号分隔的 NFS 选项列表。我们示例中的选项在上一节“使用 mount 连接到 NFS 共享”中已过过。

将条目添加到 `/etc/fstab` 后，使用 `root` 身份运行命令 `mount /mountpoint` 来挂载共享，除非。除非指定了 `noauto` 选项，否则会在启动时自动挂载。

> 提示
> 该选项也可用于允许非 `root` 用户通过 `mount /mountpoint` 命令挂载共享。如果使用了 `noauto` 选项以便在启动时不挂载共享，则这将非常有用。

## 使用 autofs 连接到 NFS 共享

最后一种方法是使用 `autofs`。`autofs` 通过使用 `automount` 守护进程监控预配置的 NFS 挂载点。只有当用户尝试访问本地挂载目录时，它们才会挂载。

使用 `autofs` 而不是在 `/etc/fstab` 中配置共享有几个优点。因为共享只有在访问时才被挂载，所以系统启动速度更快。系统不需要等待每个 NFS 服务器响应并成功。其次，它更安全。在客户端系统中，用户在进入该目录之前必须知道配置挂载共享的目录。另一方面，如果所有共享在启动时都挂载，只要有权限，你就可以浏览共享目录的内容。如果系统被未经授权的用户入侵，这将使得入侵者更容易找到共享文件。最后，如果客户端配置为使用 NIS 进行身份验证，则也可以配置 NIS 来为 `autofs` 提供必要的 `/etc/auto.*` 文件。因此，当需要添加、修改或删除共享时，管理员需要更新 NIS 服务器上的配置文件，在客户端重启 NIS 服务后，这些文件将同步到所有客户端。更新对于终端用户来说几乎是无缝的。

主配置文件是 `/etc/auto.master`。列表 13.2 显示了默认的 `auto.master` 文件。

### 列表 13.2 默认 auto.master 文件

```
#
# $Id: auto.master,v 1.4 2005/01/04 14:36:54 raven Exp $
#
# 主文件
# 这是一个自动挂载映射，它具有以下格式
# key [ -mount-options-separated-by-comma ] location
# 有关格式的详情，请查看 autofs(5).
#
/misc    /etc/auto.misc
/net    -hosts
#
# 如果可以找到，则包含中央主映射
# nswitch sources.
#
# 注意，在包含的主映射中有 /net 或 /misc（如
# 上所示）的条目，任何相同的键将不会被看到，因为第一个读取的键具有
# 优先级。
#
+auto.master
```

你可以看到，`/misc/` 目录的挂载定义在不同的文件中。每个目录一个配置文件。红帽企业 Linux 中的 `/misc/` 目录由 `autofs` 控制。由于 `/etc/auto.misc` 已经创建， NFS 挂载格式如下：

```
mountdir <options> server.example.com:exporteddir
```

将 `mountdir` 替换为想要挂载的 `/misc/` 子目录。例如，使用目录 `/misc/data/`，将 `mountdir` 替换为 `data`。当服务器共享时，它是动态创建的。不要在本地文件系统上创建它。将 `<options>` 替换在本章讨论过的逗号分隔的 NFS 选项列表。在 NFS 页面中查找。同时也替换服务器名称和导出目录。

如果目录由 `autofs` 作为挂载点使用，则不应写入远程文件系统。它是 `autofs` 的预留目录。要启动自动挂载守护进程，使用命令 `service autofs start`。停止它，使用命令 `service autofs stop`。如果 `auto.master` 文件或任何如 `auto.misc` 文件已修改，使用命令 `service autofs reload` 强制重新加载配置。要配置系统在启动时启动它，执行 `chkconfig autofs` 作为 `root` 用户。
