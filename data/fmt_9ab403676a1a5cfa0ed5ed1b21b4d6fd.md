
#!/bin/sh

#PBS -l walltime=1:00:00

#PBS -l mem=400mb

#PBS -l ncpus=4

#PBS -j oe

```
```

cd `${HOME}/PBS/test`

mpirun -np 4 myprogram

```
然后，此脚本将使用 `qsub` 命令提交给 PBS。
让我们查看一下该脚本。第一行告知使用哪种 shell 来解释脚本。第 2-4 行是资源指令，指定了“资源列表” (`-l`) 的参数。

此脚本将使用 `qsub` 命令提交给 PBS。这些行指定了 `qsub` 选项的参数。注意所有 PBS 指令都以 `#PBS` 开头。这些行告诉 PBS 对您的作业做什么。

回到上面的例子，我们请求了 1 小时的墙钟时间、400 MB 内存和 4 个 CPU。第五行是请求 PBS 将 stdout 和 stderr 流合并到单个文件中。最后两行是用户想要的命令：进入特定目录，然后执行名为 `myprogram` 的程序。
作业可以通过两种方式创建：使用文本编辑器或使用 PBS 图形界面（见下文）。

### 16.2.2 提交 PBS 作业

提交作业到 PBS 的命令是 `qsub`。例如，假设您创建一个名为 `myscriptfile` 的文件。以下示例显示了如何提交作业：

```
% qsub myscriptfile

12322.sol
```

示例中的第二行是 Server 返回的作业标识符。可以使用此唯一标识符对该作业进行操作（在运行完成之前）。本章下一节将讨论如何使用此“作业 ID”。

`qsub` 命令有很多可以在命令行或脚本指定的选项。注意，命令行选项将覆盖脚本中的相同选项。表 16.1 列出了常用的 `qsub` 选项。请参考《PBS 用户指南》获取完整列表和完整描述。

| 选项 | 目的 |
| :--- | :--- |
| -l | 作业所需的资源 |
| -q | 提交到的队列 |
| -N | 作业名称 |
| -S | 执行作业脚本的 shell |
| -p | 作业优先级值 |
| -a | 在指定日期后延迟作业 |
| -j | 合并输出和错误文件 |
| -h | 对作业挂起 |

表 16.1 PBS 命令。

`-resource_list` 选项用于指定作业所需的资源。表 16.2 列出了在集群上运行的作业可用的所有资源。

### 16.2.3 获取 PBS 作业状态

一旦作业提交给 PBS，您可以使用 `qstat` 或 `xpb` 命令检查作业状态。如果您知道作业的标识符，可以显式地请求状态。注意，除非你有多个集群，否则只需指定作业标识符的序列部分：

```
% qstat 12322

Job id User Time Use S Queue

----------- ---------- --- ---- -

12322.sol myscriptfile jjones 00:06:39 R submit
```

## 第16章

| 资源 | 含义 |
|---|---|
| arch | 作业所需的系统架构 |
| cput | 作业中所有进程所需的 CPU 时间 |
| file | 单个文件最大磁盘空间需求 |
| mem | 需要的总 RAM 内存 |
| ncpus | 需要的 CPU（处理器）数量 |
| nice | 请求的 "nice" (Unix) 值 |
| nodes | 需要的节点数量和/类型 |
| pput | 每个进程所需的最大 CPU 时间 |
| pmem | 每个进程所需的最大内存 |
| wall time | 所需的总墙钟时间 |
| workset | 总磁盘空间需求 |

**表 16.2** PBS 资源。

如果你在不指定作业标识符的情况下运行 `qstat` 命令，你将获得所有正在队列中和运行中的作业状态。
用户经常会疑惑为什么他们的作业没有运行。你可以使用 `qstat` 的 `-s` 状态选项从 PBS 中查询此类信息，例如：

```
% qstat 12323

Job id Name User Time Us S Queue

12323.sol myscriptfile jjones 00:00:00 Q submit

Requested number of CPUs not currently available.
```

`qstat` 的一些选项可以改变显示的信息。《PBS 用户指南》提供了完整的列表。

