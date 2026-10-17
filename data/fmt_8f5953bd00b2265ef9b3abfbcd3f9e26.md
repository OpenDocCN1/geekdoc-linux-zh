
root 1020 5 00:00:00 `/sbin/dhclient -d`

root 1045 1 00:00:00 `/bin/dbus-daemon`

root 1072 1 00:00:00 `/usr/libexec/upd`

root 1077 8 00:00:00 `gnome-shell`

root 1083 1 00:00:00 `/usr/bin/pulaudio`

root 1148 1 00:00:00 `/usr/libexec/go-daemon`

root 1164 1 00:00:00 `login`

root 1175 1 00:00:00 `bash`

```（注：OCR 表格在此处已交叉并重建）```

如图所示，内核的 PID 为 2，并在 Linux 启动后不久即启动进程，因为这些进程的 PPID 为 2，而大多数其他守护进程的 PPID 为 1。守护进程和内核的 TTY 列中有一个 `?` 是因为它们没有在终端上运行吗？

由于 `-ef` 命令的输出在 Linux 服务器上会跨多行显示，你通常将其管道到 `less` 命令以进行分页查看，或者管道到 `grep` 命令以只显示特定信息。例如，要只显示系统上的 BASH 壳，可以使用以下命令：

```
[root@server1]# # ps -ef grep bash

user 2094 2008 29 00:00:00 -bash

user 2157 2150 33 00:00:00 --bash

user 2294 2159 44 00:00:00 --color=auto bash
```

注意，`grep` 命令也与 BASH 壳并排显示，是因为在执行 `ps` 命令时它正在内存中运行。情况可能并非如此，因为 Linux 内核根据多种因素调度任务。

`-e` 和 `-f` 选项是 `ps` 命令中最常用的选项；还有许多其他选项被使用。`ps` 命令的 `-l` 选项列出了关于每个进程的更多信息，比 `-f` 选项提供的更详细。以下是使用该选项查看 tty 进程的示例：

```
[root@server1]# ps -l

F S UID PPID PRI NI ADDR WCHAN TTY TIME CMD

4 S 0 2159 216 8 -1238 wait tty2 00:00:00 bash

4 R 0 2259 212 8 -744 tty2 00:00:00 ps
```

`ps -f` 标志指示特定类型的僵尸进程；进程输出中的 `S` 标志对系统管理员最有价值，因为它显示了哪个进程正在运行。如果进程当前没有运行，进程状态列中的 `S`（可中断睡眠）表示进程处于这种模式，并在需要时被其他进程唤醒，如使用 `ps` 命令所示。如果进程在处理器上运行，你会在该列中看到 `R`；`D`（不可中断睡眠）则表示它正在等待磁盘访问，或者已停止或挂起。此外，你还可能在此列中看到 `Z`，表示僵尸进程。当进程执行完毕时，父进程必须检查并释放进程 PID 以再次使用。僵尸进程正在等待其父进程释放 PID。在繁忙的 Linux 服务器上，僵尸进程可能会堆积并阻止新进程的创建；如果发生这种情况，你可以杀死僵尸进程的父进程，如下一节所述。

> 注意 5
> 僵尸进程也被称为失效进程（defunct processes）。

> 注意 6
> 要查看系统上的进程列表，使用 `ps -el | grep` 命令。

优先级 `PRI` 是内核用于进程的优先级，其范围在 0（高优先级）到 127（低优先级）之间。nice 值 `NI` 可以间接影响进程优先级；其范围从 -20（更有可能是高优先级）到 19（更有可能是低优先级）。进程输出中的 `ADDR` 指进程的内存地址，`WCHAN` 指示进程睡眠时在等待什么。此外，还列出了大小 `SZ`，单位为字节；它大致等于进程可执行文件的大小。

# CompTIA Linux+ 和 LPIC-1: Linux 认证

