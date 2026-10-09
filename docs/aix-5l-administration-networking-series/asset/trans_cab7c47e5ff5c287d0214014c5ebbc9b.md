
`dfsd` 运行于客户端并管理本地缓存，同时与 DFS 文件服务器同步缓存。客户端还会运行 `dfbind` 进程，该进程与 DCE 单元目录服务、安全服务以及 FLDB 进行交互，以将路径名称解析到具体的文件服务器。

- 聚合（Aggregates）类似于 UNIX 分区。每个聚合可以包含多个文件集（Filesets）。在 AIX 中，聚合是使用 `newaggr` 命令格式化为 DCE LFS 的逻辑卷。
- 文件集是在 DCE/DFS 下作为整体管理的相关文件和目录的集合。DCE 配额在文件集级别应用。每个文件集由文件集名称和 ID 号标识。文件集 ID 号是由两个逗号分隔的两个正整数。DFS 中的配额在文件集级别以 1K 为增量应用。文件集可以是读写（RW）、只读（RO）或备份类型。备份文件集是活动文件集的克隆（快照），用于备份目的。
- 本地文件系统（LFS）是一种基于日志的文件系统，支持 DFS 下的所有功能。这包括 DCE ACL、复制、配额以及每个聚合中的多个文件集。

## 安装与配置

本讨论假设您已经安装并配置了 DCE 服务（详见第 24 章）。最低要求，您需要一个 DCE 单元目录服务器（Cell Directory Server）、一个 DCE 安全服务器（Security Server）以及三个分布式时间服务器（Distributed Time Servers）。每个 DFS 客户端或服务器还必须配置为 DCE 客户端或服务器。如果看到消息“Cannot configure DFS components until a CDS clerk (cds_cl) is configured”（在配置 CDS 管理员 (cds_cl) 之前无法配置 DFS 组件），这是 DCE 未正常工作的第一个迹象。第 24 章涵盖了安装 DCE 和 DFS 文件集之前以及日常维护所需的重要细节和系统注意事项。除了之前表 15-1 中显示的一个或多个 DFS 文件集外，您还需要安装以下 DCE 客户端：

- `dce.client.rte`：DCE 客户端
- `dce.client.sm1`：DCE SMIT 客户端工具
- `dce.msg.en_US.client.rte`：DCE 基础类消息
- `dce.msg.en_US.client.sm1`：DCE SMIT 基础消息

安装所需的 DCE 和 DFS 文件集后，您可以通过调用 `mkdcserver` 快速路径（FastPath）使用 SMIT 来配置基础 DFS 服务器。虽然存在用于管理 DFS 的命令行工具，但它们的详细说明超出了本章的范围。大多数关于 DCE 和 DFS 的 AIX 在线文档都可以通过 SMIT 帮助或 SMIT 中的 F1 键访问。

在配置每项服务时，您偶尔会被提示输入 DCE 单元管理员密码。这应该是在您安装和配置基础 DCE 服务时设置的（请参阅第 24 章以获取帮助）。DFS 的 SMIT（或 SMITTY）面板组织成了一个菜单树层次结构。以下列表说明了本章中用于配置 DFS 的各种 SMIT 面板所对应的 SMIT 快速路径。

### 快速路径 - 面板菜单树

```text
none      # 系统管理
commo     # 通信应用程序和服务
dce       # DCE (分布式计算环境)
mkdce     # 配置 DCE/DFS
mkdcesrv  # 配置 DCE/DFS 服务器
mkdfsasm  # DFS (分布式文件服务) 系统控制机
mkdfsldb  # DFS 文件集数据库机
mkdfssrv  # DFS 文件服务器机
mkdfssrepv # DFS 文件集复制服务器机
mkdfsbkdb # DFS 备份数据库机
mkdcclient # 配置 DCE/DFS 客户端
dfsadmin  # DFS (分布式文件服务) 管理
dfifs     # 添加/删除 JFS 文件系统
dfscdrom  # 添加/删除 CDROM 文件系统
dfslas    # 添加/删除 NFS 聚合和文件集
mkdfsagg  # 从本机导出和创建聚合
mkdff     # 在本机的聚合上创建文件集
dfs_acl   # DFS LFS 目录和文件的 ACLs (访问控制列表)
dfsnfs    # NFS 到 DFS 认证网关管理
```

