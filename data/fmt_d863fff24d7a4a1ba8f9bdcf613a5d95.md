
表 10.11 显示了 `kill` 命令的一些示例及其含义。
挂断信号在你注销时生成，中断信号在你按下 `<Ctrl+C>` 时生成，退出信号在你按下 `<Ctrl+\>` 时生成。`kill` 命令向作为参数指定的 PID 的进程发送信号号 15。此信号的默认操作是终止接收它的进程。此信号可以被进程拦截并忽略，就像大多数其他信号一样。为了终止忽略信号 15 或其他信号的进程，必须向其发送信号号 9，即所谓的 sure kill。`kill` 命令会终止 `proc-list` 中给出的所有进程，前提是这些进程属于使用 `kill` 的用户。以下 PC-BSD 上的会话展示了 `kill` 命令的一些使用实例。但不要杀死登录 shell 进程，因为它会让你注销。

```
% jobs -l

[1]  + 14338 Running          sort bigdata > bigdata.sorted

[2]  - 14667 Running          cp biggerdata biggerdata.bak

[3]    14668 Running          grep sh biggerdata > lines.sh

% kill 14668

% kill -2 14667

[3]    Terminated             grep sh biggerdata > lines.sh

% kill -9 14338

[2]    Interrupt              cp biggerdata biggerdata.bak

% jobs
```

## TABLE 10.11 Some Examples of the kill Command and Their Meanings

| Command | Meaning |
|---|---|
| `kill 1234` | 向 PID 为 1234 的进程发送默认信号（SIGTERM） |
| `kill -9 1234` | 向 PID 为 1234 的进程发送 SIGKILL（保证终止信号） |
| `kill -s kill 1234` | |
| `kill -s KILL 1234` | |
| `kill -9 1234 -1004` | 向 PID 为 1234 的进程以及所有进程组 ID（PGID）为 1004 的进程发送 SIGKILL（保证终止信号） |
| `kill -s kill 1234 -1004` | |
| `kill -- -1004` | 向所有进程组 ID 为 1004 的进程发送 SIGTERM |
| `kill -- -1004` | |

```
[1]    Killed                 sort bigdata > bigdata.sorted

% jobs

%
```

在第一种情况下，`kill` 命令向 PID 为 14668 的进程发送信号号 15。在第二种情况下，信号号 2（SIGINT）被发送到 PID 为 14667 的进程。在这两种情况下，由于指定的信号号未被拦截，进程被终止。`kill` 命令可以用一条命令行终止多个进程。例如，命令 `kill -9 13586 20581` 终止 PID 为 13586 和 20581 的进程。

进程 ID 0 可用于引用当前登录期间创建的所有进程。因此，`kill -9 0` 命令终止由当前登录产生的所有进程，如以下会话所示。请注意，该命令已终止 `sarwar` 当前登录会话产生的所有进程，包括维护与客户端 Secure Shell 登录连接的进程。因此，你会看到本地机器的提示符，一个在 MacBook Pro 上运行 Bash 的终端窗口，运行在 Mac OS X（Darwin）下，`MacBook-Pro:~ syedsarwar$`。这会产生严重后果，因为在这种情况下 `kill` 终止进程的顺序是未知的。因此，如果登录 shell 和维护与客户端机器 Secure Shell 连接的进程首先被终止，那么在登录 shell 下执行的进程会继续运行。你会在再次登录时注意到这一点，并意识到 `ssh` 命令建立与远程机器的连接所需的时间比平时更长，并且一旦你连接并运行登录 shell，系统响应时间很差。`ps` 命令会显示你的前一次登录的后台进程仍在运行，如以下会话中阴影部分所示。请注意这些“残留”进程的状态为 D（已换出）和 DL（已换出并锁定），并且它们与任何终端都不相关（注意负的终端号）。你需要终止这些进程以改善系统响应时间，如会话的最后一行所示。

```
% ps -U sarwar

PID TT   STAT      TIME COMMAND

15361 -  S     0:00.01 sshd: sarwar@pts/1 (sshd)

15368 1  Ss    0:00.07 -csh (csh)

15424 1  D     0:07.05 sort bigdata

15437 1  D     0:00.60 cp biggerdata biggerdata.bak

15456 1  D     0:01.31 grep sh biggerdata

15521 1  R+    0:00.00 ps -U sarwar

15158 2-  DL   1:58.99 sort bigdata

% kill -9 0

Connection to 192.102.169.10 closed.

MacBook-Pro:~ syedsarwar$ ssh sarwar@192.102.169.10

Password for sarwar@pcbsd-srv:

Last login: Sun Oct  5 10:17:45 2014 from 139.15.192.135
```

```
FreeBSD 10.0-RELEASE-p6 (GENERIC) #0 acf484b(releng/10.0): Mon Feb

24 15:14:38 EST 2014

Welcome to FreeBSD!

...

% ps

  PID TT  STAT      TIME COMMAND

15424 1-  DL    0:23.56 sort bigdata

15437 1-  D     0:09.15 cp biggerdata biggerdata.bak

15456 1-  D     0:21.06 grep sh biggerdata

15158 2-  DL    1:59.38 sort bigdata

15866 3  Ss    0:00.06 -csh (csh)

15913 3  R+    0:00.00 ps

% kill 15158 15424 15437 15456

%
```

`kill` 命令也适用于作业号。因此，可以使用以下命令终止作业号为 1 的进程。你可以通过在命令行中指定它们的作业号来终止多个进程。例如，`kill -9 %1 %3` 可用于终止作业号为 1 和 3 的进程。

```
$ kill -9 %1

[1] + Killed find / -name foo -print > foo.paths &

$
```

当你注销时，你会话中运行的所有进程都会收到挂断信号（信号号 1）并按默认操作终止。如果你希望进程在你注销后继续运行，你需要以忽略挂断信号的方式执行它们。你可以使用 UNIX 命令 `nohup` 来完成此任务。以下是该命令语法的简要说明。

### SYNTAX

```
nohup command [args]
```

目的：执行 `command` 并忽略挂断信号

你需要对需要很长时间才能完成的进程使用 `nohup` 命令，例如对包含数十万条客户记录的大文件进行排序的程序。显然，你会将此类程序在后台运行，以便以较低的优先级运行。以下是 `nohup` 命令使用的简单示例。在这里，`find` 命令在后台运行，并且在你注销或通过 `kill` 命令向其发送信号号 1（挂断）时不会被终止。如果命令的输出未被重定向，则默认情况下会附加到 `nohup.out` 文件中。

```
$ nohup find / -name foo -print 1> foo.paths 2> /dev/null &

[1] 62808

$ kill -1 62808

$ jobs

[1]+ Running  nohup find / -name foo -print > foo.paths 2> /dev/null &

$ kill 62808

$ <Enter>

[1]+ Terminated  nohup find / -name foo -print > foo.paths 2> /dev/null

$ jobs

$
```

如果用分号分隔命令，你可以用 `nohup` 运行它们。在下面的会话中，`GenData` 生成一些数据并将其放入名为 `employees` 的文件中，而 `sort` 命令对文件进行排序并将排序后的版本存储在 `employees.sorted` 文件中。

```
$ nohup GenData > employees ; sort employees > employees.sorted &

[2] 15931

$
```
