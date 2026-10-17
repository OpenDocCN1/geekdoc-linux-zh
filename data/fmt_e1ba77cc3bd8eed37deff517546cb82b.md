
```bash
$ ps U scott
```

| PID | TID | STAT | TIME | COMMAND |
| :--- | :--- | :--- | :--- | :--- |
| 14928 | ? | S | 0:00 | `/opt/oo2/program/soffice -writer` |
| 14957 | ? | S | 0:42 | `/opt/ooo2/program/soffice.bin -writer` |
| 4688 | pts/4 | S+ | 0:00 | `scott@humbug.machine.com` |
| 26751 | ? | Z | 0:00 | `[wine-preloader] <defunct>` |
| 27921 | ? | S | 0:00 | `47928k id 0.1% /usr/bin/vim` |
| 27955 | pts/5 | R+ | 0:00 | |

```bash
$ kill 27921

$ ps scott
```

| PID | TTY | STAT | COMMAND |
| :--- | :--- | :--- | :--- |
| 14928 | ? | S | 0:00 | `/opt/ooo2/program/soffice -writer` |
| 14957 | ? | S | 0:42 | `/opt/ooo2/program/soffice.bin -writer` |
| 4688 | pts/4 | S+ | 0:00 | `scott@humbug.machine.com` |
| 26751 | ? | Z | 0:00 | `[wine-preloader] <defunct>` |
| 27955 | pts/5 | R+ | 0:00 | `ps scott` |

要杀死`gvim`，你使用`ps gvim`获取`PID`，在本例中为`27921`。接着杀死该`PID`（记住`kill`默认使用`TERM`信号），然后再次用`ps`检查。是的，`gvim`不复存在了。

### 注意

为什么没有杀死`PID`为`26751`的进程？它的`STAT`为`Z`，表示它是一个僵尸进程（`zombie`）。因为`-9`对已经没有地址的僵尸进程无效，`kill`命令无法作用。重启是解决该（无关紧要）问题的唯一方法。

# 查看动态更新的运行进程列表

### top

有时你会发现你的`Linux`无缘无故变慢了。原因是某个程序在你的电脑上全负荷运行，并占用了处理器。或者你启动了一个运行命令，发现它占用的`CPU`周期比你想象的要得多。要找出导致问题的原因，或者你只是想知道系统上运行了哪些程序，可以使用`ps`，但`ps`不会自我更新。相反，它提供的是系统进程的快照，仅此而已。

相比之下，`top`命令提供了系统上运行进程的动态更新列表，以及每个进程使用的资源数量。在书中可能很难看，因为你会看到它每秒更新一次，但你至少能在某一时刻看到正在上方运行的内容。

```
$ top

time 18:05:83 up 4 days, 8:01, load average: 0.83, 0.82, 0.97

Tasks: 135 total, 3 running, 126 sleeping, 2 stopped, 4 zombie

Cpu(s): 22.9% us, 7.7% sy, 3.1% ni, 62.2% id, 3.5% wa, 0.1% hi

Mem: 103616k total, 79796k used, 48140k free, 27884k buff

Swap: 102400k total, 0k used, 102400k free

PID USER PR NI VIRT RES SHR SCPU %MEM TIME TIME+COMMAND

14928 root      20  0 123.4m  45.6m  10.2m S  0.0  0.4% 0:00:00 /opt/oo2/program/soffice -writer

14957 root      20  0 135.6m  58.7m  12.3m S  0.5  0.5% 0:00:42 /opt/ooo2/program/soffice.bin -writer

4688 scott     20  0  15.2m   5.4m   2.1m S+  0.0  0.0% 0:00:00 scott@humbug.machine.com

26751 root       Z  0  0.0m     0.0m   0.0m Z  0.0  0.0% 0:00:00 [wine-preloader] <defunct>

27921 scott     20  0 47.9m  22.1m   8.5m S  0.1  0.0% 0:00:00 /usr/bin/vim

27955 scott     20  0 10.1m   4.2m   1.5m R+  0.0  0.0% 0:00:00 ps scott
```

