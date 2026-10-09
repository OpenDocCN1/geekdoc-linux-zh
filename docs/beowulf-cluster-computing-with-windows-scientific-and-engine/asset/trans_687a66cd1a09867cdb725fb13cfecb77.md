
## cctypes

`cctypes` 命令展示了集群控制器（Cluster CoNTroller）所知晓的各种资源池以及它可以为特定资源请求考虑的功能。图 17.2 展示了 `cctypes` 命令的输出。请注意，存在几种不同的资源类型。

![](img/e2283ffaea56e577ac05056b4bb738fc_419_0.png)

**图 17.2**

cctypes 的输出。

- **ccusage**：`ccusage` 命令列出系统中的每个节点、其状态，以及（如果节点繁忙）正在使用它的用户 ID、关联的作业及其完成时间。图 17.3 展示了 `ccusage` 的输出。
- **ccs-submit 和 ccrm**：`ccs-submit` 命令允许用户向系统提交作业。带有有效 jobId 的 `ccrm` 命令允许用户移除他们提交的作业。图 17.4 展示了 `ccs-submit` 和 `ccrm` 的输出。

### 17.4.1 批处理文件语法

集群控制器（Cluster CoNTroller）的批处理文件语法实际上非常简单。用户必须指定四个字段：

- **rem ccs account**：当前，account 关键字必须设置为提交作业用户的 userid。否则，作业将被拒绝。此字段也是未来版本中计费功能的一个占位符，届时用户可能希望指定其所属组，以便为作业使用的时长进行计费。一个示例是 `rem ccs account = lifka`。
- **rem ccs nodes**：这是用户希望用于特定作业的节点或独立计算机的数量。请注意，这不一定等同于处理器数量。无论节点有多少个处理器，集群控制器（Cluster CoNTroller）都会分配节点。例如，如果您的集群拥有包含四个处理器的节点，您可以请求的最少节点数是一个，而最少处理器数是四个。一个示例是 `rem ccs nodes = 4`。
- **rem ccs minutes**：这是特定作业所需的分钟数。集群控制器（Cluster CoNTroller）按挂钟时间（wall-clock time）而非 CPU 时间进行调度。这是因为它支持交互式作业（下文将描述），用户在交互模式下运行作业时无法轻易衡量 CPU 时间，但可以通过观察墙上的时钟来了解其时间配额何时结束。
- **rem ccs type**：集群控制器（Cluster CoNTroller）支持批处理和交互式作业。如果您请求批处理作业（例如，`rem ccs type = batch`），调度器将在主节点上为您运行批处理文件，即您被分配的第一台节点。您提交的批处理文件中的任何内容都将在主节点上运行。这允许您将工作提交给系统稍后执行，例如在周末。如果您更喜欢登录到您被分配的节点并手动运行您的作业（例如进行调试工作），您可以请求交互式时间（例如，`rem ccs type = interactive`）。对于交互式作业，集群控制器（Cluster CoNTroller）为您提供对节点的访问权限，然后退出干预。当您请求的时间用完时，集群控制器（Cluster CoNTroller）将终止您的进程（包括到节点的 Telnet 会话）并释放资源供下一个作业使用。

除了这四个必选要求外，还有一个可选字段：

- **rem ccs requirements**：集群控制器（Cluster CoNTroller）支持异构资源调度。因此，如果您拥有多种类型的节点资源，您可以专门请求它们。`cctypes` 命令将显示您的集群可用的各种节点资源类型。请注意，如果您的所有节点都相同，则不需要此关键字。一个示例是 `rem ccs requirements = @development`。这被解释为 8 个具有名为“development”功能的节点。

所有集群控制器（Cluster CoNTroller）命令在 Windows 批处理文件（.bat 扩展名）中都以前缀 `rem ccs` 开头。当用户提交作业时，这些行会被解析和检查。

**JobSetup。** 批处理文件中的最后一项，位于集群控制器（Cluster CoNTroller）指令之后，是您希望在批处理中完成的具体工作。交互式作业读取集群控制器（Cluster CoNTroller）指令以分配必要的资源。批处理文件不会在节点上启动。批处理作业实际上在主节点上运行此批处理文件。图 17.5 中的示例展示了一个批处理文件，它通过两个不同的网络接口依次运行“Hello World”程序。

