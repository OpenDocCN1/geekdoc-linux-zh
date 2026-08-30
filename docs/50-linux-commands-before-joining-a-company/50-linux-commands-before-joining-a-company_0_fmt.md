
# 入职前必学的 50+ Linux 命令

## 引言

Linux 及其变体（如 Ubuntu、RedHat、OpenSUSE 等）是当今大多数严肃开发者的首选开发环境。

此外，当你开发一个供客户使用的软件系统时，在不同的 Linux 变体上进行测试至关重要，关键在于流畅地使用 Linux 以进行广泛的协作。

本书将帮助你像专业开发人员一样使用 Linux。你可以瞬间融入任何开发者团队，并对使用你的计算系统感到从容。

我们涵盖了 50 多条命令，这将使你能够高效地使用 Linux 完成任何基础开发工作。所有命令都至关重要，并且都是通过分析顶尖公司的开发工作后挑选出来的。

我们涵盖的高级概念包括：

- 获取系统的硬件详情
- 获取系统的软件详情
- 高效地在后台运行和处理进程
- 处理文件系统
- 其他关键命令

在书的最后，我们提供了使用 Linux 的关键建议，这将清晰地让你成为一名“伟大的开发者”。

让我们直接从获取当前计算系统的详情开始。这很重要，因为你可以将这些详情与主工作（可能是应用程序或基准数据）一起分享，以确保其可现性。

## 获取系统详情

获取系统信息并正确记录它对于许多用例都至关重要。这允许人们重建相同的系统环境，从而在相同的流程中工作并获得相同的性能测量结果。这涉及硬件和软件详情。

在专业环境中工作时，通常需要对所做的每一次测量/实验跟踪系统详情。这是因为在后期，可以通过创建相同的环境来复制相同的性能。

我们系统配置的基本记录如下所示：

| 系统信息 | 值 |
| --- | --- |
| 属性 | 值 |
| Model | Intel(R) Xeon(R) Platinum 8180 CPU @ 2.50GHz |
| NUMA nodes | 4 |
| Sockets | 2 |
| Cores | 28 |
| Threads per socket | 2 |
| CPUs | 112 |
| Hyperthreading | OFF |
| Frequency | 2494.256 MHz |
| RAM | 512 GB |
| Rank | 2 |
| DIMMs | 4 |
| Clock Frequency | 4200 MHz |
| Clock Speed | 2133 MT/s |

| 软件信息 | 值 |
| --- | --- |
| 属性 | 值 |
| Kernel | Linux linux-mzys 4.4.162-94.72-default |
| GCC version | GCC (SUSE Linux) 6.2.1 20160826 |
| OS | OpenSUSE 12.3 (Dartmouth) |

我们将这一过程，以便你为自己的系统重建这些详情。强烈建议你在自己的系统中尝试这些命令。我们将从该过程开始。

### `lscpu` 命令

`lscpu` 命令通过读取两个文件提供有关 CPU 架构的信息：

- `sysfs`
- `/proc/cpuinfo`

输出是收集系统配置信息的第一步。该命令提供了某些用于高效运行进程的关键信息。其原理是存在用于控制进程执行的命令，我们在本书后后部分探讨了这些。

命令：

```bash
lscpu
```

我们将首先展示我们系统中的输出，以便你查看并分析。我们随后将解释背景知识并介绍该命令。它提供了多项信息，因此强烈建议你先自己仔细检查它。