## 16.2.4 PBS 命令摘要

到为止，我们已经看到了几个 PBS 用户命令。表 16.3 提供了所有 PBS 用户命令的快速参考。每个命令的详细信息可以在 PBS 手册页和《PBS 用户指南》中找到。

## 16.2.5 使用 PBS 图形用户界面

PBS 提供两个 GUI 接口：一个基于 TCL/TK 的 GUI（称为 xpbs）以及一个可选的基于 Web 的 GUI。
XPbs 提供了一个用户友好的点击式界面来执行 PBS 命令。要作为普通非特权用户运行 xpbs，请输入

PBS（可移植批处理系统）

| 命令 | 用途 |
| --- | --- |
| qalter | 修改作业 |
| qdel | 删除作业 |
| qhold | 锁定作业 |
| qmsg | 向作业发送消息 |
| qmove | 将作业移动到另一个队列 |
| qrls | 释放锁定的作业 |
| qrerun | 重新运行作业 |
| qselect | 选择特定的作业子集 |
| qsig | 向作业发送信号 |
| qstat | 显示作业状态 |
| qsub | 提交作业 |
| xpbs | PBS 命令的图形界面 (GUI) |

表 16.3
PBS 命令。

setenv DISPLAY your_workstation_name:0
xpbs

要运行 xpbs 并具有终止 PBS 服务器、停止和启动队列、或运行或重新运行作业的额外目的，请输入

