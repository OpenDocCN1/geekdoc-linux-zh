
# 第八部分：网络管理服务

| 网站 | 名称 |
| :--- | :--- |
| fedoraproject.org/wiki/Tools/GFS | Fedora GFS 资源和链接 |
| pvfs.org | 并发虚拟文件系统, PVFS2 (开源) |
| sourceware.org/gfs | 全局文件系统 (Fedora 版本及商业版) |
| coda.cmu.edu | Coda 文件系统，离线移动访问访问（实验性） |
| ftp.coda.cmu.edu/pub/coda/linux |（实验性） |
| inter-mezzo.org | Intermezzo (开源) |
| clusterfs.com | Lustre |

表 37-1 分布式文件系统

PVFS 管理服务器使用两个配置文件，`pvfs2-fs.conf` 和 `pvfs2-server.conf`。你使用配置脚本 `pvfs2-genconf` 创建这些文件。该脚本将提示你输入配置信息，如协议、端口、日志文件和存储目录。要配置集群网络，请务必输入带有 I/O 服务器的宿主机。

管理服务器使用 `pvfs2-server`。要管理服务器，请使用 `pvfs2-server` 服务脚本。

在 I/O 服务器上，你运行 `pvfs2-server` 脚本来创建存储空间并启动服务器。I/O 服务器使用 `/etc/pvfs2-fs.conf` 配置文件。你可以使用 `pvfs2-server` 服务器脚本来自动启动系统。

在使用 PVFS 的客户端上，你需要安装文件系统配置和访问工具。每个客户端都需要一个 PVFS 守护进程 `pvfs2-client` 及其支持模块和库。文件系统挂载配置可以存储在 `/etc/fstab` 中，尽管你也可以直接将条目放在 `/etc/fstab`。在 `mount` 命令中使用 `-t` 选项挂载 PVFS 类型。PVFS 使用自己的一套文件命令，如 `pvfs2-ping`、`pvfs2-cp`、`pvfs2-is`，来列出和访问其文件系统上的文件。

客户端可以通过内核模块（提供 Linux 文件系统访问权限）或 MPI-IO 接口来访问 PVFS 文件系统，后者需要使用 `libpv2` 库，但为并行应用提供了更好的性能。PVFS 中的并行支持是通过消息传递接口 (MPI) 实现的由 ROMIO (www-unix.mscl.anol.gov) 和来自阿根根实验室 MCS 部门的 MPICH2 (www-unix.mscl.anol.gov/mpi/mpich2) 支持。

> **注意** 为了让应用程序充分利用 PVFS，它们应该启用 PVFS 功能，这将剥离其文件数据以便在 PVFS 系统上更好地使用。

# Coda

Coda 由卡内基梅隆大学开发的一个实验性项目，但免费提供。其功能特性包括支持移动计算、访问控制和带宽自适应。你可以从 `coda.cmu.edu` 获取有关 Coda 的信息，并从 `ftp.coda.cmu.edu/pub/coda/linux` 下载某些版本的包。

# 第 37 章：分布式网络文件系统

通过内核模块连接虚拟文件系统，可以从客户端上的 Coda 目录（通常为 `/coda`）访问分布式 Coda 文件。Coda 会会在客户端维护频繁访问文件的缓存以提高效率。缓存由处理所有文件系统操作的缓存管理器维护。缓存允许客户端进行离线操作，让用户可以在本地处理文件，稍后更新到主服务器。离线操作对于移动计算非常有效，因为笔记本电脑可能会长时间断开网络。用户频繁使用文件的对应数据库（称为“hordes”）也在服务器上维护，以便于更新。

要配置客户端，你需要 `coda-debug-client` 包。使用 `venus-setup` 脚本配置客户端，然后使用 `venus` 守护进程启动 Coda。对于服务器，你需要安装 `coda-debug-setup` 包并运行 `venus-setup` 来配置服务器。

## 红帽全局文件系统 (GFS 和 GFS 2)

红帽（Red Hat）发布了其全局文件系统 (GFS)，这是一个开源、免费提供的分布式网络文件系统。原始 GFS 版本随 Fedora 4 和 5 发布。从 Fedora 6 开始，包含了新版本的 GFS 2，它使用了类似的配置和管理工具集，以及原生内核支持。GFS 2 不再由一系列看似互不相关的包组成，而是通过三个包实现：`gfs2-utils`、`cman` 和 `lvm-cluster`。对 GFS 2 的原生内核支持提供了更好的内核级操作性能。

