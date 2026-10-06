
# 755 gzip

| 语法 | `gzip [options] [file-list]` |
| | `gzip [options] [file-list]` |

### 摘要
`gzip` 实用程序压缩文件，减少磁盘空间需求以及计算机之间传输文件所需。当 `gzip` 压缩一个文件时，它会在文件名后添加扩展名 `.gz`；压缩文件会创建 `fname.gz` 并删除原始文件。要恢复 `fname`，使用带有参数 `fname.gz` 的 `gzip` 命令。`.gz` 扩展是可选的。

## 参数
`file-list` 是一个或多个要压缩或解压的文件列表。如果目录带有 `--recursive` 选项出现在 `file-list`，`gzip` 会发出错误消息并忽略该目录。使用 `--recursive` 选项，`gzip` 会递归地压缩目录内的所有文件（以及所有子目录）。
如果 `file-list` 为空或存在特殊选项，`gzip` 从标准输入读取。使用 `--force` 选项（见下文）允许标准输入来自终端，并导致 `gzip` 写入标准输出。

> 本节中的信息对于 `gzip` 同样。

## 选项
- `--decompress` or `--uncompress`
- `(-d)` 解压缩用 `gzip` 压缩的文件。此选项配合 `gzip` 使用等同于 `gzip` 命令。
- `--fast` or `--best` `(-#)` 允许你控制压缩速度与压缩率之间的平衡。在 `---#` 形式中，将 `#` 替换为 1 到 9 之间的数字；级别 1 是最快压缩，级别 9 是最好的。`gzip` 采用的默认级别是 6。`--fast` 和 `--best` 分分别是 `-1` 和 `-9` 的同义词。
- `--force` `(-f)` 即使文件已存在、有多个链接或直接来自终端也强制压缩。
- `--recursive` `(-r)` 对于 `file-list` 中的目录，进入目录。配合 `gzip` 使用，递归地解压文件。
- `--stdout` `(-c)` 将压缩或解压的结果写入标准输出，而不是覆盖原始文件。

# 756 gzip

- `--verbose` `(-v)` 对于每个文件显示文件名、压缩后的文件名以及压缩率。配合 `gzip` 显示类似信息。

### 讨论
大多数文件在压缩后会变小。极少数文件会变大，但只有一点。文本文件在压缩后通常会减少 60% 到 70%。文件的属性如所有者、权限和修改时间在压缩时保持完好。

如果压缩文件已存在，`gzip` 会报告并请求确认覆盖现有文件。如果文件有多个链接，`gzip` 会发出错误消息并终止。

### 注意事项
除了 `gzip` 格式，`gzip` 还识别几种压缩格式。

要查看压缩后变大的文件示例，比较压缩过一次的大小。

以下相关工具允许你查看和操作压缩文件。这些工具都不会更改操作的文件。

### `zcat file-list`
类似于 `cat`，包含用 `gzip` 解压的压缩文件。

### `zdiff [options] file1 [file2]`
类似于 `diff`，`file1` 和 `file2` 根据需要用 `gzip` 解压。如果你省略 `file2`，`zdiff` 将比较 `file1` 与其压缩版本。

### `zless file-list`
类似于 `less`，只是每个显示。

### 示例
第一个示例中 `gzip` 压缩了两个文件。接下来解压了其中一个文件。当文件被压缩和解压时，其大小会变化，但修改时间保持不变。

```bash
$ ls -l

total 175

-rw-rw-r-- 1 alex group 33557 Jul 20 17:32 patch-2.0.7

-rw-rw-r-- 1 alex group 143258 Jul 21 17:32 patch-2.0.8

$ gzip *
```

```bash
$ ls -l

total 5

-rw-rw-r-- 1 alex group 9693 Jul 20 17:32 patch-2.0.7.gz

-rw-rw-r-- 1 alex group 40426 Jul 20 17:32 patch-2.0.8.gz

$ gzip patch-2.0.7.gz

$ ls -l

total 75

-rw-rw-r-- 1 alex group 33557 Jul 20 17:32 patch-2.0.7.gz
```

在下一个示例中，使用 `cpio` 归档 Jenny 的家目录文件。归档在写入磁带之前用 `gzip` 压缩。有关使用 `cpio` 的更多信息请见第 694 页。

```bash
$ find /home/jenny -depth -print | cpio -oBm | gzip >/dev/ftape
```

# 758 head

| `head` | 显示文件的开头 |
| :--- | :--- |
| 语法 | `head [options] [file-list]` |

# 摘要

`head` 工具显示文件的开头（头部）。它从你在命令行上指定的一个或多个文件或从标准输入读取输入。

## 参数

`file-list` 包含 `head` 显示的文件路径名。如果你指定了多个文件，`head` 在显示前几行之前会显示每个文件的文件名。如果你没有指定任何文件，`head` 将从标准输入读取输入。

# 选项 `[n[u]]`

