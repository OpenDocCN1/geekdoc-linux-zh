
如果你想给一个变量分配多个单词，你需要对分隔单词的空格加引号。你可以认为这是创建一个要分配给变量的字符串。当然，双引号内的任何其他元字符也会被加引号。在接下来的示例中，双引号包裹了由空格分隔的单词。由于空格被包含在双引号内，它们被视为字符，而不是用于解析命令行参数的分隔符。在第二个示例中，双引号还包含了一个点，将其仅视为一个字符。在第三个示例中，星号也被包含在双引号内。星号被视为字符串中的另一个字符，不会不会求值。

```bash
$ notice="The meeting will be tomorrow"
$ echo $notice
The meeting will be tomorrow
```

```bash
$ message="The project is on time."
$ echo $message
The project is on time.
```

```bash
$ notice="You can get a list of files with ls *.c"
$ echo $notice
You can get a list of files with ls *.c
```

然而，双引号并不对求值变量的运算符 `$` 加引号。双引号内的 `$` 运算符名仍会被求值，将变量名替换为它的值。变量的值将成为字符串的一部分，而不是变量名。有时你可能希望引号内的变量被求值。在下一个示例中，使用了双引号以便包含获胜者的名字。

# 第 4 章：Shell 脚本与编程 69

```bash
$ winner=dylan
$ notice="The person won is $winner"
$ echo $notice
The person won is dylan
```

另一方面，有时你不希望引号内的变量被求值。在这种情况下，你必须使用单引号。单引号会抑制变量求值并将美元符号视为另一个字符。在下一个示例中，单引号阻止了对 `winner` 变量的求值。

```bash
$ winner=dylan
$ result='The name is in $winner variable'
$ echo $result
The name is in $winner variable
```

如果在这种情况下使用了双引号，就会发生意料之外的变量求值。在下一个示例中，字符 "winner" 被解释为变量。

```bash
$ winner=dylan
$ result="The name is in $winner variable"
$ echo $result
The name is in the dylan variable
```

你始终可以在元字符前面加上反斜杠来对它加引号（包括 `$` 运算符）。反斜杠的作用是引用换行。当你想在字符串内求值变量的同时包含 `$` 字符时，反斜杠非常有用。在下一个示例中，在 `$` 之前放置反斜杠将其视为美元符号字符。与此同时，由于使用了双引号，变量 `winner` 被求值。

```bash
$ winner=dylan
$ result="$winner \100.00"
$ echo $result
dylan won $100.00
```

## 命令引用：单引号

有时你可能对 Linux 命令使用单引号。如果你这样做，可以将编写的命令分配给 Linux 命令的另一个名称。在命令行上输入变量名并加上 `$` 运算符将执行该命令。在下一个示例中，一个 shell 变量被赋予组成列表命令的字符 `'ls -F'`。单引号包裹了命令。当 shell 变量在命令行上求值时，它包含的内容将成为命令行参数，并由 shell 执行。

```bash
$ lsf='ls -F'
$ lsf
mydata /reports /letters
$
```

实际上，你正在为命令创建另一个名称，类似于一个别名（alias）。

# 第二部分：Linux Shell 与文件结构

## 来自 Linux 命令的值：反引号（Back Quotes）

尽管你可以通过输入字符或字符串来创建变量值，但也可以从其他 Linux 命令获取值。要将 Linux 命令的结果赋值给变量，你首先需要执行该命令。如果你在命令行中将 Linux 命令置于反引号中，该命令将首先执行，其结果将成为命令行上的一个参数。在赋值的情况下，可以通过将命令置于反引号中并执行它，从而将其结果赋值给变量。反引号可以被认为是一个由待执行命令组成的表达式，其结果随后被赋值给变量。构成命令本身的字符不会被赋值。在下一个示例中，命令 `ls *.c` 被执行，其结果被赋值给变量。`ls *.c` 生成了所有 .c 扩展的文件列表。然后，这个文件列表被赋值给 `ls` 变量。

