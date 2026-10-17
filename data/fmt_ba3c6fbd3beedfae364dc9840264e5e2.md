
`test \( expr1 -a expr2 \) -o expr3`

```
```

此命令在 XSI-con 系统之外并不总是可移植的。相反，可以使用以下方法：

```
( test expr1 && test expr2 ) || test expr3
```

# test

## 1403

在 >4 参数的情况下，如果 `$1` 求结果为 `(` 或 `!`，则会发生语法错误。

`test "$1" = "bat" -a "$2" = "ball"`

如果 `$1` 结果结果为 `(` 或 `!`，会导致语法错误。使用以下形式之一可以防止此错误：error；推荐使用第三种。

`test "$X1" = "Xbat" -a "X2" = "Xball"`

`test "$S1" = "bat" && test "$2" = "ball"`

`test "$S1" = "Xbat" && test "$X2" = "Xball"`

参阅 `largefile(5)` 了解 `test` 在遇到大于或等于 2 Gbytes (2**31 bytes) 文件时的行为描述。

### 示例

在 `if` 命令中，会测试三个条件，如果所有三个条件都为真或执行成功，它们的有效性将输出到屏幕上。

这三个测试是：

- 设置为 1 的变量是否大于 0。
- 设置为 2 的变量是否等于 2。
- 根目录是否包含在文本文件 `/etc/passwd` 中。

`/usr/bin/test`

以下示例在目录不存在时执行 `mkdir`。

```
test ! -d tempdir && mkdir temp
```

以下示例等待文件变为不可读状态。

```
while test -r thefile
do
  sleep 30
done
  echo "thefile" is no longer readable
```

以下示例在参数为三个字符串之一时（两种变体）会执行某个命令。

```
if [ "$1" = "pear" ] || [ "$1" = "grape" ] || [ "$1" = "apple" ]
then
  command
fi

case "$1" in
  pear|grape|apple) command ;;
esac
```

对于 `test` 内置命令的两种形式，请参阅 Bourne shell 示例。

### Bourne Shell

以下示例使用了 `sh` 内置命令。

```
ZERO=0 ONE=1 TWO=2 ROOT=root
if [ $SONE -gt $ZERO ]
  [ $TWO -eq 2 ]
grep $ROOT /etc/passwd > /dev/null  # 丢弃输出
then
  echo "$SONE is greater than 0, $TWO equals 2, and $ROOT
  is a user-name in the password file"
else
  echo "At least one of the three test conditions is false"
```

以下示例使用了 `test` 内置命令。

```
test '$ROOT /etc/passwd >&1 /dev/null'  # 丢弃输出
echo $?  # 测试成功
[ grep nosuchname /etc/passwd >&1 /dev/null ]
necho $?  # 测试失败
```

# C shell

```
@ ZERO =0; @ ONE =1; @ TWO =2; set ROOT = root
grep $ROOT /etc/passwd >&1 /dev/null  # 丢弃输出
# 紧随 grep 之后测试 $ Status
if [ "$SONE" = "0" && $ZERO && $TWO == 2 ] then
  echo "$SONE is greater than 0, $TWO equals 2, and $ROOT
  is a user-name in the password file"
endif
```

### Korn Shell

```
ZERO=0 ONE=1 TWO=$((ONE+ONE)) ROOT=root  # 算术比较
if (( ONE > ZERO ))  # 字符串比较
  [ $TWO == 2 ]
  [ [ grep $ROOT /etc/passwd >&1 /dev/null ] ]  # 丢弃输出
then
  echo "$SONE is greater than 0, $TWO equals 2, and $ROOT
  is a user-name in the password file"
else
  echo "At least one of the three test conditions is false"
```

Korn shell 也接受 Bourne shell 的命令和 `test` 命令的语法。
在 `if` 命令中使用括号 `([])` 时，你必须在括号末尾与内部字符之间隔一个空格。

## 环境变量

参阅 `environ(5)` 了解以下影响 `test` 执行的环境变量描述：`LC_CTYPE`、`LC_MESSAGES` 和 `NLPATH`。

# tftp 1405

## 退出状态

| 0 | 条件求求结果为真。 |
| 1 | 条件求结果为假或条件缺失。 |
| >1 | 发生了错误。 |

### 属性

参阅 `attributes(5)` 了解以下属性描述：

| 属性类型 | 属性值 |
| :--- | :--- |
| Availability | SUNWcsu |

## 参见

`csh(1)`, `ksh(1)`, `sh(1)`, `test(1B)`, `attributes(5)`, `environ(5)`, `largefile(5)`

# tftp — 简单文件传输程序

### 概览

```
/usr/bin/tftp [host]
```

### 描述

`tftp` 命令是 Internet TFTP（简单文件传输协议）的用户界面，它使用数据报协议 (UDP) 而不是 `ftp` 使用的传输控制协议 (TCP)。当你没有登录远程系统并想要传输公开读取的文件时，可以使用 `tftp`。由于 `tftp` 不验证用户，因此它是不安全的。由于 TFTP 协议内部没有登录或验证，许多远程站点以各种方式限制访问。允许的访问方法取决于特定站点，因此无法记录。

`tftp` 在需要时与系统通信，不会与远程主机运行交互式会话。

你可以在命令行上指定远程主机，在这种情况下 `tftp` 将 `host` 作为后续传输的默认主机（参见 `connect` 命令）。

> 注意 — 默认传输模式为 ascii。这与先 SunOS 4.0 和先 4.3 BSD 系统不同，在传输非 ASCII 二进制文件作为执行命令时，必须采取明确操作。

由于 TFTP 协议不提供用户登录或验证，许多远程站点以各种方式限制文件访问。此处无法记录访问方法取决于特定站点。

### 用法

一旦 `tftp` 运行，它会发出 `tftp` 提示符并识别以下命令。

系统 CPU 时间，等于命令执行的进程通过 `times()` 函数返回的 `tms_stime` 和 `tms_cstime` 之和。

当 `time` 用作管道的一部分使用时，如果它是该管道中分组命令中的唯一命令，则报告的时间是不确定的。例如，以下命令是不确定的：

```
time a | b | c
a | b | time c
```

以下命令会报告命令 `a` 和 `c` 的情况：

```
{ time a | b | c
a | b | (time c)
```

> 注意 — 在多处理器系统上运行 `time` 命令时，user 和 sys 输出值的总和可能会超过实际时间（real），因为在多处理器系统上，可以将任务分配给不同的处理器。

当正在被计时的命令被中断时，显示的计时值可能并不总是准确的。

### 选项

- `-p` 以以下格式将计时输出写入标准错误流。
  `real %f\user %f\nsys %f\n real-seconds, user-seconds, system-seconds`

## 操数

- `command` 要调用的命令名称。
- `argument` 调用命令时提供的任何字符串参数。

## 用

如果发生错误，命令返回退出状态 127，以便应用程序能够区分“未找到命令”和“调用的命令带错误指示退出”。选择值 127 是因为它不常用于其他含义；大多数命令在正常情况下使用较小的值，而 128 以上的值可能会因为接收到信号而与终止混淆。选择值 126 的方式类似，用于表示命令可以找到但无法调用。

### 示例

如果你想将 `time` 应用于管道或命令列表，可以将管道和命令列表放在单个文件中。你可以将此文件作为命令调用，`time` 将作用于文件中的所有内容。
或者，你可以使用以下命令将 `time` 应用于复杂的命令。

```
