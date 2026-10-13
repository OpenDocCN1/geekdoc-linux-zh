
`alias(1)`, `case(1)`, `cd(1)`, `chmod(1)`, `csh(1)`, `echo(1)`, `exec(1)`,

`exit(1)`, `find(1)`, `for(1)`, `function(1)`, `getoptcv(1)` `getopts(1)`, `glob(1)`,

`hash(1)`, `history(1)`, `intro(1)`, `jobs(1)`, `kill(1)`, `ksh(1)`, `let(1)`,

`limit(1)`, `login(1)`, `logout(1)`, `newgrp(1)`, `nice(1)`, `nohup(1)`, `print(1)`,

`pwd(1)`, `read(1)`, `readonly(1)`, `repeat(1)`, `sh(1)`, `shift(1)`,

`suspend(1)`, `time(1)`, `times(1)`, `trap(1)`, `typeset(1)`, `umask(1)`, `wait(1)`,

`while(1)`, `test(1B)`, `chdir(2)`, `chmod(2)`, `create(2)`, `umask(2)`, `getopt(3C)`,

`profile(4)`, `environ(5)`

# `shift` — 用于遍历 shell 参数列表或字段分隔单词列表的内置函数

# 语法

+   `sh`

`shift [n]`

`csh`

`shift [variable]`

`ksh`

* 

`shift [n]`

## 描述

`shift` 命令是一个 shell 内置命令，用于遍历 shell 的参数列表或一组字段分隔的单词列表。

## Bourne Shell

从 `$n+1...` 开始的位置参数将分别重命名为 `$1....`。默认值是 1。

## C Shell

如果提供了变量，`argv` 的组件将向左移动，并丢弃第一个组件。如果变量未设置或为空值，则视为错误。

## Korn Shell

从 `$n+1 $n+1...` 开始的位置参数将被重命名为 `$1....`。默认 `n` 为 1。参数 `n` 可以是任何评估为非负且小于或等于 `$#` 的算术表达式。

前面带有一个或两个星号 (`*`) 的 `ksh(1)` 命令将按以下方式特殊处理：

- 命令前的变量赋值列表在命令完成后仍然保持有效。
- I/O 重定向在变量赋值后处理。
- 错误会终止包含它们的脚本。
- 紧跟在带有 `**` 的命令之后且符合变量赋值格式的单词将按照与变量赋值相同的规则进行展开。这意味着波浪替换在等号之后执行，且不执行单词拆和文件名生成。

## 属性

后续属性的描述请参见 `attributes(5)`：

| 属性类型 | 属性值 |
| :--- | :--- |
| 可性 | SUNWcs |

### 另请

`csh(1)`, `ksh(1)`, `sh(1)`, `attributes(5)`

# `shutdown` — 在指定时间关闭系统

# 语法

```
/usr/ucb/shutdown [-fhknr] time [warning-message...]
```

## 描述

在关闭具有多个用户的系统时，请作为 root 用户使用 `/usr/ucb/shutdown` 命令。`shutdown` 命令向所有登录用户发送警告消息，等待 60 秒（默认值），然后将系统关闭到单用户状态。你可以选择不同的默认等待时间并指定不同的警告消息。

> 注意 — 默认 `/usr/bin/shutdown(1M)` 命令具有不同的选项。

`shutdown` 命令提供了一种自动化程序，在系统关闭时通知用户。`time` 指定 `shutdown` 关闭系统的时间；你可以指定单词 `now`（表示立即关闭）或以 `+number` 或 `hour:min` 格式指定的未来时间。第一种形式将在指定的分钟数关闭系统，第二种形式将在指定的 24 小时制当天某时间关闭系统。

随着关闭时间的临近，时间间隔会逐渐缩短，警告消息将在所有登录用户以及在该机器上远程挂载的用户的终端上显示。

在关闭时，一条消息将写入系统日志守护进程 `syslogd(1M)`，包含关闭时间、关闭发起者和原因。然后向终端发送一个信号；此操作将系统切换至单用户模式。

