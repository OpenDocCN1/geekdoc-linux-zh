
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

以下是关于使用 `iostat` 接收的终端、CPU 和已挂载文件系统的报告说明。由于报告略有不同，我包含了来自 HP-UX 输出的详细信息。本章末尾的 `iostat` 手册页中包含了这些字段的更详细描述。大多数字段都出现在输出中；然而，这些命令的输出在不同的 UNIX 变体中略有不同。

对于你连接的每个终端 `tty`，你都会看到 `tin` 和 `tout`，它们分别代表从终端读取的字符数和写入终端的字符数。

对于你的 CPU，你会看到花费在用户模式 `us` 的时间百分比，花费在运行称为 `nice` 的低优先级用户进程的时间百分比 `ni`，花费在系统模式 `sy` 的时间百分比，以及 CPU 空闲 `id` 的时间百分比。

对于每个本地挂载的文件系统，你会收到每秒传输的千字节数 `bps`、每秒寻道次数 `sps` 以及平均寻道毫秒数 `msps` 的信息。对于通过 NFS 挂载的磁盘或服务端客户节点上的磁盘，你将不会收到报告；`iostat` 仅报告本地挂载的文件系统。

在查看 `iostat` 的输出时，有一些参数值得注意。

首先，注意你的 CPU 在所示的四个类别中花费的时间。CPU 报告是通过 `-t` 选项生成的。我在性能较差的系统上工作过，管理员假设这是由于 CPU 速度慢造成的，但当时 `id` 数字非常高，表明 CPU 实际上大部分时间都处于空闲状态。如果 CPU 大部分时间都是空闲的，那么瓶颈很可能不是 CPU

但瓶颈可能在于 I/O、内存或网络。如果 CPU 确实大部分时间都很忙 `id` 值非常低，请检查是否有进程正在以 `nice` 低优先级方式运行 检查 `ni` 数值。可能有一些后台进程消耗了大量 CPU 时间，可以将它们改为以 `nice` 方式运行。

其次，比较所有已挂载磁盘的平均寻道毫秒数 `msps`。如果你挂载了三块相同的磁盘，但其中一块的 `msps` 远高于其他磁盘，那么你可能是在过载使用这块磁盘，而其他磁盘则大部分处于空闲状态。如果是这样，请在磁盘之间均匀分配工作负载，以便尽可能接近每块磁盘相同的访问次数。请注意，较慢的磁盘的 `msps` 总是比快速磁盘高，因此请将最常访问的信息放在更快的磁盘上。磁盘的 `msps` 通常约为 20 毫秒，而 DVD 的 msps 会高得多，约为 200 毫秒。

## 使用 vmstat 查看虚拟内存统计信息

![](img/75f39fc91296b889c0653851accdfd46_888_0.png)

`vmstat` 提供虚拟内存统计信息。它提供有关进程状态、虚拟内存、分页活动、故障以及 CPU 时间百分比细分的信息。`vmstat` 在不同的 UNIX 变体中行为略有不同。以下示例展示了在 Solaris 系统、HP-UX 系统、AIX 系统和 Linux 系统上执行 `vmstat` 的操作。当然，你需要根据你的 UNIX 变体确定最适合你需求的选项。在以下示例中，输出结果以五秒为间隔产生了九次。`vmstat` 命令的第一个参数是间隔；第二个是你希望产生输出的次数。

### Solaris 示例：
