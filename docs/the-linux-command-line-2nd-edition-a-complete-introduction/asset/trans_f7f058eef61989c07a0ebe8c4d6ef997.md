

要查看可用变量的列表，可以尝试这样操作：

```
[me@linuxbox ~]$ printenv | less
```

你可能已经注意到，对于其他类型的展开，如果拼写错误，展开将不会发生，echo 命令只会简单地显示拼写错误的模式。对于参数展开，如果拼写错误变量名，展开仍然会发生，但结果会是一个空字符串：

```
[me@linuxbox ~]$ echo $SUER
[me@linuxbox ~]$
```

## 命令替换

命令替换允许我们将命令的输出用作展开：

```
[me@linuxbox ~]$ echo $(ls)
Desktop Documents ls-output.txt Music Pictures Public Templates Videos
```

我最喜欢的一种用法是这样的：

```
[me@linuxbox ~]$ ls -l $(which cp)
-rwxr-xr-x 1 root root 71516 2007-12-05 08:58 /bin/cp
```

在这里，我们将 which cp 的结果作为参数传递给 ls 命令，从而在不知道其完整路径名的情况下获取 cp 程序的列表。我们并不局限于简单的命令。整个管道也可以使用（仅显示部分输出）：

```
[me@linuxbox ~]$ file $(ls -d /usr/bin/* | grep zip)
/usr/bin/bunzip2:      symbolic link to `bzip2'
```

## 双引号

我们要看的第一种引用类型是 *双引号*。如果你将文本放在双引号内，shell 使用的所有特殊字符都会失去其特殊含义并被视为普通字符。例外情况是“$”、“\\”（反斜杠）和“`”（反引号）。这意味着词分割、路径名展开、波浪号展开和大括号展开会被抑制，但参数展开、算术展开和命令替换仍然会执行。使用双引号，我们可以处理包含嵌入空格的文件名。假设我们不幸遇到了一个名为 `two words.txt` 的文件。如果我们在命令行上尝试使用它，词分割会将其视为两个单独的参数而不是期望的单个参数：

```
[me@linuxbox ~]$ ls -l two words.txt
ls: cannot access two: No such file or directory
ls: cannot access words.txt: No such file or directory
```

通过使用双引号，我们停止了词分割并得到期望的结果；此外，我们甚至可以修复损坏：

```
[me@linuxbox ~]$ ls -l "two words.txt"
-rw-rw-r-- 1 me me 18 2008-02-20 13:03 two words.txt
[me@linuxbox ~]$ mv "two words.txt" two_words.txt
```

好了！现在我们不必再一直输入那些讨厌的双引号了。

记住，参数展开、算术展开和命令替换在双引号内仍然会发生：

```
[me@linuxbox ~]$ echo "$USER $(($((2+2)) $(cal)"
me 4     February 2008
Su Mo Tu We Th Fr Sa
               1  2
 3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29
```

我们应该花点时间来看一下双引号对命令替换的影响。首先让我们更深入地了解一下词分割的工作原理。在我们之前的示例中，我们看到了词分割似乎会删除我们文本中多余空格的方式：

```
[me@linuxbox ~]$ echo this is a    test
this is a test
```

默认情况下，词分割会查找空格、制表符和换行符（换行字符）的存在，并将它们视为单词之间的分隔符。这意味着未加引号的空格、制表符和换行符不被视为文本的一部分。它们仅用作分隔符。由于它们将单词分隔成不同的参数，我们的示例命令行包含一个命令，后跟四个不同的参数。如果我们加上双引号：

```
[me@linuxbox ~]$ echo "this is a    test"
this is a    test
```

词分割被抑制，嵌入的空格不再被视为分隔符，而是成为参数的一部分。加上双引号后，我们的命令行包含一个命令，后跟一个参数。

由于换行符被词分割机制视为分隔符，这对命令替换产生了一个有趣的、 albeit 微妙的影响。请考虑以下内容：

```
[me@linuxbox ~]$ echo $(cal)
February 2008 Su Mo Tu We Th Fr Sa 1 2 3 4 5 6 7 8 9 10 11 12 13 14
15 16 17 18 19 20 21 22 23 24 25 26 27 28 29
[me@linuxbox ~]$ echo "$(cal)"
February 2008
Su Mo Tu We Th Fr Sa
1  2
3  4  5  6  7  8  9
10 11 12 13 14 15 16
17 18 19 20 21 22 23
24 25 26 27 28 29
```

在第一种情况下，未加引号的命令替换导致命令行包含 38 个参数。在第二种情况下，命令行包含一个参数，其中包含嵌入的空格和换行符。

## 单引号

如果我们需要抑制所有展开，我们使用单引号。以下是未加引号、双引号和单引号的比较：

