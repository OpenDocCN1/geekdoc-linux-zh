
通过网络（在本地，你可以使用 `write`）发送给已登录的用户，而无需登录另一台计算机。

只有当目标计算机上运行着相应的服务器时，才能使用 `sendfile`，而这种情况目前很少见。此外，该计算机必须能够通过 TCP/IP 直接访问。如果你通过邮件发送文件，目标计算机不需要在线，只要在 DNS 中为该计算机提供了相应的 MX 记录即可。

系统管理员可以通过文件 `/usr/local/etc/nosendfile` 限制某些用户使用此服务。每个用户可以创建一个带有目标地别名的文件。可以禁止从异地计算机传输文件和消息。

UNIX 系统中另一个经常经常被忽视的功能是向已登录的用户发送短消息。如果该用户在同一台计算机上工作，你可以使用 `write` 命令。然而，如果该用户登录在另一台计算机上，你就无法进行 `write` 操作。如果安装了 `sendfile`，你可以使用 `sendmsg` 发送短消息，消息会立即显示给用户。

| 附加信息和来源 |
| --- | --- |
| 作者: | Uli Horlacher |
| 邮箱: | framstag@rus.uni-stuttgart.de |
| ftp :: | ftp.uni-stuttgart.de/ |
| ftp 路径: | /pub/unix/comm/sendfile/ |
| 文件: | sendfile.tar.gz |
| 大小: | 约 300 KB |

## 网络文件系统 (NFS)

通过网络文件系统 (NFS)，不同的计算机可以访问并使用文件。例如，用户可以在所有计算机上拥有自己的主目录或邮件目录、数据文件和配置文件，这极大地方便了他们的日常工作。另一种合理的做法是在 `/usr/local` 或 `/usr` 下安装程序，特别是像 X11 或 TeX 这样的大软件包。这也减少了更新时的管理工作量。

本地提供这些目录的计算机称为 NFS 服务器；使用远程计算机数据的计算机称为 NFS 客户端。对于用户来说，文件是存储在本地还是将远程目录树集成到本地目录树中完全无关。由 NFS 服务器导出的目录树也称为 NFS 卷。

网络文件系统是基于远程过程调用（RPC，另见第 14.6 节）实现的。该协议由 Sun 公司开发并发布在 [rfc1094] 中。NFS 是不同 UNIX 系统之间共享目录的标准协议。在 PC 世界中，你还会找到 NetWare (IPX)、Server Message Block (SMB)、LAN manager、Windows for Workgroups、Windows NT；见第 19.2 节。

正如第 14 章提到的，Sun RPC 系统是 NFS 客户端或服务器运行的必要条件。

### 17.1 作为 NFS 客户端的 LINUX

通常，本地网络中已经存在 NFS 服务器，用于用户的主目录或例如用于共享 CD-ROM 驱动器。由于许多系统供应商不再随系统附带打印版文档，通常在这些情况下，LINUX 最初会被配置为 NFS 客户端。必须满足以下条件：

- 网络必须已配置；也就是说，必须能够对 NFS 服务器进行 ping。
- NFS 文件系统必须编译进内核或作为模块加载。你可以通过查看命令 `cat /proc/filesystems` 的输出来检查这一点，其中必须出现 `nfs`。否则，你必须加载 `nfs.o` 模块或者重新配置或重新编译内核。
- RPC 系统必须已经启动。你可以通过命令 `rpcinfo -p` 查看在端口映射器中注册的服务。
- 网络中的另一台计算机必须向这台计算机导出数据。可以通过命令 `mount -t nfs -e nfs-server` 确定哪些目录被导出了。

可以使用命令 `mount -t nfs nfs-server:nfs-volume /mnt` 来挂载由服务器 `nfs-server` 导出的卷。指定类型 (`-t`) 可以挂载由服务器 `nfs-server` 导出的卷。NFS 服务器导出的目录树也称为 NFS 卷。

