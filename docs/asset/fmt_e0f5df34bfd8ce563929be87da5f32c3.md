
# 第 2 章

注意，我们在本示例中没有使用任何文件名扩展名或后缀：Linux（以及整个 UNIX 系统）很少使用文件名扩展名来确定文件类型。如果我们愿意，可以使用 `sh` 或添加不同的扩展名，shell 并不在乎这些。大多数预装脚本都没有任何文件名扩展名，检查它们是否为脚本的最好方法是使用 `file` 命令，例如，执行 `file first` 或 `file /bin/bash`。请使用适用于你工作或适合你的任何约定。

## 使脚本具有可执行性

现在我们已经有了脚本文件，可以通过两种方式运行它。更简单的方法是将脚本文件名作为参数调用 shell，然后执行：

```bash
$ /bin/bash first
```

这应该可以工作，但如果我们能直接通过输入脚本名称来调用它，使其获得与其他 Linux 命令同等的地位，那就更好了。

我们通过使用 `chmod` 命令更改文件模式，使所有用户都能执行该文件：

```bash
$ chmod +x first
```

> 当然，这不是使用 `chmod` 使文件可执行的唯一方法。使用 `man chmod` 可以找到更多关于参数和其他选项的信息。

现在我们使用命令来执行它。

```bash
$ first
```

你可能会得到一个提示未找到命令的错误。这几乎肯定是因为 shell 环境的 `PATH` 没有设置为在当前目录查找要执行的命令。要更改此，可以在命令行上输入 `PATH=$PATH;`，或者编辑你的 `.bash_profile` 文件将此命令添加到文件末尾；然后注销并重新登录。或者，在包含脚本的目录中使用 `./first`，以给 shell 提供文件的完整相对路径。

指定带有 `.` 前缀的路径确实有一个优势：它确保你不会意外执行系统上与你的脚本文件同名的另一个命令。

> 你不应该像这样为用户修改 `PATH` 变量。这是一个安全漏洞，因为以 `root` 身份登录的系统管理员可能会被误导调用标准命令的虚假版本。其中一人曾承认这样做过一次，当然，只是为了向系统管理员证明某个观点！对于普通账户，将当前目录包含在路径中有微小的风险，因此如果你特别担心，只需养成在所有本地目录的命令前加上 `./` 的习惯即可。

## Shell 编程

一旦你确认脚本运行正常，你就可以将其移动到比当前目录更合适的位置。如果只是供自己使用，你可以在家目录下创建一个 `bin` 目录并将其添加到路径中。如果你想让其他人也能执行该脚本，可以使用 `/usr/local/bin` 或另一个系统目录作为添加新程序的方便位置。如果你在系统上没有 `root` 权限，可以请求系统管理员为你复制文件，尽管你可能需要说服他它的价值。为了防止其他用户意外更改脚本，你应该删除它的写权限。管理员设置所有权和权限的命令序列如下：

```bash
## cp first /usr/local/bin
## chown root /usr/local/bin/first
## chgrp root /usr/local/bin/first
## chmod 755 /usr/local/bin/first
```

注意，我们没有修改修改权限标志的特定部分，而是使用了 `chmod` 的绝对形式，因为我们确切知道需要哪些权限。

如果你愿意，可以使用 `chmod` 命令更长但可能更直观的形式，即如下：

```bash
## chmod u=rx,go=rx /usr/local/bin/first
```

查看 `chmod` 的手册页以获取更多细节。

> 在 Linux 中，如果你对包含文件的目录具有写权限，你就可以删除该文件。为了安全起见，你应该确保只有超级用户才能写入你想保留的安全文件的目录。这是有意义的，因为目录只是另一个文件，对目录文件的写权限允许用户添加或删除名称。

## Shell 语法

现在我们已经看了一个简单所有权程序的示例，现在是时候深入研究 shell 的编程能力了。shell 是一种非常容易学习的编程语言，这是因为在将它们组合成更大的脚本之前，很容易交互式地测试较小的程序片段。我们可以使用 `bash` shell 编写非常大的结构化程序。在接下来的章节中，我们将涵盖：