```text
Architecture:           x86_64
CPU op-mode(s):         32-bit, 64-bit
Byte Order:             Little Endian
CPU(s):                 112
On-line CPU(s) list:    0-111
Thread(s) per core:     2
Core(s) per socket:     28
Socket(s):              2
NUMA node(s):           4
Vendor ID:              GenuineIntel
CPU family:             6
Model:                  85
Model name:             Intel(R) Xeon(R) Platinum 8180 CPU @ 2.50GHz
Stepping:               4
CPU MHz:                2494.256
BogoIPS:                4988.51
Virtualization:         VT-x
L1d cache:              32K
L1i cache:              32K
L2 cache:               1024K
L3 cache:               39424K
NUMA node0 CPU(s):      0,4,8,12,16,20,24,28,32,36,40,44,48,52,56,60,64,68,72,76,80,84,88,92,96,100,104,108
NUMA node1 CPU(s):      1,5,9,13,17,21,25,29,33,37,41,45,49,53,57,61,65,69,73,77,81,85,89,93,97,101,105,109
NUMA node2 CPU(s):      2,6,10,14,18,22,26,30,34,38,42,46,50,54,58,62,66,70,74,78,82,86,90,94,98,102,106
NUMA node3 CPU(s):      3,7,11,15,19,23,27,31,35,39,43,47,51,55,59,63,67,71,75,79,83,87,91,95,99,103,107,111
```

| 属性 | 值 |
| --- | --- |
| NUMA nodes | 4 |
| Sockets | 2 |
| Cores | 28 |
| Threads per socket | 2 |
| CPUs | 112 |
| Hyperthreading | OFF |
| Frequency | 2494.256 MHz |

你也必须记录你系统的这些细节。请在继续下一个命令之前执行此操作。

### `uname -a`

```bash
uname -a
```

`uname -a` 命令将提供内核名称。这非常重要，因为操作系统起着重要的作用。

在大多数基准测试设置中，测量是在不同的操作系统上进行的，因此，内核是一项关键信息。

命令：

```bash
uname -a
```

示例输出：

```text
Linux linux-mzys 4.4.162-94.72-default #1
SMP Mon Nov 12 18:57:45 UTC 2018 (9de753f)
x86_64 x86_64 x86_64 GNU/Linux
```

以下是我们的内核信息记录：

| 系统信息（`uname -a`） |
| --- |
| 属性 | 值 |
| 内核 | Linux linux-mzys 4.4.162-94.72-default |

### `sudo dmidecode`

```bash
sudo dmidecode
```

`sudo dmidecode` 命令提供了若干重要信息，例如桌面管理接口（DMI），并与系统管理 BIOS 相关。它提供了内存结构、系统组件、设备信息等。

我们将逐一调查它的部分内容，以便理解并快速获取相关信息。

#### 时钟频率

我们需要的第一个信息是时钟频率。我们可以通过对 `sudo dmidecode` 的输出使用 `grep MT` 来方便地获取此信息。`grep` 是一个 UNIX 工具，允许我们过滤文本。

```bash
sudo dmidecode | grep MT
```

输出：

```text
MTRR (Memory type range registers)
      Speed: 2133 MT/s
      Configured Clock Speed: 1067 MT/s
```

在此命令中，我们将使用 `grep DDR` 获取物理内存插槽：

```bash
sudo dmidecode | grep DDR
```

输出：

```text
Type: DDR4
```

要获取内存秩（Rank），使用如下 `grep Rank`：

```bash
sudo dmidecode | grep Rank
```

输出：

```text
Rank: 2
```

要获取时钟频率，使用以下命令：

```bash
sudo dmidecode | grep MHz
```

输出：

```text
External Clock: 100 MHz
Max Speed: 4200 MHz
Current Speed: 3400 MHz
```

要获取 DIMM 信息，使用以下命令：

```bash
sudo dmidecode | grep DIMM
```

输出：

```text
Form Factor: DIMM
Locator: DIMM 0
Form Factor: DIMM
Locator: DIMM 1
```

要获取系统内存/RAM：

```bash
sudo dmidecode | grep GB
```

输出：

```text
Maximum Capacity: 512 GB
Range Size: 128 GB
Range Size: 128 GB
Range Size: 128 GB
Range Size: 128 GB
```

因此，我们的系统有 512GB 的 RAM（随机访问存储器）。

基于此，这是我们系统的关键信息，应为所有用途进行记录：

