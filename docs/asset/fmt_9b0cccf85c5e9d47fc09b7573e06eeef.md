
# man 显示命令的文档

语法：`man [options][section] command`
`man -k keyword`

## 摘要

`man` 实用程序为 Linux 系统上的可用命令提供在线文档。除了用户命令外，许多其他命令也有文档可用。

`section` 参数使 `man` 将搜索限制在指定的章节。

`-k keyword` 显示包含该字符串的帮助页。该选项等同于 `apropos` 命令（页 50，注：此处原文 page 50 似为笔误）。

`-M path` 使 `man` 在指定的目录中查找，而不是在默认位置。

`-t` 将 PostScript 页面格式化。

`man` 的参数并不总是命令名。例如，`ascii` 命令列出了所有的 ASCII 字符及其各种表示形式。

# man 795

`man(1)` `man(1)`

### 名称
`man` - 格式化并显示在线帮助页
`manpath` - 确定 man 页的用户搜索路径

# 概要
`man [-adfhtkww] [-p string] [-C config_file] [-M path] [-P pager] [-S section_list] [section] name`

### 描述
`man` 格式化并显示在线帮助页。此版本识别 `MANPATH` 和 `PAGER` 环境变量。

下面的示例显示了如何使用 `man` 工具查找与特定主题相关的帮助页。在这种情况下，将显示所有包含字符串 `latex` 的帮助页页头。所有这些帮助页都属于第 1 节。

```
$ man -k latex
mslatex (1) - 结构化文本格式化和排版
lacheck (1) - LaTeX 文档的一致性检查器
latex(1) - 结构化文本格式化和排版
slit (1) - 制作 LaTeX 幻灯片
transfig (1) - 为便 LaTeX 图形创建 Makefile
(END)
```

使用 `-k` 选项输入的关键字搜索是不区分大小写的。虽然在命令行上输入的关键字是小写的，但 `transfig` 的页头包含大小写的 LaTeX 字符串。

# mesg

| `mesg` | 启用/禁用接收消息 |
| 语法: | `mesg [-y|-n]` |

### 总结
`mesg` 工具启用或禁用接收使用 `write` 或 `talk` 工具的人所发送的消息。当你不带任何参数调用 `mesg` 时，它会告知你消息是否已启用或禁用。

### 选项
- `-n` no 禁用接收消息。
- `-y` yes 启用接收消息。

### 注意事项
在大多数系统中，当你首次登录时，消息是启用的。某些工具（如 `pr`）在向终端发送输出时会自动禁用消息。

# 示例
下面的示例演示了如何禁用消息：

```
$ mesg -n
```

接下来的示例在不带选项的情况下调用 `mesg`，并验证你已禁用了消息：

```
$ mesg

is n
```

# mkdir 创建目录

**语法：** `mkdir [option] directory-list`

### 总结
`mkdir` 工具创建一个或多个目录。

### 参数
`directory-list` 包含 `mkdir` 创建的一个或多个目录的路径名。

### 选项
- `-m mode` 将权限设置为 `mode`。你可以使用符号形式或八进制数字来表示模式。有关 `chmod` 的更多信息请参考第 676 页。
- `- (-p)` 创建你想要创建的目录路径中任何不存在的目录。

### 注意事项
你必须对正在创建的目录的父目录具有写入和搜索（执行）权限。`mkdir` 工具创建的目录包含标准的不可见条目 `.`（代表目录本身）和 `..`（代表父目录）。

# 示例
以下命令在工作目录下创建一个名为 `accounts` 的子目录，并在 `accounts` 的子目录下创建一个名为 `prospective` 的子目录：

下面，在不更改工作目录的情况下，同一用户在 `accounts` 目录内创建了另一个子目录：

```
$ mkdir accounts/existing
```

接下来，用户将工作目录更改到 `accounts` 目录并创建一个子目录：

```
$ cd accounts

$ mkdir closed
```

最后一个示例显示用户创建了另一个子目录。这次使用 `--mode` 选项删除了组组和其他人的访问权限。

```
$ mkdir --mode go=accounts/past_due
```

# Mtools
在文件和目录上使用 DOS 风格命令

| 语法 |
| --- |
| `mcd [directory]` |
| `mcopy [options] file-list target` |
| `mdel file-list` |
| `mdir [-w] directory` |
| `mformat [options] device` |
| `mtype [options] file-list` |

### 总结
这些工具模拟 DOS 命令并操作 Linux 文件或 DOS 文件。`mcopy` 工具提供了一种在 Linux 文件系统和 DOS 磁盘之间移动文件的简单方法。所有命令的默认驱动器为 `/dev/fd0` 或 `a:`。

