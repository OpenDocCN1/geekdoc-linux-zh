
# cfsmgr /usr /var

Domain or filename name = `/` `/`

Server Name = `molari`

Server Status : OK

Domain or filename name = `/usr`

Server Name = `molari`

Server Status : OK

Domain or filename name = `/var`

Server Name = `molari`

Server Status : OK

```
或者，你可以使用我们的 cfs 脚本。
```

# cfs | grep -E "cluster_root|cluster_usr|cluster_var"

`molari /usr cluster_root#root AdvFS`

`molari /usr cluster_usr#usr AdvFS`

`molari /var cluster_var#var AdvFS`

如果其中一个或多个文件系统（`/`、`/usr` 或 `/var`）是由另一个集群成员提供的，可以使用 `cfsmgr` 命令重新定位该文件系统。

```
# cfsmgr /var

Domain or filename name = /var

Server Name = sheridan

Server Status : OK
```

```
# cfsmgr -h sheridan -r -a SERVER=molari /var

Domain or filename name = /var

Server Name = molari

Server Status : OK
```

现在我们已经知道哪个系统是这些文件系统的服务器了，让我们确定集群中的哪个 memberid。

```
# hostname

molari
```

```
# sysconfig -q generic memberid

generic:

memberid = 1
```

或者你也可以使用 `hwmgr (8)` 命令：

```
# hwmgr -view cluster
```

| Member ID | State | Member Name |
| --- | --- | --- |
| 1 | UP | molari (localhost) |
| 2 | UP | Sheridan |

在我们的示例中，名为 `molari` 的系统（它也是集群 memberid 1）将作为滚动升级的主成员。

### 25.5.1.2 备份集群

通常情况下，系统管理的一个良好实践是，在对系统进行良好且可验证的备份之前，永远不要执行任何类型的重大维护。

### 注意（NOTE）：

我们注意到，虽然大多数系统管理员记得备份 `/usr` 和 `/var`，但大多数人忘记了每个集群成员的启动磁盘。在备份集群时，请始终记得备份每个集群成员的启动磁盘。

### 25.5.1.3 更新系统固件

新的 TruCluster Server 软件了 HP 最新系统固件更新中提供的最新功能。在新升级的 TruCluster Server 软件上运行集群之前，确保安装了最新的系统固件是非常关重要的。

何时需要升级系统固件？在实际运行新的 TruCluster Servers 之前的任何时候。为了尽可能地减少停机时间，对于集群成员，该节点的系统固件应该在安装阶段（Install Stage）早期升级。对于其他集群成员，每个节点的系统固件应在完成滚动阶段之前升级。关于如何恢复集群成员的启动磁盘，请参见第 22 章。

### 警告（WARNING）：

对 KGPSA 的固件升级可能会更改光通道（FC）节点名称。

在执行本章所需的测试期间，我们遇到了来自 HP 支持的关于升级 KGPSA 固件的问题。

升级 KGPSA 固件可能会更改 FC 节点名称。如果系统使用了“选择性存储呈现（Selective Storage Presentation）”，那么所有这些新连接都必须重命名旧连接。

以下是这些更改以及如何纠正它们的示例：

在 KGPSA 固件升级前：

- BL5-HSG1> SHOW CONNECTION |
| Name | Operating system | Controller | Port | Status | Offset |
|---|---|---|---|---|---|
| MOLARI1B01 | TR64_UNIX | THIS HOST_ID=1000-0000-C921-92C3 | 2 | OK | 0000000000 ADAPTER_ID=1000-0000-C921-92C9 |
| MOLARI1A01 | TR64_UNIX | THIS HOST_ID=1000-0000-C921-93B0 | 2 | OK | 0000000000 ADAPTER_ID=1000-0000-C921-93B0 |

在 KGPSA 固件升级后：

- BL5-HSG1> SHOW CONNECTION |
| Name | Operating system | Controller | Port | Status | Offset |
|---|---|---|---|---|---|
| NEWCON01 | WINNT | THIS HOST_ID=2000-0000-C921-92C3 | 2 | OK | 0000000000 ADAPTER_ID=1000-0000-C921-92C9 |
| NEWCON03 | WINNT | THIS HOST_ID=2000-0000-C921-93B0 | 2 | OK | 0000000000 ADAPTER_ID=1000-0000-C921-93B0 |
| MOLARI1B01 | TR64_UNIX | THIS HOST_ID=1000-0000-C921-92C9 | 2 | offline | 0000000000 |

请注意两个新连接：NEWCON02 和 NEWCON03，它们与 MOLARI1B01 和 MOLARI1A01 使用相同的 KGPSA 适配器，但固件升级更改了连接上的光纤节点名称（Fibre Channel Node Name）和 HOST_ID。系统连接现在处于离线（OFFLINE）状态，系统无法访问通过选择性存储呈现（Selective Storage Presentation）提供的任何单元。在集群中，特别是在滚动升级期间，这并不是理想的情况，但可以轻松解决。

- 重新编辑连接条目后执行 SHOW CONNECTION：

| 名称 | 操作系统 | 端口 | 地址 | 状态 | 偏移 |
| --- | --- | --- | --- | --- | --- |
| MOLARI1B01 | TRU64_UNIX | THIS | 2 | 000008 | OL this | 00 ADAPTER_ID=1000-0000-C921-92C9 |
| MOLARI1A01 | TRU64_UNIX | THIS | 2 | 000002 | OL this | 00 ADAPTER_ID=1000-0000-C921-93B0 |

注意，旧连接 MOLARI1B01 和 MOLARI1A01 已删除。新连接!NEWCON02 被重命名为 MOLARI1B01，NEWCON03 被重命名为 MOLARI1A01。

在继续之前最后说一点。如果你的集群中的任何系统具有 EISA 总线（大多数 EV5 和 EV56 Alpha 系统都具有），你必须运行 EISA 配置实用程序（ECU）。ECU 是第三方软件，通常随你的系统硬件以软盘的形式提供。如果你没有当前的 ECU 磁盘，请在开始滚动升级之前联系你的 HP 支持代表获取一份替换副本。

## 25.5.1.4 确定集群是否已准备好升级

```
# cl_upgrade -v check step 1

正在检索集群升级状态
```
