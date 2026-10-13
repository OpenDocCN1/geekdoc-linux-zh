
> 计算机上乘法的常用运算符是星号 (`*`)。请记住在命令行提示符下，这一个用于执行文件名扩展的字符。因为你想为 `expr` 提供数学运算符而不是匹配文件名列表，请始终记住在使用 `expr` 时将星号括在引号中：
```
[you@workstation20]$ expr '*' * 36
108
[you@workstation20]$
```

![](img/92a94ba94656919835b7a50a27c9d9ba_223_0.png)

计算机中的每个数字和运算符都是独立的参数，务必区分数字和运算符。

# 使用 head 和 tail 显示文本开头或结尾

有时只显示文件的开头或结尾行是有用的。`head` 和 `tail` 命令用于此目的。`head` 显示文件的前几行，而 `tail` 显示后几行。

```
[you@workstation20]$ head -n 5 filename
line 1
line 2
line 3
line 4
line 5
[you@workstation20]$ tail -n 5 filename
line 96
line 97
line 98
line 99
line 100
```

你也可以使用 `head` 和 `tail` 显示范围内的行。例如：

```
[you@workstation20]$ head -n +10 filename
line 10
line 11
line 12
...
[you@workstation20]$ tail -n -10 filename
line 91
line 92
line 93
... 100
```

# 使用 sed 编辑数据流

有时能够编辑数据流也是用的。`sed` 命令是一个搜索和转换文本的强大工具。最常用的命令是 `s`（替换）命令。

```
sed 's/search/replacement/'
```

`s` 命令替换第一个匹配项。要替换所有匹配项，请使用 `g`（全局）标志：

```
sed 's/search/replacement/g/'
```

你还可以使用 `sed` 删除匹配模式的行：

```
sed '/pattern/d'
```

`sed` 是一个多功能工具，可用于许多不同的文本处理任务。它值得学习。

## 利用 Shell 的威力

在上一条命令中，使用了两个命令——数据通过管道传递给 `sed`，以便将第一个命令（分号之前）中的数字 2 更改为数字 5；并将第二个命令（分号之后）中的数字 4 更改为 7。

为了举一个更符合现实的例子，请考虑大多数人所说的“搜索并替换”功能。假设你用 LaTeX 编写了一部长小说，并将主角命名为 Evan——现在你想把他的名字改为 Sebastian。你不需要将 LaTeX 文件加载到文本编辑器并使用搜索替换功能，只需简单地使用 `sed` 和输出重定向即可：

```
@workstation20$ sed 's/Evan/Sebastian/g' MyNovel.tex > MyNovel.tex
@workstation20$ you
```

就这样，你创建了小说的新副本 `MyNovel.tex`，其中主角的名字显示为 Sebastian——不需要任何额外工作。

![](img/92a94ba94656919835b7a50a27c9d9ba_225_0.png)

> 你可以在 `sed` 命令中使用美元符号 (`$`) 和脱字符符号 (`'`) 分别匹配行的末尾或开头。例如，为了在 `goodbye` 出现在行尾时将其替换为 `farewell`，请使用以下 `sed` 命令：
```
s/goodbye$/farewell/
```
> 同样，只有当在行开头时将文本 `Hello` 替换为 `Greetings`，请使用以下 `sed` 命令：
```
s/Hello/Greetings/
```

![](img/92a94ba94656919835b7a50a27c9d9ba_225_1.png)

> `sed` 命令是 Unix 世界的基石，因为它比这里演示的几个例子要强大得多。当使用其模式匹配能力时，`sed` 特别强大。

想要了解更多关于 `sed` 的知识，请抽空学习 `sed` 帮助页；在你经常使用 Shell 时，它可能会对你有帮助。

## 使用 Shell 变量和引号

在开始创建脚本之前，让我们来看两个随着你处理的任务日益复杂而变得变得越来越重要的概念。这两个概念是 Shell 变量（以及变量替换）和引用。

