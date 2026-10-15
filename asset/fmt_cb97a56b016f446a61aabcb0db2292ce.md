
`-a` 选项表示导出 `/etc/exports` 中列出的所有目录。`-r` 将所有导出项与当前的 `/etc/exports` 文件重新同步（禁用文件中未列出的导出）。`-v` 选项表示打印详细输出。在此示例中，本地服务器的 `/pub` 和 `/home` 目录可立即供命名为 maple 和 spruce 的客户端计算机挂载。`/mnt/win` 目录对所有客户端计算机可用。

# 加固你的 NFS 服务器

NFS 的创建时，加密和其他安全措施尚未惯常地构建到网络服务中（例如远程登录、文件共享和远程执行）。因此，NFS（即使是到版本 3）仍存在一些相当显眼的安全问题。

NFS 安全问题使其成为不适合在公共网络上使用的设施，甚至使其在组织内部的加固变得困难。以下是一些问题：

- **远程 root 用户**：即使使用了默认的 `root_squash`（防止 root 访问远程共享），任何你共享 NFS 目录的机器上的 root 用户都可以访问任何其他用户账户。因此，如果你正在进行诸如共享具有读/写权限的家目录的操作，那么与你共享的任何机器上的 root 用户都对这些家目录的内容具有完全访问权限。
- **未加密的通信**：由于 NFS 流量未加密，任何嗅探你网络的人都可以看到正在传输的数据。
- **用户映射**：NFS 共享的默认权限通过用户 ID 映射。例如，NFS 客户端上 UID 为 1000 的用户可以访问 NFS 服务器上 UID 为 1000 的文件。无论使用什么用户名。
- **文件结构暴露**：到 NFSv3 为止，如果你通过 NFS 共享目录，你就暴露了该目录在服务器文件系统上的位置。（换句话说，如果你共享了 `/var/stuff` 目录，客户端就会知道 `/var/stuff` 在服务器上的精确位置）。

这些是坏处。好消息是，大多数问题在 NFSv4 中得到了解决，但需要额外的配置。通过集成 Kerberos 支持，NFSv4 让你根据每个用户的 Kerberos 票据配置用户访问。对你来说，额外的工作是配置 Kerberos 服务器。对于暴露 NFS 共享位置，使用 NFSv4，你可以将共享目录绑定到 `/exports` 目录，在该目录中它们被共享，但其精确位置不会被暴露。

访问 `https://help.ubuntu.com/community/NFSv4Howto` 获取 Ubuntu 中 NFSv4 的特性。

至于与 NFS 相关的标准 Linux 功能，`iptables` 防火墙、`TCP wrappers` 和 `SELinux` 可以在加固和从远程客户端访问你的 NFS 服务器方面发挥任何作用。特别是，让防火墙功能与 NFS 工作可能特别具有挑战性。这些安全特性将在后面的章节中描述。

# 为 NFS 打开防火墙

NFS 服务依赖于几个不同的守护进程进行正常操作，这些守护进程大部分在不同的端口监听访问。Fedora 中使用的默认 NFSv4 必须开放 TCP 和 UDP 端口 2049 (`nfs`) 和 111 (`rpcbind`)，NFS 服务器才能正常运行。服务器还必须开放 TCP 和 UDP 端口 20048，以便 `show-mount` 命令能够从服务器上的 `rpc.mountd` 查询 NFS 共享目录。

对于 RHEL 8、Fedora 30 以及其他使用墙服务的系统，你可以使用防火墙配置窗口（`yum install firewall-config`）为你的 NFS 服务打开防火墙。**输入 `firewall-config`**，确保窗口中的 `mountd`、`nfs` 和 `rpc-bind` 已被勾选，以开放相应的端口来访问你的 NFS 服务。图 20.3 显示了此类示例：

## 图 20.3

使用防火墙配置窗口打开防火墙以允许访问 NFS 服务。

