
到此为止，Linux 服务器现在可以咨询并查询 Windows 服务器以满足身份验证需求。

# Samba 故障排除

以下是在使用 Samba 时可能会遇到的一些常见问题的解决方案：

## 总结

本章讨论了编译、安装和配置 Samba 的过程，使基于 Linux 的服务器能够与 Windows 网络集成。Samba 是一个强大的工具，具有替代用于文件打印共享 Windows 服务器的潜力。

阅读大量文档可能不是你喜欢的消遣方式，但你会发现 Samba 文档完整、有用且易于阅读。至少浏览一下这些文件看看里面有什么，以便在需要时知道去哪里获取额外信息。

凭借现有的所有的 Samba 书籍（有些免费，有些付费），你应该拥有配置最复杂设置所需的一切。我想到了两本专门针对 Samba 的优秀书籍：John Terpstra 编写的 *Samba-3 by Example* 以及 John Terpstra 和 Jelmer Vernooij 编写的 *The Official Samba-3 HOWTO and Reference Guide*，均由 Prentice Hall 出版。

## 第 24 章：分布式文件系统

![](img/3abd8558488b5c70f9f85ba63df43bc0_587_0.png)

**图 24-1.** 传统的网络文件服务器和局域网客户端

- 一组新的客户端系统——`client-G`、`client-H`、`client-I` 和 `client-J`——需要访问 `server-A` 上的海量数据（`MASSIVE_DATA`）。
- 然而，新客户端并没有直接连接到与 `server-A` 相同的局域网（LAN）。它们通过广域网（Internet）连接。
- 新客户端位于物理和地理位置完全不同的地方。

![](img/3abd8558488b5c70f9f85ba63df43bc0_587_1.png)

**图 24-2.** 传统的网络文件服务器、局域网客户端和广域网客户端

# Linux 管理：入门指南

显然，对于 `server-A` 来说，并没有太大变化——只是多了一组需要访问海量数据的新客户端。

然而，新需求产生了一个问题：尽管 `server-A` 可能仍然能够胜任将其文件系统提供给新的额外的客户端，但服务器与新客户端之间的中间网络可能无法胜任。中间网络可能太慢、拥堵、不可预测等。也可能是 `server-A` 的设计初衷就不是为了处理许多新客户端带来的额外需求和负载。

DFS（分布式文件系统）为这些问题提供的解决方案如图 24-3 所示，并在下述场景中进行了描述：

- 在需要访问海量数据的客户端物理位置附近放置一个额外的文件服务器（`server-B`）。
- 确保无论文件服务器位于何处，所有文件服务器上都存在一份海量数据的副本。
- 确保客户端能够快速、方便且一致地访问海量数据。
- 确保无论客户端在何处访问或修改数据，组成海量数据的位和字节都保持一致且未被损坏。
- 确保海量数据的任何更改都会立即反映在所有副本上，无论这些副本物理上存在于何处。

![](img/3abd8558488b5c70f9f85ba63df43bc0_588_0.png)

**图 24-3.** 分布式文件系统网络

# 第 24 章：分布式文件系统

## DFS 实现

存在许多 DFS 解决方案来解决上述描述的场景。这些解决方案在许多方面都不相同：复杂性、易管理性、易配置性、易部署性、支持的平台、成熟度、应用以及价格。实现方式之所以不同，是因为它们可以包含特殊特性，使其更适用于特定的应用程序或工作负载。以下是一些 DFS 实现方式：