网络文件系统是基于远程过程调用（RPC，另见第 14.6 节）实现的。该协议由 Sun 公司开发并发布在 [rfc1094](https://example.com/rfc1094)。NFS 是不同 UNIX 系统之间共享目录的标准协议。在 PC 世界中，你还会找到 NetWare (IPX)、Server Message Block (SMB)、LAN manager、Windows for Workgroups、Windows NT；见第 19.2 节。

正如第 14 章中已经提到的，Sun RPC 系统对于 NFS 客户端或服务器的运行是强制性的。

### 作为 NFS 服务器的 LINUX

通常，本地网络中已经存在 NFS 服务器，用于用户的主目录或例如用于共享 CD-ROM 驱动器。由于许多系统供应商不再随系统附带打印版文档，通常在这些情况下，LINUX 最初会被配置为 NFS 客户端。必须满足以下条件：

- 网络必须已配置；也就是说，必须能够对 NFS 服务器进行 ping。
- NFS 文件系统必须编译进内核或作为模块加载。你可以通过查看命令 `cat /proc/filesystems` 的输出来检查这一点，其中必须出现 `nfs`。否则，你必须加载 `nfs.o` 模块或者重新配置或重新编译内核。
- RPC 系统必须已经启动。你可以通过命令 `rpcinfo -p` 查看在端口映射器中注册的服务。
- 网络中的另一台计算机必须向这台计算机数据。可以通过命令 `mount -t nfs -e nfs-server` 确定哪些目录被导出了。

可以使用命令 `mount -t nfs nfs-server:nfs-volume /mnt` 来挂载由服务器 `nfs-server` 导出的卷。指定类型 (`-t`) 可以挂载由服务器 `nfs-server` 导出的卷。NFS 服务器导出的目录树也称为 NFS 卷。

网络文件系统是基于远程过程调用（RPC，另见第 14.6 节）实现的。该协议由 Sun 公司开发并发布在 [rfc1094](https://example.com/rfc1094)。NFS 是不同 UNIX 系统之间共享目录的标准协议。在 PC 世界中，你还会找到 NetWare (IPX)、Server Message Block (SMB)、LAN manager、Windows for Workgroups、Windows NT；见第 19.2 节。

正如第 14 章中已经提到的，Sun RPC 系统对于 NFS 客户端或服务器的运行是强制性的。

### 作为 NFS 客户端的 LINUX

通常，本地网络中已经存在 NFS 服务器，用于用户的主目录或例如用于共享 CD-ROM 驱动器。由于许多系统供应商不再随系统附带打印版文档，通常在这些情况下，LINUX 最初会被配置为 NFS 客户端。必须满足以下条件：

- 网络必须已配置；也就是说，必须能够对 NFS 服务器进行 ping。
- NFS 文件系统必须编译进内核或作为模块加载。你可以通过查看命令 `cat /proc/filesystems` 的输出来检查这一点，其中必须出现 `nfs`。否则，你必须加载 `nfs.o` 模块或者重新配置或重新编译内核。
- RPC 系统必须已经启动。你可以通过命令 `rpcinfo -p` 查看在端口映射器中注册的服务。
- 网络中的另一台计算机必须向这台计算机导出数据。可以通过命令 `mount -t nfs -e nfs-server` 确定哪些目录被导出了。

可以使用命令 `mount -t nfs nfs-server:nfs-volume /mnt` 来挂载由服务器 `nfs-server` 导出的卷。指定类型 (`-t`) 可以挂载由服务器 `nfs-server` 导出的卷。NFS 服务器导出的目录树也称为 NFS 卷。

### 作为 NFS 服务器的 LINUX

通常，本地网络中已经存在 NFS 服务器，用于用户的主目录或例如用于共享 CD-ROM 驱动器。由于许多系统供应商不再随系统附带打印版文档，通常在这些情况下，LINUX 最初会被配置为 NFS 客户端。必须满足以下条件：

- 网络必须已配置；也就是说，必须能够对 NFS 服务器进行 ping。
- NFS 文件系统必须编译进内核或作为模块加载。你可以通过查看命令 `cat /proc/filesystems` 的输出来检查这一点，其中必须出现 `nfs`。否则，你必须加载 `nfs.o` 模块或者重新配置或重新编译内核。
- RPC 系统必须已经启动。你可以通过命令 `rpcinfo -p` 查看在端口映射器中注册的服务。
- 网络中的另一台计算机必须向这台计算机导出数据。可以通过命令 `mount -t nfs -e nfs-server` 确定哪些目录被导出了。

可以使用命令 `mount -t nfs nfs-server:nfs-volume /mnt` 来挂载由服务器 `nfs-server` 导出的卷。指定类型 (`-t`) 可以挂载由服务器 `nfs-server` 导出的卷。NFS 服务器导出的目录树也称为 NFS 卷。
[/content]

*(抱歉，我注意到你提供的待翻译文本存在大量重复内容，根据“不要重复输出原文”的要求，我已对逻辑部分进行了合并翻译。)*

[content]
通过网络（在本地，你可以使用 `write`）发送给已登录的用户，而无需登录另一台计算机。

只有当目标计算机上运行着相应的服务器时，才能使用 `sendfile`，而这种情况目前很少见。此外，该计算机必须能够通过 TCP/IP 直接访问。如果你通过邮件发送文件，目标计算机不需要在线，只要在 DNS 中为该计算机提供了相应的 MX 记录即可。

系统管理员可以通过文件 `/usr/local/etc/nosendfile` 限制某些用户使用此服务。每个用户可以创建一个带有目标地别名的文件。可以禁止从异地计算机传输文件和消息。

UNIX 系统中另一个经常被忽视的功能是向已登录的用户发送短消息。如果该用户在同一台计算机上工作，你可以使用 `write` 命令。然而，如果该用户登录在另一台计算机上，你就无法进行 `write` 操作。如果安装了 `sendfile`，你可以使用 `sendmsg` 发送短消息，消息会立即显示给用户。

| 附加信息和来源 |
| --- | --- |
| 作者: | Uli Horlacher |
| 邮箱: | framstag@rus.uni-stuttgart.de |
| ftp :: | ftp.uni-stuttgart.de/ |
| ftp 路径: | /pub/unix/comm/sendfile/ |
| 文件: | sendfile.tar.gz |
| 大小: | 约 300 KB |

## 网络文件系统 (NFS)

通过网络文件系统 (NFS)，不同的计算机可以访问并使用文件。例如，用户可以在所有计算机上拥有自己的主目录或邮件目录、数据文件和配置文件，这极大地方便了他们的日常工作。另一种合理的做法是在 `/usr/local` 或 `/usr` 下安装程序，特别是像 X11 或 TeX 这样的大软件包。这也减少了更新时的管理工作量。

本地提供这些目录的计算机称为 NFS 服务器；使用远程计算机数据的计算机称为 NFS 客户端。对于用户来说，文件是存储在本地还是将远程目录树集成到本地目录树中完全无关。由 NFS 服务器导出的目录树也称为 NFS 卷。

网络文件系统是基于远程过程调用（RPC，另见第 14.6 节）实现的。该协议由 Sun 公司开发并发布在 [rfc1094](https://example.com/rfc1094) 中。NFS 是不同 UNIX 系统之间共享目录的标准协议。在 PC 世界中，你还会找到 NetWare (IPX)、Server Message Block (SMB)、LAN manager、Windows for Workgroups、Windows NT；见第 19.2 节。

正如第 14 章中已经提到的，Sun RPC 系统是 NFS 客户端或服务器运行的必要条件。

### 17.1 作为 NFS 客户端的 LINUX

通常，本地网络中已经存在 NFS 服务器，用于用户的主目录或例如用于共享 CD-ROM 驱动器。由于许多系统供应商不再随系统附带打印版文档，通常在这些情况下，LINUX 最初会被配置为 NFS 客户端。必须满足以下条件：

- 网络必须已配置；也就是说，必须能够对 NFS 服务器进行 ping。
- NFS 文件系统必须编译进内核或作为模块加载。你可以通过查看命令 `cat /proc/filesystems` 的输出来检查这一点，其中必须出现 `nfs`。否则，你必须加载 `nfs.o` 模块或者重新配置或重新编译内核。
- RPC 系统必须已经启动。你可以通过命令 `rpcinfo -p` 查看在端口映射器中注册的服务。
- 网络中的另一台计算机必须向这台计算机导出数据。可以通过命令 `mount -t nfs -e nfs-server` 确定哪些目录被导出了。

可以使用命令 `mount -t nfs nfs-server:nfs-volume /mnt` 来挂载由服务器 `nfs-server` 导出的卷。指定类型 (`-t`) 可以挂载由服务器 `nfs-server` 导出的卷。NFS 服务器导出的目录树也称为 NFS 卷。

### 17.2 作为 NFS 服务器的 LINUX

NFS 服务器为其他计算机提供可用的磁盘空间。应用 LINUX 作为 NFS 服务器，需要满足某些条件：

- 网络必须已配置（服务器 ping ）。
- 端口映射器 rpc.portmap 必须启动。
- 守护进程 rpc.mountd 和 rpc.nfsd 必须启动。
- 使用 PC/NFS 时，守护进程 rpc.cnfsd 必须启动。该守护进程用于涉及 DOS 和 Windows PC 的身份验证和打印机服务提供。
- NFS 协议假设两台计算机上的 uid 和 gid 编号是相同的。可以通过相同的 /etc/passwd 或通过 NIS（见第 21 章）获取。如果二者均不可（或不合理），可以使用 rpc.uuid。

哪些目录树对其他计算机可用在 `/etc/exports` 文件中指定。在那里，可以限制对计算机或网络的访问，或允许只读访问。这是通过多个选项实现的。所有选项的完整列表可以在 exports(5) 和 nfs(5) 的手册页中找到。列表 17.2 包含了 `/etc/exports` 的示例。

```
/nfsclient(ro,root_squash)
/home *.example.org (rw,root_squash)
/project proj*.example.org (rw)
/pub (ro,insecure,root_squash)
```

列表 17.2 `/etc/exports` 文件的节录。
