
`zach:/d 2096450 193597 116333 92% /zach_d`

接下来，使用 `-l` 和 `-h` 选项调用 `df` 生成人类可读的文件系统列表。此列表所有大小以兆字节和 GB 给出。挂载的 NFS 文件系统（来自 `zach`）不可见：

| Filesystem | Size | Used | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hda12` | 1.4G | 52M | 1.3G | 4% | |
| `/dev/hda1` | 15M | 4.7M | 9.6M | 33% | `/boot` |
| `/dev/hda8` | 988M | 108M | 830M | 11% | `/free` |
| `/dev/hda9` | 988M | 30M | 908M | 3% | `/free2` |
| `/dev/hda10` | 1.1G | 1.9G | 971M | 7% | `/free3` |
| `/dev/hda5` | 3.8G | 1.9M | 1.8G | 52% | `/home` |
| `/dev/hda7` | 988M | 60k | 938M | 0% | `/tmp` |
| `/dev/hda6` | 2.4G | 805M | 1.5G | 34% | `/usr` |

下一个示例使用 1 兆字节块显示关于 `/free2` 分区的信息。

| Filesystem | 1M-blocks | Used | Available | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `/dev/hda9` | 988 | 30 | 908 | 3% | `/free2` |

最后一个示例以人类可读的格式显示 NFS 文件系统的信息：

| Filesystem | Size | Used | Avail | Use% | Mounted on |
| :--- | :--- | :--- | :--- | :--- | :--- |
| `zach:/c12` | 2.0G | 1.7G | 278M | 86% | `/zach_c` |
| `zach:/d` | 2.0G | 1.8G | 157M | 92% | `/zach_d` |

# `diff`

显示两个文件之间的差异

```
diff [options] file1 file2

diff [options] file1 directory

diff [options] directory file2

diff [options] directory1 directory
```

`diff` 工具显示两个文件之间的行间差异。默认情况下，`diff` 将差异显示为指令，你可以使用这些指令编辑其中一个文件使其与另一个相同。

## 参数

`file1` 和 `file2` 是 `diff` 所处理的文件路径。当用目录参数替换 `file2` 时，`diff` 在 `directory2` 中查找与 `file1` 同相同名称的文件。同样地，当用目录参数替换 `file1` 时，`diff` 在 `directory1` 中查找与 `file2` 同相同名称的文件。你可以用连字符 `-` 替换 `file1` 或 `file2` 以使 `diff` 使用标准输入。当你指定两个目录参数时，`diff` 会比较 `directory1` 中的所有文件与 `directory2` 中具有相同文件名的文件。

## 选项

- `--brief` `-q` 不显示文件内行之间的差异。相反，`diff` 仅报告文件存在差异。
- `--context [lines]` `-C lines` `-c` 显示两个文件中差异的部分，包括差异行周围的行（默认为 3 行）以显示上下文。`file1` 中缺少但 `file2` 中有的行前有 `-`，`file2` 中额外的行前有 `+`，在两个文件中版本不同的行标记为 `!`。当行之间的距离在三行以内时，它们会在输出中分组。
- `--ed` `-e` 为 `ed` 编辑器创建一个脚本，该脚本将编辑 `file1` 使与 `file2` 相同，并发送到标准输出。如果你重定向输入到 `ed`，可以在脚本末添加 `w`（写入）和 `q`（退出）指令。当你使用 `--ed` 时，`diff` 会按反序显示更改——文件末尾的更改在顶部更改之前列出。这可以防止早期更改在脚本作为 `ed` 输入时影响后续更改。例如，如果删除了顶部的某行，脚本中后续行号将错误。

# 1150 `diff`

`--ignore-blank-lines` `-B` 忽略仅涉及空行数的差异。

`--ignore-case` `-i` 在比较文件时忽略大小写引起的差异。

`--ignore-space-change` `-b` 忽略行尾的空白（空格和制表符），并将其他空白字符串视为等同。

`--p` 显示每个更改位于哪个函数中。

`--recursive` `-r` 当使用 `diff` 比较两个目录中的文件时，使比较扩展到子目录。

`--side-by-side` `-y` 以并排格式显示输出。此选项生成的输出与 `sdiff` 相同。使用此选项时配合 `--width=columns` 选项使用。

`--unified[lines=n]` `-u` 使用更易读的统一输出格式。更多详细信息和示例请参阅第 67 页关于 `diff` 的讨论。`lines` 是上下文的行数，默认值为三行。

`-w whitespace` 在比较文件时忽略空白字符符。

`--width=columns` `-w` 设置 `diff` 显示输出列时使用的列数。此选项配合 `--side-by-side` 选项非常。`sdiff` 工具使用小写 `w` 来执行相同的功能：`-w columns`。

# 注意事项

`diff` 实用类似于 `sdiff`，但输出可能更容易读。`diff` 的 `--side-by-side` 选项产生的输出与 `sdiff` 相同。如果你尝试 `sdiff`，请确保使用 `-w columns` 选项，该选项将页面宽度设置为列数（默认为 130）。请参见“示例”部分并参考 `diff` 和 `diff into` 页面获取更多信息。

# 讨论

当你使用任何选项使用 `diff` 时，它会产生一系列添加 `a`、删除 `d` 和更改 `c` 指令。每行指令后面都是你需要添加、删除或更改的文件中的行。小于符号 `<` 位于 `file1` 的行之前。大于符号 `>` 位于 `file2` 的行之前。`diff` 输出格式如图 III-10 所示。由逗号分隔的一对行表示一个行范围；`diff` 使用单个行号表示单行。

# 指令含义（将 `file1` 更改为 `file2`） || tabio ill-10

| | |
|---|---|
| `line1 a line2,line3 > lines from file2` | 在 `file1` 的 `line1` 之后追加来自 `file2` 的行 |
| `line1,line2 d line3 < lines from file1` | 删除 `file2` 中的 `line1` 到 `line2` |
| `line1,line2 c line3,line4 < lines from file1` | 将 `file1` 中的 `line1` 到 `line2` 更改为来自 `file2` 的行 |

# 示例

第一个示例展示了 `diff` 如何显示两个相似文件之间的差异：

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

文件 `m` 和 `n` 之间的差异是文件 `m` 的第二行 `bbbbb` 在文件 `n` 中缺失了。`diff` 显示的第一行 `2d1` 表示你需要删除文件 1 `m` 的第二行，使其与文件 2 `n` 相同。忽略指令行中字母后面的数字（如果你正在将 `file2` 转换为 `file1`，则这些数字将适用）。`diff` 显示的下一行以小于符号 `<` 开头，表示该行文本来自 `file1`。在这个示例中，你不需要这些信息——你只需要知道行号以便删除该行。

`--side-by-side` 选项和 `diff` 实用工具将输出宽度设置为 30 列（字符）时显示相同的输出。在输出中，小于符号指向 `m` 中多出的行，而 `diff/sdiff` 在 `n` 中留出一个空行，该额外行本所在的位置将使文件相同。

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

下一个示例使用相同的 `m` 文件和新文件 `p`，展示 `diff` 发出一个追加（append）指令：

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
