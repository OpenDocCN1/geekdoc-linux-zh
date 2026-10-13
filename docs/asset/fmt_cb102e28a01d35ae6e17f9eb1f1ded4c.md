
[2]- Terminated controljob2

[3]+ Terminated controljob3

```
使用 `kill` 向一个或多个进程发送信号。`kill` 命令的选择标准包括：

- Command - 匹配模式的进程。
- UID - Linux 用户拥有的进程。
- GID - Linux 组拥有的进程。
- Parent - 特定父进程的进程。
- Terminal - 在特定终端运行的进程。
```

```
[user@host-$] ps aux | grep job

5992 0.0 0.1 222448 3040 pts/1 S 16:59 0:00 /bin/bash /home/user/bin/controljob1

5996 0.0 0.1 222448 3048 pts/1 S 16:59 0:00 /bin/bash /home/user/bin/controljob2

6884 0.0 0.1 222448 3048 pts/1 S 16:59 0:00 /bin/bash /home/user/bin/controljob3
```

## 监控和管理 Linux 进程

```
[user@host ~] kill kill1

[1] Terminated controlkill1

[2]- Terminated controljob2
```

```
[user@host ~] ps aux | grep kill

user      6219 0.0 0.1 221860 1052 pts/1 S+ 17:00 0:00 grep --color=auto kill1
```

[3]+ Terminated controljob3

```
[user@host ~] ps aux | grep test

user      6281 0.0 0.1 222448 3012 pts/1 S 17:04 0:00 /bin/bash /home/user/bin/controltest1

user      6285 0.0 0.1 222448 3128 pts/1 S 17:04 0:00 /bin/bash /home/user/bin/controltest2

user      6290 0.0 0.1 222448 3064 pts/1 S 17:04 0:00 /bin/bash /home/user/bin/controltest3

user      6318 0.0 0.1 221860 1080 pts/1 S+ 17:04 0:00 grep --color=auto test
```

```
[user@host ~] kill -u user
```

```
[user@host ~] ps aux | grep test

user      6870 0.0 0.1 221860 1048 pts/1 S 17:07 0:00 grep --color=auto test
```

```
[user@host ~]
```

## 管理性注销用户

你可能因为各种原因需要注销其他用户。列举几种可能的情况：用户违反了安全规定；用户可能耗尽了资源；系统可能无响应；或者他们访问了敏感材料。在这种情况下，你可能需要使用信号管理性地终止他们的会话。

要注销用户，首先识别要终止的会话。使用 `w` 命令列出登录用户和当前运行的进程。注意 `TTY` 和 `FROM` 列，以确定要关闭的会话。

所有用户登录会话都关联到一个终端设备（TTY）。如果设备名称格式为 `pts/N`，则它是与图形终端或远程登录会话相关的伪终端。如果格式为 `ttyN`，则用户位于系统控制台、备用控制台或直接连接的终端。

## 重要提示

管理员通常过快地使用了 `SIGKILL` 信号。

由于 `SIGKILL` 信号无法被捕获或忽略，因此它始终是致命的。然而，若要在不允许进程运行自清理程序的情况下终止进程，建议先发送 `SIGTERM`，首先尝试 `SIGINT`，只有在两者都失败时再使用 `SIGKILL` 进行重试。

首先，使用 `pgrep` 识别要杀掉的 `PID`，它的工作方式与 `pkill` 非常相似，包含相同的选项，区别在于 `pgrep` 是列出进程而不是杀死它们。

```
[root@host #] pgrep -1 -u bob

6964 bash

6998 sleep

6999 sleep

7000 sleep
```

```
[root@host #] pkill SIGKILL -u bob
```

```
[root@host #] pgrep -1 -u bob
```

```
[root@host #]
```

当需要处理的进程处于同一个会话时，没有必要杀死用户的所有进程。使用 `w` 命令确定会话的控制终端，然后只杀死引用相同终端 ID 的进程。除非指定了 `SIGKILL`，否则会话领导进程（在此处为 Bash 登录 shell）会成功处理并存活终止请求，而所有其他进程将被终止。

```
[root@host #] pgrep -1 -u bob

7391 bash

7426 sleep

7427 sleep

7428 sleep
```

```
[root@host #] w -h -u bob

tty3 18:37 5:04 0.03s 0.03s -bash
```

```
[root@host #] pkill -t tty3
```

```
[root@host #] pgrep -1 -u bob

7391 bash
```

```
[root@host #] pkill SIGKILL -t tty3
```

```
[root@host #] pgrep -1 -u bob
```

```
[root@host #]
```

同样可以使用父子关系来应用这种选择性的进程终止。使用 `pstree` 命令查看系统或单个用户的进程树，获取父进程的 `PID`，以杀死其创建的所有进程。在那里，父进程 Bash 登录 shell 会存活，因为信号只指向了它的子进程。

```
[root@host #] pstree -p bob

bash(8391)--sleep(8425)

  └─sleep(8426)

  └─sleep(8427)
```

```
[root@host #] pkill -P 8391
```

```
[root@host #] pgrep -1 -u bob
```

![](img/59afb92e10b67a9cecc358a2c65e93b5_278_0.png)

```
bash(8391)
```

```
[root@host ~]# pkill -SIGKILL -P 8391
```

```
[root@host ~]# pgrep -l -u bob

bash(8391)
```

```
[root@host ~]#
```

# 参考文献

`info libc` `signal` (GNU C Library Reference Manual)

- - 第 24 ：信号处理

`info libc` `processes` (GNU C Library Reference Manual)

- - 第 26 ：进程

`kill(1)`, `killall(1)`, `pgrep(1)`, `pkill(1)`, `pstree(1)`, `signal(7)`, and `w(1)` 手页

## 引导练习

# 杀死进程

在本次练习中，你将使用信号来管理和停止进程。

### 预期结果

你应该能够启动和停止多个 shell 进程。

# 准备工作

使用密码 `student` 以 `student` 身份登录工作站。

在工作站上，运行 `lab processes-kill start` 命令。该命令会运行一个启动脚本，用于判断主机 `servera` 在网络上是否可达。

```
[student@workstation ~]$ lab processes-kill start
```

- 1. 在工作站上，并排打开两个终端窗口。在本节中，这些终端被称为**左侧**和**右侧**。在每个终端中，使用 `ssh` 命令以 `student` 身份登录 `servera`。

```
[student@workstation ~]$ ssh student@servera

Activate the web console with: systemctl enable -- cockpit.socket

Last login: Fri Feb 8 12:04:52 2019 from 172.25.2.50

[student@servera ~]
```

- 2. 在左侧窗口中，创建一个名为 `/home/student/bin` 的新目录。在新目录中创建一个名为 `killing` 的脚本。赋予该脚本可执行权限。

```
[student@servera ~]$ mkdir /home/student/bin
```

- 2.2. 使用 `vim` 命令在 `/home/student/bin` 目录下创建一个名为 `killing` 的脚本。按 `I` 进入交互模式。使用 `:wq` 命令保存文件。

```bash
[student@servera ~]$ vim /home/student/bin/killing

#!/bin/bash
```