- `--bytes` 按字节（字符）计数。`n` 是可选的非零整数。`u` 是可选的度量单位，可以是 `b`（512 字节块）、`k`（1024 字节或 1 KB 块）或 `m`（1 MB 块）。如果你包含了度量单位，`head` 将按该单位计数代替字节计数。
- `--lines[+n]` `(-n)` 按行计数（默认值）。你可以使用 `-n` 指定行数，而无需使用 `lines` 关键字。
- `--quiet` `(-q)` 当你在命令行上指定了多个文件名时，抑制头部信息。
- `--help` 总结 `head` 的用法。

# 注意事项

`head` 工具默认显示十行。

# 示例

示例基于以下十一个行的文件：

```
$ cat eleven

line one

line two

line three

line four

line five

line six

line seven

line eight

line nine

line ten

line eleven
```

在此示例中，`head` 显示了 `eleven` 文件的前十行（无参数）：

```
$ head eleven

line one

line two

line three

line four

line five

line six

line seven

line eight

line nine

line ten
```

下一个示例显示文件的前三行（`第 3 行`）：

```
$ head --lines 3 eleven

line one

line two

line three
```

接下来的示例等同于上述示例：

```
$ head -3 eleven

line one

line two

line three
```

下一个示例显示文件中的前六个字符（`--bytes 6`）：

```
$ head --bytes 6 eleven

line o
```

# 761 ispell

| `ispell` | 检查文件的拼写错误 |
| :--- | :--- |
| 语法 | `ispell [options] file-list` 或 `ispell [options] -l` |

# 摘要

`ispell` 工具根据标准字典以及可选的个人字典检查文件中的单词。连续的小写和大写字母序列被视为单词，尽管单词的定义可以扩展到包含其他字符。

`ispell` 工具通常在*交互模式*下使用，它会显示每个拼写错误的单词以及你可以采取的操作菜单。选择包括接受该单词、将单词插入个人字典以及替换单词。在最少使用的*列表模式*中，`ispell` 从标准输入读取并向标准输出写入。当你想要将输出重定向为纯粹的拼写错误单词列表（每行一个）时，列表模式非常适用。

## 参数

如果你给 `ispell` 一个带有 `file-list` 的命令，`ispell` 将以交互模式运行并处理每个文件。在你处理文件时，屏幕顶部会显示每个文件的名称。如果你使用 `-l` 选项，`ispell` 将以列表模式运行。在列表模式下，输入来自标准输入，输出去标准输出。列表模式中所有选项在交互模式下也可用；与交互模式相关的选项将被忽略。

## 选项

许多选项的默认值是在安装 `ispell` 时确定的，不同系统之间可能会不同。然而，每当你在命令行上提供选项，它都会覆盖默认值。

# 调用列表模式的选项

- `-l` 从标准输入读取输入并将拼写错误单词列表发送到输出，每行一个。输出中单词的顺序是它们在标准输入中出现的顺序。

# 交互模式选项

- `-b` 如果对输入文件进行了任何更改，则创建一个扩展名为 `.bak` 的备份文件。
- `-x` 不创建备份文件。
- `-L` 在显示包含拼写错误单词的输入行时，包含 `numlines` 行的上下文。
- `-M` 在屏幕底部显示命令的单行摘要。
- `-N` 不在屏幕底部显示命令摘要。
- `-S` 将建议的替换单词列表按正确概率排序，而不是按字母顺序。

# 两种模式通用的选项

- `-d filename` 使用名为 `filename` 的字典文件。
- `-p filename` 使用名为 `filename` 的个人字典文件。
- `-w addchars` 除字母字符串外，还对包含 `addchars` 中字符的字符串进行字典检查。当输入文件包含技术字符或其他可能仅在扩展或补充字典中找到字符串，或者用于构建个人字典时，此选项有用。
- `-W wordlen` 不检查长度小于或等于 `wordlen` 的单词。当你检查许多不在字典中的短字符串（如缩写）时，使用此选项。

# 讨论

当 `ispell` 检查文件中的单词时，它会搜索标准字典来定位每个单词。如果未找到单词，如果在命令行上指定了个人字典，它会搜索个人字典。在列表模式下，`ispell` 将单词写入标准输出。在交互模式下，它会显示一个屏幕信息并等待你的指令。这允许你控制 `ispell` 如何处理该单词，并包含帮助你的信息。屏幕顶部显示潜在的拼写错误单词和输入文件名。屏幕的第一行显示潜在的拼写错误单词和输入文件名。如果字典中有相似单词，会给出数字供选择：

| 命令 | 效果 |
| :--- | :--- |
| SPACE | 不采取操作并进入下一个拼写错误单词 |
| `<number>` | 选择建议的数字替换拼写错误 |
| R | 使用屏幕输入的单词替换拼写错误 |
| A | 在整个 ispell 会话中接受拼写错误 |
| I | 将单词插入个人字典 |
| L | 对屏幕上的单词进行字典检查 |
| U | 不区分大小写将单词插入个人字典 |
| q | 退出 ispell 会话，忽略对文件的更改 |
| x | 保存已修复的文件并进入下一个文件 |
| ? | 显示命令表和摘要 |

# 762 ispell

