
```
[me@linuxbox ~]$ read-multiple
Enter one or more values > a b c d e
var1 = 'a'
var2 = 'b'
var3 = 'c'
var4 = 'd'
var5 = 'e'
[me@linuxbox ~]$ read-multiple
Enter one or more values > a
var1 = 'a'
var2 = ''
var3 = ''
var4 = ''
var5 = ''
[me@linuxbox ~]$ read-multiple
Enter one or more values > a b c d e f g
var1 = 'a'
var2 = 'b'
var3 = 'c'
var4 = 'd'
var5 = 'e f g'
```

如果 `read` 接收到的值少于预期数量，多余的变量为空，而过多的输入会导致最后一个变量包含所有额外输入。

如果在 `read` 命令之后没有列出变量，则 shell 变量 `REPLY` 将被分配所有输入：

```
#!/bin/bash

# read-single: read multiple values into default variable
echo -n "Enter one or more values > "
read
echo "REPLY = '$REPLY'"
```

运行此脚本的结果如下：

```
[me@linuxbox ~]$ read-single
Enter one or more values > a b c d
REPLY = 'a b c d'
```

### Options

`read` 支持以下选项：

Table 29-1: read Options

| Option | Description |

|---|---|

| `-a array` | 将输入分配给 `array`，从索引零开始。我们将在第 36 章介绍数组。 |

| `-d delimiter` | 字符串 `delimiter` 中的第一个字符用于指示输入结束，而不是换行符。 |

| `-e` | 使用 Readline 处理输入。这允许以与命令行相同的方式编辑输入。 |

| `-n num` | 读取 `num` 个字符的输入，而不是整行。 |

| `-p prompt` | 使用字符串 `prompt` 显示输入提示。 |

| `-r` | 原始模式。不要将反斜杠字符解释为转义字符。 |

| `-s` | 静默模式。输入时不要将字符回显到显示器。这在输入密码和其他机密信息时很有用。 |

| `-t seconds` | 超时。在 `seconds` 后终止输入。如果输入超时，`read` 将返回非零退出状态。 |

| `-u fd` | 使用文件描述符 `fd` 的输入，而不是标准输入。 |

使用各种选项，我们可以对 `read` 做一些有趣的事情。例如，使用 `-p` 选项，我们可以提供提示字符串：

```
#!/bin/bash

# read-single: read multiple values into default variable

read -p "Enter one or more values > "

echo "REPLY = '$REPLY'"
```

使用 `-t` 和 `-s` 选项我们可以编写一个脚本来读取“秘密”输入，并在指定时间内未完成输入时超时：

```
#!/bin/bash

# read-secret: input a secret pass phrase

if read -t 10 -sp "Enter secret pass phrase > " secret_pass; then
    echo -e "\nSecret pass phrase = '$secret_pass'"
else
    echo -e "\nInput timed out" >&2
    exit 1
fi
```

该脚本提示用户输入秘密密码短语并等待十秒钟输入。如果在指定时间内未完成输入，脚本将以错误退出。由于包含 `-s` 选项，密码短语的字符在输入时不会回显到显示器。

在 `/etc/passwd` 文件中。

第二个有趣的行是这行：

```
IFS=":" read user pw uid gid name home shell <<< "$file_info"
```

该行由三部分组成：一个变量赋值、一个带有变量名列表作为参数的 `read` 命令，以及一个奇怪的新的重定向操作符。我们先来看变量赋值。

`shell` 允许在命令之前立即进行一个或多个变量赋值。这些赋值会改变随后命令的环境。赋值的效果是临时的；仅在命令执行期间改变环境。在我们的例子中，`IFS` 的值被更改为冒号字符。或者，我们也可以这样编写：

```
OLD_IFS="$IFS"
IFS=":"
read user pw uid gid name home shell <<< "$file_info"
IFS="$OLD_IFS"
```

其中我们存储 `IFS` 的值，分配一个新值，执行 `read` 命令，然后将 `IFS` 恢复到其原始值。显然，将变量赋值放在命令前面是一种更简洁的做同样事情的方法。

`<<<` 操作符表示 here string。here string 类似于 here document，只是更短，由单个字符串组成。在我们的例子中，来自 `/etc/passwd` 文件的数据行被馈送到 `read` 命令的标准输入。我们可能会想知道为什么选择这种相当迂回的方法而不是：

```
echo "$file_info" | IFS=":" read user pw uid gid name home shell
```

嗯，有原因的...

### You Can’t Pipe read

虽然 `read` 命令通常从标准输入获取输入，但你不能这样做：

```
echo "foo" | read
```

我们期望这能工作，但它不起作用。命令看起来会成功，但 `REPLY` 变量将始终为空。为什么会这样？

解释与 `shell` 处理管道的方式有关。在 `bash` 和其他 `shell` 如 `sh` 中，管道会创建子 `shell`。这些是 `shell` 及其环境的副本，用于执行管道中的命令。在上面的例子中，`read` 在子 `shell` 中执行。

在类 Unix 系统中，子 `shell` 为进程执行时创建环境的副本。当进程结束时，环境的副本会被销毁。这意味着子 `shell` 永远无法更改其父进程的环境。`read` 会分配变量，这些变量随后成为环境的一部分。在上面的例子中，`read` 在其子 `shell` 的环境中将值“foo”分配给变量 `REPLY`，但当命令退出时，子 `shell` 及其环境被销毁，赋值的效果就丢失了。

使用 here string 是规避这种行为的一种方法。另一种方法在第 37 章中讨论。

### Validating Input

有了我们新的键盘输入能力，就带来了一个额外的编程挑战，即验证输入。经常，优秀程序与糟糕程序之间的区别在于程序处理意外的能力。经常，意外以错误输入的形式出现。我们在上一章的求值程序中已经做了一点这方面的事，在那里我们检查了整数的值并筛除了空值和非数字字符。每次程序接收输入时进行这种编程检查都很重要，以防止无效数据。这对于由多个用户共享的程序尤其重要。如果一个程序仅供作者使用一次来执行某些特殊任务，出于经济考虑省略这些保护措施是可以原谅的。即便如此，如果程序执行删除文件等危险任务，包含数据验证也是明智的，以防万一。

这里有一个验证各种输入的示例程序：

```
#!/bin/bash

# read-validate: validate input

invalid_input () {
    echo "Invalid input  $REPLY" >&2
    exit 1
}
```
