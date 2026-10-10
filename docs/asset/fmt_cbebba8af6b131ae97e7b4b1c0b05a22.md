
- `-a,--list-full` 列出完整的命令行以及进程标识符。（`id` 仅限 `pgrep`）。

- `-n,--newest` 选择匹配进程中最新的（最近启动的）一个。

- `-0,--oldest` 选择匹配进程中最旧的（最晚启动的）一个。

- `-P,--parent ppid...` 仅匹配父进程标识符（`PPID`）在列表中的进程。

- `-s,--session sid...` 仅匹配进程会话 ID（`SID`）在列表中的进程。会话 ID `0` 会被转换为 `pgrep` 或 `pkill` 自身的会话 ID。

- `-t,--terminal term...` 仅匹配控制终端在列表中的进程。指定的终端时不应带 `"/dev/"` 前缀。

- `-u,--uid eid...` 仅匹配有效用户 ID（`EUID`）在列表中的进程。可以使用数字或符号值。

- `-U,--uid...` 仅匹配真实用户 ID（`UID`）在列表中的进程。可以使用数字或符号值。

- `-v,--inverse` 反转匹配。此选项通常在 `pgrep` 的上下文中使用。在 `pkill` 的上下文中，禁用了短选项以避免意外使用该选项。

- `-w, --lightweight`

在 `pgrep` 上下文中显示所有线程而非 PID。在 `pkill` 中此选项被禁用。

- `-x, --exact`

仅匹配名称（如果指定了 `-f` 则为命令行）与模式完全匹配的进程。

- `-F, --pidfile file`

从文件中读取 PID。此选项对于 `pkill` 可能比 `pgrep` 更有用。

- `-L, --logpidfile`

如果 `pidfile`（见 `-F`）未锁定则失败。

- `-ns pid`

匹配属于相同命名空间（`namespaces`）的进程。需要以 `root` 运行以匹配其他用户的进程。参见 `nslist` 如何限制匹配哪些命名空间。

- `-nlist name,...`

仅匹配提供的命名空间。可用的命名空间：`ipc`, `mnt`, `net`, `pid`, `user`, `uts`。

- `-V, --version`

显示版本信息。

- `-h, --help`

显示帮助。

# 参数

`pattern`

指定与命令行匹配的模式。

### 示例

示例 1：查找 `root` 拥有的 `sshd` 进程：

```
$ pgrep -u root sshd
```

示例 2：杀死 `syslog` 进程：

```
$ pkill syslog
```

示例 3：获取 `xterm` 进程的详细信息：

```
$ pgrep -f xterm
```

示例 4：杀死最新的 `xterm` 进程：

```
$ pgrep -n xterm
```

# 退出状态

- `0` 匹配到进程。
- `1` 未匹配到进程。
- `2` 命令行语法错误。
- `3` 内存不足。

## 注意

`pgrep` 的模式匹配通常针对进程名。当设置了 `-f` 时，则使用完整的命令行。

# 缺陷

`pgrep` 的输出可能包含额外的字符。

# 参见另

`(1)`, `(7)`, `(1)`

# 标准

`pic` 的实现与 Unix 兼容。

# 报告

请将报告发送至

`John Doe`

```
if expr X Y if-true X [else Y if-false Y]
```

评估 `expr`；如果其非零，则执行 `if-true`，否则执行 `if-false`。`X` 可以是任意未出现在 `if-true` 中的字符。`Y` 可以是任意未出现在 `if-false` 中的字符。

```
print arg...
```

连接参数并作为的一行打印到 `stderr`。每个 `arg` 可以是表达式、位置或文本。这对于调试非常有用。

```
command arg...
```

连接参数并通过行传递给 `troff` 或 `TeX`。每个 `arg` 可以是表达式、位置或文本。这与以 `|` 或 `>` 开头的行效果相似，但允许传递变量的值。例如：

`.PS x = 14 command ".ds string x is " x." .PE *string]`

# prints

`x is 14.`

