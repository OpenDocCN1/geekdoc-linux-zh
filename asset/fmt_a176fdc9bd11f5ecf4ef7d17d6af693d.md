
```
% tr --complement "A \n" "Z" < tr.dat
AZZ ZZZ ZZZ
AZZ ZZZ ZZZ
AAA ZZZ ZZZ
```

# tr 命令

`--squeeze-repeats` 选项在本章的示例中以及第 12 章“自定义工具”中反复出现，因此这里只给出两个短示例：

```
% tr --squeeze-repeats "BC" < tr.dat
ABC DEF GHI
ABC DEF GHI
AAA B C
```

只有 `CHARSET1` 中列出的字符才会受到 `--squeeze-repeats` 选项的影响，除非同时也进行了翻译。进行翻译时，只有 `CHARSET2` 中列出的字符会受到影响——如下：

```
% tr --squeeze-repeats "ZZ" < tr.dat
AZ DEF GHI
AZ DEF GHI
AAA Z Z
```

第一行和第二行受到了影响，因为字符序列 `ABC` 首先被翻译为 `AZZ`，然后两个 `Z` 被压缩成一个。

# true 命令

摘要

`true` 以值 `0` 退出，表示成功。

语法

`true`

# tty 命令

摘要

`tty` 显示连接到 `STDIN` 的终端名称。

语法

`tty [options]`

描述：

`tty` 是简单的 Unix 命令之一——它只是让你知道当前进程使用哪个终端作为 `STDIN`。有时，你可能只需要知道 `STDIN` 是否连接到了 tty（`STDIN` 可能被重定向到了文件）。在这种情况下，必须检查退出值：

- `0`-`STDIN` 是 tty。
- `1`-`STDIN` 不是 tty。
- `2`-传递给 `tty` 命令的参数错误。
- `3`-发生了写入错误。

表 9.39 显示 `tty` 命令的选项。

# 表 9.39 tty 命令的选项

| 选项 | 描述 |
| --- | --- |
| `--help` | 显示帮助信息。 |
| `-s` 或 `--silent` 或 `--quiet` | 停止 `tty` 输出。当只需要退出值时使用此选项。 |
| `--version` | 显示 `tty` 的版本信息。 |

# type 命令

摘要

`type` 显示系统信息。

语法

`type [options] name [name...]`

描述：

`type` 命令默认显示命令行上每个 `NAME` 的信息。有些命令是哈希（例如 `ls`），这意味着 Bash 已经知道命令的位置，不需要 `PATH` 变量。

`type` 有三个选项：

- `-all` 选项显示包含 `NAME` 可执行文件的目录。当未使用 `-path` 选项时，包含别名和函数。

- `-type` 选项根据命令行类型显示别名、关键字、内置或文件。关键字是 shell 保留字，如 `for` 和 `while`。“内置”是指 Bash 内部命令，如 `type` 本身。如果找不到 `NAME`，则不显示且退出值为 `1`，否则退出值为 `0`。

- `-path` 选项显示将执行 `NAME` 命令的文件名，如果没有与 `NAME` 关联的文件，则不显示。

# uname 命令

摘要

`uname` 显示系统信息。

语法
```
uname [options]
```

描述：

`uname` 命令默认显示操作系统名称。在我的系统上显示如下：

```
% uname
Linux
```

这个结果可能看起来并不精彩。然而，如果你在多个系统上工作，可能需要知道操作系统以便运行哪些命令以及使用哪些目录。表 9.40 列出了 `uname` 命令的选项。

# 表 9.40 uname 命令的选项

| 选项 | 描述 |
| --- | --- |
| `-a` 或 `--all` | 显示 `uname` 知的所有信息。 |
| `--help` | 显示帮助信息。 |
| `-m` 或 `--machine` | 显示硬件类型。 |
| `-n` 或 `--nodename` | 显示计算机的网络主机名。 |

# 表 9.40 uname 命令的选项（续）

| 选项 | 描述 |
| --- | --- |
| `-r` 或 `--release` | 显示操作系统的发布信息。 |
| `-s` 或 `--sysname` | 显示操作系统的名称。如果没有指定选项，默认执行。 |
| `-v` | 显示操作系统的版本。 |
| `--version` | 显示版本信息。 |