```bash
$ `ls *.c`
$ echo $ls
main.c prog.c lib.c
```

你需要记住单引号和反引号的区别。单引号将 Linux 命令视为一组字符。反引号则强制执行 Linux 命令。有时你可能在想用反引号时误输入了单引号。在接第一个示例中，变量的赋值在 `ls *.c` 命令周围使用的是单引号而不是反引号。在这种情况下，`ls *.c` 只是要赋值给变量 `ls *.c` 的字符。在第二个示例中，`ls *.c` 命令周围放置了反引号，强制对命令进行求值。生成了以 .c 结尾的文件列表，并将其赋值为 lscc 的值。

```bash
$ lscc='ls *.c'
$ echo $lscc
ls *.c
```

```bash
$ lscc=`ls *.c`
$ echo $lscc
main.c prog.c
```

## Shell 脚本：用户自定义命令

你可以将 shell 命令放在文件中，然后让 shell 读取并执行文件中的命令。从这个意义上说，文件充当了 shell 程序，像执行程序中的语句一样执行 shell 命令。包含 shell 命令的文件被称为 shell 脚本。

你使用 Vi 编辑器等标准文本编辑器向脚本文件输入命令。配合脚本文件名使用的 `sh` 或 `command` 将读取脚本文件并执行其中的命令。在下一个示例中，名为 `ls` 的文件包含一个 `ls` 命令，仅显示扩展名为 .c 的文件。

```bash
ls
ls *.c
```

# 第 4 章：Shell 脚本与编程

这里显示了 lsc 脚本的运行：

```bash
$ lsc
main.c calc.c
$ .lsc
main.c calc.c
```

## 执行脚本

通过设置脚本文件的执行权限，你可以省略 `sh` 和 `.` 命令。当你的文本编辑器首次创建脚本文件时，它只具有读写权限。带有 `+x` 选项的 `chmod` 命令将赋予脚本执行权限。一旦执行，在 shell 提示符处输入脚本文件名并回车即可执行该脚本及其内部 shell 命令。实际上，脚本文件名变成了一个新命令。通过这种方式，你可以使用脚本设计并创建你自己的命令。你只需要设置一次权限。在下一个示例中，所有者的 lsc 脚本执行权限被开启。lsc 脚本像任何 Linux 命令一样直接执行。

```bash
$ chmod +x lsc
$ lsc
main.c calc.c
```

你可能需要指定正在使用的脚本位于当前工作目录。你通过在脚本名称前加上点和斜杠组合 `./` 来实现这一点，例如 `./lsc`。点是表示当前工作目录名称的特殊字符。斜杠是目录名分隔符。下面的示例显示了如何执行 lsc 脚本。

```bash
$ ./lsc
main.c calc.c
```

## 脚本参数

正如任何 Linux 命令都可以接收参数一样，shell 脚本也可以。命令行上的参数从 1 开始顺序引用。参数使用 `$` 操作符和其位置进行引用。第一个参数用 `$1` 引用，第二个用 `$2` 引用，以此此类推。在下一个示例中，ls 脚本打印出扩展名为 .c 的文件。

```bash
ls *.c
```

## 74 第二部分：Linux Shell 与文件结构

displast

lastname="Dickens"

```bash
echo "Last name is $lastname"
echo "$firstname $lastname",
```

`dispfirst` 脚本的运行如下：

```bash
$ dispfirst
First name is Charles
Last name is Dickens
Dickens
eh: firstname: not found
$
```

```bash
dispfile
myfile="List"
```

```bash
echo "Displaying $myfile"
pr -t -n $myfile
```

```bash
printfile
printfile
```

```bash
myfile="List"
```

```bash
echo "Printing $myfile"
lp $myfile &
```

`dispfile` 脚本的运行如下：

```bash
$ dispfile
Displaying List
1 screen
2 modem
3 paper
Printing List
$
```
