

现在我输入 $ 来移动到行尾：

Click here to view code image

```
total 29
drwx-- 2 taylor 512 Nov 21 10:39 Archives/
drwx-- 3 taylor 512 Dec 3 02:03 InfoWorld/
drwx-- 2 taylor 1024 Dec 3 01:43 Mail/
```

5. 如果你的键盘上有方向键，试着使用它们看看它们是否与 h、j、k 和 l 键的工作方式相同。如果方向键不能移动光标，它们可能已将你切换到插入模式。如果你输入字符并且它们被添加到文件中，请按下 Escape 键（或 Esc，取决于你的键盘）以返回到命令模式。

6. 让我们通过退出本次编辑会话来结束。 因为 vi 现在知道你已修改了文件，它会尝试确保你在未保存更改的情况下不会退出：

Click here to view code image

```
~
~
:q
No write since last change (:quit! overrides)
```

使用 :q!（:quit 的简写，丢弃你所做的任何更改，这就是 ! 的含义）来在不保存更改的情况下退出。

## Note

通常，如果你在 vi 中尝试使用冒号命令并且程序抱怨它可能会做坏事，请停止并确保这真的是你想要做的。如果是，请再次输入该命令，后面加上感叹号。我喜欢把这想成是说，“不管怎样就做吧！”

如果你愿意，可以在下一个任务中继续使用此文件，也可以输入 :q 退出。

使用这六个简单的键命令在文件中移动，在小范围内与使用 vi 编辑器处理文件时的整个过程非常相似。在你对移动感到舒适之前坚持使用这些简单命令，你就将在熟练使用 vi 的道路上迈出很大一步。

## Task 10.3: Moving by Words and Pages

早些时候，在描述 emacs 编辑器时，我评论说因为 emacs 始终处于插入模式，所有命令都必须包含 Control 键。好吧，原来 vi 也有其份额的 Control 键命令——需要你按住 Control 键并按下另一个键的命令。在本节中，你将学习关于 Ctrl-f、Ctrl-b、Ctrl-u 和 Ctrl-d。这些命令分别向前或向后移动一屏，以及向上或向下移动半屏文本。

我还会加入几个命令：w 将你向前逐词移动，b 将你向后逐词移动，而这两个命令的大写版本

具有非常相似但不完全相同的功能。（没错——vi 会区分你在输入键盘命令时是否按住 Shift。所以 A 命令与 a 不同。）

- 1. 要了解其工作原理，你需要创建一个比屏幕尺寸更长的文件。一种简单的方法是反复将常用命令的输出保存到一个文件，直到文件足够长。我使用的系统有很多用户，所以我只需使用 who 命令一次即可创建文件。你可能需要将 who 的输出追加到 big.output 文件几次，直到文件长度超过 24 行。（当然，你可以使用 wc 来检查。）

Click here to view code image

```
% who > big.output; wc -l big.output
40
% vi big.output
```

![](img/036fe100817eada43c999b050270081b_185_0.png)

因为我只有 25 行的显示，而输出有 40 行长（你可以在底部的状态行看到），该文件中的信息比屏幕一次能显示的更多。

- 2. 要查看下一屏，按下 Ctrl-f。当我这样做时，我得到以下输出：

Click here to view code image

![](img/036fe100817eada43c999b050270081b_185_1.png)

```
doerrhb ttysp  Dec  3 23:20  (dov)
cdemmert ttysq  Dec  3 23:00  (xsun22)
frazierw ttysr  Dec  3 23:01  (dov)
buckeye ttys s  Dec  3 23:20  (mac2)
mtaylor ttyst  Dec  3 23:22  (dov)
look ttysu  Dec  3 23:12  (age)
janitor ttysw  Dec  3 18:29  (age)
ajones ttysx  Dec  3 23:23  (rass)
~
~
~
~
```

请注意整个屏幕被重写，并且熟悉的波浪号字符再次出现，让我知道我已到达文件末尾。

默认情况下，vi 在从一屏移动到另一屏时有两行的重叠。如果你仔细看，可以看到 eichsted 和 sweett 同时出现在两屏数据中。这并不意味着它们在文件中出现两次；相反，vi 试图帮助我在文件中游走时不迷路。

# 3. 现在，你认为如果我按下 Ctrl-u 会发生什么？

Click here to view code image

```
leungtc ttys0  Nov 28 15:11  (gold)
chinese ttys2  Dec  3 22:53  (excalibur)
cdemmert ttys5  Dec  3 23:00  (mentor)
yuenca ttys6  Dec  3 23:00  (mentor)
janitor ttys7  Dec  3 18:18  (age)
mathisbp ttys8  Dec  3 23:17  (dov)
janitor ttys9  Dec  3 18:18  (age)
cs541 ttysC  Dec  2 15:16  (solaria)
yansong ttysL  Dec  1 14:44  (math)
mdps ttysO  Nov 30 19:39  (localhost)
md ttysU  Dec  2 08:45  (muller)
jac ttysa  Dec  3 18:18  (localhost)
eichsted ttysb  Dec  3 23:21  (pcl)
sweett ttysc  Dec  3 22:40  (dov)
wellman ttysd  Dec  3 23:01  (dov)
tuttleno ttys e  Dec  3 23:03  (indy vax)
wu ttysf  Dec  3 23:10  (term01)
daurismj ttysg  Dec  3 23:10  (dov)
cs414 ttysh  Dec  3 23:12  (xds)
cq ttysi  Dec  3 23:13  (expert)
cdemmert ttysk  Dec  3 22:37  (xsun22)
jrlee ttysn  Dec  3 22:53  (mac1)
fitzgejs ttyso  Dec  3 23:18  (dov)
```

该命令将我向上移动了半屏。请注意 eichsted 和 sweett 的位置。现在文本不是像使用 Ctrl-f 时那样一次性被替换，而是逐行向下滚动，每行新内容在程序进行时被添加。Ctrl-u 命令对你来说可能以两种方式工作——一次一行或一整屏。

# 4. 现在是时候尝试逐词在文件中移动了。输入 w 键一次看看会发生什么：

Click here to view code image

```
leungtc ttys0  Nov 28 15:11  (gold)
```

