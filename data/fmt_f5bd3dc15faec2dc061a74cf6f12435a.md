
以通常的方式启动 Emacs，要么在 X 中从窗口管理器提供的菜单中选择它，要么在 shell 提示符下输入其名称（小写字母）。

- 要在 shell 提示符下启动 GNU Emacs，输入：

```
$ emacs RET
```

- 要在 shell 提示符下启动 XEmacs，输入：

## Linux 实用手册：日常使用的技巧与方法：

```
$ xemacs RET
```

在 X 中启动时，典型的 GNU Emacs 窗口看起来像这样（窗口框架会根据你的窗口管理器而有所不同）：

![](img/8bf3d083d04b4cc3d79bd39657ac711a_167_0.png)

欢迎信息在 Emacs 第一次启动时出现，其中告诉你其他信息，例如如何运行教程（我们马上就会看到）。

顶部栏称为菜单栏，你可以通过鼠标左键单击菜单然后向下拖动来展开其菜单。当你在控制台中运行 Emacs 时，不能使用鼠标下拉菜单，但你可以通过输入 `F10` 在文本菜单中访问并选择相同的菜单项。`(17)`

在 Emacs 中打开的文件或其他文本都保存在各自的区域中，称为 `*buffer*`。默认情况下，当前缓冲区显示在菜单栏下方的较大区域中。要在缓冲区中写文本，只需输入即可。缓冲区中光标所在的位置称为 `*point*`，许多 Emacs 命令都会引用它。

Emacs 窗口底部附近、当前缓冲区正下方的水平栏称为 `*mode line*`；它提供有关当前缓冲区的信息，包括其名称、多少百分比的缓冲区适合屏幕、`point` 位于哪一行，以及缓冲区是否已保存到文件中。

`mode line` 还列出缓冲区中激活的模式。Emacs 的 `*modes*` 是控制 Emacs 行为的一般状态——例如，当 `*Overwrite*` 模式被设置时，你输入的文本会 `*overwrites*` `point` 处的文本；在 `*Insert*` 模式（默认）下，你输入的文本会在 `point` 处 `*inserted*`。通常会列出 `*Fundamental*` 模式（默认）或 `*Text*` 模式。

你可以通过切换 `*Menu bar*` 模式来使菜单栏出现或消失。输入 `F10` 以激活菜单下拉功能，无论 `*Menu bar*` 模式是否开启都有效；如果关闭，菜单选项将出现在新的缓冲区窗口中。

- 要关闭顶部的菜单栏，输入：

```
M-x menu-bar-mode RET
```

（如果菜单栏已关闭，此命令会将其打开。）

`*echo area*` 是 Emacs 写入简短状态消息的地方，例如错误消息；它是 Emacs 窗口的最后一行。当你输入需要输入的命令时，该输入会在此区域请求（此时你在 `echo area` 中输入的位置称为 `*minibuffer*`）。

Emacs 命令通常以 Control 或 Meta（Escape）键序列开头；许多命令以 `C-x` 序列开头，你可以通过按住 `CTRL` 键然后按下 `X` 键来输入（参见章节 `*Typographical Conventions*`）。

由于 Emacs 在文化上与 Microsoft Windows 和 Apple MacOS 世界的编辑器和操作方法不同，它在那些领域中获得了相当不合理的声誉，认为它很奇怪且难以使用。事实并非如此。运行其各种功能的键盘命令是为易用性和易于回忆而设计的。

例如，`*find-file*` 函数会提示输入文件名并在新缓冲区中打开文件的副本；其键盘快捷键是 `C-x C-f`（你可以在按住 `CTRL` 的同时按下并释放 `X` 和 `F` 键）。

你可以通过输入 `M-x` 然后输入函数名并按下 `RET` 来运行任何 Emacs 函数。

- 要运行 `*find-file*` 函数，输入：

```
M-x find-file RET
```

此命令运行 `*find-file*` 函数，该函数会提示输入文件名并在新缓冲区中打开文件的副本。

在 Emacs 中输入 `C-g` 可退出某个函数或命令；如果你在输入命令时出错，这对于取消和中止键盘输入非常有用。