- GlusterFS (`www.gluster.org`) 这种流行的开源分布式/集群文件系统易于设置和使用。源代码正在开发中。大多数流行的 Linux 设备都 easily获得现成的软件包二进制文件。它非常适合高性能和虚拟化云（云计算）类型的工作负载和应用。
- Lustre (`www.lustre.org`) 这种高性能 DFS 实现经常用于集群类型的工作负载和局域网环境。与其他 DFS 解决方案相比，它的架构使其安装、配置和维护变得更加复杂。标准的 Lustre 配置包含这些组件：元数据服务器 (`MDS`)、元数据目标 (`MDT`)、对象存储服务器 (`OSS`)、对象存储目标 (`OST`)，并且 Lustre 需要经过特殊补过的 Linux 内核才能运行。
- MooseFS (`www.moosefs.org`) 这种简单易用、容错的网络 DFS 是一个相对年轻但有前景的 DFS 实现。在基于 Linux 的发行版上易于安装和设置。生产环境中的典型 MooseFS 实现由这些组件组成：主服务器、块服务器（chunk servers）。
- Microsoft DFS：微软的实现是一个成熟的产品，它在 Windows 环境中易于安装。它通过 Samba 模拟某些 DFS 特性，以及 CIFS 协议。
- OpenAFS (`www.openafs.org`) 作为一个较老但健壮的实现，OpenAFS 在多个平台上都有良好的支持。虽然易于安装，但它很大程度上依赖于 Kerberos。
- XtremeFS (`www.xtre.org`) 这种适用于广域网（WAN）环境的新型 DFS 实现非常易于设置和管理。

### DFS 术语

为了应对上述描述的场景，存在许多 DFS 解决方案。这里涉及到以下概念和术语：

- 砖块（brick）：在 DFS 术语中，指的是一个物理存储单元。在某些实现中，DFS 系统通常被称为“砖块”。
- 元数据（metadata）：指的是描述数据的属性，例如文件大小、权限、时间戳等。DFS 实现通常需要专门的元数据服务器来管理这些信息。
- 容错（fault tolerance）：这是一种在发生故障时，确保系统仍然能够正常运行的特性。这对于具有冗余的系统至关重要。
- 复制（replication）：复制是将数据从一份到另一个位置的过程，以确保一致性。复制有两种方式：同步或异步。同步复制需要在服务器上并发执行操作，这可能会减慢速度；而异步复制则更适合连接较慢的环境。

# Linux 管理：入门指南

## 在客户端系统 (`client-C`) 上安装 ClusterFS

对于只需要访问 gluster 服务器导出数据的客户端系统，需要安装 `glusterfs` 服务以及原生的 `glusterfs` 客户端包。要安装这些内容，请输入以下命令：

```bash
[root@client-C ~]# yum install glusterfs glusterfs-fuse
```

## 管理 Gluster

与本书中讨论的大多数客户端/服务器架构的服务一样，管理 gluster 服务涉及启动、停止和配置它。

### 名称解析

GlusterFS 对名称解析非常挑剔。该软件需要能够可靠地将其他系统的主机名翻译为其 IP 地址。您可以通过确保所有系统上的 `/etc/hosts` 文件包含所有参与系统所需的名称和 IP 地址映射表，或者通过确保所有主机名都能通过 DNS 进行解析（见第 16 章）来实现这一点。对于我们简单的设置，我们将采用更简便的方法，确保所有服务器的 `/etc/hosts` 文件中存在以下条目：

```
192.168.0.67               server-A
192.168.0.69               server-B
192.168.0.246               client-C
```

### 在 Server-A 和 Server-B 上启动和停止 Gluster

运行以下命令检查 gluster 守护进程的状态：

```bash
[root@server-A ~]# /etc/init.d/gluster status
```

停止 gluster，请输入：

```bash
[root@server-A ~]# /etc/init.d/gluster stop
```

一旦您确认守护进程当前没有运行，可以这样启动 gluster：

```bash
[root@server-A ~]# /etc/init.d/gluster start
```

### 创建受信存储池

在 gluster 的术语中，受信池（trusted pool）由您的设置中所有信任为 DFS 一的服务器或砖块（bricks）组成。存储池的概念有助于管理 gluster 环境的不同方面——例如，您可以通过向池中添加新砖块来增加 DFS 的容量。

> `gluster` DFS 中的主机通过 TCP 端口 `24007` 和 `24008` 进行通信。请确保 `glusterFS` 和客户端之间没有冲突的防火墙规则（本地或外部）阻止这些端口。为了在我们示例的 Fedora 服务器和客户端上解决这个问题，我们通过禁用 `iptables`（`systemctl stop iptables.service`）临时禁用了默认的 netfilter 防火墙规则。

# 第 24 章：分布式文件系统

从 `server-A` 到 `server-B` 的存储池：

```bash
[root@server-A ~]# gluster peer probe server-B
```
