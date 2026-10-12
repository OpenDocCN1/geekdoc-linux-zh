
Hare, Chris, and Emmett Daney, et al. *Inside Unix*. Indianapolis, IN: New Riders Publishing, 1994. ISBN: 1-56205-401-5. 第5章涵盖了 `shell` 的基础及其功能。

LeBlanc, Dee-Ann. *General Linux I Exam Prep*. Scottsdale, AZ: The Coriolis Group, 2000. ISBN: 1-57610-567-9. 第5章，“`Shell`、`脚本`、`编程`与`编译`”提供了关于本章内讨论主题的更多信息。

`http://dafy.robelle.com/smugbook/shell.html` 是 Robelle 的 UNIX `Shell` 指南，包含了关于 `sh`、`csh` 和 `ksh` 的信息。

`www.linuxcare.com/products/prodmore.ep?PRODUCT_GROUP=Shells` 提供了各种 `shell` 的比较以及用户对每个的。

`http://metalagb.unc.edu/mdw/index.html` 是 Linux 文档项目，包含了常见问题、教程和单个手册页 (`man pages`)。

## 文本处理基础

你需要理解的术语：

- `cat`
- `tac`
- `nl`
- `head`
- `tail`
- `cut`
- `paste`
- `join`
- `sort`
- `wc`
- `fmt`
- `tr`

你需要精通的技术：

- 理解处理 Linux 文本的基本概念
- 识别 `ASCII` 操作之间的差异

# 第 3 章

在本章中，你将学习用于在 Linux 操作系统创建和修改文本文件的基本实用。我们扩展了第 2 章中的许多重定向命令。

### 最简单的文本处理工具是 `cat`，源自单词 "concatenate"连接）。默认情况下，它显示文件的全部内容（标准输出）。`cat` 还有许多实用的选项：

- `-b`—对行进行编号
- `-E`—在每行末尾显示美元符号 (`$`)（回车）
- `-T`—显示所有制表符
- `-v`—显示制表符和回车以外的非打印字符
- `-A`—作用与 `-v` 结合 `-E` 和 `-T` 相同

为了说明 `cat` 的用途，假设有一个名为 `"example"` 的四行文件内容如下：

```
How much wood
could chuck
if wood
```

要在屏幕上完全按照它们出现的方式查看文件内容，命令是：

```
cat example
```

要查看带行号的文件，命令是：

```
cat -b example

1 How much wood
2 could chuck
3 if wood
4
```

使用 `-v` 显示除了制表符和回车以外的非打印字符：

```
cat -v example

How much wood$
could chuck$
if wood$
```

使用 `-Ab` 结合选项，效果如下：

```
cat -Ab example

1 How much wood$
2 could chuck$
3 if wood$
4
```

## `nl`, `head`, 和 `tail`

三个简单的命令可以查看文件的全部或部分：`nl`、`head` 和 `tail`。第一个工具 `nl`，用于行编号，类似于 `cat -b`。两者都对显示行进行编号，默认情况下都不编号。`nl` 可以使用某些选项来更改显示：

- `-i`—允许你更改增量（默认为 1）
- `-v`—允许你更改起始数字（默认为 1）
- `-n`—更改显示的对齐方式：
  - `nln`—左对齐显示
  - `nrn`—右对齐显示
  - `nrz`—使用前导零
- `-s`—在行号和文本之间使用指定的字符（默认为空格）

第二个工具 `head`。正如其名所示，该工具查看文件的顶部部分：默认是前 10 行。你可以通过连字符后跟数字来更改行数。以下示例假设一个名为 `"numbers"` 的文本文件包含 200 行，从 `"one"` 数到 `"two hundred"`：

```
$ head numbers

one
two
three
four
five
six
seven
eight
nine
ten
$

$ head -3 numbers

one
two
three
$

$ head -50 numbers

one
two
three
（为了节省空间已省略）
forty-eight
forty-nine
ifty
$
```

在打印多个文件时，`head` 会在每个列表之前放置一个头部，标识显示的是哪个文件。`-q` 选项抑制这些头部。

![](img/f9e5762d07ca45a6f38ffcb92cd56e5e_72_0.png)

`tail` 命令有几种运行模式。默认情况下，它是 `head` 的相反，显示文件的末尾而不是开头。同样，它默认显示 10 行，但你可以通过使用连字符加数字来更改它：

```
$ tail numbers
one hundred ninety-one
one hundred ninety-two
one hundred ninety-three
one hundred ninety-four
one hundred ninety-five
one hundred ninety-six
one hundred ninety-seven
one hundred ninety-eight
one hundred ninety-nine
two hundred
$

$ tail -3 numbers
one hundred ninety-eight
one hundred ninety-nine
two hundred
$

$ tail -50 numbers
one hundred fifty-one
one hundred fifty-two
one hundred fifty-three
（为了节省空间已省略）
one hundred ninety-eight
one hundred ninety-nine
two hundred
$
```

然而，`tail` 工具的功能不仅限于此，它包含一个加号 (`+`) 选项。这允许你指定一个起始点，在此点之后你将看到整个文件。例如：

```
$ tail +50 numbers
```

```
$ tail -f numbers
```

显示文件的最后 10 行但保持打开——跟踪文件——并显示附加到文件中的任何新行。要退出无尽的监控循环，你必须按下中断键序列，在大多数系统上默认是 `Ctrl+C`。

注意：要查找你会话的中断键序列，请使用命令：

```
stty -a
```

并查找 `intr=`

## `cut`, `paste`, and `join`

### `cut`

`cut` 工具提供了从文件中分离可能构成数据字段的列的能力。默认分隔符是制表符（`tab`），`-f` 选项指定所需的字段。例如，一个名为 `"august"` 的文本文件有三列，如下：

| one two three |
| four five six |
| seven eight nine |
| ten eleven twelve |

命令：

```
cut -f2 august
```

返回：
