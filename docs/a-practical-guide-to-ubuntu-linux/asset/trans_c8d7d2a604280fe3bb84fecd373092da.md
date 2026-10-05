
```
1031  ls
1032  rm *0405
1033  fc -1
1034  cd
1035  whereis aspell
1036  man aspell
1037  cd /usr/share/doc/*-aspell/*
1038  pwd
1039  ls
1040  ls man-html
```

`fc` 内置命令可以通过 `-l` 选项接受零、一个或两个参数。这些参数指定了要显示的历史列表部分：

```
fc -l [first |last]]
```

`fc` 内置命令列出从匹配 `first` 的最近事件开始的命令。参数可以是事件编号、命令行行的前几个字符或负数（被视为倒数第 n 个命令）。如果不加 `last`，`fc` 将从最近的事件开始显示。如果包含 `last`，`fc` 将显示从最近匹配 `first` 到最近匹配 `last` 的之间的命令。

下一个命令显示了从 1030 到 1035 的历史列表：

```
$ fc -l 1030 1035
1030  cd ..memos
1031  ls
1032  rm *0405
1033  fc -1
1034  cd
1035  whereis aspell
```

以下命令列出了从以 `view` 开始的最近事件到以 `whereis` 开始的最近命令行之间的事件：

```
$ fc -1 view whereis
1025  view calendar
1026  vim.tiny letter.adams01
1027  aspell -c letter.adams01
1028  vim.tiny letter.adams01
1029  lpr letter.adams01
1030  cd ..memos
1031  ls
1032  rm *0405
1033  fc -1
1034  cd
1035  whereis aspell
```

要从历史列表中列出单个命令，请对第一个和第二个参数使用相同的标识符。以下命令列出了事件 1027：

```
$ fc -l 1027 1027
1027  aspell -c letter.adams01
```

# 334 第 9 章 THE BOURNE AGAIN SHELL

# 编辑并重新执行之前的命令

你可以使用 `fc -e` 来编辑和重新执行之前的命令。

```
fc [-e editor] [first [last]]
```

当你带有 `-e` 选项并后跟编辑器名称调用 `fc` 时，`fc` 会调用编辑器并传入工作缓冲区（Work buffer）中的事件，前提是你指定的编辑器已安装。默认情况下，`fc` 启动 `nano` 编辑器。如果不指定 `first` 和 `last`，它将默认为最近的命令。下一个示例调用 `vim` 编辑器来编辑最近的命令：

```
$ fc -e vi
```

`fc` 内置命令调用独立的 `vim` 编辑器。如果你使用 `FCEDIT` 变量，则不需要在命令行上使用 `-e` 选项来指定编辑器。由于 `FCEDIT` 的值已更改为 `/usr/bin/emacs` 且 `fc` 没有带参数，以下命令将使用 `emacs` 编辑器编辑最近的命令（`emacs` 软件包的一部分；默认不安装）：

```
$ export FCEDIT=/usr/bin/emacs
```

如果你用单个参数调用它，`fc` 会在指定的命令上启动编辑器。以下示例在工作缓冲区中使用事件 1029 启动编辑器。当你退出编辑器时，shell 会执行该命令：

```
$ fc 1029
```

如前所述，你可以通过数字或指定命令名的前几个字符来识别命令。以下示例调用编辑器处理从字母 `vim` 开始的最近事件到事件 1030 的事件：

```
$ fc vim 1030
```

# 清理 fc 缓冲区

**注意**：当你执行 `fc` 命令时，shell 会执行你在编辑器缓冲区中留下的任何内容，可能会产生意外的结果。如果你决定不想执行某个命令，请在退出编辑器之前删除缓冲区中的所有内容。

# 在不调用编辑器的情况下执行命令

你可以在不使用编辑器的情况下重新执行之前的命令。如果你带有 `-s` 选项调用 `fc`，它将跳过编辑阶段并重新执行命令。以下示例重新执行了事件 1029：

```
$ fc -s 1029
lpr letter.adams01
```

下一个示例重新执行了上一个命令：

```
$ fc -s
```

# 历史 335