GFS 将物理实现与逻辑格式分离。GFS 在你的 Linux 文件系统上显示为一个目录。逻辑卷由集群逻辑卷管理器 (CLVM) 创建和管理，它是一个集群-LVM。物理上，文件系统由分布在网络中的不同存储资源（称为集群节点）构建。管理员管理这些节点，提供必要的镜像或存储扩展。如果某个节点故障，GFS 可以隔离该系统（fence）直到其恢复。设置 GFS 需要规划。你必须提前确定不同的设置，例如你的全局文件系统的名称和数量、能够挂载文件系统的节点、隔离方法，以及要使用的分区和磁盘。

![](img/6ac214f13c9ea7c0ad85ba43163f14a1_814)

# 第八部分：网络管理服务

详细信息请查看 `sourceware.org/cluster` 上的集群项目。GFS 文档可以在 Red Hat 上找到。GFS 指南可能会有所帮助，但可能已经过时。GFS 现在使用逻辑卷代替池（pools）。

| 网站 | 名称 |
| :--- | :--- |
| redhat.com/software/GFS | 全局文件系统 (Red Hat) |
| redhat.com/docs/manager/csdg/ | 全局文件系统 Red Hat |
| source.org/cluster | 集群项目 |
| /etc/cluster/conf | 集群配置 (css) |

# GFS 2 包 (Fedora Core 6 及更高版本)

原始的 GFS (GFS 1) 使用多种不同的独立包用于集群服务器和管理工具，这些包从名称上看并没有关联。在 GFS 2 中，这些包被合并到了 `cman` 和 `gfs2-tools` 包中。在这里你将找到诸如 `fence`、`cman` 集群管理器、`dlm` 锁定和 `css` 配置等工具。集群配置由集群配置系统 `css` 支持。隔离（Fencing）用于隔离故障的资源。隔离服务器的 LVM 支持位于独立的包中，如 `lvm2-cluster` (Fedora) 或 `clvm` (Debian)。

要运行集群，你同时需要集群管理器和锁定机制。分布式锁管理器 `dlm` 通过 `cman` 实现了集群管理和锁定，`cman` 管理集群设备和之间的之间的连接，并使用 `dlm` 提供锁定。`dlm` 锁定机制作为守护进程运行，并带有支持库。

所有服务都由 `cman` 脚本调用，该脚本检查 `/etc/cluster.conf` 文件进行集群配置。

## GFS 2 服务脚本

启动 GFS 系统，你需要运行 `cman` 脚本启动所需的守护进程并实现你的配置。`cman` 脚本将运行 `csd` 以启动集群检测、`fenced` 用于隔离、`dlm_control` 用于集群管理 `dlm` 锁定以及 `cman` 用于集群管理。脚本将检查 `/etc/sysconfig/cluster` 文件中的任何 GFS 配置设置。你使用 `gfs2` 脚本挂载你的 GFS 2 文件系统。要关闭 GFS 文件系统服务，使用带有 `stop` 选项的 `cman` 脚本。

```
service cman start

service gfs2 start
```

`gfs2` 服务脚本根据 `/etc/fstab` 文件指定的路径挂载 GFS 文件系统。你需要在 `/etc/fstab` 中列出所有想要挂载的 GFS 文件系统条目。`stop` 选项将卸载文件系统。你使用 `cman_tool` 向集群添加或从集群中移除节点。

## 第 37 章：分布式网络文件系统 781

## 实现 GFS 2 文件系统

要建立一个 GFS 2 文件系统，你首先需要使用物理卷创建集群设备，并将它们组织成逻辑卷。你使用 CLVM（集群逻辑卷管理器）从物理分区设置逻辑卷（过去你使用卷管理器池来执行此操作）。然后，你可以在逻辑设备上安装 GFS 文件系统。CLVM 的工作方式类似于 LVM，使用相同的命令。它在分布式网络上运行，并要求 `clvm` 服务器正在运行。创建一个 `/etc/cluster.conf` 文件并设置你的配置。配置将包含如使用的节点、隔离方法以及使用的锁定方法等信息。详细信息请参阅 `cluster-conf` 手页。使用 `ccs_test` 工具测试配置。

```
ccs_test myfs
```
