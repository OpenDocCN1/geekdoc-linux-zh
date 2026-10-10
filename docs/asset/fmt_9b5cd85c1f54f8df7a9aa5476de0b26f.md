
AIX 同时支持 NFS 版本 3 和 NFS 版本 2。支持这两个版本的 NFS 使 AIX 能够与 NFS 版本 2 的客户端和服务器保持向后兼容。除了支持 UDP 作为传输层外，AIX 4.2.1 及更高版本还支持 TCP。事实上，自 AIX 4.3 以来，TCP 就是默认的传输协议。你可以使用 `mount` 命令的 `vers` 和 `proto` 选项来指定使用哪个版本的 NFS 或哪个传输协议。本章稍后将会详细讨论这一点。

### 配置 NFS

AIX 提供 NFS 服务器和 NFS 客户端软件包。这些软件包会自动安装在系统中，但必须采取措施启动守护进程。你可以使用以下任一方法启动 NFS 守护进程：

- `wsm` 命令（基于 Web 的系统管理器，WebSM）

- SMIT 快速路径 `smit mknfs`

- `mknfs` 命令

这些方法中的任何一种都会在 `/etc/inittab` 文件中放置一个条目，以执行 `/etc/rc.nfs` 脚本启动 NFS 守护进程。

```
rcnfss::23456789:wait::/etc/rc.nfs > /dev/console 2>&1 # Start NFS Daemon
```

`/etc/rc.nfs` 脚本首先启动 NFS 块 I/O `biord` 守护进程。如果存在 `/etc/exports` 文件，则在启动 `nfsd` 和 `rpc.mountd` 守护进程之前，使用 `exports -a` 导出该文件。`/etc/rc.nfs` 脚本最后启动 `rpc.statd` 和 `rpc.lockd` 守护进程。`/etc/rc.nfs` 脚本还包含启动 NIS 和 HANFS 子系统及子服务器的条目。

可以通过在 `/etc/vfs` 中定义 `defaultvfs` 将 NFS 设置为默认的远程文件系统类型。取消注释 `/etc/vfs` 表格中的以下行。

```
## defaultvfs jfs nfs
# nfs 2 /etc/helpers/nfsmnthelp none remote
```

NFS 还可以由 AIX `srcmstr` 作为子系统进行管理。因此，可以使用 `startsrc` 和 `stopsrc` 命令将 NFS 守护进程作为一组启动或停止。NFS 操作也可以通过 SMIT 快速路径 `smit nfs` 子菜单进行管理，并且像 `mkfsexp` 这样的 NFS 配置脚本将立即以及在系统启动时启动所有必要的子系统。

```
# lssrc -g nfs
# startsrc -g nfs
# stopsrc -g nfs
```

列出 NFS 子系统中的守护进程

启动 NFS 子系统

停止 NFS 子系统

### NFS 服务器

NFS 服务器被设计为无状态系统。这应该能够消除在服务器或客户端故障时需要支持恢复操作的需求。事实证明，这并不完全属实。NFS 使用 UDP 作为传输，我们都知道 UDP 不保证数据包传输或数据包顺序。为了克服 UDP 的缺陷，NFS 服务器必须维护最近的 RPC 握手状态的易失性缓存，以避免重复、乱序或丢失的 I/O 操作数据包。这也意味着服务器必须跟踪它正在与谁通信。为了使 `nfsd` 守护进程保持无状态，使用了额外的守护进程来跟踪机器连接、RPC 状态和文件锁。IBM 的高可用性网络文件系统（HANFS）利用易失性缓存状态和锁守护进程信息来支持备份 NFS 服务器。

为了确保文件完整性，NFS 服务器使用直通缓存，强制文件更新立即写入磁盘。为了性能，维护了数据完整性。在某些体系结构中，当数据完整性不是问题时，可以使用异步写入支持来提高读取性能。

### NFS 服务器守护进程

NFS 服务器依赖多个守护进程来管理分布式文件系统服务。来自多个客户端的 I/O 请求通过 `nfsd` 的多个线程进行多路复用。`nfsd` 守护进程管理文件 I/O 操作。`nfsd` 线程的数量是自调节的，并根据客户端对服务器的请求创建。

