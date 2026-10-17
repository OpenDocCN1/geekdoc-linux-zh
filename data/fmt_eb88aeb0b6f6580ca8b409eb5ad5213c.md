
当 `string1` 比 `string2` 长时，使用 `string1` 的初始位置（与 `string2` 相同）进行翻译。当 `string1` 比 `string2` 短时，GNU `tr` 使用 `string1` 的最后一个字符将 `string1` 扩展到 `string2` 的长度。这偏离了未定义结果的 POSIX 标准。如果你同时使用 `--delete` 和 `--squeeze-repeats`，`tr` 会删除 `string1` 中的字符，然后减少 `string2` 中字符的多次出现。

# 示例

你可以使用连字符来表示 `string1` 或 `string2` 中的字符范围。以下两个命令产生相同的结果：

```
$ echo abcdef | tr 'abcdef' 'xyz'
xyzabc
$ echo abcdef | tr 'a-f' 'x'
xyzaef
```

下一个示例演示了一种常用的文本隐藏方法，通常被称为“旋转 13”，因为它将字母表的第一个字母替换为第 13 个，第二个替换为第 14 个，依此类推：

```
$ echo The punchline of the joke is ... |> tr '[A-M][N-Z][a-m][n-z]'
characters ...
```

为了使文本变得易读，反转 `tr` 参数的顺序：

```
$ echo The punchline of the joke is ... |> tr '[N-Z][A-M][n-z][a-m]'
the joke ...
```

使用 `--delete` 选项删除指定字符

```
$ echo If you can read this, you can spot the vowels! |> tr -delete 'aeiou'
If you can read this, you can spot the vowels!
```

在以下示例中，`tr` 将相同字符对替换还原为单个字符：

```
$ echo tennsee | tr -s 'tnse' 'srne'
serene
```

以下示例将文件 `draft1` 中指定的非字母字符（所有字母字符的补集）'a-zA-Z' 替换为单个换行符。输出是每行一个单词列表。

```
$ tr --squeeze-repeats 'a-zA-Z' '\n' < draft1
```

以下两个命令与前一个等效，并将 `string2` 扩展到 `string1` 的长度。第一个命令指定换行符重复 52 次——即 `string1` 的长度。第二个命令使用足够的换行符扩展 `string2`，使其达到 `string1` 的长度。必须使用方括号：

```
$ tr -cs a-zA-Z '[52]' < draft1
$ tr -cs a-zA-Z '[]' < draft1
```

# tty 显示终端路径

| 语法： | `tty` [option] |

## 总结

`tty` 工具在标准输入是终端时显示其路径。如果标准输入是终端，`tty` 的退出状态为 0；否则为 1。

## 参数

没有参数。

## 选项

`--silent` 或 `--quiet` (`-s`) 导致 `tty` 不打印任何内容。然而，`tty` 的退出状态仍然会被。

## 注意

如果标准输入不是终端，`tty` 会显示消息 not a tty。

# 示例

以下示例说明了 `tty` 的用法：

```
$ tty
/dev/tty1
echo $?
0
tty < memo
not a tty
echo $?
1
```

# umask

| `umask` 文件创建权限掩码 |

| 语法： | `umask` [mask] |

## 总结

`umask` 内置命令指定系统在创建文件时用于设置权限的掩码。

## 参数

`mask` 是一个三位进制数，每个数字分别对应文件所有者、所属组成员以及其他所有人的权限。当你创建一个文件时，系统会将这些数字从系统本会分配给文件的权限数字中减去。结果是三个进制数，指定了文件的权限。（请参考第 676 页的 `chmod` 获取完整描述和示例。）

在没有任何参数的情况下，`umask` 显示文件创建权限掩码。

## 注意

`umask` 程序是 bash、tsch 和 zsh 的内置命令。它通常位于你 shell 的初始化文件中（bash 的 .profile、zsh 的 .profile 以及 tsch 的 .login）。在 bash 和 zsh 下，`umask` 接受 `chmod` 允许的符号参数。例如，参数 `a+w` 关闭掩码中的写位，导致创建的文件在权限中设置该位。请参考第 676 页的 `chmod` 了解更多符号权限的信息。tsch 的 `umask` 内置命令不允许符号参数；你必须始终使用如下所示的三位进制形式。

