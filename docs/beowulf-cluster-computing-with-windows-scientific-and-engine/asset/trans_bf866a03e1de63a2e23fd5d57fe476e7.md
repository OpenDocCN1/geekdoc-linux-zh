
不同所有者偏好其机器参与 Condor 资源池的设置。

当任务提交到 Condor 后，会创建一个任务 ClassAd。该 ClassAd 包含关于任务的各种属性，例如任务使用的内存量、要运行的程序名称、提交任务的用户以及提交时间。任务还可以指定对所运行机器的要求和偏好（或*排序*）。例如，你可能在寻找可用的最快浮点性能。你希望 Condor 根据浮点性能对可用机器进行排序。也许你只关心机器至少拥有 256 MB 的 RAM。或者，也许你会接受任何你能得到的机器！这些任务属性和要求被打包成一个任务 ClassAd。

Condor 充当“媒人”的角色，通过持续读取所有任务 ClassAd 和所有机器 ClassAd，对任务广告和机器广告进行匹配和排序。Condor 确保两个 ClassAd 中的要求都得到满足。

### ClassAd 的结构

ClassAd 是一组具有唯一名称的表达式的集合。每个命名表达式被称为*属性*。每个属性都有一个*属性名*和一个*属性值*。属性值可以是一个简单的整数、*字符串*或浮点值，例如：

```text
Memory = 512
OpSys = "LINUX"
NetworkLatency = 7.5
```

属性值也可以由一个逻辑表达式组成，该表达式的评估结果为 TRUE、FALSE 或 UNDEFINED。这些表达式中允许的语法和运算符类似于 C 或 Java，即使用 `==` 表示相等，`!=` 表示不相等，`&&` 表示逻辑与，`||` 表示逻辑或，等等。此外，ClassAd 表达式可以包含属性名称以引用其他属性的值。例如，考虑以下小型示例 ClassAd：

```text
MemoryInMegas = 512
MemoryInBytes = MemoryInMegas * 1024 * 1024
Cpus = 4

BigMachine = (MemoryInMegas > 256) && (Cpus >= 4)
VeryBigMachine = (MemoryInMegas > 512) && (Cpus >= 8)
FastMachine = BigMachine && SpeedRating
```

在此示例中，*BigMachine* 的评估结果为 TRUE，而 *VeryBigMachine* 的评估结果为 FALSE。但是，由于未指定属性 *SpeedRating*，*FastMachine* 的评估结果将为 UNDEFINED。

Condor 提供了*元运算符*，允许你通过测试操作数的类型和值来显式地与 UNDEFINED 值进行比较。如果两个操作数的类型和值都匹配，则这两个操作数被认为是*相同的*；`=?=` 用于元等于（即，是同）和 `!=!` 用于元不等于（即，不同同）。这些运算符总是返回 TRUE 或 FALSE，因此使 Condor 管理员能够在信息不完整的情况下指定明确策略。

ClassAd 语义和语法的完整描述记录在 Condor 手册中。

**匹配 ClassAds。** ClassAds 可以彼此匹配。这是 Condor 将任务与机器匹配的基本机制。图 14.1 显示了 Condor 中代表机器的 ClassAd 和另一个代表排队任务的 ClassAd。每个 ClassAd 都包含一个 `MyType` 属性，描述该广告代表的资源类型，以及一个 `TargetType` 属性。`TargetType` 指定匹配所需的资源类型。任务广告希望与机器广告匹配，反之亦然。

每个参与匹配的 ClassAd 都指定了**Requirements**（要求）和**Rank**（排序）属性。为了使两个 ClassAd 匹配，两个广告中的**Requirements**表达式必须都评估为 TRUE。匹配机制的一个重要组成部分在于，**Requirements**和**Rank**表达式不仅可以参考自身广告中的属性，还可以参考候选匹配广告中的属性。例如，图 14.1 中指定的任务广告的**Requirements**表达式引用了 `Arch`、`OpSys` 和 `Disk`，它们都是机器广告中找到的属性。

如果 Condor 找到多个满足**Requirements**指定约束的机器 ClassAd 会发生什么？这就是**Rank**表达式发挥作用的地方。**Rank**表达式指定了匹配的期望程度（数字越大表示匹配越好）。例如，图 14.1 中的任务广告指定了：

```text
Requirements = ((Arch=="INTEL" && OpSys=="WINNTS") && Disk > DiskUsage
Rank   = (Memory > 10000) * KFlp5
```

![](img/e2283ffaea56e577ac05056b4bb738fc_341_0.png)

**图 14.1**
Condor 中 ClassAds 的示例。

## 14.2 使用 Condor

有效使用 Condor 的道路很短。其基本原理可以快速且轻松地掌握。

### 14.2.1 使用 Condor 的路线图

