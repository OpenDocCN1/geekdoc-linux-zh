

n 表示你想要恢复的行数。恢复的行从当前行开始插入。最后删除的行是首先恢复的行。

如果行是从文件中的不同位置删除的，你可以通过使用 M（移动）前缀子命令将它们放回它们所属的位置。有关此子命令的更多信息，请参阅第 84 页的“Moving lines”。要恢复你在一次编辑会话中删除的所有行，请输入：

```
====> recover
```

在前面 A 和 D 前缀子命令的示例中，删除了六行。要仅恢复最后两行，请使用以下命令：

```
====> recover 2
```

> z/OS 类比：这类似于在 ISPF 编辑器中使用 RECOVERY ON 命令并键入 UNDO，前提是你已在每次想要恢复的编辑步骤之间按下了 Enter。

## Adding indented lines

要连续添加缩进文本行，在前缀区域键入字符 SI。按下 Enter 后，一行将直接添加到包含 SI 的行之后。光标定位在与上一行文本开始的同一列，从而使你更容易输入缩进文本。

如果你不想再添加行，再次按下 Enter 且在新行上不输入任何内容即可。要在使用 SI 时在文件中添加一个空行，请在前缀区域包含虚线的行上至少进行一次更改（例如按一次空格键）：

. . . . .

请注意，仅仅使用光标位置键将光标移过一行并不会更改该行。

如果你先在新行上输入一些内容，就可以在添加该行后离开该行并在文件其他地方进行修正。当光标远离新行时按下 Enter，另一条新行将添加到最后添加的行之后。只有在按下 Enter 且未在新行上键入文本时，SI 才会被取消。

## Duplicating lines

要复制一行，在该行的前缀区域输入双引号（"）。可以在双引号前或后加上一个数字以复制该行多次；请参阅第 84 页的 Example 2-23。

### Example 2-23 Inserting three duplicate lines

```
=3== I want three more copies of this line.
==== They will appear before this line.
```

按下 Enter 后，文件显示的输出类似于 Example 2-24。

### Example 2-24 Output from inserting three duplicate lines

```
==== I want three more copies of this line.
==== I want three more copies of this line.
==== I want three more copies of this line.
==== I want three more copies of this line.
==== They will appear before this line.
```

要复制一段行，无论是一次还是指定次数，请在该块的第一行和最后一行输入两个双引号（"）。可以在第一个双引号前或后加上一个数字（例如 5"）以复制该块多次。

当你键入一个双引号（"）并按下 Enter 时，屏幕的状态区域会显示以下状态，允许你在完成块并按下 Enter 之前滚动窗口：

```
"" pending...
```

> z/OS 类比：在 z/OS 中，这类似于在 ISPF 编辑器中使用 R n（重复）行命令。

## Moving lines

要移动一行，在要移动的行的前缀区域输入单个字符 M（move）。通过在另一行的前缀区域输入字符 F（following）或 P（preceding）来指示其目标。按下 Enter 后，包含 M 的行将从其原始位置移除，并插入到包含 F 的行之后或包含 P 的行之前，具体取决于情况。

可以在 M 前或后加上一个数字以指示移动多于一行（例如 5M 或 M5）在前缀区域。待移动的行和目标行可以位于不同的屏幕上。

在输入 M、F 或 P 后，屏幕的状态区域会显示一个 Pending 状态。此待处理状态允许你在输入其他前缀子命令之前滚动屏幕。

