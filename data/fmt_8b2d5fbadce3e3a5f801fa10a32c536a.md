
以下代码使用 `bc` 的偏移功能实现了一个计算支票的程序。该程序最好保存在文件中，这样就可以多次使用而无需每次重新输入。

```bc
scale=2 print "\ncheck program!\n" print "Remember, deposits are
negative transactions.\n" print "Exit by a 0 transaction.\n\n" print
"Initial balance"; bal = read(1) bal /= 1 print "\n" while (1) {
"current balance = "; bal = "transaction"; trans = read(1) if (trans ==
0) break; bal -= trans bal /= 1 quit
```

以下是递归阶乘函数的定义。

```bc
def f (x) { if (x <= 1) return (1); return (f(x-1) * x); }
```

## READLINE 与编辑选项

GNU `bc` 可以编译（通过配置选项）以使用 GNU `readline` 编辑器库或 BSD 库。这允许用户在将行发送到 `bc` 之前对其进行编辑。它还允许保留之前输入行的历史。当选择此选项时，`bc` 有一个特殊变量。这个特殊变量 `history` 是保留的历史行数。对于 `readline`，值 `-1` 表示保留无限数量的历史行。将 `history` 的值设置为正数会将历史行数限制为给定的数量。设置为值为 `0` 则禁用历史功能。默认值为 `100`。有关更多信息，请参阅 GNU `deadline`、`history` 和 BSD `libedit` 库的用户手册。不能同时启用 `readline` 和 `libedit`。

## 差异

此版本的 `bc` 是根据 POSIX P1003.2/D11 草稿实现的，相对于草稿和传统实现，包含若干差异和扩展。它不是使用传统的 `dc(1)` 方式实现的。此版本是一个单进程，负责解析并运行程序的字节码翻译。有一个“未文档的选项 (-c)”，它会导致程序将字节码输出到标准输出而不是运行它。它主要用于调试解析器和准备数学库。

差异的主要来源是扩展（extensions），即对功能进行扩展以添加更多功能；以及新增（additions），即添加新功能。以下是差异和扩展的列表。

## LANG 环境

此版本在处理 `LANG` 环境变量以及所有以 `LC_` 开头的环境变量时不符合 POSIX 标准。

- `names`: 传统的 POSIX `bc` 对函数、变量和数组使用字母命名。它们现在被扩展为多字符名称，以字母开头并可以包含字母、数字和下划线字符。

- `Strings`: 字符串不允许包含 NUL 字符。POSIX 规定所有字符都必须包含在字符串中。

- `last`: POSIX `bc` 没有 `last` 变量。某些 `bc` 的实现以类似的方式使用 `.(.)`。

- `comparisons`: POSIX `bc` 仅在 `if` 语句、`while` 语句和语句的第二个表达式中允许比较。此外，在这些语句中，每个只允许一个关系操作。

- `if` 语句，`else` 子句: POSIX `bc` 没有 `else` 子句。

- `for` 语句: POSIX `bc` 要求 `for` 语句中必须存在所有表达式 `&&`、`||`、`!`

- `read` 函数: POSIX `bc` 没有逻辑运算符。

- `print` 语句: POSIX `bc` 没有 `read` 函数。POSIX `bc` 没有 `print` 语句。

- `continue` 语句: POSIX `bc` 没有 `continue` 语句。

- `return` 语句: POSIX `bc` 要求在表达式周围有括号。

- `array parameters`: POSIX `bc`（目前）未完全支持数组参数。POSIX 语法允许在函数定义中使用数组，但没有提供一种将数组指定为实际参数的方法（这很可能是语法中的疏忽）。传统的 `bc` 实现仅通过值传递调用数组参数。

- `function format`: POSIX `bc` 要求左大括号与关键字在同一行，`auto` 语句在下一行。

- `=`, `-=`, `*=`, `/=`, `%,^`: POSIX `bc` 不要求定义这些“旧式”赋值运算符。此版本可能允许这些“旧式”赋值。

# 诊断

