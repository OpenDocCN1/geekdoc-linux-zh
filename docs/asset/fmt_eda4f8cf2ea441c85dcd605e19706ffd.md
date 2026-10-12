
其中 `event` 是一个如 `runlevel` 所示的事件名称，而 `arg` 是一个或多个参数。若想在系统从运行级别 1 进入运行级别 2 时停止某个任务，请指定 `stop on runlevel 2 1`。你也可以使用 `[235]` 来匹配 2、3 和 5，或者使用 `[!2]` 来匹配除 2 以外的任何值。

事件参数：尽管 Upstart 会忽略事件中的额外参数，但在任务定义文件中的事件名称中的额外参数必须存在。例如，任务定义中的 `runlevel`（无参数）匹配所有运行级别事件（无论参数是什么），而 `runlevel arg1 arg2` 则不匹配任何运行级别事件，因为 `runlevel` 接受两个参数（系统正在进入的运行级别和之前的运行级别）。

# `/etc/init` 中的任务定义文件

随着 RHEL 继续从 SysV 向 Upstart init 过渡，将会有任务被定义在 `/etc/init` 目录中。本节描述了该目录中 upstart 软件包的某些任务。

## init 守护进程

`rc` 任务：运行级别事件（`[runlevel(7) man page]`）会信号运行级别的变化，并由运行级别 级别的 `telinit`（第 449 页）和 `shutdown`（第 453 页）发出。此事件将环境变量 `RUNLEVEL` 设置为新运行级别的值。

`/etc/init/rc.conf` 任务文件定义了 `rc` 任务。该任务监控运行级别事件。关键字 `task` 指明这是一个任务（`task`）而非服务（`service`）。因为它是一个任务，它会阻塞发出运行级别事件的调用，直到 `rc` 任务运行完毕。

`rc.conf` 中的 `exec` 语句使用 `runlevel` 参数调用 `/etc/rd/rc` 脚本（而非 `rc` 任务）。该 `rc` 脚本调用 `/etc/rd/rc.d` 目录中的链接，其中 `n` 等于 `RUNLEVEL`（第 442 页）。因此，当带有 `RUNLEVEL` 为 2 被调用时，`rc` 任务会运行 `/etc/rd/rc2.d` 中链接指向的 init 脚本。

当系统进入运行级别 0 到 6 之间时，`rc` 任务会运行 `rc` 脚本（通过 `start on runlevel [0123456]`）。通常情况下，该任务在完成 `rc` 脚本后终止。

`stop (on runlevel [!RUNLEVEL])` 处理了当 `rc` 任务正在运行 `rc` 脚本时，第二个运行级别事件尝试启动的情况。在这种情况下，`RUNLEVEL` 的值不等于调用 `rc` 任务时的 `RUNLEVEL` 值，此时 `rc` 任务会停止。

```bash
$ /etc/init/rc.conf - System V运行级别兼容性

# 此任务运行旧的 sysv-rc 运行级别脚本。

# 它通常由 telinit 兼容封装器启动。

start on runlevel [0123456]

stop on runlevel [!RUNLEVEL]

task

export RUNLEVEL

console

output

exec /etc/rd/rc $RUNLEVEL
```

`tty` 服务：遵循监控 `getty` 的服务的任务定义文件（第 451 页）。`tty.conf` 在系统进入多用户模式时启动这些进程。

```bash
$ /etc/init/tty.conf

# tty - getty

# 此服务在指定的设备上维持一个 getty。

stop on runlevel [0123456]

respawn

instance $TTY

exec /sbin/getty $TTY
```

任务定义文件中的 `stop` 语句处理了系统进入运行级别的情况。`tty.conf` 在系统进入多用户模式时启动这些进程。

# initcl 的启动和停止

在前面的示例中，`cat` 显示了 `myjob` 生成的输出，而 `initcl` 显示了任务的状态。你可以通过执行命令 `initcl start myjob`（或直接执行 `start myjob`）来运行相同的任务。当你想在不触发事件的情况下运行任务时，`initcl start` 命令非常有用。例如，你可以使用命令 `initcl start mudat` 来运行上一个示例中的 `mudat` 任务，而不会触发运行级别事件。

# 事件

`upstart` 软件包定义了许多事件。以下命令列出了事件及其简要描述。有关每个事件的更多信息，请参见相应的页面。

```bash
$ apropos event | grep signalling

control-alt-delete (7) - 信号控制台按下 Control-Alt-Delete 的事件

keyboard-request (7) - 信号控制台按下 Alt-KeyUp 的事件

power-status-changed (7) - 信号电源状态变化的事件

runlevel (7) - 信号运行级别变化的事件

started (7) - 信号任务正在运行的事件

starting (7) - 信号任务正在启动的事件

startup (7) - 信号系统启动的事件

stopped (7) - 信号任务已停止的事件

stopping (7) - 信号任务正在停止的事件
```
