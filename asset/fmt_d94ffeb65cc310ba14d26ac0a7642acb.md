
# 第 8 章：编写 Korn Shell 脚本

也可以使用自动别名来定义自动加载函数。在大多数系统中，它被预设置为 `typeset -fu`。

`FPATH` 变量包含了搜索自动加载函数的路径名，必须设置并包含至少一个目录，自动加载函数才能工作。

## 律令函数 (Discipline Functions)

律令函数是 KornShell 93 中的新功能。它们是用于操作变量的特殊类型函数。它们被定义但没有被显式调用。相反，每当与函数相关的变量被访问时，它们就会被调用。

律令函数的命名和访问有一些特定规则。首先，律令函数使用以下语法命名：

`name.function`

注意函数由由点隔的两个部分组成。第一部分对应变量名，第二部分必须是 `get`、`set` 或 `unset`。这些对应于变量的以下操作：

- `get`：每当访问基础律令变量时触发
- `set`：每当基础律令变量被设置时触发
- `unset`：每当基础律令变量被取消时触发

例如，每当变量 `LBIN` 被访问、设置或取消时，就会调用律令函数 `LBIN.get`、`LBIN.set` 和 `LBIN.unset`。

所有三个律令函数都是可选的，因此不需要全部指定。

在律令函数内部，可以使用以下特殊保留变量：

- `.sh.name`：当前变量名
- `.sh.value`：当前变量的值
- `.sh.subscript`：下标名称（如果是数组变量）

从实用性角度来看，律令函数通常通过跟踪运行脚本中变量的设置过程和当前值来帮助调试。这里有一个可以用于跟踪设置 X 值的函数：

``` 
function X.set {
    print "DEBUG: ${.sh.name} = ${.sh.value}"
}
```

律令函数也是完善变量赋值验证规则的好地方。这里有一个函数，用于检查确保 X 被设置为 3 到 10 之间的数字：

``` 
function X.set {
    if (( .sh.value<3 || .sh.value >10 ))
    then
        print "Bad value for ${.sh.name}: ${.sh.value}"
}
```

注意，内置函数也可以用作额外的律令函数使用。

## `FPATH`

`FPATH` 变量包含一个由冒号分隔的目录列表，在调用自动加载函数时进行检查。它类似于 `PATH` 和 `CDPATH`，不同之处在于 Korn shell 检查的是函数文件，而不是命令或目录。`FPATH` 中的每个目录都会从左到右搜索与函数名匹配的文件。一旦找到，它将在当前环境中读取并执行。通过下面的 `FPATH` 设置，如果调用了自动加载函数 `lsf`，Korn shell 将在 `/home/anatole/.fdir` 中检查名为 `lsf` 的文件，然后在 `/etc/.functions` 中检查，如果存在则读取并执行：

```
$ print FPATH
/home/anatole/.fdir:/etc/.functions
```

FPATH 没有默认值，因此如果没有显式设置，此功能将启用。

## 移除函数定义

使用 `unset -f` 命令移除函数。这用于从当前环境中移除函数。

## 陷阱 (Traps)

`trap` 命令用于在接收信号时执行命令。陷阱对于控制 Korn shell 脚本中的副作用非常有用。`trap` 命令可以处理如 Ctrl-C 这样的信号。

### 忽略信号

可以通过指定空命令来使用 `trap` 命令来忽略信号：

```
$ trap "" 2 3
```

### 重置陷阱

`trap` 命令也可以通过省略命令参数将陷阱重置为默认操作：

- `trap -`
- `trap signals`

### 退出与陷阱

可以设置陷阱在 Korn shell 脚本退出时执行。这是通过在 `trap` 命令中使用 `0` 或 `EXIT` 作为信号参数来实现：

- `trap 'commands' 0`
- `trap 'commands' EXIT`

这可以将 Korn shell 脚本的清理工作集中在一个地方。`trap_test` 脚本包含一个陷阱命令，在脚本执行完成后打印消息：