- 变量：字符串、数字、环境和参数

- 条件：shell 布尔值

- 程序控制：`if`, `elif`, `for`, `while`, `until`, `case`

- 列表

- 函数

- shell 内置命令

- 获取命令的结果

- Here documents（在此文档中的字符串）

# 第 2 章

## 变量

我们通常不在 shell 中在使用变量之前声明它们。相反，我们通过简单地使用它们来创建它们（例如，当我们为它们分配初始值时）。默认情况下，所有变量都被视为并存储为字符串，即使它们被分配了数值。shell 和一些实用工具会将数字字符串转换为其值，以便按需要对其操作。Linux 是一个大小敏感的系统，因此 shell 认为变量 `foo` 与 `Foo` 不同，且两者都与 `FOO` 不同。

在 shell 中，我们通过在变量前加上 `$` 来访问变量的内容。当我们提取变量内容时，只需使用变量名，如果需要，它是动态创建的。检查变量内容的简单方法是将其 `echo` 到终端，并在它的名称前加上 `$`

在命令行上，我们可以通过设置和检查变量 `salutation` 的值看到实际操作：

```bash
$ salutation=Hello
$ echo $salutation
Hello
$ salutation="Yes Dear"
$ echo $salutation
Yes Dear
$ salutation=7+5
$ echo $salutation
7+5
```

> 注意，如果字符串包含空格，必须用引号界定。还要注意等号两边不能有空格。

我们可以使用 `read` 命令将用户输入赋值变量。它接受一个参数，即要读入的变量名，并等待用户输入文本。当用户按下回车键时，`read` 通常完成。从终端读取变量时，我们通常不使用引号：

```bash
$ read salutation
Wie geht?
$ echo $salutation
Wie geht?
```

## 引号

在继续之前，我们需要明确 shell 的一个特性：引号的使用。

通常情况下，脚本中的参数是通过空白字符分隔的（例如，空格、制表符或换行符）。如果你想让参数包含一个或多个空白字符，你必须对参数加引号。

## Shell 编程

引号内如 `$` 等变量的行为取决于你使用的引号类型。如果你将 `$` 表达式包含在双引号中，它在行执行时会被替换为它的值。如果你将其包含单引号中，则不会发生替换。你也可以通过在前面加上 `\` 来消除 `$` 符号的特殊含义。

## 尝试——变量

这个示例显示了引号对变量输出的影响：

```bash
#!/bin/sh

myvar="Hi there"

echo $myvar
echo "$myvar"
echo '$myvar'
echo \$myvar

echo Enter some text
read myvar

echo '$myvar' now equals $myvar
exit 0
```

给出了输出：

```text
Hi there
Hi there
$myvar
$myvar
Enter some text
Hello World
$myvar now equals Hello World
```

## 工作原理

`myvar` 被创建并赋值字符串 `Hi there`。使用 `echo` 命令显示变量的内容，展示了在变量前加上 `$` 字符如何扩展变量的内容。我们看到双引号不会影响变量的替换，而单引号和反斜杠则是。我们还使用 `read` 命令从用户处获取字符串。

## 环境变量

当 shell 启动时，某些变量根据环境中的值初始化。这些变量通常大写，以区分脚本中用户定义的（shell）变量，后者习惯上小写。创建的变量取决于你的个人配置。许多变量列在手册页中，但主要的列在下表中。

## 第2章

| 环境变量 | 描述 |
| --- | --- |
| `$HOME` | 当前用户的家目录。 |
| `$PATH` | 一个用冒号分隔的目录列表，用于搜索命令。 |
| `$PS1` | 命令提示符，通常为 `$`，但在 `bash` 中你可以使用更复杂的值；例如，字符串 `'\u@h $'` 是一个很流行的默认值，它会告诉用户用户名、机器名和当前目录，并提供一个 `$` 提示符。 |
| `$PS2` | 次级提示符，用于在提示额外输入时使用；通常为 `>`。 |
| `$IFS` | 输入字段分隔符；在 shell 读取输入时用于分隔单词的字符列表，通常是空格、制表符和换行符。 |
| `$0` | shell 脚本的名称。 |
| `$#` | 传递的参数数量。 |
| `$$` | shell 脚本的进程 ID（PID），通常在脚本内部用于生成唯一文件名；例如 `/tmp/tmp-file_$`。 |

