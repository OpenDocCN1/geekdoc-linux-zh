

![](img/a0df85c2e542a8d6c913113908553aa4_747_0.png)

# 图 25-1：滚动升级流程

## 25.5.1.1 确定哪个集群成员将成为主成员

“主成员”被选为首先进行滚动的集群成员。通常，良好的做法是选择正在提供根文件系统、/usr 文件系统和 /var 文件系统的集群成员。以下提供了如何确定哪个集群成员正在提供这些文件系统的示例。

让我们找出哪个集群成员或系统正在提供 /、/usr 和 /var：

```
# cfsmgr / /usr /var
Domain or filesystem name = /
Server Name = molari
Server Status : OK

Domain or filesystem name = /usr
Server Name = molari
Server Status : OK

Domain or filesystem name = /var
Server Name = molari
Server Status : OK
```

或者，你可以使用我们的 cfs 脚本。

```
# cfs | grep -E "cluster_root|cluster_usr|cluster_var"
molari      /          cluster#root        AdvFS
molari      /usr        cluster_usr#usr     AdvFS
molari      /var        cluster_var#var     AdvFS
```

如果其中一个或多个文件系统（/、/usr 或 /var）正在由另一个集群成员提供，你可以使用 cfsmgr 命令轻松地重新定位此文件系统。

```
# cfsmgr /var
Domain or filesystem name = /var
Server Name = sheridan
Server Status : OK
```

```
# cfsmgr -h sheridan -r -a SERVER=molari /var
```

```
# cfsmgr /var
Domain or filesystem name = /var
Server Name = molari
Server Status : OK
```

其他集群成员的系统固件。有关安装系统固件的更多信息，请参阅第 5 章 安装 Tru64 UNIX。

# 警告：

KGPSA 主机总线适配器的固件升级可能会更改光纤通道（FC）节点名称。

在制作本章所需的测试过程中，我们遇到了一个问题以及来自 HP 支持的警告，这与升级 KGPSA 上的固件有关。

升级 KGPSA 上的固件可能会更改 FC 节点名称。“此升级不能掉以轻心，因为 FC 节点名称的更改会改变 Tru64 UNIX 平台上 HSG80 上的连接状态。”如果集群的存储系统“正在使用选择性存储呈现（将条目设置到 Access_Enable 表中），那么所有这些新连接都必须重命名，并且旧连接将被删除。”³

以下是这些连接更改的示例以及如何纠正它们：

- KGPSA 固件升级前 SHOW CONNECTION：

```
BLS-HSG1> SHOW CONNECTION
Name        Operating system   Controller   Port   Address   Status   Offset
MOLARI1B01  TRU64_UNIX         THIS         2      000008    OL this  00
HOST_ID=1000-0000-C921-92C9          ADAPTER_ID=1000-0000-C921-92C9
MOLARI1A01  TRU64_UNIX         THIS         2      000002    OL this  00
HOST_ID=1000-0000-C921-93B0          ADAPTER_ID=1000-0000-C921-93B0
```

- 固件升级后 SHOW CONNECTION：

```
BLS-HSG1> SHOW CONNECTION
Name        Operating system   Controller   Port   Address   Status   Offset
INEWCON02   WINNT              THIS         2      000008    OL this  00
HOST_ID=2000-0000-C921-92C9          ADAPTER_ID=1000-0000-C921-92C9
INEWCON03   WINNT              THIS         2      000002    OL this  00
HOST_ID=2000-0000-C921-93B0          ADAPTER_ID=1000-0000-C921-93B0
MOLARI1B01  TRU64_UNIX         THIS         2      000008    Offline  00
HOST_ID=1000-0000-C921-92C9          ADAPTER_ID=1000-0000-C921-92C9
MOLARI1A01  TRU64_UNIX         THIS         2      000002    Offline  00
HOST_ID=1000-0000-C921-93B0          ADAPTER_ID=1000-0000-C921-93B0
```

> ³ Compaq Support Blitz TD 2807-C。

请注意，两个新连接 !NEWCON02 和 !NEWCON03 是出现在 MOLARI1B01 和 MOLARI1A01 中的相同 KGPSA 适配器，但固件升级已更改了连接上的光纤通道节点名称或 HOST_ID。系统的旧连接现在处于 OFFLINE 状态，系统无法访问使用选择性存储呈现⁴呈现的任何单元。在集群中，尤其是在滚动升级期间，这将不是一个非常理想的情况，但可以很容易地解决。

- 重新编辑连接条目后 SHOW CONNECTION：

![](img/a0df85c2e542a8d6c913113908553aa4_751_0.png)

请注意，旧连接 MOLARI1B01 和 MOLARI1A01 已被删除。新连接 !NEWCON02 被重命名为 MOLARI1B01，而 !NEWCON03 被重命名为 MOLARI1A01。

在我们继续之前关于固件的最后一点。如果你的集群中的任何系统具有 EISA 总线，而大多数基于 EV5 和 EV56 Alpha 的系统都有，你必须运行 EISA 配置实用程序（ECU）。ECU 是第三方软件，通常随你的系统硬件一起在软盘上提供。如果你没有当前的 ECU 软盘，请在开始滚动升级之前联系你的 HP 支持代表以获取替换副本。

## 25.5.1.4 确定集群是否已准备好升级

```
# clu_upgrade -v check setup 1
Retrieving cluster upgrade status
```

这会验证以下内容：

- 没有滚动升级正在进行中。
- 所有集群成员都在运行相同版本的 operating system 和集群软件。
- 没有集群成员在运行标记文件⁵。
- 有足够的可用磁盘空间来执行集群的滚动升级。

⁴ 有关选择性存储呈现的更多信息，我们将参考 Compaq StorageWorks 手册中关于 HSG80 控制器（ACS 手册）的部分。

⁵ 有关标记文件的更多信息，请参阅第 25.5.2.1 节。