| 系统信息（`dmidecode`） |
| --- |
| 属性 | 值 |
| RAM | 512 GB |
| Rank | 2 |
| DIMMs | 4 |
| Clock Frequency | 4200 MHz |
| Clock Speed | 2133 MT/s |

你应该尝试的其他 `dmidecode` 命令还有：

- `sudo dmidecode -s system-manufacturer`
- `sudo dmidecode | grep Product`
- `sudo dmidecode -s system-product-name`
- `sudo dmidecode | egrep -i 'manufacturer|product'`
- `sudo dmidecode | egrep -i 'vendor'`

这些命令提供了涉及你系统的制造商/供应商的重要信息等。

计算系统有几个关键组件，如处理器、主板等。以下是获取有关这些组件信息的 `dmidecode` 命令：

- `sudo dmidecode -t processor`（用于处理器）
- `sudo dmidecode -t system`
- `sudo dmidecode -t baseboard`
- `sudo dmidecode -t chassis`
- `sudo dmidecode -t bios`
- `sudo dmidecode -t cache`

你必须在你的系统上尝试上述命令，记录输出并仔细分析。

### `cat /proc/meminfo`

```bash
cat /proc/meminfo
```

`meminfo` 是 Linux 系统中的一个文件，存储与内存使用相关的信息。要获取你系统的内存统计，请使用此命令：

```bash
cat /proc/meminfo
```

输出：

```text
MemTotal:       394877600 kB
MemFree:         322057928 kB
MemAvailable:   391704744 kB
Buffers:         2735168 kB
Cached:         66592340 kB
SwapCached:      39408 kB
Active:         44374924 kB
Inactive:       25087292 kB
Active(anon):    89332 kB
Inactive(anon):  94996 kB
Active(file):    4428592 kB
Inactive(file):  2499296 kB
Unevictable:     80 kB
locked:          80 kB
SwapTotal:       1679260 kB
SwapFree:        1297158 kB
Dirty:           0 kB
Writeback:       0 kB
AnonPages:       98584 kB
Mapped:          73280 kB
Shmem:           49620 kB
Slab:            285368 kB
claimable:       2744528 kB
Sreclaim:        109160 kB
KernelStack:     20608 kB
PageTables:      7668 kB
NFS_Unstable:    0 kB
Bounce:          0 kB
WritebackTmp:    0 kB
CommitLimit:     21421806 kB
Committed_AS:    4248960 kB
VmallocTotal:    3435973867 kB
VmallocUsed:     0 kB
VmallocChunk:    0 kB
HardwareCorrupted: 0 kB
AnonHugePages:   32768 kB
HugePages_Total: 0 kB
HugePages_Free:  0 kB
HugePages_Rsvd:  0 kB
HugePages_Surp:  0 kB
Hugepagesize:    2048 kB
DirectMap4k:     669504 kB
DirectMap2M:     5038992 kB
DirectMap1G:     352321536 kB
```

这提供了很好的见解，你必须仔细分析。

### `gcc version`

```bash
gcc --version
```

`gcc --version` 命令用于获取 `gcc` 版本。这是一个重要信息，因为 `gcc` 在广泛范围内起着主要作用。

根据应用的情况，我们需要跟踪不同的信息。

命令：

```bash
gcc --version
```

输出：

```text
gcc (SUSE Linux) 6.2.1 20160826 [gcc-6-branch revision 239773]
Copyright (C) 2016 Free Software Foundation, Inc.
This is free software; see the source for copying conditions. There is NO warranty; not even for MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.
```

所以检测到的 GCC 是：GCC (SUSE Linux) 6.2.1 20160826。

### `lsb_release -a`

```bash
lsb_release -a
```

`lsb_release -a` 命令用于获取操作系统的细节。

命令：

```bash
lsb_release -a
```

输出：

```text
LSB Version:    n/a
Distributor ID: SUSE
Description:    openSUSE 12.3 (Dartmouth) (x86_64)
Release:        12.3
Codename:       n/a
```

通过此，我们获取操作系统 OpenSUSE 12.3 (Dartmouth)。

通过此，我们获得记录如下两个关键信息：

