
假设你有一个存储在变量 `filename` 中的文件名。如果你想重命名文件，使得新名称与旧名称相同，但在末尾添加一个 X，你的第一反应可能是输入

```
$filename $filenameX
```

当 shell 扫描这条命令行时，它会同时替换变量 `filename` 的值以及变量 `filenameX` 的值。shell 认为 `filenameX` 是该变量的完整名称，因为它完全由有效的名称字符组成。为了避免这个问题，你可以通过将整个名称（但不包括领先的美元符号）括在大括号中来界定变量的结束，例如：

```
${filename}
```

这消除了歧义，`mv` 命令随后按如下方式工作：

```
mv $filename $filenameX
```

记住，只有当变量名的最后一个字符后面跟着字母、数字或下划线时，大括号才是必要的。

## 内置整数算术

POSIX 标准 shell 提供了一种对 shell 变量进行整数算术的机制，称为算术扩展。注意，一些旧版本的 shell 不支持此功能。

算术扩展的格式为

```
$((expression))
```

其中 `expression` 是使用变量和运算符的算术表达式。有效的变量是那些包含数值的变量（允许有前后空格）。有效的运算符取自 C 语言，并列在附录 A“Shell 总结”中。计算 `expression` 的结果会被替换到命令行中。例如，

```
echo $((i))
```

将 shell 变量 `i` 加 1 并打印结果。注意，变量前面不需要有美元符号。因为 shell 知道在算术扩展中出现的唯一有效项是运算符、数字和变量。如果变量未定义或包含 NULL 字符串，则其值被假设为 0。因此，如果我们没有给变量赋值任何值，我们仍然可以在整数表达式中使用它：

```
$ echo a               变量 a 未设置
$ echo $((a = a + 1))   等同于 a = 0 + 1
$ echo a               现在包含 1
```

注意，赋值是一个有效的运算符，并且在上述示例的第二个 `echo` 命令中执行了赋值替换。

表达式内部可以自由使用圆括号来强制分组，例如：

```
echo $((i = (10) * 3))
```

如果你想在不使用 `echo` 或其他命令的情况下执行赋值，你可以将赋值移动到算术扩展之前。

要将变量 `i` 乘以 5并将结果赋值回 `i`，你可以写

```
i=$((i * 5))
```

注意，双括号内的空格是可选的，但赋值在外部时是不允许空格的。

最后，为了测试 `i` 是否大于 0 或小于等于 100，你可以写

```
result=$((i > 0 && i <= 100))
```

如果表达式为真，则给 `result` 赋值 1；如果为假，则赋值 0：

```
$ i=$((i > 0 && i <= 100))
$ echo $i
0
```

这就是我们对编写命令和使用变量的介绍。下一章将详细介绍 shell 中的引用机制。

## 练习

- 1：以下哪些是有效的变量名？

```
1235
HOMEDIR
file.name
file_name
limit
```

- 2：假设你的 HOME 目录是 `/users/steve`，并且你拥有如下所示的子目录：

（图像描述）

假设你刚刚登录系统并执行了以下命令：

```
$ mkdir /users/steve/documents
$ cd ~/docs/letters
$ cp ~/docs/proposals
```

编写命令来完成以下操作：

- a. 列出 `documents` 目录的内容。
- b. 将 `letters` 目录中的所有文件复制到 `proposals` 目录。
- c. 将 `letters` 目录中所有名称包含大写字母的文件移动到当前目录。
- d. 统计 `memos` 目录中的文件数量。

以下命令会产生什么影响？

- a. `ls $let/..`
- b. `cat $prop/sys.A >> $let/no.JSK`
- c. `echo $let/*`
- d. `cp $let/no.JSK $progs`
- e. `cd $prop`

- 3：编写一个名为 `nf` 的程序，显示当前目录下的文件数量。输入该程序并测试。

- 4：编写一个名为 `whos` 的程序，显示登录用户的排序后的列表。仅显示用户名，不显示其他信息。输入该程序并测试。

