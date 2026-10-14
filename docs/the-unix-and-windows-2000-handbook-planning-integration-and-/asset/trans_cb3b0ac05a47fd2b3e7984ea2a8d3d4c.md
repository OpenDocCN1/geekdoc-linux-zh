

3. 输入共享名称并从“网络资源”部分选择要挂载的机器和 NFS 文件系统。网络资源也可以使用通用命名约定手动输入。最后一步是在本地机器上创建一个共享，以便 SMB 客户端可以通过 Windows 2000 网关上的 SMB 共享访问此 NFS 目录。

> NFS 网关服务应为 NFS 活动最少的客户端机器进行配置。

## 配置 NFS 客户端

为 NFS 配置客户端是 NFS 配置服务中最简单的一项。

- 1. 在窗口左侧点击“Client for NFS”以访问配置页面。第一个页面是身份验证页面（图 8.8）。

![](img/415c89a1ede71e11e5040a0038b6916c_347_0.png)

图 8.8 Services for UNIX NFS 客户端。

- 2. 点击“Use Simple Mapping”然后输入你的 NIS 域信息或你的 PCNFSD 服务器。这将映射 Windows 域与指定 UNIX NIS 域之间相同的登录名。如果你的 Windows 和 UNIX 登录名不同，你需要点击“Use Advanced Mapping”。
- 3. “File Settings”选项卡允许你为新创建的文件或文件夹设置读、写和执行权限。
- 4. “Performance”选项卡包含缓冲区大小、超时、重试次数和挂载类型的参数。除非出现问题，否则请使用性能页面的默认值。

> 不要忘记通过点击每个配置页面右上角的磁盘图标来保存你的设置。

现在你已准备好挂载 NFS 文件系统。挂载 NFS 文件系统在 Windows 资源管理器中完成，操作与 Windows 2000 共享相同。你也可以通过命令行使用 mount 命令挂载 NFS 文件系统。mount 命令位于 Services for UNIX 目录下的 common 文件夹中。mount 命令使用以下开关/参数调用：

```
mount [switches] [network path] [drive] where
switches /u: username /o options Table8mount Valid only for that filesystem
network path = server://full/path/name or \\server\full\path\name
drive = drive: `
```

不带任何开关或参数调用的 mount 命令会显示本地机器上当前已挂载的所有 NFS 文件系统。具体选项列在表 8.8 中。

| Table 8.8 Specific Options of the mount Command |
| Option | Definition |
| Rsize=n | Read buffer size in bytes. |
| Wsize=n | Write buffer size in bytes. |
| Timeo=n | NFS timeout in tenths of a second. |
| Retrans=n | NFS retransmissions; default is 5. |
| Soft | hard | Soft or hard mount. |

要断开 NFS 文件系统连接，请在 Windows 资源管理器中右键单击该文件系统并选择 **Disconnect**。

## HUMMINGBIRD’S NFS MAESTRO SUITE FOR WINDOWS 2000

Hummingbird Communications 的 NFS Maestro 产品系列为 NFS 连接提供了额外的软件包。Hummingbird 的 NFS Maestro 产品是原生的 Microsoft 32 位 TCP/IP 实现。Maestro Server 安装为 Windows 2000 服务，并提供长文件名支持，最长可达 255 个字符。它支持 NFS 版本 2/3、WebNFS 和通过 TCP 的 NFS。Hummingbird 包含一个实用程序，用于将 UNIX 用户 ID（UID）/组 ID（GID）映射到 Windows 2000 用户和组。Maestro Suite 分为四个产品：

- **NFS Maestro Client**，使 PC 桌面能够访问本地和远程 NFS 文件系统和打印机。
- **NFS Maestro Solo**，为用户提供 NFS Maestro Client 的核心 NFS 功能，同时利用现有且功能强大的多线程 32 位操作系统。
- **NFS Maestro Server**，使 UNIX 工作站和网络连接的 NAS 计算机能够通过网络访问基于 Windows 的资源，例如 Windows NT 文件系统、目录、打印机和 CD-ROM。
- **NFS Maestro Gateway**，在为网络管理员提供集中管理的同时，提供对 UNIX 文件系统的受控、偶尔的 NFS 访问。

## SMB: A Client/Server Protocol

SMB 是 Windows 2000 主要用于网络连接文件、打印机和资源的协议。SMB 协议设计为运行在 TCP/IP（通常称为 NetBIOS over TCP/IP）、NetBEUI 和 IPX/SPX 之上。这种多功能性使 SMB 几乎可以在任何网络环境中部署。

多年来，基础 SMB 协议出现了多个变体，其中最著名的是 Windows NT 4.0 和 Windows 2000 中使用的 NTLM 协议。SMB 协议的最新变体是 CIFS，即通用 Internet 文件系统。CIFS 基本上是 NTLM 加上一些用于优化 Internet 性能的额外功能。

