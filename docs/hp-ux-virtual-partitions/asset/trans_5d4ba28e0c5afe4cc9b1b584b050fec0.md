

- 打印机/绘图仪
- 文件系统
- 用户/组
- 主目录
- 电子邮件
- 备份

虽然关于无盘 NFS 以及该领域相对于分布式 HP-UX 的诸多改进可以讨论的内容很多，但从管理角度来看，关键点是 SAM 为无盘 NFS 管理提供了集中管理点。与无盘 NFS 管理相关的所有任务都可以通过 SAM 执行。

## 服务控制管理器（SCM）概述

SCM 允许您在多台系统上复制任务。传统上需要在许多系统上单独执行的任务，现在可以在由 SCM 管理的集群的多台系统上执行。

您可以将在单个系统上运行的命令或工具（如 **find** 或 **df** 命令）分发到多台系统上运行，并在 SCM 中收集结果以供审阅。

设计用于在多台系统上运行的更高级工具，例如 Ignite-UX，也可以使用 SCM 以相同的方式运行。

通过 SCM，可以将特定任务分配给特定个人，从而创建基于角色的环境。这消除了对系统 root 访问的需求，因为特定的管理活动被分配给特定节点上的特定用户。这些用户角色在为定义个人用户可以执行的任务时提供了极大的灵活性。

您可以定义组成 SCM 集群的系统。在 SCM 环境中，中央管理服务器（CMS）是执行管理的焦点。受管节点上的代理与 CMS 通信以执行管理功能。

SCM 包含在 11i 的应用介质中，并像其他应用程序一样通过软件分发器进行加载。

从 HP-UX 11i 应用程序 CD-ROM 加载 SCM 后，我们将运行名为 **mxsetup** 的程序来设置 SCM。与 SCM 相关的大多数程序都以“**mx**”开头，应用程序本身加载在 **/opt/mx** 中，而 SCM 数据仓库保存在 **/var/opt/mx** 中。

```
# mxsetup

Please enter the ServiceControl repository password

Please re-enter the ServiceControl repository password

Please enter a name for your Managed Cluster
(default name: ‘HP Managed Cluster’): servicecluster

Please enter the login name of the initial ServiceControl trusted user
martyp

Would you like mxsetup to backup the ServiceControl repository after
it has initially configured it?(Y/N) [Y]:

Please enter the file path where mxsetup will store the backup data
(default path: /var/opt/mx/data/scm.backup):
```

```
You have entered,

ServiceControl Managed Cluster Name : servicecluster
Initial ServiceControl trusted user : martyp
Backup the ServiceControl repository : Y
Backup file path : /var/opt/mx/data/scm.backup

Would you like to continue? (Y/N) [Y] : 
```

请输入 mxsetup 将备份数据存储的文件路径（默认路径：/var/opt/mx/data/scm.backup）：

```
You have entered,

ServiceControl Managed Cluster Name : servicecluster
Initial ServiceControl trusted user : martyp
Backup the ServiceControl repository : Y
Backup file path : /var/opt/mx/data/scm.backup

Would you like to continue? (Y/N) [Y] : 
```

=====================================================================
ServiceControl Manager 配置有 'B' 个任务，配置可能需要一段时间。

请等待 mxsetup 配置 ServiceControl 管理器...
=====================================================================
1: 创建代理仓库..
2: 将 ServiceControl 受管集群命名为 'servicecluster'........................ 完成
3: 配置 ServiceControl 守护进程............ 完成
4: 启动 ServiceControl 守护进程.............. 完成
5: 安装 AgentConfig....................... 完成
6: 初始化 ServiceControl...................... 完成
7: 添加工具 ..................................... 完成
8: 备份仓库........................ 完成
ServiceControl 管理器配置成功
详情请参阅 /var/opt/mx/logs/scmgr-setup.log。

要启动 ServiceControl 管理器：
- 设置 DISPLAY 环境变量
- 并输入 '/opt/mx/bin/scmgr'
#

设置完成后，您可以运行 **ps** 查看以 *mx* 开头的进程，以查看为运行 SCM 而启动的守护进程。

设置好 SCM 后，我们现在可以运行其图形界面 */opt/mx/bin/scmgr*，如图 11-52 所示：