### 系统控制机 (System Control Machine)

首先要做的是配置一个或多个 SCM（系统控制机）。每个 SCM 将控制单元中的一个独立域。从 SMIT 菜单列表中选中“DFS (分布式文件服务) 系统控制机”，或使用快速路径 `mkdfsasm`。如果在此机器上尚未配置 DCE 客户端，则只需输入单元名称；输入该机器的主机名，选中 *Start Components And Clean Up At System Restart*（在系统重启时启动组件并清理）中的“是”，选中 *MASTER SECURITY*（主安全）服务器，选中 *Synchronize Clock*（同步时钟）中的“是”，并输入时间服务器的主机名。在验证单元管理员账户名称正确后，按 ENTER，并在提示时输入单元管理员密码。将与 `user` 和 `bosserver` 一起启动最小的 DCE 客户端。图 15-2 突出了以下 SMITTY 面板中所需的此重要信息：

```text
# smitty mkdfsasm
```

### 文件集数据库机 (Fileset Database Machine)

现在在同一台机器上配置文件集数据库 (FLDB)。多个 FLDB 可以提高可用性并分担客户端请求的工作负载，但对于初学者来说会带来重大的配置困扰。从 SMIT 菜单列表中选中 "DFS Fileset Database Machine"（DFS 文件集数据库机），或使用 `mkdfsldb` 快速路径。如果希望此机器维护自己的管理列表，DFS 系统 CONTROL 机器标识字段应保持空白。如果此机器被配置为 SCM，则此字段将被忽略。“用于管理文件集的组”是您可以添加其他组来管理此机器的地方，除了 `admin.lt.` 中列出的用于管理所有机器的主体和组。在验证单元管理员账户名称正确后，按 ENTER，并在提示时输入 cell_admin 密码。必要时，将与 `fileserv` 和 `bosserver` 一起启动最小的 DCE 客户端。以下 SMITTY 面板看起来与图 15-1 完全相同，只是底部多了两个字段。

```text
# smitty mkdfsfldb

DFS 文件集数据库机的快速路径
```

### 文件服务器机 (File Server Machine)

需要一个或多个 DFS 文件服务器来导出 DFS 聚合和文件集。从 SMIT 菜单列表中选中 DFS 文件服务器机选项，或使用快速路径 `mkdfssrv`。在验证信息和单元管理员账户名称正确后，按 ENTER，并在提示时输入单元管理员密码。必要时，将与 `fserver`、`fx4`、`dfsdind` 和 `bosserver` 一起启动最小的 DCE 客户端。您应该接受以下 SMITTY 面板（见图 15-2）中的所有默认设置：

```text
# smit mkdfssrv
    DFS 文件服务器机的快速路径
```

![](img/82f851021955589d82b22750fb3b1646_354_0.png)

**图 15-1. SMITTY DFS 系统控制机 (smitty mkdfscsm)**

### 启动 DFS 客户端

此时，您可能希望在本地机器上启动一个 DFS 客户端，以帮助验证您将要创建的以下文件集的结果。使用 SMIT 快速路径 `mkdcclient`，但如果该机器上已经运行基础 DCE 客户端，请为“要配置的客户端”选择 `dfs_cl`。在没有配置 DCE 客户端的远程 DFS 客户端机器上，您可以同时选择 `all_cl` 和 `dfs_cl`。使用以下命令，在提示时选择 Full（完整），然后参考图 15-3，并接受以下 SMITTY 面板中所有未高亮显示的默认值：

```text
# smitty mkdcclient                     到完整 DCE/DFS 客户端配置的快速路径
```

您现在应该能够使用以下 df 命令看到 DFS 共享根目录：

```text
# df /...
文件系统      512-块     空闲  使用%  inode使用数  inode使用%  挂载点
DFS          18000000 18000000   0%      0    0% /...
```

### 创建和导出聚合

创建一个聚合逻辑卷来容纳 LFS 文件。使用 `mklv` 命令在目标卷组中创建一个类型为 `lfs` 的逻辑卷。这种 lfs 类型...

![](img/82f851021955589d82b22750fb3b1646_356_0.png)

**图 15-3. SMITTY 完整 DCE/DFS 客户端配置 (smitty mkdcclient)**

