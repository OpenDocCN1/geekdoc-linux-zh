

\}: : 表示前一个字符重复 n 次。

\{n,m\} : 表示前一个字符本身重复最 n 次，最多 m 次。

\{n,\} : 表示前面的字符至少出现十次。

+ : 表示前一个字符出现一次或多次。

\? : 表示前面的字符出现 0 次或一次。

\. : 指代前一个或后一个字符。

\(\.) 将正则表达式定义为一个分组。

\. : 确保被视为特殊字符的普通字符处理。

# 示例:

- a?b : b,ab...
- a[^a-z] : a0, a1, aZ,...
- ^a : 以 a 开头的单词
- ^zzz or ^z\3\} : 行首有 3 个 z字符的单词
- \{3|5\}+ : 至少包含一次 3 或 5 个数字的单词
- \<Z> : 查找以 Zey 开头的行
- yi> : 查找以 yi 结尾的行

```
root@kemal:~# cat test
Zeynep
kemal
Ceren
cenK
Zengin
root@kemal:~# grep "\Ze" test
Zeynep
Zengin
root@kemal:~# grep "in\>" test
Zengin
root@kemal:~# _
```

例如，使用 ^B.*x$，我们可以找到以 B 开头并以 x 结尾的表达式。

```
root@kemal:~# cat test
Zeynep
kemal
Ceren
cenK
Zengin
Best of Linux
root@kemal:~# grep ^B.*x$ test
Best of Linux
root@kemal:~# _
```

# 第 18 章

# Sed 和 Awk

在 Sed（流编辑器）和 awk 命令中，我将首先谈论 sed 的用法。事实上，sed 和 awk 与其说是说是程序而不是命令。我们从控制台将它们作为命令使用，但请记住两者都是非常高级且灵活的工具。

# Sed (流编辑器)

我们可以使用 sed 程序对文本文件进行一些更改。我们可以通过直接从控制台输入命令，或确保从文件中获取命令来实现。我们在执行任务时可以使用的运算符/参数如下：

- -n: 仅对指定的行执行操作。
- -e: 下一个命令是修改命令。
- -f: 下一个语句是文件名（即从文件读取输入）。
- -p: 打印。
- -d: 意味着删除。
- s/before/after/g : 此操作可以更改文本文件中的短语。如果结尾没有添加 g，它将替换每行的第一个匹配项，而不是整个文件。

在使用 sed 时，也可以使用正则表达式。以下是一些示例：

- 5d: 5: 删除第 5 行。
- /^$/d: 删除所有空行。
- s/\$//: 删除每行末尾的空格。
- /abc/d: 删除所有包含 abc 的行。
- s/00*/0/g: 用单个零代替连续的零。
- sed -e "s/apple/orange/g" -e "s/prg/program/g" : 为了同时替换多个内容，可以使用 -e。
- s/\.\&lg: 点后的字符将移动到新行。
- 10,20d: 删除从第 10 行到第 20 行（包括第 10 行和第 20 行）。
- ^\*\*\*\$/d: 删除所有行内全是 ***** 的行。
- sed -e "s/[^|]*\*/" <file: 指定文件中的制表符和空格字符。

让我们来看 sed 的几个用法示例。例如，删除测试文件中内容的第二行。为此，我们可以使用 sed -e "2d" test 命令。

```
root@kemal:~ cat test
Zeynep
kemal
Ceren
cenK
Zengin
Best of Linux
root@kemal:~# sed -e "2d" test
Zeynep
Ceren
cenK
Zengin
Best of Linux
root@kemal:~# _
```

# 196 | Linux 命令精通

现在要在文本中用一个单词替换另一个单词，让我们使用 sed -n "s/Linux/Hacking/p" test 命令。

```
root@kemal:-# cat test
Zeynep
kemal
Ceren
cenK
Zengin
Best of Linux
root@kemal:-# sed -n "s/Linux/Hacking/p" test
Best of Hacking
root@kemal:-#
```

如你所见，我们更改了单词，并通过 p 在屏幕上显示内容。我们使用 -n 在屏幕上打印包含单词更改的行。

让我们更改文本中的单词并查看 g 参数的作用。我们想将文件中的 Linux 单词替换为 Kali。首先我们应该使用 `cat test | sed "s/Linux/ Kali /"` 命令，然后使用 `cat test | sed "s/Linux/Kali/g"` 命令，让我们看看它们的差异。

```
root@kemal:-# cat test
Best of Linux
Linux
Debian Linux and CentOS Linux
root@kemal:-# cat test | sed "s/Linux/Kali/"
Best of Kali
Kali
Debian Kali and CentOS Kali
root@kemal:-# cat test | sed "s/Linux/Kali/g"
Best of Kali
Kali
Debian Kali and CentOS Kali
root@kemal:-# _
```

如所示，如果命令末尾没有添加 g，操作将不是针对整个文件，而是在每行的第一个匹配项上执行。

# Kemal Demirez | 197

让我们再做另一个删除特定行的示例。这次，例如，删除第 2、3 和第 4 行。为此，我们使用了 sed -e "2,4d" test 命令。

```
root@kemal:-# cat test
Linux BackTrack 5
Kali Linux 2.0
Ethical Hacking
CentOS
RedHat System Mng.
root@kemal:-# sed -e "2,4d" test
Linux BackTrack 5
RedHat System Mng.
root@kemal:-#
```

我们只需要记住的一个小细节：如果我们想删除多行，可以使用范围。例如，要删除第 2 到第 4 行，我们使用 `sed -e "2,4d"`。

```
root@kemal:~# cat test
Zeynep
kemal
Ceren
cenK
Zengin
Best of Linux
root@kemal:~# sed -e "2d" test
Zeynep
Ceren
cenK
Zengin
Best of Linux
root@kemal:~# _
```

等待，原文在后面的页面有一些重复和错误。我将根据提供的文本提供清理的版本。

