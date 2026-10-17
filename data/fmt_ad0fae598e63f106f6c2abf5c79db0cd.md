
```bash
stetson@linux_rocks:#$ ps aux | sort -nk +4 | tail > processes.txt
stetson@linux_rocks:#$
root@linux_rocks:#$ cat processes.txt
USER PID %CPU %MEM VSZ RSS TTY STAT START TIME
root 792 0.0 0.0 14640 756 pts/0 S+ 22:19 0:00
sort -nk +4 793 0.0 0.0 1980 560 pts/0 S+ 22:19 0:00
tail
root 1 0.0 0.1 3744 2964 pts/0 Ss 13:10 0:00 /bin/bash
root 791 0.0 0.1 5472 2348 pts/0 R+ 22:19 0:00 ps
aux
```

这和上面的例子相同，只是最后我们将输出发送到了 `processes.txt` 文件。

管道是一个强大的运算符！通过使用管道命令，一个命令的输出变成了另一个命令的输入。

### Tee —— 不仅仅给水工用

`tee` 命令允许我们将输出同时复制到标准输出和文件。

使用 `tee` 命令在你需要在看到输出的同时也将其保存到文件中时非常有用。

热力提示 🔥：你可以使用 `-a` 标志配合 `tee` 来追加文件而不是覆盖它。

现在来看一个例子：

```bash
root@linux_rocks:/# ls -l | tee output.txt
```

在这种情况下，`ls -l` 的输出显示在屏幕上并保存到 `output.txt`。

我们还可以对多个文件使用 `tee`：

```bash
root@linux_rocks:/# ls -l | tee file1.txt file2.txt
```

现在 `ls -l` 的输出显示在屏幕并保存到 `file1.txt` 和 `file2.txt`。

`Tee` 是一个强大的工具！

### Grep 中的正则表达式

正则表达式（通常缩写为 regex）是查找和处理文本极其强大的工具。在本节中，我们将使用 `grep` 配合正则表达式搜索文本。正则表达式广泛应用于 IT 和软件开发，在许多编程语言、文本编辑器以及如 `awk` 和 `sed` 等工具中都有支持。

理论足够了，让我们进入示例。用任何文本编辑器创建一个名为 `my_regex.txt` 的文件并添加以下内容（确保行末尾没有空格）：

Free like the bird's wings

Linux soars with open-source

Freedom to explore

首先我们用 `^` 字符匹配行的开头：

```bash
stetson@linux_rocks:~$ grep ^Freedom my_regex.txt
Freedom to explore
```

接下来，我们用 `$` 匹配行尾：

```bash
stetson@linux_rocks:~$ grep wings$ my_regex.txt
Free like the bird's wings
```

通过点，我们将匹配 `L` 之后的单个字符：

```bash
stetson@linux_rocks:~$ grep L. my_regex.txt
Linux soars with open-source
```

我们可以通过多个点匹配任意数量的字符。在这里我们寻找“o”后面的任意 4 个字符：

```bash
stetson@linux_rocks:~$ grep o.... my_regex.txt
Linux soars with open-source
Freedom to explore
```

让我们尝试一些高级的正则表达式。创建一个文件并添加以下内容并为 `words.txt`：

```
babble
bubble
bubble
```

我们现在可以使用 `[]` 括号搜索括号内的字符。这里有一个例子：

```bash
stetson@linux_rocks:~$ grep b[au]bble words.txt
babble
bubble
```

我们的正则表达式返回了 `babble` 和 `bumble`，是因为我们指定了 `a` 和 `u` 字符。它没有返回 `bobble`，因为括号中没有“o”。

我们可以在括号内使用 `^` 字符来搜索**不包含**该字符的任何内容。

现在让我们查找 `b[^u]bble`：

```
stetson@linux_rocks:~$ grep b[^u]bble words.txt
babble
bobble
```

我们得到了 `babble` 和 `bobble`，但没有得到 `bubble`，因为我们告诉 `grep` 不需要返回 `u` 字符。

这是对正则表达式的简要概述。我鼓励你深入学习正则表达式，因为它们非常强大。正则表达式并不是你总能脱口而出的东西，但在搜索特定字符串时，你很可能会去 Google 或研究。我不清有多少次需要 Google 类似“搜索所有包含 192 的行的正则表达式”之类的请求。

正则表达式将成为你 Linux 之旅中的强大工具，本节将为未来的学习奠基础。

### cut

`cut` 是一个文本处理实用，我们可以用它快速地切割或分割文本并将其输出到标准输出 `stdout`。现在来看一些示例。在你的 shell 中输入以下命令：

```
stetson@linux_rocks:/tmp$ echo -e "This is my shell\nThere are many
like it\nBut this one is mine" > shell_creed.txt
```

注意，`-e` 标志告诉 `echo` 解析反斜杠转义，我们使用 `\n` 来指定新行。然后，我们将输出重定向到名为 `shell_creed.txt` 的新文件中。

接下来，我们将使用 `cut` 来切分行：

```
stetson@linux_rocks:/tmp$ cut -c 1 shell_creed.txt
T
B
```

`c` 标志告诉 `cut` 输出每行的第一个字符。现在尝试更改 `-c` 标志的参数：

```
stetson@linux_rocks:/tmp$ cut -c 4 shell_creed.txt
s
r\s
```

在上方，我用 `\s` 标记了空格字符，以显示 `cut` 会解释并输出空格！最后行的第 4 个字符恰好是一个空格。

如果我们想要每行的第二个单词呢？我们可以使用 `-f` 字段标记来获取每行的第二个单词：

```
stetson@linux_rocks:/tmp$ cut -f 2 shell_creed.txt
This is my shell
There are many like it
But this one is mine
```

等等！这不起作用。我们得到了整个文件。为什么？默认情况下，它设置为查找 TAB 分隔符，所以我们需要告诉它使用空格。现在使用 `-d` 或分隔符标志来这样做：

```
stetson@linux_rocks:/tmp$ cut -f 2 -d ' ' shell_creed.txt
is
re
this
```

好多了！

正如你所见，`cut` 是另一个可以加入我们工具箱的文本处理工具。与任何 Linux shell 工具一样，当它通过重定向 `>` 或管道运算符 `|` 与命令结合用时，它会变得更加强大。

### 使用 Word Count 统计行

在某些时刻，你可能会发现你想统计文件的行数。这很简单，只需使用 `wc` `Word Count` 命令。在不带任何参数的情况下，`wc` 会返回单词数、行数和字节数。

这是一个示例：

```
stetson@linux_rocks:/tmp$ wc file.txt
8059 8059 32236 file.txt
```

如果你只需要文件中的行数，可以使用 `-l` 标志：

```
stetson@linux_rocks:/tmp$ wc -l file.txt
8059 file.txt
```

使用 `wc` 的另一种常见方法是将 `cat` 的输出传递给 `wc`：

```
stetson@linux_rocks:/tmp$ cat file.txt | wc -l
8059
```

简单！让我们继续。

### sed and awk

`sed` 和 `awk` 是两个经常配合编辑文本的命令行工具。它们通常用于分析大型文本文件或快速编辑文本文件。例如，`sed` 可以替换大型文本文件中单词的每个实例。

### sed

`sed` 代表流编辑器 `stream editor`，到目前它已变成一个古老而强大的工具。`sed` 最初于 1971 年在贝尔实验室开发，就像 Unix 一样。`sed` 实际上被认为是一种编程语言。它是如此强大，甚至被认为是图灵完备。

让我们花一点时间了解图灵完备性。
