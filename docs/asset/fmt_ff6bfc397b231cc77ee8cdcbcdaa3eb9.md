
让我们回到`foo.txt`文件片刻。

```
The quick brown fox jumped over the lazy dog.
```

如果我们想在这句话末尾添加一些文本，就会发现`i`命令做不到，因为我们无法将光标移动到行尾之外。vi 提供了一个用于追加文本的命令，即合理命名的`a`命令。如果我们将光标移动到行尾并输入`a`，光标将移过行尾，vi 将进入插入模式。这将允许我们添加更多文本。

```
The quick brown fox jumped over the lazy dog. It was cool.
```

记得按下`ESC`键退出插入模式。

由于我们几乎总是希望将文本追加到行尾，vi 提供了一个快捷方式来移动到当前行的末尾并开始追加。它就是`A`命令。让我们试试并在我们的文件中添加更多行。

首先，我们将使用`0`（零）命令将光标移动到行的开头。现在我们输入`A`并添加以下文本行：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
```

再次按下`ESC`键退出插入模式。

正如我们所见，`A`命令更有用，因为它在开始插入模式之前会将光标移动到行尾。

### 打开一行

我们插入文本的另一种方式是通过“打开”一行。这会在两行现有行之间插入一个空白行并进入插入模式。这有两个变体，如表 12-2 所描述。

表 12-2：行打开键

| Command | Opens |
|---|---|
| `o` | The line below the current line |
| `O` | The line above the current line |

我们可以按如下方式演示：光标放在第 3 行，然后输入`o`。

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3

Line 4
Line 5
```

在第三行下方打开了一个新行，我们进入了插入模式。通过按下`ESC`键退出插入模式。按下`u`撤销我们的更改。

输入`O`在光标上方打开一行。

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2

Line 3
```

通过按下`ESC`退出插入模式，并通过输入`u`撤销我们的更改。

### 删除文本

正如我们所期望的，vi 提供了多种删除文本的方式，所有这些方式都包含两个按键之一。首先，`x`命令将删除光标位置处的字符。`x`可以前面加上一个数字，指定要删除的字符数。`d`命令更通用。与`x`类似，它前面也可以加上一个数字，指定删除执行的次数。此外，`d`总是后面跟随一个移动命令，该命令控制删除的大小。表 12-3 提供了一些示例。

表 12-3：文本删除命令

| Command | Deletes |
|---|---|
| `x` | The current character |
| `3x` | The current character and the next two characters |
| `dd` | The current line |
| `5dd` | The current line and the next four lines |
| `dw` | From the current cursor position to the beginning of the next word |
| `d$` | From the current cursor location to the end of the current line |
| `d0` | From the current cursor location to the beginning of the line |
| `d^` | From the current cursor location to the first non-whitespace character in the line |
| `dG` | From the current line to the end of the file |
| `d20G` | From the current line to the twentieth line of the file |

将光标放在我们文本第一行的单词 It 上。反复按下`x`键，直到句子其余部分被删除。接下来，反复按下`u`键，直到删除被撤销。

#### NOTE

* Real vi supports only a single level of undo. vim supports multiple levels.

让我们再次尝试删除，这次使用`d`命令。再次将光标移动到单词 It 并输入`dw`以删除该单词。

```
The quick brown fox jumped over the lazy dog. was cool.
Line 2
Line 3
Line 4
Line 5
```

输入`d$`以从光标位置删除到行尾。

```
The quick brown fox jumped over the lazy dog.
Line 2
Line 3
Line 4
Line 5
```

输入`dG`以从当前行删除到文件末尾。

```
~
~
~
~
```

输入`u`三次以撤销删除。

### 剪切、复制和粘贴文本

`d`命令不仅删除文本，还“剪切”文本。每次使用`d`命令时，删除的内容都会被复制到粘贴缓冲区（想想 clipboard）我们可以稍后使用`p`命令来粘贴缓冲区的内容到光标之前或之后。

`y`命令用于“拉取”（复制）文本，其使用方式与`d`命令用于剪切文本类似。表 12-4 提供了将`y`命令与各种移动命令组合使用的一些示例。

表 12-4：拉取命令

| Command | Copies |
|---|---|
| `yy` | The current line |
| `5yy` | The current line and the next four lines |
| `yw` | From the current cursor position to the beginning of the next word |
| `y$` | From the current cursor location to the end of the current line |
| `y0` | From the current cursor location to the beginning of the line |
| `y^` | From the current cursor location to the first non-whitespace character in the line |
| `yG` | From the current line to the end of the file |
| `y20G` | From the current line to the twentieth line of the file |

让我们试试复制和粘贴。将光标放在文本的第一行并输入`yy`以复制当前行。接下来，将光标移动到最后一行（`G`）并输入`p`以在当前行下方粘贴该行。

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
Line 5
The quick brown fox jumped over the lazy dog. It was cool.
```

就像之前一样，`u`命令会撤销我们的更改。将光标仍定位在文件的最后一行，输入`P`以在当前行上方粘贴文本。

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
Line 4
The quick brown fox jumped over the lazy dog. It was cool.
Line 5
```

尝试表 12-4 中的其他一些`y`命令，并熟悉`p`和`P`命令的行为。完成后，将文件恢复到原始状态。

### 连接行

vi 对行的概念相当严格。通常，不可能将光标移动到一行的末尾并删除换行符以将一行与下一行连接起来。正因如此，vi 提供了特定的命令`J`（不要与用于光标移动的`j`混淆）来将行连接在一起。

如果我们将光标放在第 3 行并输入`J`命令，会发生以下情况：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3 Line 4
Line 5
```

### 搜索和替换

vi 具有根据搜索结果移动光标位置的能力。它可以在单行或整个文件上执行此操作。它还可以有或无用户确认地执行文本替换。

#### 在一行内搜索

`f`命令搜索一行并将光标移动到指定字符的下一个实例。例如，命令`fa`将