```
5 S 0:00 [watchdog/0]

6 S 0:00 [migration/1]

7 S 0:00 [koftirqd/1]

8 S 0:00 [watchdog/1]

9 S 0:00 [events/0]

10 S 0:00 [events/1]

[root@server1 ~]# 
```

此处列出的列是之前讨论过的那些；然而，进程状态列被标识为 `STAT`，并可能包含额外的字符以指示进程状态的完整性质。例如，`w` 表示进程在内存中没有上下文，`c` 表示高优先级进程，`n` 表示低优先级进程。

> 注意：要查看之前输出中 `STAT` 或 `S` 列中可能显示的符号完整列表，请参考 `ps` 命令的帮助页。

`ps` 命令有几十个选项可用于显示进程及其属性；本节列出的选项是最常用的，并汇总在表 9-1 中。

## 表 9-1 ps 命令的常用选项

| 选项 | 说明 |
| :--- | :--- |
| -e | 显示所有在终端上运行的进程以及未在终端上运行的进程（守护进程） |
| -f | 显示每个进程的完整信息列表，包括 UID、PID、PPID、CPU 利用率、启动时间、处理器和命令名称 |
| -l | 显示每个进程的详细信息列表，包括标志、状态、UID、PID、CPU 利用率、优先级、值、大小、WCHAN 和命令名称 |
| -Z | 显示每个进程的 SELinux 上下文（在第 14 节讨论） |
| a | 显示所有在终端上运行的进程 |
| x | 显示所有未在终端上运行的进程 |

`ps` 命令不是查看进程信息的命令。内核在 `/proc` 目录下导出了所有进程子目录。每个子目录以其包含的进程 PID 命名，如下所示：

```
[root@server1 ~]# ls /proc

1 1174 26 208 47 852 irq slabinfo

10 1175 27 292 40 856 callsyms softirqs

1018 12 1754 3 411 48 9 kcore stat

1025 1213 176 307 412 482 acpi

1025 1216 176 308 414 488 buggy key-users

1045 1020 176 354 415 49 bus sysig

1063 138 179 351 458 616 circus kpagecount sysipc

1065 14 179 353 421 550 cmdline timer_pages

1072 15 178 354 421 552 consoles loadavg timer_stats

1079 18 170 357 422 558 cpuinfo tty

1080 164 181 358 524 595 crypto uptime

```

| 1087 | 165 | 1810 | 359 | 430 | 6 | devices | version |
| 1097 | 167 | 188 | 370 | 431 | 60 | diskstats | misc | vmallocinfo |
| 11 | 168 | 188 | 370 | 431 | 62 | dma | modules | vmstat |
| 1111 | 169 | 191 | 372 | 435 | 64 | driver | mounts | zoneinfo |
| 1114 | 170 | 191 | 384 | 437 | 7 | execodmons | mtr | net |
| 1117 | 170 | 202 | 384 | 440 | 72 | fb | filesystems | pagetypeinfo |
| 1142 | 172 | 204 | 386 | 446 | 8 | fs | partitions |
| 1148 | 173 | 205 | 387 | 435 | 81 | interrupts | sched_debug |
| 1164 | 1115 | 2206 | 388 | 46 | | 2 | | iemma | scsi |
| 1171 | 145 | 276 | 394 | 437 | 74 | ioports | self |

因此，来自 `/proc` 目录的任何程序都可以显示进程信息。例如，`pstree` 命令显示通过 PPID 追踪的进程血系关系，直到单元守护进程。该命令的前六行所示：

```
[rootserver~]$ pstree --help 2<
systemd--ModemManager-2*
--NetworkManager-3*
--accounts-daemon-2*
--dbus-daemon-2*
--at-spi-bus-2*
--at-daemon-2*
--dbus-daemon-2*
--at-spi-bus-2*
```

## CompTIA Linux+ 和 LPIC-1：Linux 认证指南

> 注意 10
> `kill -SIGQUIT 1199` 命令与前面输出所示的 `kill -3 1199` 命令相同。

> 注意 11
> 如果你在使用 `kill` 命令时不指定信号，`kill` 命令将使用默认的 SIGTERM 信号。