现在我们已经介绍了基本的 Emacs 术语，我将向你展示如何退出程序——只需输入 `C-x C-c`。

Emacs 可以同时打开多个缓冲区。要在缓冲区之间切换，输入 `C-x C-b`。然后，输入要切换到的缓冲区的名称，后跟 `RET`；或者，不带缓冲区名称输入 `RET` 以切换到上次访问的缓冲区。（在 Emacs 中查看缓冲区称为访问缓冲区。）

- 要切换到名为 `rolo` 的缓冲区，输入：

```
C-x C-b rolo RET
```

一个特殊的缓冲区称为 `*scratch*`，用于笔记和你不想保存的内容；它始终存在于 Emacs 中。

- 要切换到 `*scratch*` 缓冲区，输入：

```
C-x C-b *scratch* RET
```

作为参数传递给 `emacs` 的任何文件名都将在单独的缓冲区中打开：

```
$ emacs todo rolo /usr/local/src/nirvarna/README RET
```

（当然，你也可以稍后创建新缓冲区并在其中打开文件。）

Emacs 附带一个交互式、自定进度的教程，可教你如何使用基础知识。根据我的经验，花 25 分钟时间完成教程是你计算生涯中可以做的最好的事情之一——即使你决定自己不太喜欢 Emacs，也有很多其他应用程序使用 Emacs 风格的键盘命令和启发式方法，因此熟悉它们总是有回报的。

要在 Emacs 中随时启动教程，输入 `C-h t`。

顺便说一下，`C-h` 是 Emacs 的帮助键；所有帮助相关命令都以此键开头。例如，要阅读 Emacs FAQ，输入 `C-h F`，要运行 Info 文档浏览器（其中包含 The GNU Emacs Manual），输入 `C-h i`。

### 11.2.2 基本 Emacs 编辑键

下表列出了基本编辑键并描述了其功能。如果某个功能有两种常用的按键，两者都会给出。

| KEYS | DESCRIPTION |
|---|---|
| @uparrow or C-p | 将光标上移至上一行。 [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| @downarrow or C-n | 将光标下移至下一行。 [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| @leftarrow or C-b | 将光标在缓冲区中向左移动一个字符。 [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| @rightarrow or C-f | 将光标在缓冲区中向右移动一个字符。 [GNU INFO BUG: any <> in the preceding line should be the one of the cursor arrow keys.] |
| PgUp or C-v | 将光标在缓冲区中向前移动一屏。 |
| PgDn or M-v | 将光标在缓冲区中向后移动一屏。 |
| BKSP or C-h | 删除光标左侧的字符。 |
| DEL or C-d | 删除光标右侧的字符。 |
| INS | 在插入模式和覆盖模式之间切换。 |
| Shift-INS or C-y | 在光标处粘贴剪贴环中的文本（参见 Pasting Text 部分）。 |
| C-SPC | 设置标记（参见 Cutting Text 部分）。 |
| C-_ | 撤销上一个操作（control-underscore）。 |
| C-a | 将光标移动到当前行的开头。 |
| C-e | 将光标移动到当前行的末尾。 |
| C-g | 取消当前命令。 |
| C-h F | 在新缓冲区中打开一份 Emacs FAQ 副本。 |
| C-h a function RET | 列出与该函数相关的所有 Emacs 命令。 |
| C-h i | 启动 Info。 |
| C-h k key | 描述按键。 |
| C-h t | 启动 Emacs 教程。 |
| C-k | 从光标处删除文本至行尾。 |
| C-l | 重新居中 Emacs 窗口中的文本，将光标所在行置于屏幕中央。 |
| C-t | 将光标处的字符与光标左侧的字符互换。 |
| C-u number | 重复你接下来输入的命令或按键 number 次。 |
| C-w | 从标记处删除文本至光标处。 |
| C-x C-c | 保存 Emacs 中打开的所有缓冲区，然后退出程序。 |
| C-x C-f file RET | 在新缓冲区中打开文件进行编辑。若要创建尚不存在的新文件，只需指定你想要的文件名。若要浏览文件，输入 TAB 而不是文件名。 |
| C-left-click | 显示按主要模式排序的所有打开缓冲区的菜单（仅在 X 下有效）。 |
