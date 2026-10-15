
这一行显示 `tty` 任务正在运行，且进程 ID `1634` 正在执行该任务。（并不是所有服务作业都有关联进程。）

> 如果你知道任务名称，可以直接使用 `initctl status <job_name>` 查看其状态。

`initctl` 输出中的状态部分（例如 `stop/waiting`）可能会令人困惑。左侧（`/` 之前）是目标，即任务应该努力实现的目标，如 `start` 或 `stop`。右侧是当前的任务状态，或任务现在正在执行的操作，例如 `waiting`（等待）或 `running`（运行）。在前面的列表中，`tty1` 任务的状态是 `start/running`，意味着它的目标是 `start`。`running` 状态表示它已成功启动。（对于服务作业，`running` 状态是常态。）

`mountall` 的情况稍有些，因为任务不会一直保持运行。`stop/waiting` 状态通常表示任务已启动并完成了它的任务。在完成任务后，它从 `start` 目标移动到 `stop` 目标，现在正在等待 Upstart 的进一步指令。

遗憾的是，如前面所述，因为从未启动的任务也具有 Upstart `stop/waiting` 状态，除非启用调试并按照第 6.5.5 节所述查看日志，否则你无法真正判断任务是已经运行过还是从未启动。

你不会在系统上看到使用 Upstart 兼容性功能启动的任务。

## 任务状态转换

有很多任务状态，但有一套固定的方法在它们之间移动。例如，这里是典型任务是如何启动的：

1. 所有任务都从 `stop/waiting` 状态开始。
2. 当用户或系统事件启动一个任务时，任务的目标从 `stop` 变为 `start`。
3. Upstart 将任务的状态从 `waiting` 变为 `starting`，因此状态现在是 `start/starting`。
4. Upstart 触发一个 `starting` 任务事件。
5. 任务执行它需要执行的所有操作。
6. Upstart 将任务的状态从 `starting` 变为 `pre-start`。
7. 任务在 `pre-start` 状态下执行其需要的操作。
8. Upstart 触发一个 `pre-start` 任务事件。
9. Upstart 将任务的状态从 `pre-start` 变为 `running`。
10. 任务在 `running` 状态下执行其需要的操作。
11. Upstart 触发一个 `running` 任务事件。
12. 任务完成其需要的操作。
13. Upstart 将任务的状态从 `running` 变为 `stopping`。
14. Upstart 触发一个 `stopping` 任务事件。
15. 任务在 `stopping` 状态下执行其需要的操作。
16. Upstart 将任务的状态从 `stopping` 变为 `stopped`。
17. Upstart 触发一个 `stopped` 任务事件。

查看 `startup-events(7)` 手页可以了解状态转换细节。

## 6.5.3 Upstart 配置

让我们检查两个配置文件：一个是任务作业，另一个服务作业。正如所有 Upstart 配置文件一样，它们位于 `/etc/init`，并名为 `mountall.conf` 和 `tty.conf`。

为了开始，请打开 `mountall.conf` 文件。在第一个语句中寻找如下行：

```
description    Mount filesystems on "boot"
```

该语句提供了任务的简短描述。接下来你会看到描述任务如何启动的几个语句：

```
start on startup

stop on rc5
```

在这里，第一行告诉 Upstart 在接收到 `startup` 事件（Upstart 发出的初始事件）时启动任务。第二行告诉 Upstart 在进入单用户模式（`rc5` 事件）时终止任务。

接下来的两行告诉我们 任务的行为：

```
expect daemon

task
```

`task` 语句告诉 Upstart 这是一个任务，因此任务会在某个时刻完成。`expect` 语句很关键，它意味着 `mountall` 将产生一个独立运行的守护进程。Upstart 需要知道这一点，因为它必须知道进程何时终止（我们将在第136页的“进程跟踪”中详细讨论）。

`mountall.conf` 文件继续带有多个 `emits` 语句，指示该任务产生了以下事件：

- emits virtual-filesystems
- emits local-filesystems
- emits remote-filesystems
- emits all-swaps
- emits filesystem
- emits mounting
- emits mounted

正如第 6.5.1 节所述，尽管存在这些行，但这不是事件的实际来源。你需要搜索任务脚本来寻找它们。

你可能还会看到一个指定 Upstart 应该将输出发送到何处的语句：

```
console output
```

通过 `output` 参数将 `mountall` 任务的输出发送到系统控制台。
现在来看任务本身的细节——在这种情况下，是一个脚本：

```
script

- /etc/default/rcs

- [f /forcefsck] && force_fck="--force-fsck"

- ["$FSCKFIX="yes" && fsck_fix="fsck-fix"]
```

```
# set $LANG so that messages are translated in plymouth

if [ -r /etc/default/locale ]; then

  /etc/default/locale

  export LANG LANGUAGE LC_ALL

fi
```

```
exec mountall --daemon $force_fsck $fsck
```

这是一个脚本（第11章），大部分内容是准备工作——设置语言并确定是否需要运行 fsck。脚本底部的 `exec mountall` 命令才是实际发生的地方。该命令挂载文件系统并在完成后发出任务事件。

### 服务任务：tty

`tty` 服务任务要简单得多；它控制一个虚拟控制台登录提示符。它的整个配置文件 `tty.conf` 看起来像这样：

```
start on stopped rc RUNLEVEL=[2345] and (

  not-container or

  container CONTAINER=lxc or

  container CONTAINER=lxc-libvirt)
```

```
stop on runlevel ![2345]
respawn
exec /sbin/getty -8 38400 tty
```

该任务最复杂的部分实际上是它的启动阶段，现在先忽略容器相关的行，重点关注这部分：

```
start on stopped rc RUNLEVEL=[2345]
```

这部分告诉 Upstart 在 `rc` 任务运行并终止后，当接收到 `stopped`（停止）事件时激活该任务。要使该条件成立，`rc` 任务还需要将 `RUNLEVEL` 环境变量设置为 2 到 5 之间的值（参见第 6.5.6 节）。

其他在运行级别（runlevel）启动的任务并不挑。例如，你可能会看到下面的内容：

```
start on runlevel [2345]
```

> 最后两个 `start` 语句（stanza）之间的唯一区别在于时机；后者在运行级别设置后立即激活任务，而前者则等待 System V 的相关操作完成。

之所以存在容器配置，是因为 Upstart 并不直接运行在真实硬件的 Linux 内核上，但它可以在虚拟环境或容器中运行。这些环境某些具有虚拟控制台，而你不希望在并不存在的控制台上运行 `getty`。

停止 `tty` 任务非常简单：

```
stop on runlevel ![2345]
```

此语句告诉 Upstart 当运行级别不是 2 到 5 时（例如在系统关机期间）终止任务。底部的 `exec` 语句是要要运行的命令：

```
exec /sbin/getty -8 38400 tty
```

此语句类似于你在 `mountall` 任务中看到的脚本，但 `tty` 任务没有复杂的设置——一行即可启动。在这种，我们在 `/dev/tty` 上运行登录提示，这是第一个虚拟控制台（你在图形模式下按下 CTRL-ALT-FI1 进入的那个）。

`restart` 语句指示 Upstart 在任务终止时重启 `tty` 任务。在这种情况下，当你退出虚拟控制台时，Upstart 会运行一个新的 `getty` 提示符。

这些都是 Upstart 配置的基础。你可以在 `init(5)` 手册页和在线资源中找到更多细节，但有一个语句（stanza）需要特别注意。接下来将讨论 `expect` 语句。

# 进程跟踪与 Upstart expect 语句