## 第 6 章，我能引用这句话吗？

本章内容

- 单引号
- 双引号
- 反斜符
- 命令替换
- 练习题

本章将向你介绍 shell 脚本编程语言的一个独特特性：它解释引号字符的方式。基本上，shell 识别四种不同类型的引号字符：

- 单引号字符 `''`
- 双引号字符 `""`
- 反斜符字符 `\`
- 反引号字符 `` ``

上述列表中的前两个和最后一个字符必须成对出现，而反斜符字符本质上是单目的。这些引号中的每一个对 shell 来说都有不同的含义。我们将在本章的不同章节中分别介绍它们。

### 单引号

在 shell 中，你可能需要使用引号有很多理由，其中之一是为了保留通常会被空白字符分隔的字符。让我们来看一个例子。这里有一个包含姓名和电话号码的 `phonebook` 文件：

```
$ phonebook
Alice Smith 973-555-2015
Barbara Swingle 201-555-2257
Liz Stern 212-555-2298
Susan Goldberg 201-555-3776
Susan Topple 212-555-4932
Tony Iannino 973-555-1295
```

要在我们的电话簿文件中查找某人（为了示例，这里文件保持得很小），请使用 `grep`：

```
$ grep phonebook
Alice Cheeba 973-555-2015
$
```

看看当你查找 Susan 时发生了什么：

## 我能引用这句话吗？

```
$ grep Susan phonebook
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
$
```

有两行都包含 Susan，这解释了输出的两行内容。解决这个问题的一种方法是正确地指定名称。例如，你可以指定姓：

```
$ grep Susan Goldberg phonebook
grep: can't open Goldberg
Susan Goldberg 201-555-7776
Susan Topple 212-555-4932
$
```

回想一下，shell 使用一个或多个空白字符来分隔行上的参数，之前的命令行导致 `grep` 接收了三个参数：*Susan、Goldberg 和 phonebook*（见图 6.1）。

当执行 `grep` 时，它将第一个参数视为模式，将剩余参数视为要查找该模式的文件名。在这种情况下，`grep` 认为它应该在文件 **Goldberg 和 phonebook** 中查找 Susan。因此，它尝试打开文件 Goldberg，但没有找到它，并发布了错误消息：

```
grep: can't open Goldberg
```

然后它转到下一行 *phonebook*，打开它，搜索模式 *Susan*，并打印出两个匹配的行。这个问题的根源在于尝试将空白字符解析为程序的参数。这可以通过将整个参数括在一对单引号内来实现：

```
$ grep 'Susan Goldberg' 'phonebook'
```

当 shell 看到第一个引号时，它会忽略任何特殊字符，直到它看到闭合引号。

```
$ grep 'Susan Goldberg' 'phonebook'
Susan Goldberg 201-555-7776
$
```

在这种情况下，shell 遇到了第一个 ' ，并忽略了直到找到结尾 ' 之前的任何特殊字符。因此，Susan 和 Goldberg 之间的空格（这通常会分隔两个参数）被 shell 忽略了。因此，shell 将命令行分为两个参数：第一个是 Susan Goldberg（包含空格字符），第二个是 phonebook。然后它执行了 grep，并向其传递了这两个参数（见图 6.2）。

图 6.2. `grep 'Susan Goldberg' phonebook`.

随后，`grep` 提取了第一个参数 Susan Goldberg，并在第二个参数 phonebook 指定的文件中查找它。请注意，shell 会从命令行中移除引号，不会将它们传递给程序。

无论引号之间包含多少个空格，shell 都会保留它们。

在第一种情况下，shell 从命令行中移除引号并不会将它们传递给程序。在第二种情况下，shell 从命令行中移除引号并不会将它们传递给程序。

图 6.3. `echo 'Susan Goldberg' phonebook`.

图 6.4. `echo 'Susan Goldberg' phonebook`.

无论引号之间包含多少个空格，shell 都会保留它们。

在第一种情况下，shell 从命令行中移除引号并不会将它们传递给程序。在第二种情况下，shell 从命令行中移除引号并不会将它们传递给程序。

## 我能引用那句话吗？

```
$ echo 'How are you today,
> John
$ 
```

即使是回车键，如果包含在引号内，shell 也会忽略它：在输入第一行后，shell 看到引号未匹配，它会等待你输入。作为 shell 正在等待你完成命令的指示，它将其提示符字符从 $ 变为 >。这被称为你的次级提示符（secondary-prompt character），shell 每当等待你完成命令时都会显示。

在给变量赋值包含空格或特殊字符的值时，也需要引号：

```
$ message="I must say, this is fun"
$ echo message
$ I must say, this is fun
$ text="means all files in the directory"
$ echo
names no numbers phonebook stat means all files in the directory
```

在给变量 `message` 和 `text` 赋值时需要引号，是因为其中嵌入了空格。在前面的示例中，你被提醒 shell 在变量名替换之后仍然会进行文件名替换，这意味着在执行 `echo` 之前，* 会被替换为当前目录下所有文件的名称。有一种方法可以消除这种困扰，那就是使用双引号。

### 双引号

双引号的工作原理与单引号类似，但它们不是限制性的。单引号告诉 shell 忽略所有包含在内的字符，而双引号说是忽略大部分字符。具体来说，双引号不会忽略以下三个字符：

- 美元符号 (`$`)
- 反引号 (`` ``)
- 反斜符 (`\`)

美元符号未被忽略，意味着 shell 在双引号内部执行变量替换。

```
$ x=
$ echo $x
addresses into lotspaces names nu numbersbook stat
$ echo '$x'
```

## 我可以引用它吗？

在这里，我们看到了引号、单引号、双引号之间的主要区别。在第一种情况下，shell 看到星号并替换当前目录下的所有文件名。在第二种情况下，shell 保持单引号内的字符不变，导致显示为 \*。在最后一种情况下，双引号指示 shell 在双引号内执行变量替换。因此，shell 会对 $ 进行替换。由于在双引号内不进行文件名替换，\* 随后被作为要显示的值传递给 `echo`。

所以，你想替换变量的值，但不想让 shell 正确处理替换后的字符，你必须将变量包含在双引号内。

这里有另一个说明双引号和无引号区别的示例：

```bash
$ address=39 East 12th Street
> New York, N. Y. 10000
echo $address
39 East 12th Street New York, N. Y. 10000
echo "$address"
39 East 12th Street New York, N. Y. 10000
```

赋值给 `address` 的值包含在单引号还是双引号中并没有区别。shell 在两种情况下都会显示次级命令提示符，告诉它正在等待相应的闭合引号。

在将两行地址赋值给 `address` 后，通过 `echo` 显示了变量的值。注意 `address` 显示在单行上。原因与导致以下内容相同：

```bash
echo one
two three four
```

显示为

one two three four

回想一下，shell 会从命令行中移除空格、制表符和换行符（即空白字符），并将其切割成参数。在情况下

```bash
echo address
```

shell 简单地删除了嵌入的换行符，将其处理为空格或制表符：作为参数分隔符。然后它将九个参数传递给 `echo` 进行显示。`echo` 永远没有机会处理那个换行符；shell 先处理了它（见图 6.5）。

当使用命令

```bash
echo "address"
```

时，shell 会像以前一样替换 `address` 的值，但双引号告诉它保留任何嵌入的空白字符。因此，在这种情况下，shell 向 `echo` 传递了一个参数——一个包含嵌入换行符的参数。`echo` 简单地在终端上显示它的单个参数；图 6.6 说明了这一点。换行符由字符 `\n` 表示。

双引号可以用来向 shell 隐藏单引号，反之亦然：

```bash
$ x='Hello, he said'
$ echo $x
'Hello, he said'
$ article='Keeping the Logins from lagging, Bell Labs Record'
$ echo $article
'Keeping the Logins from Lagging, Bell Labs Record '
```

### 反斜杠

基本上，反斜杠等同于在单个字符周围加上单引号，但有少数微小的例外。反斜杠引用紧随其后的单个字符。其通用格式为

`\c`

其中 `c` 是你想要引的字符。该字符上带有的任何特殊含义都会被移除。这里有一个示例：

```bash
$ echo
syntax error: 'newline or ; unexpected'
$ echo \> 
$
```

在第一种情况下，shell 看到 > 并认为你想要将 `echo` 的输出重定向到文件。因此，它期望后面跟着一个文件名。因为没有跟着，shell 发出了错误信息。在下一种情况下，反斜杠移除了 > 的特殊含义，因此它被传递给 `echo` 进行显示。

```bash
$ x=*
$ echo \$x
x
```

在这种情况下，shell 忽略了紧随反斜杠的 $，结果没有执行变量替换。

由于反斜杠会移除其后字符的特殊含义，你能猜到如果那个字符是反斜杠会发生什么吗？对，它移除了反斜杠的特殊含义：

```bash
$ echo \\
$
```

自然，你也可以写成

```bash
$ echo '\'
$
```

### 使用反斜杠换行延续

正如开头提到的，这其中的一个例外是当行尾的反斜杠被用于续行时：

```bash
echo one \
two three four
```

### 双引号内部的反斜杠

我们之前注意到，在双引号内部，反斜杠可以用来转义某些字符。如果反斜杠后面跟随的是 $, ", \ 或反斜杠以外的任何字符，则反斜杠会被简单移除。如果反斜杠后面跟随的是 $, ", \ \ 或反斜杠本身，则该字符被保留：

```bash
$ x="1"
echo "\$x"
1
echo "\\"
"
echo "\\\"
\
```

## 我可以引用你吗？

### 反引号 (Back Quote)

反引号与之前遇到的任何类型的引号都不同。它的目的不是保护字符免受 shell 的影响，而是执行包含在其中的命令，并将命令的标准输出插入到命令行该位置。使用反引号的一般格式为：

```
command
```

其中 `command` 是要执行的命令名称，`output` 是要插入该位置的内容。

这里有一个示例：

```
echo The Date and time is: date
date and time is: Wed Aug 28 14:28:43 EST 2002
```

当 shell 开始对命令行进行初始扫描时，它发现了反引号并预期后面跟着一个命令名称。在这种情况下，shell 发现要执行 `date` 命令。因此，它执行 `date` 并命令行上的 "date" 替换为 `date` 的输出。随后，它以正常方式将命令行转换为参数，并启动 `echo` 命令的执行。

```
echo Your current working directory is: pwd
Your current working directory is: /users/steve/shell/chaf
```

在这里，shell 执行 `pwd`，将其输出插入命令行，然后执行 `echo`。请注意，在接下来的章节中，所有使用 `$(...)` 的地方都可以使用反引号。

### $(...) 结构

POSIX 标准 shell 支持使用 `$(...)` 结构进行命令替换。其一般格式为 `$(command)`，在反引号方法中，`command` 是其标准输出要替换到命令行上的命令名称。例如：

```
echo The Date and time is: $(date)
date and time is: Wed Aug 28 14:28:43 EST 2002
```

出于以下几个原因，这种方法比反引号更好。首先，使用正引号和反引号组合的复杂命令可能更容易阅读，特别是当你使用的类型在视觉上与单引号和反引号没有区别时；其次，`$(...)` 结构可以很容易嵌套，允许在命令替换内部进行命令替换。反引号也可以进行嵌套，但会有点复杂。你将在本节中看到一个嵌套命令替换的示例。

> 注意，使用反引号进行命令替换不再是首选方法；但我们在这里介绍它，是因为有许多旧的 shell 程序仍在使用它。此外，如果你以后需要编写可移植到不支持新的 `$(...)` 结构的 Unix 系统 shell 程序，你也应该了解反引号。
