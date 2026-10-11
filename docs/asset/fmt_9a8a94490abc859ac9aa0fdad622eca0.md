
要在缓冲区区域内移动光标，你可以使用箭头键和 `PageUp` 和 `PageDown` 键，假设 Emacs 正确检测到了你的终端仿真器。如果没有，这些命令可以移动光标：

- `C-p` 向上移动一行（文本中的上一行）。
- `C-b` 向左（向后）移动一个字符。
- `C-f` 向右（向前）移动一个字符。
- `C-n` 向下移动一行（文本中的下一行）。

以下命令在文本中做出更长的跳转：

- `M-f` 向右（向前）移动到下一个单词。
- `M-b` 向左（向后）移动到上一个单词。
- `C-a` 移动到当前行的开头。
- `C-e` 移动到当前行的末尾。
- `M-a` 移动到当前句子的开头。
- `M-e` 移动到当前句子的末尾。
- `M-v` 向后移动一屏数据。
- `C-v` 向前移动一屏数据。
- `M-<` 移动到文本的第一行。
- `M->` 移动到文本的最后一行。

你应该知道这些命令，用于将编辑器缓冲区保存回文件并退出 Emacs：

- `C-x C-s` 将当前缓冲区内容保存到文件。
- `C-z` 退出 Emacs，但保持其在当前会话中运行，以便你稍后返回。
- `C-x C-c` 退出 Emacs 并停止该程序。

你会注意到，其中两个功能需要两个按键组合。`C-x` 命令被称为扩展命令。这提供了另一整套可供操作的命令。

### 编辑数据

Emacs 编辑器在缓冲区中插入和删除文本方面相当健壮。要插入文本，只需将光标移动到你要插入文本的位置，然后开始输入。

要删除文本，Emacs 使用 `Backspace` 键删除当前光标位置之前的字符，并使用 `Delete` 键删除当前光标位置处的字符。

Emacs 编辑器还有用于剪切文本的命令。Emacs 文档将此称为“kill（杀戮/清除）”文本，但我们这里将使用更友好的“剪切”术语。

删除文本和剪切文本的区别在于，当你剪切文本时，Emacs 会将其放置在一个临时区域，你可以从中恢复它（参见下一节“复制和粘贴”）。删除的文本则永远消失。

这些命令用于剪切缓冲区中的文本：

- `M-Backspace` 剪切当前光标位置之前的单词。
- `M-d` 剪切当前光标位置之后的单词。
- `C-k` 剪切从当前光标位置到行尾的文本。
- `M-k` 剪切从当前光标位置到句子末尾的文本。

> **提示**
>
> 如果你在剪切文本时不小心犯了错，`C-/` 命令可以撤销剪切操作，并将数据恢复到剪切前的状态。

Emacs 编辑器还包含一种批量剪切文本的便捷方式。只需将光标移动到你想要切起始位置，然后按下 `C-@` 或 `C-空格` 键。接着，将光标移动到你想要切结束的位置，并输入 `c-w`。两个位置之间的所有文本都会被剪切。

### 复制和粘贴

你已经了解了如何从 Emacs 缓冲区区域剪切数据；现在该看看如何将其粘贴到其他位置了。不幸的是，如果你使用 vim 编辑器，当使用 Emacs 编辑器时，这个过程可能会让你困惑。

在一个不幸的巧合中，Emacs 中的粘贴操作被称为 *yanking（拖拽/抓取）*。而在 vim 编辑器中，复制也被称为 yanking，这使得如果你同时使用这两种编辑器，这就成了很难记住的事情。

在使用其中一个剪切命令剪切数据后，将光标移动到你想要粘贴数据的位置，并使用 `c-y` 命令。这将把文本从临时区域取出并粘贴到当前光标位置。`c-y` 命令会抓取最后一次剪切命令的文本。如果你执行了多个剪切命令，可以使用 `M-y` 命令在它们之间循环切换。

要复制文本，只需将其从剪切的位置反向抓取（yank）回来，然后移动到新位置并再次使用 `c-y` 命令。你可以将文本抓取回来任意多次。

### 搜索和替换

