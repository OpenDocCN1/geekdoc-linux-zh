
Ganglia 项目始于加州大学伯克利分校，旨在支持依赖计算机进行数据分析的科学研究。Ganglia 网页显示该项目“力求通过创建一个无处不在、连续且普及的国家基础设施：网格（Grid）来推进科学发展”。然而，目前我们只关心 Ganglia 监控和显示我们构建的集群信息的能力。

与“集群（cluster）”术语一样，“网格（grid）”也被描述各种计算系统。该术语最常用的用法演变自科学社区，当时被用来描述多个独立且地理位置分散的集群。根据这个定义，网格可以包含一个集群，但集群不包含一个网格。然而，网格和集群都是并行运行负载的计算环境。

Ganglia 软件包由几个命令行工具（我们稍后会看到）以及运行在集群节点上的守护进程组成。在描述如何在集群上安装 Ganglia 之前，让我们先简要检查两个 Ganglia 守护进程。

# gmond

`gmond` 是 Ganglia 的监控守护进程。`gmond` 的工作是收集其运行机器的性能指标，并跟踪集群中运行的每一个其他 `gmond` 的状态。如果其中一个 `gmond` 守护进程崩溃（例如由于集群节点故障），所有幸存的 `gmond` 都会获此消息。

`gstat` 工具可以用 XML 格式报告 `gmond` 收集的信息。从 2.7.0 版本开始，`gmond` 可以在将此 XML 数据发送到网络之前对其进行压缩。

# gmetad

每个集群节点都需要安装 `gmetad`，但 `gmetad` 守护进程只需要运行在集群节点管理器上¹。`gmetad` 每 15 秒轮询一次 `gmond` 守护进程获取性能指标信息，并使用 `RRTool` 将这些信息存储在轮询数据库中。（在轮询数据库中，最新数据会覆盖旧数据，因此数据库永远不会填满。）

`gmetad` 使用 Apache Web 服务器显示它收集的信息。其显示网页的能力通过 Ganglia Web 软件包（以前称为 Ganglia Web Frontend）实现。我们稍后会讨论 Ganglia Web。

> ¹ 参见引言部分以关于集群节点管理器的描述。

# 安装 Ganglia 的先决包

我将在描述如何安装和使用 Ganglia 的同时，解释它的工作原理。我们将从在集群节点上开始安装 `gmond`，然后在集群节点管理器上安装 `metad` 和 Ganglia Web 软件包。但首先，要安装 `metad` 和 Ganglia Web 软件包在集群节点上运行所需的其他包：PHP、RRDtool 和 Apache。

## 安装 PHP

Ganglia Web 软件包需要 PHP。PHP 的源代码包含在本书附带 CD 盘的 `chapter18/version2/dependencies` 目录中，但你可能会发现直接安装你发行版自带的 PHP 软件。例如，如果你使用的是 Red Hat，php 的 rpm 文件名为 `php-<version-number>.rpm`。在尝试安装 Ganglia 之前，你必须在集群节点管理器上安装 PHP。

## 安装 RRDtool

接下来，从源代码（`chapter18/version2/dependencies/on-CD-ROM`）在集群节点管理器上安装 RRDtool。解压源文件，然后在 RRDtool 源目录的顶部使用以下语句进行编译

> 注意来自 RRDtool 安装脚本中一个小而无害的玩笑，它假装为开发者 Tobi Oiker 订购一张 CD。你可以通过贡献 Happy RRDtool 项目来支持 RRDtool 的开发和维护（参见 http://www.rrdtool.com/license.html）。

```
#/configure --enable-shared
#make site-perl-install
#make install
```

你只需要在集群节点管理器上安装 PHP 和 RRDtool。

Ganglia 监控核心 `metad` 期望 RPM 在 `/usr/lib` 目录下找到 RRDtool 的共享库（`librrdd.so`）。使用以下命令将其拷贝到位置：

```
#cp /usr/local/RRDtool-<version>/lib/librrdd.so* /usr/lib
```

接下来，将 RRDtool 二进制文件放置在标准系统路径中，以便 Apache 找到它们：

```
#cp /usr/local/RRDtool-<version>/bin/* /usr/bin
```

## 在集群节点管理器上安装 Apache

第 12 章讨论了如何在集群节点上安装和配置 Apache（另见附录 F），你可以使用这些指令在集群节点管理器上安装 Apache。

