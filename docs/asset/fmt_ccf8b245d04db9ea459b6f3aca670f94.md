
```
[me@linuxbox ~]$ sort -k 1,1 -k 2n distros.txt | sed -f distros-nl.sed | nl

    Linux Distributions Report

      Name      Ver.  Released
      ----      ----  --------
1   Fedora  5     2006-03-20
2   Fedora  6     2006-10-24
3   Fedora  7     2007-05-31
4   Fedora  8     2007-11-08
5   Fedora  9     2008-05-13
```

6 Fedora 10 2008-11-25

7 SUSE 10.1 2006-05-11

8 SUSE 10.2 2006-12-07

9 SUSE 10.3 2007-10-04

10 SUSE 11.0 2008-06-19

11 Ubuntu 6.06 2006-06-01

12 Ubuntu 6.10 2006-10-26

13 Ubuntu 7.04 2007-04-19

14 Ubuntu 7.10 2007-10-18

15 Ubuntu 8.04 2008-04-24

16 Ubuntu 8.10 2008-10-30

我们的报告是命令管道的结果。首先，我们按发行版名称和版本号（第 1 和第 2 字段）对列表进行排序，然后使用 `sed` 处理结果，添加报告头（包括 `nl` 的逻辑分页标记）和页脚。最后，我们使用 `nl` 处理结果，默认情况下，`nl` 仅对属于逻辑页面正文部分的文本流行进行编号。

我们可以重复该命令并尝试 `nl` 的不同选项。其中一些有趣的选项如下：

```
nl -n rz
```

以及以下：

```
nl -w 3 -s ' '
```

## fold—将每行换行到指定长度

折叠是将文本行在指定宽度处断开的过程。与其他命令一样，`fold` 接受一个或多个文本文件或标准输入。如果我们向 `fold` 发送简单的文本流，就可以看到它的工作原理。

```
[me@linuxbox ~]$ echo "The quick brown fox jumped over the lazy dog." | fold -w 12
The quick br
own fox jump
ed over the
lazy dog.
```

这里我们看到 `fold` 的运行情况。`echo` 命令发送的文本被 `-w` 选项指定的段落分割。在此示例中，我们指定行宽为 12 个字符。如果未指定宽度，则默认值为 80 个字符。请注意行是如何在不考虑单词边界的情况下被断开的。添加 `-s` 选项将导致 `fold` 在达到行宽之前在最后一个可用空格处断开行。

```
[me@linuxbox ~]$ echo "The quick brown fox jumped over the lazy dog." | fold -w 12 -s
The quick
brown fox
jumped over
the lazy
dog.
```

## fmt—一个简单的文本格式化程序

`fmt` 程序也进行折叠，还能做更多。它接受文件或标准输入，并对文本流执行段落格式化。基本上，它在填充和连接文本行时保留空行和缩进。

为了演示，我们需要一些文本。让我们从 `fmt` 信息页中取一些。

```
'fmt' reads from the specified FILE arguments (or standard input if none are given), and writes to standard output.

By default, blank lines, spaces between words, and indentation are preserved in the output; successive input lines with different indentation are not joined; tabs are expanded on input and introduced on output.

'fmt' prefers breaking lines at the end of a sentence, and tries to avoid line breaks after the first word of a sentence or before the last word of a sentence. A "sentence break" is defined as either the end of a paragraph or a word ending in any of '.?!', followed by two spaces or end of line,
```

忽略任何中间的括号或引号。与 TeX 类似，`fmt` 在选择换行符之前会读取整个“段落”；该算法是 Donald E. Knuth 和 Michael F. Plass 在 "Breaking Paragraphs Into Lines", `Software--Practice & Experience` 11, 11 (November 1981), 1119-1184 中给出的算法的一个变体。

我们将把这段文本复制到文本编辑器中并将文件保存为 `fmt-info.txt`。现在，假设我们想将此文本重新格式化为适合 50 个字符宽的列。我们可以通过使用 `fmt` 和 `-w` 选项处理文件来实现。

```
[me@linuxbox ~]$ fmt -w 50 fmt-info.txt | head
`fmt' reads from the specified FILE arguments
(or standard input if
none are given), and writes to standard output.

By default, blank lines, spaces between words,
and indentation are
preserved in the output; successive input lines
with different indentation are not joined; tabs
are expanded on input and introduced on output.
```

嗯，这是一个别扭的结果。也许我们应该实际阅读这段文本，因为它解释了正在发生的事情。

默认情况下，空行、单词之间的空格和缩进在输出中得以保留；缩进不同的连续输入行不会被连接；输入时制表符会被扩展，输出时会被引入。

因此，`fmt` 保留了第一行的缩进。幸运的是，`fmt` 提供了纠正此问题的选项。

```
[me@linuxbox ~]$ fmt -cw 50 fmt-info.txt
`fmt' reads from the specified FILE arguments
(or standard input if none are given), and writes
to standard output.

By default, blank lines, spaces between words,
and indentation are preserved in the output;
successive input lines with different indentation
are not joined; tabs are expanded on input and
```

introduced on output.

`'fmt' prefers breaking lines at the end of a sentence, and tries to avoid line breaks after the first word of a sentence or before the last word of a sentence. A "sentence break" is defined as either the end of a paragraph or a word ending in any of `.?!`, followed by two spaces or end of line, ignoring any intervening parentheses or quotes. Like TeX, `fmt' reads entire "paragraphs" before choosing line breaks; the algorithm is a variant of that given by Donald E. Knuth and Michael F. Plass in "Breaking Paragraphs Into Lines", `Software--Practice & Experience' 11, 11 (November 1981), 1119-1184.
