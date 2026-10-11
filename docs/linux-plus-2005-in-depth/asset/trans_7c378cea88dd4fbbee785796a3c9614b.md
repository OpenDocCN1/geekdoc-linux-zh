
## 将字符串（STRING(s)）回显到标准输出
- `-e` 不输出末尾的换行符
- 启用以下列出的反斜杠转义字符的解析
- `-E` 禁用对字符串（STRINGS）中这些序列的解析
- `--help` 显示此帮助并退出
- `--version` 输出版本信息并退出

如果没有使用 `-E`，以下序列会被识别并插值：
- `\NNN` ASCII 代码为 NNN（八进制）的字符
- `\\` 反斜杠
- `\a` 警报（BEL）
- `\b` 退格
- `\c` 抑制末尾的换行符
- `\f` 换页符
- `\n` 换行符

虽然这种输出可能不太易读，但它确实包含了有助于用户找到更多有关 `/bin/echo` 命令信息的文本片段。另一个可以安全地用于二进制文件和文本文件的命令是 `od` 命令，它以八进制格式（数值基数 8 格式）显示文件内容。以下示例展示了使用 `od` 命令显示文件 `project4` 的前五行：

```bash
[root@server1 root]# od project4 | head -5
0000000 0704510 072040 062550 062562 020054 020111 067550 062560
0000020 072040 064550 020163 065044 020171 064546 062156 020163
0000040 067571 020165 062567 066154 066456 006412 052412 063156
0000060 071157 072564 065556 062564 074554 073440 020145 062567
0000100 062562 067040 072157 060440 066142 020145 067564 064440
[root@server1 root]#
```

# 注意
> 你可以使用 `od` 命令的 `-x` 选项以十六进制格式（数值基数 16 格式）显示文件。

## 在文件中搜索文本

回想一下，Linux 是以 UNIX 操作系统为模型建立的。UNIX 操作系统常被称为所有操作系统的“祖父”，因为它已有 30 多年的历史，并且构成了大多数计算技术进步的基础。过去 30 年中，UNIX 操作系统的主要用途是通过数据库应用程序简化商业和科学管理。因此，为 UNIX 操作系统开发了许多命令（称为**文本工具**），这些命令可以通过许多不同且有利的方式搜索和操作文本，例如数据库信息。还开发了一组文本通配符，以简化对特定文本信息的搜索。这些文本通配符被称为*正则表达式 (regexp)*，被多种文本工具和编程语言识别，包括但不限于以下工具：

- grep
- awk
- sed
- vi
- Emacs
- ex
- ed
- C++
- PERL
- Tcl

由于 Linux 是 UNIX 操作系统的近亲，这些文本工具和正则表达式也可在 Linux 中使用。通过结合使用文本工具（正如你稍后所见），典型的 Linux 系统几乎可以以任何可能的方式搜索和操作数据。因此，正则表达式和使用它们的文本工具在当今的商业中很常用。

## 正则表达式

如前所述，正则表达式（也称为“regexp”）允许你在文本文档中指定某种特定的文本模式。它们的工作方式与通配符元字符相似，因为它们都用于匹配字符，但它们有许多不同之处：

- 通配符元字符由 shell 解释，而正则表达式由文本工具程序解释。
- 通配符元字符匹配 Linux 文件系统中文件名（或目录名）中的字符，而正则表达式匹配 Linux 文件系统中*文本文件内*的字符。
- 通配符元字符通常与正则表达式元字符具有不同的定义。
- 可用的正则表达式元字符比通配符元字符更多。

此外，正则表达式元字符分为两类：通用正则表达式和扩展正则表达式。通用正则表达式适用于大多数文本工具；然而，扩展正则表达式不太常见，仅在特定的文本工具中可用。表 4-4 展示了一些通用和扩展正则表达式的定义和示例。

### 表 4-4 正则表达式