`sh X X` 将命令传递给 `shell`。`X` 可以是任意未出现在 `command` 中的字符。`copy ",filena"` 在文件的此位置包含过滤器。`copy ",filena" thru X body Y [until,"word]` `copy ",filena" thru macro [until,"word]` 此结构对文件的每一行执行 `body`；该行被拆分为由分隔符分隔的单词，`body` 中 `Si`（`i` 在 1 到 9 之间）被替换为行的第 `i` 个单词。如果没有给出 `filena`，则从当前输入到 `.PE` 取行。如果指定了子句，则只读取到第一个被使用的单词所在的行；该行将被丢弃。`X` 可以是任意未出现在 `body` 中的字符。例如：

`.PS thru % circle at ($1,$2) only "END" 1 2 3 4 5 6 box .PE`

等同于

`.PS circle at (1,2) circle at (3,4) circle at (5,6) box .PE`

为每行执行的命令可以从之前定义的名为 `thru` 的宏中获取。

# reset

```
reset variable1[1] variable2 ...
```

将预定义变量 `variable1`、`variable2` ... 重置为它们的默认值。如果没有提供参数，分配比例也会将所有控制重置的预定义变量重置为 `scale` 的新值。

```
plot expr ["text"]
```

这是使用 `text` 作为字符串并将 `expr` 作为参数进行打印而构建的对象。如果 `text` 是格式化字符串，`s` 将被替换。属性可以像普通对象一样在 `sa` 中指定。请务必指定正确的格式字符串；`pic` 对字符串的检查非常有限。此功能已废弃，改由 `print` 替代。

```
variable:expr
```

这与 `=` 类似，但 `variable` 已经定义，且 `expr` 将赋值给 `variable` 而不会在当前块中创建局部变量。（相比之下，`=` 如果变量未定义，则在当前块中定义它，然后仅更改当前块中的值。）例如，如下：

`.PS x = 3 y = 3 [ x := 5 y = 5 ] print x " " y.PE`

打印 `5 3`

# 形式的参数

`X anything`

也允许形式为

`{anything}`

在任何情况下，`anything` 都可以包含平衡的 `{` 和 `}`。字符串可以包含 `X` 或不平衡的 `{` 和 `}`。

# 表达式

表达式的语法已大幅扩展：`x^y`（幂） `sin(x)` `cos(x)` `atan2(y,x)` `log(x)`（底为10） `exp(x)`（底为10，即 `10^x`） `sqrt(x)` `int(x)` `rand()`（返回 0 到 1 之间的随机数） `rand(x)`（返回 1 到 `x` 之间的随机数；已废弃） `srand(x)`（设置随机数种子） `max(e1,e2)` `min(e1,e2)` `le e1 & e2 e1 || e2 == e2 e1 != >= e2 e1 > e2 e1 <= e2 e1 < e2 <2, "str1" == "str2", "str1" != "str2"`

字符串比较表达式在某些语文中必须加括号，以避免歧义。

# 其他更改

裸表达式 `expr` 可以作为属性；它等同于 `direpr`，其中 `dir` 是当前方向。例如：

`line 2i`

`ans` 在当前方向画一条 2 英的线。‘`i`’（或‘`I`’）字符被忽略；要使用其他字符作为单位，将 `scale` 变量设置为适当的值。

图片的最大宽度和高度从变量 `maxpswid` 和 `maxpsht` 获取。这些初始值为 8.5 和 11。

数字允许科学计数法。例如：

`x = 5e-2`

文本属性可以组合。例如：

`“foo” above ljust`

是有效的。

块的检查深度没有限制。例如：

`[A: [B: [C: box ]] with .A.B.C.sw scale at 1,2 circle at last [].A.B.C`

是可接受的。

弧的罗盘点由其所在的圆或圆的一部分决定。

圆、椭圆和弧可以是点线或虚线。在 TeX 模式下，脊线可以是点线或虚线。

框具有圆角。`rad` 属性指定每个角四分之一圆的半径。如果没有给出 `rad` 属性，框为正方形。其初始值为 0。

在所有情况下，`rad` 属性可以是点线或虚线。它指定每个角四分之一圆的半径。如果没有给出 `rad` 属性，框为正方形。其初始值为 0。

## 转换

要从 `pic` 文件获取单独的图片，请将你的 `pic` 代码封装在 `.PS` 和 `.PE` 请求中；可以在文件开头添加 `roff` 配置命令，但不要包含 `roff` 文本。
