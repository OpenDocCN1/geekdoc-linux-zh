
在配置 HACMP 之前，必须正确配置网络。以下步骤显示了如何检查集群的网络配置。

1. 检查两个节点的网络接口上是否配置了 IP 地址。
2. 检查 `/etc/hosts` 文件是否包含所有 IP 地址条目，且这些标签被 HACMP 使用。
3. 使用 `host` 命令验证名称解析是否正常。如果有问题，请检查并修改 `/etc/hosts` 文件。
4. 检查串口网络连接。建议为 HACMP 存活检测提供辅助网络，以使 HACMP 故障检测更加可靠。更多信息请参阅 HACMP Administration Guide, SC23-4862-09。

### 配置共享磁盘

此要求专门针对 HACMP 共享磁盘配置。由于共享磁盘是 HACMP 设置中不可或缺的一部分，本节列出了设置共享磁盘资源所需的高级步骤。

以下是涉及 AIX 逻辑卷的一些术语：

- 卷组 `VG`
- 逻辑卷 `LV`
- 日志文件系统 `JFS`
- 文件系统 `FS`

执行以下步骤来设置共享磁盘资源：

1. 检查两个节点的网络接口上是否配置了 IP 地址。
2. 检查 `/etc/hosts` 文件是否包含所有 IP 地址条目...（此处后续省略）

#### 示例 8-4 导入卷组

导入卷组

在输入字段中输入或选择值。

在完成所有所需的更改后按 Enter 键。

```
[Entry Fields]
VOLUME GROUP name [db2vg] +
PHYSICAL VOLUME name [hdisk1]
Volume group MAJOR NUMBER [58] +
```

接下来，更改 VG 以便其在重新启动时不激活：

##### `smit vg`

选择 Set Characteristics of a Volume Group（设置卷组特性）→ Change a Volume Group（更改卷组）。然后选择 VOLUME GROUP 名称。在 Change a Volume Group（更改卷组）菜单中，将 Activate volume group AUTOMATICALLY（自动激活卷组）设置为 no（否）。

+ 7. 将 VG 移回服务节点。

将文件系统和 VG 移回 node1，以便下一步操作，在下一步中将在 node1 上创建一个 DB2 实例用户。

```
##### unmount /home/db2inst
# varyoffvg db2vg
```

在 node1 上运行以下命令：

```
# varyonvg db2vg
##### mount /home/db2inst
```

### 用户/组设置与 DB2 安装

现在共享磁盘已设置完毕，我们可以在共享磁盘上创建 DB2 实例和数据库。在 node1 上执行以下步骤：

+ 1. 为 DB2 实例创建组。

使用 `mkgroup` 命令创建组。

+ 2. 为 DB2 实例创建用户。

使用 `mkuser` 和 `passwd` 命令。

+ 3. 更改 FS（文件系统）和 LV（逻辑卷）的所有者。

+ 4. 安装 DB2 并设置许可证密钥。DB2 产品必须安装在两个节点的本地磁盘上。

+ 5. 创建 DB2 实例。

+ 6. 在共享文件系统中创建数据库。

+ 7. 将实例主目录故障转移到 node2。

卸载共享磁盘上的 FS 并在 node1 上对 VG 执行下线操作（`varyoff`）。

在 node2 上激活 VG 并挂载所有 FS。删除目录 `home/db2inst1/sqlib`，这使我们能够在 node2 上创建实例并进行其控制文件。

接下来，在 node2 上重复步骤 1 到 6。

### 准备应用程序服务器脚本

应用程序服务器由启动脚本和停止脚本组成。在本节中，我们将解释这些应用程序脚本中必须包含的内容。

+ 在脚本中，我们简单地重启 DB2 实例并激活数据库以运行崩溃恢复。

+ 企业服务器版 `ESE` 实例在实例主目录的 `sqllib` 子目录下有一个 `db2nodes.cfg` 文件。当在另一个节点上重启 DB2 实例时，该文件必须包含正确的主机和 IP 地址。DB2 单分区实例也有此文件。我们将在第 203 页的 8.5 节“`db2nodes.cfg` 文件的考虑因素”中详细详细介绍此主题。

