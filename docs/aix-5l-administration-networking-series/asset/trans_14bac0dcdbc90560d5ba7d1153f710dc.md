
## 预定义挂载

*预定义*挂载是指将 NFS 文件系统定义配置为 `/etc/filesystems` 文件中的段（stanza）。该段类似于本地文件系统定义，并额外列出了 `nodename` = 参数中的远程主机名。`dev` = 参数定义了要在远程机器上挂载的目录路径。您可以使用 `options` = 参数指定挂载选项。例如，除其他选项外，若要为该挂载条目指定使用 NFS 版本 3 和传输协议 UDP，请在 *options* 属性的参数列表末尾添加 `vers`=3、`proto`=udp。如果您未指定版本或协议，`mount` 命令将首先尝试使用 TCP 的 3 版本，然后是使用 UDP 的 3 版本，接着是使用 TCP 的 2 版本，最后尝试使用 UDP 的 2 版本。`/etc/filesystems` 条目可以直接编辑，也可以使用 SMIT FastPath *smit* mnkfmnt 进行管理（参见图 14-2）。默认情况下，`mount` 命令会尝试挂载以下条目：

```
# smit mnkfsmnt
```

![](img/82f851021955589d82b22750fb3b1646_331_0.png)

以下是一个 /etc/filesystems NFS 段（stanza）的示例：

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

可以在段定义中添加 type = nfsfile 参数，以将 NFS 文件系统识别为 nfsfile 组。这样，可以使用 mount 和 umount 命令的 -t 选项将它们作为一组进行挂载或取消挂载。

```
# mount -t nfsfile
# umount -t nfsfile
```

## 显式挂载

*显式挂载*用于短期挂载文件或目录，且无需在系统重启后保持持久化。对于此类挂载，请在命令行上使用带有所有所需挂载选项的 **mount** 命令。例如，若要使用后台模式、NFS 版本 3、传输协议 **tcp** 以及最多重试三次的挂载选项，将主机 **lobo** 上的 `/tmp/STUFF` 挂载到 `/tmp/lobo`，请发出以下命令行：

```
# mount -n lobo -o "bg,vers=3,proto=tcp,retry=3" /tmp/STUFF /tmp/lobo
```

另一种选择是使用以下命令调用 NFS 挂载默认值：

```
# mount lobo:/tmp/STUFF /tmp/lobo
```

## 自动挂载

*AutoFS* 控制*自动*挂载。在程序或用户尝试访问挂载点之前，自动挂载没有显式挂载。关于 AutoFS 的详细信息请参阅本章稍后的内容。

## CacheFS

缓存文件系统（Cache File System）允许在 NFS 客户端系统上为 NFS 文件系统提供缓存，以提高慢速网络上客户端的性能。文件在首次访问时会被存储在缓存中。随后的请求可以在 CacheFS 本地访问，而无需通过网络。CacheFS 会定期检查缓存中文件的修改时间与之前修改时间的比较。如果修改时间**不同**，缓存中的文件数据将被刷新，并从文件系统检索更新的数据。

使用 SMIT FastPath **smit cachefs** 进行 CacheFS 的管理和挂载。

## AutoFS

AutoFS 包括一个内核扩展、**automountd** 守护进程以及 **automount** 命令。当程序或用户访问 NFS 文件系统时，AutoFS 会将其挂载。**automount** 命令用于将 AutoFS *map*（映射）文件加载到 AutoFS 内核扩展中，该文件包含本地目录到服务器目录的映射信息。当用户访问映射文件中列出的本地目录时，内核扩展会向 **automountd** 守护进程发送挂载请求，以挂载该目录（如果当前未挂载）。如果在适当的时间间隔内（默认五分钟）未访问该文件系统，**automount** 守护进程将卸载该文件系统。

可以使用 AIX 的 **sremfs** 命令 **startrsc** 和 **stoptrsc** 来管理 **automountd** 守护进程。

```
# starttrsc -G autofs  # 启动 AutoFS 子系统
# stoptrsc -g autofs   # 停止 AutoFS 子系统
```

## 网络信息服务：NIS 和 NIS+

Sun 开发了命名服务，最初将其称为黄页（Yellow Pages，YP）。由于 YP 是英国电信的注册商标，Sun 被迫将该服务重命名为网络信息服务。顾名思义，网络信息服务（NIS）旨在集中管理网络中系统和用户的信息，以简化系统管理。

