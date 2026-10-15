
你可以对数组变量应用 `${name}` 运算符，返回数组中的元素数量（不是 bash）。另一个与数组配合运算符是 `${^name}`，其中 `name` 具有数组值（不是 bash）。类似于 `${name}` 会开启 `SH_WORD_SPLIT`，`${^name}` 仅对本次评估开启 `RC_EXPAND_PARAM`。使用两个脱字符 (`^`) 可以将其关闭。当选项 `RC_EXPAND_PARAM` 开启且 `aa` 的值为数组时（不是 bash）。

（注：提供的 OCR 文本在后半部分似乎有重复或损坏的内容。我将根据提供的文本进行清理并保持逻辑流。）

## 可选项（继续）

| 运算符 | 含义 |
| --- | --- |
| == | 等于 |
| != | 不等于 |
| && | 逻辑与 (AND) |
| ^^ | 逻辑异或 (XOR) |
| || | 逻辑或 (OR) |
| ? | 三元运算符 |
| =, -=, +=, *= /=, %%, &=, ^=, |=, <<=, >>==, &&=, ||= | 赋值，逗号运算符 |

递增、后增、减和后减运算符适用于变量。前置运算符出现在变量名之前（如 `++COUNT` 和 `--VALUE`），它们会先改变变量的值（`++` 加1；`--` 减1），然后提供该结果供表达式使用。后置运算符出现在变量名之后（如 `COUNT++` 和 `VALUE--`），它们会先提供变量未变化的原始值供表达式使用，然后再改变变量的值。

```zsh
zsh % ((N=10))
zsh % echo "$N"
10
zsh % echo "$((N-3))"
12
zsh % echo "$N"
9
zsh % echo "$(N++ - 3))"
6
zsh % echo "$N"
10
```

运算符 `&&`、`^&`、`|`、`||`、`^^` 都是短路的。如果使用这些运算符的结果可以通过查看左操作数来判断，那么右操作数将不会被求。

```zsh
zsh % ((N=10))
zsh % ((Z=0))
zsh % echo "$(((N || Z--)))"
1
zsh % echo $Z
0
```

## 可选项（继续）

在这里，N 的值为非零，无论右侧的值是多少，`||`（或）操作的结果都将是1（真），因为 `||=` 永远不会执行，Z 保持其原始值。

像 `+=` 等赋值运算符是简写。例如，`((N+=3))` 等同于 `((N=N+3))`。逗号运算符允许在单个表达式中放置多个操作序列。

```zsh
zsh % ((N=10,Z=0))
zsh % echo "$N and $Z"
10 and 0
```

三元运算符 `?:` 根据第三个表达式返回的值来决定评估两个表达式中的哪一个。

`expression1 ? expression2 : expression3`

如果 `expression1` 产生一个假（0）值，则评估 `expression2`，否则评估 `expression3`。整个表达式的值是 `expression2` 或 `expression3` 的值，取决于哪一个被评估。如果 `expression1` 为真，则不评估 `expression3`。同样，如果 `expression1` 为假，则不评估 `expression2`。

```zsh
zsh % ((N=10,Z=0,COUNT=1))
zsh % ((T=N-COUNT)?+:-Z))
zsh % echo $T
1
zsh % echo $Z
1
```

取模运算符（%`）在第一个操作数被除以第二个操作数时给出余数。

（注：此处提供的原文似乎存在大量乱码或重复错误，如大量无意义的重复 `zsh` 示例代码片段，根据指令要求，已对可逻辑文本进行了翻译，并保留了原始格式。）

## 478 第 13 章：Z Shell 高级 Shell 编程

由于无效的菜单会选择 zsh 为 `var` 赋值一个空字符串以及 `do` 和 `done` 之间的命令，因此在命令中测试空字符串是一个好主意。如果用户在不输入选择的情况下按下回车（RETURN），Z Shell 将重新启动菜单和 PS3 提示符。Z Shell 将用户的响应存储在关键字变量 `REPLY` 中。

如语法所示，你可以省略关键字 `in` 和参数列表。如果这样做，将选择位置参数 `$@` 的当前值。

## repeat

`repeat` 结构结构在其他 shell 中是不可见的。它允许你指定执行命令序列的次数。`repeat` 的语法如下：

```zsh
repeat word
do
  commands