```
$ cat trap_test
trap 'print exit being executed' EXIT
print "This is just a test"
$ trap_test
This is just a test
exit being executed
```

### 使用 `trap` 调试

`trap` 命令对于调试 Korn shell 脚本非常有帮助。特殊的信号参数 `DEBUG` 和 `ERR` 用于在每条命令执行后或仅在脚本失败时执行陷阱命令。

### 陷阱信号优先级

如果设置了多个陷阱，优先级顺序为：

- `DEBUG`
- `ERR`
- 信号数字
- `EXIT`

### 捕捉键盘信号

Korn shell 捕获 `KEYBD` 信号（当你输入字符时发送），并自动分配以下保留变量：

```
.sh.edchar 包含键序列的最后一个字符
.sh.edtext 包含当前输入行
.sh.edmode 包含空字符（或转义字符）
```

## 调试 Korn Shell 脚本

**表 8.9: Korn Shell 调试选项**

| 选项 | 描述 |
| --- | --- |
| `set -e`, `set -o errexit` | 当任何命令以非零状态退出时执行 ERR 陷（如果已设置） |
| `set -n`, `set -o noexec` | 在不执行的情况下读取命令 |
| `set -v`, `set -o verbose` | 按照读取顺序显示输入行 |
| `set -x`, `set -o xtrace` | 在执行时显示命令及其参数 |
| `typeset -ft function` | 在执行时显示函数中的命令和参数 |

Korn shell 提供了许多调试脚本非常有用的选项：`noexec`、`verbose` 和 `xtrace`。`noexec` 选项导致命令在不执行的情况下被读取。它被用于检查 Korn shell 脚本中的语法错误。`verbose` 选项会在读取输入时显示内容。`xtrace` 选项会在执行脚本时显示脚本中的命令。这是最有用且通用的调试选项。

### 启用调试选项

这些选项的启用方式与其他选项相同。

你可以在启用选项的情况下调用脚本：

```
$ ksh -option script
```

在启用选项的情况下调用子 shell：

```
$ ksh -option
$ script
```

在调用脚本之前全局设置该选项：

```
$ set -option
$ script
```

或者在脚本内部设置该选项。

```
$ cat script
. .
set -option
. .
```

### 调试示例

这是一个名为 `dbtest` 的 Korn shell 脚本。它将变量 `X` 设置为 `ABC`，然后检查该值并打印消息。注意第 2 行有一个未匹配的双的双引号：

```
$ cat dbtest
X=ABC
if [ $X = "foo"
then
    print "X is set to ABC"
fi
```

```
$ ksh -n dbtest
dbtest[2]: syntax error at line 2: "unmatched {:?
```

当在执行 Korn shell 脚本时检测到错误，将显示脚本或函数的名称、错误信息以及包含在 `['']` 中的行号。对于函数，显示的是相对于函数开头的行号。`dbtest` 脚本已修复并使用 `noexec` 选项再次运行：

```
$ ksh -n dbtest
$
```

这次没有标记错误，但请注意没有生成输出。这是因为 `noexec` 选项导致命令被读取但未被执行。现在使用 `xtrace` 选项运行 `dbtest` 脚本：

```
$ ksh -x dbtest
+ alias -x echo=print
+ alias -x vi=SHELL=/bin/sh vi
+ PS0=!
+ PS1=!:/home/anatole/bin>
+ typeset -fx cd md
+ typeset -x EDITOR=vi
+ X=ABC
+ [ X = ABC ]
+ print X is set to ABC
X is set to ABC
```

现在有大量的输出，大部分是处理环境文件时的执行跟踪输出。`PS4` 的值显示在每行执行跟踪之前。如果没有显式重置，默认值是字符 `+`。通过在 `PS4` 设置中包含 `LINENO`，也可以在调试提示中包含行号。

```
$ typeset -x PS4='[$LINENO] '
```

现在行号以括号显示在跟踪输出中：
