
```bash
[root@localhost raid10]# mdadm -E /dev/sd[b-e]1 | grep raid10
Raid Level : raid10
Raid Level : raid10
Raid Level : raid10
Raid Level : raid10
[root@localhost raid10]#
```

# 第 18

使用 `lsblk` 检查块设备

=> `lsblk`

```bash
[root@localhost raid10]# lsblk
NAME | MAJ:MIN | RM | SIZE | TYPE | MOUNTPOINT |
| :--- | :--- | :--- | :--- | :--- | :--- |
| sda | 8:0 | 0 | 70G | disk | |
| └-sda1 | 8:1 | 0 | 1G | part | /boot |
| └-sda2 | 8:2 | 0 | 69G | part | |
| └-centos-root | 253:0 | 10 | 45G | lvm | |
| └-centos-swap | 253:1 | 0 | 26G | lvm | [SWAP] |
| └-centos-home | 253:2 | 0 | 22G | lvm | /home |
| sdb | 8:16 | 0 | 20G | disk | |
| └-sdb1 | 8:17 | 0 | 20G | part | |
| └-md0 | 9:0 | 0 | 40G | raid10 | /mnt/raid10 |
| sdc | 8:32 | 0 | 20G | disk | |
| └-sdc1 | 8:33 | 0 | 20G | part | |
| └-md0 | 9:0 | 0 | 40G | raid10 | /mnt/raid10 |
| sdd | 8:48 | 0 | 20G | disk | |
| └-sdd1 | 8:49 | 0 | 20G | part | |
| └-md0 | 9:0 | 0 | 40G | raid10 | /mnt/raid10 |
| sde | 8:64 | 0 | 20G | disk | |
| └-sde1 | 8:65 | 0 | 20G | part | |
| └-md0 | 9:0 | 0 | 40G | raid10 | /mnt/raid10 |
| sr0 | 11:0 | 1 | 4.3G | rom | |
[root@localhost raid10]#
```

# LINUX 进程管理

我们在 Linux 操作系统中所的一切的一切都由进程处理。有不同的命令来管理进程：如何启动和停止进程、如何在前台和后台运行进程、如何自定义进程以及如何使用 `cron` 和 `anacron` 调度进程执行。进程管理和进程监控是提高和优化服务器性能的方法。

# 不同类型的

Linux 基本上有两种进程：

1) 自动进程（后台进程）

2) 交互式进程

# 自动进程

自动进程也称为守护进程（Daemon）。自动进程在系统启动（服务器启动）时启动。此进程不受用户的直接控制。它们不会直接向标准输出写入。

# 交互式进程

交互式进程是用户使用不同命令启动的进程。进程在 shell 中启动并将输出直接写入标准输出。要启动一个交互式进程，用户必须在 shell 中输入命令，进程作为用户输入命令的 shell 的子进程启动。当我们终止子进程时，该进程会向父进程返回退出状态然后安全退出。如果父进程死亡，将无法进行监控，这被称为僵尸进程。僵尸进程是程序不当的结果。启动其他进程的进程是该进程的子进程。

# 一后台进程（守护进程）

| 进程名称（守护进程） |  |

| :--- | :--- |

# UBUNTU $ CENTOS 管理员

`systemd` 是产生所有其他进程的 Unix 程序。在 2016 年之后，它取代了大多数 Linux 操作系统中的 Init 进程。`systemd` 是所有进程树的顶层进程。如果我们打开终端并使用 `pstree` 命令查看进程树。

为 `pstree` 命令安装包：

```bash
ubuntu : sudo apt-get install pstree
centos : sudo yum install pstree
suse : sudo zypper install pstree
```

`Cron` 是一个作业调度程序。该程序用于调度任务，这些任务可以是按时间间隔定期运行的命令和 shell 脚本。它通常用于系统自动化。对于从互联网下载文件或在固定时间间隔下载或发送电子邮件非常有用。它是动态主机配置协议守护进程。此程序在后台运行并自动为客户端计算机设置 TCP/IP 信息。

| ftpd | 该程序处理文件服务器。它处理来自用户的 ftp 请求 |

| Httpd | Httpd 是 Web 服务器守护进程，处理 Web 服务器请求 |

| sshd | sshd 安全 shell 程序。它处理来自用户的 ssh 请求 |

| nfsd | Nfsd 处理用户对 nfs 操作请求（nfs 代表网络文件系统） |

| Sendmail | SMTP 守护进程。它处理 smtp 请求 |

| fingerd | 为 finger 提供网络接口，Finger 用于查找并显示用户信息 |

## UBUNTU & CENTOS 管理员

情况保持不变。这意味着如果我们运行一个程序或在后台运行一个程序，我们仍然可以在终端中看到输出和错误信息（如果发生的话）。如果我们不想要终端输出，可以使用符号 `>` 将此输出重定向到文件中。例如：

`command > /somewhere`

例如，如果我们输入 `ls > output.txt`

它会将该命令的输出写入到当前目录下的 `output.txt` 文件中。

## 如何将进程发送到后台

有两种简单的方法可以将任何进程发送到后台：