> 注意 — 只有当你使用绝对方法时，`/usr/ucb/shutdown` 才允许你在现在到 23:59 之间关闭系统。

## 选项

作为上述程序的替代方案，你可以指定以下选项。

+ `-f` 以 `fastboot(1B)` 的方式安排，当系统重启时不检查文件系统。
- `-h` 执行 `halt(1M)`。
- `-k` 模拟系统关闭。不实际关闭系统。
- `-n` 在停止前防止正常的 `sync(2)`。
- `-r` 执行 `reboot(1M)`。

## 示例

以下示例使用 `-k` 选项来模拟系统关闭。

```
# /usr/ucb/shutdown -k +1
Shutdown at 15:22 (in 1 minute) [pid 519]
```

## 1240 sleep

```
964(.plt) + 160(.dynamic) + 32(.ex_shared) + 188(.data) + 624(.data) 
+ 12396(.bss) = 58864
caste$% size -F /usr/ccs/bin/admin
44711(r-x) + 14372(rwx) = 59243
caste$%
```

## Attributes

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
|可用性 | SUNWbtool |

## See Also

`as(1)`, `ld(1)`, `cc(1B)`, `a.out(4)`, `ar(4)`, `attributes(5)`

## `sleep` — 暂停执行一段时间

### Synopsis

```
/usr/bin/sleep time
```

## Description

`sleep` 命令将暂停执行至少操作数 `time` 所指定的整数秒数。

如果 `sleep` 命令接收到 `SIGALRM` 信号，将采取以下操作之一：

- 以退出状态 0 正常终止。
- 有效忽略该信号。

`sleep` 命令对所有其他信号采取标准操作。

## Operands

`time` 一个非负十整数，指定要暂停执行的秒数。

## Examples

以下示例在 105 秒后执行一个命令。

```
caste$% sleep 105; find -name core -print)&
caste$%
```

## smart2cfg

以下示例每隔一段时间执行一次命令。

```
while true
do
  command sleep 37
done
```

## Environment Variables

参见 `environ(5)` 获取对影响 `sleep` 执行的环境变量的描述：`LC_CTYPE`, `LC_MESSAGES`, 和 `NLPATH`。

## Exit Status

`0`

执行已成功暂停至少 `time` 秒，并接收到了 `SIGALRM` 信号。

`>0`

发生了错误。

## Attributes

参见 `attributes(5)` 获取以下属性的描述：

| 属性类型 | 属性值 |
|---|---|
| 可用性 | SUNWcsu |

## See Also

`wait(1)`, `alarm(2)`, `wait(3B)`, `sleep(3C)`, `attributes(5)`, `environ(5)`

## `smart2cfg` — Compaq Smart-2 EISA/PCI 和 Smart-2SL PCI Array 控制 ioctl 命令

### Synopsis

```
/bin/smart2cfg -c [controller-num]
/bin/smart2cfg -d [controller-num]
/bin/smart2cfg -h
/bin/smart2cfg -l logical-drive-num [controller-num]
/bin/smart2cfg -p physical-drive-num bus-num [controller-num]
```

## Description

`smart2cfg` x86 命令使用 `smartii(7)` 驱动向 Compaq Smart-2 EISA/PCI 和 Smart-2SL 阵列控制器发送特定的 ioctl。

`smart2cfg` 提供有关安装在系统上的 Smart-2 和 Smart2SL 控制器、逻辑驱动和物理驱动，以及每个控制器上读写缓存的详细信息。该命令基于命令行参数并由其驱动。`smart2cfg` 和 `smartii(7)` 驱动通过使用 ioctls 进行通信。`smart2cfg` 还支持多个命令。

注意 — 如果未指定控制器，则采用第一个控制器。

## Options

- `-c controller-num`

  打印控制器 `controller-num` 上缓存的详细信息。
- `-d controller-num`

  打印控制器 `controller-num` 上所有物理磁盘、所有逻辑驱动以及缓存的细节。
- `-h`

  显示 `smart2cfg` 命令的在线帮助。
- `-l logical-drive-num controller-num`
