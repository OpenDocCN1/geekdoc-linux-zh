
```
# df -t nfs
Filesystem              512-blocks     Used  Available Capacity Mounted on
babylon5:/etc            1002864   185468    805728    19%     /mnt
```

本质上，如果当前为导出的文件系统提供访问服务的成员发生故障，另一个集群成员应接替其职责，继续提供服务。

NFS 客户端和服务器守护进程可以同时在多个集群成员上运行。目前，无法限制将某个挂载点导出到特定别名。但通过使用 /etc/exports.aliases 文件，客户端可以使用仅由特定集群成员加入的别名来执行挂载命令，从而使得只有集群中被选中的成员（该别名的成员）才会为请求的客户端提供 NFS 服务。

```
# *** You must be very careful to ensure that for each file system
# being exported to NFS clients, the CFS server of the file system
# is a member of the cluster alias being used by the clients.
# Otherwise performance will be severely degraded for NFS over UDP
# mounts. This is because an attempt is always made to tunnel NFS
# over UDP packets to the CFS server for the file system. If the
# server is not a member of the cluster alias being used, then
# each packet is randomly assigned to a node that is a member of
# the alias by the cluster alias round robin algorithm. Having 10
# requests for the same file handled by different CFS clients will
# severely degrade performance.
```

更多信息，请参阅 exports.aliases(4) 参考手册页。

可以使用 nfsconfig 或 sysman 配置 NFS。使用 sysman 而不指定焦点，表示配置应面向整个集群进行。因此，任何配置信息都将放置在 /etc/rc.config.common 中。

### 20.4.3 NFS 锁定

在应用程序与 NFS 挂载的文件系统打交道时，可能需要进行文件锁定。如果需要，则必须在客户端成员上运行 rpc.lockd(8) 和 rpc.statd(8) 守护进程的客户端副本。这些锁定守护进程的服务器版本每次将在集群中的一个成员上运行。在您的集群中，这些守护进程作为由 CAA 管理的高可用性应用程序资源（cluster_lockd）运行。

```
# caa_stat -t cluster_lockd
Name           Type        Target   State    Host
---------------------------------------------------
cluster_lockd  application ONLINE   ONLINE   molari
```

有关 CAA 的更多信息，请参阅第 23 章和第 24 章。有关 NFS 锁定的更多信息，请参阅 `rpc.lockd(8)` 和 `rpc.statd(8)` 参考手册页，以及 *Tru64 UNIX* 网络管理指南（V5.0A 和 V5.1）和 *Tru64 UNIX* 网络管理：服务指南（V5.1A 及更高版本）。

## 20.5 集群中的 NIS

网络信息服务（NIS）是另一种基于客户端/服务器的机制，通过该机制可以有效地在网络节点间分发数据。NIS 的一个常见用途是在多个网络节点之间分发 `/etc/passwd` 文件，以便在一个节点上更改的密码能够有效地分发到所有节点。主服务器负责将数据库文件（例如密码文件）的副本分发给从服务器（如果有）。NIS 客户端向服务器请求信息，并随着请求获取数据。客户端不保存数据库文件的副本。从服务器则保存有主服务器发送给它们的文件副本。

集群可以是 NIS 客户端、NIS 从服务器或 NIS 主服务器。此服务在集群中不具备与 NFS 同等的灵活性。您不能使某些成员提供服务，而其他成员作为客户端运行。所有成员必须使用相同的 NIS 域名。这意味着，您不能将 NIS 设置为集群的一半服务一个域，而另一半服务另一个域。如果在创建集群时已配置 NIS，则集群启动时 NIS 将正常工作。您也可以在集群启动后使用 `nissetup(8)` 配置 NIS。在其他成员上，使用“`/sbin/init.d/nis start`”。对于主服务器、从服务器或客户端，配置 NIS 的一般顺序是在一个成员上使用 nissetup，然后手动在其余所有成员上启动 NIS。

NIS 服务器映射传输守护进程（`ypxfrd(8)`）控制以下活动：主服务器向从服务器发送信息（`yppush(8)`），或从服务器向主服务器请求数据（`ypxfr(8)`）。`ypxfrd(8)` 是多实例的，在所有成员上均处于活动状态。`rpc.yppasswdd(8)` 也存在于主服务器集群的所有成员上，但它是单实例的。换句话说，同一时间集群中只有一个 `rpc.yppasswdd` 实例在运行，但它并未作为 CAA 实现。

## 20.6 杂项服务

本节提供您可能在集群中使用的其他几个服务的概要信息。

### 20.6.1 Internet 服务器守护进程（`inetd`）

Internet 守护进程（`inetd(8)`）负责响应传入的网络请求，启动许多其他服务器守护进程。inetd 的配置文件（`/etc/inetd.conf`）是一个集群范围的文件。它提供了一种机制，用于请求应在每个成员上以相同方式运行的基于守护进程的服务。在集群中，还有另一个配置文件（`/etc/inetd.conf.local`）