为了让 Ganglia Web 软件包正常工作，必须配置 Apache 以支持 PHP 模块，我们稍后会讨论。

# 在集群节点管理器上安装 Ganglia

安装好所需的包后，你就可以在集群节点管理器上安装 Ganglia 了。

从 Ganglia 网站下载最新的 Ganglia 软件 RPM 包，并使用标准的 RPM 命令安装它们。以下是 Ganglia 发布 3.0 前后的 RPM 包名列表：

| 旧版 RPM 包名 | 3.0 及以后的 RPM 包名 |
| :--- | :--- |
| `ganglia-monitor-core` | `ganglia-gmetad` |
| `ganglia-monitor` | `ganglia-gmond` |
| `ganglia-webdriver` | `ganglia-web` |
| `ganglia-monitor-lib` | `ganglia-devel` |
| `gexec` | `ganglia-client` |

在集群节点管理器上，你需要安装 `gmetad`、`gmond`、`web` 以及（可选的）`ganglia-client`。

> 注意：在安装 `ganglia-web` 时可能需要使用 `--nodeps` 来忽略依赖关系。

> 如果你是从源码编译 `gmond` 而不是从 RPM 安装，你必须使用 `gexec` 标志来支持 `gexec`。

# 在集群节点上安装 Ganglia

在集群节点上安装 `gmond`，但不安装 `gmetad`（我们只想在集群节点管理器上收集并存储历史指标）。

以下是 Ganglia 版本前后的 RPM 包名：

| RPM 包名 | 新（3.0）RPM 包名 |
| :--- | :--- |
| `ganglia-monitor` | `ganglia-gmond` |
| `ganglia-core-lib` | `ganglia-devel` |
| `gexec` | `ganglia-server` |

# 在集群节点管理器上配置 gmetad 和 gmond

是时候配置 Ganglia 了。让我们从集群节点管理器上的 `gmetad` 和 `gmond` 开始。`gmetad` 由 `/etc/gmetad.conf` 文件控制，`gmond` 由 `/etc/gmond.conf` 控制。

## 修改 /etc/gmetad.conf

集群节点管理器上的 `/etc/gmetad.conf` 文件只需要一行指定集群名称²以及集群内部节点的名称。例如，以下条定义了一个名为 Cluster1 的集群以及本地（集群节点管理器）以及两个名为 `clnode1` 和 `clnode2` 的集群节点：

```
data_source "Cluster1" localhost clnode1 clnode2
```

- 如果节点名称发生变化，你需要修改集群节点管理器上的 `/etc/gmetad.conf` 文件，重启所有节点上的 `gmond`，然后重启集群节点管理器上的 `gmetad` 以使更改生效。
- 数据源中的每个节点应具有相同的信息供 Ganglia 监控。因为 Ganglia 通信使用对称模型（广播），列表中一个节点的故障意味着 Ganglia 可以连接到下一个节点。因此，没有在每个 `data_source` 条目中指定集群中的所有主机。

## 修改 /etc/gmond.conf

`/etc/gmond.conf` 文件只需要指定集群名称。我们稍后将在所有集群节点上使用此配置文件。例如：

```
name "Cluster1"
```

- 查看 `/etc/gmond.conf` 文件中的注释，了解你配置时可能需要的其他选项（例如 `gmond` 应使用的以太网端口、对于未连接到同一以太交换机的集群，允许的广播跳数，以及 `gmond` 对 XML 数据应使用的压缩级别³）。

> ² 这是书中首次（也是唯一一次）我们被为安装的任何软件包为集群命名（除了你用于客户端连接集群服务的 VIP 地址的名称外）。
> ³ 默认压缩级别为 0，即不压缩。你只有在非常大的集群上或当你正在监控网格（集群的集群）时才应该使用压缩。

# 启动 gmond 和 gmetad

在集群节点管理器上对两个配置文件（`/etc/gmond.conf` 和 `/etc/gmetad.conf`）进行更改后，启动 `gmond` 和 `gmetad`：

```
#service gmond restart
#service gmetad restart
```

注意：请参阅第 1 章获取有关如何在系统启动时自动启动这些服务的说明。

现在，在集群节点管理器上输入以下命令以确保 `gmond` 正常工作：
