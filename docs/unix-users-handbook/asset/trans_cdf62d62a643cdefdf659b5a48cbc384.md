
## 标准 UNIX 命令

首先，让我们来看看一些你可以在 UNIX 提示符下执行的命令，以获取有关系统的信息。我将涵盖的命令包括：

- **iostat**
- **vmstat**
- **netstat**
- **ps**
- **kill**
- **showmount**
- **swapinfo 和 swap**
- **sar**

我们将首先介绍这些命令中的每一个，以便你了解每个命令产生的输出以及如何利用这些输出。本章末尾提供了许多相关命令的手册页。

请记住，正如我们之前介绍的所有主题一样，这些命令的输出在不同的 UNIX 变体中可能略有不同。大多数 UNIX 变体产生的基本信息是相同的；但是，输出的格式可能略有差异。如果你只是在查看输出，这通常并不重要；但是，如果你正在编写程序来接受这些输出并以某种方式操作它们，那么输出的格式就很重要。

## 使用 iostat 获取 I/O 和 CPU 统计信息

**iostat** 命令让你了解 CPU 在 I/O 上投入的努力程度，以及磁盘和终端之间发生的 I/O 量。**iostat** 提供了许多有用的信息；然而，它在不同的 UNIX 变体中的行为略有不同。以下示例展示了在 Solaris 系统、HP-UX 系统和 AIX 系统上执行 **iostat** 的情况。我在本章中使用的 Linux 系统不支持 **iostat**。请注意，在某些系统上，使用终端信息的 **-t** 选项仅产生终端信息，而在某些系统上则产生完整输出。当然，你需要根据需求确定最适合你的 UNIX 变体的选项。以下示例展示了 **iostat** 命令：

### 在 Solaris 上每 5 秒执行一次的 iostat 示例，共执行 10 次：

```
# iostat 5 10

tin tout kps tps serv  kps tps serv    kps tps serv  us sy wt id
tty   fd0                    sd1                 sd6
cpu
0  0  0  0  0  0   0   0   0   3   0  57   0  0  0  0  7  49 43
0  47 0  0  0   0   0   0  14  2  75   0  0  0  0  2  0 98
0  16 0  0  0   0   0   0   0   0  0   0   0  0  0  1  0 98
0  16 0  0  0   0   0   0   0   0  0   0   0  0  0  2  0 98
0  16 0  0  0   0   0   0   0   0  0   0   0  0  0  0  0 100
0  16 0  0  0   0   0   0   0   0  0   0   0  0  0  1  0 99
0  16 0  0  0   0   0   0   0   0  0   0   0  0  0  0  0 100
0  16 0  0  0   0   0   0   0   6  1  35   0  0  0  0  4  0 96
0  16 0  0  0   0   0   0   0   0  0   0   0  0  0  0  0 100
```

### 在 HP-UX 上每 5 秒执行一次的 iostat 示例，包含 -t 选项，共执行 5 次：

```
# iostat -t 5 5

               tty    cpu
          tin tout us  ni  sy  id
             0  3  17  0  3  80

device     bps    sps    mps
c0t6d0     0     0.0    1.0
c5t4d0     0     0.0    1.0
c4t5d0     0     0.0    1.0
c4t5d1     0     0.0    1.0
c5t4d1     0     0.0    1.0
c5t4d2     0     0.0    1.0
c5t4d3     0     0.0    1.0

               tty    cpu
          tin tout us  ni  sy  id
             0  0  30  0  12  58

device     bps    sps    mps
c0t6d0     0     0.0    1.0
c5t4d0     20    2.4    1.0

c4t5d0      0    0.0     1.0
c4t5d1     26    2.4     1.0
c5t4d1      0    0.0     1.0
c5t4d3      0    0.0     1.0

tty    cpu
   tin tout us  ni  sy  id
    0   36  0  14  51

device    bps     sps     msp

c0t6d0      2    0.2     1.0
c5t4d0     33    3.9     1.0
c4t5d0      0    0.0     1.0
c4t5d1     48    4.9     1.0
c5t4d1      0    0.0     1.0
c5t4d2      1    0.2     1.0
c5t4d3      0    0.0     1.0

tty    cpu
   tin tout us  ni  sy  id
    0   25  0  12  64

device    bps     sps     msp

c5t4d0      6    1.0     1.0
c4t5d0      0    0.0     1.0
c4t5d1     17    2.2     1.0
c4t5d1      0    0.0     1.0
c5t4d3      0    0.0     1.0

tty    cpu
   tin tout us  ni  sy  id
    0   31  0  13  56

device    bps     sps     msp

c5t4d0     11    1.4     1.0
c4t5d0      0    0.0     1.0
c4t5d1     14    1.6     1.0
c5t4d1      0    0.0     1.0
c5t4d2      3    0.4     1.0
c5t4d3      0    0.0     1.0
```

