
如果两个单词相同则为 *true*，如果不同则为 *false*。$word1 和 $word2 周围的双引号确保在输入包含空格或其他特殊字符的字符串时，测试能正常工作。

```
$ cat if1
read -p "word 1: " word1
read -p "word 2: " word2

if test "$word1" = "$word2"
then
    echo "Match"
fi
echo "End of program."

$ ./if1
word 1: peach
word 2: peach
Match
End of program.
```

在前面的示例中，*test 命令* 是 test "$word1" = "$word2"。test 内建命令如果其第一个和第三个参数之间存在由第二个参数指定的关系，则返回 *true* 状态。如果此命令返回 *true* 状态（= 0），Shell 会执行 *then* 和 *fi* 语句之间的命令。如果命令返回 *false* 状态（不等于 0），Shell 将控制权传递给 fi 之后的语句，而不会执行 *then* 和 *fi* 之间的语句。这个 if 语句的效果是，如果两个单词相同，则显示 *Match*。脚本总是显示 *End of program*。

在 Bourne Again Shell 中，*test* 是一个内建命令——是 Shell 的一部分。它也是一个独立的实用工具，位于 *usr/bin/test* 中。本章讨论并演示了许多 Bourne Again Shell 内建命令。如果可用，Shell 将使用内建版本；如果不可用，则使用实用工具。命令的每个版本在不同的 Shell 之间以及实用工具和 Shell 内建命令之间可能会略有不同。有关 Shell 内建命令的更多信息，请参阅第 1040 页。

下一个程序使用 *if* 结构在脚本开始时确认你在命令行上至少提供了一个参数。*test -eq* 标准比较两个整数；Shell 将展开 $@ 特殊参数（第 1027 页）为命令行参数的数量。如果你没有提供至少一个参数，此结构将显示一条消息并以退出状态 1 退出脚本。

```
$ cat chkargs
if test $# -eq 0
then
	echo "You must supply at least one argument."
	exit 1
fi
echo "Program running."

$ ./chkargs
You must supply at least one argument.
$ ./chkargs abc
Program running.
```

类似于 chkargs 中所示的测试是任何需要参数的脚本的关键组成部分。为了防止用户从脚本中接收无意义或令人困惑的信息，脚本需要检查用户是否提供了适当的参数。有些脚本仅测试参数是否存在（如 chkargs）；其他脚本则测试特定数量或特定类型的参数。

你可以使用 test 来验证文件参数的状态或两个文件参数之间的关系。在验证命令行上至少给出一个参数后，以下脚本测试该参数是否是普通文件的名称（不是目录或其他类型的文件）。带有 -f 标准和第一个命令行参数（$1）的 test 内建命令用于检查该文件。

```
$ cat is_ordfile
if test $# -eq 0
then
	echo "You must supply at least one argument."
	exit 1
fi
if test -f "$1"
then
	echo "$1 is an ordinary file."
else
	echo "$1 is NOT an ordinary file."
fi
```

你可以使用 test 标准测试文件的许多其他特性；参见表 27-1。

### 表 27-1 test 内建标准

| 标准 | 测试文件是否 |
|---|---|
| -d | 存在且是目录文件 |
| -e | 存在 |
| -f | 存在且是普通文件（不是目录） |
| -r | 存在且可读 |
| -s | 存在且大小大于 0 字节 |
| -w | 存在且可写 |
| -x | 存在且可执行 |

其他 **test** 标准提供了测试两个文件之间关系的方法，例如一个文件是否比另一个文件新。有关更多信息，请参阅本章后面的示例。

## 始终测试参数

> 为了使本书的示例简短并专注于特定概念，验证参数的代码通常会被省略或简写。对于其他人将使用的 Shell 程序，测试参数是一个好习惯。这样做可以使脚本更容易调试、运行和维护。

下面的示例——`chkargs` 的另一个版本——以 Linux Shell 脚本更传统的方式检查参数。此示例使用方括号 \[ \] 作为 `test` 的同义词。在脚本中，你可以用方括号包围 `test` 的参数，而不用使用单词 `test`。方括号必须被空白（空格或制表符）包围。