# 示例

以下命令将文件创建权限掩码设置为 066。该命令的效果是移除与其所属组成员以及其他所有人的读、写权限。如果系统本会创建一个权限值为 777 的文件（所有者、组和其他其他人都有读、写、执行权限），它现在将创建一个 711 的文件（所有者拥有所有权限，组和其他人只有执行权限）。

```
$ umask 066
```

下一个示例显示了 zsh 版本的 `umask` 允许你通过符号指定掩码值：

```
$ umask
002
$ umask g+rw,o-rw
$ umask
000
$ umask g-rw,o-rw
$ umask
066
```

# uniq 显示文件中文件中唯一的行

语法: `uniq` [options] [input-file] [output-file]

# 摘要

`uniq` 工具用于显示文件，删除所有连续的重复行，只保留其中一个。如果文件已经过排序（请参考 `sort` 工具），`uniq` 可以确保文件中没有两行显示的内容是完全相同的。

`uniq` 工具从你在命令行上指定的文件或从标准输入（standard input）中获取输入。除非你在命令行上指定了输出文件，否则 `uniq` 会将输出结果发送到标准输出。

## 参数

如果你没有在命令行上指定输入文件，`uniq` 将使用标准输入。如果你没有在命令行上指定输出文件，`uniq` 将使用标准输出。

## 选项

在接下来的描述中，字段（field）是指任何不包含空白字符（空格和制表符的任意组合）的字符序列。字段由空白字符或行的开始或结束界定。

- `--count` (`-c`) 在每行前面显示该行在输入文件中出现的次数。
- `--repeated` (`-d`) 仅显示重复的行。
- `+nchar` 或 `--skip-chars=nchar` (`-s nchar`) 忽略每行的前 nchar 个字符。如果你也使用了 `--skip-fields` 选项（见下文），`uniq` 将忽略第一个字段以及随后的 nchar 个字符。此选项可用于跳过字段开头的空白带。`uniq` 识别此选项的缩写形式 `+nchar`。
- `+nfield` 或 `--skip-fields=nfield` (`-f nfield`) 忽略每行的前 nfield 个由空白符分隔的字段。`uniq` 工具基于行的剩余部分进行比较，包括行中下一个字段开头的空白带（即上文的 `--skip-chars` 选项）。`uniq` 识别此选项的缩写形式 `--nfield`。
- `--unique` (`-u`) 仅显示不重复的行。

# 示例

这些示例假设工作目录下的名为文件 test 包含以下内容：

```
$ cat test
boy took bat home
boy took bat home
girl took bat home
dog brought hat home
dog brought hat home
dog brought hat home
```

在不使用任何 `uniq` 参数的情况下，仅显示连续重复行的一个副本。

```
$ uniq test
boy took bat home
girl took bat home
dog brought hat home
```

`--count` 选项显示文件中每行连续出现的次数。

```
$ uniq --count test
2 boy took bat home
1 girl took bat home
3 dog brought hat home
```

`--repeated` 选项仅显示在文件中连续重复的行。

```
$ uniq --repeated test
boy took bat home
dog brought hat home
```

`--unique` 选项仅显示在文件中未连续重复的行。

```
$ --unique test
girl took bat home
```

`--nfields` 参数 (`-1`) 跳过每行的第一个字段，这导致以 boy 开头的行和以 girl 开头的行被视为连续重复。`uniq` 工具仅显示这些行中的一次出现。

```
$ uniq --skip-fields=1 test
boy took bat home
dog brought hat home
```

下一个示例同时使用了 `-nfields` 和 `+nchars` (`-2` 和 `+2`) 来先跳过两个字段，然后跳过两个字符。该命令跳过的两个字符是分隔第二个和第三个字段的空格以及第三个字段的首个字符。忽略这些字符后，所有行看起来都是包含字符串 "home" 的重复行。`uniq` 工具仅显示这些行中的第一行。