![](img/eff8b9287a5f38c5adf538f24aacf29e_759_0.png)

图 11-52 *ServiceControl 管理器 scmgr* 屏幕

显示的四个图标是您在 SCM 中执行的任务的启动点，如下所述：

1. *节点组* 提供受管节点的组视图。显示节点组后，用户可以在选定的节点组上执行任务。
2. *节点视图* 提供所有受管节点的视图。这是您可以执行各种节点相关任务（如添加和删除节点）的起点。
3. *工具视图* 提供 SCM 工具的视图。
4. *用户视图* 提供属于 SCM 的 HP-UX 用户的视图。可信用户可以从该视图执行各种用户相关任务，例如添加或删除用户。

如果您的所有系统都是 11i，则无需在客户端上加载任何软件即可从中央 SCM 系统管理它们。如果您有 11.0 或 10.20 系统，则客户端系统需要额外软件。您可以从 docs.hp.com 获取*ServiceControl 管理器的规划、安装、配置和更新*文档，其中提供了安装所有 SCM 相关软件的程序。

要添加受管节点，您需进入 *操作 - 新建 - 节点...* 菜单项，然后选择要添加的节点。

在此菜单项下还有一个用于*用户和角色*的标签区域。在图 11-53 中，我们添加了具有*操作员*角色的用户 *martyp*：

![](img/eff8b9287a5f38c5adf538f24aacf29e_761_0.png)

图 11-53 为新节点上的用户选择*操作员*角色

在添加节点并将其分组，以及添加用户并定义其角色后，您就设置好了 SCM 管理环境。您可以使用预定义的用户工具，也可以添加自己的自定义工具。

图 11-54 显示了 SCM 中预定义的一些软件管理工具：

![](img/eff8b9287a5f38c5adf538f24aacf29e_762_0.png)

**图 11-54** **SCM 软件管理工具**

图 11-54 中显示的工具是软件管理的默认工具。您也可以定义和添加自己的工具。请注意图左侧显示的工具类别。

从图 11-54 所示的图形环境中，您可以启动 SCM 相关的工作。您也可以从命令行与 SCM 配合使用。表 11-3 列出了您可以在命令行中发出的一些常用 SCM 命令：

## 表 11-3 常用 SCM 命令

| 命令 | 描述 |
| --- | --- |
| mxauth | 在 SCM 中添加、删除或列出授权。 |
| mxexec | 运行 SCM 工具。 |
| mxngroup | 在 SCM 中添加、修改、删除或列出节点组。 |
| mxnode | 在 SCM 中添加、删除或列出节点。 |
| mxrepositoryrestore | 恢复 SCM 仓库。 |
| mxrepositorysave | 备份 SCM 仓库。 |
| mxrole | 列出或修改 SCM 角色。 |
| mxsetup | 设置或卸载 SCM 管理集群的中央管理服务器。 |
| mxtool | 在 SCM 中添加、修改、删除或列出工具。 |
| mxuser | 在 SCM 中添加、修改、删除或列出用户。 |

要查看 SCM 角色，请发出以下命令：

```
# mxrole -1t
```

| 名称 | 启用？ | 描述 |
| --- | --- | --- |
| role16 | true | 供 ServiceControl 管理员使用 |
| role15 | true | 供 ServiceControl 管理员使用 |
| role14 | true | 供 ServiceControl 管理员使用 |
| role13 | true | 供 ServiceControl 管理员使用 |
| role12 | true | 供 ServiceControl 管理员使用 |
| role11 | true | 供 ServiceControl 管理员使用 |
| role10 | true | 供 ServiceControl 管理员使用 |
| role9 | true | 供 ServiceControl 管理员使用 |
| role8 | true | 供 ServiceControl 管理员使用 |
| role7 | true | 供 ServiceControl 管理员使用 |
| role6 | true | 供 ServiceControl 管理员使用 |
| lvmadmin | true | 供 LVM 管理员使用的角色 |
| operator | true | 供操作员使用的只读角色 |
| webadmin | true | 供 WEB 服务器管理员使用的角色 |
| dbadmin | true | 供数据库管理员使用的角色 |
| Master Role | true | ServiceControl 主角色 |

```
#
```

