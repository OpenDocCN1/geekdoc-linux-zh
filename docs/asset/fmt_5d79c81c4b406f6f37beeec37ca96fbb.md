
| `++ val` | 前置递增 |
| `-- val` | 前置递减 |
| `!` | 逻辑非 |
| `~` | 按位非 |
| `**` | 乘方 |
| `<<` | 按位左移 |
| `>>` | 按位右移 |
| `&` | 按位布尔 AND |
| `|` | 按位布尔 OR |
| `&&` | 逻辑 AND |
| `||` | 逻辑 OR |

你可以将双括号命令用于 `if` 语句中，也可以用于脚本中作为普通命令来赋值：

```bash
$ cat DoubleParentheses.sh
#!/bin/bash
# Testing a double parentheses command
#
val1=10
#
if (( $val1 ** 2 > 90 ))
then
    (( val2 = $val1 ** 2 ))
    echo "The square of $val1 is $val2,"
    echo "which is greater than 90."
#
fi
$ ./DoubleParentheses.sh
The square of 10 is 100,
which is greater than 90.
$
```

请注意，在双括号内的表达式中，无需转义大于号（greater-than symbol）。这是双括号命令之外的另一个高级特性。

## 使用双方括号

双方括号命令为字符串比较提供了高级功能。以下是双方括号命令的格式：

```text
[[ expression ]]
```

带双方括号的表达式使用 `test` 评估中标准的字符串比较。然而，它提供了一种 `test` 评估没有的功能——模式匹配。

> **注意**
>
> 双方括号在 Bash shell 中工作良好。但请注意，并非所有 shell 都支持双方括号。

在模式匹配中，你可以定义一个正则表达式（在第 20 章“正则表达式”中详细讨论），并将其与字符串值进行匹配：

```bash
$ cat DoubleBrackets.sh
#!/bin/bash
# Using double brackets for pattern matching
#
#if [[ $BASH_VERSION == 5.* ]]
then
    echo "You are using the Bash Shell version 5 series."
fi
$
$ ./DoubleBrackets.sh
You are using the Bash Shell version 5 series.
$
```

在上面的脚本中请注意，使用了双等号（`==`）。这些双等号将右侧的字符串（`5.*`）指定为模式，并应用模式匹配规则。双方括号命令将 `$BASH_VERSION` 环境变量进行匹配，以检查它是否以 `5.` 字符串开头。如果是，比较成功，shell 将执行 `then` 部分的命令。

## 考虑使用 case 命令

通常，你会发现自己正在评估一个变量的值，试图在一组可能的值中找到特定的值。在这种情况下，你不得不编写一个冗长的 `if`-then-else 语句，如下所示：

```bash
$ cat LongIf.sh
#!/bin/bash
# Using a tedious and long if statement
#
if [ $USER == "rich" ]
then
	echo "Welcome $USER"
	echo "Please enjoy your visit."
elif [ $USER == "barbara" ]
then
	echo "Hi there, $USER"
	echo "We're glad you could join us."
elif [ $USER == "christine" ]
then
	echo "Welcome $USER"
	echo "Please enjoy your visit."
elif [ $USER == "tim" ]
then
	echo "Hi there, $USER"
	echo "We're glad you could join us."
elif [ $USER == "testing" ]
then
	echo "Please log out when done with test."
else
	echo "Sorry, you are not allowed here."
fi
$
$ ./LongIf.sh
Welcome christine
Please enjoy your visit.
$
```

`elif` 语句继续 `if`-then 检查，针对单个比较变量寻找特定的值。

与其编写所有的 `elif` 语句来继续检查相同的变量值，你可以使用 `case` 命令。`case` 命令以列表导向的格式检查单个变量的多个值：

### 通过一个实际示例进行操作

在本节中，我们将描述一个脚本，该脚本将本章中介绍的 shell 结构命令付诸实用——确定当前系统上有哪些可用的包管理器。它还通过安装的包管理器作为参考，推测当前系统基于哪个 Linux 发行版。

为了进行分析，该脚本首先检查标准的基于 Red Hat 的包管理器（`rpm`、`dnf` 和 `flatpak`）。它对每个包管理器使用 `which` 命令，并在 `if` 条件语句中使用单括号。如果找到该包管理器，则针对该特定管理器的特殊布尔变量被设置为 `TRUE` (1)；如果未找到，则设置为 `FALSE` (0)，如下面的片段所示：

```bash
$ cat PackageMgrCheck.sh
#!/bin/bash
[...]
if (which rpm &> /dev/null)
then
    item_rpm=1
    echo "You have the basic rpm utility."
#
else
    item_rpm=0
#
fi
[...]
if (which flatpak &> /dev/null)
then
    item_flatpak=1
    echo "You have the flatpak application container."
#
else
    item_flatpak=0
#
fi
[...]
$
```

对于 `dnf` 和 `yum` 有特殊处理（详见第 9 章“安装软件”），以应对您正在较旧的基于 Red Hat 的发行版上运行该脚本且该发行版尚未具备 `dnf` 工具的情况。请注意，如果未找到 `dnf`，则使用 `elif` 语句来检查 `yum`：

```bash
$ cat PackageMgrCheck.sh
[...]
if (which dnf &> /dev/null)
then
    item_dnfyum=1
    echo "You have the dnf package manager."
elif (which yum &> /dev/null)
then
    item_dnfyum=1
    echo "You have the yum package manager."
else
    item_dnfyum=0
#
fi
[...]
$
```

> **注意**
>
> 在单括号内的 `which` 命令之后使用了输出重定向。基于第 10 章“使用编辑器”中介绍的内容，`which` 命令的常规（标准）输出和任何错误消息都通过 `&>` 符号进行重定向。它们被重定向到 `/dev/null`，这幽默地被称为黑洞，因为放入其中的东西永远不会出来。这一操作显著清理了脚本的输出，但并不会对其完整性产生不利影响。错误重定向在第 15 章中有更详细的介绍。

在脚本完成对系统的包管理器分析后，它计算一个得分（`redhatscore`）。这个得分稍后用于提出关于该系统发行版基础的假设：

```bash
$ cat PackageMgrCheck.sh
[...]
redhatscore=$[item_rpm + $item_dnfyum + $item_flatpak]
[...]
$
```

当基于 Red Hat 的包管理器审计完成后，开始进行基于 Debian 的分析。它与基于 Red Hat 的评估非常相似，只是涵盖了基于 Debian 的包管理器（`dpkg`、`apt`、`snap`），并确定一个 Debian 得分，如下面的片段所示：

```bash
$ cat PackageMgrCheck.sh
[...]
if (which dpkg &> /dev/null)
then
    item_dpkg=1
    echo "You have the basic dpkg utility."
#
else
    item_dpkg=0
#
fi
[...]
debeanscore=$[item_dpkg + $item_aptget + $item_snap]
[...]
$
```

比较两个得分 `redhatscore` 和 `debeanscore`，并声明一个发行版的判定结果：