xpbs -admin
```

请注意，你必须被识别为 PBS 操作员或管理员，额外的“-admin”功能才能生效。

可选的基于 Web 的用户界面可以通过几乎任何 Web 浏览器访问 xpbs 的所有功能。要访问它，只需在浏览器中输入你的 PBS 服务器主机的 URL 即可。其布局和用法与 xpbs 类似。详情请参阅《PBS 用户指南》。

## 16.2.6 PBS 应用程序接口

PBS 软件包的一部分是 PBS 接口库，或 IFL。该库提供了构建新 PBS 客户端的方法。任何服务请求都可以通过调用接口库来触发。用户可能希望构建一个能够检查自身状态的 PBS 作业或提交新作业，或者他们可能希望自定义作业状态而不是使用 `qstat` 命令。管理员可以使用接口库来构建新的控制命令。

IFL 提供了一个与每个 PBS 客户端命令对应的用户可调用函数。命令与 PBS 服务请求之间存在（大约）一对一对应关系。还提供了用于网络连接管理的额外例程。用户可调用例程声明在头文件 `PBS_ifl.h` 中。用户通过调用适当的库例程并传递所需的参数来请求批服务器的服务。这些参数与命令上的选项和操作数对应。用户必须确保参数符合正确的语法。每个函数在成功时返回零，失败时返回非零错误代码。这些错误代码可以在头文件 `PBS_error.h` 中找到。库例程将接受参数并构建相应的批请求。该请求将传递给服务器通信例程。（PBS API 在《PBS 外部参考规范》中有完整的文档说明。）

## 16.3 安装 PBS

PBS 支持广泛的配置。它可以被安装并用于控制单个系统上的作业，或在多个系统上进行作业负载均衡。它可以用于将集群或并行系统的节点分配给串行和并行作业。它还可以处理这些情况的混合。然而，本书的主题重点关注集群的推荐配置。《PBS 管理员指南》解释了其他配置。

当 PBS 安装在集群上时，每个执行主机上必须有一个 MOM 守护进程，服务器（Server）和调度器（Scheduler）应该安装在一个系统或前端系统中。

对于 Linux 集群，PBS 以流行的 RPM 格式（Red Hat 软件包管理器）打包。（其他系统的安装说明请参见《PBS 管理员指南》。）PBS RPM 包以单个 tar文件提供，包含：

- Postscript 和 PDF 格式的《PBS 管理员指南》

- Postscript 和 PDF 格式的《PBS 用户指南》

- 不同组件的 PBS RPM 包

- 安装文档

当安装 PBS 时，会创建一个子树。该子树的名称将反映版本和补丁级别。守护进程使用的名称是主机名。根据 IETF RFC 标准，该名称对于任何 IP 地址必须是完全限定且一致的。

## 16.4 配置 PBS

### 16.4.1 网络地址与 PBS

PBS 使用限定名称来识别作业及其位置。PBS 安装通过运行服务器的主机名识别。PBS（可移植批处理系统）

### 16.4.2 Qmgr 命令

PBS 管理命令 `qmgr` 提供了一个命令行界面。该命令从标准输入读取指令。每个指令的语法都会经过检查，并向服务器发送相应的请求。`qmgr` 指令采取以下形式之一：

```
command server [names] [attr value[...]]
command queue [names] [attr value[...]]
command node [names] [attr value[...]]
```

其中 command 是在对象上执行的命令。`qmgr` 命令列在表 16.4 中。

| 命令 | 解释 |

| --- | --- |

| active | 设置活动对象 |

| create | 创建新对象，适用于队列和节点 |

| delete | 删除现有对象（队列或节点） |

| set | 定义或更改对象的属性值 |

| unset | 清空对象的属性值 |

| list | 列出对象的当前属性和值 |

| print | 打印所有队列和服务器属性 |

表 16.4 qmgr 命令。

`qmgr` 的 `list` 或 `print` 子命令可以由普通用户执行。创建或删除队列需要 PBS 管理员权限。设置或取消服务器或队列属性需要 PBS 操作员或管理员权限。

以下是几个说明 `qmgr` 命令的示例。下面将详细解释其他 `qmgr` 命令及其完成的具体任务。

```
% qmgr
Qmgr: create node mars np=2,type=cluster
Qmgr: create node properties="inner,moonless"
Qmgr: set node mars properties = inner
Qmgr: set node properties += haslife
Qmgr: delete node mars
Qmgr: d n venus
```

可以缩写为最小无歧的形式（如示例中最后一行所示）。命令以换行符或分号结束。单行可以输入多个命令。命令可以通过在换行符前标记反斜杠来跨行扩展。

PBS: 移植式批处理系统

381

反斜杠。注释以井号符号开头并一直持续到行尾。qmgr 会忽略注释和空行。详细的用法和语法说明请参阅 qmgr 手页。

### 16.4.3 节点

作业在何何位置由调度器（Scheduler）与服务器（Server）之间的交互决定。这种交互受 PBS ‘nodes’文件内容以及你部署 PBS 的系统配置的影响。如果没有此节点列表，服务器将无法与 MOM（或多个 MOM）建立通信，且 MOM 将无法报告正在运行作业的信息，也无法在作业完成时通知服务器。在集群配置中，将作业分发到各个主机取决于调度器决定将所选作业放置在哪个主机上。

无论执行节点的类型如何，每个节点都必须在 PBS nodes 文件中向服务器定义（其默认位置为 `/usr/spool/PBS/server-priv/nodes`）。这是一个简单的文本文件，文件中每行指定一个节点的规范。

```
node_name[:ts] [attributes]
```

名称是节点的网络名称（主机名），不需要是完全限定的（事实上，它保持尽可能短）。名称后附加的可选 ':ts’ 表示这是一个分时共享节点（timeshares node）。

节点具有与其关联的属性。属性有三种：属性（property）、name=value 对以及 name.resource=value 对。

可以指定零或多个属性。属性无非一个字母数字字符串（第一个字符必须是字母），对 PBS 没有任何意义。属性用于将一类节点分组，以便分配给一系列作业。

在节点文件格式中，可以以 qsub 指令的形式指定任何合法的 node=value 对：`attribute.resource=value`。考虑以下示例：

```
NodeA resource_available.ncpus=3 max_running=1
```

表达式 `np=N` 可以 `resources_available.ncpus=N` 的简写，可以添加它来声明节点上的虚拟处理器（VP）数量。此语法指定一个数字字符串，例如 `np=4`。此表达式将允许该节点分配给一个作业 N 次或多次。如果为集群节点未指定 `np=N`，则假设它有一个 VP。

你可以通过两种方式之一编辑节点列表。如果服务器没有运行，你可以使用文本编辑器直接编辑节点文件。如果服务器正在运行，你应该使用 qmgr 来编辑节点列表。

行中的每项之间必须用空格分隔。项可以按顺序列出，但主机名必须始终在第一。如果第一个非空格字符是井号，则可以包含注释行。

以下是一个名为“planets”的集群可能的节点文件示例：

```
# 第一组节点是集群节点。
# 注意，提供属性是为了
# 在逻辑上将某些节点分组在一起。
# 最后一个节点是分时共享节点。

