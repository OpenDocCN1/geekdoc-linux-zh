

## 示例：

![](img/477ccb2f05b6ba1b2d563ea74f18c197_569_0.png)

图 12-45：/etc/rpc 文件的输出。

## XDR 格式

外部数据表示（XDR）格式是二进制格式下数据的标准化表示。XDR 格式允许系统通过网络进行通信，特别是在异构网络中。它使用 C API 编程语言开发。XDR 格式定义在 rpc.h 头文件中。它主要应用于所有基于 Linux 和 UNIX 的系统。

## 端口映射器

### 定义：

端口映射器（portmapper）是一个程序，RPC 应用程序使用该程序来注册应用程序使用的端口号。该程序存储在 /sbin 目录或 /usr/sbin 目录中。端口映射器充当系统中所有正在运行的 RPC 服务器的服务代理。要访问具有给定程序编号的服务，客户端首先查询端口映射器以获取有关该服务可用端口号的信息。端口映射器接受请求，处理它，并向客户端返回该服务的 TCP 和 UDP 端口号。

当系统尝试访问端口映射器时，它会读取存储在 /etc 目录中的 hosts.allow 和 hosts.deny 文件。这些文件列出了使用 portmap 变量允许或拒绝访问的系统的 IP 地址。端口映射器控制一组守护进程，如 nfsd、mountd、ypbind/ypserv、rquotad、lockd、statd、riptime 和 users。

> 在 Linux 中，端口映射器被称为 portmap 或 rpc.portmap。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_570_0.png)

*图 12-46：端口映射器程序的工作原理。*

## portmap 守护进程

**定义：**

*portmap* 服务是一个守护进程，动态为 RPC 分配端口，用于客户端和服务器之间的通信。它将服务名映射到服务正在运行的端口号。它维护一个包含端口列表以及每个端口上可访问的服务的端口映射器。portmap 程序存储在 /sbin 目录中。只有超级用户才能启动 portmap 服务。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_570_1.png)

portmap 守护进程

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_571_0.png)

![](img/477ccb2f05b6ba1b2d563ea74f18c197_571_1.png)

**图 12-47：** portmap 程序在服务器和客户端之间运行，以动态为 RPC 分配端口。

## NFS 守护进程

NFS 由四个守护进程实现：

- **rpc.nfsd** 守护进程是主要守护进程，处理所有 NFS 请求。
- **rpc.mountd** 守护进程在文件系统被挂载之前评估导出文件系统的权限。
- **rpc.lockd** 守护进程提供崩溃系统上的锁恢复。
- **rpc.statd** 守护进程处理文件锁定问题。

## NFS 防火墙选项

端口映射器用于动态为 RPC 服务分配端口。这可能会给防火墙的设置带来困难。因此，使用 `/etc/sysconfig/nfs` 文件来控制端口。默认情况下，端口映射器分配给 111 端口的 TCP 和 UDP，而 nfssd 分配给 2049 端口的 TCP 和 UDP。使用的其他守护进程包括 mountd、statd、lockd 和 rquotad。nfs 文件中定义的变量列在表中。这些变量被分配给任何服务均未使用的端口值。在配置防火墙时，所有这些分配的端口和默认端口都允许访问 NFS。

| 变量 | 描述 |
| :--- | :--- |
| MOUNTD_PORT | 指定 mount 服务使用的 TCP 和 UDP 端口。 |
| STATD_PORT | 指定 statd 服务使用的 TCP 和 UDP 端口的状态。 |
| LOCKD_TCPORT | 指定 lockd 服务使用的 TCP 端口。 |

## Exports 文件

**定义：**

*exports 文件* 是用于导出文件系统的配置文件。该文件包含定义，例如要导出的目录以及可以访问该目录的客户端。客户端通过其主机名、IP 地址范围、IP 地址或子网掩码组合，或 NIS 工作组进行寻址。客户端的导出选项在客户端列表旁边的括号内指定。exports 文件存储在 /etc 目录中。默认情况下，主机对文件系统具有只读访问权限。可以使用 *exportfs* 命令激活或停用 exports 文件。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_572_0.png)

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_572_1.png)

## 客户端侧的 NFS 共享

