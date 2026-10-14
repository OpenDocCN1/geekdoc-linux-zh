
February 2012
Su Mo Tu We Th Fr Sa
1 2 3 4
5 6 7 8 9 10 11
12 13 14 15 16 17 18
19 20 21 22 23 24 25
26 27 28 29

首次， unquoted 的命令替换导致命令行包含 38 个参数；在第二次， 结果是包含嵌入空格和换行的 1 个参数的命令行。

## Single Quotes

如果我们需要抑制所有展开，我们使用单引号。以下是未加引号、双引号和单引号的比较：

```
[me@linuxbox ~]$ echo text "/*.txt {a,b} $(echo foo) $((2+2)) $USER
text /home/me/is-output.txt a b foo 4 me
[me@linuxbox ~]$ echo text "/*.txt {a,b} $(echo foo) $((2+2)) $USER"
text /*.txt {a,b} foo 4 me
[me@linuxbox ~]$ echo text '/*.txt {a,b} $(echo foo) $((2+2)) $USER'
text /*.txt {a,b} $(echo foo) $((2+2)) $USER
```

正如我们所见，随着引号层级的增加，越来越多的展开被抑制。

## Escaping Characters

有时我们只想引用单个字符。为此，我们可以在字符前加上反斜杠，在此上下文中称为转义字符。通常这是在双引号内完成，以有选择地阻止展开。

```
[me@linuxbox ~]$ echo "The balance for user $USER is: \$5.00"
The balance for user me is: $5.00
```

使用转义来消除文件名中字符的特殊含义也很常见。例如，可以在文件名中使用 shell 通常赋予特殊含义的字符。这些包括 $、!、&、（空格）等。要在文件名中包含特殊字符，可以这样做：

```
[me@linuxbox ~]$ mv bad\&filename good_filename
```

要允许反斜杠字符出现，请通过输入 \\ 来转义它。注意，在单引号内，反斜杠会失去其特殊含义并被视为普通字符。

## BACKSLASH ESCAPE SEQUENCES

除了作为转义字符的作用外，反斜杠还被用作表示某些称为控制码的特殊字符的记法的组成部分。ASCII 编码方案中的前 32 个字符用于向电传打字机类设备传输命令。其中一些代码我们很熟悉（制表符、退格、换行符和回车符），而其他代码则不熟悉（空字符、传输结束和确认），如表 7-2 所示。

## Table 7-2: Backslash Escape Sequences

| Escape Sequence | Meaning |
|---|---|
| \a | Bell ("alert"—causes the computer to beep) |
| \b | Backspace |
| \n | Newline (on Unix-like systems, this produces a linefeed) |
| \r | Carriage return |
| \t | Tab |

本表列出了一些常见的反斜杠转义序列。使用反斜杠的想法起源于 C 编程语言，并已被许多其他语言采用，包括 shell。

为 echo 添加 -e 选项将启用对转义序列的解释。你也可以将它们放在 $' ' 内。在这里，使用 sleep 命令，一个简单的程序，只等待指定的秒数然后退出，我们可以创建一个原始的倒计时器。

```
sleep 10; echo -e "Time's up\a"
```

我们也可以这样做：

```
sleep 10; echo "Time's up" $'\a'
```

## Final Note

随着我们继续使用 shell，我们会发现展开和引用会以越来越高的频率使用，因此了解它们的工作方式是有意义的。事实上，可以说它们是关于 shell 最重要的学习主题。如果没有对展开的正确理解，shell 将始终是神秘和困惑的来源，其大部分潜在威力将被浪费。

## 8

## ADVANCED KEYBOARD TRICKS

我经常开玩笑地描述 Unix 为“喜欢打字的人的操作系统”。当然，它甚至拥有命令行就证明了这一点。但命令行用户并不喜欢打太多字。否则为什么会有这么多命令的名字如此简短，比如 cp、ls、mv 和 rm？

事实上，命令行最珍视的目标之一就是懒惰——用最少的击键完成最多的工作。另一个目标是永远不必把手指从键盘上抬起——永远不要去够鼠标。在本章中，我们将介绍使键盘使用更快、更高效的 bash 功能。

以下命令将会出现：

- clear—Clear the screen.
- history—Display the contents of the history list.
