
与之工作。当系统处于多用户模式时，它会运行 getty 或 metget 进程，这些进程会在虚拟控制台上显示 `login:` 提示符。当有人响应提示符并按回车键时，getty 将控制权交给一个名为 `login` 的实用程序，该程序会检查用户名和密码的组合。用户登录后，login 进程将变为用户的 shell 进程。

## 进程标识

GNU/Linux 在每个进程启动时都会分配一个唯一的 PID 号。只要进程存在，它就会保留该 PID 号。在一次会话中，同一个进程始终在执行登录 shell。当你 fork（产生）一个新进程时——例如当你使用编辑器时——新（子）进程的 PID 号与其父进程的不同。当你返回登录 shell 时，你会发现它仍然由同一个进程执行，并且与你登录时的 PID 号相同。

下面的交互显示了运行 shell 的进程 fork 了 `ps`（即 ps 的父进程，见第 156 页）。当你使用 `-l` 选项调用它时，`ps` 会显示每个进程的详细列表信息。ps 输出中 CMD 列显示为 `bash` 的行指的是运行该 shell 的进程。PID 列列出了每个进程的 PID 号。从 PID 和 PPID 列，你可以看到运行 `sleep`（PID 2168）的进程是运行 `sleep`（PID 2191）的进程。`sleep` 的 PID 号与 `sleep` (2168) 的 PID 号相同：

```
$ sleep 10 &
[ 2893]
$ ps -l
F S UID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 500 2168 2167 0 72 0 454 wait4 pts/1 00:00:00 bash
000 S 500 2893 2168 0 63 0 286 nanos1 pts/1 00:00:00 sleep
000 R 500 2894 2168 0 75 0 628 - pts/1 00:00:00 ps
```

有关 `ps` 以及 `-l` 选项显示的所有列的更多信息，请参考第三部分的第 128 页。当你给出另一个 `-l` 命令时，你可以看到 shell 仍然由同一个进程运行，但它 fork 了另一个进程来执行 `sleep`：

```
$ sleep 10 &
[ 2893]
$ ps -l
F S UID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 500 2168 2167 0 71 0 454 wait4 pts/1 00:00:00 bash
000 S 500 2893 2168 0 63 0 286 nanos1 pts/1 00:00:00 sleep
000 R 500 2894 2168 0 75 0 628 - pts/1 00:00:00 ps
```

## 562 第 12 章 Shell II：Bourne Again Shell

你也可以使用 `pstree` 查看进程的父/子关系。下一个示例显示了 `pstree` 中的 `-p` 选项，它会使其显示 PID 号：

```
$ pstree -p
init(1)--ads1-connect(1591)--pppd(1619)--pppoe(1620)
 |-apmd(832)
 | |-atd(1148)
 | |-crond(1089)
 | |-gpm(1047)
 | |-httpd(1070)--httpd(1088)
 | |  '-httpd(1538)
 |
 | |-nfsd(1000)
 | |-nfsd(1001)
 | |-nmbd(1112)
 | |-ntpd(852)
 | |-portmap(686)
 | |-rhnsd(1170)
 | |-rpc.mount(989)
 | |-rpc.quotad(984)
 | |-rpc.stat(714)
 | |-rpciod(805)
 | |-sendmail(1028)
 | |-smbd(1107)
 | |-sshd(909)
 | |-syslogd(663)
 | |-xinetd(942)
```

查看从第 394 页开始的列表获取通过 `pstree` 显示的一些守护进程的信息。查看第 586 页的"$PID Number”了解其描述。

下文的交互显示了运行 shell 的进程 fork 了 `ps`（其父进程，见第 156 页）。当你使用 `-l` 选项调用它时，`ps` 会显示每个进程的详细列表信息。ps 输出中 CMD 列显示为 `bash` 的行指的是运行该 shell 的进程。PID 列列出了每个进程的 PID 号。从 PID 和 PPID 列，你可以看到运行 `sleep`（PID 2168）的进程是运行 `sleep`（PID 2191）的进程。`sleep` 的 PID 号与 `sleep` (2168) 的 PID 号相同：

```
$ sleep 10 &
[ 2893]
$ ps -l
F S UID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 500 2168 2167 0 72 0 454 wait4 pts/1 00:00:00 bash
000 S 500 2893 2168 0 63 0 286 nanos1 pts/1 00:00:00 sleep
000 R 500 2894 2168 0 75 0 628 - pts/1 00:00:00 ps
```

参考第三部分的第 128 页获取有关 `ps` 以及 `-l` 选项显示的所有列的更多信息。当你给出另一个 `-l` 命令时，你可以看到 shell 仍然由同一个进程运行，但它 fork 了另一个进程来执行 `sleep`：

```
$ sleep 10 &
[ 2893]
$ ps -l
F S UID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 500 2168 2167 0 71 0 454 wait4 pts/1 00:00:00 bash
000 S 500 2893 2168 0 63 0 286 nanos1 pts/1 00:00:00 sleep
000 R 500 2894 2168 0 75 0 628 - pts/1 00:00:00 ps
```