| mercury | inner moonless |
| venus | inner moonless np=1 |
| earth | inner np=1 |
| mars | inner np=2 |
| jupiter | outer np=18 |
| saturn | outer np=16 |
| uranus | outer np=14 |
| neptune | outer np=12 |
| pluto:ts | |
```

### 16.4.4 创建或添加节点

启动 pbs_server 之后，可以通过 qmgr 命令输入或更改节点列表：

```
create node node_name [attribute=value]
```

其中属性及其相关的可能值如表 16.5 所示。以下是通过 qmgr 设置节点属性的几个示例：

```
% qmgr
Qmgr: create node mars np=2,ntype=cluster
Qmgr: create node venus properties="inner,moon"
```

一旦创建了节点，可以使用以下 qmgr 语法修改其属性和/或特性：

```
set node node_name [attribute[+-]=value]
```

## PBS: 移植式批处理系统

| 属性 | 取值 |

| --- | --- |

| state properties | free, down, offline |

| resources_available.ncpus (np) | 任意字母数字字符串 |

| ntype | cluster, time-shared |

| resources_available | 虚拟处理器数量 > 0 |

| resources_assigned | 节点上可用资源列表 |

| max_running | 节点正在使用的资源列表 |

| max_user_run | 每个用户最大运行作业数 |

| max_group_run | 每个组最大运行作业数 |

| queue | 与节点关联的队列名称（如果有） |

| reservations | 节点上等待处理的保留列表 |

| comment | 通用注释 |

表 16.5

PBS 节点语法。

其中属性与 create 命令的相同，例如，

```
% qmgr
Qmgr: set node mars properties=inner
Qmgr: set node mars properties+=haslife
```

也可以通过 qmgr 删除节点，删除节点的语法如下例所示：

```
% qmgr
Qmgr: delete node mars
Qmgr: delete node pluto
```

注意，忙碌状态（busy state）是由执行守护进程 pbs_mom 在节点达到负载平均阈值时设置的。请参阅 MOM 配置中的 `max_load`。作业独占（job-exclusive）和作业共享（job-sharing）状态在作业完成时设置。

### 16.4.5 默认配置

MOM 的行为由配置文件控制。此节描述了 MOM 的配置。执行守护进程 MOM 的配置比服务器要少得多。

一个最小的配置文件应包含：

```
$logevent 0
$clienthost
```

## 16.4.6 配置 MOM

MOM 的行为由配置文件控制。此节描述了 MOM 的配置。执行守护进程 MOM 的配置比服务器要少得多。

一个最小的配置文件应包含：

```
$logevent 0
$clienthost
```

### 16.4.7 调度器配置

现在服务器和 MOM 都配置完毕，我们将注意力转向调度器。如之前所述，调度器负责实施关于运行哪些作业以及在哪些资源上运行的站点策略。此节讨论了典型集群的推荐配置。可调调度器参数的完整列表和详细说明见 PBS 管理手册。

PBS 调度器提供了多种调度策略。除了 FIFO 顺序外，它还可以以多种不同的方式对作业进行排序。它还可以根据用户和组优先级进行排序。队列按优先级排序，以确定考虑它们的顺序。在运行时，调度器配置为表 16.6 所示的默认值。

| 选项 | 默认值 |

| --- | --- |

| round_robin | False |

| by_queue | True |

| strict_fifo | False |

| load_balancing | False |

| load_balancing_rr | False |

| fair_share | False |
