
```
% unalias fl
% aliases

cpto \!:1 \!$
dir echo Gilbers Directory List; ls -1 | more
```

## 别名总结

表 5.5 总结了三种 shell 中别名的使用方法。

表 5.5 别名总结

| 特性 | Korn 和 Bash | C |
|---|---|---|
| 定义 | `$ alias x=command` | `% aliases x command` |
| 参数 | 仅在末尾 | 任何位置 |
| 列出 | `$ aliases` | `% aliases` |
| 删除 | `$ unalias x y z` | `% unalias x y z` |
| 删除所有 | `$ unalias -a` | `% unalias *` |

## 5.12 变量

变量是内存中可以存储值的位置。每个 shell 都允许我们创建、存储和访问变量中的值。每个变量必须有一个名称。变量名必须以字母或下划线 `_` 开头。随后可以跟零或多个字母数字或下划线字符。变量大分为两类：用户定义和预定义。

![](img/6e4cdc423ec40606ea72b32fdafff220_197_0.png)

图 5.15 变量

### 用户定义变量

UNIX 中并没有单独定义用户变量。变量的首次引用会建立它。当我们书中稍之后讨论 shell 时，将对其进行详细说明。Korn 和 Bash shell 在变量中存储值的语法相同，但与 C shell 不同。

### 预定义变量

预定义变量用于配置用户的 shell 环境。例如，一个系统变量决定使用哪个编辑器来编辑命令历史。其他系统变量存储有关环境的信息。例如，一个系统变量包含主目录的路径。我们将在下一节中详细讨论这些变量。

### 在变量中存储数据

三个 shell 都提供了在变量中存储值的方法。遗憾的是，C shell 的方法不同。每个 shell 的基本命令如表 5.6 所示。

表 5.6 变量 shell 命令

| 操作 | Korn 和 Bash | C Shell |
|---|---|---|
| 赋值 | `variable=value` | `set variable = value` |
| 引用 | `$variable` | `$variable` |

#### 在 Korn 和 Bash Shell 中存储数据

Korn 和 Bash shell 使用赋值运算符 `=` 在变量中存储值。就像代数表达式一样，首先编码左侧变量，然后是赋值运算符，最后是需要存储的值。赋值运算符前后不能有空格；变量、运算符和值必须紧挨着按顺序连续编码，如下例所示：

```
varA=7
```

在此示例中，`varA` 是接收数据的变量，`7` 是存储在其中的值。

## 第 5 章 Shell 简介

a. `cd` 命令在当前目录中搜索 `reports` 目录。如果找到，当前目录将切换到 `reports`。

b. 如果在家目录中未找到 `reports` 目录，`cd` 会尝试在家目录中查找，这是 `CDPATH` 中的第二个项目。注意，家目录可能是当前目录。

同样，如果在家目录中找到了 `reports` 目录，它将成为当前目录。

c. 如果在家目录中未找到 `reports` 目录，`cd` 会尝试在 `/bin/usr/files` 中查找，这是 `CDPATH` 中的第三个项目。如果在 `/bin/usr/files` 中找到了 `reports` 目录，它将成为当前目录。

d. 如果在 `/bin/usr/files` 中未找到 `reports` 目录，`cd` 将显示错误信息并终止。

在会话 5.49 中，我们将 `CDPATH` 设置为之前示例所示的 `PATH`，然后输出了该路径。注意它以冒号开头，但由于我们使用了 `HOME`，因此 `HOME` 被替换为了它的绝对路径。

### 会话 5.49 设置 CDPATH

```
$ echo $CDPATH
$ CDPATH=$HOME:/bin/usr/files
```

```
$ echo $CDPATH
:/mnt/diska/staff/gilberg:/bin/usr/files
```

### HOME

`HOME` 变量包含你家目录的路径。默认值是你的登录目录。某些用户在需要家目录路径时会使用此变量的值。例如，当你不带任何参数地使用 `cd` 命令时，该命令会使用 `HOME` 的值作为参数。我们不建议更改它，因为它会影响所有使用它的命令和脚本。在会话 5.50 中，我们演示了如何将其更改为当前工作目录。注意由于 `pwd` 是一个命令，它必须包含在反引号。