| 软件信息 |
| --- |
| 属性 | 值 |
| GCC version | GCC (SUSE Linux) 6.2.1 20160826 |
| OS | OpenSUSE 12.3 (Dartmouth) |

计算系统的系统和软件细节完整示例记录如下：

| 系统信息 |
| --- |
| 属性 | 值 |
| Model | Intel(R) Xeon(R) Platinum 8180 CPU @ 2.50GHz |
| NUMA nodes | 4 |
| Sockets | 2 |
| Cores | 28 |
| Threads per socket | 2 |
| CPUs | 112 |
| Hyperthreading | OFF |
| Frequency | 2494.256 MHz |
| RAM | 512 GB |
| Rank | 2 |
| DIMMs | 4 |
| Clock Frequency | 4200 MHz |
| Clock Speed | 2133 MT/s |

| 软件信息 |
| --- |
| 属性 | 值 |
| Kernel | Linux linux-mzys 4.4.162-94.72-default |
| GCC version | GCC (SUSE Linux) 6.2.1 20160826 |
| OS | OpenSUSE 12.3 (Dartmouth) |

你应该遵循这些命令，在你的系统上运行它们并制作你自己的系统和软件信息表。这很重要，因为你应该准备好在特定系统上运行软件的所有内容，以便其他程序员可以复制你的工作。

## 在后台运行进程



在后台运行进程意味着该进程不会占用屏幕，我们可以使用不同的命令继续处理它。进程将继续运行，输出可以出现在屏幕上，但它不会接受任何输入。我们稍后将其带回屏幕。

简而言之，语法是：

```bash
<command> &
```

注意，这并不意味着进程在关闭终端时会继续运行。

进程有两种类型，即：

- 后台进程
- 前台进程

其核心思想是：后台进程不会与 `screen` 会话的 `STDOUT` 和 `STDERR` 管道链接，而前台进程则与 `screen` 会话的 `STDOUT` 和 `STDERR` 管道链接。因此，如果后台进程在终端中产生输出，它会被打印出来。所以，如果一个进程不产生输出或者输出被重定向到文件，它是很有用的。

注意，后台和前台进程都与 `STDIN` 管道链接。因此，如果后台进程需要来自 `STDIN` 管道的输入，它会被挂起（hang），直到我们将其带回前台。

要让进程在后台运行，我们需要在命令后添加 `&`。

### 语法

```bash
command &
```

### 示例

```bash
python code.py &
```

它将输出如下内容：

```text
[1] 121378
```

`1` 是作业 ID（job id），`121378` 是进程 ID（process id）。

### 检查后台进程

我们可以通过以下方式检查处于后台的进程：

```bash
jobs
```

在我们的案例中输出如下：

```text
[1]-  Running             python code.py &
[2]+  Running             python opengenus.py &
```

第一个整数是随附提供的命令的 Job ID。例如，命令`python opengenus.py &`的 Job ID 为`2`。

我们可以使用 Job ID 来管理后台进程并执行若干操作，如：

- 将后台进程带回前台
- 杀死后台进程

### 将进程带回前台

要将进程带回前台，我们需要使用以下命令：

```bash
fg %<job_id>
```

### 示例

```bash
fg %2
```

这将进程`python opengenus.py &`带回前台。输出将如下：

```bash
(base) [opengenus@localhost Desktop]$ fg %2
python opengenus.py
```

如果你的代码正在等待输入，现在可以提供了。

### 让正在运行的进程进入后台

现在，如果你的进程已经在运行并且你想将其转到后台，可以按照以下步骤操作：

1. 按下 Control + Z
2. 使用`jobs`检查 job id：

```bash
jobs
```

3. 让作业进入后台：

```bash
bg %<job id>
```

进程将移动到后台。

如果你只按下 Control + Z，它会停止该进程，我们可以在`jobs`命令中看到：

```text
[1]   Running             python code.py &
[2]-  Running             python opengenus.py &
[3]+  Stopped             python code_2.py
```

