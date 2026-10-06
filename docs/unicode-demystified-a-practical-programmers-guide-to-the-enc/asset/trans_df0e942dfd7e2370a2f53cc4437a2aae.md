

# 1150 diff

--ignore-blank-lines -B 忽略仅涉及空行数的差异。

--ignore-case -i 在比较文件时忽略大小写引起的差异。

--ignore-space-change -b 忽略行尾的空白（空格和制表符），并将其他空白字符串视为等同。

--p 显示每个更改位于哪个函数中。

--recursive -r 当使用 diff 比较两个目录中的文件时，使比较扩展到子目录。

--side-by-side -y 以并排格式显示输出。此选项生成的输出与 sdiff 相同。使用此选项时配合 --width=columns 选项使用。

--unified[lines=n] -u 使用更易读的统一输出格式。更多详细信息和示例请参阅第 67 页关于 diff 的讨论。lines 是上下文的行数，默认值为三行。

-w whitespace 在比较文件时忽略空白字符符。

--width=columns -w 设置 diff 显示输出列时使用的列数。此选项配合 --side-by-side 选项非常。sdiff 工具使用小写 w 来执行相同的功能：-w columns。

# 注意事项

diff 实用类似于 sdiff，但输出可能更容易读。diff 的 --side-by-side 选项产生的输出与 sdiff 相同。如果你尝试 sdiff，请确保使用 -w columns 选项，该选项将页面宽度设置为列数（默认为 130）。请参见“示例”部分并参考 diff 和 diff into 页面获取更多信息。

# 讨论

当你使用任何选项使用 diff 时，它会产生一系列添加 (a)、删除 (d) 和更改 (c) 指令。每行指令后面都是你需要添加、删除或更改的文件中的行。小于符号 (<) 位于 file1 的行之前。大于符号 (>) 位于 file2 的行之前。diff 输出格式如图 III-10 所示。由逗号分隔的一对行表示一个行范围；diff 使用单个行号表示单行。

# 指令含义（将 file1 更改为 file2） || tabio ill-10

| | |
|---|---|
| line1 a line2,line3 > lines from file2 | 在 file1 的 line1 之后追加来自 file2 的行 |
| line1,line2 d line3 < lines from file1 | 删除 file2 中的 line1 到 line2 |
| line1,line2 c line3,line4 < lines from file1 | 将 file1 中的 line1 到 line2 更改为来自 file2 的行 |

# 示例

第一个示例展示了 diff 如何显示两个相似文件之间的差异：

```
$ cat m
aaaaa
bbbbb
cccc
```

```
$ cat n
aaaaa
cccc
```

```
$ diff m n
2d1
< bbbbb
```

文件 m 和 n 之间的差异是文件 m 的第二行 (bbbbb) 在文件 n 中缺失了。diff 显示的第一行 (2d1) 表示你需要删除文件 1 (m) 的第二行，使其与文件 2 (n) 相同。忽略指令行中字母后面的数字（如果你正在将 file2 转换为 file1，则这些数字将适用）。diff 显示的下一行以小于符号 (<) 开头，表示该行文本来自 file1。在这个示例中，你不需要这些信息——你只需要知道行号以便删除该行。

--side-by-side 选项和 diff 实用工具将输出宽度设置为 30 列（字符）时显示相同的输出。在输出中，小于符号指向 m 中多出的行，而 diff/sdiff 在 n 中留出一个空行，该额外行本所在的位置将使文件相同。

```
$ diff --side-by-side --width=30 m n
aaaaa aaaaa
bbbbb <
ccccc ccccc

$ diff -w 30 m n
aaaaa aaaaa
bbbbb <
ccccc ccccc
```

下一个示例使用相同的 m 文件和新文件 p，展示 diff 发出一个追加（append）指令：

```
$ cat p
aaaaa
bbbbb
rrrrrrr
ccccc
$ diff m p
2a3
> rrrrr
```

在这个示例中，diff 发出指令 2a3，表示你必须在 file m 的第 2 行之后追加一行，使其与 file p 相同。diff 显示的第二行表示该行来自 file p（该行以 > 开头，表示 file2）。在这个示例中，你需要这一行的信息；追加的行必须包含文本 rrrrr。

下一个示例再次使用 m，这次使用文件 r，展示 diff 如何指示需要更改的行：

```
$ cat r
aaaaa
-q
ccccc

$ diff m r
2c2
---
< bbbbb
> -q
```

两个文件之间的差异在第 2 行：File m 包含 bbbbb，file r 包含 -q。diff 先显示 2c2 表示你需要更改第 2 行。在指示需要更改后，diff 显示你必须将 file m 中的第 2 行 (bbbb) 更改为 file r 中的第 2 行 (-q)，使文件相同。三个字符表示 file1 中文本的结束。

--side-by-side 选项和 diff 实用工具将输出宽度设置为 30 列（字符）时显示相同的输出。在输出中，小于符号指向 m 中多出的行，而 diff/sdiff 在 n 中留出一个空行，该额外行本所在的位置将使文件相同。

```
$ diff --side-by-side --width=30 m n
aaaaa aaaaa
bbbbb <
ccccc ccccc

$ diff -w 30 m n
aaaaa aaaaa
bbbbb <
ccccc ccccc
```

下一个示例再次使用 m 文件和新文件 p，展示 diff 发出一个追加（append）指令：

```
$ cat p
aaaaa
bbbbb
rrrrrrr
ccccc
$ diff m p
2a3
> rrrrr
```

在这个示例中，diff 发出指令 2a3，表示你必须在 file m 的第 2 行之后追加一行，使其与 file p 相同。diff 显示的第二行表示该行来自 file p（该行以 > 开头，表示 file2）。在这个示例中，你需要这一行的信息；追加的行必须包含文本 rrrrr。

下一个示例再次使用 m，这次使用文件 r，展示 diff 如何指示需要更改的行：

```
$ cat r
aaaaa
-q
ccccc

$ diff m r
2c2
---
< bbbbb
> -q
```

两个文件之间的差异在第 2 行：File m 包含 bbbbb，file r 包含 -q。diff 先显示 2c2 表示你需要更改第 2 行。在指示需要更改后，diff 显示你必须将 file m 中的第 2 行 (bbbb) 更改为 file r 中的第 2 行 (-q)，使文件相同。三个字符表示 file1 中文本的结束。

# du

显示磁盘使用信息

du [options] | [path-list]

du（磁盘使用）实用工具报告目录（及其所有子目录和文件）或文件占用的磁盘空间。默认情况下，du 显示占用的 1024 字节块数。

# 参数

如果不带参数，du 显示工作目录及其子目录和文件的信息。path-list 指定你想获取信息的目录和文件。

# 选项

+ 不使用任何选项时，du 显示 path-list 中每个参数的总存储空间。对于目录，du 在递归列出每个子目录的总计后显示此。
--all -a 与目录目录的同时显示所有普通文件的空间。
--total -c 显示总计。
--human-readable -h 以 K（千字节）、M（兆字节）和 G（吉字节）块显示大小。
--kilobytes -k 以 1 千字节块显示大小。
--megabytes -m 以 1 兆字节块显示大小。
--one-file-system -x 仅报告与正在处理的参数相同文件系统的文件和目录。
--summarize -s 仅显示命令行指定的每个目录或文件的总计；不显示总计。

# 示例

以下 du 显示关于工作目录子目录的大小信息。最后一行包含工作目录及其子目录的总计。

```
$ du
26 /Postscript
4 /RCS
47 /XIcon
4 /Printer/RCS
12 /Printer
105
```