（注：由于示例中`top`输出内容不完整，此处在翻译时保持了其逻辑结构）

`top`命令提供了系统上运行进程的动态更新列表，以及每个进程使用的资源数量。在书中可能很难看，因为你会看到它每秒更新一次，但你至少能在某一时刻看到正在上方运行的内容。

# 第四部分：环境

### 查看文件打开情况

```bash
# lsof /usr/sbin/sshd  TYPE
```

| COMMAND | PID | USER | NAME |
| :--- | :--- | :--- | :--- |
| `sshd` | 7814 | root | `REG /usr/sbin/sshd` |
| `sshd` | 10542 | root | `REG /usr/sbin/sshd` |
| `sshd` | 10548 | scott | `REG /usr/sbin/sshd` |

这就是你想要的结果：两个用户，`root`和`scott`。如果这里出现了一个意料之外的用户，你就知道你的系统被攻破了。

### 注意

是的，`ssh`是一个程序，但记住，这是从你人类的角度来看的。对于`Linux`来说，`/usr/sbin/sshd`仅仅是另一个文件。

### 列出特定程序的进程列表

### `lsof -c [program]`

在上一节中，你看到了谁在用`/usr/sbin/sshd`。然而，你收到的结果并没有告诉全部情况。任何程序实际上都是由调用（可能是许多）其他进程、程序、套接字和设备而成的，所有这些内容在`Linux`看来都是文件。要找到与特定运行进程关联的所有其他文件，请在`lsof`后面加上`-c`选项，然后是（因此是“已打开的”）进程的名称。例如，`lsof /usr/sbin/sshd`显示与该特定文件关联有两个用户和三个打开的文件。那么整个`sshd`命令又是呢？

```bash
#### lsof -c ssh

COMMAND PID USER NAME

sshd 10542 root /lib/ld-2.3.5.so

sshd 10542 root /dev/null

sshd 10542 root 192.168.0.170:ssh->192.168.0.100:4577 (ESTABLISHED)

sshd 10548 scott /usr/sbin/sshd

sshd 10548 scott 192.168.0.170:ssh->192.168.0.100:4577 (ESTABLISHED)
```

在前面的代码中，你可以看到与`sshd`进程连接的`94`行（代表`94`个打开的文件）中的几行。其中一个是一个`.so`文件（共享对象，类似于`Windows`上的`DLL`），还有几处显示此机器与另一台机器之间发生了网络连接（实际上，该网络上的那台机器通过`SSH`连接到这里；关于这更多信息，请参见第`15`章“在网络工作”中的“安全地登录另一台计算机”）。

通过将`lsof`应用于计算机上的各种命令，你可以发现海量信息；至少，你会了解到现代程序有多复杂。尝试用你每天使用的软件试一下，你可能会对那些努力工作为你提供服务的程序员们产生全新的赞赏。

### 注意

`lsof`命令拥有惊人的选项数量，而你只会查看其中极小的一个子集。`lsof`的源代码包含一个名为`00QUICKSTART`的文件（开头有两个零），该文件是该命令一些更强大功能的教程。在`Google`上搜索该文件名并开始阅读即可。

### 显示系统内存信息

`free`

如今，大多数计算机都配备了数百兆甚至几`GB`的内存，但你仍然可能发现你的机器因为内存使用过多或虚拟内存交换而运行变慢。要查看系统内存的当前状态，请使用`free`命令。

```bash
$ free total used free buffers cached

Mem: 103616 995852 0 80816 332264

-/+ buffers/cache: 582772 453364

Swap: 1012084 49584 516500
```

默认情况下，`free`以千字节显示结果，与你使用的相同。然而，你可以更改它。`b`选项以字节显示内存使用情况，而`-m`（你可能大部分时候应该使用它）使用兆字节。

```bash
$ free -m total used free shared buffers cached

Mem: 1011 963 48 0 78 316

-/+ buffers/cache: 569 442

Swap: 988 483 504
```