### 在 AIX 上每 5 秒执行一次的 iostat 示例，共执行 10 次：

```
# iostat 5 10

tty:         tin           tout          avg-cpu:  % user    % sys     % idle    % iowait
           0.0           0.0             0.3     1.0     98.4      0.3

Disks:        % tm act     Kbps         tps     Kb read   Kb wrtn
hdisk0          0.4         2.7         0.4    2366635    959304
hdisk1          0.0         0.0         0.0     18843     37928
hdisk2          0.1         0.6         0.1    269803    423284
hdisk3          0.0         0.0         0.0     20875       172
cd0             0.0         0.0         0.0        14         0

tty:         tin           tout          avg-cpu:  % user    % sys     % idle    % iowait
           0.0          108.2            0.0      0.2     99.8      0.0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0
cd0 0.0 0.0 0.0 0 0

tty: tin tout avg-cpu: % user % sys % idle % iowait
0.0 108.4 0.2 0.8 99.0 0.0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0
cd0 0.0 0.0 0.0 0 0

tty: tin tout avg-cpu: % user % sys % idle % iowait
0.0 108.4 0.4 0.2 99.4 0.0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0
cd0 0.0 0.0 0.0 0 0

tty: tin tout avg-cpu: % user % sys % idle % iowait
0.0 108.2 0.4 0.6 99.0 0.0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0
cd0 0.0 0.0 0.0 0 0

tty: tin tout avg-cpu: % user % sys % idle % iowait
0.0 108.4 0.0 0.4 99.6 0.0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0
cd0 0.0 0.0 0.0 0 0

tty: tin tout avg-cpu: % user % sys % idle % iowait
0.0 108.4 0.6 0.0 99.4 0.0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0
cd0 0.0 0.0 0.0 0 0

tty: tin tout avg-cpu: % user % sys % idle % iowait
0.0 108.2 0.2 0.8 99.0 0.0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0

cd0 0.0 0.0 0.0 0 0
tty: tin tout avg-cpu: % user % sys % idle % iowait
0.0 108.4 0.4 0.4 99.2 0.0

Disks: % tm_act Kbps tps Kb_read Kb_wrtn
hdisk0 0.0 0.0 0.0 0 0
hdisk1 0.0 0.0 0.0 0 0
hdisk2 0.0 0.0 0.0 0 0
hdisk3 0.0 0.0 0.0 0 0
cd0 0.0 0.0 0.0 0 0
```

以下是关于使用 iostat 接收的终端、CPU 和已挂载文件系统的报告说明。由于报告略有不同，我包含了来自 HP-UX 输出的详细信息。本章末尾的 iostat 手册页中包含了这些字段的更详细描述。大多数字段都出现在输出中；然而，这些命令的输出在不同的 UNIX 变体中略有不同。

对于你连接的每个终端（tty），你都会看到“tin”和“tout”，它们分别代表从终端读取的字符数和写入终端的字符数。

对于你的 CPU，你会看到花费在用户模式（“us”）的时间百分比，花费在运行称为 nice 的低优先级用户进程的时间百分比（“ni”），花费在系统模式（“sy”）的时间百分比，以及 CPU 空闲（“id”）的时间百分比。

对于每个本地挂载的文件系统，你会收到每秒传输的千字节数（“bps”）、每秒寻道次数（“sps”）以及平均寻道毫秒数（“msps”）的信息。对于通过 NFS 挂载的磁盘或服务端客户节点上的磁盘，你将不会收到报告；iostat 仅报告本地挂载的文件系统。

在查看 iostat 的输出时，有一些参数值得注意。

首先，注意你的 CPU 在所示的四个类别中花费的时间。CPU 报告是通过 -t 选项生成的。我在性能较差的系统上工作过，管理员假设这是由于 CPU 速度慢造成的，但当时“id”数字非常高，表明 CPU 实际上大部分时间都处于空闲状态。如果 CPU 大部分时间都是空闲的，那么瓶颈很可能不是 CPU
