
# 第 7 章 安全资源分区

## 配置 PRM 处理器集

|  |  |  |  |  |  |  |  |  |  |
|---|---|---|---|---|---|---|---|---|---|
| `payroll_db` | `zoo21` (vPar) |  | 是 (Psets) | 否 | 否 | 否 |  |  |  |
| `finance_db` | `zoo19` (vPar) | 4 | 是 (FSS) | 否 | 是 (60%) | 是 (80%) | 60% | 是 |  |
| `sales_db` | `zoo19` (vPar) |  | 是 (FSS) | 否 | 是 (40%) | 是 (60%) | 40% | 是 |  |

配置 PRM 软件的第一步是确保软件已正确安装。PRM 软件封装在 HP-UX 11 企业操作系统环境中。以下命令显示了构成 PRM 软件的产品。这三个组件

PRM 的组成包括内核基础设施、PRM 用户级库以及实际的 PRM 产品。可以使用以下命令验证软件是否已安装：

```
# swlist -l product | grep "Process Resource Manager"
PRM-Sw-Krn C.01.01 Process Resource Manager PRM-Sw-Krn product
PRM-Sw-Lib C.02.02 Process Resource Manager PRM-Sw-Lib product Proc-Resrc-Mgr Product
```

在验证 PRM 软件已正确安装后，可以启动 PRM 配置过程。PRM 允许直接编辑配置文件或通过图形用户界面 (GUI) 进行编辑。在本文整个场景中，将使用 PRM GUI 来创建配置文件。配置过程完成后，将显示生成的配置文件。

PRM GUI 位于 `/opt/prm/bin/xm`。初始 PRM 界面如图 7-3 所示。左侧显示系统名称，默认配置文件为：

![](img/fd7e17168a916afa5a44c7402dd35df2_183_0.png)

**图 7-3** 显示在右上角的 PRM 图形配置工具。注意，配置文件的状态显示其当前未加载。在右下角，列出了每个 PRM 管理器及其相应的状态值。

为了创建所需的配置，请选择默认配置文件 `/etc/prconf`。选择 Action（操作）菜单并选择 Edit（编辑）菜单。这将打开一个用于配置 PRM 组的表单编辑器，如图 7-4 所示。

要创建的第一个 PRM 组是 `hr_db`。该组将在 VPar 中分配三个 CPU。要创建该组，请在 Group（组）字段中指定名称。勾选 PSET 复框。最后，在 Number of CPUs（CPU 数量）字段中指定三个 CPU。按 Add（添加）按钮将 PRM 组添加到配置中。

第二个 PRM 组是 `payroll_db`。如表 7-1 所示，`zoo21` VPar 中四个 CPU。其中三个 CPU 已分配给 `hr_db` PRSET 组。因此，有一个处理器留在了默认 PSET 中，而 PSET 必须始终至少有一个处理器。实际上，PRM 组的配置可以在此处停止，因为 `hr_db` PRM 组将在默认 PSET 中运行。实际上，位于 3 个 CPU 和 `payroll_db` 实例将被限制在默认 PSET 中的单个处理器上。然而，`payroll_db` 组将与系统的所有其他进程（包括登录 shell、`cron` 任务和系统守护进程）竞争。为了确保

![](img/fd7e17168a916afa5a44c7402dd35df2_184_0.png)

**图 7-4** 安全资源分区配置编辑器

`payroll_db` 在默认 PRM 组中获得大部分 CPU 资源，将在默认 PSET 内创建一个公平调度器组。`payroll_db` FSS 组将分配默认 PSET 中 90% 的 CPU 资源。这是通过在 Group 字段中指定名称并在 Shares（份额）字段中指定值 900 实现的。接下来，为 `OTHERS` 组分配 100 个份额。这创建了对 `payroll_db` 组的 90% 分配；剩余的 10% 用于系统的所有其他进程。

最后的 PRM 组配置如图 7-5 所示。注意，`hr_db` 组拥有系统 75% 的资源，包含三个 CPU。`payroll_db` 组被分配了系统 22.5% 的资源，`OTHERS` 组被分配了系统 2.5%。`payroll_db` 和 `OTHERS` 组共享默认 PSET。`PRM_SYS` 组未在配置中显式列出，但 PRM 软件会自动创建该组。`PRM_SYS` 组将接收所需的资源；`PRM_SYS` 组中进程的实际利用率通常较低。

完成 PRM 组和 CPU 配置后，必须指定 PRM 应用。PRM 应用管理器使用应用程序组来确定应该与哪些组进程关联。要配置 PRM 应用，请选择 PRM 配置编辑器中的 Applications（应用程序）选项卡，如图 7-6 所示。对于每个 PRM 组，都定义了一个应用程序记录。应用程序记录由指向可执行文件的完整路径组成

```
zoo21.fc.home:/etc/prmconf
Applications  Disk Bandwidth  Group/CPU  Memory  Users
Group  Shares  Percentage  Number of CPUs  CPU IDs
PRM Groups
  OTHERS  |  100  |           
  hr_db  |  75  |  3 (Select at runtime)
  payroll_db  | 900  |  22.5

Group:
nPset:
Shares:
Number of CPUs:
CPU IDs:

Advanced CPU Selection
```

**图 7-5** 最终的 PRM 组配置

![](img/fd7e17168a916afa5a44c7402dd35df2_186_0.png)

**图 7-6** PRM 安全资源分区应用程序

到可执行文件的路径、与应用程序关联的组，以及一组备用名称。备用名称列表对于 Oracle 数据库等应用程序特别重要，因为数据库在启动时根据 `ORACLE_SID` 环境变量进行重命名。当 PRM 管理器将进程分配到 PRM 组时，会对备用名称进行检查，以确保备用名称是应用程序字段中指定的可执行文件。要配置应用程序区域，在 Application 字段中指定可执行文件的绝对路径。应用程序文件名部分允许通配符字符。当通用目录中的所有可执行文件都关联到特定的 PRM 组时，这非常有用。使用 Group 字段选择如图 7-5 所示的 PRM 组。最后，在 Alternate Name 字段中指定备用名称。这些步骤适用于 `hr_db` 和 `payroll_db` 实例。

现在 PRM 配置完成，但文件尚未保存。如果你点击 7-6 所示对话框上的 OK 按钮，应用程序将返回如图 7-3 所示的原始 PRM 界面。配置状态将为未加载，Modified 字段将指示为。通过选择 Action 菜单并选择 Save 项保存 PRM 配置。

保存 PRM 配置后，可以使用 `prmlist` 命令从命令行查看，或使用文本编辑器直接查看配置文件。列表 7-1 显示了 `prmlist` 命令的输出。

**列表 7-1** 使用 `prmlist` 的 PRM 配置