现在，如果我们使用`bg`命令将 Job ID `3` 移动到后台，可以使用`jobs`命令检查影响。

```bash
bg %3
```

它将输出如下：

```text
[3]+ python code_2.py &
```

注意末尾的`&`符号。它表示该进程正在后台运行。

尝试`jobs`命令：

```bash
jobs
```

输出将如下：

```text
[1]   Running             python code.py &
[2]-  Running             python opengenus.py &
[3]+  Running             python code_2.py &
```

### 获取作业的进程 ID

我们可以使用`jobs`命令获取所有后台作业的进程 ID：

```bash
jobs -l
```

输出如下：

```text
[1] 121378 Running             python code.py &
[2]- 127536 Running             python opengenus.py &
[3]+ 12623 Running             python code_2.py &
```

注意，第一个数字（`1`、`2` 和 `3`）是 Job IDs，而第二个数字（如`121378`）是 Process ID。

### 杀死进程

杀死进程有两种方法：

- 直接使用进程 ID 杀死
- 将其带回前台并使用 Control + C 杀死

一旦我们获得了作业的进程 ID，就可以直接杀死它：

```bash
kill 121378
```

这将杀死第一个作业。它将输出如下：

```text
[1]  Terminated      code.py
```

我们可以使用`jobs`命令验证这一点：

```bash
jobs -l
```

输出为：

```text
[2]- 27536 Running             python opengenus.py &
[3]+ 2623 Running             python code_2.py &
```

注意第一个作业消失了。我们将使用第二种方法，将其带回前台并杀死，如下：

```bash
fg %3
(base) [opengenus@localhost Desktop]$ fg %3
python code.py
```

终端卡住了。如果我们按下 Control + C，进程将如下所示被终止：

```bash
(base) [opengenus@localhost Desktop]$ fg %3
python code.py
Traceback (most recent call):
  File "code.py", line 7, in <module>
    time.sleep(1)
KeyboardInterrupt
```

我们可以通过`jobs -l`命令验证此。输出为：

```text
[2]+ 27536 Running             python opengenus.py &
```

（注：原文末尾部分存在大量重复且混乱的快捷键表，根据要求已进行清理并保留核心结构）

### 安装 Screen

我们可以在 Ubuntu 等 Linux 版本安装 `screen`：

```bash
sudo apt-get install screen
```

对于其他系统如 RedHat (RHEL)，可以使用：

```bash
sudo yum install screen
```

### 启动 screen 会话

要启动 `screen` 会话，使用以下命令：

```bash
screen
```

这将打开一个新的会话。我们可以在此 `screen` 中工作并使用它提供的功能。

### 获取 screen 帮助

要获取 `screen` 应用的帮助，按顺序按下快捷键：Control + A 然后按 `?`。注意：为了使此操作有效，必须处于 `screen` 会话中。

### 退出 screen 会话

退出 `screen` 会话，可以使用以下快捷键进行分离（detach）：

Control + A 然后按 d

输出将类似于：

```text
[detached from 12921.pts-1.localhost]
(base) [opengenus@localhost ~]$
```

### 列出 screen 会话

一旦离开了 `screen` 会话，就可以回到它。为此，我们应该使用以下命令：

```bash
screen -ls
```

在我们的案例中，输出如下：

```text
There are screens on:
    12921.pts-1.localhost (Detached)
    120455.pts-1.localhost (Detached)
```

# `/var/run/screen/S-opengenus` 中的 2 个 Socket

我们有两个 `screen` 会话，分别是：

- `129921`
- `120455`

也可以回到其中一个会话。

## 在 screen 会话中运行命令

使用 `screen` 的优势在于你可以在 `screen` 会话中运行命令，然后关闭终端，此时进程仍会继续运行。如果你在远程机器上工作或需要关闭终端，这非常有用。

流程如下：

```bash
// 创建一个 screen 会话
screen

// 现在在后台运行命令
command &

// 退出 screen
按下 control key + A 接着按 d

// 现在你可以安全地关闭终端
exit
```