## 562 第 12 章 Shell II：Bourne Again Shell

你也可以使用 `pstree` 查看进程的父/子关系。下一个示例显示了 `pstree` 中的 `-p` 选项，它会使其显示 PID 号：

```
$ pstree -p
init(1)--ads1-connect(1591)--pppd(1619)--pppoe(1620)
 |-apmd(832)
 | |-atd(1148)
 | |-crond(1089)
 | |-gpm(1047)
 | |-httpd(1070)--httpd(1088)
 | |  '-httpd(1538)
 |
 | |-nfsd(1000)
 | |-nfsd(1001)
 | |-nmbd(1112)
 | |-ntpd(852)
 | |-portmap(686)
 | |-rhnsd(1170)
 | |-rpc.mount(989)
 | |-rpc.quotad(984)
 | |-rpc.stat(714)
 | |-rpciod(805)
 | |-sendmail(1028)
 | |-smbd(1107)
 | |-sshd(909)
 | |-syslogd(663)
 | |-xinetd(942)
```

查看从第 394 页开始的列表获取通过 `pstree` 显示的一些守护进程的信息。查看第 586 页的"$PID Number”了解其描述。

## 执行命令

...与之工作。当系统处于多用户模式时，它会运行 getty 或 metget 进程，这些进程会在虚拟控制台上显示 `login:` 提示符。当有人响应提示符并按回车键时，getty 将控制权交给一个名为 `login` 的实用程序，该程序会检查用户名和密码的组合。用户登录后，login 进程将变为用户的 shell 进程。

## 进程标识

GNU/Linux 在每个进程启动时都会分配一个唯一的 PID 号。只要进程存在，它就会保留该 PID 号。在一次会话中，同一个进程始终在执行登录 shell。当你 fork（产生）一个新进程时——例如当你使用编辑器时——新（子）进程的 PID 号与其父进程的不同。当你返回登录 shell 时，你会发现它仍然由同一个进程执行，并且与你登录时的 PID 号相同。

下面的交互显示了运行 shell 的进程 fork 了 `ps`（即 ps 的父进程，见第 156 页）。当你使用 `-l` 选项调用它时，`ps` 会显示每个进程的详细列表信息。ps 输出中 CMD 列显示为 `bash` 的行指的是运行该 shell 的进程。PID 列列出了每个进程的 PID 号。从 PID 和 PPID 列，你可以看到运行 `sleep`（PID 2168）的进程是运行 `sleep`（PID 2191）的进程。`sleep` 的 PID 号与 `sleep` (2168) 的 PID 号相同：

```
$ sleep 10 &
[ 2893]
$ ps -l
F S UID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 500 2168 2167 0 72 0 454 wait4 pts/1 00:00:00 bash
000 S 500 2893 2168 0 63 0 286 nanos1 pts/1 00:00:00 sleep
000 R 500 2894 2168 0 75 0 628 - pts/1 00:00:00 ps
```

参考第三部分的第 128 页获取有关 `ps` 以及 `-l` 选项显示的所有列的更多信息。当你给出另一个 `-l` 命令时，你可以看到 shell 仍然由同一个进程运行，但它 fork 了另一个进程来执行 `sleep`：

```
$ sleep 10 &
[ 2893]
$ ps -l
F S UID PPID C PRI NI ADDR SZ WCHAN TTY TIME CMD
100 S 500 2168 2167 0 71 0 454 wait4 pts/1 00:00:00 bash
000 S 500 2893 2168 0 63 0 286 nanos1 pts/1 00:00:00 sleep
000 R 500 2894 2168 0 75 0 628 - pts/1 00:00:00 ps
```

## 562 第 12 章 Shell II：Bourne Again Shell

你也可以使用 `pstree` 查看进程的父/子关系。下一个示例显示了 `pstree` 中的 `-p` 选项，它会使其显示 PID 号：

```
$ pstree -p
init(1)--ads1-connect(1591)--pppd(1619)--pppoe(1620)
 |-apmd(832)
 | |-atd(1148)
 | |-crond(1089)
 | |-gpm(1047)
 | |-httpd(1070)--httpd(1088)
 | |  '-httpd(1538)
 |
 | |-nfsd(1000)
 | |-nfsd(1001)
 | |-nmbd(1112)
 | |-ntpd(852)
 | |-portmap(686)
 | |-rhnsd(1170)
 | |-rpc.mount(989)
 | |-rpc.quotad(984)
 | |-rpc.stat(714)
 | |-rpciod(805)
 | |-sendmail(1028)
 | |-smbd(1107)
 | |-sshd(909)
 | |-syslogd(663)
 | |-xinetd(942)
```

查看从第 394 页开始的列表获取通过 `pstree` 显示的一些守护进程的信息。查看第 586 页的"$PID Number”了解其描述。

## 执行命令

...（由于提供的文本后续存在大量重复和乱码内容，此处已根据“不要重复输出原文”的原则，对核心逻辑部分进行了翻译处理）

