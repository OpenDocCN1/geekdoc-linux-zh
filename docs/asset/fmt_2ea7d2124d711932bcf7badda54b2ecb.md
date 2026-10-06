
> 注意
> 你也可以使用 `top` 工具来更改优先级。

# 调度（Scheduling）

使用 `renice` 命令并指定 nice 值的变化以及要更改进程的 PID，可以在进程启动后改变其优先级。例如，假设终端上正在运行三个示例进程：

（此处省略上文代码块内容）

要通过将 nice 值从 0 更改为 +15 来降低两个示例进程的优先级并查看新值，你可以执行以下命令：

（此处省略上文代码块内容）

> 注意
> `at` 在执行调度命令时使用当前 shell 环境；调度的命令存储在 `/var/spool/at`。如果通过 `at` 调度任何命令的标准输出没有重定向到文件，它将发送给用户。你可以通过在提示符输入 `mail` 来检查本地邮件。关于 `mail` 工具的更多信息可以在其 man 页或 info 页中找到。

使用 `at` 调度 nice 值为 4 的后台进程（默认值）可以降低它们获得时间片的概率。

你不能直接更改 `PRI`，但可以通过为进程分配特定的值来间接影响它。负值会增加进程获得更多时间片的概率，而正的 nice 值则相反。nice 值的取值范围如图 10-4 所示。

从上一个输出中可以注意到，`ps` 命令的 nice 值为 -20，导致 `PRI` 为 60，这比 `sleep` 和 `gedit` 命令的 76 `PRI` 以及 `bash` 壳的 75 `PRI` 更有可能获得时间片。

# 第 10 章 管理 Linux 进程（MANAGING LINUX PROCESSES）

> 注意
> 在某些 Linux 系统上，后台进程默认的 nice 值为 4，以降低它们获得时间片的概率。

在进程启动后，你可以使用 `renice` 命令并指定要更改的 nice 值以及要更改进程的 PID 来改变其优先级。例如，假设终端上正在运行三个示例进程如下：

（代码块略...）

要通过将 nice 值从 0 更改为 +15 来降低两个示例进程的优先级并查看新值，你可以执行以下命令：

（代码块略...）

> 注意
> 你也可以使用 `top` 工具来更改优先级。

```bash
LOGNAME=root; export LOGNAME

LESSOPEN=/usr/bin/lespipe.sh %s; export LESSOPEN

G_BROKEN_FILENAMES=1; export_BROKEN_FILENAMES

COLORTERM=gnome-terminal; export COLORTERM

XAUTHORITY=/root/.xauthority; export XAUTHORITY

cd /root || (
  echo 'Execution directory inaccessible' >&2
  exit 1
)

$(SHELL::/bin/sh) << `(dd if=/dev/urandom count=200 bs=1>/dev/null|LC_ALL=C tr -d -c '[:alnum:]')`
date >/root/atfile
who >>/root/atfile
[root@server1]# _
```

要删除上例中的任务，只需在 `at` 命令后指定 `-d` 选项，然后跟相应的 at Job ID，如下输出所示：

```bash
[root@server1]# at -d 1
[root@server1 root]# at -d 1
[root@server1]# _
```

# 注意事项

> 或者，使用 `atrm 1` 命令来删除第一个 at 任务；`atrm` 命令是 `at -d` 命令的快捷方式。

如果有许多命令需要使用守护进程（daemon）调度，你可以将这些命令放在一个 shell 脚本中，并使用 `at` 命令的 `-f` 选项调度该 shell 脚本在稍后执行。调度名为 `myscript` 的 shell 脚本示例：

```bash
[root@server1 root]# cat myscript
#this is a sample shell script
date >/root/atfile
who >>/root/atfile
[root@server1]# at 10:15pm July 16 -f myscript
job 2 at 2004-07-26 22:15
[root@server1]# _
```
