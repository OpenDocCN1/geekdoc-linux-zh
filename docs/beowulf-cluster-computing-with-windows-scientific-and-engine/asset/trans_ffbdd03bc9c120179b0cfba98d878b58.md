

```
universe = vanilla
executable = mathematica
# Give some command line args, remap stdio
arguments = -solver matrix
input = test.data
output = loop.out
error = loop.error
log = loop.log

initialdir = run_1
queue
initialdir = run_2
queue
```

# 示例 3。

示例 3 的提交描述文件为程序 'foo' 的 150 次运行排入队列。此任务要求 Condor 在物理内存大于 128 MB 的机器上运行该程序，并且进一步要求该任务不被调度到特定节点上执行。在满足要求的机器中，任务优先选择当前可用于接受该任务的最快浮点运算节点运行。它还向 Condor 提示该任务运行时将使用多达 180 MB 的内存。程序每次运行都分配一个独立的进程号，从进程号 0 开始。提交描述文件中可以使用多个内置宏；其中一个就是 $(Process) 宏，Condor 会将其展开为该任务集群中的进程号。这使得程序的第一次运行的文件 'stdin'、'stdout' 和 'stderr' 分别对应 'in.0'、'out.0' 和 'err.0'，第二次运行对应 'in.1'、'out.1' 和 'err.1'，依此类推。单个日志文件将列出此任务集群中所有 150 个任务的运行事件。

```
# Example 3: Submit lots of runs and use the
# pre-defined $(Process) macro.
universe = vanilla
executable = foo
requirements = Memory > 128 && Machine != "server-node.cluster.edu"
rank = Kflops
image_size = 180

Error  = err.$(Process)
Input  = in.$(Process)
Output = out.$(Process)
Log = foo.log

queue 150
```

请注意，提交描述文件中的 **requirements**（要求）和 **rank**（排名）条目将转化为随后为该任务创建的 ClassAd 的要求和排名属性。这些是任意表达式，可以引用机器或 *任务* 的任何属性；有关 ClassAd 中要求和排名表达式的更多信息，请参见 14.1.2 节。

# 14.2.3 用户命令概述

一旦你向 Condor 提交了任务，就可以管理并监控它们的进度。表 14.1 列出了供 Condor 用户使用的几种命令，用于查看任务队列、检查池中节点的状态以及执行其他几项活动。这些命令大多数都有许多命令行选项；有关完整文档，请参阅 Condor 手册中的命令参考章节。为了从用户角度提供入门介绍，我们在此提供一个快速游览，展示其中几个命令的实际运行效果。

| 命令 | 描述 |
|---|---|
| condor_history | 查看截至当前已完成的 Condor 任务日志 |
| condor_hold | 将队列中的任务置于挂起状态 |
| condor_prio | 更改队列中任务的优先级 |
| condor_qedit | 修改先前提交任务的属性 |
| condor_q | 显示队列中任务的信息 |
| condor_release | 释放队列中处于挂起状态的任务 |
| condor_reschedule | 向中央管理器更新调度信息 |
| condor_rm | 从队列中移除任务 |
| condor_run | 将 shell 命令行作为 Condor 任务提交 |
| condor_status | 显示 Condor 池的状态 |
| condor_submit_dag | 在指定的 DAG 中管理和排入任务以实现任务间依赖关系 |
| condor_submit | 将任务排入队列以执行 |
| condor_userlog | 显示并汇总来自任务日志文件的任务统计信息 |

表 14.1
用户命令列表。

当任务被提交时，Condor 将尝试寻找资源来处理这些任务。可以通过使用 -submitters 选项的 **condor_status** 命令获取已提交任务的所有用户列表。此操作的一个示例输出类似于以下内容：

```
C:\>condor_status -submitters
```

| 名称 | 机器 | 正在运行 | 空闲任务 | 挂起任务 |
|---|---|---|---|---|
| ballard@cs.wisc.edu | bluebird.c | 0 | 11 | 0 |
| nice-user.condor@cs. | cardinal.c | 6 | 504 | 0 |
| wright@cs.wisc.edu | finch.cs.w | 1 | 1 | 0 |
| jbasney@cs.wisc.edu | perdita.c | 0 | 0 | 5 |

| | | 正在运行的任务 | 空闲任务 | 挂起任务 |
|---|---|---|---|---|
| ballard@cs.wisc.edu | | 0 | 11 | 0 |
| jbasney@cs.wisc.edu | | 0 | 0 | 5 |
| nice-user.condor@cs. | | 6 | 504 | 0 |
| wright@cs.wisc.edu | | 1 | 1 | 0 |
| 总计 | | 7 | 516 | 5 |

### 检查任务进度。

`condor_q` 命令显示队列中所有任务的状态。`condor_q` 输出的一个示例如下：