1) 在任何命令的末尾添加 `&` 符号

2) 在中断正在运行的前台进程后使用 `bg` 命令

1) 假设我们想在后台运行 `ping 8.8.8.8 > out.txt` 命令，我们在命令末尾添加一个 `&` 符号 => `ping 8.8.8.8 > out.txt &`

2) 当程序在前台运行时，我们使用 `CTRL+Z` 中断该程序，然后使用 `bg` 命令在后台恢复该程序。

```
vagrant@localhost ~$
vagrant@localhost ~$ ping 8.8.8.8 > out1.txt
Z
[1]+ Stopped      ping 8.8.8.8 > out1.txt
vagrant@localhost ~$ bg
[1]+ ping 8.8.8.8 > out1.txt &
vagrant@localhost ~$
vagrant@localhost ~$ jobs
[1]+ Running      ping 8.8.8.8 > out1.txt &
vagrant@localhost ~$ █
```

在将程序发送到后台后，如果我们实际上想查看它们的活动，可以使用 `jobs` 命令查看它们的运行状态。

```
[vagrant@localhost ~]$ ping 8.8.8.8 > out1.txt & 
[1] 23599
[vagrant@localhost ~]$ ping 8.8.4.4 > out2.txt & 
[2] 23600
[vagrant@localhost ~]$ jobs
[1]- Running      ping 8.8.8.8 > out1.txt &
[2]+ Running      ping 8.8.4.4 > out2.txt &
[vagrant@localhost ~]$█
```

## 将进程从后台调前台

要将任何进程从后台带回前台，我们使用 `fg` 命令。

如果只输入 `fg`，它会将最后一个后台作业带回前台。要将特定作业带回前台，我们在 `fg` 命令后使用进程 ID。

例如：

=> `fg %1`

=> `fg %2`

## Tanvir Rahman

## 进程管理

Linux 操作系统有很多优秀的性能监控工具。

下面解释了其中一些：

### ps

与进程管理相关最常用且最简单的命令是 `ps` 命令。通过 `ps` 命令，你可以查看系统当前运行的进程列表。它将显示进程名称和进程 ID (PID)：

```
[vagrant@localhost ~]$ ps
PID TTY TIME CMD
4613 pts/0 00:00:00 bash
23890 pts/0 00:00:00 ps
[vagrant@localhost ~]$ _
```

通过 `ps` 命令，我们可以尝试不同的开关，例如，如果我们使用 `ps -e`，我们可以看到系统中的所有进程，或者你可以使用此命令逐个查看：

=> `ps -e | more`

```
vagrant@localhost:~# ps -e | more
PID TTY          TIME CMD
1 ?             00:00:03 systemd
2 ?             00:00:00 kthread
3 ?             00:00:00 ksoftqd
5 ?             00:00:00 worker/0
6 ?             00:00:00 worker/1
7 ?             00:00:00 worker/2
8 ?             00:00:00 worker/3
9 ?             00:00:00 worker/4
10 ?            00:00:00 worker/5
11 ?            00:00:00 worker/6
13 ?            00:00:00 worker/7
14 ?            00:00:00 worker/8
15 ?            00:00:00 worker/9
16 ?            00:00:00 worker/10
17 ?            00:00:00 worker/11
18 ?            00:00:00 worker/12
19 ?            00:00:00 worker/13
20 ?            00:00:00 worker/14
21 ?            00:00:00 worker/15
22 ?            00:00:00 worker/16
23 ?            00:00:00 worker/17
24 ?            00:00:00 worker/18
25 ?            00:00:00 worker/19
26 ?            00:00:00 worker/20
27 ?            00:00:00 worker/21
28 ?            00:00:00 worker/22
29 ?            00:00:00 worker/23
30 ?            00:00:00 worker/24
31 ?            00:00:00 worker/25
32 ?            00:00:00 worker/26
33 ?            00:00:00 worker/27
34 ?            00:00:00 worker/28
35 ?            00:00:00 worker/29
36 ?            00:00:00 worker/30
37 ?            00:00:00 worker/31
38 ?            00:00:00 worker/32
```

（注：此处示例文本输出不全，翻译时保持了逻辑一致性）

通过 `ps` 命令，我们可以尝试不同的开关...（此处原文内容重复，按要求显示逻辑）

```
[vagrant@localhost ~]$ ping 8.8.8.8 > out1.txt & 
[1] 23599
[vagrant@localhost ~]$ ping 8.8.4.4 > out2.txt & 
[2] 23600
[vagrant@localhost ~]$ jobs
[1]- Running      ping 8.8.8.8 > out1.txt &
[2]+ Running      ping 8.8.4.4 > out2.txt &
[vagrant@localhost ~]$█
```

（由于原文中 `ps` 之后存在大量重复的占位符和描述，译文已根据核心逻辑进行处理，并保持格式一致）

UBUNTU $ CENTOS 管理员

处于睡眠模式，最后一个是僵尸进程（僵尸进程是指已停止但无法向其父进程提供退出状态的进程）。

第三行：第三行包含这些值

| 表头名称 | 描述 |

