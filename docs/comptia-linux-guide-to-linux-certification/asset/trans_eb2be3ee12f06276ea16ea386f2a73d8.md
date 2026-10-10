

# 第 9 章 管理 Linux 进程

```
root      5  2 0 21:22 ? 00:00:00 [kworker/0:0H]
root      6  2 0 21:22 ? 00:00:00 [kworker/u128:0]
root      7  2 0 21:22 ? 00:00:00 [migration/0]
root      8  2 0 21:22 ? 00:00:00 [rcu_bh]
root      9  2 0 21:22 ? 00:00:00 [rcu_sched]
root     10  2 0 21:22 ? 00:00:00 [watchdog/0]
root     11  2 0 21:22 ? 00:00:00 [khelper]
root     12  2 0 21:22 ? 00:00:00 [kdevtmpfs]
root     13  2 0 21:22 ? 00:00:00 [netns]
root     14  2 0 21:22 ? 00:00:00 [writeback]
root    394  1 0 21:22 ? 00:00:00 /sbin/auditd -n
root    407 394 0 21:22 ? 00:00:00 /sbin/audispd
root    409 407 0 21:22 ? 00:00:00 /usr/sbin/sedispatch
root    411  1 0 21:22 ? 00:00:00 /usr/sbin/alsacl1 -s -n
root    418  1 0 21:22 ? 00:00:00 /sbin/rngd -f
root    420  1 0 21:22 ? 00:00:00 /usr/sbin/ModemManager
avahi   422  1 0 21:22 ? 00:00:00 avahi-daemon: running
dbus    424  1 0 21:22 ? 00:00:00 /bin/dbus-daemon --system
chrony  430  1 0 21:22 ? 00:00:00 /usr/sbin/chronyd -u
root    431  1 0 21:22 ? 00:00:00 /usr/sbin/crond -n
root    432  1 0 21:22 ? 00:00:00 /usr/sbin/atd -f
root    435  1 0 21:22 ? 00:00:00 /usr/sbin/abrted -d -s
root    437  1 0 21:22 ? 00:00:00 /usr/bin/abrt-watch-log
root    441  1 0 21:22 ? 00:00:00 /usr/sbin/gdm
root    446  1 0 21:22 ? 00:00:00 /usr/sbin/mcelog
root    481 441 0 21:22 ? 00:00:00 /usr/libexec/gdm-simple-
polkitd 482  1 0 21:22 ? 00:00:00 /usr/lib/polkit-1/polkitd
root    488 481 0 21:22 tty1 00:00:00 /usr/bin/Xorg : 0
root    551 481 0 21:22 ? 00:00:00 gdm-session-worker
root    552  1 0 21:22 ? 00:00:00 /usr/bin/NetworkManager
gdm     842 823 0 21:23 ? 00:00:00 (sd-pam)
gdm     852 551 0 21:23 ? 00:00:00 /usr/bin/gnome-session
gdm     856  1 0 21:23 ? 00:00:00 /usr/bin/dbus-launch
root   1018  1 0 21:23 ? 00:00:00 /bin/dbus-daemon --fork
root   1020 552 0 21:23 ? 00:00:00 /sbin/dhclient -d -sf
gdm    1025  1 0 21:23 ? 00:00:00 /usr/libexec/at-spi-bus
gdm    1045 1025 0 21:23 ? 00:00:00 /bin/dbus-daemon
root   1072  1 0 21:23 ? 00:00:00 /usr/libexec/upowerd
gdm    1077 852 0 21:23 ? 00:00:03 gnome-shell --mode=gdm
colord  1080  1 0 21:23 ? 00:00:00 /usr/libexec/colord
gdm    1087  1 0 21:23 ? 00:00:00 /usr/bin/pulseaudio
gdm    1114 1111 0 21:23 ? 00:00:00 /usr/libexec/ibus-daemon
gdm    1122 1111 0 21:23 ? 00:00:00 /usr/libexec/ibus-engine
gdm    1148  1 0 21:23 ? 00:00:00 /usr/libexec/goa-daemon
root   1164  1 0 21:23 ? 00:00:00 login -- root
root   1174 1171 0 21:23 ? 00:00:00 (sd-pam)
root   1175 1164 0 21:23 tty2 00:00:00 -bash
root   1208  2 0 21:28 ? 00:00:00 [kworker/0:0]
root 1213 1 0 21:31 ? 00:00:00 /usr/sbin/sshd -D
root 1216 1213 0 21:32 ? 00:00:00 sshd: root@pts/0
root 1220 1216 0 21:32 pts/0 00:00:00 -bash
root 1253 2 0 21:33 ? 00:00:00 [kworker/0:2]
root 1260 1 0 21:33 ? 00:00:00 /usr/libexec/packagekitd
root 1742 1220 0 21:33 pts/0 00:00:00 ps -ef
[root@server1 -]# _
```

