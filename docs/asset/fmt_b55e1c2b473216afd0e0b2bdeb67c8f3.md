
## 光标移动

| `k` or `Up Arrow` | Up one line. |
| `0` (zero) | To the beginning of the current line. |
| `^` | To the first non-whitespace character on the current line. |
| `$` | To the end of the current line. |
| `w` | To the beginning of the next word or punctuation character. |
| `W` | To the beginning of the next word, ignoring punctuation characters. |
| `b` | To the beginning of the previous word or punctuation character. |
| `B` | To the beginning of the previous word, ignoring punctuation characters. |
| `Ctrl-f` or `Page Down` | Down one page. |
| `Ctrl-b` or `Page Up` | Up one page. |
| `numberG` | To line number. For example, `1G` moves to the first line of the file. |
| `G` | To the last line of the file. |

为什么使用 `h`、`j`、`k` 和 `l` 键进行光标移动？因为 vi 最初编写时，并非所有视频终端都有方向键，而熟练的打字员可以使用常规键盘键移动光标，而无需将手指从键盘上抬起。

vi 中的许多命令都可以加上数字前缀，就像上面列出的 "`G`" 命令一样。通过在命令前加上数字，我们可以指定命令执行的次数。例如，命令 "`5j`" 会使 vi 将光标向下移动五行。

## 基本编辑

大多数编辑工作都由几个基本操作组成，例如插入文本、删除文本以及通过剪切和粘贴移动文本。vi 当然以其独特的方式支持所有这些操作。vi 还提供了一种有限的撤销形式。如果我们在命令模式下按下 "`u`" 键，vi 将撤消你所做的最后一次更改。在我们尝试一些基本编辑命令时，这会很有用。

## 追加文本

vi 有几种进入插入模式的不同方法。我们已经使用过 `i` 命令来插入文本。

让我们回到我们的 `foo.txt` 文件片刻：

```
The quick brown fox jumped over the lazy dog.
```

如果我们想在这句话末尾添加一些文本，就会发现 `i` 命令做不到，因为我们无法将光标移动到行尾之外。vi 提供了一个用于追加文本的命令，即合理命名的 "`a`" 命令。如果我们将光标移动到行尾并输入 "`a`" ，光标将移出行尾，vi 将进入插入模式。这将允许我们添加更多文本：

```
The quick brown fox jumped over the lazy dog. It was cool.
```

请记住按下 `Esc` 键以退出插入模式。

由于我们几乎总是想在行尾追加文本，vi 提供了一个快捷方式来移动到当前行末并开始追加。它就是 "`A`" 命令。让我们试试它并向我们的文件添加更多行。

首先，我们将使用 "`0`" （零）命令将光标移动到行首。

现在我们键入 "`A`" 并添加以下文本行：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
```

再次按下 `Esc` 键退出插入模式。

正如我们所见，"`A`" 命令更加有用，因为它在启动插入模式之前将光标移到行尾。

## 打开一行

另一种插入文本的方式是“打开”一行。这会在两个现有行之间插入一个空白行并进入插入模式。它有两种变体：

表 12-2：打开行按键

| 命令 | 打开 |
|---|---|
| `o` | 当前行的下一行。 |
| `O` | 当前行的上一行。 |

我们可以如下演示：将光标放在“Line 3”上，然后按 `o` 键。

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3

Line 4
Line 5
```

在第三行下方打开了一个新行，我们进入了插入模式。按 `Esc` 键退出插入模式。按 `u` 键撤销我们的更改。

按 `O` 键在光标上方打开一行：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
```

```
Line 3
Line 4
Line 5
```

按 `Esc` 键退出插入模式，并按 `u` 键撤销我们的更改。

## 删除文本

正如我们所料，vi 提供了多种删除文本的方法，所有这些方法都包含两个按键之一。首先，`x` 键将删除光标位置的一个字符。`x` 前面可以加一个数字，指定要删除的字符数。`d` 键更为通用。与 `x` 一样，它前面可以加一个数字，指定删除操作的执行次数。此外，`d` 后面总是跟一个移动命令来控制删除的范围。以下是一些示例：

表 12-3：文本删除命令

| 命令 | 删除 |
|---|---|
| `x` | 当前字符。 |
| `3x` | 当前字符及其后两个字符。 |
| `dd` | 当前行。 |
| `5dd` | 当前行及后四行。 |
| `dw` | 从当前光标位置到下一个单词的开头。 |
| `d$` | 从当前光标位置到当前行末尾。 |
| `d0` | 从当前光标位置到行首。 |
| `d^` | 从当前光标位置到行中第一个非空白字符。 |
| `dG` | 从当前行到文件末尾。 |
| `d20G` | 从当前行到文件的第二十行。 |

将光标放在文本第一行的“It”一词上。反复按 `x` 键，直到句子的其余部分被删除。接下来，反复按 `u` 键，直到删除被撤销。

> **注意：** 真正的 vi 只支持单级撤销。vim 支持多级撤销。

让我们再次尝试删除，这次使用 `d` 命令。再次将光标移到“It”一词上，然后按 `dW` 删除该词：

```
The quick brown fox jumped over the lazy dog. was cool.
Line 2
Line 3
Line 4
Line 5
```

按 `d$` 从光标位置删除到行尾：

```
The quick brown fox jumped over the lazy dog.
Line 2
Line 3
Line 4
Line 5
```

按 `dG` 从当前行删除到文件末尾：

```
~
~
~
~
```

按 `u` 键三次以撤销删除。

## 剪切、复制和粘贴文本

`d` 命令不仅删除文本，还会“剪切”文本。每次使用 `d` 命令时，被删除的内容都会复制到粘贴缓冲区（可以理解为剪贴板），之后我们可以使用 `p` 命令将缓冲区内容粘贴到光标之后，或使用 `P` 命令将内容粘贴到光标之前。

`y` 命令用于“提取”（复制）文本，方式与 `d` 命令用于剪切文本非常相似。以下是一些将 `y` 命令与各种移动命令组合使用的示例：

*表 13-4：复制命令*

| 命令 | 复制 |
|---|---|
| `yy` | 当前行。 |
| `5yy` | 当前行及后四行。 |
| `yW` | 从当前光标位置到下一个单词的开头。 |
| `y$` | 从当前光标位置到当前行末尾。 |
| `y0` | 从当前光标位置到行首。 |
| `y^` | 从当前光标位置到行中第一个非空白字符。 |
| `yG` | 从当前行到文件末尾。 |
| `y20G` | 从当前行到文件的第二十行。 |

让我们尝试一些复制和粘贴。将光标放在文本的第一行，然后输入 `yy` 复制当前行。接下来，将光标移动到最后一行（`G`），然后输入 `p` 在当前行下方粘贴该行：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
The quick brown fox jumped over the lazy dog. It was cool.
```

和之前一样，`u` 命令将撤销我们的更改。在光标仍位于文件最后一行的情况下，输入 `P` 将文本粘贴到当前行上方：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
```

The quick brown fox jumped over the lazy dog. It was cool.

Line 5

Try out some of the other `y` commands in the table above and get to know the behavior of both the `p` and `P` commands. When you are done, return the file to its original state.

## Joining Lines
