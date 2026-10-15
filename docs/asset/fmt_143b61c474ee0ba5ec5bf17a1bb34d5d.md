
`lpc` 允许你对打印环境进行许多更改，例如禁用打印机和重新排序打印队列。虽然其中一些功能可供用户使用，但 `lpc` 主要是一个管理工具。表 26.5 总结了与 BSD 打印系统相关的命令和守护进程。

## 表 26.5 BSD 打印命令

| Cmd | Location | Function |
|---|---|---|
| `lpc` | `/usr/sbin` | 控制打印机或队列 |
| `lpd` | `/usr/sbin` | 调度和打印作业 |
| `lpq` | `/usr/bin` | 显示打印队列内容和状态 |
| `lpr` | `/usr/bin` | 将作业排队以便打印 |
| `lprm` | `/usr/bin` | 取消排队或正在打印的作业 |
| `lptest` | `/usr/bin` | 生成 ASCII 测试模式 |

## `lpd`: spool 打印作业

如果你使用 `-l` 标志启动 `lpd`，它会通过 syslog 在 `lpr` 设施下记录打印请求。如果没有 `-l` 标志，`lpd` 仅记录错误。

访问控制的粒度为主机；BSD 打印系统不支持对特定远程用户的访问控制。只有名称出现在 `/etc/hosts.equiv` 或 `/etc/hosts.lpd` 文件中的主机才允许 spool 打印作业。由于安全问题，`hosts.equiv` 的使用已被弃用；请使用 `hosts.lpd`。

## `lpr`: 提交打印作业

`lpr` 是 BSD 风格系统上唯一可以为打印排队文件的程序。其他导致文件被打印的程序（例如 `enscript` 或浏览器）必须通过调用 `lpr` 来实现。

`-#num` 标志打印 `num` 份副本，`-h` 标志抑制页眉页。例如，要将名为 `thesis` 的文件打印两份到名为 `howler-lw` 的打印机，只需运行

```
$ lpr -Phowler-lw -#2 thesis
```

## `lpq`: 查看打印队列

`lpq` 通常仅与 `-P` 选项一起使用以选择打印机，尽管 `-l` 标志可用以产生更详细的输出。`lpq` 的输出如下所示：

```
$ lpq
anchor-lj is ready and printing
Rank Owner Job Files Total Size
active garth 314 domain.2x1.ps 298778 bytes
1st kingery 286 standard input 17691 bytes
2nd evi 12 appendices 828 bytes
...
```

输出行始终按顺序排列，活动作业在顶部，最后要打印的作业在底部。如果第一个作业列为第 1 而不是活动作业，则表示打印机上没有运行打印守护进程，你需要重新启动它。

第二列列出了排队每个作业的用户，第三列给出作业的识别号；如果你打算稍后使用 `lprm` 或 `lpc` 操作该作业，这个号码非常重要。第四列显示在排队该作业的 `lpr` 命令行上列出的文件名。如果数据是通过管道传入，则该列的条目为标准输入。作业大小不幸地没有提供有关作业将产生多少页或打印需要多长时间的信息。

## `lprm`：删除打印作业

`lprm` 最常见的形式是 `lprm jobid`，其中 `jobid` 是 `lpq` 报告的作业识别号。`lprm user` 删除属于该用户的所有作业。`lprm` 不带参数时删除活动作业。`lprm -`（即一个连字符）删除你提交的所有作业；如果你是 `root`，则删除队列中的每个作业。普通用户不能删除彼此的作业，但超级用户可以删除任何作业。

矛盾的是，`lprm` 静默失败但成功时会产生输出。如果你运行 `lprm` 后没有看到类似这样的输出

```
dfA621xinet dequeued
cfA621xinet dequeued
```

则表示命令失败。可能是 `lprm` 无法删除作业，或者你错误地调用了该命令。

打印系统会记录作业来源的主机以及排队它的用户，`lprm` 的匹配过程会同时考虑这两项数据。因此 `garth@sigi` 不等同于 `garth@boulder`，两者都无法删除对方的作业。

尝试 `lprm` 活动作业可能会在某些打印机上造成问题。作业的过滤进程可能未被正确通知终止，导致整个系统陷入停滞，过滤进程持有端口的独占锁，阻止其他进程使用打印机。

解决这种情况的唯一方法是使用 `ps` 识别过滤进程并手动将其杀掉。`lpc` 在这种情况下毫无用处。重新启动系统总能治愈卡住的打印机，但这是一种极端的措施。在求助于重启之前，先杀掉并重启 `lpd` 的主拷贝，并使用 `rm` 命令手动从 spool 目录中删除作业。

## `lpc`：进行管理更改

`lpc` 命令可以执行以下功能：

- 启用或禁用特定打印机的排队
- 启用或禁用特定打印机的打印
- 从打印机的队列中删除所有作业
- 将作业移至打印机队列的顶部
- 启动、停止或重启 `lpd` 守护进程
- 获取打印机状态信息

当打印系统运行顺畅时，`lpc` 工作得很好。但一旦过滤器卡住或出现其他小问题，`lpc` 就会完全失常。而且它会撒谎：它有时声称已修复一切，而实际上什么也没做。你可能不得不手工修复，甚至在 BSD 打印严重混乱时对设备进行断电重启。

`lpc` 不能跨网络使用，因此你必须登录到拥有要操作的打印机的机器。`lpc` 通常以交互方式使用，尽管你也可以通过在 `lpc` 的命令行上放置其中一个交互命令来以一次性模式调用它。一旦激活 `lpc`，下面的各种命令即可使用：

```
help [command]
```

不带参数的 `help` 会显示所有可用 `lpc` 命令的简短列表。带参数时，它会显示特定命令的一行描述。

```
enable printer
disable printer
```

这些命令启用或禁用向指定打印机排队作业。尝试排队文件的用户会被礼貌告知排队已被禁用。队列中已有的作业不受影响。

```
start printer
stop printer
```

`start` 启用打印，`stop` 禁用指定打印机的打印。打印机停止后仍可排队打印作业，但直到打印重新启动后才会被打印。`start` 和 `stop` 通过设置或清除 `/var/spool/lpd/printer/lock` 上的所有者执行权限来操作。它们还会启动和终止打印机对应的守护进程。`stop` 会允许活动作业完成后再禁用打印。

explanation of why the printer is unavailable and when it will be back in service. The `up` command reverses the effect of a `down`.

```
clean printer
```

The `clean` command removes all queued jobs from the printer's queue but allows the current job to complete.

```
topq printer jobid
topq printer username
```

The first form of `topq` moves the specified job to the top of the printer's queue.

The second form promotes all jobs belonging to `username`.

```
restart printer
```

The `restart` command restarts a printing daemon that has mysteriously died.

You'll know that the daemon is dead when `lpq` tells you "no daemon present."

Although you might think `restart` would have the same effect as a `stop` followed by a `start`, it does not; `restart` will not restart a printer that still has a filter running.

```
status printer
```

The `status` command shows you four things about a printer: whether spooling is enabled, whether printing is enabled, the number of entries in the queue, and the status of the daemon for that printer. If no entries are in the queue, you'll see something like this:

```
lpq> status cer
cer:
    queuing is enabled
    printing is enabled
    no entries
    no daemon present
```
