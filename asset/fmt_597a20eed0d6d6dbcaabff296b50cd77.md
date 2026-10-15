
| File3 | File4 | File5 |
|---|---|---|
| File 3: line 001 | File 4: line 001 | File 4: line 001 |
| File 3: line 002 | File 4: line 002 | File 4: line 002 |
| File 3: line 003 | File 4: line 003 | File 4: line 003 |
| File 3: line 004 | File 4: line 004 | File 4: line 004 |
| File 3: line 005 | File 4: line 005 | File 4: line 005 |
| File 3: line 006 | File 4: line 006 | File 3: line 003 |
| File 3: line 007 | File 4: line 007 | File 3: line 004 |
| File 3: line 008 | File 4: line 008 | File 3: line 005 |
| File 3: line 009 | File 4: line 009 | File 4: line 006 |
| File 3: line 010 | File 4: line 010 | File 4: line 007 |

# 脚本终止 (`exit` 命令)

偶尔，脚本会遇到一种使其无法继续处理的情况。发生这种情况时，它必须停止。对于这些情况，UNIX 提供了 `exit` 命令。

# 第 17 章 · C SHELL 编程

`exit` 命令终止脚本并设置退出状态。它可以带有数字参数使用，也可以不带参数使用。当带有数字使用时，脚本的退出状态被赋予该数字。当不带参数使用时，脚本的退出状态为 0。

# 参数和位置参数

之前的示例演示了 shell 脚本的基本概念。然而，shell 脚本在泛化时更有用。泛化脚本可以在不更改的情况下用于许多不同情况。例如，考虑提取行问题（参见第 719 页的提取行）。如果它能处理任何输入并能创建任意数量的行，将变得更有用。

C shell 使用参数和位置参数使脚本泛化。参数是用户提供的数据，在命令行中位于脚本名之后，并输入到脚本。位置参数是 shell 中预定义的内存变量（缓冲区）。共有九个位置参数，标记为 `$argv[1]`、`$argv[2]`...`$argv[9]`，用于存储用户输入的参数。

当执行脚本时，shell 将第一个参数放在第一个位置参数（`$argv[1]`）中，将第二个参数放在第二个位置参数（`$argv[2]`）中，依此类推，直到参数被存储完毕。脚本可以在任何可以使用变量的地方（以美元符号作为正确前缀）使用它们。这一概念如图 17.4 所示。

![](img/6e4cdc423ec40606ea72b32fdafff220_743_0.png)

**图 17.4** 参数和位置参数

**泛化文件名** 让我们重复提取行（参见第 719 页），但不再使用特定的文件名，而是使用位置参数。在这种情况下，我们有四个参数和四个位置参数。第一个参数是 `TheRaven`。第四个参数是 `midRaven.txt`。第二个和第三个参数是要提取的行范围。当调用脚本时，参数 1（`TheRaven`）的值被存储在 `$argv[4]` 中。参数 4（`midRaven.txt`）的值存储在参数 `$argv[2]` 中。通过这种机制，我们可以使用 `$argv[1]` 到 `$argv[4]` 的值编写一个通用脚本。该设计如图 17.5 所示。

> 我们可以拥有超过九个的位置参数，但无法直接访问它们。我们必须使用 `shift` 命令来处理它们。这些技术将在本章后面的部分讨论。

# 第 17.2 节 • 表达式 • 723

```bash
# fileExtr.scr TheRaven 42 47 midraven.txt
      Start               End
$argv[1] $argv[2] $argv[3] $argv[4]
TheRaven | 42      | 47      | midraven.txt
head -argv[3] $argv[1] | tail +argv[2] > $argv[4]
Script
Shell
```

图 17.5 匹配参数与位置参数

使用参数和位置参数的优势是，每当我们想要从不同的文件提取行或将输出存储在不同的文件中时，不需要重写提取脚本。通过泛化脚本，我们可以通过使用不同的参数更改位置参数（脚本 17.6）。

## 17.6 `fileExtr.scr` 脚本

```bash
#!/bin/sh
# Script: fileExtr.scr
# 从 $argv[1] 提取 $argv[2]-$argv[3] 行
# 并将它们放入 $argv[4]
head -argv[3] $argv[1] | tail +argv[2] > $argv[4]
# fileExtr.scr TheRaven 42 47 midraven.txt
```

% `cat` `midRaven.txt`
Open the shutter, when, with a flirt and flutter
In there flung a stately Raven of the saintly days of yore.
Not the least obedience he made; not a minute stopped or stayed;
But, with mien of lord or lady, perched above my chamber----
Perched upon a bust of Pallas just above my chamber door----
Perched, and sat, and nothing more.

# 17.2 表达式

表达式是求值为某个值的字符序列。C shell 支持几种类型的表达式，如图 17.6 所示。这些用于用于计算、做出决策和比较值。运算符总结在表 17.1 中。

| 运算符 | 描述 |
|---|---|
| `+` | 两个数的和。 |
| `-` | 前者减去后者。 |
| `*` | 两个数的积。 |
| `/` | 前者除以后者的商。 |
| `%` | 前者除以后者的余数。 |
| `++` | 变量加 1。 |
| `--` | 变量减 1。 |
| `=` | 赋值。 |
| `+= *= /= %=` | 执行操作 (`op`)并将结果存储在 `a`。 |

表 17.1 数学运算符

从表 17.1 可以看出，要使用表达式运算符，数据必须是数值。然而，正如第 504 页 13.3 节所述，C shell 将所有数据存储为字符串。它无法解释数值。这引出了一个问题：我们如何计算数值？答案是我们必须使用 `arithmetic` (`@`) 命令。

# 17.1 给字符串加

```bash
% set count = 5
% set count=$count+2
% echo $count
5+2
```

# `arithmetic` (`@`) 命令

如表 17.1 所示，C shell 提供了全算术运算符。然而，它们必须配合 `arithmetic` (`@`) 命令使用。算术命令仅处理整数；它无法处理浮点值。图 17.7 描述了算术命令的语法。

# 17.2 数学表达式运算符

```bash
% set operand1 = 15
% set operand2 = 6
% @ result = $operand1 * $operand2
% echo $result
90
```

我们现在准备好解决原始的变量加问题了。在本节开始时，我们在 17.1 节中演示了不能使用直观的方法来完成。相反，我们必须使用表达式来执行加法或其他任何数学运算。这段代码在 17.3 节中。

# 17.3 使用表达式加法

```bash
% set count = 5
% @ count += 2
% echo $count
7
```
