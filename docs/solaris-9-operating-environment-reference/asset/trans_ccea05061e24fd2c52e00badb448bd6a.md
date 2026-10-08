

# 726

## 操作数

file

要打印的文件名。将 `file` 指定为路径名或使用连字符 (-) 来表示标准输入。如果不指定 `file`，则使用标准输入。

## 用法

有关 `lp` 在遇到大于或等于 2 Gbytes (2^31 字节) 的文件时的行为描述，请参阅 `largefile(5)`。

## 退出状态

- 0 成功完成。
- 非零 发生错误。

## 文件

- `/var/spool/lp/*` LP 打印队列。
- `$HOME/.printers` 用户可配置的打印机数据库。
- `/etc/printers.conf` 系统打印机配置数据库。
- `fns_ctx_dir.domain` `/etc/printers.conf` 的 NIS+ 版本。

## 属性

请阅 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability CSI | SUNWpccu Enabled |

> 注意 — CSI 能力假设打印机名称由 ASCII 字符组成。

## 参见

cancel(1), enable(1), lpstat(1), mail(1), postprint(1), pr(1), stty(1), lpq(1B), lpr(1B), lprm(1B), ladmin(1M), accept(1M), lpfilter(1M), lpforms(1M), lpmove(1M), lpched(1M), lpshut(1M), lpsystem(1M), lusers(1M), nswitch.conf(4), printers(4), printers.conf(4), terminfo(4), attributes(5), environ(5), largefile(5), standards(5)

# Lpc

# Lpc - 行打印机控制程序

## 概要

```
/usr/ucb/lpc [command {parameter...}]
```

## 描述

使用 lpc（行打印机控制）命令控制打印机的操作。
lpc 执行以下功能。

- 启动或停止打印机。
- 禁用或启用打印机池队列。
- 重新排列打印队列中作业的顺序。
- 显示打印机打印队列和打印守护进程的状态。

你可以从命令行运行 lpc，也可以以交互方式运行。指定 lpc 带有可选的命令和参数参数会将第一个参数解释为 lpc 命令，并将所有其他参数视为该命令的参数。不带参数指定 lpc 将以交互方式运行，通过 `lpc>` 提示输入 lpc 命令。如果重定向了标准输入，lpc 可以从文件中读取命令。

## 用法

你可以输入完整的 lpc 命令，或将其缩写为无歧义的子字符串。某些 lpc 命令对所有用户可用；另一些则仅对超级用户可用。

- 所有用户都可以执行以下 lpc 命令。

```
? [command...]
```

> 显示作为 lpc 命令的命令简短描述。如果未指定 command，则显示 lpc 命令列表。

```
exit | quit Exit lpc.
```

```
restart [all | printer...]
```

尝试启动一个新的打印机守护进程。当打印机守护进程意外并在打印队列中遗留作业时，restart 非常有用。all 对所有本地连接的打印机执行此命令。

printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printer.conf(4)。

```
status [all | printer...]
```

显示打印守护进程和打印队列的状态。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

只有超级用户可以执行以下 lpc 命令。

- abort [all | printer...]

终止活动的池化守护进程。禁用打印（通过防止 lpr(1B) 启动新的守护进程）。对于 printer，all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- clean [all | printer...]

从打印机的打印队列中移除打印进程在池目录下创建的文件。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- disable [all | printer...]

关闭打印机的打印队列；并禁用打印机文件上的打印。在打印机状态文件中插入消息。不需要对消息加引号，处理多个参数作为消息的方式与 echo(1) 的参数相同。使用 down 关闭打印机并通知用户。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

down [all | printer...] [message]

- down [all | printer...]

关闭打印机的队列；并禁用打印机文件上的打印。在打印机状态文件中插入消息。不需要对消息加引号，处理多个参数作为消息的方式与 echo(1) 的参数相同。使用 down 关闭打印机并通知用户。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- enable [all | printer...]

启用 lpr(1B) 以将作业到池中。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- start [all | printer...]

启用打印机并启动池守护进程。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- stop [all | printer...]

在作业完成后停止池守护进程。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- top [all | printer...]

将打印作业移动到打印队列开头。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- up [all | printer...]

开启打印机队列并启用打印。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

## 退出状态

- 0 成功完成。
- 非零 发生错误。

## 文件

- `/var/spool/lp/*` 打印队列。
- `/var/spool/lp/status` 打印状态文件。

## 属性

阅 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNWpccu Enabled |

## 参见

cancel(1), enable(1), lpstat(1), mail(1), postprint(1), pr(1), stty(1), lpq(1B), lpr(1B), lprm(1B), ladmin(1M), accept(1M), lpfilter(1M), lpforms(1M), lpmove(1M), lpched(1M), lpshut(1M), lpsystem(1M), lusers(1M), nswitch.conf(4), printers(4), printers.conf(4), terminfo(4), attributes(5), environ(5), largefile(5), standards(5)

# Lpc