`rpc.mountd` 守护进程由服务器用于管理和跟踪客户端挂载请求。客户端和服务器之间的最近 RPC 操作由 `rpc.statd` 守护进程缓存。服务器通过 `rpc.lockd` 守护进程支持 Sysv 建议文件记录和记录锁定。

NFS 服务器守护进程如表 14-1 所示。由于 NFS 基于 RPC，NFS 服务器守护进程必须向 `portmap` 守护进程注册自己。`portmap` 守护进程维护特定机器上可用的 RPC 应用程序集合。每个应用程序表示为应用程序名称、版本和端口号的元组。服务器将其应用程序数据注册到 `portmap` 守护进程。客户端应用程序查询 `portmap` 守护进程以了解与已知的服务器应用程序名称和版本关联的端口号。`portmap` 监听列在 `/etc/services` 中的知名端口号，从而避免了确定 `portmap` 端口号是什么的“先有鸡还是先有蛋”问题。

| 守护进程 | 用途 |
| :--- | :--- |
| `nfsd` | NFS 服务器守护进程 |
| `portmap` | RPC 程序到端口管理器 |
| `rpc.mountd` | NFS 挂载管理器 |
| `rpc.statd` | RPC 状态管理器 |
| `rpc.lockd` | NFS 锁管理器 |
| `rpc.pcnfsd` | PC 认证服务 |

表 14-1. NFS 服务器守护进程

`nfsd`、`rpc.lockd`、`rpc.mountd` 和 `rpc.statd` NFS 服务器守护进程在 `/etc/rc.nfs` 脚本中启动，而其他 NFS 服务器守护进程由 `inetd` 超级守护进程控制。

### 导出服务器文件系统

可用于远程挂载的每个文件系统或目录都由服务器 `/etc/exports` 文件中的条目标识。除了目录路径名称外，`/etc/exports` 条目还控制允许哪些机器名称拥有 root 权限和写入访问权限。如果未为远程 NFS 客户端启用 NFS root 访问权限，则服务器的 root UID 将映射为默认 UID -2 (4294967294)，用户名为 `nobody`。这限制了远程机器上超级用户 UID 的访问权限。

`/etc/exports` 文件是一个平面 ASCII 文本文件，可以使用你喜欢的编辑器手动编辑，或者使用 SMIT 快速路径 `smit mknfsexp` 进行维护（见图 14-1）。

![](img/82f851021955589d82b22750fb3b1646_329_0.png)

图 14-1. 向导出列表添加目录的 SMIT 面板

对 `/etc/exports` 文件的手动更新必须通过调用 `/usr/sbin/exportfs` 命令让服务器守护进程知晓。

以下是 `/etc/exports` 的一个示例：

```
/var/spool/lpd/pio/@local -ro
/scripts -root=bambam:dino:wilma,access=bambam:dino:wilma
```

```
# /usr/sbin/exportfs -a <————— 导出 /etc/exports 文件中的所有条目
```

### PC-NFS

PC-NFS 是一个用于 PC 挂载由 NFS 服务器导出的文件系统并向 NFS 服务器请求网络地址和主机名的程序。如果 `rpc.pcnfsd` 守护进程在 NFS 服务器上运行，PC 还可以访问认证和打印 spooling 服务。

要启动 `rpc.pcnfsd` 守护进程，请取消注释 `/etc/inetd.conf` 文件中的以下行：

```
pcnfsd sunrpc_udp udp wait root /usr/sbin/rpc.pcnfsd pcnfs 150001 1-2
```

### NFS 客户端

为了提高性能，NFS 客户端实现了客户端数据缓存。这要求多个 NFS 客户端和服务器之间维持一定级别的缓存一致性。使用时间戳过期机制，允许客户端在缓存信息变得陈旧时更新缓存信息。

每个客户端运行多线程 NFS `biOd` 块 I/O 守护进程。创建的线程数量取决于工作负载。NFS 客户端还运行 `portmap` 守护进程。通过查询 `portmap` 守护进程来识别 RPC 服务并将端口连接到 NFS 服务器。

