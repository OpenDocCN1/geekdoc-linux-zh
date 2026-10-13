
```bash
@user:~$ echo "Hello, world!"
Hello, world!
```

你也可以用 `echo` 打印变量的值：

```bash
@user:~$ NAME=Linux
@user:~$ echo Hello, $NAME
Hello, Linux
```

## 使用 `expr` 执行简单计算

`expr` 命令提供了从命令行评估算术表达式的方法。它只能执行整数运算。以下是执行基础计算的示例：

```bash
@user:~$ expr 5 + 2
7
@user:~$ expr 5 - 2
3
@user:~$ expr 5 * 2
10
@user:~$ expr 5 / 2
2
```

### 使用星号时要小心

在使用星号（`*`）时，记住它是 shell 中的通配符。为了将其用于乘法，必须始终将其包含在引号中：

```bash
@user:~$ expr 5 \* 2
10
```

## 使用 `sed` 编辑数据流

有时你可能想在输出数据之前对它们进行实时编辑。你执行此操作的命令是流编辑器（`sed`），它是 Unix 世界中最常用的命令之一。

使用 `sed` 的常用方法是让它通过管道（竖线，`|`）接受数据流，并提供一个参数来确定如何更改数据。虽然有很多 `sed` 命令，但本章只涵盖了其中一个最常用的命令。它是 `s`（替换）命令，以两种方式之一工作：

```bash
sed 's/search/replace/'
sed 's/search/replace/g'
```

在两种情况下，`search` 是要搜索的文本字符串，而 `replace` 是替换它的文本。如果你在参数末尾添加 `g`，则行中的所有匹配项都会被替换。

## 第 25 章：利用 Shell 的力量

搜索引用将被替换为替换中的文本；如果不使用 `g`，则只替换每行的第一个出现处。注意，如有必要，任何字符都可以作为斜杠（`/`）这允许你在需要时在搜索或替换字符串中使用斜杠。注意，你还可以通过在引号内部用分号分隔为 `sed` 提供多个命令。

以下是 `sed` 与 `head` 结合使用的示例，`head` 通过管道向 `sed` 提供输入：

```bash
[you@workstation20 you]$ head -4 myfile.txt ; sed 's/file/jolly file/'
This is 1 in a jolly file called myfile.txt that is 16 lines long.
This is 2 in a jolly file called myfile.txt that is 16 lines long.
This is 3 in a jolly file called myfile.txt that is 16 lines long.
This is 4 in a jolly file called myfile.txt that is 16 lines long.
[you@workstation20 you]$ head -4 myfile.txt ; sed 's/file/silly/g'
This is 1 in a silly file called silly myfile.txt that is 16 lines long.
This is 2 in a silly file called silly myfile.txt that is 16 lines long.
This is 3 in a silly file called silly myfile.txt that is 16 lines long.
This is 4 in a silly file called silly myfile.txt that is 16 lines long.
[you@workstation20 you]$ head -4 myfile.txt ; sed 's/2/e 5/s; e 4/7/'
This is 1 in a file called myfile.txt that is 16 lines long.
This is 2/3 in a file called myfile.txt that is 16 lines long.
This is 3 in a file called myfile.txt that is 16 lines long.
This is 4 in a file called myfile.txt that is 16 lines long.
[you@workstation20 you]$ sed $
```

在最后一个示例中，使用了两个命令：数据被管道传输到 `sed`，在第一个命令（分号之前）将数字 2 更改为数字 5，在第二个命令（分号之后）将数字 4 更改为数字 7。

为了一个更实际的例子，考虑大多数人所说的“搜索并替换”功能。假设你必须用 LaTeX 写小说，其中你将主角命名为 Evan——而现在你想把他的名字改为 Sebastian。与其将长 LaTeX 文件加载到编辑器并使用搜索替换功能，你只需简单地使用 `sed` 和输出重定向：

```bash
[you@workstation20 you]$ sed 's/Evan/Sebastian/g' MyNovel.txt > MyNovel.txt
[you@workstation20 you]$
```

就这样这样，你创建了小说的一个新副本 `MyNovel.txt`，其中主角的名字显示为 Sebastian——不需要任何额外工作。

## 匹配行的开头或结尾

你可以在 `sed` 命令中使用美元符号（`$`）和脱字符（`^`）分别匹配行尾或行首。例如，仅当 `goodbye` 现在行尾时将文本 `goodbye` 替换为 `farewell`，使用以下 `sed` 命令：

```bash
/s/goodbye$/farewell/
```

同样，仅当 `Hello` 现在行首时将文本 `Hello` 替换为 `Greetings`，使用以下 `sed` 命令：

```bash
/s/^Hello/Greetings/
```

`sed` 命令是 Unix 世界的基石，因为它比这里演示的几个示例要强大得多。当 `sed` 使用其模式匹配能力时，它特别强大。

要了解更多关于 `sed` 的信息，请花时间空闲学习 `sed` 手册页；在你经常使用 shell 时，它可能会对你有帮助。

## 使用 Shell 变量和引号

在开始创建之前，让我们看看在处理手头任务复杂性时变得越来越重要的两个概念。这些概念是 shell 变量（以及变量替换）和引号。变量是特殊的单词，在展开时，会被赋值给它们的值替换。shell 提供了一个内置过程来创建和跟踪变量，称为变量替换。变量替换允许你泛化这些命令。

### 使用替换时要具体

当变量名具有歧义时，你也可以将变量名括在大括号（`{}`）中，以指示变量的开始和结束。

例如，假设你想使用数字 2000 之前的 own。shell 可能会误认为你指的是一个名为 `WORD000` 的变量：

```bash
[@workstation20 you]$ WORD=YEAR
[@workstation20 you]$ echo ${WORD}2000
YEAR2000
[@workstation20 you]$
```

通过将你的变量名 `WORD` 括在大括号中，你向 shell 显示哪个变量应该是展开的——你创建的变量，而不是你没有创建的 `WORD000`。

### 小心引号

当你创建变量时，通常建议将要赋值的值用引号起来。它们告诉 shell 你赋值的是引号内部的值，而不是展开模式或其他变量，或者将空格分隔的值视为参数或命令。多种类型的引号可以在命令行完成，可以使用任何一种来创建或赋值：

```bash
VARIABLE=value
```

```bash
VARIABLE='value'
```

这些命令中的每一个都微妙地不同。第一种（无引号）是最简单的，因为 shell 通常以特殊方式使用字符，例如使用空格分隔参数或使用竖线（`|`）创建管道，如果你想将这些字符赋值给变量，引号是必要的：

```bash
[@workstation20 you]$ MYNAME=Horace Walpole
bash: Walpole: command not found
[@workstation20 you]$ MYNAME="Horace Walpole"
[@workstation20 you]$
```

在这种情况下，需要引号来防止 shell 使用空格作为分隔符。在赋值给变量时，必须用引号括的其他字符还有括号（`()`）、大括号（`{}`）和中括号（`[]`）。单引号包裹数据的结果之间也存在差异。

# 第 25 章：利用 Shell 的力量

这是用双引号包含数据的结果。在双引号中，虽然大多数特殊字符会被忽略，但命令替换和变量替换仍然会执行；而在单引号中，则不会执行。这种区别非常细微，通过示例来解释可能最为合适。请考虑以下序列：