```
$ uniq -f 2 -s test
boy took bat home
```

以下示例等同于上一个，但使用了 `-nfields` 和 `-nchars` 选项的缩写形式：

```
$ uniq -2 +2 test
boy took bat home
```

# w 895

| 显示系统用户信息 |

| 语法: `w` [options] [login-name] |

# 摘要

`w` 工具显示当前登录系统的用户的名称，以及他们的终端设备号、登录时间、正在运行的命令以及其他信息。

## 选项

- `-f` (from) 如果用户是从远程系统登录的，此选项将显示一列，显示远程系统的名称。此外，对于某些用户，该字段可能会出现 X Window 系统的名称。对于直接连接的用户，该字段为空。
- `-h` (no header) 抑制 `w` 工具通常输出的表头行。
- `-s` (short) 显示较少的信息：用户名、终端设备、空闲时间和命令名称。

## 参数

如果将 `login-name` 作为参数提供给 `w` 工具，则显示将限制为仅该用户的信息。

# 讨论

`w` 工具显示的第一行与 `uptime` 命令提供的相同。该报告包括当前时间、计算机已运行的时间（以天、小时和分钟计算）以及登录的用户数。该报告还指示了系统的忙碌程度（平均负载）。从左到右，平均负载表示在过去 1 分钟、5 分钟和 15 分钟内等待运行的进程数。

`w` 为每个用户显示的信息格式为

```
name line time activity cpu cpu2 command
```

`name` 是用户的登录名。`line` 是用户登录的线路名称。`time` 是用户登录的日期和时间。`activity` 列表示该用户空闲了多久（自上次活动以来有多少分钟）。接下来的列 `cpu` 和 `cpu2` 提供了处理器使用量的衡量。`command` 列显示正在运行的内容。

## 注意

`w` 工具显示的第一行与 `uptime` 命令提供的相同。该报告包括当前时间、计算机已运行的时间（以天、小时和分钟计算）以及登录的用户数。该报告还指示了系统的忙碌程度（平均负载）。从左到右，平均负载表示在过去 1 分钟、5 分钟和 15 分钟内等待运行的进程数。

# 示例

第一个示例显示 `w` 产生的完整列表：

```
$ w
14:20:01 up 2 days, 3:45, 1 user, load average: 0.01, 0.05, 0.01
```

下一个示例显示 `-s` 选项产生的简短列表：

```
$ w -s
user     tty0001    2:05m  bash
```

最后一个示例请求了关于 alex 的信息：

```
$ w alex

alex     tty0001    2:05m  bash
```

# WC 显示文件的行数、单词数和字符数

语法: `wc` [options] [file-list]

# 摘要

`wc` 显示一个或多个文件的行数、单词数和字符数。如果你在命令行上指定多个文件，`wc` 会显示每个文件的统计以及文件组的总计。

`wc` 工具从你在命令行指定的文件或从标准输入获取输入。

## 参数

`file-list` 包含 `wc` 分析的一个多个文件路径。

## 选项

- `--bytes` (`-c`) 仅显示文件的字节数。
- `--lines` (`-l`) （选项字符是字母 "l"，代表行。）仅显示文件的行数（即换行符数量）。
- `--words` (`-w`) 仅显示文件的单词数。

## 注意

单词是由空格、制表符、换行符或这些组合界定的字符序列。

# 示例

以下命令显示了名为 memo 的文件的分析。这些数字代表文件的行数、单词数和字符数。

```
$ wc memo
5 31 146 memo
```

下一个命令显示三个文件的行数和单词数。底部的行（右侧列为单词总计）包含每列的和。

```
$ wc -lw memo1 memo2 memo3
10 62 memo1
12 74 memo2
12 68 memo3
34 204 total
```

## which

`which` 显示命令在你的路径中的位置

语法：`which` command-list

### 摘要