NIS 采用客户端/服务器模型实现。其组件包括服务器、客户端、映射（maps）以及一组管理工具。NIS 的设计假设是针对小型网络，其中大部分配置数据是静态的；网络信息由系统管理员管理。在当今的计算环境中，出现了去中心化管理和适应组织层级结构的需求。NIS+ 的开发旨在解决这些问题以及 NIS 中的安全问题。请注意，NIS+ 是 NIS 的替代方案。在类似概念中存在许多术语差异，并且 NIS+ 还具有许多新功能。

以下各节概述了 NIS 和 NIS+ 的组件及其配置方法。

### NIS

NIS 使用域（domains）来组织系统，这些域通过 NIS 服务共享一组配置数据。一个 NIS 域由一个主服务器、零个或多个从服务器以及一组客户端机器组成。您需要为每个相应的 NIS 应用程序安装 **bos.net.nisserver** 或 **bos.net.nis.client** 文件集。以下 NIS 讨论中的所有 SMIT FastPath 面板都可以通过主 NIS 配置 SMIT FastPath **smit yp** 访问。

一个 NIS 域中有一个主服务器，其中维护着主要的映射。从服务器从主服务器获取 NIS 映射的副本。从服务器可以像主服务器一样响应客户端请求，从而提高信息的可用性。如果主服务器正在运行 **ypupdated** 守护进程，或者主服务器停止并重新启动，或者在主服务器上调用了 **yppush** 命令，从服务器可以自动获取更新的映射。主服务器和从服务器都运行 **ypserv** 守护进程以处理客户端对映射中包含信息的请求。主服务器还运行 **ypasswd** 守护进程来处理用户的密码更改请求。

NIS 客户端构成了 NIS 名称空间中大多数主机。一个 NIS 客户端运行 **ypbind** 守护进程以定位最近的 NIS 服务器，并查询服务器以获取 IP 地址或用户数据等信息。

### NIS 域

域定义了可供服务器使用的管理控制区域。属于某个域的系统共享一组常见的配置和网络信息，例如用户、组、主机名和 IP 地址。必须在域中的所有系统上设置域名。使用以下 **chypdom** 命令在此时及下次重启时定义域名：

```
# chypdom -B <DomainName>
```

若要显示 NIS 域名，请使用不带参数的 **domainname** 命令。

```
# domainname
```

### NIS 映射

NIS 映射由标准文本文件构建，例如 */etc/passwd*、*/etc/group*、*/etc/hosts*，在主服务器上使用 **makedbm** 命令转换为 DBM 数据库格式。本质上，映射记录是一个键值对。NIS 提供了一个 *makefile*（制作文件），即 */var/yp/Makefile*，当调用 **make all** 时，它运行 **makedbm** 来创建默认的 NIS 映射。总体上，NIS 映射构成了 NIS 数据库。NIS 数据库可以使用 **ypxfr** 命令传输到另一个域。在使用这些方法创建或传输任何映射之前，必须在目标 NIS 服务器上创建 */var/yp/<DomainName>* 子目录。

| 文件 | 映射 | 文件 | 映射 |
| :--- | :--- | :--- | :--- |
| */etc/passwd* | passwd.byname | */etc/services* | services.byname |
| | passwd.byuid | */etc/protocols* | protocols.bynumber |
| */etc/group* | group.byname | */etc/group* | protocols.byname |
| | group.bygid | */etc/netgroup* | netgroup |
| */etc/hosts* | hosts.byaddr | */etc/hosts* | netgroup.byhost |
| | hosts.byname | | netgroup.byuser |
| */etc/ethers* | ethers.byaddr | */etc/publickey* | publickey.byname |
| | ethers.byname | */etc/bootparams* | bootparams |
| */etc/networks* | networks.byaddr | */etc/aliases* | mail.aliases |
| | networks.byname | */etc/aliases* | mail.byaddr |
| */etc/rpc* | rpc.bynumber | */etc/netmasks* | netmasks.byaddr |
| *master&slave* | ypservers | *passwd&group* | netid.byname |

**ypservers** 映射是一个特殊的映射，其中包含域中主服务器和从服务器的名称。客户端使用 **ypservers** 映射来查找最近可用的服务器。主服务器引用它以确定从服务器的名称，以提示获取 NIS 映射的更新副本。

