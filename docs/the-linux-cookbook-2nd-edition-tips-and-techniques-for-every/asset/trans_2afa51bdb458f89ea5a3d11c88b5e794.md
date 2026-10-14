

+   • 在 X 中运行 Emacs 时，要将其图标化，输入：
+     ⟨CTRL⟩-⟨Z⟩

## 10.1.2 运行 Emacs 教程

Emacs 附带一个交互式、自定进度的教程，可教你如何使用基础功能。根据我的经验，花 25 分钟完成该教程是你计算生涯中可以做的最好的事情之一。即使你最终决定不太喜欢 Emacs，[content]

+   • 在 X 中运行 Emacs 时，要将其图标化，输入：
+     ⟨CTRL⟩-⟨Z⟩

## 10.1.2 运行 Emacs 教程

Emacs 附带一个交互式、自定进度的教程，可教你如何使用基础功能。根据我的经验，花 25 分钟完成该教程是你计算生涯中可以做的最好的事情之一。即使你最终决定不太喜欢 Emacs，许许多多其他应用程序都使用 Emacs 风格的键盘命令和启发式方法，因此熟悉它们总是有回报的。任何时候，只要你在 Emacs 中，都可以使用 ⟨CTRL⟩-⟨H⟩ t 命令启动教程。

⇒ 要启动 Emacs 教程，输入：
  ⟨CTRL⟩-⟨H⟩ t

该命令会打开教程，一个特殊的只读文件，放入其自己的缓冲区中。

NOTES：顺便说一下，⟨CTRL⟩-⟨H⟩ 是 Emacs 的帮助键；所有与帮助相关的命令都以此键开头。例如，要阅读 Emacs FAQ，输入 ⟨CTRL⟩-⟨H⟩ F，要运行 Info 文档浏览器（其中包含《GNU Emacs 手册》），输入 ⟨CTRL⟩-⟨H⟩ i。

## 10.1.3 使用基本的 Emacs 编辑键

你在 Emacs 中输入的任何内容都称为键序列，当你输入一个绑定到命令的序列时，它会运行该命令。

下表列出了基本编辑键并描述了其功能。如果某个功能有两种常见的按键，两者都会给出。

### Moving Point
⟨↑⟩ or ⟨CTRL⟩-⟨P⟩    将光标上移至上一行。
⟨↓⟩ or ⟨CTRL⟩-⟨N⟩    将光标下移至下一行。
⟨←⟩ or ⟨CTRL⟩-⟨B⟩    将光标向后（向左）移动一个字符。
⟨→⟩ or ⟨CTRL⟩-⟨F⟩    将光标向前（向右）移动一个字符。
⟨ALT⟩-⟨F⟩            将光标向前移动一个词。

ALT - ←
将光标向后移动一个词。

ALT - ↑
将光标移回下一个段落开头。

ALT - ↓
将光标向前移动到下一个段落结尾。

PgUp or CTRL - V
将光标向前通过缓冲区移动一屏。

PgDn or ALT - V
将光标向后通过缓冲区移动一屏。

CTRL - A
将光标移动到当前行的开头。

CTRL - E
将光标移动到当前行的末尾。

CTRL - L
重新居中 Emacs 窗口中的文本，将光标所在的行置于屏幕中央。

### Inserting and Deleting

INS
切换覆盖模式。

CTRL - T
交换光标处的字符与光标左侧的字符。

ALT - T
交换光标处的词与光标左侧的词。

BKSP or CTRL - H
删除光标左侧的字符。

DEL or CTRL - D
删除光标右侧的字符。

### Cutting and Pasting

SHIFT - INS or CTRL - Y
在光标处粘贴剪贴环中的文本（参见 Recipe 10.3.2 [Pasting Text], page 254）。

CTRL - SPACEBAR
设置标记（参见 Recipe 10.3.1 [Cutting Text], page 254）。

CTRL - _
撤销上一个操作（control-underscore）。

CTRL - K
从光标处杀死文本到行尾。

CTRL - W
从标记处杀死文本到光标处。

### Getting Help

CTRL-(H) t  启动 Emacs 教程。

CTRL-(H) k keystroke  描述按键。

CTRL-(H) a function RET  列出与函数相关的所有 Emacs 命令。

CTRL-(H) F  在新缓冲区中打开 Emacs FAQ 的副本。

CTRL-(H) i  启动 Info。

### Command Operations

CTRL-(G)  取消当前命令。

CTRL-(U) number  重复你接下来输入的命令或按键 number 次。

### File Operations

CTRL-(X) CTRL-(C)  保存 Emacs 中打开的所有缓冲区，然后退出程序。

CTRL-(X) CTRL-(F) file RET  在新缓冲区中打开文件进行编辑。要创建尚不存在的新文件，只需指定你想要的文件名。要浏览你的文件，输入 TAB 而不是文件名。

### Special Menus

CTRL-left-click  显示按主要模式排序的所有打开缓冲区的菜单（仅在 X 中有效）。

SHIFT-left-click  显示字体选择菜单（仅在 X 中有效）。

## 10.1.4 在 Emacs 中插入特殊字符

有些字符你不能正常地输入到 Emacs 缓冲区中。例如，在文本文件中，你可以通过插入换页字符，即 ASCII CTRL-(L) 或八进制代码 014 来指定分页；当你打印带有换页符的文件时，当前页会在此字符处被弹出，打印将在新页上继续。

然而，CTRL-(L) 作为 Emacs 命令有其含义。要插入此类字符，请使用 quoted-insert 函数，CTRL-(Q)。它接受你想要插入的字符的字面按键，或该字符的八进制代码。它在光标处插入字符。