`which` 实用程序取 `command-list` 中的每个命令名称，并定位包含该命令的文件。

## 参数

`which` 的每个参数都被假设为命令的名称。对于每个命令名称，`which` 会按照顺序在你的 PATH 环境变量中列出的所有目录中搜索，直到找到该命令。在找到该命令后，`which` 会显示命令的完整路径。

如果 `which` 没有在你的搜索路径中找到该命令，它将显示错误信息。

### 注意事项

`which` 实用程序无法定位别名（aliases）、函数（functions）和 shell 内置命令（shell builtins），因为它们不会出现在你的搜索路径中。然而，tsch 和 zsh 都有内置的 `which`，可以定位别名、函数和 shell 内置命令。

`which` 实用程序一旦在搜索路径中发现命令的第一次出现，就会停止搜索。tsch 的内置 `which` 也是如此。通过 `-a` 选项，zsh 内置的 `which` 会列出搜索路径中命令的所有出现处。

### 示例

第一个示例定位了 nvi、dir 和 which 命令：

```
$ which nvi dir which
/usr/bin/nvi
/bin/dir
/usr/bin/which
```

在第二个示例中，运行 tsch 时给出了相同的命令。这次使用了内置命令 `which` 代替了实用程序 `which`。zsh 中的内置命令产生了相似的结果。

```
> which nvi dir which
/usr/bin/nvi
/bin/dir
which: shell built-in command.
```

## who

| `who` 显示登录用户名称 |

| :--- |

| 语法：`who` [options] `who am i` |

### 摘要

`who` 实用程序显示当前登录用户的名称，以及他们的终端设备号、登录时间以及其他信息。

## 参数

当给出两个参数 `am i` 时，`who` 显示在终端命令给出的终端登录的用户的登录名、终端设备号以及用户登录时间（在 rxvt 中不起作用）。登录名之前是主机名（运行 `who` 的机器名称）。

## 选项

- `--count` (`-q`) 仅列出用户名称，后跟系统上登录的用户的人数。
- `--heading` (`-H`) 显示表头。
- `--idle` (`-i`) (`-u`) 在显示中包含每个用户的空闲时间。如果用户终端在过去一分钟内有输入，`who` 会放置一个点 (.)。如果终端超过一天没有输入，`who` 会显示字符串 o。
- `-m` 等同于两个参数 `am` 和 `i`（在 rxvt 中不起作用）。
- `--message` 或 `--mesg` (`-T`) 在每个用户的登录名后附加一个字符，显示用户是否启用了消息功能。加号 (+) 表示消息已启用，连字符 (-) 表示已禁用。`who` 实用程序会显示问号 (?) 表示它无法确定用户所处的位置。如果启用了消息，你可以使用 `write` 与该用户通信。请参阅第 56 页的“使用 mesg 拒绝或接受消息”。

### 讨论

`who` 显示的行语法为

`name [messages] line time [activity] source`

`name` 是用户的登录名。`messages` 表示消息是否启用或禁用（参见上文的 `--message` 选项）。`line` 是用户登录所在终端对应的设备号。`time` 是用户登录的日期和时间。`activity` 是自终端上次被使用以来的时间长度（空闲时间——参见 `--idle` 选项）。`source` 是用户登录的远程机器或 X 显示（对于直接连接的用户为空）。

### 注意事项

`finger` 实用程序（第 736 页）提供了与 `who` 类似的信息。

### 示例

以下示例演示了 `who` 实用程序用法：

```
$ who
hls tty1 Jul 30 06:01
jenny tty2 Jul 30 06:02
alex tty3 Jul 30 14:56 (bravo)

$ who am i
bravalex tty3 Jul 30 14:56 (bravo)

$ who -heading --idle -w
USER MSG LINE IDLE FROM
hls - tty1 Jul 30 06:01 03:53
jenny + tty2 Jul 30 06:02 14:47
alex + tty3 Jul 30 14:56 . bravo)
```

## write

`write` 向另一个用户发送消息

语法：`write` destination-user [tty-name]

### 摘要