## 回到会话

要回到已有的 `screen` 会话，我们应该使用 `list screen` 命令获取会话名称（例如 `129921`），并使用以下命令：

```bash
screen -r 129921
```

这将让你获得该会话的访问。

## 如何知道你正处于 screen 中？

简单的检测方法是执行 `screen list` 命令，如果有任何活跃的 `screen` 会话，可能意味着你或其它用户正在其中运行。

```bash
screen -ls
```

或者，你也可以尝试退出 `screen`。如果你在 `screen` 中，它会分离（detached）；如果你不在其中，则该操作将无效。

按下 control key + A 接着按 d

## 删除 screen 会话

要删除 `screen` 会话，我们需要进入想要删除的 `screen` 会话，随后有两种选项：

使用 `exit` 命令：

```bash
exit
```

使用以下命令：

`Control key + A` 接着按 `k`

将出现如下提示：

`Really kill this window [y/n]`

按下 `y` 键后，`screen` 会话终止并显示以下消息：

```
[screen is terminating]
(base) [opengenus@localhost ~]$
```

这将终止会话并杀死其中的所有进程。

## 为 screen 会话命名

我们可能需要为 `screen` 会话命名，这样在列出会话时，我们可以理解哪个会话对应哪个任务。

要做到这一点，在创建 `screen` 会话期间，可以使用以下命令：

```bash
screen -S name
```

这将创建一个名为 `"name"` 的 `screen` 会话，以下是 `screen list` 命令的输出：

```
There are screens on:
      113050.name     (Detached)
      105349.pts-1.localhost  (Detached)
      129921.pts-1.localhost  (Detached)
      120455.pts-1.localhost  (Detached)
```

# `/var/run/screen/S-opengenus` 中的 4 个 Socket

## 锁定你的 screen 会话

如果你想锁定 `screen` 会话，可以使用以下组合键：

`control key + A` 接着按 `x`

这将屏幕变为：

`Screen used by opengenus <opengenus> on localhost.`

`Password:`

可以输入 UNIX 用户密码重新登录会话。

## 记录 screen 会话活动

我们可以通过以下命令创建会话来记录 `screen` 会话中的所有活动：

```bash
screen -L
```

如果已经在 `screen` 会话中，可以使用以下组合键：

`control key + A` 接着按 `H`

这将保存一个包含所有活动的文件。

`screen` 应用程序还有许多可用选项。你可以查阅我们之前演示过的帮助选项并尝试每个选项。事实上，我们演示的选项已经足够让你像大师一样使用 `screen` 了。

## 文件处理

我们已经创建了包含文件的目录结构作为工作区。

- `file1`
- `folder1.0.0`
- `--- --- file2`
- `--- --- --- folder1.1.0`
- `--- --- --- --- --- --- folder1.1.1`
- `--- --- --- --- --- --- file3`
- `--- --- --- --- --- --- file4`
- `--- --- --- folder1.2.0`
- `--- folder2.0.0`
- `--- --- file5`

我们将对此进行工作。

`ls`命令用于列出当前层级下的文件和目录。

命令：

```bash
ls
```

输出：

```
file1  folder1.0.0  folder2.0.0
```

`ls -l`命令是上述`ls`命令的进阶，包含了其他关键信息，如文件/目录的大小、修改日期、所有者、权限等。

命令：

```bash
ls -l
```

输出：

```
total 0
-rw-rw-r--. 1 opengenus aditya  0 Aug  7 00:10 file1
drwxrwxr-x. 4 opengenus aditya 57 Aug  7 00:11 folder1.0.0
drwxrwxr-x. 2 opengenus aditya 19 Aug  7 00:11 folder2.0.0
```

`ls -R`

这是一个非常重要的命令，因为它会递归地列出通向任何深度的所有文件和子目录。

命令：

```bash
ls -R
```

输出：

```
.:
file1  folder1.0.0  folder2.0.0
./folder1.0.0:
file2
```