NFS RPC 机制允许在服务器故障时阻止客户端应用程序。当恢复对服务器的访问时，I/O 操作继续。提供了重试限制，以便在长期服务器故障的情况下，客户端应用程序不会永远等待。Sun 还添加了 `hard` 和 `soft` 挂载选项，以便在服务器访问被阻塞时中断客户端。只需要两个 NFS 客户端守护进程：

```
biOd <————— NFS 块 I/O 守护进程
portmap <————— RPC 程序到端口管理器
```

### 导入文件系统

导入（`mount`）网络文件系统有三种不同方式：预定义、显式和自动。

## 预定义挂载

预定义挂载是指将 NFS 文件系统定义配置为 `/etc/filesystems` 文件中的段（stanza）。该段类似于本地文件系统定义，并额外列出了 `nodename` = 参数中的远程主机名。`dev` = 参数定义了要在远程机器上挂载的目录路径。您可以使用 `options` = 参数指定挂载选项。例如，除其他选项外，若要为该挂载条目指定使用 NFS 版本 3 和传输协议 UDP，请在 `options` 属性的参数列表末尾添加 `vers`=3、`proto`=udp。如果您未指定版本或协议，`mount` 命令将首先尝试使用 TCP 的 3 版本，然后是使用 UDP 的 3 版本，接着是使用 TCP 的 2 版本，最后尝试使用 UDP 的 2 版本。`/etc/filesystems` 条目可以直接编辑，也可以使用 SMIT FastPath `smit mnkfmnt` 进行管理（参见图 14-2）。默认情况下，`mount` 命令会尝试挂载以下条目：

```
# smit mnkfsmnt
```

![](img/82f851021955589d82b22750fb3b1646_331_0.png)

以下是一个 `/etc/filesystems` NFS 段（stanza）的示例：

```
/usr/local/common:
    dev    = "/usr/local/common"
    vfs    = nfs
    nodename = yogi
    mount  = false
    type   = nfsfile
    options = bg,hard,intr
    account = false

/usr/sys/instd.images:
    dev    = "/usr/sys/instd.images"
    vfs    = nfs
    nodename = bambam
    mount  = false
    type   = nfsfile
    options = bg,hard,intr
    account = false

/usr/share/man:
    dev    = "/usr/share/man"
    vfs    = nfs
    nodename = dino
    mount  = false
    type   = nfsfile
    options = bg,hard,intr
    account = false

/sapmnt/help:
    dev    = "/sapmnt/help"
    vfs    = nfs
    nodename = sapprod1
    mount  = false
    type   = nfsfile
    options = ro,bg,hard,intr
    account = false
```

可以在段定义中添加 `type = nfsfile` 参数，以将 NFS 文件系统识别为 `nfsfile` 组。这样，可以使用 `mount` 和 `umount` 命令的 `-t` 选项将它们作为一组进行挂载或取消挂载。

```
# mount -t nfsfile
# umount -t nfsfile
```

## 显式挂载

显式挂载用于短期挂载文件或目录，且无需在系统重启后保持持久化。对于此类挂载，请在命令行上使用带有所有所需挂载选项的 `mount` 命令。例如，若要使用后台模式、NFS 版本 3、传输协议 `tcp` 以及最多重试三次的挂载选项，将主机 `lobo` 上的 `/tmp/STUFF` 挂载到 `/tmp/lobo`，请发出以下命令行：

```
# mount -n lobo -o "bg,vers=3,proto=tcp,retry=3" /tmp/STUFF /tmp/lobo
```

另一种选择是使用以下命令调用 NFS 挂载默认值：

```
# mount lobo:/tmp/STUFF /tmp/lobo
```

## 自动挂载

`AutoFS` 控制自动挂载。在程序或用户尝试访问挂载点之前，自动挂载没有显式挂载。关于 `AutoFS` 的详细信息请参阅本章稍后的内容。

## CacheFS