如果命令行上的任何文件无法打开，`bc` 将报告该文件不可用并终止。此外，还有编译和运行诊断信息，其含义通常是不言自明的。

## 缺陷

目前的错误恢复机制尚不完善。

请将错误报告发送至 `bug-bc@gnu.org`。请确保在“主题（Subject:）”字段某处包含“`bc`”字样。

### 作者

Philip A. Nelson `philnelson@acm.org`

# 感谢

作者感谢 Steve Sommars (`Steve.Sommars@att.com`) 在测试实现方面提供的巨大帮助。他给出了许多棒的建议。由于他的参与，这个产品变得好得多。

`bccmd` - 用于 CSR BCCMD 接口的实用程序

### 概要

```
bccmd bccmd [-t <transport>] [-d <device>] <command> [<args>] bccmd [-h--help]
```

### 描述

`bccmd` 向 Cambridge Silicon Radio 设备发送 BlueCore 命令。如果在未提供 `<command>` 参数的情况下运行，将显示简短的帮助页面。

### 选项

`-t <transport>`

指定通信传输层。有效的选项有：

- `HCI`

带有主机控制器接口（Host Controller Interface）的本地设备（默认）。

- `USB`

直接 USB 连接。

- `BCSP`

蓝牙核心串口协议（Blue Core Serial Protocol）。

- `H4`

H4 串口协议。

- `3WIRE`

3WIRE 协议（未实现）。

# -D <DEV>

指定要操作的特定设备。如果没有指定，默认为第一个可用的 HCI 设备，或串口传输的 `/dev/ttyS0`。

### 命令

`builddef`

获取构建定义

`keylen <handle>`

获取当前加密密钥长度

`clock`

获取本地蓝牙时钟

`rand`

获取随机数

`chiprev`

获取芯片版本号

`buildname`

获取完整构建名称

`panicarg`

获取崩溃代码参数

`faultarg`

获取故障代码参数

`coldreset`

执行冷启动

`warmreset`

执行热启动

`disablex`

禁用设备上的 TX（发送）

`enablex`

启用设备上的 TX（发送）

`singlechan <channel>`

在特定通道上锁定无线电

`hopping`

恢复通道跳频模式

`rttdata1 <decimal freq MHz> <level>`

TXDadio 无电测试

`radiotest <decimal freq MHz> <level> <id>`

运行无线电测试，4, 6 和 7 是发送测试

`memtypes`

获取内存类型

`psget [-r] [-s <stores>] <key>`

获取 PS 键值。`-r` 在之后发送一次热启动。

`psset [-r] [-s <stores>] <key> <value>`

设置 PS 键值。`-r` 在之后发送一次热启动。

`psclr [-r] [-s <stores>] <key>`

清除 PS 键值。`-r` 在之后发送一次热启动。

`plist [-r] [-s <stores>]`

列出所有 PS 键。`-r` 在之后发送一次热启动。

```
psread [-r] [-s <stores>]
```

读取所有 PS 键。`-r` 在之后发送一次热启动。

```
psload [-r] [-s <stores>] <file>
```

从 PSR 文件加载所有 PS 键。`-r` 在之后发送一次热启动。

```
pscheck [-r] [-s <stores>] <file>
```

检查 PSR 文件的语法。`-r` 在之后发送一次热启动。

# 键

`bdaddr` `country` `devclass` `keymin` `keymax` `features` `commands` `version` `remver` `hciextn` `mapsco` `baudrate` `hostintf` `anafreq` `anaftrim` `usbvid` `usbpid` `dfupid` `bootmode`

### 作者

Marcel Holtmann `<marcel@holtmann.org>` 编写，帮助页由 Adam Laurie `<adam@algroup.co.uk>` 编写

## 名称

`bdftopcf` f - 将 X 字体从位图分布格式（BDF）转换为可移植编译格式（PCF）

### 概要

`bdftopcf [ -pn ] [ -un ] [ -m ] [ -l ] [ -M ] [ -L ] [ -t ] [ -i ] [ -outputfile ] fontfile.bdf`