> 如果你想查看程序在不同环境下是如何运行的，可以使用 `env <command>`，请尝试查看 `env` 的手册页。此外，我们将在本章后面向你如何使用 `export` 命令在子 shell 中设置环境变量。

## 参数变量

如果调用脚本时带有参数，则会创建一些额外的变量。即使没有传递参数，之前的环境变量 `$#` 仍然存在，但其值为 `0`。

参数变量列在下表中。

| 参数变量 | 描述 |
| --- | --- |
| `$1`, `$2`, ... | 传递给脚本的参数。 |
| `$*` | 所有参数的列表，存储在单个变量中，由环境变量 `IFS` 中的第一个字符分隔。 |
| `$@` | `$*` 的细微变体；它不使用 `IFS` 环境变量，因此如果 `IFS` 为空，参数可能会合并在一起。 |

## Shell 编程

通过尝试运行它们，可以很容易看到 `'$*'` 和 `"$*"` 之间的区别：

```bash
$ IFS=''
$ set foo bar bam
$ echo $$
foo bar bam
$ echo "*"
foobarbam
$ unset IFS
$ echo "*"
foo bar bam
```

如你所示，在双引号内，`$$` 会将位置参数展开为独立的字段，无论 `IFS` 的值是什么。通常情况下，如果你想访问参数，`$@` 是明智的选择。

除了使用 `echo` 命令打印变量内容外，我们还可以使用 `read` 命令读取它们。

## 尝试一下——参数和环境变量

下面的脚本演示了一些简单的变量操作。一旦你输入脚本并将其保存为 `try_var`，请忘记使用 `chmod +x try_var` 使其具有可执行权限。

```bash
#!/bin/sh

salutation="Hello"
echo $salutation
echo "The program $0 is now running"
echo "The second parameter was $2"
echo "The first parameter was $1"
echo "The parameter list was $*"
echo "The user's home directory is $HOME"

echo "Please enter a new greeting"
read salutation

echo $salutation
echo "The script is now complete"
exit 0
```

如果我们运行这个脚本，将得到以下输出：

```bash
$ ./try_var foo bar baz
Hello
The program ./try_var is now running
The second parameter was bar
The first parameter was foo
The parameter list was foo bar baz
The user's home directory is /home/rick
Please enter a new greeting
Sire
Sire
The script is now complete
```

## 第2章

## 工作原理

此脚本创建了变量 `salutation`，显示其内容，然后展示各种变量和环境变量 `$HOME` 如何已经存在并具有适当的值。

我们将在本章的后后部分详细讨论参数替换。

## 条件

所有编程语言的基础都是测试条件并根据这些决策执行不同操作的能力。不过，在讨论此之前，我们将先看可以在 shell 脚本中使用的条件结构，并查看它们所使用的控制结构。

shell 脚本可以测试任何从命令行调用的命令的退出码，包括你编写的脚本。这就是为什么在你编写的任何脚本末尾始终包含退出码是重要的。

## `test` 命令或 `[ ]` 命令

在实践中，大多数脚本都广泛使用 `test` 命令，即 shell 的布尔检查。在大多数系统上，使用 `[ ]` 命令，末尾的 `]` 也用于提高可读性。拥有 `[ ]` 命令似乎可能有点奇怪，但在代码中它让命令的语法看起来简单、整洁，并且更像其他编程语言。

```bash
# ls -1 /usr/bin/
lrwxrwxrwx 1 root 4 Oct 13 10:46 /usr/bin/test -> test
```

