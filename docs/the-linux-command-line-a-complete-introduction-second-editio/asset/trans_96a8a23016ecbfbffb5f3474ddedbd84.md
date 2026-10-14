

不同的 Linux 发行版以不同的方式打包 vim。某些发行版默认安装的是 vim 的精简版本，仅支持有限的 vim 功能。在进行接下来的练习时，你可能会遇到缺少功能的情况。如果是这样，请安装 vim 的完整版本。

就像我们之前对 nano 所做的那样，首先要学习的是如何退出。要退出，我们输入以下命令（注意冒号字符是命令的一部分）：

```
:q
```

shell 提示符应该返回。如果由于某种原因 vi 无法退出（通常是因为我们对尚未保存的文件进行了更改），我们可以通过在命令后加上感叹号来告诉 vi 我们是认真的。

```
:q!
```

TIP
如果你在 vi 中“迷路”了，试着按两次 ESC 键来重新找到方向。

## 编辑模式

让我们再次启动 vi，这次向它传递一个不存在的文件名。这就是我们如何使用 vi 创建新文件的方法：

```
[me@linuxbox ~]$ rm -f foo.txt
[me@linuxbox ~]$ vi foo.txt
```

如果一切顺利，我们应该会看到如下屏幕：

```
~
~
```

![](img/314a0280bc10c5c0d45be132de172677_195_0.png)

前导的波浪号字符（~）表示该行上不存在文本。这表明我们有一个空文件。暂时不要输入任何内容！

关于 vi 最重要的第二件事需要学习（在学会如何退出之后）是 vi 是一个*模式编辑器*。当 vi 启动时，它开始于*命令模式*。在此模式下，几乎每个键都是一个命令，因此如果我们开始输入，vi 基本上会发疯并弄出一大堆混乱。

## 进入插入模式

要向我们的文件添加一些文本，我们必须首先进入*插入模式*。为此，我们按下 i 键。之后，如果 vim 以其通常的增强模式运行，我们应该在屏幕底部看到以下内容（这在 vi 兼容模式下不会出现）：

```
-- INSERT --
```

现在我们可以输入一些文本。试试这个：

```
The quick brown fox jumped over the lazy dog.
```

要退出插入模式并返回到命令模式，请按 ESC 键。

## 保存我们的工作

要保存我们刚刚对文件所做的更改，我们必须在命令模式下输入一个 ex 命令。这很容易做到，只需按下 : 键即可。执行此操作后，冒号字符应该出现在屏幕底部。

```
:
```

要写入我们修改过的文件，我们在冒号后跟上 w 然后按 ENTER。

```
:w
```

文件将被写入硬盘，我们应该在屏幕底部看到确认消息，如下所示：

```
"foo.txt" [New] 1L, 46C written
```

TIP
如果你阅读 vi 文档，你会注意到（令人困惑的是）命令模式被称为普通模式，而 ex 命令被称为命令模式。注意这一点。

## 移动光标

在命令模式下，vi 提供了大量移动命令，其中一些与 less 共享。表 12-1 列出了其中一部分。

Table 12-1: Cursor Movement Keys

| Key | Moves the cursor |
|---|---|
| l or right arrow | Right one character. |
| h or left arrow | Left one character. |
| j or down arrow | Down one line. |
| k or up arrow | Up one line. |
| 0 (zero) | To the beginning of the current line. |
| ^ | To the first non-whitespace character on the current line. |
| $ | To the end of the current line. |
| w | To the beginning of the next word or punctuation character. |
| W | To the beginning of the next word, ignoring punctuation characters. |
| b | To the beginning of the previous word or punctuation character. |
| B | To the beginning of the previous word, ignoring punctuation characters. |
| CTRL-F or PAGE DOWN | Down one page. |
| CTRL-B or PAGE UP | Up one page. |
| numberG | To line number. For example, 1G moves to the first line of the file. |
| G | To the last line of the file. |

为什么使用 h、j、k 和 l 键进行光标移动？当 vi 最初编写时，并非所有视频终端都有方向键，而熟练的打字员可以使用常规键盘键移动光标，而无需将手指从键盘上抬起。

vi 中的许多命令都可以加上数字前缀，就像表 12-1 中列出的 G 命令一样。通过在命令前加上数字，我们可以指定命令执行的次数。例如，命令 5j 会使 vi 将光标向下移动五行。