缓存文件系统（Cache File System）允许在 NFS 客户端系统上为 NFS 文件系统提供缓存，以提高慢速网络上客户端的性能。文件在首次访问时会被存储在缓存中。随后的请求可以在 `CacheFS` 本地访问，而无需通过网络。`CacheFS` 会定期检查缓存中文件的修改时间与之前修改时间的比较。如果修改时间不同，缓存中的文件数据将被刷新，并从文件系统检索更新的数据。

使用 SMIT FastPath `smit cachefs` 进行 `CacheFS` 的管理和挂载。

## AutoFS

`AutoFS` 包括一个内核扩展、`automountd` 守护进程以及 `automount` 命令。当程序或用户访问 NFS 文件系统时，`AutoFS` 会将其挂载。`automount` 命令用于将 `AutoFS` 映射（map）文件加载到 `AutoFS` 内核扩展中，该文件包含本地目录到服务器目录的映射信息。当用户访问映射文件中列出的本地目录时，内核扩展会向 `automountd` 守护进程发送挂载请求，以挂载该目录（如果当前未挂载）。如果在适当的时间间隔内（默认五分钟）未访问该文件系统，`automount` 守护进程将卸载该文件系统。

可以使用 AIX 的 `sremfs` 命令 `starttrsc` 和 `stoptrsc` 来管理 `automountd` 守护进程。

```
# starttrsc -G autofs  # 启动 AutoFS 子系统
# stoptrsc -g autofs   # 停止 AutoFS 子系统
```

## 网络信息服务：NIS 和 NIS+

Sun 开发了命名服务，最初将其称为黄页（Yellow Pages，YP）。由于 YP 是英国电信的注册商标，Sun 被迫将该服务重命名为网络信息服务。顾名思义，网络信息服务（NIS）旨在集中管理网络中系统和用户的信息，以简化系统管理。

NIS 采用客户端/服务器模型实现。其组件包括服务器、客户端、映射（maps）以及一组管理工具。NIS 的设计假设是针对小型网络，其中大部分配置数据是静态的；网络信息由系统管理员管理。在当今的计算环境中，出现了去中心化管理和适应组织层级结构的需求。NIS+ 的开发旨在解决这些问题以及 NIS 中的安全问题。请注意，NIS+ 是 NIS 的替代方案。在类似概念中存在许多术语差异，并且 NIS+ 还具有许多新功能。

以下各节概述了 NIS 和 NIS+ 的组件及其配置方法。

### NIS

NIS 使用域（domains）来组织系统，这些域通过 NIS 服务共享一组配置数据。一个 NIS 域由一个主服务器、零个或多个从服务器以及一组客户端机器组成。您需要为每个相应的 NIS 应用程序安装 `bos.net.nisserver` 或 `bos.net.nis.client` 文件集。以下 NIS 讨论中的所有 SMIT FastPath 面板都可以通过主 NIS 配置 SMIT FastPath `smit yp` 访问。

一个 NIS 域中有一个主服务器，其中维护着主要的映射。从服务器从主服务器获取 NIS 映射的副本。从服务器可以像主服务器一样响应客户端请求，从而提高信息的可用性。如果主服务器正在运行 `ypupdated` 守护进程，或者主服务器停止并重新启动，或者在主服务器上调用了 `yppush` 命令，从服务器可以自动获取更新的映射。主服务器和从服务器都运行 `ypserv` 守护进程以处理客户端对映射中包含信息的请求。主服务器还运行 `ypasswd` 守护进程来处理用户的密码更改请求。

NIS 客户端构成了 NIS 名称空间中大多数主机。一个 NIS 客户端运行 `ypbind` 守护进程以定位最近的 NIS 服务器，并查询服务器以获取 IP 地址或用户数据等信息。

### NIS 域

域定义了可供服务器使用的管理控制区域。属于某个域的系统共享一组常见的配置和网络信息，例如用户、组、主机名和 IP 地址。必须在域中的所有系统上设置域名。使用以下 `chypdom` 命令在此时及下次重启时定义域名：

```
# chypdom -B <DomainName>
```

若要显示 NIS 域名，请使用不带参数的 `domainname` 命令。

```
# domainname
```

### NIS 映射