# Lpc - 行打印机控制程序

## 概要

```
/usr/ucb/lpc [command {parameter...}]
```

## 描述

使用 lpc（行打印机控制）命令控制打印机的操作。
lpc 执行以下功能。

- 启动或停止打印机。
- 禁用或启用打印机池队列。
- 重新排列打印队列中作业的顺序。
- 显示打印机打印队列和打印守护进程的状态。

你可以从命令行运行 lpc，也可以以交互方式运行。指定 lpc 带有可选的命令和参数会将第一个参数解释为 lpc 命令，并将所有其他参数视为该命令的参数。不带参数指定 lpc 将以交互方式运行，通过 `lpc>` 提示输入 lpc 命令。如果重定向了标准输入，lpc 可以从文件中读取命令。

## 用法

你可以输入完整的 lpc 命令，或将其缩写为无歧义的子字符串。某些 lpc 命令对所有用户可用；另一些则仅对超级用户可用。

- 所有用户都可以执行以下 lpc 命令。

```
? [command...]
```

> 显示作为 lpc 命令的命令简短描述。如果未指定 command，则显示 lpc 命令列表。

```
exit | quit Exit lpc.
```

```
restart [all | printer...]
```

尝试启动一个新的打印机守护进程。当打印机守护进程意外并在打印队列中遗留作业时，restart 非常有用。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printer.conf(4)。

```
status [all | printer...]
```

显示打印守护进程和打印队列的状态。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

只有超级用户可以执行以下 lpc 命令。

- abort [all | printer...]

终止活动的池化守护进程。禁用打印（通过防止 lpr(1B) 启动新的守护进程）。对于 printer，all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- clean [all | printer...]

从打印机的打印队列中移除打印进程在池目录下创建的文件。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- disable [all | printer...]

关闭打印机的打印队列；并禁用打印机文件上的打印。在打印机状态文件中插入消息。不需要对消息加引号，处理多个参数作为消息的方式与 echo(1) 的参数相同。使用 down 关闭打印机并通知用户。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

down [all | printer...] [message]

- down [all | printer...]

关闭打印机的队列；并禁用打印机文件上的打印。在打印机状态文件中插入消息。不需要对消息加引号，处理多个参数作为消息的方式与 echo(1) 的参数相同。使用 down 关闭打印机并通知用户。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- enable [all | printer...]

启用 lpr(1B) 以将作业到池中。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- start [all | printer...]

启用打印机并启动池守护进程。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- stop [all | printer...]

在作业完成后停止池守护进程。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- top [all | printer...]

将打印作业移动到打印队列开头。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

- up [all | printer...]

开启打印机队列并启用打印。all 对所有本地连接的打印机执行此命令。printer 在指定的打印机上执行此命令。将 printer 指定为原子名称。有关原子名称命名规范的信息，请参阅 printers.conf(4)。

## 退出状态

- 0 成功完成。
- 非零 发生错误。

## 文件

- `/var/spool/lp/*` 打印队列。
- `/var/spool/lp/status` 打印状态文件。

## 属性

阅 attributes(5) 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability | SUNWpccu Enabled |

## 参见

cancel(1), enable(1), lpstat(1), mail(1), postprint(1), pr(1), stty(1), lpq(1B), lpr(1B), lprm(1B), ladmin(1M), accept(1M), lpfilter(1M), lpforms(1M), lpmove(1M), lpched(1M), lpshut(1M), lpsystem(1M), lusers(1M), nswitch.conf(4), printers(4), printers.conf(4), terminfo(4), attributes(5), environ(5), largefile(5), standards(5)

# 诊断

Ambiguous command

lpc 命令或缩写匹配多个命令。

?Invalid command

lpc 命令或缩写未被识别。

?Privileged command

lpc 命令或缩写只能由超级用户执行。

lpc: printer: unknown printer to the print service

该打印机不在数据库中。检查指定的 printer 是否正确。使用 lstat -p 或 status 命令（参见 lstat(1））检查打印机状态。

lpc: error on opening queue to spool

连接 lpsched 失败。通常意味着打印服务器崩溃或挂起。使用 /usr/lib/lpsched 检查打印池守护进程是否正在运行。

lpc: Can't send message to LP service

lpc: Can't receive message from LP service

LP 服务停止。联系 LP 管理员。

lpc: Received unexpected message from LP service

软件问题。联系 LP 管理员。

# Lpq — 显示打印队列

## 概要
/usr/ucb/lpq [-P destination] [-1] [+ [interval]] [request-ID] [user]

## 描述

lpq 命令显示打印队列内容的信息。
lpqq 向标准输出显示以下信息。

- 与打印请求关联的用户。
- 打印请求在打印队列中的位置。
- 组成打印请求的文件名。
- 打印请求的作业号。
- 打印请求的文件大小。大小以字节报告。
通常，只显示能放入单行的信息。如果与打印请求关联的输入文件名不可，则输入文件字段指示标准输入。