+ 将数据库配置参数 `AUTORESTART` 设置为 ON。

当应用程序连接到数据库或数据库被激活时，数据库管理器会自动调用重启数据库实用程序。默认设置为 ON。

+ 在脚本中，我们必须停止所有访问共享磁盘的应用程序和进程，以确保节点能够成功释放共享磁盘。在 DB2 术中，这意味着 `force application all`（强制所有应用程序）、`deactivate all databases`（取消激活所有数据库）、`terminate`（终止停止后台进程）以及 `db2stop`（停止 dbbm/实例）。可能需要 `db2stop force` 和 `db2_kill` 等升级命令，以便应用程序在合理时间内断开连接。

DB2 ESE 包含了一个示例脚本，用于协助在热备节点或互接管节点中配置 HACMP 故障转移或恢复。脚本文件对于单节点（ESE 以外的）称为 `rc.db2pe.ee`，对于多节点称为 `rc.db2pe.ee`。它们位于 DB2 实例主目录下的 `samples/sqlib/hcmp` 子目录下。可以复制适当的文件并根据系统进行自定义。完成自定义并重命名后，将 `rc.db2pe.ee` 重命名为 `rc.db2pe`。例如，这些示例脚本设计为使用 `rc.db2pe db2inst1 start` 和 `rc.db2pe db2inst1 stop` 的语法进行调用。

有关 HACMP/ES 的更多信息，请参阅 DB2 9 手册《Data Recovery and High Availability Guide and Reference》，SC10-4228 中“Cluster Support for AIX”章节下的“HACMP 事件监控和用户定义事件”部分。该主题在 DB2 信息 Center 中同样可用。

```
http://publib.boulder.ibm.com/infocenter/db2lu/v9/index.jsp?topic=/com_ibm.db2.udb.admin.com/doc/c007500.htm
```

### 配置 HACMP

AIX `smitty` HACMP 配置接口。主要步骤如下：

+ 1. 将节点添加到 HACMP 集群
2. 添加服务 IP 标签/地址
3. 配置应用程序服务器
4. 添加资源组
5. 向资源组添加资源
6. 定义串行网络和串行网络设备
7. 验证并同步 HACMP 配置
8. HACMP 配置的基本验证

以下是每个步骤的扩展：

+ 1. 将节点添加到 HACMP 集群。

```
#smitty hacmp
```

在 HACMP for AIX 菜单中，选择 Initialization and Standard Configuration（初始化和标准配置）→ Add Nodes to an HACMP Cluster（向 HACMP 集群添加节点）。

在 Configure Nodes to a HACMP Cluster (standard) 菜单中，输入集群名称和新节点。

+ 2. 添加服务 IP 标签/地址

```
##### smitty hacmp
```

在 HACMP for AIX 菜单中，选择 Initialization and Standard Configuration（初始化和标准配置）→ Configure Resources to Highly Available（配置高可用资源）→ Add Service IP（添加服务 IP）。

在 Add Service IP 菜单中，输入 IP 标签和网络名称。

+ 3. 配置应用程序服务器

```
##### smitty hacmp
```

在 HACMP for AIX 菜单中，选择 Initialization and Standard Configuration（初始化和标准配置）→ Configure Resources to Highly Available（配置高可用资源）→ Add Application Server（添加应用程序服务器）。

在 Add Application Server 菜单中，输入服务器名称、启动和停止脚本的路径。

+ 4. 添加资源组

```
##### smitty hacmp
```

在 HACMP for AIX 菜单中，选择 Initialization and Standard Configuration（初始化和标准配置）→ Configure Cluster Groups（配置资源组）→ Add Resource Group（添加资源组）。

在 Add Resource Group 菜单中，输入资源组名称和参与节点。

+ 5. 向资源组添加资源

```
##### smitty hacmp
```