当你重新执行一个命令时，你可以告诉 `fc` 用一个字符串替换另一个。下一个示例将事件 1029 中的字符串 `adams` 替换为字符串 `john` 并执行修改后的事件：

```
$ fc -s ad=john 1029
lpr letter.adams01
```

# 使用感叹号 (!) 引用事件

Shell 机制使用感叹号来引用事件。这种技术在 bash 中可用，虽然经常很繁琐，但仍非常有用的功能。例如，`!!` 命令重新执行上一个事件，shell 会将 `!!` 替换为上一行的最后一个单词。

你可以使用绝对编号、相对编号或其包含的文本来引用事件。所有对事件的引用（称为事件标识符，event designators）都以感叹号 (`!`) 开始。感叹号后跟着一个或多个字符以指定事件。你可以将历史放在命令的任何位置。要转义感叹号以便 shell 将其字面解释而非历史事件的开头，请在感叹号前加反斜杠 (`\`) 或将其包含在引号内。

# 事件标识符

事件标识符指定历史列表中的命令。事件标识符列表见表 9-8。

通过提供 `!!` 命令重新执行上一个事件。在示例中，事件 45 重新执行了事件 44：

```
44 $ !!
ls - text
--rw-r-- max group 45 2010-04-30
45
52 $ !-4
ls - text
--rw-r-- max group 45 2010-04-30
```

当感叹号后跟一个文本字符串时，shell 会搜索并执行以该字符串开始的最近事件。如果你将字符串包含在问号内，shell 将执行包含该字符串的最近事件。如果后面是换行符，则最后的标记是可选的。

```
68 $ history
59 ls -l text
60 tail text5
61 cat text1 text5 > letter
62 vim.tiny letter
63 cat letter
64 cat memo
65 lpr memo
66 pine zach
67 ls -l
68 history
69 $ !
70 ls -1
70 $ !lpr
lpr memo
71 $ !letter?
```

表 9-8 事件标识符
| 标识符 | 含义 |
| :--- | :--- |
| ! | 启动历史事件，除非后面紧跟空格、换行或等。 |
| !! | 上一个命令。 |
| !n | 历史列表中的第 n 命令。 |
| !-n | 倒数 n 个命令。 |
| !string | 以字符串开始的最近命令。 |
| !string[] | 包含字符串的最近命令。最后一个是可选的。 |
| # | 当前命令（你目前输入的内容）。 |
| {event} | 事件本身。大括号将事件与周围文本隔离开。例如，!!3 是后面跟数字3的第三个最近执行命令。 |

# 标识符

单词标识符指定事件中的单词（标记）或一系列单词。（第 338 页的表 9-9 列出了单词标识符。）单词从 0 开始（行的第一个单词——通常是命令），接着是 1（命令后的第一个单词），并在 n（行的最后一个单词）结束。

要从之前的事件指定特定单词，请在事件标识符（如 `!14`）后跟冒号以及单词编号。例如，`!14:3` 指定事件 14 命令后的第三个单词。你可以使用脱字符 (`^`) 指定命令后的第一个单词（单词数 1），使用美元符号 (`$`) 指定最后一个单词。你可以通过连字符连接两个单词标识符来指定单词范围。

```
72 $ echo apple grape orange pear
apple grape orange pear
73 $ echo !72:2
echo grape
grape
74 $ echo !72:^
echo apple
apple
75 $ !72:0 !72:$
echo pear
pear
76 $ echo !72:2-4
echo grape orange pear
grape orange pear
77 $ !72:0-
echo apple grape orange pear
grape orange pear
```

如果事件包含单个命令，单词编号对应于参数。如果事件包含多个命令，这种对应关系在第一个命令之后的命令就不适用。在示例中，事件 78 包含两个用分号隔的命令，因此 shell 按顺序执行它们；命令是单词 5。

```
78 $ !72 ; echo helen zach barbara
echo apple grape orange pear ; echo helen zach barbara
apple grape orange pear
helen zach barbara
79 $ echo helen !78:7
echo helen
helen
80 $ echo !78:4-7
echo pear ; echo helen
pear
helen
```
