
如果这是一个新文件，你将看到类似下面的内容：

```
+   - 
~ 
~
```

`"/tmp/test" [New File]`
顶部一个闪烁的框表示你的光标所在位置。底行会让你了解编辑的当前状态（在这里，只是刚打开了一个新文件）。中间有很多波浪号（`~`）作为占位符，因为文件中还没有任何文本。现在，令人生畏的`ing`在这里了：这里没有提示、菜单或图标来告诉你该做什么。更糟糕的是，你才刚刚开始。如果你乱按按键，计算机可能会向你发出蜂叫声。（有些人甚至说 Linux 并不友好。）

首先，你需要了解两种模式：**命令模式**和**输入模式**。`vi`编辑器始终从命令模式启动。在修改文件中的文本之前，你必须输入一个命令（一个或两个字母，前面带有可选的数字）来告诉`vi`你想做什么。大小写很重要，所以请务必按照示例完全使用大写和小写！

> 注意
> 在 Red Enterprise Linux、Fedora 以及其他 Linux 发行版中，对于普通用户，`vi`命令被别命名为运行`vim`。如果你输入`alias vi`，你会看到`alias vi='vim'`。`vi`和`vim`之间的第一个区别是，任何已知文件类型（如 HTML、C 或配置文件）都会以颜色显示。颜色表示文件的结构。`vim`的`vi`中不包含的功能还包括视觉高亮和分屏模式等。默认情况下，root 用户没有别名到`vim`。

## 添加文本

要进入输入模式，输入一个输入命令字母。开始时，输入以下任意一个字母。完成文本输入后，按下`Esc`键（有时）返回命令模式。记住`Esc`键！

- `a`—添加命令。使用此命令，你可以在光标右侧开始输入文本。
- `A`—行尾添加命令。使用此命令，你可以在当前行尾开始输入文本。

![](img/3886a4c1a684ab63e25e82e0a2d63de9_158_0.png)

## 第二部分：成为 Linux 高级用户

- `i`—插入命令。使用此命令，你可以在光标左侧开始输入文本。
- `I`—行首插入命令。使用此命令，你可以在当前行开头开始输入文本。
- `O`—在下方打开命令。此命令会在当前行下方打开新行并让你进入插入模式。
- `o`—在上方打开命令。此命令会在当前行上方打开新行并让你进入插入模式。

> 提示
> 当你在插入模式时，屏幕底部会显示 -- INSERT --。

输入几个单词，然后按回车键。重复几次，直到你有了几行文本。完成输入后，按下`Esc`返回命令模式。现在你已经有了一个包含某些文本的文件，尝试使用下一节描述的按键或字母在文本中移动。

> 提示
> 记住`Esc`键！它总是能带你回到命令模式。记住，有时你必须按两次`Esc`。例如，如果你输入冒号（`:`）进入模式，你必须按两次`Esc`才能返回命令模式。

## 在文本中移动

要在文本中移动，你可以使用上、下、右、左箭头键。然而，在打字时，许多移动按键就在你的指尖下：

- 箭头键—逐个字符地在行内向上、向下、向左或向右移动光标。左右移动时可以使用 Backspace 和空格键。
- `h`—逐个字符地在行内向左移动一个字符。
- `l`—向右移动一个字符。
- `k`—向上移动一个字符。
- `j`—向下移动一个字符。
- `w`—单词内向后移动到下一个单词的开头。
- `W`—向后移动到下一个单词的开头。
- `b`—向后移动到上一个单词的开头。
- `B`—向后移动到上一个单词的开头。
- `e`—移动到单词结尾。
- `E`—移动到单词结尾。
- `0`—移动到行首。
- `$`—移动到行尾。
- `H`—移动到屏幕左上角。
- `M`—移动到屏幕中间。
- `L`—移动到屏幕右下角。
- `gg`—移动到文件第一行。
- `G`—移动到文件最后一行。

## 移动文本

要在文本中移动，你可以使用上、下、右、左箭头键。然而，在打字时，许多移动按键就在你的指尖下：