此表中的项目出现在屏幕底部的菜单中（除非使用 `-N` 选项）。还会显示包含潜在拼写错误（已高亮）的行及其上下文。

如果替换了单词且没有给出 `q` 命令，`ispell` 会创建一个扩展名为 `.bak` 的备份文件。`-x` 选项禁用此行为。

## 注意

某些版本的 UNIX 使用 `spell` 工具。在没有选项的情况下，`spell` 将拼写错误列表写入标准输出。使用 `ispell` 的等效命令是：

```
$ ispell -l <inputfile
```

`ispell` 工具不是寻找拼写错误的万能方法。它也不检查用错误的正确单词（例如下方倒数第二个示例中的 `quiet`）。
`ispell` 工具设计用于通过管道与其他程序交互。请参阅 `ispell` 手页中的 `-a` 和 `-A` 选项获取更多信息。

# 示例

以下示例使用 `ispell` 更正 `check` 文件的拼写。

```
$ cat check

Here's a document for teh ispell utility

to check. It obviously needs proving

quiet badly.
```

第一个示例未使用选项运行 `ispell`。第一个拼写错误单词 `teh` 的屏幕显示所示。屏幕底部是此时可以给命令菜单。这七个数字都与拼写错误单词略有不同。

```
$ ispell check

File: check

teh

0: eh

1: tea

2: tech

3: tee

4: ten

5: te

6: Tex

7: the

.

Here's a document for teh ispell utility

[SP] <number> R)epl A)cept I)nsert L)ook U)ncap Quit e(X)it or ? for help
```

下一个示例使用了 `-S` 选项，以便建议的替换按可能的正确概率排序。

```bash
$ ispell -S check

the File: check

0: tech

1: the

2: eh

3: tea

4: tee

5: ten

6: Tex

7: TeX
```

这里是关于 ispell 程序的文档

`<number>` R)epl A)cept I)nsert L)ookup U)ncap Quit e(X)it 或输入 ? 获取帮助
下一个示例使用列表模式显示拼写错误单词的列表。单词 "quiet" 不在列表中——它没有被正确使用，但它的拼写是正确的。

```
$ ispell -l < check

teh

ispell utility

obviously
```

最后一个示例也使用了 `ispell` 命令的第二种形式。它展示了通过单条命令检查单词拼写的快速快捷方法。提供给 `ispell` 的输入是拼写错误的，因此 `ispell` 将其写入标准输出。

```bash
$ echo seperate | ispell -1

seperate
```

# 764 kill

| | |
| :--- | :--- |
| `kill` 终止一个进程 | 语法: `kill [option] PID-list` |
| `kill -l` | |

## 总结

`kill` 工具通过向进程发送信号来终止一个或多个进程。默认，`kill` 发送软件终止信号（信号数 15），尽管有一个选项允许你发送不同的信号。该进程必须属于执行 `kill` 的用户，但超级用户（Superuser）可以终止任何进程。`kill` 工具在终止进程时会显示一条消息。

在命令的第二种形式中，`kill` 会显示所有可用信号名称的列表。你可以在 `kill` 工具中使用信号数字或信号名称，尽管信号名称更具具描述性。

## 参数

`PID-list` 包含 `kill` 要终止的进程的进程标识符 `PID` 数字。

## 选项

你可以在 `PID-list` 之前指定一个以连字符开头的信号数字或名称作为选项，以便 `kill` 向进程发送你指定的信号。

## 注意事项

当你启动后台进程时，shell 会显示该后台进程的 PID 数字。你也可以使用 `ps` 工具来确定 PID 数字。

如果软件终止信号没有终止进程，请尝试使用 KILL 信号（信号数 9）。进程可以选择忽略除 KILL 以外的任何信号。

`kill` 工具内置于 `bash`、`tcsh` 和 `zsh` 中。当你使用这些 shell 之一时，可以使用作业标识符代替 `PID-list`。作业标识符由一个百分号 `%` 后跟一个作业数或唯一标识作业的字符串组成。`kill` 的内置版本还允许你通过名称而非数字来指定信号。你可以使用 `kill -l` 命令列出信号名称。

要终止由当前登录进程启动且已退出操作系统的进程，请执行命令 `kill -9 0`。

## 警告

如果你以超级用户登录并运行 `kill -9 0`，你将导致系统崩溃。

## 示例

第一个示例显示了命令行执行文件 `compute` 作为后台进程，并由 `kill` 工具将其终止：

```bash
$ compute &

[2] 259

$ kill 259

$

[2] + terminated compute --
```

下一个示例显示了 `ps` 工具确定了运行名为 `xprog` 程序的后台进程的 PID 数字，以及 `kill` 工具使用 KILL 信号终止了 `xprog`：

```bash
$ ps

PID TTY STAT TIME COMMAND

116 1 S N 0:00 -zsh

128 1 S N 0:00 xinit /home/alex/.xinitrc --

137 1 S N 0:01 fwwm

138 p0 S N 0:00 -zsh

161 p0 S N 0:10 xprog

262 p0 R N 0:00 ps

$ kill -KILL 161 ps

[1] + killed xprog

$
```
