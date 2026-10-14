
## NIS — 网络信息服务

一旦网络中的多个 UNIX 系统想要访问公共资源，就必须确保例如所有用户和组标识对该网络中的所有机器都相同。网络对用户应该是透明的：无论用户使用哪台机器，他始终会在完全相同的环境中找到自己。这是通过 NIS 和 NFS 服务实现的。NFS 将文件系统分布在网络上，并在第 365 页的章节 NFS — 共享文件系统 中讨论。

NIS（Network Information Service）是一种数据库服务，可在网络上实现对 `/etc/passwd`、`/etc/shadow` 和 `/etc/group` 的访问。NIS 可用于其他更专业的任务（例如 `/etc/hosts` 或 `/etc/services`）。

> **Note**
>
> 在 YaST2 中配置 NIS 最为简便。详细的配置说明可在 *Basic* 手册的 YaST2 章节中找到。如果您仍想自定义配置 NIS，可以在下面找到必要的信息。

### Manual Installation of an NIS Client

SuSE Linux 包含安装 NIS 客户端所需的所有软件包。操作如下：

- 在文件 `/etc/defaultdomain` 中设置 NIS 域。NIS 域名不应与 DNS 域名混淆。两者互不相关。
- NIS 服务器通过 `/etc/yp.conf` 设置：
```
ypserver 192.168.0.1
```
- NIS 使用 RPC（远程过程调用）。因此，RPC 端口映射器需要运行。该服务器由 `/etc/init.d/portmap` 启动。
- 完成 `/etc/passwd` 和 `/etc/group` 中的条目。为使请求在本地文件搜索后发送到 NIS 服务器，需要在相关文件中添加以 '+' 开头的行。

¹ NIS 通常被称为 YP。这源自“yellow pages”，即网络上的“黄页”。

- NIS 允许您在文件 `/etc/sysconfig/ypbind` 中设置多种其他选项。
- 激活 NIS 服务器的最后一步是启动 `ypbind`。这实际上启动了 NIS 客户端。
- 要激活更改，请重新启动系统或输入：
```
earth:  # rcnetwork restart
earth:  # rcypbind restart
```

## NIS Master and Slave Server

一个 NIS 服务器需要软件包 ypserver、ypserv 以及正在运行的 portmap。如果您的端口映射器内置了 tcp-wrapper，请确保 `/etc/hosts.allow` 和 `/etc/hosts.deny` 设置正确。NIS 主要用于 `/etc/passwd`、`/etc/shadow` 和 `/etc/group`，但 `/etc/hosts` 和 `/etc/services` 也可通过网络共享。客户端和服务器机器需要一个共同的域名。它不一定是 DNS 域名。您可以选择任意名称。将名称写入文件 `/etc/defaultdomain`。

## NFS — Shared File Systems

如第 363 页的章节 *NIS — Network Information Service* 所述，NFS（与 NIS 结合使用）使网络对用户透明。通过 NFS，可以将文件系统分布在网络上。用户登录到哪个终端并不重要。他始终会在相同的环境中找到自己。

与 NIS 一样，NFS 是一种不对称服务。存在 NFS 服务器和 NFS 客户端。一台机器可以同时兼任两者——它可以提供文件系统供网络使用（导出）并挂载来自其他主机的文件系统（导入）。通常，这些是具有非常大硬盘容量的服务器，其文件系统由其他客户端挂载。

### Importing File Systems

要从 NFS 服务器导入文件系统，唯一的要求是 RPC 端口映射器已在运行。与 NIS 相关的启动该服务器已在第 363 页的章节 *Manual Installation of an NIS Client* 中介绍。如果是这种情况，其他文件系统（只要由服务器导出）就可以像本地文件系统一样轻松地使用 mount 程序挂载，语法如下：

```
mount -t nfs {host}:{remote path} {local path}
```

例如，如果要导入机器 sun 的用户目录，可以使用以下命令：

```
earth:/ # mount -t nfs sun:/home /home
```

### Exporting File Systems

导出文件系统的机器称为 NFS 服务器。在 NFS 服务器上，有几个需要启动的工具：