- 箭头键—逐个字符地在行内向上、向下、向左或向右移动光标。左右移动时可以使用 Backspace 和空格键。
- `h`—逐个字符地在行内向左移动一个字符。
- `l`—向右移动一个字符。
- `k`—向上移动一个字符。
- `j`—向下移动一个字符。
- `w`—单词内向后移动到下一个单词的开头。
- `W`—向后移动到下一个单词的开头。
- `b`—向后移动到上一个单词的开头。
- `B`—向后移动到上一个单词的开头。
- `e`—移动到单词结尾。
- `E`—移动到单词结尾。
- `0`—移动到行首。
- `$`—移动到行尾。
- `H`—移动到屏幕左上角。
- `M`—移动到屏幕中间。
- `L`—移动到屏幕右下角。
- `gg`—移动到文件第一行。
- `G`—移动到文件最后行。

## 文本文本

文本文本移动，你可以使用，、、、、、、键。。
光光光光，

- ——光标标一个字符。
- —删除光标删除一个字符。
- `k`—删除光标下的字符。
- —删除光标标一个字符。
- `w`—删除一个单词。
- `dw`—删除一个单词。
- `w`—删除一个单词。
- `W`—删除一个单词。
- `b`—删除一个单词。
- `B`—删除一个单词。
- `e`—删除一个单词。
- `E`—删除一个单词。
- `0`—删除到行首。
- `$`—删除从删除到行尾。
- `H`—删除到屏幕左上角。
- `M`—删除到屏幕中间。
- `L`—删除到屏幕右下角。
- `gg`—删除到文件第一行。
- `G`—删除到文件最后行。

## 删除、删除

文本：

- `x`—删除光标下的字符。
- `r`—删除光标到行尾。
- `d`—删除光标到行尾。
- `w`—删除一个单词。
- `dw`—删除一个单词。
- `W`—删除一个单词。
- `b`—删除一个单词。
- `B`—删除一个单词。
- `e`—删除一个单词。
- `E`—删除一个单词。
- `0`—删除到行首。
- `$`—删除到行尾。
- `H`—删除到屏幕左上角。
- `M`—删除到屏幕中间。
- `L`—删除到屏幕右下角。
- `gg`—删除到文件第一行。
- `G`—删除到文件最后行。

- `x`—删除光标下的字符。
- `r`—删除光标到行尾。
- `d`—删除光标到行尾。
- `w`—删除一个单词。
- `dw`—删除一个单词。
- `W`—删除一个单词。
- `b`—删除一个单词。
- `B`—删除一个单词。
- `e`—删除一个单词。
- `E`—删除一个单词。
- `0`—删除到行首。
- `$`—删除到行尾。
- `H`—删除到屏幕左上角。
- `M`—删除到屏幕中间。
- `L`—删除到屏幕右下角。
- `gg`—删除到文件第一行。
- `G`—删除到文件最后行。

- `x`—删除光标下的字符。
- `r`—删除光标到行尾。
- `d`—删除光标到行尾。
- `w`—删除一个单词。
- `dw`—删除一个单词。
- `W`—删除一个单词。
- `b`—删除一个单词。
- `B`—删除一个单词。
- `e`—删除一个单词。
- `E`—删除一个单词。
- `0`—删除到行首。
- `$`—删除到行尾。
- `H`—删除到屏幕左上角。
- `M`—删除到屏幕中间。
- `L`—删除到屏幕右下角。
- `gg`—删除到文件第一行。
- `G`—删除到文件最后行。

## 复制、复制

- `x`—delete the character under cursor.
- `r`—delete from cursor to the end of line.
- `d`—delete from cursor to the end of line.
- `w`—delete a word.
- `dw`—delete a word.
- `W`—delete a word.
- `b`—delete a word.
- `B`—delete a word.
- `e`—delete a word.
- `E`—delete a word.
- `0`—delete to beginning of line.
- `$`—delete to end of line.
- `H`—delete to top-left of screen.
- `M`—delete to middle of screen.
- `L`—delete to bottom-right of screen.
- `gg`—delete to first line of file.
- `G`—delete to last line of file.

