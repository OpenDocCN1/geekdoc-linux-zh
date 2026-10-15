
It started in command mode, switched to text-entry (append) mode, escaped to command mode, detour to ex mode, returned to command mode. The clue to mastering vi is gaining fluency with such sequences to the point where you move between the modes without thinking about them. You even reach the stage where vi seems completely intuitive!

![](img/0aad0e0ec0359d5e535f4b2e4c2df9e9_195_1.png)

# EXIT The vi Family of Editors 173

Finally, let's exit vi. Since you have just saved your work, a simple `:q` (quit) will bring you back to the shell from which vi was invoked. If you try `:q` before all current changes have been saved, you will be warned and vi will not exit until you write your changes or vi to discard them. You overload the warning with `:q!` (quit and discard recent changes without complaint). As noted earlier, you can

2. 你现在处于文本输入模式。具体来说，你处于插入模式（append mode），`APPEND MODE` 应该出现在状态行的右侧，即第 25 行。（如果没有显示，你可能正在使用关闭了 `showmode` 的 vi？要修复此问题，按 `Esc`，输入冒号 `:`，然后输入 `set showmode` 并按回车。现在从第 1 步重复。）

3. 在每行末尾带有回车的情况下输入文本：

最后，我正在使用 vi，这是一个视觉编辑器。

我正处于插入模式，因此我的按键记录被存储（追加）到编辑缓冲区中。稍后，在进一步编辑之后，我将将缓冲区写入文件 `test.data` 来保存这段文本。

我在每个句号后面都输入了换行符（Enter）和两个空格，以匹配 vi 中“句子”的定义。某些 vi 命令在逐句移动光标时依赖于这一惯例。

注意第 2 到第 6 行的波浪号（~）已经消失，但在未使用的第 7 到 24 行中，第一列仍有波浪号。如果你输入了错误，请暂时忽略它们！在你学习了一些光标移动后，我将解释如何进行纠正。

上面的文本存储在编辑缓冲区中。在你将其写入磁盘之前，`test.data` 文件始终保持空状态。在长时间的编辑过程中，定期保存缓冲区是一个良好的习惯。要做到这一点，请遵循以下步骤：

- 1. 按 `Esc` 退出插入模式并返回命令模式。
- 2. 输入冒号 `:`。你现在处于 ex 模式。状态行会显示这个冒号，它作为 ex 模式的提示符。
- 3. 输入 `w`（ex 命令）并按回车。这将编辑缓冲区写入磁盘。由于你没有指定文件名，缓冲区将写入当前文件，即 `test.data`。你现在回到了命令模式。

你可以在任何你拥有写权限的目录/文件名组合中保存缓冲区。例如，如果文件 `test.temp` 不存在，`:w test.temp` 将创建一个文件并将缓冲区写入其中。如果 `test.temp` 存在，`:w` 将不会覆盖它，但你可以使用 `:w! test.temp` 强制覆盖。当前文件名不会被 `:w` 命令改变，因此在没有文件名参数的情况下，后续写入仍将默认指向 `test.data`。

![](img/0aad0e0ec0359d5e535f4b2e4c2df9e9_194_0.png)

# 172 第十章

实用的变体是：`:w>>filename`，它将 vi 缓冲区追加到文件名。写入并退出 vi 有三种方便的方法：

- `:wq` (回车) 等同于 `:w` (回车) 后接 `:q` (回车)。
- `:x` (回车) 效果与上述。
- `ZZ` 效果与上述，但注意你不需要输入冒号或按回车。当你处于命令模式而非 ex 模式时，命令后不需要按回车；你的输入在命令完成后会立即生效。状态行将确认你的写入操作：

"test.data" [新文件] 5 行, 237 个字符

从现在起，上面的序列将被描述为“输入 `:w`”或简单的 `:w`，就像它是一个命令一样。这类命令有时被称为冒号命令——它们由进入 ex 模式的冒号、执行 ex 命令后跟回车（或 `Esc`）组成，并通常会将你返回命令模式。我说“通常”是因为有些冒号命令会退出 vi 或临时返回 shell。使用此类命令时，你将清除视觉提示（例如 shell 提示符），这些提示本表明你尚未回到 vi 命令模式。