done
```

在这里，`word` 会被展开并作为算术表达式求值。该表达式的值决定了命令重复的次数。

```zsh
zsh % repeat 3; do
  echo "Bye"
  done
Bye
Bye
Bye
zsh % read number
  3
zsh % repeat $number; do
  echo "Bye"
  done
Bye
Bye
Bye
```

## 控制结构的备用语法

与其他 shell 不同，Z Shell 为许多命令提供了几种不同的语法，通常是为了提供类似于 `tcsh` 的形式。符合 `tcsh` 语法的控制结构如下。

`for` 结构具有以下备用语法：

```
foreach name ( word ... )
  commands
end
```

如果你设置了 `CSH_JUNKIE_PAREN` 选项，也允许以下语法：

```
for name (word ... ) {
  commands
}
```

## 内内置 479

当设置 `CSH_JUNKIE_PAREN` 时，你可以这样写 `if` 结构：

```
if ( command ) {
  commands
} elif ( command ) {
  commands
} ... else {
  commands
}
```

当命令的形式为 `|| expression || expression ||` 时，可以省略括号。结构中的 `elif` 部分以及 `else` 部分也可以省略。

`while` 结构可以写成：

```
while ( command ) {
  commands
}
```

## 选项处理

Linux 工具解释其命令行的方式取决于特定的工具。然而，存在大多数 Linux 工具遵循的惯例。请参阅第 91 页的“命令行”。特别是，任何选项工具都由连字符开头的字母来标识。

```zsh
zsh % ls -l -r
```

（关于 `ls` 这些参数的描述请参见第 777 和 779 页。）选项通常必须位于文件名之前。大多数工具允许你在单个连字符后面组合选项。上一个命令也可以写为：

```zsh
zsh % ls -lrt
```

某些工具的选项本身需要参数。`cc` 工具有一个 `-o` 选项，后面必须跟随可执行文件的文件名。（参阅第 747 页的 `gcc`。）通常，选项的参数与其选项之间通过空格分隔。

```zsh
zsh % cc -o prog prog.c
```

另一个惯例允许工具处理以连字符开头的文件名。如果你有一个文件名恰好是 `-l`，那么以下命令就是歧义的：

```zsh
zsh % ls -l
```

它可能表示当前工作目录下所有文件的列出，也可能是名为 `-l` 的文件的列出。它被解释为前者。避免创建以连字符开头的文件，但如果你确实创建了它们，许多

## 480 第 13 章：Z Shell 高级 Shell 编程

Linux 工具遵循以下惯例：参数 `--`（两个连续连字符）表示选项的结束。你可以输入：

```zsh
zsh % 1s --1
```

或者

```zsh
zsh % 1s ./1
```

来消除命令歧义。

这些是惯例而非硬规则，有很多 Linux 工具并不遵循它们（例如 `find`），但遵循这些惯例是一个好主意；它让用户更容易学习使用你的程序。当你编写需要选项的 shell 程序时，请遵循 Linux 选项惯例。

## getopts 内置

Z Shell 的内置命令 `getopts` 设计用于方便编写遵循参数惯例的程序。`getopts` 的语法为：

```
getopts optstring varname [arg ...]
```

`optstring` 是有效选项字母的列表。如果选项需要参数，你通过在相应的字母后面指示这一点。选项字符串 `ox:lttr` 表示 `getopts` 应该搜索 `-d`, `-x`, `-o`, `-l`, `-t`, `-r` 选项，并且 `-o` 和 `-t` 选项需要参数。

`getopts` 内置检查参数列表中是否存在 `optstring` 中的选项。它将找到的字母存储在 `varname` 中。默认情况下，`getopts` 使用命令行。如果你在 `varname` 之后提供参数列表 (`arg`)，则使用它们。

`getopts` 使用 `OPTIND` 和 `OPTARG` 变量来存储选项相关的值。当 Z Shell 程序启动时，`OPTIND` 的值为 1。每当 `getopts` 定位一个参数时，它就会增加 `OPTIND` 为下一个要处理参数的索引。如果选项需要参数，`zsh` 将参数赋值赋予 `OPTARG`。

考虑以下问题：你必须编写一个可以接受三个选项的程序。

- `-b` 标志表示你的程序应该忽略
- `-t` 标志表示你的程序应该测试
- `-o` 标志表示你的程序应该输出

以下代码使用 `getopts` 来处理这些选项：

## 内置命令 483

Z Shell 允许你通过 `varname?prompt` 语法为第一个输入变量名指定输入提示。例如，如果你的脚本中有某行如下形式的代码：

```bash
read MON?"Enter month, day and year separated by spaces: " DAY Y
```

那么执行此命令将导致脚本发出提示信息：

Enter month, day and year separated by spaces:

并等待你输入一行。如果你输入了三个值，它们将分别赋值给 MON、DAY 和 Y。问号 (?) 会被转义，以防止 Z Shell 将其作为文件名模式匹配操作符。

`read` 内置命令支持其他选项。以下列表描述了其中一些最常用的选项：

- -p: 命令 `read -p...` 从协进程（coprocess）的标准输出中读取输入行。请参阅“I/O 重定向与协进程”（第 508 页）。
- -r: 原始输入。通常情况下，如果输入行以反斜杠字符 (\)结尾，反斜杠及其随后的换行将被丢弃，下一行被视为同一行输入的延续。此选项允许将末尾的反斜杠视为普通字符。一个应用是读取一个本身包含你想处理的反斜杠的 shell 脚本输入文件。
- -query: 读取一个字符并返回。如果用户输入 y 或 Y，则 `read sets varname` 被设置为 n。如果用户输入 y 或 Y，`read` 内置命令返回值为 0。这更容易提示用户进行简单的“是/否”回答，如下：
```zsh
if read -q ANSWER?"Do you want to play a game (y/n)?"
then
fi
```
一旦用户输入单个字符，`read` 就会返回——无需按回车。
- -E echo: 使 `read` 内置命令在用户按下回车后显示其输入的单词。
- -e echo: `read` 内置命令在用户按下回车后显示其输入的单词，但不会将其赋值给参数列表中指定的变量。
- -A: 根据 IFS 将输入拆分为单词，并作为数组赋值给参数列表中的第一个变量。
- -u: 使用整数 n 作为文件描述符，`read` 从其获取输入。

```bash
read -u4 arg1 arg2
```

等同于

```bash
read arg1 arg2 <&4
```

关于重定向和文件描述符的讨论，请参阅“文件描述符”（第 487 页）。

`read` 内置命令在成功读取任何数据时退出状态为 0。当到达文件结束符（EOF）时，退出状态为非零。

```zsh
zsh % cat names
Alice Jones
Robert Smith
Alice Paulson
John Q. Public
zsh % while read First Rest
> do
  print $Rest, $First