如上所示的输出，内核线程守护进程（kthreadd）的 PID 为 2，并启动了实际 Linux 内核中的大多数子进程，因为这些子进程的 PPID 为 2；而 init 守护进程（/usr/lib/systemd/systemd，PID = 1）则启动了大多数其他守护进程，因为这些守护进程的 PPID 为 1。此外，由于守护进程和内核子进程不在终端上运行，因此在 TTY 列中显示为 ?。

由于在 Linux 服务器上 `ps -ef` 命令的输出可能长达数百行，通常会将输出通过管道传递给 `less` 命令以分页显示在终端屏幕上，或者传递给 `grep` 命令，后者可用于仅显示包含特定信息的行。例如，要仅显示系统上的 BASH shell，可以使用以下命令：

```
[root@server1 -]# ps -ef | grep bash
user1 2094 2008 0 01:29:35 pts/1 00:00:00 -bash
root 2159 2156 0 14:30 t2 00:00:00 -bash
root 2294 2159 0 14:44 t2 00:00:00 grep --color=auto bash
[root@server1 -]# _
```

请注意，在前面的输出中，`grep bash` 命令也与其他 BASH shell 一起显示，因为在执行 `ps` 命令时它正在内存中运行。但这并不总是如此，因为 Linux 内核会根据多种因素安排命令执行。

`-e` 和 `-f` 选项是与 `ps` 命令配合使用最常见的选项；然而，还有许多其他选项可用。`ps` 命令的 `-l` 选项比 `-f` 选项列出关于每个进程的更多详细信息。以下输出展示了使用此选项查看终端 `tty2` 中的进程的示例：

```
[root@server1 -]# ps -l
F S UID PID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
4 S 0 2159 2156 0 80 0 - 1328 wait t2 00:00:00 bash
4 R 0 2295 2159 2 80 0 - 744 - t2 00:00:00 ps
[root@server1 -]# _
```

进程标志（F）表示进程的特征；前面输出中的标志 4 表示该进程由 root 用户运行。进程状态（S）列对系统管理员最有价值，因为它指示进程当前正在做什么。如果进程当前未在处理器上运行，你会在进程状态列看到 S（睡眠）；如前面输出中的 bash 所示，进程大部分时间都处于此状态。如果进程当前正在处理器上运行，你会在该列看到 R；如果进程已停止或正在被其他进程跟踪，则会看到 T。除了这些状态外，你还可能在该列看到 Z，表示僵尸进程。当进程执行完成后，父进程必须检查其是否成功执行以提高效率，然后释放子进程的 PID，以便其可以被再次使用。在进程等待父进程释放 PID 期间，该进程被称为处于僵尸状态，因为它已经结束但仍保留 PID。在繁忙的 Linux 服务器上，僵尸进程会积累并阻止新进程创建；如果发生这种情况，你可以简单地杀死僵尸进程的父进程，如下节所述。

![](img/c27875544958897d817484d558c208c8_422_0.png)

僵尸进程也被称为失效进程（defunct processes）。

![](img/c27875544958897d817484d558c208c8_422_1.png)

要查看整个系统上僵尸进程列表，可以使用 `ps -ef | grep Z` 命令。

进程优先级（PRI）是内核用于该进程的优先级；它介于 0（高优先级）到 127（低优先级）之间测量。nice 值（NI）可间接影响进程优先级；它介于 -20（获得较高优先级的几率更大）到 19（获得较低优先级的几率更大）之间测量。前面输出中的 ADDR 指示进程的内存地址，而 WCHAN 指示进程睡眠时在等待什么。此外，还列出了进程在内存中的大小（SZ），单位为千字节；通常，它大致相当于文件系统中可执行文件的大小。

`ps` 命令的某些选项不以连字符开头；这些被称为 Berkeley 风格选项。其中最常见的是 `a` 选项，它列出所有终端上的进程，以及 `x` 选项，它列出不运行在终端上的进程，如下面输出所示，显示了系统前 10 个进程：

```
[root@server1 ~]# ps ax | head -11

PID   TTY    STAT      TIME COMMAND
1 ?   S      0:01 /usr/lib/systemd/systemd
2 ?   S      0:00 [kthreadd]
3 ?   S      0:00 [migration/0]
4 ?   S<     0:00 [ksoftirqd/0]
5 ?   S      0:00 [watchdog/0]
6 ?   S      0:00 [migration/1]
7 ?   S      0:00 [ksoftirqd/1]
8 ?   S      0:00 [watchdog/1]
9 ?   S      0:00 [events/0]
10 ?  S      0:00 [events/1]

[root@server1 ~]# 
```

刚才列出的列与前面讨论的列等价；然而，进程状态列由 STAT 标识，可能包含额外字符以指示进程状态的完整性质。例如，`w` 表示进程在内存中没有内容，`<` 符号表示高优先级进程，而 `N` 表示低优先级进程。