- `x`—delete the character under cursor.
- `r`—delete from cursor to the end of line.
- `d`—delete from cursor to the end of line.
- `w`—delete a word.
- `dw`—delete a word.
- `W`—delete a word.
- `b`—delete a word.
- `B`—delete a word.
- `e`—delete a word.
- `E`—delete a word.
- `0`—delete to beginning of line.
- `$`—delete to end of line.
- `H`—delete to top-left of screen.
- `M`—delete to middle of screen.
- `L`—delete to bottom-right of screen.
- `gg`—delete to first line of file.
- `G`—delete to last line of file.

- `x`—delete the character under cursor.
- `r`—delete from cursor to the end of line.
- `d`—delete from cursor to the end of line.
- `w`—delete a word.
- `dw`—delete a word.
- `W`—delete a word.
- `b`—delete a word.
- `B`—delete a word.
- `e`—delete a word.
- `E`—delete a word.
- `0`—delete to beginning of line.
- `$`—delete to end of line.
- `H`—delete to top-left of screen.
- `M`—delete to middle of screen.
- `L`—delete to bottom-right of screen.
- `gg`—delete to first line of file.
- `G`—delete to last line of file.

## 粘贴、粘贴

- `y`—copy the character under cursor.
- `r`—delete from cursor to the end of line.
- `y`—Move to the next word.
- `w`—Move to the next word.
- `W`—Move to the next word.
- `b`—Move to the previous word.
- `B`—Move to the previous word.
- `e`—Move to the next word.
- `E`—Move to the next word.
- `0`—Move to the beginning of line.
- `$`—Move to the end of line.
- `H`—Move to the top-left of screen.
- `M`—Move to the middle of screen.
- `L`—Move to the bottom-right of screen.
- `gg`—Move to the first line of file.
- `G`—Move to the last line of file.

- `y`—copy the character under cursor.
- `r`—delete from cursor to the end of line.
- `y`—Move to the next word.
- `w`—Move to the next word.
- `W`—Move to the next word.
- `b`—Move to the previous word.
- `B`—Move to the previous word.
- `e`—Move to the next word.
- `E`—Move to the next word.
- `0`—Move to the beginning of line.
- `$`—Move to the end of line.
- `H`—Move to the top-left of screen.
- `M`—Move to the middle of screen.
- `L`—Move to the bottom-right of screen.
- `gg`—Move to the first line of file.
- `G`—Move to the last line of file.

- `y`—copy the character under cursor.
- `r`—delete from cursor to the end of line.
- `y`—Move to the next word.
- `w`—Move to the next word.
- `W`—Move to the next word.
- `b`—Move to the previous word.
- `B`—Move to the previous word.
- `e`—Move to the next word.
- `E`—Move to the next word.
- `0`—Move to the beginning of line.
- `$`—Move to the end of line.
- `H`—Move to the top-left of screen.
- `M`—Move to the middle of screen.
- `L`—Move to the bottom-right of screen.
- `gg`—Move to the first line of file.
- `G`—Move to the last line of file.

## 粘贴、粘贴

- `y`—copy the character under cursor.
- `r`—delete from cursor to the end of line.
- `y`—Move to the next word.
- `w`—Move to the next word.
- `W`—Move to the next word.
- `b`—Move to the previous word.
- `B`—Move to the previous word.
- `e`—Move to the next word.
- `E`—Move to the next word.
- `0`—Move to the beginning of line.
- `$`—Move to the end of line.
- `H`—Move to the top-left of screen.
- `M`—Move to the middle of screen.
- `L`—Move to the bottom-right of screen.
- `gg`—Move to the first line of file.
- `G`—Move to the last line of file.

以下是为您翻译的中文内容：

## 开始使用 vi

大多数情况下，你启动 `vi` 是为了打开一个特定的文件。例如，要打开名为 `/tmp/test` 的文件，输入以下命令：

```bash
```