> 注意 12
> 你可以使用 `pidof` 命令找到进程的 PID，并将其作为 `kill` 命令的参数。例如，`pidof sample` 将返回 sample 进程的 PID。

在向多个进程发送信号时，使用 `pgrep` 命令定位进程 PID 通常更简单。`pgrep` 会返回匹配正则表达式或特定标准的进程 PID 列表。例如，要向所有由名称以 psql 开头的用户启动的进程发送 SIGKILL，可以使用以下命令来定位并终止这些进程：

```bash
[@server1 ~]# pgrep -u "^psql"
1344
1501
1522
[@server1 ~]# kill -3 1344 1501 1522
[@server1 ~]# _
[@server1 ~]# pgrep -u "^psql"
[@server1 ~]# _
```

某些进程能够忽略或捕获发送给它们的 kill 信号。唯一无法被任何进程捕获的 kill 信号是 SIGKILL。但如果 SIGINT、SIGQUIT 和 SIGTERM 无法终止一个顽固的进程，你应该只将 SIGKILL 作为最后的手段，因为它会阻止进程正常关闭打开的文件和其他资源。

> 注意 13
> 在发送 SIGKILL 之前，可以使用 `lsof`（列出打开的文件）命令查看该进程是否有已打开的文件。例如，要查看 PID 为 1399 的进程使用的文件，可以使用 `lsof -p 1399` 命令。

如果你向带有子进程的进程发送信号，父进程将终止自身。因此，要杀死多个相关的进程，你只需向其父进程发送 kill 信号。为了杀死僵尸进程，通常需要向其父进程发送 kill 信号。

> 注意 14
> 为了防止父进程在终止时子进程也被终止，你可以使用 `nohup` 命令启动子进程。例如，在 shell 中执行 `nohup celery` 将脱离与启动它的父进程的所有关联。

## 第 9 章 管理 Linux 进程

另一个可以向进程发送 kill 信号的命令是 `killall`。
`killall` 命令的工作原理与 `kill` ，它也是作为选项发送 kill 信号；但它使用的是进程名称而不是 PID。一次可以杀死多个同名的进程。以下输出了使用 `killall` 命令向 sample 进程发送 SIGQUIT 的示例：

```bash
[root@server1 # ps -ef | grep sample
root             1729  1 00 Jun tty3      00:00:00 /bin/sample
root             20198  1 00 Jun tty4      00:00:00 /bin/sample
[root@server1 #] kill -3 sample
[root@server1 #] ps -ef | grep sample
[root@server1 #]#
```

或者，你也可以使用 `kill -SIGQUIT sample` 命令，达到与前面输出所示的 `kill -3 sample` 相同的功能。

与 `kill` 命令一样，如果你在使用 `kill` 命令时不指定信号，它默认会发送 SIGTERM。

你可以使用 `pkill` 命令通过进程名杀死进程。然而，`pkill` 命令允许你使用正则表达式或指定的其他标准来识别进程。例如，`pkill -u binary -d "psql"` 将向由以 psql 开头的用户启动的进程发送 SIGQUIT。
除了 `kill`、`killall` 和 `pkill` 之外，还可以使用 `top` 命令来杀死进程。在 `top` 工具中，在提示时按 `k` 选择相应的 PID 和 kill 信号。

### 进程执行

你可以执行三种类型的 Linux 命令：

- 二进制程序
- Shell 脚本
- Shell 函数

大多数命令（如 `ls`、`find` 和 `grep`）都是文件系统中的二进制程序，直到执行之前存在。它们用编程语言编写并编译成计算机可以理解的二进制格式。其他命令（如 `cd` 和 `exit`）内置在运行的 shell 中，它们被称为函数。Shell 脚本也可以包含一组二进制程序、shell 函数和特殊结构，供 shell 按顺序执行。

