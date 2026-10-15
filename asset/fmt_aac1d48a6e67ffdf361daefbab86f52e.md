
现在，我们可以启动集群：

```
pcs cluster start --all
```

要验证集群是否正在运行，我们可以使用 `pcs` 命令进行检查：

```
pcs cluster status
```

一个健康的新集群应该返回与以下示例类似的输出：

```
[root@web1 conf.d]# pcs cluster status

Cluster Status:

Status of pacemaker-mgr: 'Pacemaker is running' (last updated 2023-07-29 21:04:38 -04:00)

Cluster Summary:

  * Stack: corosync

  * Current: DC2 (version 2.1.5-0.1.el18-a3f4474f94) - partition with quorum

  * Last updated: Sat Jul 29 21:03:33 by hacluster via crmd on web2

  * Last change: 22 configured

  * 0 resource instances configured

Node List:

  * Online: [ web1 web2 ]

PCS Status:

web1: Online

web2: Online
```

![](img/110fa0d6324f0893fff03cee6394144d_214_0.png)

在仅包含两个节点的集群中，法定人数（quorum）的运行机制与更多节点的集群不同。在这样的集群中，法定人数值设置为 1，以确保主节点始终被考虑在法定人数内。如果两个节点都由于网络中断而离线，集群将竞争相互隔离（fencing），第一个成功的节点将获得法定人数通过。为了增加首选节点赢得法定人数的概率，可以配置隔离代理（fencing agent）给其提供优先级。这通过以下命令完成：

```
pcs resource defaults update
```

最后一步是禁用 STONITH，它代表“Shoot The Other Node In The Head”（打掉另一个节点的头）。这是一个高级的隔离工具，需要根据你的环境进行特定配置。如果你想通过技术监控此项，请查看这里的 Oracle 官方文档 — https://docs.oracle.com/en/operating-systems/oracle-linux/8/availability/ConfiguringFencingstonith.html

```
pcs property set stonith-enabled=false
```

为了设置集群，我们需要创建一个集群。

```
[root@web1 ~]# pcs constraint

Location Constraints:

Resource: WebApp

Enabled on:

  Node: web2 (score:INFINITY) (role:Started)

Ordering Constraints:

Colocation Constraints:

Ticket Constraints:

[root@web1 ~]# #
```

![](img/110fa0d6324f0893fff03cee6394144d_218_0.png)

Pacemaker/Corosync 强大之处在于其灵活性。你可以用它对任何内容进行集群化，使其系统管理员的强大工具。

# 在多机器间共享文件系统——集群还是分布式？

当你开始使用负载均衡器和集群软件技术时，通常会遇到需要在多台服务器上使用相同文件的情况。你可以简单地复制文件，但如果可以在每台服务器上挂载文件，从而在不引入 NFS 服务器带来的单点故障（SPOF）的情况下跨系统共享文件系统呢？实现这一点最简单的方法之一就是使用 Cluster。

Gluster（也称为 GlusterFS）是一个开源分布式文件系统，为海量数据提供可扩展且灵活的存储。它最初由 Gluster, Inc. 开发，现在由开源社区维护。Gluster 使用分布式架构创建一个单一且统一的文件系统，该系统可以跨越多个服务器和存储设备。这种方法允许你聚合多个服务器的存储容量，并将其作为一个单一、结构良好的文件系统呈现给用户和应用程序。它有广泛的应用，如数据存储、备份和内容分发。

Gluster 的核心特性和概念包括：

- 可扩展性：向集群中添加更多存储服务器允许 Gluster 能够通过水平扩展轻松应对不断增长的数据需求。
- 冗余性：Gluster 通过在多个节点之间复制数据来确保冗余和容错能力，从而保证可用性。
- 灵活性：Gluster 支持多种存储选项，包括本地磁盘、NAS 和云存储。它可以根据特定的用例和技术进行定制。
- 文件系统抽象：它为用户和应用程序提供了标准的文件系统接口，使其集成到现有系统中变得相对于容易。
- **数据分布**：数据以一种提高性能和可靠性的方式分布在整个集群中。数据可以均匀分布，也可以根据特定标准进行分布。
- **自动修复**：Gluster 具有自愈功能，可以自动检测并修复数据不一致或损坏的文件。

Gluster 通常用于需要大规模分布式存储的环境，例如 Web 服务器、云计算、大数据分析和媒体流传输服务。它为管理跨网络服务器和存储设备的数据提供了一种极具成本效益且灵活的解决方案。

## 准备工作

对于本教程，你需要两个 Oracle Linux 8 系统，每台系统都能够访问 YUM 仓库。在练习中，我们将它们命名为 `gluster1` 和 `gluster2`。它们是相同的系统，每台配有 8 GB 内存、4 个 vCPU 和 100 GB 空间。文件系统有 50 GB，`/home` 目录有 5 GB，swap 分有 8 GB。剩余空间未分配。此外，在本示例中，每个节点将有一个用于 Gluster 数据的 100 GB LUN。

## 警告

强烈建议集群中至少有三个节点，以避免出现“脑裂”（split-brain）集群。虽然双节点集群是可行的，但如果系统发生分裂，就会带来数据损坏的风险。脑裂集群在分布式计算环境中是不受欢迎的，因为它们可能导致数据不一致、损坏和操作问题。脑裂发生在集群中的节点失去彼此的连接或通信时，导致集群分裂为多个孤立的节点。每个节点都认为自己是活动或主集群，导致产生冲突和数据差异的可能。

在每台服务器上，你将执行以下准备工作：

- 1. 在 100 GB LUN 上创建一个 XFS 文件系统。这将用于存储 Gluster 数据，称为 bricks（砖）。在 Gluster 的语境中，brick 是存储集群内的基本存储单元。集群由多个 bricks 组成，每个 brick 本质上指向存储设备。每个 brick 代表了集群总存储容量的一部分。
- 2. 由于我们将使用 Gluster 来管理存储，将不会使用 LVM。在这些系统中，`/dev/sdb` 是 100 GB LUN。使用以下命令来创建并挂载文件系统：

```
mkfs.xfs -i size=512 -L gluster /dev/sdb

mkdir -p /data/glusterfs/volumes/bricks

echo 'LABEL=gluster /data/glusterfs/volumes/bricks xfs defaults 0 0' | sudo tee -a /etc/fstab

mount -a
```
- 3. 完成后，使用 `df` 命令验证文件系统已挂载，如下所示：

```
root@gluster2 # df -h

Filesystem      Size Used Avail Mounted on

tmpfs           3.8G 0 3.8G 0% /dev

tmpfs           3.8G 0 3.8G 0% /dev/shm

tmpfs           3.8G 9.0M 3.8G 1% /run

tmpfs           3.8G 0 3.8G 0% /sys/fs/cgroup

dev/mapper/ol-root 50G 5.6G 45% /

dev/sdb                 100G 0 100G /glusterfs/volumes/bricks

dev/mapper/ol-var 50G 7.1G 43% /var

dev/mapper/ol-home 50G 8.3M 50% /home

dev/mapper/ol-tmp 50G /tmp

dev/sda1          10G 4.5G 47% /boot

tmpfs            256M 0 /user
```
- 4. 我们需要确保所有节点都在 `/etc/hosts` 文件中。在示例中，gluster2 和 gluster3 同时使用了短名和完全限定域名（FQDN）。如下：

```
root@gluster3 ~]# cat /etc/hosts

127.0.0.1 localhost.localdomain

::1 localhost.localdomain
```
