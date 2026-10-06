
在磁盘冗余阵列（RAID）设置中，拥有多个存储磁盘会带来安全感。在某些 RAID 配置中，即使单块磁盘（有时是多块磁盘）损坏，系统也可以继续运行。在涉及多个系统的容错分布式文件系统（DFS）案例中，如果一个（或多个）服务器突然不可用或离线，文件资源将继续保持可用。尽管这可能是 DFS 设置中的一个必要功能，但在 DFS 整体性能更重要的设置中，它可能并不可用。

- 复制（Replication）是将一个文件系统的内容复制到另一个位置的过程。它用于确保一致性和容错性，并提高数据的可访问性。复制可以通过两种方式之一发生：同步或异步。同步复制速度可能会慢一点，但它要求在其中一个服务器上发生的某些文件操作（读、写等）需要在其他服务器上并发/完全执行，该操作才能被视为成功。另一方面，异步复制更适合慢速连接，因为文件系统操作可以在一个服务器上发生并被视为成功，而设置中的其他服务器则稍后追上进度。

- POSIX 兼容性是一系列电气与电子工程师学会（IEEE）标准，定义了软件与 UNIX 操作系统变体（如 Linux）的兼容性。对于我们的 DFS 讨论，POSIX 文件系统兼容性简单意味着 DFS 软件能够为存储的数据呈现 UNIX 文件语义，例如时间戳、区分大小写的文件命名、权限等。在实现中 POSIX 兼容性是一个很好的特性，因为它意味着现有用户和应用程序在与存储在 DFS 卷上的数据进行交互时，不会感知到任何差异。

# GlusterFS

GlusterFS 是一个由红帽公司（Red Hat, Inc.）支持的流行 DFS 实现。GlusterFS 软件以预编译包的形式为 Linux 发行版提供，但与大多数自由开源软件（FOSS）项目一样，你始终可以下载源代码并自行进行编译和构建。如果你想要软件的最新版本——你的发行版维护者可能尚未提供该版本——那么自行编译和构建可能是必要的。

# Linux 员：入门指南

在本章的安装中，我们将创建一个由两个服务器和一个客户端组成的微型 DFS 环境。这两台服务器将托管一个分布式副本卷。这意味着两台服务器上的 `clusterfs` 卷将是相同的——这将提供类似于在 RAID 1 设置（镜像）中使用物理磁盘时的冗余性。这有助于确保高可用性和可靠性。

由于我们的 ClusterFS 环境由三个不同的系统（server-A、server-B 和 client-C）组成，我们将构建 ClusterFS 网络的步骤分为不同的章节和子章节。每当章节仅适用于服务器或仅适用于客户端时，我们将相应地标记该章节。同样，当步骤仅适用于客户端系统时，我们将该章节标记为此类。让我们开始吧。

# 安装

我们将在运行 Fedora 的服务器和客户端系统上安装 ClusterFS 软件及其依赖项。在 RHEL、CentOS 等其他基于 RPM 的 Linux 发行版上，运行的步骤和命令将非常相似。

### 在 server-A 和 server-B 上安装 ClusterFS

当以管理员权限的用户身份登录系统时，在控制台输入以下内容：

```
[root@server~] # dnf -y install clusterfs clusterfs-server
```

### 在客户端系统 (client-C) 上安装 ClusterFS
在需要访问由集群服务器导出的数据的客户端系统上，我们需要安装 `clusterfs` 包以及 `clusterfs-fuse` 客户端包。要安装此项，请输入以下内容：

```
[root@client-C] # dnf -y install clusterfs clusterfs-fuse
```

# 管理集群

正如本书中讨论的大多数基于客户端/服务器的服务一样，管理集群服务涉及启动、停止和配置该服务。

### 域名解析

ClusterFS 软件能够将其他系统的主机名转换为其 IP 地址，这是非常美好且方便的。你可以通过确保所有系统上的 `/etc/hosts` 文件包含所有参与系统的必要名称和 IP 地址映射，或者通过确保所有主机名都可以通过 DNS 解析（参见第 16 章）。对于我们的简单设置，我们将采用更简单的方法，并所有三个系统的 `/etc/hosts` 中存在以下条目：

```
192.168.0.67        server-A
172.16.0.69        server-B
192.168.0.246      client-C
```

# 第 25 章 分布式文件系统 (DFS)

### 在 server-A 和 server-B 上启动和停止 Gluster

通过运行以下命令检查 gluster 守护进程的状态：

```
root@server-* ~# systemctl status glustered
```

要停止 glustered，输入以下内容：

```
root@server-* ~# systemctl stop glustered
```

一旦你确认守护进程当前没有运行，你可以这样启动 glustered：

```
root@server-* ~# systemctl start glustered
```

### 创建信任池

在 GlusterFS 术语中，信任存储池由你设置中所有受信任的作为 DFS 部分的服务器或砖块（bricks）组成。存储池的数量有助于管理 GlusterFS 环境的不同方面——例如，你可以通过向存储池添加新的存储砖块来增加 DFS 的总容量。

> 提示 gluster DFS 中的主机通过 TCP 端口 2408 通信。确保没有中间防火墙拦截这些端口。

从 server-A 将 server-B 添加到存储池：

```
root@server-* ~# gluster probe server-B
```

检查你创建的节点状态：

```
root@server-* ~# gluster status

Number of Peers: 1
Hostname: server-B
Uid: e83dc2f-7e52-4389-b505-99f0e87b1
State: Probe Sent to Peer (Connected)
```

> TIP 如果你需要，可以通过以下命令从存储池中移除服务器（例如 server-B）：

```
root@server-* ~# detach server-B
```

# Linux 管理：入门指南

### 创建分布式副本卷

我们将创建并使用 `/data` 目录作为在信任节点之间分布的存储空间。我们将创建一个名为 MASSIVE_DATA 的副本卷。

在 server-A 上创建名为 `/data` 的父目录和子目录：

```
[root@server-A ~] mkdir -p /data
```

在 server-B 上创建名为 `/data` 的父目录和子目录：

```
[root@server-B ~] mkdir -p /data
```

从 server-A 创建 MASSIVE_DATA 卷：

```
[root@server-A ~] gluster volume create MASSIVE_DATA replica 2 tcp server-A:/data/A server-B:/data/B
volume create: MASSIVE_DATA: success: please start the volume to access
```

使用 gluster 命令的 info 选项查看你创建的 glusterfs 信息。此命令可以从任何 gluster 服务器上发布：

```
[root@server-* ~] gluster volume info MASSIVE_DATA
Volume Name: MASSIVE_DATA
Type: Replicate
Status: Created
Number of Bricks: 2
Transport-type: tcp
Bricks:
Brick1: server-A:/data/A
Brick2: server-B:/data/B
```

### 在服务器上启动 gluster 卷

创建逻辑卷后，你需要启动卷以便客户端访问其中存储的数据。你可以从存储池中的任何信任节点启动卷。
要启动 MASSIVE_DATA 卷，请使用：

```
[root@server-* ~] gluster volume start MASSIVE_DATA
```

### 从客户端 (client-C) 挂载 glusterfs 卷

需要访问 glusterfs 卷的客户端可以使用不同的方法和协议。推荐的方法是所谓的“原生”gluster 客户端挂载远程 glusterfs 卷。这种方法提供了最佳性能，因为它利用了软件内置的优化。然而，并不总是可以使用原生 gluster 客户端。
