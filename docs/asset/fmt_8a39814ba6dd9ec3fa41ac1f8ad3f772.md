
在这里，我们将 `which cp` 的结果作为参数传递给 `ls` 命令，从而在不知道其完整路径名的情况下获取 `cp` 程序的列表。我们不仅限于简单的命令。整个管道都可以使用（仅显示部分输出）：

```
[me@linuxbox ~]$ file $(ls /usr/bin/* | grep zip)
/usr/bin/bunzip2: symbolic link to 'bzip2'
/usr/bin/bzip2: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.9, stripped
/usr/bin/bzip2recover: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV), dynamically linked (uses shared libs), for GNU/Linux 2.6.9, stripped
/usr/bin/funzip: ELF 32-bit LSB executable, Intel 80386, version 1 (SYSV
), 动态链接（使用共享库），适用于 GNU/Linux 1.6.9，已剥离
/usr/bin/gpg-zip:    Bourne shell 脚本文本可执行文件
/usr/bin/gunzip:    符号链接到 '../../bin/gunzip'
/usr/bin/gzip:      符号链接到 '../bin/gzip'
/usr/bin/mzip:      符号链接到 'mtools'
```

在此示例中，管道的结果成为了 `file` 命令的参数列表。

在旧版 shell 程序中，命令替换还有一种替代语法，`bash` 也支持这种语法。它使用反引号而不是美元符号和括号：

```
[me@linuxbox ~]$ ls -l `which cp`
-rwxr-xr-x 1 root root 71516 2012-12-05 08:58 /bin/cp
```

## Quoting

现在我们已经看到了 shell 可以执行多少种扩展，是时候学习如何控制它了。例如，看看这个：

```
[me@linuxbox ~]$ echo this is a    test
this is a test
```

或者这个：

```
[me@linuxbox ~]$ echo The total is $100.00
The total is 00.00
```

在第一个示例中，shell 的词分割移除了 `echo` 命令参数列表中的多余空白。在第二个示例中，参数扩展将空字符串替换为 `$1` 的值，因为它是一个未定义的变量。shell 提供了一种称为引用的机制来有选择地抑制不需要的扩展。

## Double Quotes

我们要看的第一种引用类型是双引号。如果你将文本放在双引号内，shell 使用的所有特殊字符都会失去其特殊含义并被视为普通字符。例外情况是 `$`（美元符号）、`\`（反斜杠）和 `` ` ``（反引号）。这意味着词分割、路径名扩展、波浪号扩展和大括号扩展会被抑制，但参数扩展、算术扩展和命令替换仍然会执行。使用双引号，我们可以处理包含嵌入空格的文件名。假设我们是不幸的受害者，拥有一个名为 `two words.txt` 的文件。如果我们在命令行上尝试使用它，词分割会将其视为两个独立的参数而不是期望的单个参数：

```
[me@linuxbox ~]$ ls -l two words.txt
ls: cannot access two: No such file or directory
ls: cannot access words.txt: No such file or directory
```

通过使用双引号，我们停止了词分割并得到了期望的结果；此外，我们甚至可以修复损坏：

```
[me@linuxbox ~]$ ls -l "two words.txt"
-rw-rw-r-- 1 me me 18 2012-02-20 13:03 two words.txt
[me@linuxbox ~]$ mv "two words.txt" two_words.txt
```

好了！现在我们不必一直输入那些讨厌的双引号了。记住：参数扩展、算术扩展和命令替换在双引号内仍然会进行：

```
[me@linuxbox ~]$ echo "$USER $(($((2+2)) ) $(cal)"
me  4  February 2012
Su Mo Tu We Th Fr Sa
          1  2  3  4
 5  6  7  8  9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29
```

我们应该花点时间来看一下双引号对命令替换的影响。首先让我们更深入地了解一下词分割的工作原理。在之前的示例中，我们看到了词分割如何似乎移除了我们文本中的多余空格：

```
[me@linuxbox ~]$ echo this is a    test
this is a test
```

默认情况下，词分割会查找空格、制表符和换行符（换行字符）的存在，并将它们视为单词之间的分隔符。这意味着未加引号的空格、制表符和换行符不被视为文本的一部分。它们仅用作分隔符。由于它们将单词分隔成不同的参数，我们的示例命令行包含一个命令，后跟四个不同的参数。然而，如果我们加上双引号，词分割就会被抑制，嵌入的空格不会被视为分隔符；相反，它们成为参数的一部分：

```
[me@linuxbox ~]$ echo "this is a    test"
this is a    test
```

一旦加上双引号，我们的命令行就包含一个命令，后跟一个参数。

由于换行符被词分割机制视为分隔符，这对命令替换产生了有趣的、尽管微妙的效果。请考虑以下内容：

```
[me@linuxbox ~]$ echo $(cal)
 February 2012 Su Mo Tu We Th Fr Sa 1 2 3 4 5 6 7 8 9 10 11 12 13 14 15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
[me@linuxbox ~]$ echo "$(cal)"
```

February 2012
Su Mo Tu We Th Fr Sa
1 2 3 4
5 6 7 8 9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29

首次， unquoted 的命令替换导致命令行包含 38 个参数；在第二次， 结果是包含嵌入空格和换行的 1 个参数的命令行。

## Single Quotes

如果我们需要抑制所有展开，我们使用单引号。以下是未加引号、双引号和单引号的比较：

```
[me@linuxbox ~]$ echo text "/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/is-output.txt a b foo 4 me
[me@linuxbox ~]$ echo text "/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text /*.txt {a,b} foo 4 me
[me@linuxbox ~]$ echo text '/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text /*.txt {a,b} $(echo foo) $((2+2)) $USER
```

正如我们所见，随着引号层级的增加，越来越多的展开被抑制。

## Escaping Characters

有时我们只想引用单个字符。为此，我们可以在字符前加上反斜杠，在此上下文中称为转义字符。通常这是在双引号内完成，以有选择地阻止展开。

```
[me@linuxbox ~]$ echo "The balance for user $USER is: \$5.00"
The balance for user me is: $5.00
```

使用转义来消除文件名中字符的特殊含义也很常见。例如，可以在文件名中使用 shell 通常赋予特殊含义的字符。这些包括 `$`、`!`、`&`、（空格）等。要在文件名中包含特殊字符，可以这样做：

```
[me@linuxbox ~]$ mv bad\&filename good_filename
```