> 这些命令在某些旧的 UNIX shell 中调用外部程序，但在更现代的时代它们倾向于是内置的。我们将在稍后的章节查看命令时回到这一点。`test` 命令经常在 shell 脚本之外使用；许多从未写过 shell 脚本的 Linux 用户尝试编写简单的程序并把它们命名为 `test`。如果这样的程序不起作用，它可能与 shell 的 `test` 命令冲突。要确定你的系统是否具有给定名称外部命令，请尝试运行 `test` 来检查执行的是哪个命令，或者使用 `./test` 确保执行的是当前目录下的脚本。

我们将使用最简单的条件之一来介绍 `test` 命令：检查文件是否存在。

```bash
if [ -f /usr/bin/test ];
then
  echo "file exists"
```

（注：由于原文中存在大量重复的段落和代码，已按要求进行翻译并确保不重复输出原文。）

## Shell 编程

## 控制结构

Shell 拥有一组控制结构，再次强调，它们与其他编程语言非常相似。

> 在接下来的章节中，这些语句是在当、当或直到条件满足时要执行的一系列命令。

## if

`if` 语句非常简单：它测试命令的结果，然后根据条件执行一组语句：

```bash
if condition
then
  statements
else
  statements
fi
```

### 尝试一下——使用 if 命令

`if` 的一个常用用途是问一个问题，然后根据答案做出决定：

```bash
#!/bin/sh
echo "Is it morning? Please answer yes or no"
read timeofday

if [ $timeofday = "yes" ]; then
  echo "Good morning"
else
  echo "Good afternoon"
fi

exit 0
```

这将会产生如下输出：

```text
Is it morning? Please answer yes or no

yes

Good morning

$
```

此脚本使用命令来测试变量 `timeofday` 的内容。结果由 `if` 命令评估，允许执行不同的代码行。

> 注意，我们使用额外的空格来缩进 `if` 内部的语句。这只是为了方便人类阅读；shell 会忽略额外的空白字符。

## 第 2 章

## elif

不幸的是，这个简单的脚本存在几个问题。它会接受除 `yes` 以外的任何答案，这意味着否定。我们可以通过使用 `elif` 结构来防止这种情况，它允许我们在执行 `elif` 部分时添加要检查的条件。

### 尝试一下——使用 elif 进行进一步检查

我们可以通过替换内容来修改之前的脚本，以便如果用户输入 `yes` 或 `no` 以外的任何内容，我们就报告错误信息。我们通过将 `else` 替换为 `elif` 并添加另一个条件来实现。

```bash
#!/bin/sh
echo "Is it morning? Answer yes or no"
read timeofday

if [ $timeofday = "yes" ]
then
    echo "Good morning"
elif [ $timeofday = "no" ] ; then
    echo "Good afternoon"
else
    echo "Sorry, $timeofday not recognized. Enter yes or no"
    exit 1
fi

exit 0
```

## 工作原理

与之前的示例非常相似，但现在如果第一个条件不成立，`elif` 命令会再次测试变量。如果两个测试都没有成功，则会打印错误信息并且脚本以值 `1` 退出，调用者可以在调用程序中使用该值来检查脚本是否成功。

## 变量的问题

这修复了最明显的缺陷，但一个更微妙的问题潜伏其中。让我们尝试这个新脚本，但只按回车（或键盘上的 `Return` 键）而不回答问题。我们将得到这个错误信息：

```text
: = unary operator expected
```

哪里出错了？问题出在第一个 `if` 子句中。当变量 `timeofday` 被测试时，它是一个空字符串。所以 `if` 看起来像：

```bash
if [ = "yes" ]
```

这不是一个有效条件。为了避免这种情况，我们必须在变量周围加上引号：

```bash
if [ "$timeofday" = "yes" ]
```

## Shell 编程

空变量将给我们提供一个有效的测试：

```bash
if [ "" = "yes" ]
```

我们新的脚本是：

```bash
#!/bin/sh
echo "Is it morning?? Please answer yes or no"
read timeofday

if [ "$timeofday" = "yes" ]
then
echo "Good morning"
elif [ "$timeofday" = "no" ]; then
echo "Good afternoon"
else
echo "Sorry, $timeofday not recognized. Enter yes or no"
exit 1
fi

exit 0
```