让我们逐行分析这个示例。命令：

```bash
set MPI_COMM=TCP
```

和

```bash
set MPI_COMM=VIA
```

告知 MPI/Pro 分别使用以太网或 Emulex CLAN 进行通信；两者都安装在康奈尔理论中心（Cornell Theory Center）的集群上。请注意，这是 MPI/Pro 特定的命令。

命令：

```bash
h:
```

从本地 c: 驱动器切换到共享驱动器。

命令：

```bash
cd h:\users\lifka
```

将用户（lifka）移动到其主目录。

命令：

```bash
call machinemaker
```

运行 CTC 开发的脚本，该脚本根据运行脚本的节点为 MPI 创建主机文件。

命令：

```bash
echo "TCP Run" > howdy.log
```

和

```bash
echo "VIA Run" >> howdy.log
```

向日志文件添加文本，说明即将开始特定的运行。最后一个命令：

```bash
mpirun -np 32 h:\users\lifka\howdy.exe >> howdy.log
```

运行 **howdy.exe** 程序并包含 32 个进程。这些行按照它们在图 17.5 中出现的顺序执行。

**运行并行作业。** 集群控制器（Cluster CoNTroller）与 MPI/Pro 紧密集成。MPI/Pro 能够使用集群控制器（Cluster CoNTroller）用于批处理作业启动的相同模拟（impersonation）机制。这意味着可以在批处理中运行 MPI/Pro 作业。康奈尔理论中心（Cornell Theory Center）正在与微软合作，提供标准的微软模拟机制，以便所有并行库和调度系统都能兼容。当然，在集群控制器（Cluster CoNTroller）下，所有并行库都可以交互式使用。

### 17.4.2 作业的生命周期

现在让我们通过一个典型用户体验的示例，演示向集群控制器（Cluster CoNTroller）提交作业的过程。在这个示例中，我们展示了在康奈尔理论中心（Cornell Theory Center）实际与集群控制器（Cluster CoNTroller）的交互。

假设您希望运行一个四节点的并行“Hello World”作业。

1.  确定您需要什么资源以及您希望请求什么。为此，您可以使用 **ccq**、**ccusage** 和 **cctypes** 来提供有关哪些节点可用以及当前正在运行和等待的信息。
2.  验证您所需的资源存在后，您可以设置批处理文件以请求这些资源。以下批处理文件请求 4 个“development”资源类型的节点，时长为 5 分钟。

```batch
C:\> Command Prompt\ C:\> l\>howdy.bat
rem ccs.mnodes = 4
rem ccs.account = lifka
rem ccs.minutes = 5
rem ccs.type = batch
rem ccs.requirements = @development
set MPI_COMM=TCP
h:
cd H:\Users\Lifka
call notify lifka@tc.cornell.edu "Job started"
call mpirunscheduler
echo "TCP Run" > howdy.log
mpirun -np 8 h:\users\lifka\howdy.exe >> howdy.log
echo "VIA Run" >> howdy.log
mpirun -np 8 h:\users\lifka\howdy.exe >> howdy.log
ccrelease
"howdy.bat": 16 lines, 426 characters.
```

3.  要将您的作业放入队列，您必须使用 ccssubmit，它与调度节点上的 JobManager 服务交互，为您排队作业。一旦作业成功排队，JobManager 会返回一个唯一的 job id。

![](img/e2283ffaea56e577ac05056b4bb738fc_425_0.png)

4.  也在调度节点上运行的调度器服务检查等待作业队列和可用资源，当有匹配时，通过运行在“主节点”上的 impersonator 服务启动作业，“主节点”是分配给作业的节点集中的第一个节点。impersonator 服务以您的身份为您运行通过 ccssubmit 提交的批处理脚本。
5.  当作业完成时，作为批处理文件的最后一行会发出 cc release。这告诉调度器服务启动清理。您随时可以使用 ccrm 命令取消正在运行的作业或移除已排队的作业。如果作业超过其时间限制，调度器将自动清除作业占用的资源。
6.  调度器服务通过从每个节点的全局域组中移除用户来移除用户对节点的访问，然后通过在每个节点上启动 nodemanager 服务来清除任何剩余的用户进程。在此期间，作业处于“清理状态”，如这里所示：