变量是特殊的单词，当它们被展开时，会被替换为你分配给它们的值。Shell 提供了一个内置过程来创建和跟踪变量，称为变量替换。变量替换允许你对 Shell 脚本中使用的命令进行泛化，使你能够通过更改脚本所用变量的值，来改变脚本的行为（例如它将影响的文件）。

在 Shell 脚本中使用变量涉及三个基本步骤：

- 1. 创建变量，通常只是简单地使用等号给单词赋一个值。通常，这还涉及使用引号括起赋值的值，以确保 Shell 不会对其产生误解。
- 2. 在脚本的后后部分，告诉 Shell 你希望变量的值在出现的任何地方被精确替换。这是通过在变量名前前加上美元符号 (`$`) 实现的。
- 3. （在其他文本中展开变量时）将变量名括在大括号 (`{}`) 中，以向 Shell 明确你正尝试展开的变量名称。

例如，使用变量，你可以编写一个对文件执行特定 `set` 操作的脚本，而不需要在脚本中显式命名文件——从而允许用户在每次运行脚本时指定要影响的文件。

### 创建和替换变量

为了理解如何创建变量，假设一下在日常工作中，你经常遇到人们路过你的桌子请求打印这些文档——`newmpl.txt`、`hours.txt` 和 `phonebook.txt`——它们都存储在 `/home/you/textfiles` 中。你熟悉的从任何工作目录打印这些文件的命令是

```
$@workstation20$ cp /home/you/textfiles/newmpl.txt /home/you/textfiles/hours.txt /home/you/textfiles/phonebook.txt
```

```
$@workstation20$
```

减少输入量的方法是使用变量。你可以创建一个变量来存储你需要重复打印的文件名和路径，省去输入所有名称和路径信息的麻烦：

```
[@workstation20 you]$ PRINTFILES="/home/you/textfiles/newmpl.txt /home/you/textfiles/hours.txt /home/you/textfiles/phonebook.txt"
[@workstation20 you]$
```

你创建了一个名为 `PRINTFILES` 的变量，它包含了你经常需要打印的文件列表。在命令行中使用该变量，替换文件名和路径名。从以后，每当你在此会话中打印这三个文件时，只需输入

```
[@workstation20 you]$ cp $PRINTFILES
[@workstation20 you]$
```

这条命令要短得多！它是如何工作的？Shell 用变量 `PRINTFILES` 的内容替换了单词 `PRINTFILES`。为了通过一个清晰可见的命令看到这种效果，请尝试使用 `echo` 命令显示 `PRINTFILES` 的值：

```
[@workstation20 you]$ echo $PRINTFILES
[@workstation20 you]$
```

因为 Shell 将单词 `PRINTFILES` 替换为变量 `PRINTFILES` 的内容，`/home/you/textfiles/newmpl.txt /home/you/textfiles/hours.txt /home/you/textfiles/phonebook.txt`，输出显示了这些文件名。

> 你可以在 `sed` 命令中使用美元符号 (`$`) 和脱字符符号 (`'`) 分别匹配行的末尾或开头。例如，为了在 `goodbye` 出现在行尾时将其替换为 `farewell`，请使用以下 `sed` 命令：
```
s/goodbye$/farewell/
```
> 同样，只有在在行开头时将文本 `Hello` 替换为 `Greetings`，请使用以下 `sed` 命令：
```
s/Hello/Greetings/
```
> `sed` 命令是 Unix 世界的基石，因为它比这里演示的几个例子要强大得多。当使用其模式匹配能力时，`sed` 特别强大。

## 小心使用引用

当你创建变量时，最好将要赋值的值括在引号中。这告诉 Shell 你想要赋值的是引号内的精确值，而不是展开模式或其他变量。有几种类型的引用可以在命令行完成；变量可以采用其中任何一种：

```
VARIABLE=value
VARIABLE='value'
VARIABLE=' value'
```

这些方法都有细微的区别。第一种（无引用）最简单。然而，因为 Shell 通常以特殊方式使用许多字符，例如使用空格分隔参数或使用竖线 (`|`) 创建管道，如果你想将这些字符赋值给变量，引用是必要的：
