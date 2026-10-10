
要学习系统何时启动的，可以使用 `who -b`；要查看运行级别信息，可以使用 `who -r` 命令。

```
root@kemal:-# who -b
system boot 2015-09-18 10:14
root@kemal:-# who -r
acılış-seviyesi 5 2015-09-18 10:15
```

特别是使用 `whoami` 命令，我们可以轻松地看到此时在系统中以何种身份工作。你可能会问为什么我们需要它。如果你只在自己的系统中工作，那么确实没有需要，但如果你作为多用户系统的管理员工作，你可能非常需要它。

现在让我们看看如何冒充他人的身份。对于 root 用户来说已经没有限制，因此他们可以使用任何用户的身份执行任何进程。然而，如果其他用户想以 root 或另一个用户的 ID 进行处理，他们必须知道密码。要冒充其他用户的 ID，我们基本上使用 `su` 命令。它们的工作原理如下：

- `su <user_name>` 切换到另一个用户 ID。
- `su - <user_name>` 既切换到另一个用户的 ID 又在他/她的 shell 中开始工作。

```
root@kemal:-# su zeynep
zeyep@kemal:/root$ whoami
zeyep
zeyep@kemal:/root$ exit
root@kemal:-# _
```

正如你通过 `su zeynep` 命令看到的，我们开始以 zeynep 的身份工作。当我们要退出时，使用了 `exit` 命令。因为我们是 root 用户，所以它没有询问密码。让我们看看 `su - zeynep` 命令。

```
root@kemal:-# su - zeynep
zeyep@kemal:-$ whoami
zeyep
zeyep@kemal:-$ _
```

我们提到，如果一个普通用户想以 root 或另一个用户的身份工作，他 必须知道密码。让我们做一个示例。

```
zeynep@kemal:-$ su - root
Parola:
root@kemal:-# _
```

在任何用户的 ID 下，如果你想冒充 root ID，你可以可以使用 `su` 或 `su -` 命令。当然，你必须输入 root 的密码。正如我之前提到的，你可以通过 `su` 命令成为另一个用户，但你仍然在自己的目录中工作。使用 `su -` 命令，你可以同时做到这两点：成为该用户并在他/她的目录中工作。

```
zeyep@kemal:-$ su
Parola:
root@kemal:/home/zeynep# exit
zeynep@kemal:-$ su -
Parola:
root@kemal:-# _
```

## 进程

进程是指文件运行状态的名称。当你运行一个程序时，它会被加载到内存中。除了我们在系统中启动的进程外，系统中有很多服务和服务进程正在运行。同时运行程序可能包含多个进程。

我们使用 `ps` 命令来查看任何正在运行的进程。要学习此命令的参数，可以使用 `ps --help` 命令。

```
root@local~$ ps aux
USER       PID CPU VSZ RSS TTY START COMMAND
root      1 0.1 24184 ? S 23:36 [/bin/init
root      7 0.0 0 ? S 23:36 [thread]
root      3 0.0 0 ? S 23:36 [kthread]
root      5 0.0 0 ? S 23:36 [kworker/events]
root      7 0.0 0 ? S 23:36 [rcu_sched]
root      8 0.0 0 ? S 23:36 [rcu_bh]
root      9 0.0 0 ? S 23:36 [migration]
root     10 0.0 0 ? S 23:36 [watchdog]
root     11 0.0 0 ? S 23:36 [khelper]
```

当然，为了达到最好的效果，使用参数是一个更好的主意。我们可以使用如下命令：

- `ps`: 与活动用户相关的进程。
- `ps -e`: 系统中运行的所有进程。
- `ps -e` 或 `ps -f`: 用于系统中运行进程的详细列表。
- `ps -u <user>`: 与特定用户相关的进程。

如果我们希望看到所有进程以获取我们想要查看的进程。为了获取关于进程的信息，可以使用 `ps aux`。

```
root@local:~# ps aux
root      1 0.1 24184 ? S 23:36 [/bin/init
root      7 0.0 0 ? S 23:36 [thread]
root      3 0.0 0 ? S 23:36 [kthread]
root      5 0.0 0 ? S 23:36 [kworker/events]
root      7 0.0 0 ? S 23:36 [rcu_sched]
root      8 0.0 0 ? S 23:36 [rcu_bh]
root      9 0.0 0 ? S 23:36 [migration]
root     10 0.0 0 ? S 23:36 [watchdog]
root     11 0.0 0 ? S 23:36 [khelper]
```

特别是使用 `whoami` 命令，我们可以轻松地看到此时在系统中以何种身份工作。你可能会问为什么我们需要它。如果你只在自己的系统中工作，那么确实没有需要，但如果你作为多用户系统的管理员工作，你可能非常需要它。

如果你关注命令的输出，我们必须查看最近使用的进程。为了避免这种情况，我们可以尝试以下命令。

```
root@kemal:~# ps aux | grep 'ssh'
root      819 0.0 6412 24 7 Ss 23:07 /usr/bin/ssh-agent /dbus-agent-exit-with-session-classic
```

### Ptree

为了以分级列表查看系统进程，可以使用 `ptree` 或 `ps -forest` 命令。

```
root@kemal:~# ptree
systemd--ModemManager--gdbus
               |{gmain}
           -NetworkManager--NetworkManager
                                     |{gdbus}
                                     |{gmain}
           -accounts-daemon--gdbus
                                     |{gmain}
               -agetty
               -at-spi-bus-laun--dbus-daemon
                                     |--dconf worker
                                     |--gdbus}
                                     |{gmain}
```

如果你想查看带有 PID 数字的进程，可以使用 `ptree -p` 命令。
