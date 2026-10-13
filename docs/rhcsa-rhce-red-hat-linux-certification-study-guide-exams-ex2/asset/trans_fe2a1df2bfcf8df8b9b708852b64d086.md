
其他参数与 NFS 共享目录的用户处理方式相关。如表 16-2 所示，这些选项与 root 管理用户、仅匿名用户以及可在参数中指定的其他用户相关联。

## 激活导出列表

仅仅配置 /etc/exports 文件是不够的，因为它只是导出的目录的默认集合。你需要使用 exportfs -a 命令来激活它们。下次 RHEL 6 启动时，如果正确的服务已激活，nfs 启动脚本 (/etc/init.d/nfs) 会自动运行 exportfs -r 命令，该命令会重新导出 /etc/exports 中配置的目录。

然而，如果你正在修改、移动或删除共享，最安全的做法是先使用 exportfs -ua 命令临时取消导出所有文件系统，然后再使用 exportfs -a 命令重新导出共享。

一旦导出处于活动状态，很容易检查。只需在服务器上运行 showmount -e 命令即可。要查看远程 NFS 服务器的导出列表，只需添加 NFS 服务器的名称即可。例如，showmount -e server1.example.com 命令会查找来自 server1.example.com 系统的已导出 NFS 目录列表。如果此命令无法工作，通信可能被防火墙阻止。

## /home 目录的特殊要求

某些系统将用户 /home 目录存储在中央服务器上。此类目录可通过 NFS 共享。然后管理员可以定期备份 /home 目录，或许辅以 RAID 数组的配置。这基于用户和密码的中央身份验证数据库，例如 LDAP 或 Kerberos。在某些情况下，/home 目录可能在没有共享身份验证数据库的小型网络上共享。

无论哪种情况，你都应配置 /etc/idmapd.conf 文件，以设置 NFS 共享的 /home 目录如何读取身份验证数据库。否则，此类主目录可能会配置为由名为 nobody 的用户拥有，这对普通用户来说会很麻烦。

/etc/idmapd.conf 文件简洁明了且注释完善。在所有情况下，你都应更改 Domain、Nobody-User 和 Nobody-Group 指令，使其与当前网络的域以及 nfsnobody 用户和组相匹配，以最小化相关权限。对于 example.com 域，应该是

```
DOMAIN = example.com
Nobody-User = nfsnobody
Nobody-Group = nfsnobody
```

虽然所示的 nsswitch 选项本应是默认值，但在我的测试中，我发现将其明确写出很有用：

```
Method = nsswitch
```

正如第 8 章所述，LDAP 身份验证可以纳入关联的 /etc/nsswitch.conf 文件中。尽管如此，数据库中还显示了用于连接 LDAP 和 Kerberos 服务的额外自定义选项。

你需要在每个 NFS 客户端上的所有 /etc/idmapd.conf 文件中进行相同的更改。更改在 NFS 服务器和每个 NFS 客户端上运行 /etc/init.d/rpcidmapd restart 命令时生效。

表 16-2
NFS 工具用户访问选项

| Parameter | Corresponding /etc/exports Command / Description |
|---|---|
| no_root_squash | 将远程 root 用户视为本地 root；远程 root 用户在共享目录上获得 root 权限。 |
| all_squash | 将所有客户端用户视为匿名用户；所有远程用户都映射为匿名用户。 |
| anonuid=user id | 指定匿名用户的本地用户 ID；支持将远程用户映射到特定用户 ID，例如 guest。 |
| anongid=user id | 指定匿名组的本地组 ID；支持将远程组映射到特定的组 ID。 |

## /etc/sysconfig/nfs 中的固定端口

NFSv4 更易于配置，尤其是在防火墙方面。要启用与 NFSv4 服务器的通信，你绝对需要打开的端口只有 TCP 端口 2049 和 UDP 端口 111。端口 2049 是 NFSv4 通信的标准。端口 111 支持网络上的 RPC 通信。然而，这并不能支持 NFS 相关命令的完整功能。

