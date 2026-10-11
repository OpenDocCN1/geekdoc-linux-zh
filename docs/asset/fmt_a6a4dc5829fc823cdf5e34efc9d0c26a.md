
% `lpr -Phowler-lw -2 thesis`

## lpq：查看打印队列

`lpq` 通常配合 `-P` 选项选择打印机，尽管 `-l` 标志可以产生更详细的输出。`lpq` 的输出如下：

```
% lpq

anchor-l is ready and printing
```

| own | 所有者 | 文件 | 总大小 |
| --- | --- | --- | --- |
| active | 314 | domain.2x1.ps | 29878 bytes |
| 1st | kingery | standard input | 17691 bytes |
| 2nd | evi | appendices | 828 bytes |
| 3rd | proc | 43229 bytes |
| 4th | scott | periodic | 16676 bytes |
| 5th | garth | standard input | 489 bytes |

第一列告诉你哪些任务将被打印。这些信息是多余的，因为输出行总是有序的，活动的任务在顶部，最后一个打印的任务在底部。如果第一个任务显示为 `active`，则没有打印守护进程在运行。

第二列告诉你谁列队了每个任务。第三列给出每个任务的标识符；如果你打算稍后用 `lpq` 操控任务，这很重要。第四列显示在命令行用于列队任务的文件名。如果数据来自管道（如上面的五个任务），此列将显示标准输入。第五列和最后一列告诉你任务在发送到进程之前的大小以及打印需要多长时间。

## lprm：移除打印任务

`lprm` 最常用的功能是 `lprm jobid`，其中 `jobid` 是 `lpq` 报告的标识。不带参数的 `lprm` 活动任务；如果你是 `root`，它会移除队列中的所有任务。普通用户无法移除其他用户的任务，但超级用户可以。

# Linux 管理手册

打印系统维护了任务来源以及列队任务的用户的概念。因此，匹配不等同于，且无法移除其他任务。

尝试 `lpr` 活动任务可能会在某些打印机上引起问题。任务的过滤器没有正确收到终止通知，导致整个系统处于打印机锁定状态并阻止其他进程使用它。修复这种情况的唯一方法是使用 `ps` 识别过滤器并杀死它们。`LPC` 没用。重启系统总是能治卡住的打印机，但这是一种极端措施。在采取重启措施之前，重启 `lpd` 并手动从 `spool` 目录移除任务。

## lpc：进行管理更改

`lpc` 命令可以执行以下操作：

- 启用或禁用特定打印机的列队
- 启用或禁用特定打印机的打印
- 从打印机队列中移除所有任务
- 将任务移动到打印机队列顶部
- 启动、停止或重启 `lpd` 守护进程
- 获取打印机状态

当打印系统运行顺畅时，`lpc` 工作良好。但一旦过滤器卡住或出现其他问题，`lpc` 会完全挂起。它声称修复了一切，但实际上什么都没做。当打印任务糟糕时，你可能需要通过拔掉或重启设备来修复问题。

`lpc` 无法跨网络使用；你必须登录到打印机的机器。它通常以交互方式使用，尽管你也可以通过在命令行放置交互命令之一以单次模式调用它。一旦激活了 `lpc`，可以使用下面的各种命令：

```
help [command]
```

不带参数的 `help` 显示所有可用 `lpc` 命令的短列表。带有参数时，它显示特定命令的行描述。

```
enable printer

disable printer
```

这些命令启用或禁用向指定打印机列队任务。尝试列队文件的用户会收到礼貌通知，列队已禁用。已经在队列中的任务不受影响。你执行此操作只需简单的设置或清除 `/var/spool/lpd/printer/lock` 的执行权限。

`start` 启用或停止指定打印机的打印。当打印机停止时，打印任务仍然可以列队，但在重启之前它们不会被打印。`start` 和 `stop` 通过设置或清除 `/var/spool/lpd/printer/lock` 的所有者执行权限来操作。它们还会杀死打印机相应的守护进程。`stop` 允许活动任务在禁用打印之前完成。

```
abort printer
```

`abort` 就像 `stop`，但它不允许活动任务完成。当重新启用打印时，此任务将再次打印。

```
down printer message

up printer
```

这些命令同时影响列队和打印。当打印机真的损坏或必须离线较长时间时使用它们。向 `down` 提供的 `message` 参数可以任意长（单行）且不需要引号；它位于打印机的 `/var/spool/lpd/printer/status` 文件并显示运行 `lpq` 的用户。`up` 命令反转 `down` 的效果。

```
clean printer
```

此命令从打印机队列中移除所有任务，包括活动任务。由于打印守护进程仍然持有当前任务的文件引用，Linux 不会真正删除它们，且当前任务将完成。

```
topq printer jobid

topq printer username
```

第一种形式指定任务到打印机队列顶部。第二种形式提升属于 `username` 的所有任务。

```
restart printer
```

`restart` 命令重启死亡的守护进程。当 `lpq` 告诉你 "no daemon present" 时，你就知道守护进程坏了。尽管你可能认为 `restart` 与 `stop` 后接 `stop` 的效果相同，但并非如此；对于仍过滤器运行的打印机，`restart` 将失败。

```
status printer
```

`status` 命令告诉你关于打印机的四种信息：是否启用列队、是否启用打印、队列中的项数以及该打印机守护进程的状态。如果队列中没有项，你将看到如下的内容。

# Linux 管理手册

```
lpc> status cer

cer:

  queuing is enabled

  printing is enabled

  no entries

  no daemon present
```

不存在守护进程（`daemon`）并不令人担心；特定打印机的守护进程在队列为空后会消失，并且不会被 `lpd` 的主复制程序重启，直到有另一个任务被置入队列。

## /etc/printcap 文件

`/etc/printcap` 是 `LPD` 打印系统的主数据库。它包含了向本地和远程打印机打印所需的信息。在提交任务到打印机之前，必须在 `printcap` 文件中描述该打印机。

空语句（`null statement`）是允许的，因此你可以并列放置两列。这有助于每行都以冒号开头和结束，以便于后续修改。`/etc/printcap` 中的注释以井号 (`#`) 开头。如果中间行以反斜杠结尾，则条目可以跨多行。按照惯例，延续行需要缩进。

`printcap` 文件的语法如如下示例所示，该示例定义了一个连接到机器的远程打印机：

```
# LaserJet 5M remote printcap. CS Department

anchor-lj|cer1-56[LaserJet 5M in cer lab]:

lp=/var/pool/lpd/anchor-lj;/null:

sd=/var/pool/lpd/anchor-lj;:

if=/var/adm/lpd-errs:

rm:mx#0:anchor-rp-lj:
```