```
$ cat chkargs2
if [ $# -eq 0 ]
then
    echo "Usage: chkargs2 argument..." 1>&2
    exit 1
fi

echo "Program running..."
exit 0

$ ../chkargs2
Usage: chkargs2 argument...
$ ../chkargs2 abc
Program running...
```

`chkargs2` 显示的错误消息称为 *usage message*，并使用 `1>&2` 符号将其输出重定向到标准错误（第 335 页）。在发出 usage message 之后，`chkargs2` 以退出状态 1 退出，指示已发生错误。脚本末尾的 `exit 0` 命令使 `chkargs2` 在程序无错误运行后以 0 状态退出。如果你省略状态码，Bourne Again Shell 将返回脚本运行的最后一个命令的退出状态。

Usage message 常用于指定脚本所需的参数类型和数量。许多 Linux 实用工具提供类似于 `chkargs2` 中那样的 usage message。如果你以错误的数量或错误类型的参数调用实用工具或其他程序，它通常会显示 usage message。以下是当你仅用一个参数调用 `cp` 时显示的 usage message：

```
$ cp a
cp: missing destination file operand after 'a'
Try 'cp --help' for more information.
```

![](img/243613168ac865b539f12460d966088e_1043_0.png)

图 27-2 一个 if…then…else 流程图

## if…then…else

引入 else 语句将 if 结构变成了图 27-2 所示的双向分支。if…then…else 控制结构具有以下语法：

```
if test-command  then  commands  else  commands  fi
```

因为分号（;）和换行符（NEWLINE）都结束一个命令，所以你可以在 if 的同一行放置 then，只需在其前面加上分号即可。（因为 if 和 then 是单独的内建命令，它们之间需要一个控制运算符；分号和换行符同样有效 [第 341 页]。）有些人出于审美原因喜欢这种写法；其他人则因为它节省空间而喜欢。

```
if test-command; then  commands  else  commands  fi
```

![](img/243613168ac865b539f12460d966088e_1044_0.png)

图 27-3 一个 if…then…elif 流程图

如果 *test-command* 返回 *true* 状态，**if** 结构会执行 **then** 和 **else** 语句之间的命令，然后将控制权转向 **fi** 之后的语句。如果 *test-command* 返回 *false* 状态，**if** 结构会执行 **else** 语句之后的命令。

当你运行带有文件名参数的 **out** 脚本时，它会将在终端显示这些文件。如果第一个参数是 `-v`（在此情况下称为选项），**out** 使用 `less`（第 220 页）一次显示一个屏幕的文件。在确定它至少带有一个参数被调用后，**out** 测试其第一个参数以查看它是否为 `-v`。如果测试结果 *true*（第一个参数是 `-v`），**out** 使用 `shift` 内建命令（第 1025 页）移位参数以去除 `-v`，并使用 `less` 显示文件。如果测试结果 *false*（第一个参数 *不是* `-v`），脚本使用 `cat` 显示文件。

```
$ cat out
if [ $# -eq 0 ]
then
echo "Usage: $0 [-v] filenames..." 1>&2
exit 1
fi
if [ "$1" = "-v" ]
then
shift
less -- "$@"
else
cat -- "$@"
fi
```

**可选** 在 out 中，cat 和 less 的 -- 参数告诉这些实用工具命令行上没有更多选项跟随，并且不将后续列表中的前导连字符 (-) 视为指示选项。因此，-- 允许你查看名称以连字符开头的文件（第 146 页）。虽然不常见，但以连字符开头的文件名偶尔会发生。（你可以通过使用命令 cat > -fname 创建这样的文件。）-- 参数适用于所有使用 getopts 内建命令（第 1052 页）解析其选项的 Linux 实用工具；但它不适用于更多和少数其他实用工具。当你使用 rm 删除名称以连字符开头的文件（rm -- -fname）时，包括你在实验 -- 参数时创建的任何文件，这个参数特别有用。

## if...then...elif

if...then...elif 控制结构（图 27-3）具有以下语法：

```
if test-command
then
commands
elif test-command
then
commands
...
else
commands
fi
```

elif 语句结合了 else 语句和 if 语句，使你可以构建嵌套的 if...then...else 结构集合（图 27-3）。else 语句和 elif 语句的区别在于，每个 else 语句必须与一个 fi 语句配对，而多个嵌套的 elif 语句只需要一个结束 fi 语句。

