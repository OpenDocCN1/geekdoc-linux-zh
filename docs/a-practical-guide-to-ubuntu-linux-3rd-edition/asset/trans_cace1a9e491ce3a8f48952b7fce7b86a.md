
# 图 27-1 if...then 流程图

![](img/2344fc4a798f29dca9e8b5ed7288171a_1005_0.png)

在语法描述中，**粗体** 单词是你提供的项，以使结构产生所需的效果。*非粗体* 单词是 shell 用于识别控制结构的关键词。

图 27-1 表明 **if** 语句测试 *test-command* 返回的状态，并根据该状态转移控制权。**if** 结构的结尾由一个 **fi** 语句标记（即 **if** 拼写倒序）。以下脚本提示输入两个单词，读取它们，然后使用 **if** 结构根据 **test** 内建命令比较这两个单词时返回的结果来执行命令。（有关 **test** 实用程序的信息，请参阅 **test** 信息页，该实用程序类似于 **test** 内建命令。）如果两个单词相同，**test** 内建命令返回 *true* 状态；如果不同，则返回 *false* 状态。$word1 和 $word2 周围的引号确保如果你输入包含 SPACE 或其他特殊字符的字符串，test 能正常工作：

```bash
$ cat if1
echo -n "word 1: "
read word1
echo -n "word 2: "
read word2

if test "$word1" = "$word2"
    then echo "Match"
fi
echo "End of program."
```

# 第 27 章 编程 BOURNE AGAIN SHELL

```bash
$ ./if1
word 1: peach
word 2: peach
Match
End of program.
```

在上面的示例中，*test-command* 是 test *$word1* = *$word2*。如果 test 内建命令的第一个和第三个参数之间存在第二个参数指定的关系，则返回 *true* 状态。如果该命令返回 *true* 状态（零），shell 执行 *then* 和 *fi* 语句之间的命令。如果命令返回 *false* 状态（非零），shell 会跳过 *then* 和 *fi* 之间的语句，直接执行 *fi* 之后的语句。此 *if* 语句的效果是：如果两个单词相同，则显示 *Match*。该脚本始终显示 *End of program*。

- **内建命令**
  在 Bourne Again Shell 中，*test* 是一个内建命令——shell 的一部分。它也是一个保留在 **/usr/bin/test** 中的独立实用程序。本章讨论并演示了许多 Bourne Again Shell 内建命令。如果可用，你通常使用内建版本；如果不可用，则使用实用程序版本。某个命令的每个版本从一个 shell 到下一个 shell，或从实用程序到任何 shell 内建命令可能略有不同。有关 shell 内建命令的更多信息，请参阅第 1002 页。

- **检查参数**
  下一个程序在脚本开头使用一个 *if* 结构，以确认你在命令行上至少提供了一个参数。test -eq 运算符比较两个整数；特殊参数 *$#*（第 997 页）取值为命令行参数的数量。如果你没有提供至少一个参数，此结构会显示一条消息并以退出状态 1 退出脚本：

```bash
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

像 *chkargs* 中所示的测试是任何需要参数的脚本的关键组成部分。为了防止用户从脚本中接收无意义或令人困惑的信息，脚本需要检查用户是否提供了适当的参数。有些脚本仅测试是否存在参数（如 *chkargs*）。其他脚本测试特定数量或特定类型的参数。

你可以使用 *test* 来验证文件参数的状态或两个文件参数之间的关系。在验证命令行上已给出至少一个参数后，以下脚本测试该参数是否为工作目录中普通文件（不是目录或其他类型的文件）的名称。使用带有 -f 选项的 test 内建命令和第一个命令行参数（$1）检查该文件：

```bash
$ cat is_ordinary
if test $# -eq 0
then
    echo "You must supply at least one argument."
    exit 1
fi
if test -f "$1"
then
    echo "$1 is an ordinary file in the working directory"
else
    echo "$1 is NOT an ordinary file in the working directory"
