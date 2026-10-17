
将行距设置为 `number` 打印请求。用数字指定每英寸行数。使用 `pica` 设置 `pica`（每英寸 6 行），使用 `elite` 设置 `elite`（每英寸 12 行），或使用 `compressed` 设置尽可能处理的压缩格式。你不能配合 `-f` 选项使用此选项。

`stty=stty-list`

根据 `stty-list` 中的模式打印请求。`stty-list` 的允许值是本地定义的。只有当可用过滤器来处理它时你才能使用此选项；否则打印请求被拒绝。

`-p` 启用打印请求完成后的通知。

`-P page-list` 按升序顺序打印 `page-list` 中指定的页。将 `page-list` 指定为数字范围、单页码或两者组合。只有当可用过滤器来处理它时你才能使用 `-P`；否则打印请求被拒绝。

## 725
# `lp`

`-q priority-level` 在打印队列中为打印请求分配优先级。将 `priority-level` 指定为 0 到 39 之间的整数。使用 0 表示最高优先级；39 表示最低优先级。如果你未指定优先级，服务的默认优先级由 LP 管理员分配。LP 管理员还可以为单个用户分配默认优先级。

`-s` 抑制从 `lp` 发出的消息的显示。

`-S character-set|print-wheel` 使用 `character-set` 或 `print-wheel` 打印请求。如果请求了表单且需要非 `-S` 选项中指定的字符集或打印轮，则拒绝请求。使用可挂载打印轮的打印机：如果 `print-wheel` 未被 LP 管理员列为打印机接受，则请求被拒绝，除非打印轮已挂载到打印机上。使用可选或可编程字符集的打印机：由于你未指定 `-S` 选项，`lp` 使用标准字符集。如果 `character-set` 未在打印机的 `terminfo` 数据库中定义（参见 `terminfo(4)`）或不是 LP 管理员定义的别名，则请求被拒绝。

`-t title` 在输出的横幅页上打印标题。如果标题包含空格，则将其括起来。如果你未指定标题，则在横幅页上打印文件名。

`-T content-type [-x]` 在支持指定 `content-type` 的打印机上打印请求。如果没有打印机接受此类型，则使用过滤器将内容转换为接受的类型。如果你指定了 `-r` 选项。如果你指定 `-r` 且没有打印机直接接受 `content-type`，则拒绝请求。如果 `content-type` 直接或通过过滤器被任何打印机接受，则请求被拒绝。

`-w` 在文件打印后在用户终端上写入消息。如果用户未登录，则改为发送电子邮件。

`-y mode-list` 根据 `mode-list` 中的模式打印请求。`mode-list` 的允许值是本地定义的。只有当可用过滤器来处理它时你才能使用此选项；否则打印请求被拒绝。

## 726

### 操作数

`file`

要打印的文件名。将 `file` 指定为路径名或使用连字符 (`-`) 来表示标准输入。如果不指定 `file`，则使用标准输入。

### 用法

有关 `lp` 在遇到大于或等于 2 Gbytes (`2^31` 字节) 的文件时的行为描述，请参阅 `largefile(5)`。

## 退出状态

- `0` 成功完成。
- 非零 发生错误。

## 文件

- `/var/spool/lp/*` LP 打印队列。
- `$HOME/.printers` 用户可配置的打印机数据库。
- `/etc/printers.conf` 系统打印机配置数据库。
- `fns_ctx_dir.domain` `/etc/printers.conf` 的 NIS+ 版本。

### 属性

请阅 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
| --- | --- |
| Availability CSI | SUNWpccu Enabled |

> 注意 — CSI 能力假设打印机名称由 ASCII 字符组成。

## 参见

`cancel(1)`, `enable(1)`, `lpstat(1)`, `mail(1)`, `postprint(1)`, `pr(1)`, `stty(1)`, `lpq(1B)`, `lpr(1B)`, `lprm(1B)`, `ladmin(1M)`, `accept(1M)`, `lpfilter(1M)`, `lpforms(1M)`, `lpmove(1M)`, `lpched(1M)`, `lpshut(1M)`, `lpsystem(1M)`, `lusers(1M)`, `nswitch.conf(4)`, `printers(4)`, `printers.conf(4)`, `terminfo(4)`, `attributes(5)`, `environ(5)`, `largefile(5)`, `standards(5)`

# `Lpc`

# `Lpc` - 行打印机控制程序

### 概要

```
/usr/ucb/lpc [command {parameter...}]
```

### 描述

使用 `lpc`（行打印机控制）命令控制打印机的操作。
`lpc` 执行以下功能。

- 启动或停止打印机。
- 禁用或启用打印机池队列。
- 重新排列打印队列中作业的顺序。
- 显示打印机打印队列和打印守护进程的状态。

你可以从命令行运行 `lpc`，也可以以交互方式运行。指定 `lpc` 带有可选的命令和参数参数会将第一个参数解释为 `lpc` 命令，并将所有其他参数视为该命令的参数。不带参数指定 `lpc` 将以交互方式运行，通过 `lpc>` 提示输入 `lpc` 命令。如果重定向了标准输入，`lpc` 可以从文件中读取命令。

### 用法

你可以输入完整的 `lpc` 命令，或将其缩写为无歧义的子字符串。某些 `lpc` 命令对所有用户可用；另一些则仅对超级用户可用。

- 所有用户都可以执行以下 `lpc` 命令。

```
? [command...]
```

> 显示作为 `lpc` 命令的命令简短描述。如果未指定 `command`，则显示 `lpc` 命令列表。

```
exit | quit Exit lpc.
```

```
restart [all | printer...]
```

尝试启动一个新的打印机守护进程。当打印机守护进程意外并在打印队列中遗留作业时，`restart` 非常有用。`all` 对所有本地连接的打印机执行此命令。

`printer` 在指定的打印机上执行此命令。将 `printer` 指定为原子名称。有关原子名称命名规范的信息，请参阅 `printer.conf(4)`。

```
status [all | printer...]
```