虽然 NFSv4 是默认版本，但 RHEL 6 仍然支持 NFSv2 和 NFSv3。因此，鉴于 RHCE 考试中公开可用的信息，你还需要知道如何处理这些版本的 NFS。NFSv2 和 NFSv3 及其相关服务使用动态端口号。即使对于 NFSv4，你也可能希望固定其中一些相关端口，以支持 showmount 命令的使用。有了固定端口，你就可以配置防火墙，打开适当的端口来支持 NFS 服务器。

为此，请查看 /etc/sysconfig/nfs 文件。它已预先配置好注释，建议使用适当的固定端口号。虽然你不必遵循文件中注释版本中建议的端口号，但可以这样做。一般来说，这样的端口号不会引起问题，因为它们不会与任何常用的 RHEL 6 服务冲突。然而，为了方便，许多管理员为此目的设置一系列连续的未使用端口，例如 4000 到 4003。

表 16-3 中列出的端口号按 /etc/sysconfig/nfs 文件默认版本中所示的顺序列出。该表不包括现已过时的 rpc.lockd 守护进程的引用，因为 RHEL 6 中不可用。

一旦对 /etc/sysconfig/nfs 文件进行更改并保存后，使用 /etc/init.d/nfs restart 命令重启相关服务。如果成功，你将在 rpcinfo 命令的输出中看到相关端口，该命令列出与 RPC 关联的所有通信通道。以下命令更精确，因为它隔离了实际端口号：

```
# rpcinfo -p
```

示例输出显示在图 16-1 中。乍一看，这些行可能显得重复；然而，每一行都有其目的。除非运行了另一个 RPC 相关服务，例如网络信息服务 (NIS)，否则当使用 NFSv2 或 NFSv3 时，这里显示的所有行都是 NFS 通信所必需的。请查看此处显示的第一行：

```
program vers proto port service
100000 4 tcp 111 portmapper
```

## 表 16-3

NFS 固定端口选项

| Port | Parameter | Description |
|------|-----------|-------------|
| 875 | RQUOTAD | 远程配额守护进程 |
| 892 | MOUNTD_PORT | 用于挂载请求 |
| 662 | STATD_PORT | 用于状态请求，包括锁定文件（端口 662 分配给通常未使用的 FTP 协议） |
| 2020 | STATD_OUTGOING_PORT | 引用到传出通信。 |

## 图 16-1

带有 NFS 相关端口的 rpcinfo -p 示例输出

```
[root@MinimalRHEL6 ~]# rpcinfo -p
program vers proto port service
100000 4 tcp 111 portmapper
100000 3 tcp 111 portmapper
100000 2 tcp 111 portmapper
100000 4 udp 111 portmapper
100000 3 udp 111 portmapper
100000 2 udp 111 portmapper
100011 1 udp 875 rquotad
100011 2 udp 875 rquotad
100011 1 tcp 875 rquotad
100011 2 tcp 875 rquotad
100003 2 tcp 2049 nfs
100003 3 tcp 2049 nfs
100003 4 tcp 2049 nfs
100227 2 tcp 2049 nfs_acl
100227 3 tcp 2049 nfs_acl
100003 2 udp 2049 nfs
100003 3 udp 2049 nfs
100003 4 udp 2049 nfs
100227 2 udp 2049 nfs_acl
100227 3 udp 2049 nfs_acl
100021 1 udp 32769 nlockmgr
100021 3 udp 32769 nlockmgr
100021 4 udp 32769 nlockmgr
100021 1 tcp 32803 nlockmgr
100021 3 tcp 32803 nlockmgr
100021 4 tcp 32803 nlockmgr
100005 1 udp 892 mountd
100005 1 tcp 892 mountd
100005 2 udp 892 mountd
100005 2 tcp 892 mountd
100005 3 udp 892 mountd
100005 3 tcp 892 mountd
[root@MinimalRHEL6 ~]#
```

第一行表示任意 RPC 程序号、NFS 版本、使用 TCP 作为通信协议、通过端口 111、以及 portmapper 服务。请注意 portmapper 服务对 NFS 版本 2、3 和 4 的可用性；通过 TCP 和 UDP 协议进行通信。

通过所选端口的通信也应允许通过任何配置的防火墙。例如，图 16-2 显示了支持远程访问本地 NFS 服务器的防火墙的 /etc/sysconfig/iptables 文件。

当然，你可以使用第 10 章中讨论的防火墙配置工具来设置这些防火墙规则。