### 会话 5.50 演示更改家目录

```
$ echo $HOME
:/mnt/diska/staff/gilberg
$ OLDHOME=$HOME
$ echo $OLDHOME
:/mnt/diska/staff/gilberg
```

```
$ HOME=$(pwd)
$ echo $HOME
:/mnt/diska/staff/gilberg/unix13bash
```

```
$ HOME=$OLDHOME
$ echo $HOME
:/mnt/diska/staff/gilberg
```

### PATH

`PATH` 变量用于搜索命令目录。`PATH` 变量中的项目必须用冒号分隔。

`PATH` 的工作原理与 `CDPATH` 相同。当 `SHELL` 遇到命令时，它会使用 `PATH` 变量中的项目在每个目录下搜索该命令。主要区别在于，出于安全考虑，例如防止木马病毒，我们应该将当前目录放在最后。

如果我们按照下一个示例所示设置 `PATH` 变量，

```
$ PATH=/bin:/usr/bin:
```

shell 将首先搜索 `/bin` 目录，然后是 `/usr/bin` 目录，最后是当前工作目录来查找 `date` 命令。

### 主提示符 (PSI Prompt)

主提示符在 Korn 和 Bash shell 以及 C shell 的提示符变量 `PS1` 中设置。当 shell 待接收命令时，会使用主提示符。Korn 和 Bash shell 的默认是美元符号 `$`，C shell 的默认是百分号 `#`。

我们可以像会话 5.51 所示更改提示符的值。我们首先更改主提示符，以反映我们正在使用的 shell，即 Korn shell。由于我们在提示符末尾有一个空格，因此必须使用引号来设置它。一旦设置，就会显示新的提示符。最后，我们将将其改回默认值。

### 会话 5.51 更改主提示符

```
$ PS1="KSH> ="
KSH> echo $PS1
KSH>
KSH> PS1="$ "
```

### SHELL

`SHELL` 变量持有你登录 shell 的路径。

### TERM

`TERM` 变量持有你正在使用的终端描述。该变量的值可以被 `vi` 或 `emacs` 等交互式命令使用。你可以测试此变量的值或重置它。

### 处理变量

我们需要设置、取消和显示变量。表 5.8 显示了如何这些操作。

#### 表 5.8 处理变量

| 操作 | Korn 和 Bash | C |
|---|---|---|
| 设置 | `set` | `set` |
| 取消 | `unset` | `unset` |
| 显示 | `echo` | `echo` |

## C Shell 选项

### 设置与取消选项

在 C shell 中，使用 `set` 命令设置选项，使用 `unset` 命令取消选项，但在两种情况下都不带减号 `minus sign`。下面的示例展示了这两种操作：

```
# set verbose      # 开启打印命令选项
# unset verbose     # 关闭打印命令选项
```

### 显示选项

要显示设置了哪些选项，我们使用不带参数的 `set` 命令。然而，C shell 会显示所有变量的设置情况，包括那些作为变量的 t 选项。选项之所以被识别，是因为它们没有被赋值：列表中仅列出它们的名称。下一个示例显示了选项的显示格式：

```
% C shell 格式：列出所有变量
```

## 5.15 Shell/环境自定义

UNIX 允许我们自定义所使用的 shell 和环境。当我们自定义环境时，可以对其进行扩展，以包含我们创建的子 shell 和程序。

自定义 shell 和环境有四个元素。根据建立它们的方式，它们可以是临时的或永久的。临时自定义仅对当前会话有效。当启动新会话时，原始设置将重新建立。

### 临时自定义

临时自定义用于更改当前会话或会话部分部分的 shell 环境和配置。通常，我们只对会话的部分时间进行自定义，例如当我们在处理某些特殊任务时。例如，如果我们正在编写脚本，在命令执行时查看展开后的命令会非常方便。我们通过开启 `verbose` 选项来实现这一点。当我们编写脚本时，我们会关闭 `verbose` 选项。会话期间更改的任何选项在下次登录时都会自动重置为默认值。

### 永久自定义
