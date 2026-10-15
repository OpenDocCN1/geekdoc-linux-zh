
```
$ ls -l myfifo3 myfifo4

prw-r--r-- 1 sarwar faculty 0 Aug 9 08:30 myfifo3

prw------ 1 sarwar faculty 0 Aug 9 08:31 myfifo4

$
```

两个命令 `cmd1` 和 `cmd2` 可以通过名为 `myfifo1` 的 FIFO 进行通信的通用方法如下所示的命令序列。

```
cmd1 < myfifo1 &
cmd2 infile | tee myfifo1 | cmd3
```

请注意，我们在后台运行第一个命令（参见第 10 章了解后台进程），以便我们可以运行 `cmd2`。当我们执行 `cmd1` 时，它会阻塞，因为 `myfifo1` 为空。请注意，如果 `myfifo1` 是一个文件，`cmd1` 会阻塞并立即返回。当 `cmd2` 的输出通过 `tee` 实用程序发送到 `myfifo1` 和 `cmd3` 时，`cmd1` 解锁并开始处理 `myfifo1` 中的数据。命令 `cmd1` 和 `cmd3` 的输出发送到标准输出（即显示屏）。图 9.18 使用图表帮助说明了这些语义。

在下面的会话中，命令序列显示系统上运行的所有进程的状态、守护进程的数量以及系统上运行的进程总数。两个 `cat` 命令会阻塞，直到有内容写入 `myfifo1` 和 `myfifo2`。`ps -a` 命令将系统上运行的所有进程的状态发送到 `tee` 命令，该命令将此数据重定向到两个 FIFO，同时将其发送到 `grep` 命令。`grep` 命令从其输入中（即 `ps -a` 命令的输出）提取所有守护进程，并通过管道将其发送到 `wc -l` 命令。因此，第一个 `cat` 命令显示系统上运行

![](img/02e070097d401d3bf7de4bf1c470b267_367_0.png)

图 9.18 命令序列 `cmd1 < myfifo1 &` 后跟 `cmd2 infile | tee myfifo1 | cmd3` 的执行语义。

on the system. 第二个 `cat` 命令的输出是系统上运行的进程数，而第三个命令（`ps -a`）的输出是系统上运行的守护进程数。如输出最后两行所示，在运行此命令序列时，系统运行着 20 个进程，其中两个是守护进程。

```
$ cat myfifo1 &
$ cat myfifo2 | wc -l &
$ ps -a | tee myfifo1 myfifo2 | grep 'd$' | wc -l
  PID TT  STAT TIME COMMAND
1533 v0- I  0:00.01 /bin/sh /usr/local/sbin/PCDMd
1548 v0- IN 3:43.82 /bin/sh /usr/local/sbin/pbid
1790 v0  Is+ 0:00.00 /usr/libexec/getty Pc ttyv0
1791 v1  Is+ 0:00.00 /usr/libexec/getty Pc ttyv1
...
1797 v7  Is+ 0:00.00 /usr/libexec/getty Pc ttyv7
56478 1  Is  0:00.24 -csh (csh)
57216 1  S  0:00.12 /bin/sh
58002 1  S  0:00.01 cat myfifo1
58045 1  S  0:00.01 cat myfifo2
58046 1  I  0:00.01 wc -l
58089 1  R+ 0:00.02 ps -a
58090 1  S+ 0:00.01 tee myfifo1 myfifo2
58091 1  S+ 0:00.02 grep d$
58092 1  S+ 0:00.01 wc -l
    2
$   20
```

此会话中输出的顺序取决于三个命令的调度；上面显示的输出是我们系统产生的输出，也是最可能的输出。一个有趣的练习是想出一个命令序列，以确保输出始终按此处所示的相同顺序产生。

当你不再需要使用 FIFO 时，可以像删除普通文件一样删除它。这意味着你可以使用 `unlink()` 系统调用（在进程内部）或在命令行中使用 `rm` 命令从文件系统层次结构中删除 FIFO。在下面的会话中，我们使用 `rm` 命令删除 `myfifo1` 和 `myfifo2` FIFO。`rm` 命令执行前后的 `ls` 命令输出显示，这两个 FIFO 确实已被删除。

```
$ ls
myfifo1 myfifo2
$ rm myfifo1 myfifo2
$ ls
$
```