fi
```

你可以使用 test 选项测试文件的许多其他特性；参见表 27-1。

### 表 27-1 test 内建命令的选项

| 选项 | 测试文件是否... |
| :--- | :--- |
| -d | 存在且是目录文件 |
| -e | 存在 |
| -f | 存在且是普通文件（不是目录） |
| -r | 存在且可读 |
| -s | 存在且大小大于 0 字节 |
| -w | 存在且可写 |
| -x | 存在且可执行 |

其他 test 选项提供了测试两个文件之间关系的方法，例如一个文件是否比另一个文件新。有关更多信息，请参阅本章后续的示例。

### 始终测试参数

> **提示** 为了使本书中的示例简短并专注于特定概念，验证参数的代码通常会被省略或缩写。在供他人使用的 shell 程序中测试参数是一种良好的实践做法。这样做可使脚本更容易运行和调试。

> [!] 是 test 的同义词

以下示例——chkargs 的另一个版本——以一种更符合 Linux shell 脚本传统的方式检查参数。此示例使用 test 的括号（[!]）同义词。在脚本中，你可以用括号包围 test 的参数，而不使用单词 test。括号必须被空白（SPACE 或 TAB）包围。

```bash
$ cat chkgargs2
if [ $# -eq 0 ]
then
    echo "Usage: chkgargs2 argument..." 1>&2
    exit 1
fi
echo "Program running."
exit 0

$ ./chkgargs2
Usage: chkgargs2 argument...

$ ./chkgargs2 abc
Program running.
```

**用法消息** `chkgargs2` 显示的 错误消息称为用法消息，并使用 `1>&2` 表示法将其输出重定向到标准错误（第 297 页）。发出用法消息后，`chkgargs2` 以退出状态 1 退出，表示已发生错误。脚本末尾的 `exit 0` 命令使 `chkgargs2` 在程序无错误运行后以 0 状态退出。如果你省略状态码，Bourne Again Shell 会返回 0 状态。

用法消息通常用于指定脚本接受的参数类型和数量。许多 Linux 实用程序提供类似于 `chkgargs2` 中那样的用法消息。如果你以错误的数量或错误类型的参数调用实用程序或其他程序，它通常会显示一条用法消息。以下是当你不带任何参数调用 `cp` 时显示的用法消息：

```bash
$ cp
cp: missing file operand
Try 'cp --help' for more information.
```

# if...then...else

引入 else 语句将 `if` 结构转变为图 27-2 所示的双向分支。if...then...else 控制结构具有以下语法：

```
if test-command
    then
    commands
    else
    commands
fi
```

由于分号 (;) 和 NEWLINE 一样都结束一条命令，因此你可以通过在 `then` 前加分号将其放在与 `if` 相同的行上。（由于 `if` 和 `then` 是独立的内建命令，它们之间需要一个命令分隔符；分号和 NEWLINE 效果相同 [第 304 页]。）有些人出于美观原因更喜欢这种表示法；其他人则喜欢它因为它节省空间。

```
if test-command; then
    commands
    else
    commands
fi
```

# 图 27-2 if...then...else 流程图

![](img/2344fc4a798f29dca9e8b5ed7288171a_1009_0.png)

如果 test-command 返回 true 状态，if 结构执行 then 和 else 语句之间的命令，然后将控制权转移到 fi 之后的语句。如果 test-command 返回 false 状态，if 结构执行 else 语句之后的命令。

当你使用文件名作为参数运行 out 脚本时，它会在终端上显示这些文件。如果第一个参数是 -v（在这种情况下称为选项），out 会使用 less（第 162 页）逐屏显示文件。在确定它被调用时至少带有一个参数后，out 测试其第一个参数以查看它是否为 -v。如果测试结果 true（第一个参数是 -v），out 使用 shift 内建命令（第 998 页）移动参数以去除 -v，并使用 less 显示文件。如果测试结果 false（第一个参数不是 -v），脚本使用 cat 显示文件：

```bash
$ cat out
if [ $# -eq 0 ]
then
    echo "Usage: out [-v] filenames..." 1>&2
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

