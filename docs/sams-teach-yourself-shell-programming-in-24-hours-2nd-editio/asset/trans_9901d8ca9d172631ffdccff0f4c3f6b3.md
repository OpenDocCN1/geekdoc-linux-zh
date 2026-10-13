
## 查找单词

grep 命令的基本语法是

```
grep word file
```

这里 file 是你要搜索指定 word 的单词的文件名。file 中包含 word 的每一行都会被显示。当你指定多个文件时，grep 会在每一行输出前加上包含该行的文件名称。

例如，以下命令会定位文件 ch15.doc（本章）中单词 pipe 的所有出现位置：

```
$ grep pipe ch15.doc
I’ve broken the command into two lines, with the pipe character
as the
the right thing and use the next line as the command to pipe to. It’s
The first few lines look like (ten actually, I piped the output to
```

如果指定多个文件，输出将如下所示：

```
$ grep pipe ch15.doc ch15-01.doc
ch15.doc:I’ve broken the command into two lines, with the pipe
character as the
ch15.doc:the right thing and use the next line as the command to
pipe to. It’s
ch15.doc:The first few lines look like (ten actually, I piped the
output to
ch15-01.doc:I’ve broken the command into two lines, with the pipe
character as the
ch15-01.doc:the right thing and use the next line as the command to
pipe to. It’s
ch15-01.doc:The first few lines look like (ten actually, I piped
the output to
```

正如你所见，包含单词 pipe 的每一行前都加上了文件名。

如果 grep 在任何指定的文件中都找不到包含所请求单词的行，则不会产生输出。例如，

```
$ grep utilities ch15.doc
```

因为单词 utilities 未出现在文件 ch15.doc 中，所以不会产生输出。

## 不区分大小写的匹配

grep 的一个特性是它区分大小写；grep 只匹配在内容和大小写上都与该单词相同的单词。例如，grep 将单词 Apple† 和 applet 视为不同的单词。例如，命令

产生输出：

```
all unix users
The GNU versions of these commands support all the
unix has several additional pieces of information associated with it.
unix counterparts, but implement a few nice options which makes their
unix files names, but they are, and handling them correctly is
```

另一方面，命令

```
$ grep UNIX ch15.doc
```

产生不同的输出：

```
GNU stands for GNU's not UNIX and is the name of a UNIX-compatible
Project utilities are the GNU implementation of familiar UNIX programs
```

有时你希望无论指定的大小写如何都能匹配单词。这可以通过使用 -i 选项来实现。你可以使用 -i 选项如下获取前面两个示例输出的总和：

```
$ grep -i UNIX ch15.doc
```

```
GNU stands for GNU's not UNIX and is the name of a UNIX-compatible
Project utilities are the GNU implementation of familiar UNIX programs
*programs
all unix users
The GNU versions of these commands support all the
unix has several additional pieces of information associated with it.
unix counterparts, but implement a few nice options which makes their
unix files names, but they are, and handling them correctly is
```

## 从 STDIN 读取

当未指定文件时，grep 会在输入到 STDIN 的行中查找匹配项。这使得 grep 非常适合与管道一起使用。例如，以下命令会在 who 命令的输出中查找所有名为 ranga 的用户：

```
$ who | grep ranga
ranga tty1 Aug 26 14:12
ranga tty2 Nov 23 14:15 (rishi.bosland.u)
```

## -v 选项

大多数情况下你使用 grep 在文件中搜索特定单词，但有时你想要获取所有不匹配特定单词的行列表。使用 grep，这很简单——指定 -v 选项。例如，以下命令会生成 /etc/hosts 中不包含 # 字符的所有行列表：
$ grep -v '^ #' /etc/hosts
输出将类似于以下内容：
10.32.43.51 scotch scotch.CSUA.CSUA.Berkeley.EDU
10.32.43.52 internal.internal.soda.CSUA.Berkeley.EDU
10.32.43.139 mkv.csua.berkeley.edu

-v 选项的一个常见用途是解析 ps 命令的输出。例如，如果你正在查找系统中正在运行的所有 bash 实例，你可以使用以下命令

```
$ /bin/ps -ef | grep bash
```

通常输出只包含 bash 的信息，但有时输出看起来像以下内容：

```
ranga 3277 3276 2 13:41:45 pts/0 0:02 -bash
ranga 3463 3277 4 18:38:26 pts/0 0:00 grep bash
```

此列表中的第二个进程是你刚刚运行的 grep 命令。因为它并不是真正的 bash 实例，所以你希望将其从输出中移除。你可以使用 -v 选项如下操作：

```
$ /bin/ps -ef | grep bash | grep -v grep
```

这会移除多余的输出：

```
ranga 3277 3276 0 13:41:45 pts/0 0:02 -bash
```

## 行号

当 grep 在文件中查找给定单词时，它会跟踪已检查的行号。你可以通过指定 -n 选项让 grep 列出行号以及匹配的行。当指定此选项时，grep 的输出格式如下：

```
file:line number:line
```

这里 file 是匹配发生的文件名，line number 是匹配行所在文件的行号，而 line 是包含指定单词的完整行。例如，命令

```
$ grep -n pipe ch15.doc ch15-01.doc
```

产生以下输出：

```
ch15.doc:968:I've broken the command into two lines, with the
character as the
ch15.doc:971:the right thing and use the next line as the command
to pipe to. It's
ch15.doc:1014:The first few lines look like (ten actually, I piped
the output to
ch15-01.doc:964:I've broken the command into two lines, with the
pipe character as the
ch15-01.doc:966:the right thing and use the next line as the command
to pipe to. It's
ch15-01.doc:1009:The first few lines look like (ten actually, I
piped the output to
```

正如你所见，行在两个文件中可能相同，但行号不同。

## 仅列出文件名

有时你并不关心文件中匹配特定单词的实际行。你只想要包含该单词的所有文件列表。例如，以下命令会在 projects 目录中的所有文件中查找单词 delete：

```
$ grep delete projects/*
```

在这种情况下，它产生以下输出：

```
poops.c:/* Function to delete a node from the heap. Adapted from
*introduction
poops.c:void heap_delete(binary_heap *a,int i) {
poops.c: node deleted;
poops.c: /* return void if an error if the input is invalid, ie trying
*to delete
poops.c: sprintf(messages,"heap_delete()"); hd, no such element.",i);
poops.c: /* switch the item to be deleted with the last item, and
*then
poops.c: deleted = a->elements[i];
poops.c: /* compare priority(a->elements[i][deleted]) ? heap_
*up(a,i); heap_down(a,i); */
poops.c:heap_delete(binary_heap *a,int i) {
scheduler.c: /* if the requested id is in the heap, delete it */
scheduler.c: heap_delete(any_heap,node_num);
```

查看输出时，你会看到只有三个文件——poops.c、poops.h 和 scheduler.c——包含单词 delete。在这里，你必须生成匹配行的列表，然后手动查看包含这些行的文件名。通过使用 grep 命令的 -l 选项，你可以更快地得出此结论。例如，以下命令

```
$ grep -l delete projects/*
```

```
poops.c
poops.h
scheduler.c
```

产生你想要的列表。

## 计数单词

计数单词是 shell 脚本中的一项基本功能。有很多方法可以做到这一点，其中最简单的是 wc 命令。不幸的是，它只显示字符数、单词数或行数。那么当你需要统计文件中特定单词的出现次数时怎么办？wc 命令就不够用了。在本节中，你将使用以下命令解决此问题：

- tr