- RPC portmapper (*rpc.portmap*)
- RPC mount daemon (*rpc.mountd*)
- RPC NFS daemon (*rpc.nfsd*)

这些由脚本 /etc/init.d/portmap 和 /etc/init.d/nfsserver 在启动时启动。启动 RPC 端口映射器已在第 363 页的章节 *Manual Installation of an NIS Client* 中描述。在这些守护进程启动后，配置文件 /etc/exports 决定应将哪些目录导出到哪些机器。

对于每个要导出的目录，需要一行来指定哪些机器可以用什么权限访问该目录。该目录下的所有子目录也将自动导出。通常，所有授权机器都用其全名（包括域名）表示，但也可以使用通配符如 ‘*’ 或 ‘?’。如果此处未指定机器，则任何机器都可以用给定权限导入此文件系统。

要导出文件系统的权限用机器名后的括号表示。最重要的选项有：

| Option | Description |
|---|---|
| `ro` | 文件系统以只读权限导出（默认）。 |
| `rw` | 文件系统以读写权限导出。 |
| `root_squash` | 这确保给定机器的 root 用户在此文件系统上没有 root 特定权限。这是通过将用户 ID 0（root）的用户分配用户 ID 65534 实现的。该用户 ID 应设为 nobody。 |
| `no_root_squash` | 不将用户 ID 0 分配给用户 ID 65534（默认）。 |
| `link_relative` | 将绝对链接（以 `/` 开头）转换为 `../` 的序列。这仅在整台机器的文件系统被挂载时才有用（默认）。 |
| `link_absolute` | 符号链接保持不变。 |
| `map_identity` | 客户端和服务器上的用户 ID 完全相同（默认）。 |
| `map-daemon` | 客户端和服务器没有匹配的用户 ID。这告诉 nfsd 为用户 ID 创建转换表。`ugidd` 需要此功能才能工作。 |

Table 13.13: Permissions for Exported File Systems

您的 exports 文件可能如下所示 File 56。

```
# /etc/exports
#
/home          sun(rw)    venus(rw)
/usr/X11       sun(ro)    venus(ro)
/usr/lib/texmf sun(rw)    venus(rw)
/              earth(ro,root_squash)
/home/ftp      (ro)
# End of exports
```

### File 56: /etc/exports

文件 /etc/exports 由 mountd 读取。如果您更改此文件中的任何内容，请重新启动 mountd 和 nfsd 以使更改生效。这可以用 `rcnfsserver restart` 轻松完成。

## DHCP

### The DHCP Protocol

“动态主机配置协议”的目的是从服务器集中分配网络设置，而不是在每台工作站上本地配置。配置为使用 DHCP 的客户端无法控制自己的静态地址。它能够根据服务器的指示完全自动配置自身。

使用 DHCP 的一种方式是使用网络卡的硬件地址（在大多数情况下是固定的）来识别每个客户端，然后每次客户端连接到服务器时为其提供相同的设置。DHCP 也可以配置为服务器从为此目的设置的地址池中动态地为每个“感兴趣”的主机分配地址。在后一种情况下，DHCP 服务器会尝试每次收到来自客户端的请求时都分配相同的地址（即使在较长的时间段内）。当然，如果网络中的客户端主机数量超过可用网络地址数量，这将无法工作。

凭借这些可能性，DHCP 可以在两个方面让系统管理员的生活更轻松。任何与地址和网络配置总体相关的更改（甚至更大的更改）都可以通过编辑服务器的配置文件集中实现。这比重新配置大量客户端机器更方便。此外，将机器（特别是新机器）集成到网络中也变得更加容易，因为它们可以从池中获得 IP 地址。从 DHCP 服务器检索适当的网络设置对于经常在不同网络中使用的笔记本电脑尤其有用。

DHCP 服务器不仅提供 IP 地址和网络掩码，还提供客户端要使用的主机名、域名、网关和名称服务器地址。此外，DHCP 允许以集中方式配置许多其他参数，例如客户端可以从中轮询当前时间的时服务器，甚至是打印服务器。

以下小节概述了 DHCP，而不详细描述该服务。特别是，我们想展示如何在自己的网络中使用 DHCP 服务器 dhcpd，以便从一个中心点轻松管理其整个设置。