```
C:\>condor_q
-- Schedd: ug.cs.wisc.edu : <128.115.121.12:31302>
     ID     OWNER           SUBMITTED     RUN_TIME ST PRI SIZE CMD
55574.0     jane          6/23 11:33   4+03:35:28 R 0 25.7 seycplex m Seymour.d
55575.0     jane          6/23 11:44   0+03:24:50 R 0  25.8 seycplex peduo sey
83193.0     jane          3/28 15:11   48+15:50:55 R 0  17.5 cplexmp test1.mp
83196.0     jane          3/29 08:32  48+03:16:44 R 0  83.1 cplexmp test3.mps
83212.0     jane          4/13 16:31   41+18:44:40 R 0  39.7 cplexmp test2.mps
5 jobs; 0 idle, 5 running, 0 held
```

此输出包含关于排队任务的许多列信息。`ST` 列（代表状态）显示队列中当前任务的状态。状态列中的 `R` 表示任务正在运行。`I` 表示空闲。状态 `H` 是挂起状态。在挂起状态下，除非通过 `condor_release` 命令释放，否则任务不会被调度运行。报告的任务 `RUN_TIME` 是任务被分配到机器的时间，格式为天+小时+分钟+秒。

跟踪任务进度的另一种有用方法是通过用户日志。如果在你的提交文件中指定了 `log` 命令，可以通过查看日志文件来跟踪任务进度。各种事件（如执行开始、检查点、驱逐和终止）及其发生时间都会记录在文件中。以下是来自用户日志文件的一个示例片段：

```
000 (8135.000.000) 05/25 19:10:03 Job submitted from host: <128.105.146.14:1816> ...
001 (8135.000.000) 05/25 19:12:17 Job executing on host: <128.105.165.131:1026> ...
005 (8135.000.000) 05/25 19:13:06 Job terminated
(1) Normal termination (return value 0)
User 0 00:00:37, Sys 0 00:00:00 - Run Remote Usage
User 0 00:00:00, Sys 0 00:00:05 - Run Local Usage
User 0 00:00:37, Sys 0 00:00:05 - Total Remote Usage
User 0 00:00:00, Sys 0 00:00:05 - Total Local Usage
9624 - Run Bytes Sent By Job
7146159 - Run Bytes Received By Job
9624 - Total Bytes Sent By Job
7146159 - Total Bytes Received By Job
...
```

`condor_jobmonitor` 工具可以解析用户日志文件中的事件，并使用这些信息以图形方式显示任务的进度。图 14.2 包含 `condor_jobmonitor` 运行时的屏幕截图。

你可以使用 `condor_status` 命令找到所有正在运行你任务的机器。例如，要找到所有正在运行由 `breach@cs.wisc.edu` 提交的任务的机器，请输入：

```
C:\>condor_status -constraint 'RemoteUser == "breach@cs.wisc.edu"'
```

| 名称 | 架构 | 操作系统 | 状态 | 活动 | 负载平均值 | 内存 | 活动时间 |
| --- | --- | --- | --- | --- | --- | --- | --- |
| alfred.cs | INTEL | LINUX | 已认领 | 忙碌 | 0.980 | 64 | 0+07:10:02 |
| biron.cs.w | INTEL | LINUX | 已认领 | 忙碌 | 1.000 | 128 | 0+01:10:00 |
| cambridge.cs | INTEL | LINUX | 已认领 | 忙碌 | 0.988 | 64 | 0+00:15:00 |
| falcons.cs | INTEL | LINUX | 已认领 | 忙碌 | 0.996 | 32 | 0+02:05:03 |
| happy.cs.w | INTEL | LINUX | 已认领 | 忙碌 | 0.988 | 128 | 0+02:05:00 |
| istat03.st | INTEL | LINUX | 已认领 | 忙碌 | 0.883 | 64 | 0+06:45:01 |
| istat04.st | INTEL | LINUX | 已认领 | 忙碌 | 0.988 | 64 | 0+00:10:00 |
| istat09.st | INTEL | LINUX | 已认领 | 忙碌 | 0.301 | 64 | 0+03:45:00 |
| ... | | | | | | | |

要找到所有正在运行任何任务的机器，请输入：

```
C:\>condor_status -run
```

| 名称 | 架构 | 操作系统 | 负载平均值 | 远程用户 | 客户端机器 |
| --- | --- | --- | --- | --- | --- |
| adriana.cs | INTEL | LINUX | 0.980 | breach@cs.wisc.edu | chevre.cs.wisc. |
| alfred.cs | INTEL | LINUX | 0.980 | breach@cs.wisc.edu | neufchatel.cs.w |
| amul.cs.wi | INTEL | LINUX | 1.000 | nice-user.condor.cs | chevre.cs.wisc. |
| anfrom.cs | INTEL | LINUX | 1.023 | ashoek@jules.ncsa.ui | jules.ncsa.uiuc |
| anthrax.cs | INTEL | LINUX | 0.285 | hepcron@cs.wisc.edu | chevre.cs.wisc. |

