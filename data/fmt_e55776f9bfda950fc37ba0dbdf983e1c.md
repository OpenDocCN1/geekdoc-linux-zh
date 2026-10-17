
# 作业监控与管理

`condor_jobmonitor` 工具解析用户日志并可以使用图形化方式显示作业进度。图 14.2 显示可以使用 `condor_status` 命令定位所有运行由 `breach@cs.wisc.edu` 提交的作业的机器。

| 名称 (Name) | 操作系统 (OpSys) | 状态 (State) | 负载 (LoadAv) | 活动时间 (Time) |
|---|---|---|---|---|
| alfred.cs | ELUX | Claimed | 0.980 | 64 \| 0+07:10 |
| biron.cs | ELUX | Claimed | 1.000 | 128 \| 0+01:10 |
| cambridge.cs | ELUX | Claimed | 0.988 | 64 \| 0+00:15 |
| falcons.cs | ELUX | Claimed | 0.996 | 32 \| 0+02:05 |
| happy.cs | ELUX | Claimed | 0.988 | 128 \| 0+03:05 |
| istat03.st | ELUX | Claimed | 0.883 | 64 \| 0+06:45 |
| istat04.st | ELUX | Claimed | 0.988 | 64 \| 0+00:10 |
| istat09.st | ELUX | Claimed | 0.301 | 64 \| 0+03:45 |

要查找运行任何作业的机器，输入：

```
% condor_status -run
```

| 名称 (Name) | 架构 (Arch) | 操作系统 (OpSys) | 远程用户 (RemoteUser) | 客户端机器 (ClientMachine) |
|---|---|---|---|---|
| adrian.cs | | ELUX | 0.980 | hepcon@cs.wisc. | chevre.cs.wisc. |
| alfred.cs | | ELUX | 0.980 | breach@cs.wisc.edu | neufchatel.w |
| amul.cs | | ELUX | 1.000 | nice-user.condor@cs. | wvre.cs.wisc. |
| anfrom.cs | | ELUX | 1.023 | ashoks@jules.ncsa.ui | julesncaui |
| ananthrac.cs | | LIN | 0.285 | hecpon@cs.wisc | chevre.cs.wisc. |
| astro.cs | | ELUX | 1.000 | nice-user.condor@cs | chevre.cs.wisc. |
| aura.cs | | ELUX | 0.996 | nice-user.condor@cs | chevre.cs.wisc. |
| balder.cs | | ELUX | 1.000 | nice-user.condor@cs | chevre.cs.wisc. |
| bamba.cs | | ELUX | 1.574 | dmarino@cs.wisc.edu | riola.cs.wisc.e |
| bardolph.cs | | ELUX | 1.000 | nice-user.condor@cs | chevre.cs.wisc. |

## 从队列中移除作业

你可以随时使用 `condor_rm` 命令从队列中移除作业。如果正在移除的作业当前正在运行，该作业将被杀死且不创建检查点，其队列条目将被移除。以下示例显示了移除作业前后的作业队列。

```
% condor_q
-- froth.cs.wisc.edu : <128.105.74.33847> : froth.cs.wisc.edu
ID OWNER SUBMITTED RUNTIME ST PRI SIZE CMD
125.0 janeney 4/10 15:35 0+00:00 I -10 1.2
132.0 roman 4/11 16:57 0+00:00 R 0 1.4
2 个作业；1 空闲，1 运行中，0 保持

% condor_rm 132.0
Job 132.0 removed.

% condor_q
-- froth.cs.wisc.edu : <128.105.74.33847> : froth.cs.wisc.edu
ID OWNER SUBMITTED RUNTIME PRI SIZE CMD
125.0 jane 4/10 15:35 0+00:00 I -10 1.2
```

## 更改作业的优先级

除了分配给每个用户的优先级外，Condor 还提供了用户分配优先级的能力。作业的默认优先级为 0。这些优先级范围从 -20 到 +20，数值越大越好。可以使用 `condor_prio` 命令修改作业优先级。例如，要将作业优先级更改为 -15，输入：

```
% condor_q
-- froth.cs.wisc.edu : <128.105.74.33847> : froth.cs.wisc.edu
ID OWNER SUBMITTED RUNTIME PRI SIZE CMD
126.0 raman 4/11 15:06 0 0.3

% condor_prio -p -15 126.0
```

我们强调，这些作业优先级与 Condor 分配的用户优先级完全不同。作业优先级控制你的作业中哪一个下一个运行；对于你的作业是否在另一个用户的作业之前运行没有任何影响。

## 确定作业不运行的原因

特定作业可能由于多种原因而不运行。这些原因包括作业或机器限制、由于偏好导致的偏差、优先级不足以及 `condor_negotiator` 实现的防止抖动（thrashing）的抢占限制。许多此类原因可以使用 `condor_q` 的 `-analyze` 选项进行诊断。例如，用户 jbasney 提交的以下作业几天没有运行。

```
% condor_q 125.0 -analyze
-- froth.cs.wisc.edu : <128.105.74.33847> : froth.cs.wisc.edu

125.000: 运行分析总结。在 323 个资源提议中，
320 个不满足请求约束
0 个资源提议约束未满足此请求
0 个正在服务优先级相等或更高的客户
0 个正在服务更受青的客户
0 个无法抢占，因为抢占已被锁定
0 个可提供您的请求的服务

警告：请注意；
没有资源匹配请求约束
请检查下方的 Requirements 表达式：

Requirements = Arch == "INTEL" && OpSys == "IRIX6" &&
Disk >= ExecutableSize && VirtualMemory >= ImageSize
```