在 Emacs 编辑器中搜索文本是使用 `c-s` 和 `c-r` 命令完成的。`c-s` 命令在缓冲区区域中从当前光标位置到缓冲区末尾执行向前搜索，而 `c-r` 命令在缓冲区区域中从当前光标位置到缓冲区开头执行向后搜索。

当你输入 `c-s` 或 `c-r` 命令时，底部行会出现一个提示，询问你要搜索的文本。你可以执行两种类型的搜索。

在 *增量* 搜索中，Emacs 编辑器以实时模式执行文本搜索，随着你输入单词进行搜索。当你输入第一个字母时，它会突出显示缓冲区中该字母的所有出现位置。当你输入第二个字母时，它会突出显示文本中这两个字母组合的所有出现位置，依此类推，直到你完成要搜索的文本。

在 *非增量* 搜索中，在 `C-s` 或 `C-r` 命令后按下 `Enter` 键。这将搜索查询锁定在底部行区域，允许你在搜索之前完整输入搜索文本。

要将现有文本字符串替换为新的文本字符串，你必须使用 `M-x` 命令。该命令需要文本命令以及参数。

文本命令是 `replace-string`。输入命令后，按下 `Enter` 键，Emacs 会询问你现有的文本字符串。输入后，再次按下 `Enter` 键，Emacs 会询问你新的替换文本字符串。

### 在 Emacs 中使用缓冲区

Emacs 编辑器允许通过拥有多个缓冲区区域来同时编辑多个文件。你可以将文件加载到缓冲区中，并在编辑时在缓冲区之间切换。

要在 Emacs 中加载新文件到缓冲区，请使用 `C-x C-f` 命令。这是 Emacs 的查找文件模式，称为 *Dired*。它会带你进入窗口底部行，允许你输入想要开始编辑的文件名。如果你不知道文件名或位置，只需按下 `Enter` 键。这会在编辑窗口中调出一个文件浏览器，如图 10-4 所示。

```
File Edit Options Buffers Tools Operate Mark Regex Immediate Subdir Help 
/home/christine:
total used in directory 120 available 11645800
drwxr-xr-x 17 christine christine 4096 May 8 16:05 .
drwxr-xr-x 4 root root 4096 Apr 23 15:12 ..
-FW------- 1 christine christine 828 May 8 14:11 .bash_history
-FW------- 1 christine christine 220 Feb 25 07:03 .bash_logout
-FW------- 1 christine christine 3782 May 7 13:55 .bashrc
drwx------ 14 christine christine 4096 May 1 15:14 .cache
drwxr-xr-x 13 christine christine 4096 May 1 15:06 .config
drwxr-xr-x 2 christine christine 4096 Apr 23 15:13 Desktop
drwxr-xr-x 2 christine christine 4096 Apr 23 15:13 Documents
drwxr-xr-x 2 christine christine 4096 Apr 23 15:13 Downloads
drwx------ 3 christine christine 4096 May 8 15:35 .local
drwx------ 3 christine christine 4096 May 2 15:35 .gnupg
drwx------ 3 christine christine 4096 Apr 23 15:13 .mozilla
drwxr-xr-x 2 christine christine 4096 May 1 15:14 Music
-rwxrwxr-x 1 christine christine 16688 May 7 14:26 myprog
-FW-FW-r-- 1 christine christine 248 May 8 16:05 myprog.c#
lrwxrwxrwx 1 christine christine 34 May 8 16:03 .#myprog.c -> christine\
@UDesktop:3662:1589892380
-FW-FW-r-- 1 christine christine 248 May 8 11:11 myprog.c
-FW------- 20 christine christine 807 Feb 23 14:29 myprog.c.save
drwxr-xr-x 2 christine christine 4096 May 8 15:13 Pictures
-FW------- 1 christine christine 807 Feb 25 07:03 .profile
drwxr-xr-x 2 christine christine 4096 May 8 15:13 Public
-UUU:%*-F1 christine Top L3 (dir by name) -------------------
```

**图 10-4** Emacs 文件浏览器

从这里，你可以浏览到你要编辑的文件。要向上遍历一层目录，移动到双点条目并按下 `Enter` 键。要向下遍历目录，移动到目录条目并按下 `Enter` 键。当你找到要编辑的文件时，按下 `Enter`，Emacs 会将其加载到一个新的缓冲区区域中。