在执行程序或 shell 脚本时，shell 会解释命令并创建一个新的 shell。这种新 shell 的创建被称为“分叉”（forking），由 Linux 中的 `fork` 函数执行。新的子 shell 使用其函数执行程序或 shell 脚本。二进制文件或 shell 脚本完成后，新 shell 使用其退出函数返回原始 shell。原始 shell 使用其函数等待新 shell 完成其规避的任务后返回。当用户在命令行使用 `ls` 命令时，用户就描述了这一过程。

```bash
root@server1 ~# jobs & 
[+] Running sample & 
root@server1 ~# ps | grep sample
2583 tty2 00:00:00 sample
root@server1 ~#
```

要终止后台进程，你可以向 PID 发送信号（如本章前面所示），也可以向后台作业 ID（job ID）发送信号。后台作业必须以 `%` 字符为缀。要向创建的后台进程发送 SIGINT 信号，可以使用以下 kill 命令：

```bash
[root@server1 ~]# jobs
[1]+ Running sample
[root@server1 ~]# kill -2 %1
[1]+ Interrupt sample
[root@server1 ~]# jobs
[root@server1 ~]# _
```

> 注意 18
> 你也可以使用 `killall -2 sample` 工具来终止前面示例中使用的后台进程。

后台进程启动后，你可以使用 `fg`（前景）命令将其移动到前台。同样，你可以通过 `Ctrl+z` 键暂停进程。然后可以使用 `bg`（后台）命令将其发送到后台。`Ctrl+z` 键会将进程分配一个后台作业 ID，该 ID 作为 `bg` 命令的参数。要在后台启动 sample 进程并将其移动到前台，然后暂停并移回后台，可以使用以下操作：

```bash
[root@server1 ~]# sample &
[root@server1 ~]# fg
[root@server1 ~]# Ctrl-z
[root@server1 ~]# bg
```

## 图 9-4 nice 值刻度表

- -20 ... 0 +19
- 最有可能获得时间片，PRI 将越接近 0
- 新进程的默认 nice 值
- 最无可能获得时间片，PRI 将越接近 127

所有用户都可以通过增加自己进程的 nice 值来降低优先级，从而对同一台计算机上的其他用户“友好”。然而，只有 root 用户有能力通过降低 nice 值来提高进程的优先级。

进程默认启动时的 nice 值为 0，正如之前的 `ps -1` 输出中的 NI 所示。要启动一个 nice 值为 -19（低优先级）的进程，可以使用 `nice` 命令并使用 `-n` 选项指定 nice 值，随后后跟启动命令。如果省略 `-n` 选项，则假设 nice 值为 0。要启动一个 nice 值为 -19 的 `ps -1`，可以执行以下命令：

```
[root@server1]# nice -n -19 ps -1
```

来自前述输出的说明：`ps` 命令的 nice 为 -19，而 `sleep` 和 `bash` 为 0；`ps` 命令的 PRI 为 99，获得的时间片比 `sleep` 和 `edit` 命令的 76 少。

相反，若要提高 `ps -1` 的优先级，可以使用以下命令：

| F S UID PID PID NI ADDR SZ WCHAN TTY TIME CMD |
|---|---|---|---|---|---|---|---|---|---|---|---|
| 4 S 0 3192 3194 0 - 12384 | pts/1 00:00:00 bash |
| 4 S 0 3896 3194 76 - 953 | pts/1 00:00:00 sleep |
| 4 S 0 3939 3194 0 - 7015 | pts/1 00:00:02 edit |
| 4 R 0 3947 3194 60 - 687 | pts/1 00:00:00 ps |

来自前述输出的说明：`ps` 命令的 nice 值为 -20，导致 PRI 为 60，相比于 bash shell 中 `sleep` 和 `edit` 命令的 76 的 PRI，它更有可能获得时间片。

> 注意 19
> 在 Linux 系统上，后台进程被赋予 nice 值 4，以降低它们获得时间片的概率。

在进程启动后，你可以使用 `renice` 命令并指定 nice 值以及要更改的进程 PID 来改变其优先级。例如，假设终端正在执行三个示例进程：