该作业的 `Requirements` 表达式指定了一个不存在的平台。因此，表达式始终评估为 `FALSE`（假）。虽然分析器可以诊断大多数常见问题，但在某些情况下，它无法可靠地检测到检测问题时所使用的瞬时性和局部性信息。分析器可能会报告有可用资源提供您的请求，但作业仍然不会运行。在大多数情况下，这种延迟是瞬时的，作业将在下一个协商周期内运行。

如果问题持续存在且分析器无法检测到该情况，作业可能会开始运行但立即终止并返回空闲状态。查看作业的 `SHADOW.LOG` 日志（在提交命令文件中指定）和 Condor 的 `SHADOW.LOG` 日志文件可能有助于追踪问题。如果原因不明，您应该联系您的系统管理员。

## 作业完成

当一个 Condor 作业完成时（通过正常手段或异常手段），Condor 将将其从作业队列中移除（因此，它将不再出现在 `condor_q` 的输出中），并将其插入作业历史文件。您可以使用 `condor_history` 命令检查作业历史文件。如果您在提交描述文件中指定了日志文件，则作业的退出状态将记录在那里。

默认情况下，Condor 在作业完成时会向您发送电子邮件消息。您可以使用 `condor_submit "notification"` 命令修改此行为。该消息将包含作业的退出状态，或者作业异常终止的通知。

## 14.2.4 提交不同类型的作业：替代宇宙（Universes）

Condor 中的 Universe（宇宙）定义了一个执行环境。Condor 在 Linux 上支持以下 Universe：

- Vanilla（原生）
- MPI
- PVM
- Globus
- Scheduler（调度器）
- Standard（标准）

Universe 属性在提交描述文件中指定。如果未指定 Universe，它将默认为 Standard。

### Vanilla Universe

Vanilla Universe 用于运行串行（非并行）作业。前一节提供的示例中 Condor 优先使用 Standard Universe 来提交串行作业，因为 Standard Universe 有几个非常有用的功能。然而，Standard Universe 对支持的串行作业类型有若干限制。相比之下，Vanilla Universe 没有这些限制。任何在 Condor 中运行的程序都会在 Vanilla Universe 中运行。二进制执行文件以及脚本都欢迎进入 Vanilla Universe。

典型的 Universe 作业依赖于提交机器和所有节点之间的共享文件系统，以便作业访问其数据。然而，如果没有共享文件系统，Condor 可以传输作业和执行机器所需的文件。更多信息请参见第 14.2.5 节。

### MPI Universe

MPI Universe 允许由 Condor 管理带有 MPI 的并行程序。要向 Condor 提交 MPI 程序，请指定并行作业中使用的节点数。在提交描述文件中使用 `machine_count` 属性，如下例：

```
# 为一个需要 8 个大内存节点的 MPI 作业的提交文件
universe = mpi
executable = my-parallel-job
requirements = Memory >= 512
machine_count = 8
queue
```

提交描述文件中的其他选项允许各种参数，供作业需求或执行文件跨不同节点使用。

到 2001 年底，Condor 期望您的 MPI 作业与配置了 `ch_p4` 设备的 MPICH MPI 实现链接（参见第 9.6.1 节）。然而，预计将支持不同的设备和 MPI 实现，因此请检查您特定版本 Condor 带的文档，获取有关您的作业应如何与 Condor MPI 链接的附加信息。

如果您的 Condor 池包含专用机器（即 Beowulf 集群节点）和乐观机器（即工作站），默认情况下，Condor 将 MPI 作业调度在专用资源上运行。

### PVM Universe

存在几种不同的并行编程范式。常见之一是“主/工作”（master/worker）或“任务池”安排。在主/工作程序模型中，一个节点充当并行应用的控制主，并向工作节点发送工作任务。工作节点进行一些计算并将结果传回主节点。主节点有一个待完成的任务池，并将任务分配给下一个可用的工作节点。

PVM Universe 允许使用为并行虚拟机（Parallel Virtual Machine）接口（参见第 11 章）编写的主/工作风格程序。Condor 在提交作业的机器上运行主程序，且不会抢占主程序。工作节点在可用时填充到 Condor 池中。

具体来说，在 PVM Universe 中，Condor 作为 PVM 守护进程资源管理器。每当 PVM 程序通过 `pvm_hosts()` 调用请求节点时，请求将转发给 Condor。Condor 在 Condor 池中找到一台机器并将其添加。如果机器需要离开，PVM 程序将通过正常的 PVM 机制通知，例如 `pvm_notify()` 调用。

PVM Universe 的独特之处在于提交到 Condor 的 PVM 作业可以通过动态添加和删除机器通过池利用专用机器和工作站。

编写处理 Condor 乐观环境的 PVM 程序是一项复杂的任务。为此，创建了 MW 框架。MW 是在 Condor 中制作主/工作风格应用程序的工具。更多信息请参见 `www.cs.wisc.edu/mw` 首页。

提交 PVM Universe 与提交 MPI Universe 类似，只是 `machine_count` 的语法不同。这里是一个简单的提交描述文件：

```
# Condor: 分布式作业调度器
# 要求 Condor 在启动作业前给我们一个节点，
# 我们最多使用 75 个节点。
universe = pvm
executable = master.exe
machine_count = 1..75
queue
```