| :--- | :--- |

| us | 代表用户空间。它代表用户空间中的 CPU 活动。这些活动实际上是由用户名的不同命令启动的 |

| sy | 代表系统空间中的 CPU 活动。这些实际上是内核程序。它们通常代表守护进程（Daemons）执行工作。 |

ni 表示处理低优先级进程花费的时间以及 CPU 空闲时间。高值实际上表示系统未执行任何操作。

它表示 CPU 等待连接到系统的输入（I/O 硬件）的时间（如硬盘、键盘、鼠标），wa是 CPU 与硬件通信花费的时间。例如，如果你从闪存盘读取数据，此时该值将很高（hi）。

CPU 与软件通信花费的时间。通常它应该很低（si）。

此参数表示虚拟机监视程序（Hypervisor）从虚拟机中窃取的时间。如果你的系统没有虚拟机，此值将为 0。

第四行：显示 `free` 命令的准确输出（当前系统的内存统计）。

第五行：这部分是 top 窗口的下部。它提供了关于 CPU 使用率最活跃的进程详情。

| 表头名称 | 描述 |

| :--- | :--- |

| PID | 每个进程都有唯一的进程 ID（称为 PID），进程 ID 非常重要。例如，如果你想杀死一个进程，你需要提供该进程的 ID |

| USER | 使用该进程的用户名。许多进程作为 root 运行，所以你会经常看到它 |

PR 显示进程的优先级。这个数字指示进程何时再次获得 CPU 周期。值越小，优先级越高。高优先级进程将更早获得 CPU 周期，而低优先级进程较后获得 CPU 周期。

NI 进程的 NICE 值。通过 NICE 值我们可以更改进程的优先级。

VIRT 进程占用的内存总量。

RES 进程此时正在使用的内存大小。

SHR 进程与其他进程共享的共享内存量。

- S 显示进程的状态

- ‘R’表示正在运行

- ‘S’表示处于睡眠模式

- ‘Z’表示僵尸进程

- ‘T’表示已停止，可能是由作业控制信号引起的

- ‘D’表示不可中断睡眠

%CPU 上一个轮询周期（通常为 5 秒）使用的 CPU 比例。

%MEM 上一个轮询周期使用的内存量（通常为 5 秒）。

TIME 表示进程自启动以来已使用的 CPU 总时间。

这是启动进程的命令。

```
COMMAND
```

# 杀死进程的命令

有不同的命令用于终止进程

| 进程终止命令 | 描述 |

| :--- | :--- |

| Kill | 最常用的命令，带有数字参数（SIGKILL），如果没有指定信号，则向进程发送默认信号（15） |

killall 如果我们想杀死多个进程，可以使用 `killall` 命令。例如，如果我们使用 `killall httpd`，它将杀死 Apache 服务器的所有实例。

我们可以使用 `top` 命令杀死进程。在 top 界面按下‘k’。系统会提示你输入进程的 PID。输入后，你必须输入要发送给进程的信号。指定数字值它将终止进程。

pkill 是根据进程的其他信息终止进程的命令。它允许管理员通过详细信息查找进程，例如 `pkill -U 501` 将杀死所有属于用户 501 的进程。

# 高级 LINUX 进程管理

Linux 操作系统有一些高级进程监控工具。下面解释其中一些。

# htop

大多数熟悉 Linux 的系统管理员都用过 `top` 命令行工具来查看哪个进程占用最多的 CPU 或内存。有一个名为 `htop` 的类似工具，对于普通任务来说更容易使用。它是交互式的、实时的，最重要的是，它非常用户友好，你可以一眼看出 CPU 利用率。

但要使用 `htop` 工具，我们必须先安装它。因为默认情况下系统中没有安装。

在 Linux 中安装 `htop` 的过程（使用不同的包管理器）：

# Ubuntu:

```
=> sudo apt install htop
```

# Centos:

在 CentOS 中安装，我们只需要添加 EPEL 仓库， `yum` 就能找到它。

- => `sudo yum -y install epel-release`

- => `sudo yum -y update`

- => `sudo yum install htop`

安装成功后，我们必须输入：

```
=> sudo htop
```

我们应该能看到系统的系统的状态。

它几乎就像 `top` 命令，但更具交互性和用户友好。

让我们谈谈 top 工具的每个选项。

- 1. 第一选项是 CPU，显示 CPU 利用率百分比并以图形模式显示。

- 2. 第二选项是内存选项，显示实际使用的内存。

- 3) 第三选项是系统使用的交换空间（Swap）。

- 4) 右侧下一个选项是任务（Task）。显示总任务数、线程和运行中的任务。

- 5) 下一个选项显示系统的平均负载（Load average）。

- 6) 右侧第三选项显示服务器的运行时间（Uptime），显示服务器运行的时间。

下部提供了进程详情，就像 `top` 命令一样，让我们再次查看：

| 表头名称 | 描述 |

| :--- | :--- |

| PID | 每个进程都有唯一的进程 ID（称为 PID），进程 ID 非常重要。例如，如果你想杀死一个进程，你需要提供该进程的 ID |