| 工具 | 功能 |
| --- | --- |
| `mcd` | 更改 DOS 磁盘上的目录 |
| `mcopy` | 将 DOS 文件从一个目录复制到另一个 |
| `mdel` | 删除 DOS 文件 |
| `mdir` | 列出 DOS 目录的内容 |
| `mformat` | 向磁盘添加 DOS 格式信息 |
| `mtype` | 显示 DOS 文件的内容 |

### 参数
用于 `mcd` 和 `mdir` 的 `directory` 参数必须是 DOS 磁盘上的目录名称。
用于 `mcopy` 和 `mtype` 的 `file-list` 参数是一个一个或多个由空格分隔的文件名列表。
用于 `mcopy` 的 `target` 是普通文件或目录的名称。如果你给 `mcopy` 提供包含多个文件名的 `file-list`，则 `target` 必须是目录名称。
用于 `mformat` 的 `device` 参数是待格式化磁盘驱动器的 DOS 驱动器号（例如，`A`）：

### 选项
- `mcopy` 工具接受以下内容：
- `-m modification` 在复制文件时保留文件的修改时间。
- `-n` 自动替换现有文件而不进行询问。通常 `mcopy` 在覆盖文件之前会请求验证。

# Mtools 799
- `-t` 将 DOS 文本文件转换为供 Linux 系统使用。DOS 文本文件的行以 RETURN-NEWLINE 字符对结束。此选项导致 `mcopy` 在复制时移除 RETURN 字符。

`mdir` 工具接受以下选项：
- `-w wide` 仅显示文件名并在每行尽可能显示多个文件名。默认情况下，`mdir` 在单独行列出每个文件的信息，显示文件名、大小和创建时间。

`mformat` 工具接受以下选项：
- `-h` 将磁盘视为具有 `heads` 个面。
- `-l` 为新格式化的磁盘设置卷。
- `-s` 将磁盘视为具有 `s` 个扇区。

`mtype` 工具接受以下选项：
- `-t` 与 `mcopy` 的 `-t` 选项类似，将 RETURN 字符替换为单个 NEWLINE 字符。

# 讨论
这些工具模拟了对应的工具，但不精确匹配 DOS。例如，使用星号 (`*`) 匹配所有文件名是不可能的。

### 注意事项
如果你的内核支持 DOS 文件系统，可以使用这些工具来挂载 DOS 磁盘。使用正斜杠 (`/`) 或反斜杠 (`\`) 来区分文件名。需要转义反斜杠以防止 shell 在将其传递给工具之前解析它。

# 示例
在第一个示例中，使用 `mdir` 工具检查 DOS 磁盘的内容：

```
$ mdir

Volume in drive A

Directory for A/:
```

| | | |
|---|---|---|
| ACAD | LIF | 59904 |
| CADANCE | LIF | 40560 |
| CHIP | EXE | 2209 |
| DISK | ID | 31 |
| GENERIC | LIF | 836 |
| INSTALL | COM | 45277 |
| INSTALL | TXT | 11029 |
| KDINEXT | EXE | 11029 |
| LOTUS | LIF | 44099 |
| PCAD | LIF | 17846 |
| READIED | EXE | 17261 |
| README | TXT | 9853 |
| UTILITY | LIF | 51069 |
| WORD | LIF | 16817 |
| WP | LIF | 57992 |
| 15 File(s) | | 599040 bytes free |

接下来，使用 `mcopy` 将 `*.TXT` 文件从 DOS 磁盘复制到 Linux 文件系统的工作目录。由于只有一个扩展名为 `.TXT` 的副本，因此复制了一个文件。TXT 文件通常在 DOS 下使用，使用 `-o` 删除行尾不必要的 RETURN 字符。歧义的文件引用 = 在命令行上进行转义，以防止 shell 在将参数传递给工具 之前尝试扩展它。`mcopy` 工具在给定模式 `*.txt` 时可以找到 `README.TXT`，因为 DOS 不区分文件名中的大小写。

```
$ mcopy -t a:\*.txt

Copying README.TXT
```

最后，使用 `mformat` 格式化 DOS 软磁盘。如果磁盘没有进行过低级格式化，你需要在执行以下命令之前使用 `dformat`。格式化后用 `mdir` 检查显示它是空的。

```
$ mformat a:

$ mdir a:

Volume in drive A has no label

Directory for A/:
```

```
File "* not found
```