![](img/cc1e2b1a5739a47bac1a4c7cfac7c1a6_550_0.png)

对于 RHEL 6 和其他直接使用 `iptables` 服务的系统（在添加防火墙之前），要内核 NFS 服务器上开放端口，请确保 `iptables` 已启用并带有类似以下 `/etc/sysconfig/iptables` 文件的防火墙规则启动：

```
-A INPUT -m state --state NEW -m tcp -p tcp --dport 111 -j ACCEPT
-A INPUT -m state --state NEW -m udp -p udp --dport 111 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 2049 -j ACCEPT
```

```
-A INPUT -m state --state NEW -m udp -p udp --dport 2049 -j ACCEPT
-A INPUT -m state --state NEW -m tcp -p tcp --dport 20048 -j ACCEPT
-A INPUT -m state --state NEW -m udp -p udp --dport 20048 -j ACCEPT
```

在 Red Hat Enterprise Linux 6.x 及更早版本中，防火墙要复杂一些。与防火墙相关的问题是与 NFS 相关的多个服务在不同的端口监听，而这些端口是随机分配的。为了绕过这个问题，你需要锁定这些服务使用的端口号并打开防火墙以便这些端口可以被访问。

为了锁定 NFS 端口项的过程，需要在 `/etc/sysconfig/nfs` 文件中添加内容以为服务分配特定的端口号。以下是 `/etc/sysconfig/nfs` 中静态端口的选项示例：

```
QUOTAD_PORT=4901
LOCKD_TCP=4902
LOCKD_UDP=4903
MOUNT_PORT=4904
STAT_PORT=4905
STAT_OUTGOING_PORT=4906
RDMA_PORT=4907
```

使用这些端口，我重启了 NFS 服务（`service nfs restart`）。使用 `netstat` 命令，你可以看到在分配端口上监听的结果：

```
tcp 0 0 0.0.0.0:4901 0.0.0.* LISTEN 4682/rpc.quotad
tcp 0 0 0.0.0.0:4902 0.0.0.* LISTEN
tcp 0 0 0.0.0.0:4904 0.0.0.* LISTEN 4698/rpc.mountd
tcp 0 0 ::4902 ::: LISTEN
tcp 0 0 ::4904 ::: LISTEN 4698/rpc.mountd
udp 0 0 0.0.0.0:4901 0.0.0.*
udp 0 0 0.0.0.0:4904 0.0.0.* LISTEN 4698/rpc.mountd
udp 0 0 ::4903 :::
nudp 0 0 ::4904 ::: 4698/rpc.mountd
```

# 在 TCP wrappers 中允许 NFS 访问

对于 `vsft` 和 `sshd` 等服务，Linux 中的 `TCP wrappers` 允许向 `/etc/hosts.allow` 和 `/etc/hosts.deny` 文件添加信息，以指示哪些主机可以访问该服务。虽然 `nfsd` 守护进程未启用 `TCP wrappers`，但 `rpcbind` 服务启用了。

对于 NFSv3 及更早版本，只需在 `/etc/hosts.deny` 文件中添加如下行即可拒绝 `rpcbind` 服务的访问，但也拒绝访问你的 NFS 服务的：

```
rpcbind ALL
```

## 第 20 章：配置 NFS 服务器

然而，对于默认运行 NFSv4 的服务器，`rpcbind ALL` 行仅阻止了外部主机使用 `showmount` 等命令获取有关 RPC 服务（如 NFS）的信息。但是，它并不会阻止你挂载 NFS 共享目录。

### 为你的 NFS 服务器配置 SELinux

当 SELinux 设置为允许（`permissive`）或禁用（`disabled`）时，它不会阻止对 NFS 服务的访问。但在强制（`enforcing`）模式下，你应该了解一些 SELinux 布尔值。要检查系统上 SELinux 的状态，请查看以下：

```bash
# getforce
Enforcing
# grep SELINUX=/etc/sysconfig/selinux
SELinux-enforcing
```
