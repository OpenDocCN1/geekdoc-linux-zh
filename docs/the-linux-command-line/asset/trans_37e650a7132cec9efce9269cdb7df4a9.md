

是一个模式编辑器。当 vi 启动时，它开始于命令模式。在此模式下，几乎每个键都是一个命令，因此如果我们开始输入，vi 基本上会发疯并制造一团乱。

## 进入插入模式

为了向我们的文件添加一些文本，我们必须先进入插入模式。为此，我们按下 “i” 键。之后，如果 vim 以其通常的增强模式运行，我们应该在屏幕底部看到以下内容（在 vi 兼容模式下不会出现）：

```
-- INSERT --
```

现在我们可以输入一些文本。试试这个：

```
The quick brown fox jumped over the lazy dog.
```

要退出插入模式并返回命令模式，请按下 Esc 键。

## 保存我们的工作

要保存我们刚刚对文件所做的更改，我们必须在命令模式下输入一个 ex 命令。这很容易，只需按下 “:” 键即可。执行此操作后，冒号字符应出现在屏幕底部：

```
:
```

要写入我们修改过的文件，我们在冒号后跟一个 “w” 然后按 Enter：

```
:w
```

文件将被写入硬盘，我们应该在屏幕底部得到一个确认消息，像这样：

```
"foo.txt" [New] 1L, 46C written
```

提示：如果阅读 vim 文档，你会注意到（令人困惑的是）命令模式被称为普通模式，而 ex 命令被称为命令模式。注意。

## 移动光标

在命令模式下，vi 提供了大量移动命令，其中一些与 less 共享。以下是其中一部分：

表 13-1：光标移动键

| Key | Moves The Cursor |
|---|---|
| l or Right Arrow | Right one character. |
| h or Left Arrow | Left one character. |
| j or Down Arrow | Down one line. |
| k or Up Arrow | Up one line. |
| 0 (zero) | To the beginning of the current line. |
| ^ | To the first non-whitespace character on the current line. |
| $ | To the end of the current line. |
| w | To the beginning of the next word or punctuation character. |
| W | To the beginning of the next word, ignoring punctuation characters. |
| b | To the beginning of the previous word or punctuation character. |
| B | To the beginning of the previous word, ignoring punctuation characters. |
| Ctrl-f or Page Down | Down one page. |
| Ctrl-b or Page Up | Up one page. |
| number G | To line number. For example, 1G moves to the first line of the file. |
| G | To the last line of the file. |

为什么使用 h、j、k 和 l 键进行光标移动？因为 vi 最初编写时，并非所有视频终端都有方向键，而熟练的打字员可以使用常规键盘键移动光标，而无需将手指从键盘上抬起。

vi 中的许多命令可以前面加上一个数字，如上面列出的 “G” 命令。通过在命令前加上数字，我们可以指定命令执行的次数。例如，命令 “5j” 会使 vi 将光标向下移动五行。

## 基本编辑

大多数编辑都由几个基本操作组成，例如插入文本、删除文本以及通过剪切和粘贴移动文本。vi 当然以其独特的方式支持所有这些操作。vi 还提供了一种有限的撤销形式。如果我们在命令模式下按下 “u” 键，vi 将撤消你所做的最后一次更改。当我们尝试一些基本编辑命令时，这会很有用。

## 追加文本

vi 有几种进入插入模式的不同方法。我们已经使用过 i 命令来插入文本。

让我们回到我们的 foo.txt 文件片刻：

```
The quick brown fox jumped over the lazy dog.
```

如果我们想在此句末尾添加一些文本，就会发现 i 命令做不到，因为我们无法将光标移至行尾。vi 提供了一个用于追加文本的命令，即合理命名的 “a” 命令。如果我们将光标移动到行尾并输入 “a”，光标将移至行尾之外，vi 将进入插入模式。这将允许我们添加更多文本：

```
The quick brown fox jumped over the lazy dog. **It was cool.**
```

记得按下 Esc 键以退出插入模式。

由于我们几乎总是希望将文本追加到当前行的末尾，vi 提供了一个快捷方式来移动到当前行末并开始追加。它是 “A” 命令。让我们试试