![](img/0aad0e0ec0359d5e535f4b2e4c2df9e9_195_0.png)

> 注意：如果你想中止一个输入了一部分的 ex 命令，请按中断键（在大多数终端上为 Del、Delete 或 Rubout）。

现在你已经回到了命令模式，你会发现 `APPEND MODE` 消失了。没有显式的 `COMMAND MODE` 标识，但有一个简单的技巧可以确认你的模式状态（尤其在 `showmode` 关闭时非常有用）。只需再次按 `Esc`，你就会听到哔的一声。如果你已经处于命令模式，`Esc` 是一个无效选择。而如果你不在命令模式下，`Esc` 是 `showmode` 功能的可行替代方案。我们可以总结上述的操作：

```
a[text]Esc[:w<Return>
```

它从命令模式开始，切换到文本输入（插入）模式，逃回到命令模式，跳转到 ex 模式，返回命令模式。精通 vi 的关键在于熟练掌握此类序列，直到你在这些模式之间切换时无需思考。你甚至会达到 vi 看起来完全直觉的阶段！

![](img/0aad0e0ec0359d5e535f4b2e4c2df9e9_195_1.png)

# EXIT vi 编辑器家族 173

最后，让我们退出 vi。由于你刚刚保存了工作，一个简单的 `:q` (quit) 将带你回到当初调用 vi 的 shell。如果你在所有当前更改都保存之前尝试 `:q`，你将收到警告，并且在你写入更改或丢弃它们之前，vi 将不会退出。你可以用 `:q!`（退出并在不抱怨的情况下丢弃最近的更改）来覆盖该警告。如前提到的，你可以

（注：由于原始文本中存在大量重复内容，我已根据您的要求进行了翻译并去重处理，确保输出逻辑清晰且符合 Markdown 格式。）

## 光标移动

| 命令 | 动作 |
|---|---|
| `h` 或 `backsp` | 光标向左移动，直到行首。 |
| `j` 或 `Ctrl-N` | 光标向下移动。 |
| `k` 或 `Ctrl-P` | 光标向上移动。 |
| `l` | 光标向右移动，直到行尾。 |
| `w` | 光标向前移动到下一个单词的开头。 |
| `W` | 同 `w`，但单词是以空格分隔的字符串。 |
| `b` | 同 `w`，但向后移动到上一个单词的开头。 |
| `B` | 同 `W`，但向后移动到上一个单词的开头。 |
| `e` | 同 `w`，但停止在下一个单词的末尾。 |
| `E` | 同 `W`，但停止在下一个单词的末尾。 |
| `(` | 光标移动到当前句子的开头，或者如果光标已经在句首，则移动到上一个句首。 |
| `)` | 光标移动到下一个句子的开头。 |
| `H` | 光标移动到屏幕的第一行（home），即第 1 列（sweet home处为笔误）。 |
| `L` | 光标移动到屏幕的底部（bottom）。 |
| `^` | 光标移动到当前行的第一个非空字符。 |
| `0` (zero) | 光标移动到当前行的第 1 列（无论是否为空）。 |
| `$` | 光标移动到当前行的最后一个字符。 |

# 174 第十章

| 命令 | 动作 |
|---|---|
| `+` | 光标移动到下一行的第一个非空字符。 |
| `-` | 光标移动到上一个行的第一个非空字符。 |
| `g` | 光标移动到文件的第一行。 |
| `G` | 光标移动到文件的最后一行。 |
| `{` | 光标移动到当前段落的第一个非空行。 |
| `}` | 光标移动到当前段落的最后一个非空行。 |
| `f[char]` | 光标移动到当前行中下一个 `char` 处。 |
| `F[char]` | 光标移动到当前行中上一个 `char` 处。 |
| `t[char]` | 光标移动到当前行中下一个 `char` 之前的位置。 |
