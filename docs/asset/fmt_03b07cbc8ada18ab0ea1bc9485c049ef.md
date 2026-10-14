
你可以配合 `grep` 命令使用的选项包括：

# 表 1-20 grep 命令的选项

| 选项 | 描述 |
| :--- | :--- |
| -i | 忽略大小写。 |
| -l | 只显示包含搜索字符串的文件名。 |
| -r | 递归搜索整个目录树。 |
| -v | 显示所有不包含搜索字符串的行。 |
| -n | 显示行号。 |
| -h | 不显示文件名。 |

### 使用正则表达式

正则表达式是由元字符、普通字符和数字（也称为“字面量”）组成的字符串。在正则表达式的语境下，元字符是指那些不代表自身而具有特殊含义的字符。它们可以作为其他字符的占位符，也可以用于指示字符串中的位置。

许多命令（如 `grep`）依赖于正则表达式进行模式匹配。然而，重要的是，shell 用于文件名扩展的某些元字符的含义与此处讨论的含义不同。

要了解更多关于正则表达式的结构，请通过 `man 7 regex` 读取相应的帮助页。

下表列出了最重要的元字符及其含义：

# 表 1-21 正则表达式中的元字符

| 字符 | 含义 | 示例 |
| :--- | :--- | :--- |
| ^ | 行首 | ^The: 如果 The 在行首则匹配 The |
| $ | 行尾 | $: 如果 eighty 在行尾则匹配 eighty |
| \< | 单词边界 | \<thing>: 匹配整个单词 thing |
| \> | 单词边界 | \>thing>: 匹配整个单词 thing |
| [abc] | 集合中的任意一个字符 | [abc]: 匹配 "a", "b", 或 "c" 中的任意一个 |
| [0-9] | 范围内的任意数字 | [0-9]: 匹配 "0" 到 "9" 之间的任意数字 |
| [-+] | 不属于字符中的任意 | [-+]: 匹配 "-" 或 "+" |
| + | 一个或多个前一个字符 | file*: 匹配数字 |
| * | 任意次数（包括零） | file*: 匹配 file1, file2 |
| {min,max} | 前一个表达式重复 min 到 max 次 | {1,5}: 匹配一个到五个数字数字 |
| (...) | 用于分组的备选方案 | (f): 匹配 file |
| ? | 前一个字符零或一个 | file?: 匹配 file 和 file2 |
| \ | 转义后续字符以移除其特殊含义 | \.novell.com: 匹配 novell.com |
| | | 括号 | [(a-Z]+) |

# 使用过滤器处理文本流

你还需要熟悉如何使用过滤器处理文本流。你可以使用多个 Linux 命令处理来自文件或标准输入的文本并以指定的方式对其格式化。输出发送到文件或标准输出。原始文件不会发生任何修改。

> 提示：你可以使用管道和重定向将文本流从一个命令发送到另一个命令以执行复杂的修改。

你可以使用以下工具：

- `cut`
- `expand`
- `fmt`
- `join`
- `nl`
- `od`
- `paste`
- `pr`
- `sed` and `awk`
- `sort`
- `split`
- `tr`
- `unexpand`
- `uniq`
- `wc`

`cut` 命令用于从文件中打印指定的列或字段到标准输出。默认情况下，使用 Tab 字符作为分隔符。可以使用以下选项：

- `blist`: 仅选择这些字节。
- `cclist`: 仅选择这些字符。
- `ddelim`: 使用指定的字符代替 Tab 作为字段分隔符。
- `flist`: 仅选择指定的字段。打印任何包含分隔符锚点的行，除非指定了 `-s` 选项。
- `-s`: 不打印包含分隔符的行。

例如，你可以使用 `cut` 从 `/etc/passwd` 文件显示所有用户名。用户名位于文件每行的第一个字段。然而，该文件使用冒号作为字段分隔符，因此你必须指定除 Tab 以外的分隔符。执行此操作的命令所示：

```bash
dal:~ # cut -d: -f1 /etc/passwd

at

bin

daemon

ftg

games

qdm

haldaemon

lp

mail

man

...
```

### expand

`expand` 命令用于处理文本流并移除所有的制表符字符，将其替换为指定数量的空格（默认为 8）。你可以使用 `-t number` 选项指定指定数量的空格。语法为 `expand -t number filename`。

### fmt

你可以使用 `fmt` 命令来重新格式化文本文件。它通常用于将文件内长行的换行更改为易于管理的宽度。命令的输出写入标准输出；但也可以将其重定向到文件。

使用 `fmt` 的语法为 `fmt option file name`。例如，假设你在名为 `lorem.txt` 的文件中有以下正文：

Lorem ipsum dolor sit amet, consectetuer adipiscing elit. Curabitur digniss pede. Queisque dui dui, ultricies ut, facilisis non, pulvinar purus. Duis arcu a purus volutpat iaculis. Morbi id in diam dictum. Praesent consectetuer vehicula ipsum. Praesent tortor massa, neque, in posuere eget, pede.

该文本太宽，无法适应此页面，也无法很好地适应标准的终端窗口。为了解决这个问题，你可以运行 `fmt` 命令并配合 `-w` 选项将文本收窄到 40 列，如下：

```bash
dal:~ # fmt -w 40 lorem.txt

Lorem ipsum dolor sit amet,

consectetur adipiscing elit. Curabitur

dignim venenatis velit. Queisque

dui ultricies ut, facilisis non,

pulvinar non, purus. Quis arcu

a purus volutpat dictum. Morbi id

duin in ornare. Praenet

consectetur Vehicula ipsum. Praesent

tortor massa, congue et, ornare in,

posuere est, pede.
```

### join

`join` 命令从两个指定的输入文件中打印具有相同连接字段的行。第一个字段是默认的连接字段，用空格分隔。你可以使用 `-j field` 选项指定不同的连接字段。

例如，你有两个文件。第一个文件（名为 `firstnames`）包含以下内容：

- 1 Robb
- 2 Kimberly
- 3 Mary

第二个文件（名为 `lastnames`）包含以下内容：

- 1 Tracy
- 2 Sanders
- 3 Morgan

你可以使用 `join` 命令连接每个文件中对应的行，如下所示：

```bash
dal:~ # join -j 1 firstnames lastnames

1 Robb Tracy

2 Kimberly Sanders

3 Morgan
```

### nl

你可以使用 `nl` 命令来确定文件的行数。当你运行该命令时，输出将写入标准输出，并在文件的每行开头添加行号。

在下面的示例中，对 `Lorem.txt` 文件运行 `nl` 命令并将输出写到屏幕：

```bash
dal:~ # nl /home/geeko/Desktop/Lorem.txt

1 Lorem ipsum dolor sit amet, consectetuer adipiscing elit.

Curabitur digniss

2 venenatis pede. Queisque dui dui, ultricies ut, facilisis non,

pulvinar non,

3 purus. Duis aquis a arcu purus velit volutpat iaculus. Morbi dui in

diam ornare

4 dictum. Praesent consectetuer vehicula ipsum., Praesent tortor

massa, congue et,

5 ornare in, posuere eget, pede.
```