使用 Condor 运行任务涉及以下步骤：

- **准备任务以无人值守方式运行。** 在 Condor 下运行的应用程序必须能够作为批处理任务执行。Condor 在后台无人值守地运行程序。在后台运行的程序将无法执行交互式输入和输出。Condor 可以将控制台输出（stdout 和 stderr）和键盘输入（stdin）重定向到文件及从文件读取。你应该创建包含程序输入所需正确按键的文件。你还应确保程序能正确使用这些文件。通常，提交到 Condor 的程序将是控制台模式程序，因为 `stdin` 和 `stdout`/`err` 可以被重定向。然而，基于 GUI 的程序也可以提交到 Condor，前提是它们不会阻塞等待鼠标/键盘输入。

- **选择 Condor 宇宙（Universe）。** Condor 提供五种运行时环境供选择。每种运行时环境被称为一个*Universe*。通常，你选择的 Universe 取决于你要求 Condor 运行的应用程序类型。总共有三个 MPI Universe：一个用于串行任务（Vanilla），一个用于并行 MPI 任务（MPI），还有一个用于元调度器（Scheduler）。第 14.2.4 节提供了有关这些 Universe 的更多信息。

- **创建提交描述文件。** 任务提交的详细信息在*提交描述*文件中定义。该文件包含关于任务的信息，例如要运行的可执行文件、使用的 Universe、用于 `stdin`、`stdout` 和 `stderr` 的文件、关于应运行该程序的机器的要求和偏好，以及任务完成时发送电子邮件的位置。你还可以告诉 Condor 运行程序多少次；使用不同的数据集多次运行同一程序很简单。

- **提交任务。** 使用 `condor_submit` 命令将程序提交到 Condor。

任务提交后，Condor 处理运行任务的各个方面。随后，你可以使用 `condor_q` 和 `condor_status` 命令监控任务的进度。你可以使用 `condor_prior` 修改 Condor 运行任务的顺序。如果需要，通过在使用提交时指定的日志文件，Condor 还可以记录任务生命周期中每个阶段所执行的操作。

当程序完成时，Condor 会通知所有者（通过电子邮件、用户指定的日志文件或两者兼有）退出状态，以及各种统计数据，包括使用的时间和执行的 I/O。你可以随时使用 `condor_rm` 从队列中移除任务。

### 14.2.2 提交任务

要将任务提交给 Condor 执行，你使用 `condor_submit` 命令。该命令接受提交描述文件的名称作为参数，该文件包含用于指导任务排队的命令和关键字。在提交描述文件中，你定义 Condor 执行任务所需的一切。可执行文件的名称、初始工作目录以及程序的命令行参数等项目都包含在提交描述文件中。`condor_submit` 命令根据这些信息创建一个任务 ClassAd，然后 Condor 对任务进行调度。

提交描述文件的内容在你使用 Condor 时可以节省大量时间。向 Condor 提交多次程序运行很容易。要在 500 个不同的输入数据集上运行同一程序 500 次，数据文件的排列方式使得每次运行读取其自己的输入，每次运行写入其自己的输出。每个单独的运行可以拥有自己的初始工作目录、`stdin`、`stdout`、`stderr`、命令行参数和 shell 环境。

以下示例说明了使用 Condor 的灵活性。我们假设提交的任务是串行任务，旨在用于拥有跨所有节点共享文件系统的集群。因此，所有任务都使用 Vanilla Universe，这是运行串行任务最简单的一种。其他 Condor Universe 将在后面探讨。

#### 示例 1

示例 1 是最简单的提交描述文件。它排队一个程序 `foo` 的副本供 Condor 执行。Condor 生成名为 `foo.log` 的日志文件。日志文件包含任务在 Condor 内运行期间相关的事件。当任务结束时，其退出条件记录在日志文件中。我们建议你始终拥有日志文件，以便了解你的任务发生了什么情况。提交描述文件中的 `queue` 语句告诉 Condor 使用迄今为止指定的所有信息创建任务 ClassAd 并将任务放入队列。以井号字符（#）开头的行是注释，会被 `condor_submit` 忽略。

```text
# Example 1 ; Simple submit file
universe = vanilla
executable = foo
log = foo.log
queue
```

#### 示例 2

示例 2 排队两个程序 `mathematica` 的副本。第一个副本在目录 `run.1` 中运行，第二个在目录 `run.2` 中运行。对于排队的两个副本，`stdin` 将是 `test.data`，`stdout` 将是 `loop.out`，`stderr` 将是 `loop.error`。将写入两组文件，因为文件分别写入其各自的目录。这是一种方便的方式来为大型 Condor 任务组组织数据。

```text
# Example 2: demonstrate use of multiple
# directories for data organization.
universe = vanilla
executable = mathematica
...
```
