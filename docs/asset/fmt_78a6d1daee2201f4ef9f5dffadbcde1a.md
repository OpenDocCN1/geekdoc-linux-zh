
# 任务 (JOBS)

选项：

- `--show-ids`：显示任务 ID 以及名称
- `-p, --pid=PID`：目标进程
- `-q, --quiet`：将输出仅限制为错误
- `-V, --verbose`：增加输出以包含信息
- `--help`：显示此帮助并退出
- `--version`：输出版本信息并退出

将列表替换为您想要获取更多信息的 `initctl` 命令。`start`、`stop` 和 `status` 实用程序都是 `initctl`，它们运行与其名称同名的 `initctl` 命令。

`/etc/event.d` 目录下的每个文件都定义了一个任务，并且通常包含至少一个事件和一个命令。当事件被触发时，它会执行该命令。本节描述了管理员定义的任务以及通过 Upstart 软件包安装的任务的示例。

## 管理员定义的任务

### mudat 示例

管理定义的任务使用 `exec` 关键字来执行 shell 命令行。您也可以使用该关键字执行存储在文件中的 shell 脚本或二进制可执行文件。

```
$ cat /event.d/mudat
start on runlevel 2
exec echo "Entering multiuser mode on " $(date) > /tmp/mudat.out
```

此文件定义了一个任务：当系统进入多用户模式（runlevel 2）时，它运行 `echo` shell。此命令将一个包含时间和日期的消息写入 `/tmp/mudat.out`。该 shell 使用命令替换（第 344 页）来执行 `date` 工具。在该任务运行完成后，`mudat` 任务停止并进入等待状态。在下一个示例中，`cat` 工具显示 `/tmp/mudat.out` 文件的内容，`initctl list` 报告该任务（`status` 实用程序）显示相同的信息：

```
$ cat /tmp/mudat.out
Entertering multiuser mode on Tue Jul 10 17:34:39 PDT 2007
```

```
$ sudo initctl list mudat
mudat (stop) waiting
```

如果 `exec` 命令行包含 shell 特殊字符（第 146 页），`init` 会执行 `/bin/sh` 并将命令行传递给 shell。否则，`exec` 直接执行命令行。要运行多个 shell 命令，请使用 `exec` 运行存储在文件中的 shell 脚本，或使用 `script...end script`（下文讨论）。

Upstart init 守护进程只能监控使用 `exec` 执行程序的服务的（`services`）任务。它无法监控使用 `script...end script` 运行的任务。另一种方法，需要使用 `exec` 任务的服务可以使用任一方法来运行程序。

您还可以定义并设置一个由该事件触发的任务。`myob` 任务定义文件定义了一个由 `hithere` 事件触发的任务：

```
$ cat /etc/event.d/myob
script
start on hithere
echo "Hi there, here am!" > /tmp/myob.out
date >> /tmp/myob.out
end script
```

`myob` 文件显示了另一种执行命令的方法：它在 `script` 和 `end script` 关键字之间包含了两个命令。这些关键字始终通过 `/bin/sh` 执行。这些命令将消息和日期写入 `/tmp/myob.out` 文件。您可以使用 `init` 命令来触发该任务。随后，当您触发它时，`init` 会显示 `myob` 运行时的状态：

```
$ sudo init hithere
hithere
myob (start) waiting
myob (start) starting
myob (start) pre-start
myob (start) spawned, process 6064
myob (start) post-start, (main) process 6064
myob (start) running, process 6064
myob (stop) running
myob (stop)
myob (stop) stopping
myob (stop)
myob (stop) killed
myob (stop) post-stop
myob (stop) waiting
```

```
$ cat /tmp/myob.out
Hi, here I am!
Sat Jul 7 20:19:13 PDT 2006
```

```
$ sudo initctl list myob
myob (stop) waiting
```

在前面的示例中，`cat`、`initctl start` 和 `stop` 显示了 `myob` 生成的输出并显示任务的状态。您可以使用 `initctl start myob`（或直接 `start myob`）运行相同的任务。`initctl start` 命令在您想运行一个任务时非常有用，例如运行上一个示例中的 `mudat` 任务，而不触发运行时 2 事件。

## /etc/event.d 中的任务定义文件

随着 Ubuntu 从 SysVinit 过渡到 Upstart init，`/etc/event.d` 目录中将定义更多的任务。本节描述了 Upstart 软件包（第 501 页）放入此目录的一些任务。

## 可选：使用参数指定事件

`telinit shutdown` 实用程序会发出带有参数的 runlevel 事件。例如，`shutdown` 发出 runlevel 0，而 `telinit` 发出 runlevel 2。您可以在任务定义中使用以下语法匹配这些事件：

```
start stop on event
```

其中 `event` 是一个事件，`arg` 是可选的。在任务定义中匹配这些事件可以使用以下语法：

```
start stop on event [arg]
```
