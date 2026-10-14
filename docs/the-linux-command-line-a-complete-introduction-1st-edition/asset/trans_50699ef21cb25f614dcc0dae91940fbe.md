

我们可以通过以下方式演示：把光标放在第 3 行，然后输入 o。

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3

Line 4
Line 5
```

在第三行下方打开了一行新行，并且我们进入了插入模式。通过按 ESC 键退出插入模式。输入 u 以撤销我们的更改。

输入 O 以在光标上方打开一行：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
```

按 ESC 键退出插入模式并通过输入 u 撤销我们的更改。

## 删除文本

正如我们所预期的那样，vi 提供了多种删除文本的方式，所有方式都包含其中两个按键之一。首先，X 键会删除光标位置处的字符。x 前面可以加上一个数字，指定要删除的字符数。D 键用途更广。与 x 类似，它前面也可以加上一个数字，指定删除执行的次数。此外，d 总是后面跟随一个移动命令，该命令控制删除的大小。表 12-3 列出了一些示例。

把光标放在第一行文本中的单词 It 上。重复输入 x 直到句子其余部分被删除。接下来，重复输入 u 直到撤销删除。

> 注意：真正的 vi 仅支持单层撤销。vim 支持多层撤销。

## 表 12-3：文本删除命令

| Command | Deletes |
|---|---|
| x | The current character |
| 3x | The current character and the next two characters |
| dd | The current line |
| 5dd | The current line and the next four lines |

## 表 12-3（续）

| Command | Deletes |
|---|---|
| dW | From the current cursor location to the beginning of the next word |
| d$ | From the current cursor location to the end of the current line |
| d0 | From the current cursor location to the beginning of the line |
| d^ | From the current cursor location to the first non-whitespace character in the line |
| dG | From the current line to the end of the file |
| d20G | From the current line to the 20th line of the file |

让我们再次尝试删除，这次使用 d 命令。再次将光标移动到单词 It 并输入 dW 以删除该单词：

```
The quick brown fox jumped over the lazy dog. was cool.
Line 2
Line 3
Line 4
Line 5
```

输入 d$ 以从光标位置删除到行尾：

```
The quick brown fox jumped over the lazy dog.
Line 2
Line 3
Line 4
Line 5
```

输入 dG 以从当前行删除到文件末尾：

```
~
~
~
~
```

输入 u 三次以撤销删除。

## 剪切、复制和粘贴文本

d 命令不仅删除文本，还会“剪切”文本。每次使用 d 命令时，删除的内容都会被复制到一个粘贴缓冲区（可视为剪贴板），我们之后可以用 p 命令将缓冲区内容粘贴到光标之后，或用 P 命令将内容粘贴到光标之前。

y 命令用于“拉取”（复制）文本，其使用方式与 d 命令用于剪切文本的方式类似。表 12-4 列出了将 y 命令与各种移动命令结合使用的一些示例。

## 表 12-4：拉取命令

| Command | Copies |
|---|---|
| yy | The current line |
| 5yy | The current line and the next four lines |
| yw | From the current cursor location to the beginning of the next word |
| y$ | From the current cursor location to the end of the current line |
| y0 | From the current cursor location to the beginning of the line |
| y^ | From the current cursor location to the first non-whitespace character in the line |
| yG | From the current line to the end of the file |
| y20G | From the current line to the 20th line of the file |

让我们尝试一些复制和粘贴。把光标放在文本的第一行并输入 yy 以复制当前行。接下来，将光标移动到最后一行（G）并输入 p 以在当前行下方粘贴复制的行：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
The quick brown fox jumped over the lazy dog. It was cool.
```

正如之前一样，u 命令会撤销我们的更改。光标仍位于文件最后一行时，输入 P 以在当前行上方粘贴文本：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
The quick brown fox jumped over the lazy dog. It was cool.
Line 5
```

尝试表 12-4 中的其他 y 命令，并熟悉 p 和 P 命令的行为。完成后，将文件恢复到原始状态。

