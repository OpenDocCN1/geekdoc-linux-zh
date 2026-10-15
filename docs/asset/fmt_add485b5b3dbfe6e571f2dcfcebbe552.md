

当你担心系统性能时，可以使用`time`命令。如果你的许多命令显示大量的页故障和交换，说明系统内存不足。可以使用`time`报告的信息来比较各种系统配置和程序算法的性能。

`period`设置此变量以控制每隔分钟执行一次特殊的周期别名（第 689 页）。

`user` shell 将此变量设置为你的登录名。

`version` shell 将此变量设置为包含你正在使用的版本的详细信息。

`watch`将此设置为要监控的用户和终端对数组。如果设置了`flec`，你可以在命令行输入部分文件名并按 TAB 键让 shell 补全，或者可以按 CONTROL-D 列出所有匹配输入前缀的文件。请参阅第 691 页的“替换 (Substitution)”。

设置后，你无法通过 CONTROL-D 退出 shell，无法意外注销。当声明此变量时，你必须使用`exit`或`logout`离开 shell。

当有作业被挂起时，shell 会列出所有作业。

`ls`内置命令会显示每个符号链接指向的文件类型，而不是用`@`符号标记符号链接。

如果当前 shell 是作为登录 shell 运行的，由 shell 设置。

`nobeep`禁用 shell 的所有蜂鸣声。

`noclobber`防止你在重定向输出时不小心覆盖文件，并防止在尝试向一个不存在的文件追加输出时创建该文件（表 14-8）。若要覆盖`noclobber`，可以在你用于重定向或追加输出的符号后添加一个感叹号（例如`!>`和`!!`）。有关`noclobber`的更多信息，请参阅第 554 页和第 824 页。

### `noclobber`工作原理

#### 表 14-8

| 命令行 | 未声明`noclobber` | 已声明`noclobber` |
|---|---|---|
| `> fileout` | 将进程 x 的标准输出重定向到`fileout`。如果`fileout`存在，则覆盖`fileout`。 | 将进程 x 的标准输出重定向到`fileout`。如果`fileout`存在，shell 将显示错误消息且不覆盖该文件。 |
| `>> fileout` | 将进程 x 的标准输出重定向到`fileout`。如果`fileout`存在，则将新输出追加到`fileout`的末尾。如果不存在，则创建`fileout`。 | 将进程 x 的标准输出重定向到`fileout`。如果`fileout`存在，则将新输出追加到`fileout`的末尾。如果`fileout`无法创建文件，shell 将显示错误消息。 |

当你声明`noclobber`时，`tsh`不扩展歧义的文件名。你可以在命令行或 shell 脚本中使用`*`、`~`和`[]`而无需对其加引号。请参考第 824 页的“Z Shell Options”获取等效`zsh`选项。

设置后，`tsh`会将一个不匹配文件名的模糊引用传递给调用的命令。shell 不扩展该文件。当你没有设置`nonnonatch`时，`tsh`会生成`No match`错误消息且不执行命令。

```text
tsh $ cat questions?

cat: No match

tsh $ set nonnonatch

tsh $ cat questions?

cat: questions?: No such file or directory
```

设置后，每当你的一个后台作业完成时，`tsh`都会向终端发送消息。通常，`tsh`在下一个提示符出现之前立即通知你作业完成。请参阅第 554 页的“Job Control”。

# 控制结构

`pushdhome`当不带参数调用`pushd`时，它会将你移动到家主目录。这等同于`pushd -`。

`pushdsilent`设置后，`pushd`或`pop`都不打印目录栈。

`rmstar`设置后，每当你执行`rm *`时，shell 都会警告你并请求确认。

`verbose`当你使用`-v`选项调用它时，TC Shell 会声明此变量。你也可以使用`set`声明它。无论哪种情况，`verbose`都会导致`tsh`在历史替换后显示每个命令。请参阅第 686 页的“History”。

`visiblebell`设置后，听性蜂鸣声将被屏幕闪烁取代。

TC Shell 使用了许多与 Bourne Again Shell 相同的控制结构。在每情况下，语法是不同的，但效果是相同的。本节总结了两个 shell 中控制结构之间的差异。有关更多信息，请参阅第 626 页的“Control Structures”。

`if`控制结构的语法为：

```text
if (expression) simple-command
```

该控制结构仅适用于简单命令，不适用于管道或命令列表。你可以使用`if...then`控制结构（第 718 页）来执行更复杂的命令，例如如下：

```text
tcsh $ cat if_1

#!/bin/tcsh

# 用于显示简单 if

# 控制结构的例。

if ( $argv == 0 ) echo "if_1: there are no arguments
```

此程序检查它是否在没有任何参数的情况下被调用。（括号内的内容）评估为真——即如果命令行上有零个参数——`if`结构将显示相应效果的消息。

除了第 702 页描述的逻辑表达式外，你还可以使用根据文件状态返回值的表达式。此类表达式的语法为：`-n filename`

其中`n`来自表 14-9 中的列表。

# `n`的值

| | |
|---|---|
| `b` | 文件是块特殊设备文件。 |
| `c` | 文件是字符特殊设备文件。 |
| `d` | 文件是目录文件。 |
| `e` | 文件存在。 |
| `f` | 文件是普通文件。 |
| `g` | 文件设置了组 ID (set-group-ID) 位。 |
| `k` | 文件设置了粘性位 (sticky bit)。 |
| `l` | 文件是符号链接。 |
| `o` | 用户拥有该文件。 |
| `p` | 文件是命名管道 (FIFO)。 |
| `r` | 用户对文件有读取权限。 |
| `s` | 文件不是空的（具有非零大小）。 |
| `S` | 文件是 socket 特殊设备文件。 |
| `t` | 文件描述符（单个数字）已打开并连接到终端。 |
| `u` | 文件设置了用户 ID (set-user-ID) 位。 |
| `w` | 用户对文件有写入权限。 |
| `x` | 用户对文件有执行权限。 |
| `X` | 文件是由于搜索`Spath`中的目录而找到的内置命令或可执行文件。 |
| `z` | 文件长度为 0 字节。 |

如果指定的文件不存在或不可访问，测试将表达式评估为 0。如果测试结果为真，则表达式的值为 1；如果为假，表达式的值为 0。以下示例检查文件是否存在：

```text
tcsh $ cat if_1

!/bin/tcsh

# -f $1 ] && echo "Ordinary file"
```

当你声明`noclobber`时，`tsh`不扩展歧义的文件名。你可以在命令行或 shell 脚本中使用`*`、`~`和`[]`而无需对其加引号。请参考第 824 页的“Z Shell Options”获取等效`zsh`选项。

设置后，`tsh`会将一个不匹配文件名的模糊引用传递给调用的命令。shell 不扩展该文件……（此处原文重复逻辑）

如果指定的文件不存在或不可访问，测试将表达式评估为 0。如果测试结果为真，则表达式的值为 1；如果为假，表达式的值为 0。以下示例检查命令行上的文件是否存在：

```text
tcsh $ cat if_2

!/bin/tcsh

[ -f $1 ] && echo "Ordinary file"
```