> done < names
Jones, Alice
Smith, Robert
Paulson, Alice
Q. Public, John
```

## 可选内容

复合 `while` 结构中重定向符号 (<) 的位置至关重要。重要的是，你只能将重定向符号放在 `done` 语句处，而不是 `read` 的调用处。每次你重定向它，shell 都会打开文件并将 `read` 定置于文件的开头。

```zsh
zsh % read line1 < (print $line1); read line2 < (print $line2)
Alice Jones
Alice Jones
zsh % (read line1; print $line1; read line2; print $line2) < names
Alice Jones
Robert Smith
```

在第一个示例中，`read` 在 names 文件的开头打开了 names。在第二个示例中，names 作为由圆括号创建的子 shell 标准输入被打开一次。每个 `read` 读取标准输入的连续行。

获得相同效果的另一种方法是使用 `exec` 打开文件并保持开启，如下所示。（参阅第 487 页的“文件描述符”）。

```zsh
zsh % exec 3< names
zsh % read -u3 line1; print $line1; read -u3 line2; print $line2
Alice Jones
Robert Smith
zsh % exec 3<&-
```

## 内置命令 485

## print 内置命令

**print** 内置命令是 **echo** 的替代方案，语法如下：

```bash
print [-cDilnNoOpPrRs] [-un] [string...]
```

默认情况下，*print* 将字符串写入标准输出，并识别两种抑制末尾换行符语法（字符串末尾的 \c 和 -n 选项）。

| 转义字符 | 含义 |
| :--- | :--- |
| \a | 警报字符（通常使显示器响铃或闪烁） |
| \b | 退格字符 |
| \c | 不打印，并抑制末尾换行符 |
| \e | ESC 字符 |
| \f | 换页——在输出流中放入一个 CONTROL-L 字符 |
| \n | 换行符——允许一次 print 调用写入多行 |
| \r | 回车符——在输出流中放入一个 CONTROL-M 字符 |
| \t | 制表符字符 |
| \v | 垂直制表符字符 |
| \\ | 反斜杠字符 |
| \nnn | 八进制值为 nnn 的 ASCII 字符——你可以省略前导零 |
| \nnnn | 十六进制值为 nnn 的 ASCII 字符 |

记住，反斜杠 (\) 是 shell 的特殊字符，在任何 print 转义序列中，你都必须对其加引号或对其进行转义。这里有一个 print 转义的示例：

```zsh
zsh % print "backslash: \\"
backslash: \
zsh % print "tab: \t"
tab:	
zsh % print "newline: \nline"
newline
line
```

记住，反斜杠 (\) 是 shell 的特殊字符，在任何 print 转义序列中，你都必须对其加引号或对其进行转义。这里有一个 print 转义的示例：

（注：此处原文似乎重复，已按要求处理翻译）

- -p: 命令 `read -p...` 从协进程的标准输出中读取输入行。请参阅“I/O 重定向与协进程”（508）。
- -r: 原始输入。通常情况下，如果输入行以反斜杠字符 (\)结尾，反斜杠及其随后的换行将被丢弃，下一行被视为同一行输入的延续。此选项允许将末尾的反斜杠视为普通字符。一个应用是读取一个本身包含你想处理的反斜杠的 shell 脚本输入文件。
- -query: 读取一个字符并返回。如果用户输入 y 或 Y，则 `read sets varname` 被设置为 n。如果用户输入 y 或 Y， `read` 内置命令返回值为 0。这更容易提示用户进行简单的“是/否”回答，如下：
```zsh
if read -q ANSWER?"Do you want to play a game (y/n)?"
then
fi
```
一旦用户输入单个字符，`read` 就会返回——无需按回车。
- -E echo: 使 `read` 内置命令在用户按下回车后显示其输入的单词。
- -e echo: `read` 内置命令在用户按下回车后显示其输入的单词，但不会将其赋值给参数列表中指定的变量。
- -A: 根据 IFS 将输入拆分为单词，并作为数组赋值给参数列表中的第一个变量。
- -u: 使用整数 n 作为文件描述符，`read` 从其获取输入。

```bash
read -u4 arg1 arg2
```

等同于

```bash
read arg1 arg2 <&4
```

关于重定向和文件描述符的讨论，请参阅“文件描述符”（第 487 页）。

`read` 内置命令在成功读取任何数据时退出状态为 0。当到达文件结束符（EOF）时，退出状态为非零。

```zsh
zsh % cat names
Alice Jones
Robert Smith
Alice Paulson
John Q. Public
zsh % while read First Rest
> do
  print $Rest, $First
```