| 正则表达式 | 描述 | 示例 | 类型 |
| :--- | :--- | :--- | :--- |
| `*` | 匹配前一个字符 0 次或多次出现 | `letter*` 匹配 `lette`、`letter`、`letter`、`letterrr`、`letterrrr` 等 | 通用 |
| `?` | 匹配前一个字符 0 次或 1 次出现 | `letter?` 匹配 `lette`、`letter` | 扩展 |
| `+` | 匹配前一个字符 1 次或多次出现 | `letter+` 匹配 `letter`、`letter`、`letterrr`、`letterrrr` 等 | 扩展 |
| `.` (句点) | 匹配任意类型的 1 个字符 | `letter.` 匹配 `lettera`、`letterb`、`letterc`、`letter1`、`letter2`、`letter3` 等 | 通用 |
| `[...]` | 匹配括号内指定范围内的一个字符 | `letter[1238]` 匹配 `letter1`、`letter2`、`letter3`、`letter8`<br>`letter[a-c]` 匹配 `lettera`、`letterb` 和 `letterc` | 通用 |
| `[^...]` | 匹配*不在*括号内指定范围内的一个字符 | `letter[^1238]` 匹配 `letter4`、`letter5`、`letter6`、`lettera`、`letterb` 等（除 1、2、3 或 8 外的任意字符） | 通用 |
| `{ }` | 匹配前一个字符的特定数量或范围 | `letter{3}` 匹配 `letterr`，而 `letter[2,4]` 匹配 `letter`、`letterr` 和 `letterrr` | 扩展 |
| `^` | 如果紧随其后的字符是行首字符，则匹配这些字符 | `^letter` 如果 `letter` 是行中的第一组字符，则匹配 `letter` | 通用 |
| `$` | 如果前一个字母字符是行尾字符，则匹配这些字符 | `$` 如果 `letter` 是行中的最后一组字符，则匹配 `letter` | 通用 |
| `(...\|...)` | 匹配两组字符中的任意一组 | `(mother\|father)` 匹配单词 "mother" 或 "father" | 扩展 |

## grep 命令

允许你使用正则表达式搜索信息的最常用文本工具是 `grep` 命令。**grep** 命令（**glob al regular expression print** 的缩写）用于显示文本文件中匹配特定通用正则表达式的行。要显示匹配扩展正则表达式的文本行，必须使用 **egrep 命令**（或 `grep` 命令的 `-E` 选项）。此外，**fgrep 命令**（或 `grep` 命令的 `-F` 选项）不解释任何正则表达式，因此返回结果的速度要快得多。例如，以之前展示的 `project4` 文件为例：

```bash
[root@server1 root]# cat project4
Hi there, I hope this day finds you well.

Unfortunately we were not able to make it to your dining
room this year while vacationing in Algonquin Park - I
especially wished to see the model of the Highland Inn
and the train station in the dining room.

I have been reading on the history of Algonquin Park but
no where could I find a description of where the Highland
Inn was originally located on Cache lake.

If it is no trouble, could you kindly let me know such that
I need not wait until next year when I visit your lodge?

Regards,
Mackenzie Elizabeth
[root@server1 root]#
```

`grep` 命令至少需要两个参数，第一个参数指定要搜索的文本，其余参数指定要搜索的文件。如果匹配到某种文本模式，`grep` 命令会在终端屏幕上显示整行内容。例如，要仅列出文件 `project4` 中包含单词 “Algonquin Park” 的行，请输入以下命令：

```bash
[root@server1 root]# grep "Algonquin Park" project4
room this year while vacationing in Algonquin Park - I
I have been reading on the history of Algonquin Park but
[root@server1 root]#
```

若要返回不包含文本 “Algonquin Park” 的行，可以使用 `grep` 命令的 `-v` 选项来反转上一条命令的含义：

```bash
[root@server1 root]# grep -v "Algonquin Park" project4
Hi there, I hope this day finds you well.
```