`uname --all` 命令的输出如下：

`Linux localhost.localdomain 2.0.32#1`

`Wed Nov 19 00:06:45 EST 1997`

# uniq 命令

摘要

`uniq` 从排序后的输入中删除重复行。

语法

`uniq [options] [input_file] [output_file]`

描述：

`uniq` 命令从 `STDIN` 或 `INPUT_FILE` 读取，过滤信息，然后输出到 `STDOUT` 或 `OUTPUT_FILE`。不同的过滤动作由表 9.41 列出的选项控制。

# 表 9.41 uniq 命令的选项

| 选项 | 描述 |
| --- | --- |
| `-c` 或 `--count` | 显示每行的重复次数以及行本身。每行的计数最小为 `1`。 |
| `-d` 或 `--repeated` | 仅显示重复行。 |

# 表 9.41 uniq 命令的选项（续）

| 选项 | 描述 |
|---|---|
| `-f NUM_FIELDS` 或 `--skip-fields=NUM_FIELDS` 或 `-NUM_FIELDS` | 在检查输入行的唯一性之前跳过 `NUM_FIELDS` 个字段。字段由任意数量的空间和制表符分隔。如果同时使用 `--skip-fields` 和 `--skip-chars` 选项，先跳过字段。 |
| `--help` | 显示帮助信息。 |
| `-s NUM_CHARS` 或 `--skip-chars=NUM_CHARS` 或 `+NUM_CHARS` | 在检查输入行的唯一性之前跳过 `NUM_CHARS` 个字符。如果同时使用 `--skip-fields` 和 `--skip-chars` 选项，先跳过字段。 |
| `-u` 或 `--unique` | 仅显示唯一行。这意味着重复行不会发送到输出文件。 |
| `-w NUM_CHARS` 或 `--check-chars=NUM_CHARS` | 指定检查唯一性的字符数。通常检查整行（跳过部分除）。 |
| `--version` | 显示版本信息。 |

```bash
% uniq uniq.dat
01 12345 67890
02 12345 67890
03 12345 22222 <- 注意重复的 03 行已
04 11111 22222 <- 被删除。
```

`-unique` 选项会移除所有重复或相同行的痕迹：

```bash
% uniq -unique uniq.dat
01 12345 67890 <- 注意所有的 03 行都
02 12345 67890 <- 被删除了。
04 11111 22222
```

`-repeated` 选项与 `-unique` 选项相反。它对每个重复的行只输出一个副本：

```bash
% uniq -repeated uniq.dat
03 12345 22222
```

当你需要 `uniq` 忽略输入行的开头时，可以使用 `--skip-fields` 选项：

```bash
% uniq --skip-fields=1 uniq.dat
01 12345 67890
03 12345 22222
04 11111 22222
```

`-check-chars` 选项限制了检查唯一性的字符数：

```bash
% uniq --skip-fields=1 --check-chars=5 uniq.dat
01 12345 67890
04 11111 22222
```

行 `03` 没有被输出，是因为 `01` 和 `03` 在第二个字段中具有 `12345`，且 `--check-chars` 选项将唯一性检查限制在了第二个字段。

## wc 命令

### 概要

`wc` 用于统计文件中的字符数、单词数和行数。

### 语法
```
wc [options] [filename...]
```

## wc 命令

描述：

`wc` 命令在需要快速确定文件大小时是一个实用的工具。如果命令行上没有指定文件名，`wc` 将从 `STDIN` 读取。当指定了多个文件时，输出中会附加一行带有累计计数。

默认情况下，会显示字节、单词和行的总数。但是，你可以使用表 9.42 所示选项进行更具选择性的操作。通过组合选项，你可以显示任何计数组合。

### 表 9.42 wc 命令的选项

| 选项 | 描述 |
| :--- | :--- |
| `-c` or `--bytes` or `--chars` | 仅显示文件的字节数。 |
| `-w` or `--words` | 仅显示文件的单词数。单词被定义为由空白字符分隔的字母。 |
| `-l` or `--lines` | 仅显示文件的行数。 |
| `--help` | 显示帮助信息。 |
| `--version` | 显示版本信息。 |

## who 命令

### 概要
