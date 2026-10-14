

# 基本编辑

大多数编辑操作都由几个基本操作组成，例如插入文本、删除文本，以及通过剪切和粘贴移动文本。vi 当然以其独特的方式支持所有这些操作。vi 还提供了一种有限形式的撤销。如果我们在命令模式下按下 u 键，vi 将撤销你所做的最后一次更改。在我们尝试一些基本编辑命令时，这会很有用。

## 追加文本

vi 有几种不同的进入插入模式的方式。我们已经使用过 i 命令来插入文本。

让我们回到我们的 foo.txt 文件片刻。

```
The quick brown fox jumped over the lazy dog.
```

如果我们想在这句话末尾添加一些文本，就会发现 i 命令做不到，因为我们无法将光标移动到行尾之外。vi 提供了一个用于追加文本的命令，即合理命名的 a 命令。如果我们将光标移动到行尾并输入 a，光标将移过行尾，vi 将进入插入模式。这将允许我们添加更多文本。

```
The quick brown fox jumped over the lazy dog. It was cool.
```

记得按下 ESC 键退出插入模式。

由于我们几乎总是希望将文本追加到行尾，vi 提供了一个快捷方式来移动到当前行的末尾并开始追加。它就是 A 命令。让我们试试并在我们的文件中添加更多行。

首先，我们将使用 0（零）命令将光标移动到行的开头。现在我们输入 A 并添加以下文本行：

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3
```

再次按下 ESC 键退出插入模式。
正如我们所见，A 命令更有用，因为它在开始插入模式之前会将光标移动到行尾。

## 打开一行

我们插入文本的另一种方式是通过“打开”一行。这会在两行现有行之间插入一个空白行并进入插入模式。这有两个变体，如表 12-2 所描述。

表 12-2：行打开键

| Command | Opens |
|---|---|
| o | The line below the current line |
| O | The line above the current line |

我们可以按如下方式演示：光标放在第 3 行，然后输入 o。

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2
Line 3

Line 4
Line 5
```

在第三行下方打开了一个新行，我们进入了插入模式。通过按下 ESC 键退出插入模式。按下 u 撤销我们的更改。

输入 O 在光标上方打开一行。

```
The quick brown fox jumped over the lazy dog. It was cool.
Line 2

Line 3
```

通过按下 ESC 退出插入模式，并通过输入 u 撤销我们的更改。

## 删除文本

正如我们所期望的，vi 提供了多种删除文本的方式，所有这些方式都包含两个按键之一。首先，x 命令将删除光标位置处的字符。x 可以前面加上一个数字，指定要删除的字符数。d 命令更通用。与 x 类似，它前面也可以加上一个数字，指定删除执行的次数。此外，d 总是后面跟随一个移动命令，该命令控制删除的大小。表 12-3 提供了一些示例。

表 12-3：文本删除命令

| Command | Deletes |
|---|---|
| x | The current character |
| 3x | The current character and the next two characters |
| dd | The current line |
| 5dd | The current line and the next four lines |
| dw | From the current cursor position to the beginning of the next word |
| d$ | From the current cursor location to the end of the current line |
| d0 | From the current cursor location to the beginning of the line |
| d^ | From the current cursor location to the first non-whitespace character in the line |
| dG | From the current line to the end of the file |
| d20G | From the current line to the twentieth line of the file |

将光标放在我们文本第一行的单词 It 上。反复按下 x 键，直到句子其余部分被删除。接下来，反复按下 u 键，直到删除被撤销。

### NOTE

* Real vi supports only a single level of undo. vim supports multiple levels.

让我们再次尝试删除，这次使用 d 命令。再次将光标移动到单词 It 并输入 dw 以删除该单词。

```
The quick brown fox jumped over the lazy dog. was cool.
Line 2
Line 3
Line 4
Line 5
```

输入 d$ 以从光标位置删除到行尾。

```
The quick brown fox jumped over the lazy dog.
Line 2
Line 3
Line 4
Line 5
```

输入 dG 以从当前行删除到文件末尾。

```
~
~
~
~
```

输入 u 三次以撤销删除。

## 剪切、复制和粘贴文本

d 命令不仅删除文本，还“剪切”文本。每次使用 d 命令时，删除的内容都会被复制到粘贴缓冲区（想想

