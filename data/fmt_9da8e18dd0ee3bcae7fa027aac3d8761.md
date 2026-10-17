
```
# cat LICENSE
...
1. You may make and give away verbatim copies of the source form of the Standard Version of this Package without restriction, provided that you duplicate all of the original copyright notices and associated disclaimers.

2. You may apply bug fixes, portability fixes and other modifications derived from the Public Domain or from the Copyright Holder. A Package modified in such a way shall still be considered the Standard Version.
...
```

屏幕或默认 `pr` 下可能正常，但左边界 10 空格时会超行：

```
# pr -o 10 <LICENSE
...
1. You may make and give away verbatim copies of the source fo
rm of the
Standard Version of this Package without restriction, provided
that you
duplicate all of the original copyright notices and associated
disclaimers.
2. You may apply bug fixes, portability fixes and other modifi
cations
Package derived from the Public Domain or from the Copyright Holder. A
version modified in such a way shall still be considered the Standard V
ersion.
...
```

打印效果不佳。可先用 `fmt` 缩小行宽再用 `pr` 格式化：

```
# cat LICENSE | fmt -w 60 | pr -o 10
```

+   1. You may make and give away verbatim copies of the source form of the Standard Version of this Package without restriction, provided that you duplicate all of the original copyright notices and associated disclaimers.

+   2. You may apply bug fixes, portability fixes and other modifications derived from the Public Domain or from the Copyright Holder. A Package modified in such a way shall still be considered the Standard Version.

+   ...

文本现已合适。也可将 `fmt` 输出与 `pr` 的多列选项结合。例如对 `pilotprimer.txt`，先用 `fmt` 格式化为 26 字符窄列，再用 `pr` 生成多列：

```
# fmt -26 <pilotprimer.txt | pr -2 -s\| -o 2 -t -w 60
```

| HACKING THE 3COM PALM

PILOT PERSONAL DIGITAL

ASSISTANT

Although most manufacturers tout their brand of Personal Digital Assistant, or PDA, as the 'easiest to use,' or most 'convenient' device, when it comes to connecting to the Internet, novice PDA and Internet users may still have a hard time in making that first connection to | Information You Need

to Connect

There are several things you need to know before you can starting web browsing, Usenet news reading, or sending and receiving email on your Pilot. When you signed up for your Internet service, you should have received an information packet from your ISP. This information should include: |

未显示全部输出，但可看出 `fmt` 将文本流转为 26 字符宽列，再由 `pr` 格式化为两列。`-s` 后接 `\` 和 `|` 指定竖线为列分隔符，`-o` 设左边界为两空格，`-t` 关闭页眉页脚，`-w 60` 设页宽 60 字符，适合大多数打印机。

若想省纸在一页显示至少两页，可用 `mpage` 将多页打印在一页：

```
# mpage -2 myfile.txt >myfile.ps
```

该命令用 `/usr/bin` 下的 `mpage` 创建 PostScript 文件，将 `myfile.txt` 内容以每页两页并排形式输出。X11 下可用 `gv` 预览：

```
# gv myfile.ps
```

![](img/b5a8a94bdbf7778e1f1f2a5ed6c74e27_363_0.png)

> `mpage` 的 `-O`、`-E` 或 `-R` 选项可打印双面文档，方便制作小册子。也可设置不同边距、字体及页序，详见 `mpage` 手册页。

结合 `fmt`、`pr` 或 `mpage` 及其他文本过滤器，可进行快速粗略的文本排版。若需更复杂排版，可使用文本格式化程序。

## 使用 groff 格式化文本

使用 OpenLinux 数小时并阅读过手册页后，您可能已熟悉一个复杂格式化程序：`groff`。用

```
# man ls
```

阅读手册页等价于：

```
# nroff -man /usr/man/man1/ls.1 | less
```

## 新术语

请注意，在命令行上使用的是 `nroff` 命令而不是 `groff`。这是因为系统上安装的 `nroff` 命令是一个 shell 脚本，其编写目的是使用 GNU `groff` 格式化程序来模拟 `nroff` 命令。所有 OpenLinux 手册页都是使用一组特殊的 `nroff` 命令编写的，称为 `man` 宏。你可以使用 `groff` 命令使用 `man` 宏来格式化自己的手册页。例如，如果你为一个名为 `nw` 的新游戏创建手册页，名为 `nw.6` 的手册页可能如下所示：

```
.TH Nano-Warrior 6 Games 1/1/98 Linux
.SH NAME
nw - play Nano-Warrior
.SH SYNOPSIS
nw
.B -d
.PP
-d = play deathmatch mode
.SH DESCRIPTION
.PP
The nw command is used to play a game of Nano-Warrior on your Linux console. Play continues until you are wiped out by hordes of alien invaders swarming down the screen.
.PP
Don't give up the fight!
.SH FILES
/usr/games/nw
.PP
$HOME/.nw_scores
.SH BUGS
Probably too many.
```

你可以用以下命令处理此手册页并将其发送到显示器：

```
# groff -Tascii -man nw.6
```
