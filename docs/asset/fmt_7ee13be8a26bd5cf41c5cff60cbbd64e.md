
```
% alias apropos="man -k !* | uniq | grep 1"
% apropos cd
1. cd(1t) /usr/share/man/man1t/cd.1t
2. cd(1) /usr/share/man/man1/cd.1
3. cdrw(1) /usr/share/man/man1/cdrw.1
4. sound-juicer(1) /usr/share/man/man1/sound-juicer.1
6. eject(1) /usr/share/man/man1/eject.1
7. cdrecord(1) /usr/share/man/man1/cdrecord.1
10. cdda2wav(1) /usr/share/man/man1/cdda2wav.1
11. brasero(1) /usr/share/man/man1/brasero.1
12. rmmount(1m) /usr/share/man/man1m/rmmount.1m
%
```

这样好多了。

## 6. 在我结束之前，我还想查阅一个命令——`sort`：

Click here to view code image

```
% man sort

SORT(1)                                      SORT(1)

NAME
    sort - sort lines of text files
```

以及选项，或者作为一种轻松了解命令功能的方法，`man` 很棒。我鼓励你探索手册页，甚至可以阅读 `man` 命令本身的手册页。

# Task 1.2: Other Ways to Find Help in Unix

阅读手册页确实是了解 Unix 命令的最佳方式，但一些替代方法也可能有所帮助。一些系统有 `help` 命令。许多 Unix 实用程序也通过 `-h`, `-help`, 或 `-?` 标志提供信息。最后，你可以尝试向命令提供一组无意义的标志，有时这会生成错误并显示一条有用的消息，提醒你命令接受哪些可能的选项。

### 1. 在大学技术计算中心，支持团队安装了一个 `help` 命令：

Click here to view code image

```
% help
Look in a printed manual, if you can, for general help. You should have someone show you some things and then read one of the tutorial papers (e.g., UNIX for Beginners or An Introduction to the C Shell) to get started. Printed manuals covering all aspects of Unix are on sale at the bookstore.

Most of the material in the printed manuals is also available online via "man" and similar commands; for instance:
apropos keyword - lists commands relevant to keyword
whatis filename - lists commands involving filename
man command - prints out the manual entry for a command
help command - prints out the pocket guide entry for a command are helpful; other basic commands are:
cat - display a file on the screen
date - print the date and time
d u - summarize disk space usage
edit - text editor (beginner)
ex - text editor (intermediate)
finger - user information lookup program
learn - interactive self-paced tutorial on Unix
--More(40%)--
```

你的系统可能有类似的东西。然而，如果你在 HP-UX 系统上运行要小心，因为它的 `help` 命令并非旨在启发 shell 用户，而是完全做别的事情。输入 `man help` 以了解更多。

### 2. 一些命令版本如果指定 `-h` 标志会提供有用的输出：

Click here to view code image

```
% ls -h
usage: ls [ -acdfgilqr stulAC LFR ] name ...
$
```

然后又是，其他的则不会：

Click here to view code image

```
% ls -h
Global.Software   Mail/      Src/      history.usenet.Z
```

Interactive.Unix News/ bin/ testme %

在这种情况下，试试 `--help` 并祈祷好运。

少数命令在使用 `-h` 标志时会输出大量内容：

Click here to view code image

```
% elm -h
Possible Starting Arguments for ELM program:
arg          Meaning
-a           Arrow - use the arrow pointer regardless
-c           Checkalias - check the given aliases only
-dn          Debug - set debug level to 'n'
-fx          Folder - read folder 'x' rather than incoming mailbox
-h           Help - give this list of options
-k           Keypad - enable HP 2622 terminal keyboard
-K           Keypad&softkeys - enable use of softkeys + "-k"
-m           Menu - Turn off menu, using more of the screen
-sx          Subject 'x' - for batchmailing
-V           Enable sendmail voyeur mode.
-v           Print out ELM version information.
-w           Supress warning messages...
-z           Zero - don't enter ELM if no mail is pending
$
```

不幸的是，没有一个适用于所有 Unix 实用程序的通用命令标志来列出可能的命令标志。

### 3. 有时你可以通过激怒程序来获得帮助。你可以指定一组不可能的、不可用的或纯粹令人困惑的标志。我总是使用 `-xyz` 因为它们是不常见的标志：

Click here to view code image

```
% man -xyz
usage:  man [-] [-adF1prtl] [-M path] [-T macro-package ] [ -s section ] name ...
man [-M path] [-s section] -k keyword ...
man [-M path] -f file ...
man [-M path] [-s section] -K keyword ...
$
```

对于每个能做一点点有帮助事情的命令，就有半打命令会对这些标志给出无用且有趣不同的输出：

```
grep: illegal option – z
Usage: grep [-c|-l|-q] -bhinsvw pattern file …
$
%
```

你不能指望程序对它们友好，但你可以指望手册页几乎适用于系统上的所有东西。

我多么希望告诉你 Unix 内部有大量有用且有趣的信息，但实际上，Unix 只有手册页，而几乎没有其他东西。此外，本地安装的一些命令甚至可能没有手册页条目，这就让你去猜测它们的工作方式。如果你遇到未记录的命令，我建议你询问你的系统管理员或供应商发生了什么以及为什么没有关于该程序的进一步信息。

## Summary

在本第一小时中，目标是让你了解一些关于 Unix 的知识，它来自何处，以及它与你过去可能使用过的其他操作系统有何不同。你还了解了多用户系统上安全性的需求，以及密码如何帮助维护这种安全性，这样你的文件就不会被除了你之外的任何人轻易读取、更改或删除。