在客户端，使用 *mount* 命令挂载 NFS 共享。mount 命令的语法是：mount *nfs-type* -o *options* remote host:*remote directory local directory*，其中 *nfs-type* 指使用的 NFS 版本，*options* 指挂载选项，*remote directory* 指文件系统要从中挂载的位置，而 *local directory* 指文件系统要挂载到的本地目录。在系统重启期间，必须使用 mount 命令手动重新挂载文件系统。

有两种方法可以在系统重启时自动挂载文件系统。

| 挂载类型 | 描述 |
| :--- | :--- |
| /etc/fstab | 在 /etc/fstab 文件中添加一行代码，由 netfs 服务引用。当初始化脚本从 /etc/init.d/netfs 文件运行时，NFS 共享会被挂载。添加的行的语法是：{server *IP 地址或主机* 名称} {<u>导出的文件系统</u>} {<u>挂载点</u>} nfs ({<u>挂载选项</u>} 0, 0 |
| autofs | 这是一个自动挂载实用程序，用于自动挂载和卸载文件系统，而无需系统资源。它压缩了实现文件系统的内核模块和控制其他功能用户空间守护进程。它使用 /etc/auto.master 文件作为主配置文件。 |

![](img/477ccb2f05b6ba1b2d563ea74f18c197_573_0.png)

## rsync 实用程序

**定义：**

*rsync* 实用程序是用于在系统之间同步文件的工具。它比较两个文件，并以压缩形式发送差异，而不是发送整个文件。*rsync* 守护进程使用存储在 /etc 目录中的 rsyncd.conf 文件进行管理。*rsync* 实用程序使用 rsync 算法来确定文件之间的差异。

**示例：**

![](img/477ccb2f05b6ba1b2d563ea74f18c197_573_1.png)

*rsync* 实用程序的语法是 rsync {源文件或文件夹} {目标文件或文件夹}。

## 语法

## SMBFS 和 CIFS

Samba 文件系统（SMBFS）和公共互联网文件系统（CIFS）是在 Linux 中用于挂载和访问异构网络上可用共享资源的标准文件系统。SMBFS 仅用于 Linux 系统。CIFS 是一个虚拟文件系统，广泛用于共享网络文件和资源。CIFS 提供高级功能，如身份验证、Unicode、分布式缓存和其他核心内核功能。SMBFS 和 CIFS 也可以被理解为客户端协议，它们使安装了 Samba 的 Linux 系统能够作为网络服务器使用。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_574_0.png)

## Samba 守护进程

Samba 有三个守护进程：smbd、nmbd 和 winbindd。smbd 和 nmbd 守护进程由 SMB 服务控制，而 winbindd 守护进程由 WINS 服务控制。

![](img/477ccb2f05b6ba1b2d563ea74f18c197_574_1.png)

| 守护进程 | 描述 |
| :--- | :--- |
| smbd | 服务器消息块守护进程（smbd）用于共享网络资源。它还用于使用 SMB 协议提供用户身份验证、网络资源的访问控制以及数据共享。默认情况下，它监听 139 和 445 端口的 SMB 流量，并从 /usr/sbin/smbd 目录调用。 |
| nmbd | NetBIOS 名称服务守护进程（nmbd）用于处理 WINS 请求并解析 NetBIOS 名称。默认情况下，它监听 137 端口的 NMB 流量，并从 /usr/sbin/nmbd 目录调用。 |
| winbindd | winbindd 用于以 UNIX 平台可理解的方式从 Windows NT 服务器解析用户和组信息。它允许 Windows 用户使用 RPC 调用、PAM 和名称服务切换（NSS）访问 Unix 系统。 |

## NSS

NSS 是一种协议，它允许服务访问数据库以从各种来源检查用户帐户。这在必须访问一个数据库的多个服务的情况下非常有用。例如，hosts 数据库可以通过 NSS 由 NIS 和 DNS 等各种服务访问。

## WINS 服务

Windows Internet 名称服务（WINS）是一个实现 Windows 特定名称解析方法的服务。WINS 由两个主要组件组成：WINS 服务器和 WINS 客户端。WINS 将 Windows 网络上的 IP 地址转换为 NetBIOS 名称。它使用包含网络上计算机的 IP 地址和名称的分布式数据库。数据库会定期更新为最新信息。

