
> 注意：必要时，请参阅你的 X Window System 文档以获取有关完成此过程的更多信息。根据你所使用的 X 软件，你可能需要以不同的顺序完成任务。

1. 启动 X Window System 软件。
2. 配置 X Window System 软件的安全设置，以允许远程主机在本地系统上显示 X 应用程序。
3. 连接到你想要安装软件的远程系统，以 Oracle Grid Infrastructure 客户端软件所有者（`grid`, `oracle`）的身份登录，并在系统中启动终端会话；例如，一个终端（`xterm`）。
4. 在远程系统上打开另一个终端，并以 `root` 用户身份登录远程系统，以便你可以在提示时以 `root` 身份运行脚本。

## 2.5 为 Oracle Grid Infrastructure 创建组、用户和路径

以 `root` 登录，并使用以下指令查找或创建 Oracle Grid Infrastructure 的 Oracle Inventory 组和软件所有者。

- 确定 Oracle Inventory 和 Oracle Inventory 组是否存在
- 如果不存在 Oracle Inventory，则创建 Oracle Inventory 组
- 创建 Oracle Infrastructure 用户
- 创建 Oracle Base 目录路径
- 创建作业角色分离的操作系统权限组和用户
- 创建标准组、用户和路径的示例
- 创建角色分配组、用户和路径的示例

> 注意：在安装 Oracle Grid Infrastructure 期间，会安装 Oracle Clusterware 和 Oracle 自动存储管理（Oracle ASM）。你不再可以拥有单独的 Oracle Cluster 安装所有者和 Oracle ASM 安装所有者。

### 2.5.1 确定 Oracle Inventory 和 组是否存在

当你首次在系统上安装 Oracle 软件时，OUI 会创建 `orainst.loc` 文件。该文件标识了 Inventory 组的名称（默认是 `oinstall`）以及 Oracle 中央清单（Central Inventory）的路径。`orainst.loc` 文件的内容类似于：

```
inventory_loc=central_inventory_location
inst_group=oinstall
```

在前面的示例中，`central_inventory_location` 是 Oracle 中央清单的位置，而 `group` 是具有向中央清单写入权限的组名（OINSTALL 权限）。

如果你已有一个现有的 Oracle 中央清单，请确保在所有 Oracle 软件安装中都使用相同的 Oracle Inventory，并确保你打算用于安装的所有 Oracle 用户都具有写入该目录的权限。

要确定你的系统上是否存在 Oracle 中央清单目录 (`oraInventory`)：

输入以下命令：

```bash
# more /etc/orainst.loc
```

如果 `orainst.loc` 文件存在，该命令的输出与以下类似：

```
inventory_loc=/u01/app/oracle/oraInventory
inst_group=oinstall
```

在之前的输出示例中：

- `inventory_loc` 组显示了 Oracle Inventory 的位置。
- `inst_group` 参数显示了 Oracle Inventory 组的名称（在此示例中为 `oinstall`）。

使用命令 `grep groupname /etc/group` 来确认指定的组是否存在于系统上。例如：

```bash
$ grep oinstall /etc/group
oinstall:x:1000:grid,oracle
```

### 2.5.2 如果不存在 Oracle Inventory，则创建 Oracle Inventory 组

如果 `orainst.loc` 文件不存在，通过输入类似的命令来创建 Oracle Inventory 组：

```bash
# /usr/bin/groupadd -g 1000 oinstall
```

上述命令创建了清单组 `oinstall`，其组 ID 为 `1000`。Inventory 组的成员被授予向 Oracle 中央清单 (`oraInventory`) 的权限。

默认情况下，如果不存在 Inventory 组，安装程序会将 Oracle Grid Infrastructure for Cluster 软件安装所有者的主组列为 oraInventory 组。确保该组可以作为所有用户的主组。

> 注意：组 ID 和用户 ID 在集群中的所有节点上必须一致。检查并确保你要使用的组 ID 和用户 ID 在每个集群成员节点上可用，并确认每个 Oracle Grid Infrastructure for a Cluster 安装所有者的主组具有相同的名称和组 ID。

### 2.5.3 创建 Oracle Grid Infrastructure 用户

在以下情况下，你必须为 Oracle Grid Infrastructure 创建软件所有者：

- 如果 Oracle 软件所有者用户不存在；例如，如果这是首次安装；
- 如果 Oracle 软件所有者用户存在，但你想使用不同的操作系统、不同的组设置。
